<template>
  <div id="app">
    <menu-bar @trocar-conteudo="receberTrocaConteudo"></menu-bar>
    <transition mode="out-in" name="fade" appear>
      <component :is="componenteAtivo"></component>
    </transition>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      componenteAtivo: 'AllCountries'
    }
  },
  components: {
    AllCountries: () => import('./components/AllCountries.vue'),
    ByCurrency: () => import('./components/ByCurrency.vue'),
    ByName: () => import('./components/ByName.vue'),
    ViewCountry: () => import('./components/ViewCountry.vue')
  },
  methods: {
    receberTrocaConteudo(msg){
      this.componenteAtivo = msg
    }
  },
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  text-decoration: none;
  list-style-type: none;  
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

body{
  background: #f3f1f0;
}

.fade-enter, .fade-leave-to{
  opacity: 0;
}

.fade-enter-active, .fade-leave-active{
    transition: opacity .3s;
}
</style>
