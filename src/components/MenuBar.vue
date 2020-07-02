<template>
    <nav>
        <ul>            
            <li><a @click="enviarConteudo" data-href="ByName" href="#">Country per Name</a></li>
            <li><a  @click="enviarConteudo" data-href="AllCountries" href="#">All Countries</a></li>
            <li><a @click="enviarConteudo" data-href="ByCurrency" href="#">By Currency</a></li>
            <li><a @click="enviarConteudo" data-href="ViewCountry" href="#">By components</a></li>            
        </ul>
    </nav>
</template>

<script>
export default {
    name: 'MenuBar',
    data() {
        return {
            
        }
  },
  props: ['componenteAtivo'],
  methods: {
      enviarConteudo(event){
          const component = event.currentTarget.getAttribute('data-href'); 
          this.$emit('trocar-conteudo', component)
      }
  },
}
</script>

<style>
    :root {
        --shadow: 0px 3px 8px -4px rgba(0, 0, 0, 0.355);        
    }
    nav{
        width: 100%;
        position: sticky;
        top: 0;
        background: rgb(238, 237, 237);
        box-shadow: var(--shadow);
        margin-bottom: 1rem;
    }
    ul{
        width: 100%;
        display: flex;        
        justify-content: space-between;
    }    
    ul li{
        padding: 10px;    
    }

    ul li, ul li a{
        transition: .2s;            
    }

    ul li:hover, ul li:hover a{
        background: rgb(212, 212, 212);
        color: white;
        transition: .2s;
    }


    .input-form{
        padding: 5px;
        border: none;
        border-radius: 3px;
    }
</style>