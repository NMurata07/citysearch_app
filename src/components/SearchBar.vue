<template>
  <div>
    <input class="input control city-search" type="text" 
           placeholder="San Francisco"
           v-model="input"
           @keyup="filteredCities">

    <a class="button is-primary control city-search--btn" @click="showResults">Search</a>
    <!-- <a class="button is-success" @click="searchFilterClicked">
      <i class="fa fa-sliders" aria-hidden="true"></i>
    </a> -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      input: ''
    }
  },
  methods: {
    filteredCities() {
      if ( this.input.length > 2 ) {
        // add payload to the custom event
        this.$emit('filteredCities', this.input)
      }
    },
    searchFilterClicked() {
      this.$emit('searchFilterClicked');
    },
    showResults() {
      this.$emit('showResults');
    }
  }
}
</script>