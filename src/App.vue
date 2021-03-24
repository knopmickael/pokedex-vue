<template>
  <div id="app">

    <div class="cabecalho">
      <a href="https://pokeapi.co/" target="_blank"><img class="responsive" src="https://raw.githubusercontent.com/PokeAPI/media/master/logo/pokeapi_256.png" alt="logoPokeAPI"></a>
      <input type="text" placeholder="Pesquise o Pokemon" v-model="busca">
      <button @click="filtrarPokemons">OK</button>
    </div>

      <div class="flexible" v-if="pokemonsFiltrados!=pokemons">
        <div v-for="(pokemon, index) in pokemonsFiltrados" :key="pokemon.name">
          <Pokemon :n="index" :name="pokemon.name" :url="pokemon.url" :solo="false"/>
        </div>
      </div>

      <div class="flexible" v-else>
        <div v-for="(pokemon, index) in pokemonsFiltrados" :key="pokemon.name">
          <Pokemon :n="index" :name="pokemon.name" :url="pokemon.url" :solo="true"/>
        </div>
      </div>

  </div>
</template>

<script>

import axios from 'axios';
import Pokemon from './components/Pokemon.vue'

export default {
  
  name: 'App',

  components: {
    Pokemon
  },

  data(){
    return {
      pokemons: [],
      pokemonsFiltrados: [],
      busca: ''
    }
  },

  created: function() {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res => {
      // console.log(res.data.results)
      this.pokemons = res.data.results
      this.pokemonsFiltrados = this.pokemons
    });
  },

  methods: {
    filtrarPokemons: function() {
      // console.log("filtrando");
      // this.pokemonsFiltrados = this.pokemons
      // console.log(this.pokemonsFiltrados)
      // console.log("Buscando... " + this.busca)
      // console.log(this.pokemonsFiltrados)
      if(this.busca == '') this.pokemonsFiltrados = this.pokemons
      else this.pokemonsFiltrados = this.pokemons.filter(pokemon => pokemon.name == this.busca )
      this.busca = ''

    }
  }

}

</script>

<style>

  body {
    background: rgb(255, 95, 0);
  }

    /* width */
  ::-webkit-scrollbar {
    width: 8px;
  }

  /* Track */
  ::-webkit-scrollbar-track {
    background:orangered;
  }

  /* Handle */
  ::-webkit-scrollbar-thumb {
    background: white;
    border-radius: 25px;
  }

  /* Handle on hover */
  ::-webkit-scrollbar-thumb:hover {
    background: lightgray;
  }

  * {
    padding: 0;
    margin: 0;
    font-family: verdana, tahoma;
  }

  .cabecalho {
    padding-top: 45px;
    display: flex;
    justify-content: center;
  }

  .cabecalho img {
    width: 300px;
    transition: all 0.25s ease;
    align-self: center;
  }

  .cabecalho img:hover {
    transform: scale(1.1);
  }

  .cabecalho input {
    font-size: 20px;
    border: none;
    border-radius: 10px;
    padding: 10px 15px;
    margin-left: 50px;
    margin-right: 15px;
    height: 25px;
    width: 350px;
    align-self: center;
  }

  .cabecalho input:focus {
    outline-style: none;
  }

  .cabecalho button {
    height: 50px;
    width: 50px;
    align-self: center;
    background: #3761A8;
    border: none;
    border-radius: 10px;
    color: white;
    font-size: 16px;
    font-weight: bolder;
  }

  .cabecalho button:hover {
    cursor: pointer;
    transform: scale(1.05);
  }

  .cabecalho button:focus {
    outline-style: none;
  }

  @media screen and (max-width: 901px) {
        .cabecalho img {
          width: 200px;
        }
  }

  @media screen and (max-width: 751px) {
        .cabecalho {
          padding-top: 25px;
        }
        .cabecalho img {
          width: 200px;
        }
        .cabecalho button {
          height: 50px;
          width: 50px;
          font-size: 16px;
        }
        .cabecalho input {
          font-size: 16px;
          margin-left: 20px;
          margin-right: 15px;
          height: 25px;
          width: 250px;
        }
  }

  @media screen and (max-width: 631px) {
        .cabecalho img {
          width: 150px;
        }
        .cabecalho button {
          height: 40px;
          width: 45px;
          font-size: 12px;
        }
        .cabecalho input {
          height: 20px;
          width: 200px;
        }
  }

   @media screen and (max-width: 481px) {
        .cabecalho {
          padding-top: 15px;
        }
        .cabecalho img {
          width: 120px;
        }
        .cabecalho button {
          height: 30px;
          width: 35px;
          font-size: 10px;
        }
        .cabecalho input {
          font-size: 12px;
          margin-left: 20px;
          margin-right: 15px;
          height: 12px;
          width: 160px;
        }
  }

  @media screen and (max-width: 376px) {
        .cabecalho {
          padding-top: 12px;
        }
        .cabecalho img {
          width: 100px;
        }
        .cabecalho button {
          height: 25px;
          width: 30px;
          font-size: 8px;
        }
        .cabecalho input {
          font-size: 10px;
          margin-left: 15px;
          margin-right: 5px;
          height: 5px;
          width: 120px;
        }
  }

  #app {
    justify-content: center;
  }

  .flexible  {
    padding-top: 10px;
    padding-bottom: 50px;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }

</style>
