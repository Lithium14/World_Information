<template>
  <v-card style="background :linear-gradient(90deg,#61DAFB 0%, rgb(10, 167, 211) 100%)"
      elevation="24" shaped width="420px">
    <v-row>
      <v-col justify="center" class="col-2">
        <v-img :src="card.flag" width="100px" />
      </v-col>
      <v-col class="col-7">
        <v-card-title class="text-center subtitle-2">
          {{ card.name}}
        </v-card-title>
      </v-col>
      <v-col class="col-3">
        <v-card-subtitle>
          {{ card.population }}
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
  }
}
</script>

<style scoped>
/* .col {
  border: 1px solid red;
}
.row {
  border: 1px solid green
} */
</style>
