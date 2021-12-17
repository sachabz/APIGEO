<template>
  <div class="card dep m-2" style="width: 18rem;">
    <div class="card-body">
      <h5 class="card-title">{{ nom }} | {{ code }}</h5>
      <Population v-bind:population="population" @click="getPopulation()" />
    </div>
  </div>
</template>

<script>
import Population from "./Population.vue";

const axios = require("axios");
export default {
  name: "Dep",
  props: {
    nom: String,
    code: String,
    codeDepartement: String,
  },
  components: { Population },

  data: () => {
    return {
      population: "",
    };
  },

  methods: {
    getPopulation() {
      axios
        .get(`https://geo.api.gouv.fr/departements/${this.code}/communes`)
        .then((response) => {
          console.log(response.data);
          this.population = response.data;
          let population = 0;
          for (let i in this.population) {
            population += this.population[i].population;
            console.log(population);
          }
          this.population = population;
        })
        .catch((error) => {
          console.log(error);
        });
    }
  },

  mounted() {
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.dep {
  background-color: black;
  color: white;
}
</style>

