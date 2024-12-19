<template>
  
  <div id="app">
    
    <div class="column is-half is-offset-one-quarter">
      <img class="logoPagina" src="./assets/NovaLogoHibit_Banner.png">
      <hr>
      <h4 class="is-size-4">Pokedex</h4>

      <input type="text" name="" id="" placeholder="Pesquisar Pokemon pelo nome (minusculo)" class="input is-rounded" v-model="busca">
      <button id="btnBusca" class="button is-success is-rounded" @click="buscar">Buscar</button>

      
      <div v-for="(poke,index) in filteredPokemons" :key="poke.url">
        <pokemon :num="index+1" :name="poke.name" :url="poke.url"></pokemon>
      </div>
    </div>
    
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon.vue';
export default {
  name: 'App',
  data(){
    return {
      pokemons: [],
      filteredPokemons: [],
      busca:''
    }
  },
  created: function() {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0')
      .then(response => {
        console.log(response.data);
        this.pokemons = response.data.results;
        this.filteredPokemons = this.pokemons;
      })
      .catch(error => {
        console.log(error);
        this.pokemons = [];

      });
  },
  components: {
    Pokemon
  },
  methods: {
    buscar: function(){
      this.filteredPokemons = this.pokemons;
      if(this.busca === '' || this.busca === null || this.busca === undefined || this.busca === ' '){
        this.filteredPokemons = this.pokemons;
      }
      else{
        this.filteredPokemons = this.pokemons.filter(poke => poke.name == this.busca);
      }
    }
  },
  computed: {
    /*
    resultadoBusca: function(){
      if(this.busca === '' || this.busca === null || this.busca === undefined || this.busca === ' '){
        return this.pokemons;
      }
      else{
        return this.pokemons.filter(poke => poke.name == this.busca);
      }
    } */
  },
  
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
#logoPagina {
  width: 100%;
  height: 100%;
  padding: 1%;
}
#btnBusca {
  margin-top: 2%;
}
</style>
