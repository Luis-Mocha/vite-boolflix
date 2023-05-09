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
        
        <SingleMovie
        v-for="(elem, index) in store.arrayMovies" :key="index"
        :infoMovies="elem" :infoIndex="index"
        />

    </div>

</template>

<style lang="scss" scoped>
@import "../style/main.scss";

</style>