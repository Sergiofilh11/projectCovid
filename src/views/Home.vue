<template>
  <div class="home">
    <div>
      <img src="../assets/logo-unime-p.png" alt="Unime logo">
    </div>
    <div>
      <label for="buscador"><strong>Buscar pelo Estado(UF)</strong></label><br>
      <select name="buscador" id="buscador">
        <option v-for="estado of estados" :key="estado.uid">{{ estado.state }}</option>
        </select>
      <!-- <button @click="buscarDados">Carregar Estados</button> -->
      
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
