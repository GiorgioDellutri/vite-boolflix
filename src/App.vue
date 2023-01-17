<script>
import AppMain from './components/AppMain.vue';
import AppHeader from './components/AppHeader.vue';
import axios from 'axios';
import { store } from './store';

export default {
  components: {
    AppMain,
    AppHeader,
  },

  data() {
    return {
      store,
      apiUrl: 'https://api.themoviedb.org/3/search/movie',
      apiKey: '0a31e483fb79ecbceb90e01e63e05acf'
    }
  },
  methods: {
    getMovies(searchedQuery,) {
      axios.get(this.apiUrl, {
        params: {
          api_key: this.apiKey,
          query: searchedQuery
        }
      })
        .then((response) => {
          console.log(response.data.results);
          this.store.moviesData = response.data.results
        })
        .catch(function (error) {
          console.log(error);
        })
    },
    test() {
      alert('TEST')
    }
  },

  created() {
    this.getMovies()
  },
}
</script>

<template>
  <header>
    <AppHeader @search="getMovies" />
  </header>
  <main>
    <AppMain />
  </main>
</template>

<style lang="scss">
@use './styles/general.scss' as *;
@use './styles/partials/variables' as *;
@import 'bootstrap/scss/bootstrap.scss';
</style>
