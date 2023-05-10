<script>
import { store } from '../store';
import SingleMovie from '../components/SingleMovie.vue'

export default {
    name: 'MoviesComp',
    components: {
        SingleMovie,
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
            Movies
        </h2>

        <div class="slider"> 
            <SingleMovie
            v-for="(elem, index) in store.arrayMovies" :key="index"
            :infoMovies="elem" :infoIndex="index"
            />
        </div>
    </div>

</template>

<style lang="scss" scoped>
@import "../style/main.scss";
     

</style>