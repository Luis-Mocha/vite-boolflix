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
        apiSearchMovies() {
            if (store.searchValue !== '') {
                axios.get( `https://api.themoviedb.org/3/search/movie?${store.ApiPath}&query=${store.searchValue}`)
                .then( (res) => {
                console.log(res.data) 
                
                const infoMovies = res.data;
                store.arrayMovies = infoMovies;
            }) 
            }
            else {
                console.log('Non hai scritto niente');
            }
        },
    }
}
    
</script>


<template>

    <div class="d-flex align-items-center">

        <div class="input-gruppo">
            <span class="input-icon" id="basic-addon1" @click="apiSearchMovies()">
                <i class="fa-solid fa-magnifying-glass"></i>
            </span>
            <input type="search" class="search-input" placeholder="Cerca un titolo..." aria-label="Titoli" aria-describedby="basic-addon1" name="search-input" v-model="store.searchValue" @keyup.enter="apiSearchMovies()">
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