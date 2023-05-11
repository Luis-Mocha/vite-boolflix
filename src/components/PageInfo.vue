<script>
import axios from 'axios';
import { store } from '../store';

export default {
    name: "PageInfo",
    props: ["info" , "infoTipo"],
    data() {
        return {
            store
        };
    },
    methods: {
        nextPage() {
            if (this.infoTipo === 'movie') {

                if (this.info.page === this.info.total_pages) {
                    axios.get( `https://api.themoviedb.org/3/search/movie?${store.ApiPath}&query=${store.searchValue}&language=it_IT&page=1`)
                    .then( (res) => {
                    console.log(res.data) 

                    store.arrayMovies = res.data;
                    });
                } else {
                    axios.get( `https://api.themoviedb.org/3/search/movie?${store.ApiPath}&query=${store.searchValue}&language=it_IT&page=${this.info.page + 1}`)
                    .then( (res) => {
                    console.log(res.data) 

                    store.arrayMovies = res.data;
                    });
                }
            
            } else {
                if (this.info.page === this.info.total_pages) {
                    axios.get( `https://api.themoviedb.org/3/search/tv?${store.ApiPath}&query=${store.searchValue}&language=it_IT&page=1`)
                    .then( (res) => {
                    console.log(res.data) 

                    store.arrayTv= res.data;
                    });
                } else {
                    axios.get( `https://api.themoviedb.org/3/search/tv?${store.ApiPath}&query=${store.searchValue}&language=it_IT&page=${this.info.page + 1}`)
                    .then( (res) => {
                    console.log(res.data) 

                    store.arrayTv= res.data;
                    }); 
                } 
            }
        },

        prevPage() {
            if (this.infoTipo === 'movie') {

                if (this.info.page === 1) {
                    axios.get( `https://api.themoviedb.org/3/search/movie?${store.ApiPath}&query=${store.searchValue}&language=it_IT&page=${this.info.total_pages}`)
                    .then( (res) => {
                    console.log(res.data) 

                    store.arrayMovies = res.data;
                    });
                } else {
                    axios.get( `https://api.themoviedb.org/3/search/movie?${store.ApiPath}&query=${store.searchValue}&language=it_IT&page=${this.info.page - 1}`)
                    .then( (res) => {
                    console.log(res.data) 

                    store.arrayMovies = res.data;
                    });
                }
            
            } else {
                if (this.info.page === 1) {
                    axios.get( `https://api.themoviedb.org/3/search/tv?${store.ApiPath}&query=${store.searchValue}&language=it_IT&page=${this.info.total_pages}`)
                    .then( (res) => {
                    console.log(res.data) 

                    store.arrayTv= res.data;
                    });
                } else {
                    axios.get( `https://api.themoviedb.org/3/search/tv?${store.ApiPath}&query=${store.searchValue}&language=it_IT&page=${this.info.page - 1}`)
                    .then( (res) => {
                    console.log(res.data) 

                    store.arrayTv= res.data;
                    }); 
                } 
            }
        },
            
    },
}

</script>

<template>

    <div class="info-pagina mb-2">
        <span>Hai cercato "{{ store.searchValue }}"</span>
        <span>Risultati totali: {{ this.info.total_results }}</span>
        <div class="d-inline" v-if="info.total_results != 0">
            <span>
                <i class="fa-solid fa-angle-left" @click="prevPage()"></i>
            </span>
            <span>Pagina {{this.info.page}} di {{this.info.total_pages}}</span>
            <span>
                <i class="fa-solid fa-angle-right" @click="nextPage()"></i>
            </span>
        </div>
        
    </div>

</template>

<style lang="scss" scoped>

@import "../style/main.scss";

</style>