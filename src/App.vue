<script>
import axios from 'axios';
import {store} from './store';
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';

export default {
  name: 'app',
  components: {
    AppHeader,
    AppMain,
  },

  data() {
    return {
      store
    }
  },

  created() {
  },
  
  computed: {
  },
  methods: {
    apiSearchMovies() {
      axios.get( `https://api.themoviedb.org/3/search/movie?${store.ApiPath}&query=${store.searchValue}`)
        .then( (res) => {
          console.log(res.data) 
        
          const infoMovies = res.data;
          store.arrayMovies = infoMovies;
      })
    },
  }
}

</script>

<template>

  <AppHeader/>

  <AppMain/>

</template>

<style lang="scss">
@use './style/main.scss';
</style>
