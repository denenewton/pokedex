<template>
<div class="pokemon">
<div class="card">
  <div class="card-image">
   <figure>
     <img :src="this.currentImg" alt="Pokemons">
   </figure>
  </div>
  <div class="card-content">
    <div class="media">
      <div class="media-left">
       
      </div>
      <div class="media-content">
        <p class="title is-4"> {{name | upper}}</p>
        <p class="subtitle is-5">{{pokemon.types}}</p>
      </div>
    </div>

    <div class="content">
       <a> </a>
      <a href="#"> </a> <a href="#"> </a>
      <br>
      <time datetime="2016-1-1">11:09 PM - 1 Jan 2016</time>
    </div>
    <button @click="mudarSprites" class="button is-medium is-fullwidth">Mudar Sprites</button>
  </div>
 </div>
</div>
</template>

<script>
import axios  from "axios";
export default {

  data(){
      return{
       currentImg: '', 
       isFront: true,
       pokemon: {
           types: '',
           front: '',
           back: ''
       }
      }
  },
  created: function(){
      axios.get(this.url).then( res =>{
          this.pokemon.types = res.data.types[0].type.name
          this.pokemon.front = res.data.sprites.front_default
          this.pokemon.back = res.data.sprites.back_default
          this.currentImg = this.pokemon.front
      })
  },
  props:{
      num: Number,
      name: String,
      url: String
  },
  filters:{ //filtro para deixar a prim. letra maiscula.
      upper: function(value){
          var newName = value[0].toUpperCase() + value.slice(1);
          return newName;
          
      }
  },
  methods:{
      mudarSprites: function(){
          if(this.isFront === true){
              this.isFront = !this.isFront
              this.currentImg = this.pokemon.back
          }else if(this.isFront === false){
              this.isFront = !this.isFront
              this.currentImg = this.pokemon.front
          }
      }
  }

}
</script>

<style>
.pokemon{
    margin-bottom: 15px;
}


</style>