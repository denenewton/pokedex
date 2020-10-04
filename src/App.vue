<template>
  <div id="app">
    
 <div class="column is-half is-offset-one-quarter">
   <img src="./assets/guia.png" alt="">
    <hr>
    <h1 class="is-size-1 ">Pokedex</h1>
    <div id="busca" ><button @click="buscarPokemon" class="button is-info is-rounded">Buscar pokemon</button>
    <input id="busc" type="text" class="input is-rounded" 
    placeholder="Buscar pokemon pelo nome" v-model="busca">
    </div>
    <div v-for="(poke,index) in this.filterPokemons" :key="poke.url">
   <Pokemon :num="index +1 "  :name= "poke.name" :url=" poke.url"/>
  </div>
   
 </div>

  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon'
export default {
  name: 'App',
  data(){
    return{
      pokemons: [],
      filterPokemons: [],
      busca: ''
    }
  },
  created: function(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res => {
      this.pokemons = res.data.results
      this.filterPokemons = this.pokemons
      console.log('pegou a lista de pokemons')
    })
  },

  methods:{
    buscarPokemon: function(){
            this.filterPokemons = this.pokemons;
            if(this.busca.trim() == ""){
                 this.filterPokemons = this.pokemons;
            }else{
            return this.filterPokemons = this.pokemons.filter( pokemon => pokemon.name == this.busca )
            }
    }
  },
  /*computed:{ 
    result_busca: function(){
       
            if(this.busca.trim() == ""){
               return   this.pokemons;
            }else{
            return this.pokemons.filter( pokemon => pokemon.name == this.busca )
            }

  },*/
  components:{
    Pokemon
  }
  
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#busca{
  width:100%;
  display: flex; 
  justify-content: space-between;
  padding-bottom: 4%;
  padding-top: 4%;
}
#busca #busc{
  margin-left: 15px;
}
</style>
