<template>
  <v-container>
    <div class="home">
      <div class="imagem">
        <img class="logo" src="../assets/logo-unime-p.png" alt="Unime logo" />
      </div>
      <div class="select">
        <label for="select"><h3>Buscar pelo Estado(UF)</h3></label><br />
        <v-row>
          <v-col cols="6" class="seletor">
            <v-select
              id="select"
              :items="estados"
              item-text="state"
              label="Estados"
              clearable
              @change="estado($event)"
            >
            </v-select>
          </v-col>
        </v-row>
      </div>

      <div>
        <label><h3>Numero de casos confirmados</h3></label>
        <v-row>
          <v-col cols="6">
            <v-input> {{ this.cases }} </v-input>
          </v-col>
        </v-row>
      </div>
      <div id="dados">
        <label><h3>Numero de casos suspeitos</h3></label>
        <v-row>
          <v-col cols="6" class="susp">
            <v-input> {{ this.suspects }} </v-input>
          </v-col>
        </v-row>
      </div>
      <div>
        <label><h3>Numero de óbitos</h3></label>
        <v-row class="dados">
          <v-col cols="6">
            <v-input> {{ this.deaths }} </v-input>
          </v-col>
        </v-row>
      </div>

      <div                                                  >
        <label><h3>Casos rejeitados</h3></label>
        <v-row>
          <v-col cols="6">
            <v-input> {{ this.refuses }} </v-input>
          </v-col>
        </v-row>
      </div>
      <div class="dados">
        <label><h3>Atualização</h3></label>
        <v-row>
          <v-col cols="6">
            <v-input> {{ this.datetime }} </v-input>
          </v-col>
        </v-row>
      </div>
      <div class="status">
        <img v-if="status" src="../assets/status-covid.png" alt="Status Covid" />
      </div>
    </div>
  </v-container>
</template>
<script>
export default {
  data() {
    return {
      estados: [],
      cases: null,
      state: null,
      deaths: null,
      refuses: null,
      suspects: null,
      datetime: null,
      convertDatetime: null,
      status: true

    };
  },
  mounted() {
    this.buscarDados();

  },
  watch: {},

  methods: {
    async buscarDados() {
      const endpoint = "https://covid19-brazil-api.vercel.app/api/report/v1";

      await fetch(endpoint)
        .then((response) => response.json())
        .then((json) => {
          this.estados = json.data;
        });
    },
    async estado(e) {
      this.status = false
      if(e === null){
        this.cases = null;
          this.deaths = null;
          this.refuses = null;
          this.suspects = null;
          this.datetime = null;
          this.status = true
      }
      for (let i = 0; i < this.estados.length; i++) {
        if (this.estados[i].state == e) {
          this.cases = this.estados[i].cases;
          this.deaths = this.estados[i].deaths;
          this.refuses = this.estados[i].refuses;
          this.suspects = this.estados[i].suspects;
          this.convertDatetime = this.estados[i].datetime;
          this.datetime = new Date(this.convertDatetime);
        }
      }
    },

  },
};
</script>

<style scope>

.home {
  width: 600px;
  background: rgb(245, 244, 244);
  margin-left: 25%;
  border: solid rgb(214, 214, 214);
  border-radius: 20px;
}
.logo {
  width: 200px;
  margin-top: 30px;
  margin-bottom: 50px;
  margin-left: 200px;
}
.status {
  margin-left: 115px;
}
.seletor {
  margin-left: 170px;
}

h3 {
  margin-left: 200px;
}

label {
  color: red;
  margin-bottom: 50px;
}

</style>