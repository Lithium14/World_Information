<template>
  <v-container>
    <h1 style="color: #61DAFB">Population Mondiale</h1>
    <v-row>
      <v-col v-for="(country, index) in countries" :key="index" class="col-3" max-height="340px">
        <card :card="country">></card>
      </v-col>
    </v-row>

  </v-container>
</template>
<script>
import card from '@/components/card'
export default {
  components: { card },
  data() {
    return {
      countries: {}
    }
  },
  async fetch() {
    try {
      this.countries = await fetch('https://restcountries.eu/rest/v2/all').then(res => res.json())
      console.log(this.countries)
    } catch (error) {
      console.log(error)
    }
  }
}
</script>
<style scoped>
h1 {
  text-transform: uppercase;
}
</style>
