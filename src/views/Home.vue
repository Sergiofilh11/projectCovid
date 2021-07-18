<template>
  <v-container fluid>
    <div class="home">
      <div>
        <img class="logo" src="../assets/logo-unime-p.png" alt="Unime logo" />
      </div>
      
      <div>
        <label for="buscador"><h3>Buscar pelo Estado(UF)</h3></label><br />
        <v-row align="center">
          <v-col cols="4">
            <v-select 
              id="select"
              :items="estados"
              item-text="state"
              label="Estado"      
              >
            </v-select>
          </v-col>
        </v-row>
      </div>
      
      <div id="dados">
        <label><h3>Numero de casos confirmados</h3></label>
        <v-row align="center">
          <v-col cols="4" class="select">
            <v-input > {{ cases }}
            </v-input>
          </v-col>
        </v-row>
      </div>

      <div id="dados">
        <label><h3>Numero de casos suspeitos</h3></label>
        <v-row align="center">
          <v-col cols="4" class="select">
            <v-select 
              :items="estados"
              item-text="suspects"     
              >
            </v-select>
          </v-col>
        </v-row>
      </div>

      <div id="dados">
        <label><h3>Numero de óbitos</h3></label>
        <v-row align="center">
          <v-col cols="4" class="select">
            <v-select 
              :items="estados"
              item-text="deaths"     
              >
            </v-select>
          </v-col>
        </v-row>
      </div>

      <div id="dados">
        <label><h3>Casos rejeitados</h3></label>
        <v-row align="center">
          <v-col cols="4" class="select">
            <v-select 
              :items="estados"
              item-text="refuses"     
              >
            </v-select>
          </v-col>
        </v-row>
      </div>
  
      <div class="status">
        <img src="../assets/status-covid.png" alt="Status Covid" />
      </div>
    </div>
  </v-container>
</template>
<script>
export default {
  data() {
    return {
      estados: [],
      cases: ""
    };
  },
  mounted() {
    this.buscarDados();
  },
  watch: {
    findCases() {
      const find = document.querySelector("#select")
      this.cases = find
    }
  },

  methods: {
    async buscarDados() {
      const endpoint = "https://covid19-brazil-api.vercel.app/api/report/v1";

      await fetch(endpoint)
        .then((response) => response.json())
        .then((json) => {
          this.estados = json.data;
        });
    },

  },
};
</script>

<style>
.home {
  text-align: center;
}
.logo {
  width: 200px;
  margin-top: 30px;
  margin-bottom: 30px;
}
label {
  color: red
}

</style>