<template>
  <div>
    <h1>Imóveis para alugar</h1>

    <v-text-field v-model="termoPesquisa" label="Fiter by City" prepend-icon="search" @keyup="filtrar()" />
    <v-layout>
      <imovel v-for="meuImovel in imoveis" :key="meuImovel.id" :imovel="meuImovel" />
    </v-layout>
  </div>
</template>

<script>
import Imovel from '@/components/Imovel'

export default {
  components: { Imovel },

  data() {
    return {
      imoveis: [],
      termoPesquisa: null
    }
  },

  mounted() {
    this.carregar()
  },

  methods: {
    carregar(params) {
      this.$axios.get('/imoveis', { params }).then((response) => {
        this.imoveis = response.data
      })
    },
    filtrar() {
      this.carregar({ city: this.termoPesquisa })
    }
  }
}
</script>

<style scoped>

</style>
