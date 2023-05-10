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
            let infoMovies;
            if (store.searchValue !== '') {
                axios.get( `https://api.themoviedb.org/3/search/movie?${store.ApiPath}&query=${store.searchValue}&language=it_IT`)
                // axios.get( `https://api.themoviedb.org/3/discover/movie?include_adult=false&include_video=false&language=en-US&page=1&sort_by=popularity.desc&${store.ApiPath}`)
                    .then( (res) => {
                    console.log(res.data) 
                    
                    infoMovies = res.data;

                    infoMovies.results.forEach(element => {
                        // modifico i codici lingua non riconosciuti dall'api per le bandiere
                        this.changeFlag(element)

                        // moddifico le date
                        const newFormat = element.release_date.split('-');
                        element.release_date = `${newFormat[2]}-${newFormat[1]}-${newFormat[0]}`;

                        //Modifico i voti
                        const newVote = Math.ceil((element.vote_average  * 5 / 10));
                        element.vote_average = newVote;

                    })
                    store.arrayMovies = infoMovies;
                });

            }
            else {
                console.log('Non hai scritto niente');
                store.arrayMovies = []
            };
        },

        apiSearchTv() {
            let infoMovies;
            if (store.searchValue !== '') {
                axios.get( `https://api.themoviedb.org/3/search/tv?${store.ApiPath}&query=${store.searchValue}&language=it_IT`)
                    .then( (res) => {
                    console.log(res.data.results) 
                    
                    infoMovies = res.data.results;

                    infoMovies.forEach(element => {
                        // modifico i codici lingua non riconosciuti dall'api per le bandiere
                        this.changeFlag(element)

                        // moddifico le date
                        const newFormat = element.first_air_date.split('-');
                        element.first_air_date = `${newFormat[2]}-${newFormat[1]}-${newFormat[0]}`;

                        //Modifico i voti
                        const newVote = Math.ceil((element.vote_average  * 5 / 10));
                        element.vote_average = newVote;

                    })
                    store.arrayTv = infoMovies;
                });

            }
            else {
                console.log('Non hai scritto niente');
                store.arrayTv = []
            };
        },

        // modifico i codici lingua non riconosciuti dall'api per le bandiere
        changeFlag(par) {
            if (par.original_language === 'en') {
                par.original_language = 'gb'
            }
            else if (par.original_language === 'ko') {
                par.original_language = 'kr'
            }
            else if (par.original_language === 'da') {
                par.original_language = 'dk'
            }
            else if (par.original_language === 'ja') {
                par.original_language = 'jp'
            };
        },

    } //fine methods
}
    
</script>


<template>

    <div class="d-flex align-items-center">

        <div class="input-gruppo">
            <span class="input-icon" id="basic-addon1" @click="apiSearchMovies() ; apiSearchTv()">
                <i class="fa-solid fa-magnifying-glass"></i>
            </span>
            <input type="search" class="search-input" placeholder="Cerca un titolo..." aria-label="Titoli" aria-describedby="basic-addon1" name="search-input" v-model="store.searchValue" @keyup.enter="apiSearchMovies() ; apiSearchTv()" @keyup="apiSearchMovies() ; apiSearchTv()">
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