<template>
  <v-card style="background :linear-gradient(90deg,#61DAFB 0%, rgb(10, 167, 211) 100%)"
      elevation="24" shaped width="450px">
    <v-row class="ma-0">
      <v-col class="col-2" align-self="center" >
        <v-img :src="card.flag"/>
      </v-col>
      <v-col class="col-5">
        <v-card-title class="text-left subtitle-2">
          {{ card.name}}
        </v-card-title>
      </v-col>
      <v-col class="col-5 text-left">
        <v-card-subtitle>
          {{ formatNumber(card.population) }}
        </v-card-subtitle>
      </v-col>

    </v-row>

  </v-card>
</template>

<script>
export default {
  props: {
    card: {
      type: Object,
      default: () => {}
    }
  },
  methods: {
    formatNumber(num) {
      return num.toString().replace(/(\d)(?=(\d{3})+(?!\d))/g, '$1.')
    }
  },
}
</script>

<style scoped>
.col {
  border: 1px solid red;
}
.row {
  border: 1px solid green
}
</style>
