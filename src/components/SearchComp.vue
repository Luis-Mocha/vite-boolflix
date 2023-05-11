<script>
import axios from 'axios';
import { store } from '../store';

export default {
    name: 'SearchComp',
    data() {
        return {
            store
        }
    },
    methods: {     
        
        apiSearchFunction() {
            // Movies
            if (store.searchValue !== '') {
                axios.get( `https://api.themoviedb.org/3/search/movie?${store.ApiPath}&query=${store.searchValue}&language=it_IT`)
                    .then( (res) => {
                    console.log(res.data)

                    store.arrayMovies = res.data;
                });
            }
            else {
                console.log('Non hai scritto niente');
                store.arrayMovies = []
            };

            // Tv series
            if (store.searchValue !== '') {
                axios.get( `https://api.themoviedb.org/3/search/tv?${store.ApiPath}&query=${store.searchValue}&language=it_IT`)
                    .then( (res) => {
                    console.log(res.data)

                    store.arrayTv = res.data;
                });
            }
            else {
                console.log('Non hai scritto niente');
                store.arrayTv = []
            };
        },

    } //fine methods
}
    
</script>


<template>

    <div class="d-flex align-items-center">

        <div class="input-gruppo">
            <span class="input-icon" id="basic-addon1"  @click="apiSearchFunction()">
                <i class="fa-solid fa-magnifying-glass"></i>
            </span>
            <input type="search" class="search-input" placeholder="Cerca un titolo..." aria-label="Titoli" aria-describedby="basic-addon1" name="search-input" v-model="store.searchValue" @keyup.enter="apiSearchFunction()" @keyup="apiSearchFunction()">
        </div>

    </div>

</template>

<style lang="scss" scoped>
@import "../style/main.scss";
    .input-gruppo {
        // width: min-content;
        display: flex;
        border: 1px solid white;
        .input-icon {
            display: flex;
            align-items: center;
            padding: 0 10px;
            cursor: pointer;
        }
        .search-input {
            color: white;
            border: none;
            padding: 10px 15px;
            background-color: transparent;
            outline: none;
        }
    }

</style>