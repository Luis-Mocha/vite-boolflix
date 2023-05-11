<script>
import { store } from '../store';
import SingleTv from './SingleTv.vue';

export default {
    name: 'TvComp',
    components: {
        SingleTv,
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

    <div id="tvSection" class="main-section">
        <h2>
            Tv series
        </h2>

        <div class="info-pagina mb-2">
            <span>Hai cercato "{{ store.searchValue }}"</span>
            <span>Risultati totali: {{ store.arrayTv.total_results }}</span>
            <span>
                <i class="fa-solid fa-angle-left" @click="$emit('emitPrevPage')"></i>
            </span>
            <span>Pagina {{store.arrayTv.page}} di {{store.arrayTv.total_pages}}</span>
            <span>
                <i class="fa-solid fa-angle-right" @click="$emit('emitNextPage')"></i>
            </span>
        </div>

        <div class="slider"> 
            <SingleTv
            v-for="(elem, index) in store.arrayTv.results" :key="index"
            :infoTv="elem"
            />
        </div>
    </div>

</template>

<style lang="scss" scoped>
@import "../style/main.scss";

</style>