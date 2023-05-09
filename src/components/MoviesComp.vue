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

    <div id="movieSection">
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

    #movieSection {
        // border: 1px solid red;
        color: white;
        margin-bottom: 50px;

        h2 {
            text-transform: uppercase;
            font-size: 40px;
            margin-bottom: 10px;
        }
        .slider {
            // border: 1px solid yellow;
            display: flex;        
            height: 500px;
            overflow: auto;
        }
    }      

</style>