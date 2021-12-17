<template>
  <div class="home d-flex justify-content-center align-items-center" id="home"></div>
  <div>
    <h2 @mouseenter="hover()">Nos belles régions de France</h2>
  </div>
  <Region
    v-for="(region) in regions"
    v-bind:key="region.id"
    v-bind:nom="region.nom"
    v-bind:code="region.code"
    class="m-4 border-3 d-flex justify-content-center align-items-center region"
  />
</template>

<script>
// @ is an alias to /src

const axios = require("axios");
import Region from "../components/Region.vue";
import { gsap } from 'gsap';
import { CSSPlugin } from 'gsap/CSSPlugin'
gsap.registerPlugin(CSSPlugin);

export default {
  name: "Home",
  components: { Region },
  data: () => {
    return {
      regions: "",
    };
  },

  mounted() {
    axios
      .get("https://geo.api.gouv.fr/regions")
      .then((response) => {
        console.log(response.data);
        this.regions = response.data;
      })
      .catch((error) => {
        console.log(error);
      });
  },

  methods: {
    getRegion() {
      axios
        .get("https://geo.api.gouv.fr/regions")
        .then((response) => {
          console.log(response.data);
          this.regions = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    hover() {
      gsap.to(".region", { scale: 1.12, color: "blue", duration: 1.5, paused: true, ease: "power1.inOut" });
    }

  },
};
</script>
 <style scoped lang="scss">
.border-3 {
  border-width: 3px !important;
}

h2 {
  animation-duration: 3s;
  animation-play-state: running;
}

.home {
  background: url("../assets/paysage.jpg");
}
</style>