<script>
import axios from 'axios';
import { store } from '../store';
import SingleCard from './SingleCard.vue';
import PageInfo from './PageInfo.vue';

export default {
    name: 'AppMain',
    components: {
        SingleCard,
        PageInfo,
    },
    data() {
        return {
            store
        }
    },
    created() {
        this.apiGetPopular()
    },
    methods : {

        apiGetPopular() {
            // Movies
            axios.get(`https://api.themoviedb.org/3/discover/movie?include_adult=false&include_video=false&language=en-US&page=1&sort_by=popularity.desc&${store.ApiPath}`)
            // axios.get( `https://api.themoviedb.org/3/discover/movie?include_adult=false&include_video=false&language=en-US&page=1&sort_by=popularity.desc&${store.ApiPath}`)
                .then( (res) => {
                console.log(res.data)

                store.arrayPopularMovies = res.data;
            });
            
            // Tv series
            axios.get(`https://api.themoviedb.org/3/discover/tv?include_adult=false&include_video=false&language=en-US&page=1&sort_by=popularity.desc&${store.ApiPath}`)
                .then( (res) => {
                console.log(res.data)

                store.arrayPopularTv = res.data;
            });
        },

        // Movies Funzione per cambiare pagina
        nextPageMovie(parTipo, parArray) {

            axios.get( `https://api.themoviedb.org/3/search/${parTipo}?${store.ApiPath}&query=${store.searchValue}&language=it_IT&page=${parArray.page + 1}`)
            // axios.get( `https://api.themoviedb.org/3/discover/movie?include_adult=false&include_video=false&language=en-US&page=1&sort_by=popularity.desc&${store.ApiPath}`)
                .then( (res) => {
                console.log(res.data) 
                
                infoMovies = res.data;

                store.arrayMovies = infoMovies;
            });
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

        scrollHorizontal(e, elemHtml) {

            const slider = document.getElementById(elemHtml)

            if (e.deltaY > 0) {
                slider.scrollLeft += 100
            } else {
                slider.scrollLeft -= 100
            }
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

            <PageInfo :info="store.arrayMovies" :infoTipo="'movie'"/>

            <div id="slider-film" @wheel.prevent="scrollHorizontal($event, 'slider-film')" class="slider row flex-nowrap overflow-x-hidden" v-if="store.arrayMovies.results != 0"> 
                <SingleCard
                v-if="store.arrayMovies.results.length"
                v-for="(elem, index) in store.arrayMovies.results" :key="index"
                :info="elem"
                />
            </div>
        </div>

        <div id="tvSection" class="main-section" v-if="store.searchValue">
            <h2>
            Tv Series
            </h2>

            <PageInfo :info="store.arrayTv" :infoTipo="'tv'"/>

            <div id="slider-tv" @wheel.prevent="scrollHorizontal($event, 'slider-tv')" class="slider row flex-nowrap overflow-x-hidden" v-if="store.arrayTv.results != 0"> 
                <SingleCard
                v-for="(elem, index) in store.arrayTv.results" :key="index"
                :info="elem"
                />
            </div>
        </div>

        <div id="popMovieSection" class="main-section">
            <h2>
                Popular Movies
            </h2>

            <div id="slider-popfilm" @wheel.prevent="scrollHorizontal($event, 'slider-popfilm')" class="slider row flex-nowrap overflow-x-hidden"> 
                <SingleCard
                v-for="(elem, index) in store.arrayPopularMovies.results" :key="index"
                :info="elem"
                />
            </div>
        </div>

        <div id="popTvSection" class="main-section">
            <h2>
                Popular TvSeries
            </h2>

            
            <div id="slider-poptv" @wheel.prevent="scrollHorizontal($event, 'slider-poptv')" class="slider row flex-nowrap overflow-x-hidden position-relative"> 
                <SingleCard
                v-for="(elem, index) in store.arrayPopularTv.results" :key="index"
                :info="elem"
                />
            </div>
        </div>

    </main>
    
</template>

<style lang="scss" scoped>
    @import "../style/main.scss";

    main {
        background-color: black;
        min-height: calc(100vh - 100px);
        padding: 20px 0;
    }
</style>