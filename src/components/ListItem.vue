<template>
  <div class="list">
      <div @click="detailCountry" v-for="(pais, index) in paises" :key="index" :id="pais.name" class="list-item">
          <div class="list-img">
              <img class="img-flag" :src="pais.flag" :alt="pais.nome">
          </div>
          <h4 class="p-l-1 header">
              {{pais.name}}
          </h4>
      </div>
  </div>
</template>

<script>
export default {
    name: 'ListItem',
    data(){
        return{
            country: false,
            err: false
        }
    },
    props: ['paises'], 
    methods:{
        detailCountry(event){
            const nameCountry = event.currentTarget.getAttribute('id');
            fetch(`https://restcountries.eu/rest/v2/name/${nameCountry}`)
            .then(r => r.json())
            .then(json => this.country = json)
            .catch(err => this.err = err)
        },        
    },
    watch:{
        country(){
            this.$emit('trocarPais', this.country)            
        }
    }
}
</script>

<style>
 .p-l-1{
     padding-left: 1rem;
 }
</style>