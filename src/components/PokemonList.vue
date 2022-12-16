<!-- Laurane Mouronval -->

<template>
  <div class="list" v-if="ok">

    <article v-for="pokemon in pokemonListFiltre" v-bind:key="pokemon.name" v-on:click="AfficheDetail(pokemon.url)">
      <img v-bind:src="IMG_URL + pokemon.name + '.png'">
      <h3>{{ pokemon.name }}</h3>
    </article>
    
  </div>
</template>

<script>
import config from "../config/config.json";
import axios from 'axios';

// package lodash  = permet de faire des opérations complexes sur des tableaux
const _ = require('lodash');

export default {

  props: ['recherche', 'url'],
  
  data: function () {
    return {
      listePokemons: null,
      IMG_URL: config['IMG_URL'],
      ok: false,
    }
  },

  methods: {
    AfficheDetail: function(url) {
      this.$emit('afficheDetailEmit', url);
    },
  },

  beforeMount () {
    axios
      .get(config['API_URL']+'/pokemon')
      .then((response) => {
        this.listePokemons = response.data;
        this.ok = true;
    })
  },

  computed: {

    pokemonListFiltre() {
      // Si valeur de recherche est vide alors ça retourne le tableau du data qui stockait la liste de tous les pokemons
      if (this.recherche == "") {
        return this.listePokemons.results;
      } else {
        var listeTousPokemons = this;

        // Pour chaque pokemon dans la liste la fonction dans les parametre sera appelée
        // la fonction filter 
        return this.listePokemons.results.filter(
          
          function (pokemon) {
            // includes est une fonction de lodash
            // elle renvoie true si les lettres saisies dans la recherche sont retrouvées
            // dans le nom du pokemon, false sinon

            // console.log(pokemon)
            return _.includes(pokemon.name.toUpperCase(), listeTousPokemons.recherche.toUpperCase());
        
          });
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  grid-gap: 10px;
  width: 100%;
  max-width: 510px;
}
article {
  height: 150px;
  background-color: #efefef;
  text-align: center;
  text-transform: capitalize;
  border-radius: 5px;
  cursor: pointer;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}
h3 {
  margin: 0;
}
#scroll-trigger {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 150px;
  font-size: 2rem;
  color: #efefef;
}

img {
  width: 96px;
  height: 96px;
}
</style>

