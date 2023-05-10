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
        // Funzione per cambiare pagina
        nextPage() {
            let infoMovies;
            if (store.searchValue !== '') {
                axios.get( `https://api.themoviedb.org/3/search/movie?${store.ApiPath}&query=${store.searchValue}&language=it_IT&page=${store.arrayMovies.page + 1}`)
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

        prevPage() {
            let infoMovies;
            if (store.searchValue !== '') {
                axios.get( `https://api.themoviedb.org/3/search/movie?${store.ApiPath}&query=${store.searchValue}&language=it_IT&page=${store.arrayMovies.page - 1}`)
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
    }
}
    
</script>


<template>

    <div id="movieSection" class="main-section">
        <h2>
            Movies
        </h2>

        <div class="mb-2">
            <span>Hai cercato "{{ store.searchValue }}"</span>
            <span>Risultati totali: {{ store.arrayMovies.total_results }}</span>
            <span>
                <i class="fa-solid fa-angle-left" @click="prevPage()"></i>
            </span>
            <span>Pagina {{store.arrayMovies.page}} di {{store.arrayMovies.total_pages}}</span>
            <span>
                <i class="fa-solid fa-angle-right" @click="nextPage()"></i>
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
     span {
        margin-right: 10px;
        
        i{
            cursor: pointer;
            &:hover {
                color: red;
            }
        }
     }

</style>