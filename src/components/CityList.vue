<template>
  <section v-if="cityItems.length">
    
    <article class="results" v-for="obj in cityItems">
      <div class="columns" >
        <div class="column">
          <div class="city--stats">
            <p><strong>City: </strong> {{ obj.city }} </p>
            <p><strong>State: </strong> {{ obj.state }} </p>
          </div>
        </div>

        <div class="column">
          <div class="city--stats">
            <p><strong>Rank: </strong> {{ obj.rank }} </p>
            <p><strong>Population: </strong> {{ obj.population | formattedNumber }} </p>
          </div>
        </div>
      </div> 

      <div class="columns">
        <div class="column">
          <h4>Check the weather in {{ obj.city }}</h4>
          <a @click="showModal(obj.city, 'weather')">
            <img class="city--icon " src="../assets/weather-circle-icon.png">
          </a>
        </div>

        <div class="column">
          <h4>Top Recreation Areas in {{ obj.city }}</h4>
          <a @click="showModal(obj.city, 'city-todos')">
            <img class="city--icon " src="../assets/bowl-food-icon.png">
          </a>
        </div>

        <div class="column">
          <h4>Top 10 Cafes in {{ obj.city }}</h4>
          <a @click="showModal(obj.city, 'cafes')">
            <img class="city--icon " src="../assets/beer.png">
          </a>
        </div>

        <div class="column">
          <h4>Find {{ obj.city }} on Google Maps</h4>
          <a @click="showModal(obj.city, 'map')">
              <img class="city--icon " src="../assets/map-512.png">
          </a>
        </div>
      </div>
    </article><!-- end cityItems -->
    
    <div id="results-bottom" class="p-2 is-centered ">
      <a class="button is-primary" @click="addResults" v-show="showMore()">SHOW MORE</a>
    </div>

  </section>

  <section v-else-if="!results.length && input !== ''">
    <article class="results">
      <h3 class="is-centered">
        Sorry there are no US cities that match <span class="error-input">{{ input }}</span>.
      </h3>
      </article>
  </section>
</template>
<script> 
export default {
	props: [ 'results', 'input', 'city', 'cityItems' ],
  data() {
    return {}
  },
	methods: {
		showModal(city, type) {
			this.$emit('showModal', city, type);
		},
    addResults() {
      this.$emit('addResults');
    },
    showMore() {
      return this.cityItems.length < this.results.length && this.cityItems.length;
    }
  },
  filters: {
    formattedNumber(x) {
      return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ', ');
    }
  }
}
</script>

