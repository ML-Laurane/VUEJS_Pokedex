<!-- Laurane Mouronval -->

<template>
  <!-- sans la variable ok, le programme essaye de lire les valeurs de l'initialisation de la carte pokemon = erreur-->
  <div class="detail" v-if="visible && ok">
    <div class="detail-view card">

      <!-- Présentation du détail d'un pokemon -->
      <div class="data card-body">
        <img class="image" v-bind:src="IMG_URL + pokemon.name + '.png'">
        <h2 class="card-title">{{pokemon.name}}</h2>

        <h3>Types :</h3>
        <div class="types" v-for="item in pokemon.types" v-bind:key="item.slot">
          <div class="type">
            <span v-bind:class="item.type.name">{{ item.type.name }}</span>
          </div>
        </div>

        <h3>Talents :</h3>
        <div class="abilities" v-for="item in pokemon.abilities" v-bind:key="item.ability.name">
          <div class="ability">{{ item.ability.name }}</div>
        </div>
        <div class="property">
          <div class="left bold">Taille :</div>  
          <div class="right">{{pokemon.height}}</div>
        </div>
        <div class="property">
          <div class="left bold">Poids :</div>  
          <div class="right">{{pokemon.weight}}</div>
        </div>
      </div>
      <button class="close" v-on:click="closeDetail();">Fermer</button>
    </div>
  </div>

</template>

<script>
import config from "../config/config.json";
import axios from 'axios';

export default {
  props: ['detailPokemonUrl', 'visible'],
  data: function () {
    return {
      // initialisation de la carte détail d'un pokemon
      pokemon: null,
      IMG_URL: config['IMG_URL'],
      ok: false,
    }
  },

  // dès qu'un changement est detécté sur le detail pokemon, je le mets à jour
  watch: {
    // personnalisation de la carte detail du pokemon choisi
    detailPokemonUrl(value) {
      axios
        .get(value)
        .then((response) => {
        // je récupère les données du pokemon 
          console.log(response.data)
          this.pokemon = response.data;
          this.ok = true;
      })
    }
  },

  methods: {
    closeDetail: function() {
      this.$emit('closeEmit');
    },
  }

};
</script>

<style lang="scss" scoped>
.type {
  .grass {
    background: rgb(3, 139, 44) !important;
  }
  .poison {
    background: rgb(74, 7, 105) !important;
  }
  .water {
    background: rgb(8, 135, 219) !important;
  }
  .dragon {
    background: rgb(27, 2, 68) !important;
  }
  .ice {
    background: rgb(78, 199, 255) !important;
  }
  .flying {
    background: rgb(145, 215, 255) !important;
  }
  .fire {
    background: rgb(238, 135, 17) !important;
  }
  .ghost {
    background: rgb(74, 52, 87) !important;
  }
  .fighting {
    background: rgb(122, 0, 0) !important;
  }
  .normal {
    background: rgb(104, 104, 104) !important;
  }
  .psychic {
    background: rgb(195, 0, 255) !important;
  }
  .bug {
    background: rgb(52, 87, 6) !important;
  }
  .dark {
    background: rgb(43, 43, 43) !important;
  }
  .steel {
    background: rgb(116, 116, 116) !important;
  }
  .fairy {
    background: rgb(248, 165, 237) !important;
  }
  .eletric {
    background: rgb(255, 217, 1) !important;
  }
  .rock {
    background: rgb(88, 95, 100) !important;
  }
  .ground {
    background: rgb(92, 70, 70) !important;
  }
}

.detail {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  position: fixed;
  top: 0;
  left: 0;
  padding: 90px 10px 10px;
  //width: calc(100% - 20px);
  // height: calc(100vh - 20px);
  width: 100%;
  height: 100vh;
  background: rgba(10, 7, 0, 0.562);
}
.detail-view {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 90%;
  padding: 50px 0 0;
  position: relative;

  max-width: 510px;

  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}
.image {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: -60px;
  width: 120px;
  height: 120px;
  background-color: #ffcb04;
  border-radius: 50%;
  overflow: hidden;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}

h2 {
  text-transform: capitalize;
}

.data {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  flex-direction: column;
  width: 100%;
  margin-bottom: 40px;
}
.property {
  width: 90%;
  max-width: 400px;
  border-bottom: 1px solid #ccc;
  margin-bottom: 10px;
}
.left {
  float: left;
}
.right {
  float: right;
}
h3 {
  width: 90%;
  max-width: 400px;
  border-bottom: 1px solid #ccc;
}

.types,
.abilities {
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
  width: 90%;
  max-width: 400px;
}
.type {
  // color: rgb(17, 67, 182);
  margin: 0 0 10px 0;
  padding: 5px 10px;
  font-weight: bold;
  font-size: 1rem;
  letter-spacing: 2px;
  text-transform: capitalize;
  span {
    color: #ffffff !important;
    padding: 10px 14px;
    border-radius: 29px;
  }
}
.ability {
  color: rgb(10, 119, 10);
  margin: 0 10px 10px 0;
  border-radius: 20px;
  padding: 5px 10px;
  font-weight: bold;
  font-size: 1rem;
  letter-spacing: 2px;
  text-transform: capitalize;
  word-wrap: none;
  word-break: keep-all;
  background-color: #ffffff;
  border: 3px solid;
}

.close {
  outline: none;
  border: none;
  border-radius: 5px;
  background-color: #c73015;
  color: #efefef;
  padding: 10px 20px;
  margin-bottom: 20px;
  font-size: 1.2rem;
  cursor: pointer;
}
i {
  font-size: 2rem;
  color: #efefef;
}
.bold {
  font-weight: bold;
}
</style>
