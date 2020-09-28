<template>
  <div id="app">
   <pokemon></pokemon>
  </div>
</template>

<script>
import data_pokemon from './components/Pokeguia.vue'
  export default {
    data() {
      return {
      };
    },
    components: {
      'pokemon': data_pokemon,
    }
  }
</script>

<style scoped>

</style>
