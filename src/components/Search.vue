<template>
  <div class="search">
    <h2>Type In Your Search Term</h2>
    <form v-on:submit.prevent="getResult(query)">
      <input type="text" placeholder="Type in your search" v-model="query">
    </form>
    <div class="results" v-if="results">

      <div v-for="result in results">
        <img width="250px" v-bind:src="result.strMealThumb" />
        <h1 v-bind:title="result.strMeal"></h1>
        <p v-bind:caption="result.strTags"></p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'search',
  data () {
    return {
      msg: 'Search',
      query: '',
      results: ''
    }
  },
  methods: {
    getResult (query) {
      axios.get('https://www.themealdb.com/api/json/v1/1/search.php?s=' + query).then(response => {
        console.log(response.data.meals)
        this.results = response.data.meals
      })
    }
  }
}
</script>

<style scoped>
.result img {
  height: 300px;
  margin: 10px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

</style>
