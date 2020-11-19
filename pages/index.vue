<template>
  <v-container fluid class="mt-12">

    <v-dialog v-model="isModalDetailVisible" width="450px" >
      <detail :detail="detail" @closedetail-card="closeDetailCard"></detail>
    </v-dialog>

    <h1 style="color: #61DAFB" class="text-center">Population Mondiale</h1>

    <search @onsearch-country="onSearchCountry" class="mt-12"></search>

    <v-row v-if="loading">
      <v-col v-for="p in 20" :key="p" class="col-12 col-sm-6 col-md-4 col-lg-4 col-xl-4">
        <v-skeleton-loader type="card"></v-skeleton-loader>
      </v-col>
    </v-row>

    <v-row v-else>
      <v-col v-for="(country, index) in displayCard" :key="index" class="col-12 col-sm-6 col-md-4 col-lg-4 col-xl-4">
        <card :card="country" @seeDetails="seeDetails"></card>
      </v-col>
    </v-row>

    <div class="text-center">
      <v-pagination
        v-model="pagePagination"
        :length="lengthPagination"
        circle
      ></v-pagination>
  </div>

  </v-container>
</template>

<script>

import card from '@/components/card'
import search from '@/components/search'
import detail from '@/components/detail'

export default {
  components: { card, search, detail },
  data() {
    return {
      countries: [],
      loading: false,
      searchResult: [],
      isSearch: false,
      isModalDetailVisible: false,
      detail: {},
      pagePagination:1,
      limitPagination: 12,
      lengthPagination: 1
    }
  },
  async fetch() {
    try {
      this.loading = true
      this.countries = await fetch('https://restcountries.eu/rest/v2/all').then(res => res.json())
      this.lengthPagination = Math.ceil(this.countries.length/ this.limitPagination);

    } catch (error) {
      console.log(error)
    }
    this.loading = false
  },
  methods: {
    onSearchCountry(value) {
      this.isSearch = true
      this.searchResult = this.countries.filter(x => x.name.toLowerCase().includes(value.toLowerCase()))
    },
    seeDetails(value) {
      this.detail = value;
      this.isModalDetailVisible = true
    },
    closeDetailCard() {
      this.isModalDetailVisible = !this.isModalDetailVisible
    }
  },
  computed: {
    displayCard() {
      const start = this.pagePagination * this.limitPagination - this.limitPagination,
        end = start + this.limitPagination;
      return this.isSearch ? this.searchResult.slice(start, end) : this.countries.slice(start, end);
    }
  }
}
</script>

<style scoped>
h1 {
  text-transform: uppercase;
}
</style>
