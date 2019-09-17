<template>
  <div class="ResultSection">

    <!-- Widok wyników gdy występuje co najmniej jeden rezultat wyszukiwania -->
    <div v-if="results.results.length > 0">
      <!-- TODO Zmienić wartość znalezionych rezultatów -->
      <p>Found {{results.results.length}} songs</p>
      <SongComponent  v-for="i in results.results.length" :key="i" v-bind:song="results.results[i-1]" />
    </div>
    
    <!-- Komunikat w przypadku braku rezultatów -->    
    <div v-else style="padding: 25px">Sorry, no matches found</div>
    
  </div>
</template>


<script>
import SongComponent from './SongComponent.vue'

export default {
  name: 'ResultSection',
  components: {
    SongComponent
  },
  props: ['results'],
}
</script>


<style scoped>
.ResultSection {
  max-width: 660px;
  margin: 15px auto;
  color: #000000;
}
</style>
