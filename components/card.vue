<template>
  <v-container >
    <v-hover v-slot="{ hover }">
      <v-card style="background :linear-gradient(90deg,#61DAFB 0%, rgb(10, 167, 211) 100%)"
        :elevation="hover ? 24 : 2" shaped width="450px" min-height="100px" :class="{ 'on-hover': hover }">

        <v-row class="ma-0" >

          <v-col class="col-2" align-self="center" >
            <v-img :src="card.flag" min-width="50px"/>
          </v-col>

          <v-col class="col-6" align-self="center">
            <v-card-title class="text-left subtitle-2">
              {{ card.name}}
            </v-card-title>
          </v-col>

          <v-col class="px-0 col-4 text-center " align-self="center">
            <v-card-subtitle>
              {{ formatNumber(card.population) }} <br>
              Habitants
            </v-card-subtitle>
          </v-col>

          <v-col class="pt-0">
            <v-btn :class="{ 'show-btns': hover }"
                    color="transparent" icon block
                    @click="seeDetails()">
              Voir plus
            </v-btn>
          </v-col>

        </v-row>

      </v-card>

    </v-hover>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      transparent: 'rgba(255, 255, 255, 0)',
    }
  },
  props: {
    card: {
      type: Object,
      default: () => {}
    }
  },
  methods: {
    formatNumber(num) {
      return num.toString().replace(/(\d)(?=(\d{3})+(?!\d))/g, '$1.')
    },
    seeDetails() {
      this.$emit('seeDetails', this.card)
    }

  },
}
</script>

<style scoped>

.v-card {
  transition: opacity .4s ease-in-out;
  cursor: pointer;
}

.v-card:not(.on-hover) {
  opacity: 0.7;
 }

.show-btns {
  color: rgba(255, 255, 255, 1) !important;
}

</style>
