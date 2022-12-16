<!-- Laurane Mouronval -->

<template>
  <div class="container">
    <!-- barre de recherche tout en haut de l'écran, elle permet de filtrer les pokemons dont le noms contient les lettres saisies -->
    <PokemonSearch @searchPokemonEmit="setPokemonSearch"/>

    <!-- carte d'identité d'un pokemon avec ses détails qui s'affiche si l'utilisateur clique sur un pokemon en particulier -->
    <PokemonDetail @closeEmit="closeDetail" v-bind:detailPokemonUrl='pokemonURL' v-bind:visible='visible' />

    <!-- liste de tous les pokemons affichée en fonction de la recherche-->
    <PokemonList @afficheDetailEmit="openDetail" v-bind:recherche='recherche' v-bind:pokemonURL='listeUrl'/>
  </div>
</template>

<script>
import PokemonDetail from "../components/PokemonDetail.vue";
import PokemonList from "../components/PokemonList.vue";
import PokemonSearch from "../components/PokemonSearch.vue";
import config from "../config/config.json";

export default {
  data: function () {
    return {
      pokemonURL: config.IMG_URL,
      listeUrl: config.API_URL +'/pokemon',
      visible: false,
      recherche: "",
    }
  },
  components: {
    PokemonDetail,
    PokemonList,
    PokemonSearch,
  },
  methods: {
    openDetail: function(pokemonURL) {
      this.pokemonURL = pokemonURL;
      this.visible = true;
    },
    closeDetail: function() {
      this.visible = false;
    },
    setPokemonSearch: function(pokemonRecherche) {
      this.recherche = pokemonRecherche;
    },
  }
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 10px;
  width: calc(100% - 20px);
  min-height: calc(100vh - 20px);
  //background: radial-gradient(#ffbf0b, #e20000);

  font-family: "Acme", arial;
  font-size: 1rem;
  font-weight: normal;
}

h1 {
  color: #efefef;
}
</style>