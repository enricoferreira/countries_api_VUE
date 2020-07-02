<template>
  <div class="container">
      <div class="segment">
        <h1>Countries</h1>
      </div>
      <div class="segments" v-if="region.asia">
        <div class="segment" v-for="(continent, index) in region" :key="index">
            <div class="head-segment">
                <div class="d-flex align-base">
                    <h3 class="header p-r-1">{{index | capitalize}}</h3>                    
                    <div class="input-filter p-r-1">
                        <input @change="order" class="p-r-1" type="radio" checked value="asc" :name="index" :id="index+'asc'">
                        <label :for="index+'asc'">A - Z</label>
                    </div>
                    <div class="input-filter">
                        <input @change="order" class="p-r-1" type="radio" :name="index" value="desc" :id="index+'desc'">
                        <label :for="index + 'desc'">Z - A</label>
                    </div>
                </div>
                <span class="badge badge-info">{{continent.length}}</span>
            </div>
            <list-item @trocarPais="trocaPais" :paises="continent"></list-item>
        </div>
      </div>      
      <transition mode="in-out" name="fade" appear>
          <modal-detail @updateCountry="updateCountry" :pais="pais"></modal-detail>
      </transition>
  </div>
</template>

<script>
export default {
    name: 'AllCountries',
    components:{        
        ListItem: ()=>import('./ListItem.vue'),
        ModalDetail: ()=>import('./ModalDetail.vue')
    },
    data(){
        return{            
            err: false,
            regions: ['americas', 'europe', 'africa', 'oceania', 'asia'],
            region: {
                americas: false,
                europe: false,
                africa: false,
                oceania: false,
                asia: false
            },
            pais: false
        }
    },
    methods: {        
        fetchRegions(region){
            fetch(`https://restcountries.eu/rest/v2/region/${region}`)
            .then(r => r.json())
            .then(json => this.region[region] = json)
            .catch(err => this.false = err)
        },
        order(event){            
            const region = event.currentTarget.getAttribute('name');
            this.region[region].reverse();
        },
        trocaPais(country){
            this.pais = country
        },
        updateCountry(status){
            this.pais = status
        }
    },
    computed: {
    },
    created() {
        this.regions.forEach(region => this.fetchRegions(region));        
    },
    filters:{
        capitalize(value){
            return value.charAt(0).toUpperCase().concat(value.slice(1));
        },
       
    }
}
</script>

<style>
    .align-base{
        align-items: baseline;
    }

    .d-flex{
        display: flex;
    }

    .p-r-1{
        padding-right: 1rem;
    }

    :root{
        --divider: 1px solid #e2e2e2;
        --container-color: #f7f7f7
    }

    .container{
        margin: 0 auto;
        width: 90%;
    }

    .segments{
        display: flex;
        width: 100%;
        overflow: auto;
    }

    .segment{
        min-width: 400px;        
        border-radius: 3px;
        box-shadow: var(--shadow);
        margin-bottom: 1rem;
        background: var(--container-color);
        padding: 0 5px;
        max-height: 500px;
        overflow-y: auto;
        position: relative;
        margin: 1rem 10px;
    }

    .list{
        overflow-y: auto;
        overflow-x: hidden;
        scroll-behavior:smooth;
        display: flex;
        padding: 0 5px;
        flex-direction: column;        
    }

    .segment::-webkit-scrollbar, body::-webkit-scrollbar, .segments::-webkit-scrollbar{
        width: 5px;
        background: rgba(0, 0, 0, 0);
        height: 5px;
    }

    .segment::-webkit-scrollbar-thumb, body::-webkit-scrollbar-thumb, .segments::-webkit-scrollbar-thumb{
        background: rgb(221, 220, 220);
    }

    .list-item{
        width: 100%;
        display: flex;
        padding: 10px 5px;
        align-items: flex-end;
        border-bottom: var(--divider);
    }
    
    .cards .card{
        padding: 0 8px;
    }

    .head-segment{
        padding: 5px;
        border-bottom: var(--divider);
        margin-bottom: .5rem;
        display: flex;
        justify-content: space-between;
        position: sticky;
        top: 0;
        background: var(--container-color);
    }

    .badge{
        padding: 4px;
        border-radius: 3px;
        display: flex;
        align-items: center;
    }

    .badge-info{
        background: rgb(101, 138, 241);
        color: white;
    }

    .list-img{
        width: 50px;
        height: 50px;
    }

    .img-flag{
        width: 100%;
        height: 100%;
        border-radius: 50%;
        box-shadow: var(--shadow);
        border: 1px solid #e0e0e0;
    }
</style>