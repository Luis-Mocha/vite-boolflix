<script>
import axios from 'axios';
import { store } from '../store';
import MoviesComp from './MoviesComp.vue';
import TvComp from './TvComp.vue';
import PopularMovies from './PopularMovies.vue';
import PopularTv from './PopularTv.vue';

export default {
    name: 'AppMain',
    components: {
        MoviesComp,
        TvComp,
        PopularMovies,
        PopularTv,
    },
    data() {
        return {
            store
        }
    },
    created() {
        this.apiPopularMovies()
        this.apiPopularTv()
    },
    methods : {

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

        //api film popolari
        apiPopularMovies() {
            let infoMovies;
            
            axios.get( `https://api.themoviedb.org/3/discover/movie?include_adult=false&include_video=false&language=en-US&page=1&sort_by=popularity.desc&${store.ApiPath}`)
                .then( (res) => {
                console.log(res.data.results) 
                
                infoMovies = res.data.results;

                infoMovies.forEach(element => {
                    // modifico i codici lingua non riconosciuti dall'api per le bandiere
                    this.changeFlag(element)

                    // moddifico le date
                    const newFormat = element.release_date.split('-');
                    element.release_date = `${newFormat[2]}-${newFormat[1]}-${newFormat[0]}`;

                    //Modifico i voti
                    const newVote = Math.ceil((element.vote_average  * 5 / 10));
                    element.vote_average = newVote;

                })
                store.arrayPopularMovies = infoMovies;
                console.log(store.arrayPopularMovies);
            });
        },

        // serie tv popolari
        apiPopularTv() {
            let infoMovies;
            
            axios.get( `https://api.themoviedb.org/3/discover/tv?include_adult=false&include_video=false&language=en-US&page=1&sort_by=popularity.desc&${store.ApiPath}`)
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
                store.arrayPopularTv = infoMovies;
                console.log(store.arrayPopularTv);
            });
        },

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

    }
}
    
</script>


<template>

    <main>
        
        <MoviesComp v-if="store.arrayMovies != '' " 
        @emitNextPage="nextPage()"
        @emitPrevPage="prevPage()"
        />

        <TvComp v-if="store.arrayTv != '' "/>

        <PopularMovies/>

        <PopularTv/>

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