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

        <div class="slider"> 
            <SingleTv
            v-for="(elem, index) in store.arrayTv" :key="index"
            :infoTv="elem"
            />
        </div>
    </div>

</template>

<style lang="scss" scoped>
@import "../style/main.scss";
     

</style>