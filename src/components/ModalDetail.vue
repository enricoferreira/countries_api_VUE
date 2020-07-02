<template>
    <div @click="close_wrapper" v-if="pais" class="card-wrapper">
        <transition name="fade">                
            <div v-for="(dados, index) in pais" :key="index" class="card">
                <button @click="close" class="close">X</button>
                <div class="card-header">
                    <img :src="dados.flag" :alt="dados.name">
                </div>
                <div class="card-body">
                    <p><strong>País: </strong> {{dados.name}}</p>
                    <p><strong>Capital: </strong>{{dados.capital}}</p>
                    <p><strong>Continente: </strong>{{dados.region}}</p>
                    <p><strong>População: </strong>{{dados.population}}</p>
                    <p><strong>Área: </strong>{{dados.area}}</p>
                    <p><strong>Idioma: </strong>{{dados.languages[0].name}}</p>
                    <p><strong>Currency: </strong>{{dados.currencies[0].symbol}}</p>        
                </div>
            </div>
        </transition>
    </div>
</template>

<script>
export default {
    name: 'ModalCountry',
    props: ['pais'],
    methods:{
        close(){
            this.pais = false;
            this.$emit('updateCountry', this.pais);
        },
        close_wrapper(event){
            if(event.target == event.currentTarget){
                this.close();
            }
        }
    }
}
</script>

<style>   
    :root{
        --card-color: rgb(248, 246, 246);
    }

    .card-body:nth-child(1){
        background: #000;
    }

    .card-wrapper button.close{
        background: var(--card-color);
        border: none;
        padding: 5px;
        width: 30px;
        height: 30px;
        border-radius: 50%;
        position: absolute;
        top: -10px;
        right: -7px;
        box-shadow: var(--shadow);
    }

    .card-wrapper{
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.11);        
        position: fixed;
        top: 0;
        left: 0;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .card{
        position: relative;
        max-width: 300px;                        
        background: var(--card-color);
        min-height: 400px;
        border-radius: 4px;
        box-shadow: var(--shadow);
    }

    .card-header{
        height: 150px;   
        margin-bottom: 20px;     
        padding: 10px;
        border-bottom: 1px solid rgb(228, 228, 228);
    }

    .card-body{
        padding: 10px;
    }

    img{
        width: 100%;
        height: 100%;
    }

    .fade-enter, .fade-leave-to{
        opacity: 0;
    }

    .fade-enter-active, .fade-leave-active{
        transition: opacity .5s;
    }
</style>