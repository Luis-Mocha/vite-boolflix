<script>
import { store } from '../store';
import SinglePopularMovie from './SinglePopularMovie.vue';

export default {
    name: 'PopularMovies',
    components: {
        SinglePopularMovie,
    },
    data() {
        return {
            store
        }
    },
    methods: {

    }
}
    
</script>


<template>

    <div id="movieSection" class="main-section">
        <h2>
            Popular Movies
        </h2>

        <div class="slider"> 
            <SinglePopularMovie
            v-for="(elem, index) in store.arrayPopularMovies" :key="index"
            :infoMovies="elem" :infoIndex="index"
            />
        </div>
    </div>

</template>

<style lang="scss" scoped>
@import "../style/main.scss";
     

</style>