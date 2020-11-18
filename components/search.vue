<template>
  <div>
    <v-row justify="center">
      <v-col class="col-6">
        <v-text-field v-model="searchCountry" label="RECHERCHER" filled dense rounded
                      @input="$emit('onsearch-country', searchCountry)"
        ></v-text-field>
      </v-col>
    </v-row>

  </div>
</template>

<script>
export default {
  data() {
    return {
      searchCountry: ''
    }
  },
}
</script>
