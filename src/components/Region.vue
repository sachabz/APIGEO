<template>
  <div class="region">
    <div class="card border-3" style="width: 18rem;">
      <div class="card-body">
        <h5 class="card-title" @click="getDep()">{{ nom }} | {{ code }}</h5>
        <Dep
          class="dep"
          v-for="(dep) in deps"
          v-bind:key="dep.id"
          v-bind:nom="dep.nom"
          v-bind:code="dep.code"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Dep from "./Dep.vue";
import { gsap } from 'gsap';
import { CSSPlugin } from 'gsap/CSSPlugin'
gsap.registerPlugin(CSSPlugin);

const axios = require("axios");

export default {
  name: "Region",
  props: {
    nom: String,
    code: String,
  },
  components: { Dep },

  data: () => {
    return {
      deps: "",
    };
  },

  methods: {
    getDep: function () {
      console.log("hello");
      axios
        .get(`https://geo.api.gouv.fr/regions/${this.code}/departements`)
        .then((response) => {
          console.log(response.data);
          this.deps = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
      gsap.to(".region", { duration: 2, rotation: 360 });


    }
  },

  mounted() {
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.border-3 {
  border-width: 3px !important;
}
</style>
