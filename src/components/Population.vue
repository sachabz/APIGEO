<template>

    <div class="button">
      <button type="button" class="btn btn-warning">{{ population}}</button>
  </div>
</template>

<script>
export default {
  name: "Population",
  props: {
    population: Number,
    code: String,
    codeDepartement: String,
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
