<template>
  <div class="home">

    <div>
      <img class="logo" src="../assets/logo-unime-p.png" alt="Unime logo">
    </div>
    <div>
        <label for="buscador"><strong>Buscar pelo Estado(UF)</strong></label><br>

        <select name="buscador" id="buscador">
        <option v-for="estado of estados" :key="estado.uid">{{ estado.state }}</option>
        </select>

    </div>
    <div id="dados">
        <strong>Numero de casos (Confirmados)</strong>
        <input type="text-area" disabled value="">
        <input type="text-area" disabled value="">
    </div>

    <div class="status">
        <img src="../assets/status-covid.png" alt="Status Covid">
    </div>
  </div>
</template>
<script>

export default {
  data() {
    return {
      estados: []
    }
  },
  mounted() {
      this.buscarDados()
  },
  methods: {

    async buscarDados() {
      const endpoint = "https://covid19-brazil-api.vercel.app/api/report/v1"
    //   const estadoSelect = document.querySelector('#buscador')

      await fetch(endpoint)
        .then(response => response.json())
        .then(json => {
            this.estados = json.data
            // estadoSelect.innerHTML = ""
         
            // this.estados.forEach (estado => {
            //     estadoSelect.innerHTML += `<option value="${estado.uf}">${estado.state}</option>`
            })
        }
    }
  }

</script>

<style>
    .logo {
        width: 200px;
        margin-top: 30px;
        margin-bottom: 10px;
    }
    #buscador {
        margin-top: 10px;
    }
    .status {
        margin-top: 30px;
    }
</style>