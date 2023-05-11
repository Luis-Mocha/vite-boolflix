<script>
import axios from 'axios';
import { store } from '../store';
import SingleCard from './SingleCard.vue';
import PopularMovies from './PopularMovies.vue';
import PopularTv from './PopularTv.vue';

export default {
    name: 'AppMain',
    components: {
        PopularMovies,
        PopularTv,
        SingleCard,
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

        // Movies Funzione per cambiare pagina
        nextPageMovie(parTipo, parArray) {
            let infoMovies;
            if (store.searchValue !== '') {
                axios.get( `https://api.themoviedb.org/3/search/${parTipo}?${store.ApiPath}&query=${store.searchValue}&language=it_IT&page=${parArray.page + 1}`)
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

        prevPageMovie(parTipo, parArray) {
            let infoMovies;
            if (store.searchValue !== '') {
                axios.get( `https://api.themoviedb.org/3/search/${parTipo}?${store.ApiPath}&query=${store.searchValue}&language=it_IT&page=${parArray.page - 1}`)
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

        // Tv series Funzione per cambiare pagina
        nextPageTv(parTipo, parArray) {
            let infoMovies;
            if (store.searchValue !== '') {
                axios.get( `https://api.themoviedb.org/3/search/${parTipo}?${store.ApiPath}&query=${store.searchValue}&language=it_IT&page=${parArray.page + 1}`)
                // axios.get( `https://api.themoviedb.org/3/discover/movie?include_adult=false&include_video=false&language=en-US&page=1&sort_by=popularity.desc&${store.ApiPath}`)
                    .then( (res) => {
                    console.log(res.data) 
                    
                    infoMovies = res.data;

                    infoMovies.results.forEach(element => {
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
                store.arrayMovies = []
            };
        },

        prevPageTv(parTipo, parArray) {
            let infoMovies;
            if (store.searchValue !== '') {
                axios.get( `https://api.themoviedb.org/3/search/${parTipo}?${store.ApiPath}&query=${store.searchValue}&language=it_IT&page=${parArray.page - 1}`)
                // axios.get( `https://api.themoviedb.org/3/discover/movie?include_adult=false&include_video=false&language=en-US&page=1&sort_by=popularity.desc&${store.ApiPath}`)
                    .then( (res) => {
                    console.log(res.data) 
                    
                    infoMovies = res.data;

                    infoMovies.results.forEach(element => {
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
                store.arrayMovies = []
            };
        },

    }
}
    
</script>


<template>

    <main>

        <div id="movieSection" class="main-section" v-if="store.searchValue">
            <h2>
            Movies
            </h2>

            <div class="info-pagina mb-2">
                <span>Hai cercato "{{ store.searchValue }}"</span>
                <span>Risultati totali: {{ store.arrayMovies.total_results }}</span>
                <span>
                    <i class="fa-solid fa-angle-left" @click="prevPageMovie('movie', store.arrayMovies)"></i>
                </span>
                <span>Pagina {{store.arrayMovies.page}} di {{store.arrayMovies.total_pages}}</span>
                <span>
                    <i class="fa-solid fa-angle-right" @click="nextPageMovie('movie', store.arrayMovies)"></i>
                </span>
            </div>
            

            <div class="slider"> 
                <SingleCard
                v-for="(elem, index) in store.arrayMovies.results" :key="index"
                :info="elem"
                />
            </div>
        </div>

        <div id="tvSection" class="main-section" v-if="store.searchValue">
            <h2>
            Tv Series
            </h2>

            <div class="info-pagina mb-2">
                <span>Hai cercato "{{ store.searchValue }}"</span>
                <span>Risultati totali: {{ store.arrayTv.total_results }}</span>
                <span>
                    <i class="fa-solid fa-angle-left" @click="prevPageTv('tv', store.arrayTv)"></i>
                </span>
                <span>Pagina {{store.arrayTv.page}} di {{store.arrayTv.total_pages}}</span>
                <span>
                    <i class="fa-solid fa-angle-right" @click="nextPageTv('tv', store.arrayTv)"></i>
                </span>
            </div>
            

            <div class="slider"> 
                <SingleCard
                v-for="(elem, index) in store.arrayTv.results" :key="index"
                :info="elem"
                />
            </div>
        </div>

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