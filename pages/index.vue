<template>
  <v-container>
    <cardDetail />
    <h1 style="color: #61DAFB" class="text-center">Population Mondiale</h1>

    <v-row v-if="loading">
      <v-col v-for="p in 4" :key="p">
        <v-skeleton-loader type="card"></v-skeleton-loader>
      </v-col>
    </v-row>

    <v-row v-else>
      <v-col v-for="(country, index) in countries" :key="index" class="col-3" max-height="340px">
        <card :card="country"></card>
      </v-col>
    </v-row>

  </v-container>
</template>

<script>

import card from '@/components/card'
import cardDetail from '@/components/cardDetail'

export default {
  components: { card, cardDetail },
  data() {
    return {
      countries: {},
      loading: false,
    }
  },
  async fetch() {
    try {
      this.loading = true
      this.countries = await fetch('https://restcountries.eu/rest/v2/all').then(res => res.json())
      console.log(this.countries)
    } catch (error) {
      console.log(error)
    }
    this.loading = false
  }
}
</script>

<style scoped>
h1 {
  text-transform: uppercase;
}
</style>
