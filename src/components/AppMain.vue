<script>
import { store } from '../store';
import MoviesComp from './MoviesComp.vue';

export default {
    name: 'AppMain',
    components: {
        MoviesComp,
    },
    data() {
        return {
            store
        }
    },
}
    
</script>


<template>

    <main class="border">
        
        <MoviesComp/>

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