<!-- Laurane Mouronval -->

<template>
  <div class="searchbar">
    <input type='text' v-model="recherche" placeholder="Rechercher un pokémon"/>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      // la recherche par defaut est vide 
      recherche: "",
    }
  },

  // le watch permet de detecter un changement dans l'input
  watch: {
    recherche(value) {
      // a chaque changement fait dans cet input, on emit 
      // = ça permet une mise à jour de la liste de pokemon en temps reel
      this.$emit('searchPokemonEmit', value);
    }
  },
};
</script>

<style scoped>
.searchbar {
  position: relative;
  width: 100%;
  max-width: 510px;
  padding-bottom: 20px;
}
input {
  border: none;
  outline: none;
  border-radius: 5px;
  padding: 10px 40px 10px 10px;
  width: calc(100% - 50px);
  font-size: 1rem;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}
</style>
