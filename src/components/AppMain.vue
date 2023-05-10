<script>
import { store } from '../store';
import MoviesComp from './MoviesComp.vue';
import TvComp from './TvComp.vue';

export default {
    name: 'AppMain',
    components: {
        MoviesComp,
        TvComp,
    },
    data() {
        return {
            store
        }
    },
}
    
</script>


<template>

    <main>
        
        <MoviesComp v-if="store.arrayMovies != '' "/>

        <TvComp v-if="store.arrayTv != '' "/>

    </main>
    
</template>

<style lang="scss" scoped>
    @import "../style/main.scss";

    main {
        background-color: black;
        min-height: calc(100vh - 100px);
        padding: 20px;
    }
</style>