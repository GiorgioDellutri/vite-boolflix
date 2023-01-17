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
    }
  },
  methods: {
    getCardList() {
      axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php?num=50&offset=0', {
        params: {
        }
      })
        .then((response) => {
          console.log(response.data.data);
          this.store.cardList = response.data.data;
          console.log(this)

        })
        .catch(function (error) {
          console.log(error);
        })
    }
  },

  created() {
  },
}
</script>

<template>
  <header>
    <AppHeader />
  </header>
  <main>
    <AppMain />
  </main>
</template>

<style lang="scss">
@use './styles/general.scss' as *;
@use './styles/partials/variables' as *;
</style>
