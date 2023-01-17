<script >
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
      moviesApiUrl: 'https://api.themoviedb.org/3/search/movie',
      tvShowApiKey: 'https://api.themoviedb.org/3/search/tv',
      apiKey: '0a31e483fb79ecbceb90e01e63e05acf'
    }
  },

  methods: {
    getMovies(searchedQuery) {
      const firstApiPromise = axios.get(this.moviesApiUrl, {
        params: {
          api_key: this.apiKey,
          query: searchedQuery
        }
      });
      const secondApiPromise = axios.get(this.tvShowApiKey, {
        params: {
          api_key: this.apiKey,
          query: searchedQuery
        }
      });
      Promise.all([firstApiPromise, secondApiPromise])
        .then(([firstResponse, secondResponse]) => {
          console.log(firstResponse.data.results, secondResponse.data.results);
          this.store.moviesData = firstResponse.data.results
          this.store.tvShowData = secondResponse.data.results;
        })
        .catch(function (error) {
          console.log(error);
        });
    }
  },

  created() {

  }
}

</script>

<template>
  <header>
    <AppHeader />
  </header>
  <main>
    <AppMain @search="getMovies" />
  </main>
</template>

<style lang="scss">
@use './styles/general.scss' as *;
@use './styles/partials/variables' as *;
@import 'bootstrap/scss/bootstrap.scss';
</style>
