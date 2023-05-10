<script>
import { store } from '../store';
import SinglePopularTv from './SinglePopularTv.vue';

export default {
    name: 'PopularTv',
    components: {
        SinglePopularTv,
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

    <div id="popularTvSection" class="main-section">
        <h2>
            Popular Tv Series
        </h2>

        <div class="slider"> 
            <SinglePopularTv
            v-for="(elem, index) in store.arrayPopularTv" :key="index"
            :infoTv="elem" :infoIndex="index"
            />
        </div>
    </div>

</template>

<style lang="scss" scoped>
@import "../style/main.scss";
     

</style>