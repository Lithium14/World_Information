<template>
  <v-container>
    <v-card style="background :linear-gradient(90deg,#61DAFB 0%, rgb(10, 167, 211) 100%)"
        elevation="24" shaped width="450px" min-height="300px" class="black--text">

        <v-row class="ma-0" >

          <v-col class="col-2 mt-4">
            <v-img :src="detail.flag" width="50px"/>
          </v-col>
          <v-col class="col-10 mt-5">
            <span>{{ detail.name}}, {{detail.alpha2Code}} </span>
          </v-col>

            <v-btn icon @click="$emit('closedetail-card')" top right absolute fab x-small class="mt-5">
              <v-icon small >
                mdi-close
              </v-icon>
            </v-btn>



          <v-row class="ma-0">
            <v-col class="col-6">
              <span> Capital : {{ detail.capital }} </span>
            </v-col>

            <v-col class="col-6">
              <span> Continent : {{ detail.region }} </span>
            </v-col>
          </v-row>


          <v-row class="ma-0">
            <v-col class="col-6">
              <span> Superficie : {{ formatNumber(detail.area) }} km²</span>
            </v-col>

            <v-col class=col-6>
              <span>Langues parlées :</span>
            <ul v-for="(langue,index) in detail.languages" :key="index">
              <li>
                {{ langue.name }}
              </li>
            </ul>
            </v-col>
          </v-row>

          <v-row class="ma-0">
            <v-col class="col-6">
              <span> Indicatif : +{{ detail.callingCodes }} </span>
            </v-col>

            <v-col class="col-6">
              <span> Fuseau horaire : {{ detail.timezones }} </span>
            </v-col>
          </v-row>


        </v-row>

      </v-card>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      isVisible: true,
    }
  },
  props :{
    detail: {
      type: Object,
      default: () => {}
    }
  },
  methods: {
    formatNumber(num) {
      return num.toString().replace(/(\d)(?=(\d{3})+(?!\d))/g, '$1.')
    },
  },
}
</script>
