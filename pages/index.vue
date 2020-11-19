<template>
  <v-container fluid class="mt-12">
    <h1 style="color: #61DAFB" class="text-center">Population Mondiale</h1>
    <search @onsearch-country="onSearchCountry" class="mt-12"></search>
    <v-row v-if="loading">
      <v-col v-for="p in 20" :key="p" class="col-12 col-sm-6 col-md-4 col-lg-4 col-xl-4">
        <v-skeleton-loader type="card"></v-skeleton-loader>
      </v-col>
    </v-row>

    <v-row v-else>
      <v-col v-for="(country, index) in searchResult" :key="index" class="col-12 col-sm-6 col-md-4 col-lg-4 col-xl-4">
        <card :card="country" @seeDetails="seeDetails"></card>
      </v-col>
    </v-row>

  </v-container>
</template>

<script>

import card from '@/components/card'
import search from '@/components/search'

export default {
  components: { card, search },
  data() {
    return {
      countries: [],
      loading: false,
      searchResult: [],
      isSearch: false,
    }
  },
  async fetch() {
    try {
      this.loading = true
      this.countries = await fetch('https://restcountries.eu/rest/v2/all').then(res => res.json())
    } catch (error) {
      console.log(error)
    }
    this.loading = false
  },
  methods: {
    onSearchCountry(value) {
      this.searchResult = this.countries.filter(x => x.name.toLowerCase().includes(value.toLowerCase()))
    },
    seeDetails() {
      
    }
  },
  computed: {
    displayCard() {
      return this.isSearch ? this.searchResult : this.countries
    }
  }
}
</script>

<style scoped>
h1 {
  text-transform: uppercase;
}
</style>
