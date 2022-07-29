<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter ">
      <h4 class="is-size-1">Pokedex</h4>
      <hr>
      <input type="text" name="" id="" placeholder="Buscar pokemon pelo nome" v-model="busca" class="input is-rounded">
      <button class="button is-fullwidth is-success" id="buscaBtn">Normal</button>

      <div v-for="(poke,index) in resultadoBusca" :key="poke.url">
         <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/PoKemon';
export default {
  name: 'App',
  data(){
    return{
      pokemons:[],
      busca:''

    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res=> {
      console.log("esta pegando lista");
      this.pokemons = res.data.results;
      
    })
  },
  components:{
    Pokemon
  },
  computed:{
    resultadoBusca: function(){
      if(this.busca == '' || this.busca == ' '){
        return this.pokemons;
      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }
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

#buscaBtn{
  margin-top: 2% 
}
</style>
