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

    <div id="tvSection">
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

    #tvSection {
        // border: 1px solid red;
        color: white;

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