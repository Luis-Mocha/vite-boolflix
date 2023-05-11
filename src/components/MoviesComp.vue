<script>
import axios from 'axios';
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

        <div class="info-pagina mb-2">
            <span>Hai cercato "{{ store.searchValue }}"</span>
            <span>Risultati totali: {{ store.arrayMovies.total_results }}</span>
            <span>
                <i class="fa-solid fa-angle-left" @click="$emit('emitPrevPage')"></i>
            </span>
            <span>Pagina {{store.arrayMovies.page}} di {{store.arrayMovies.total_pages}}</span>
            <span>
                <i class="fa-solid fa-angle-right" @click="$emit('emitNextPage')"></i>
            </span>
        </div>
        

        <div class="slider"> 
            <SingleMovie
            v-for="(elem, index) in store.arrayMovies.results" :key="index"
            :infoMovies="elem" :infoIndex="index"
            />
        </div>
    </div>

</template>

<style lang="scss" scoped>
@import "../style/main.scss";

</style>