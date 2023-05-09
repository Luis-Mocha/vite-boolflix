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
                axios.get( `https://api.themoviedb.org/3/search/movie?${store.ApiPath}&query=${store.searchValue}&language=it_IT`)
                    .then( (res) => {
                    console.log(res.data.results) 
                    
                    const infoMovies = res.data.results;
                    store.arrayMovies = infoMovies;


                    store.arrayMovies.forEach(element => {
                    // modifico i codici lingua non riconosciuti dall'api per le bandiere
                        if (element.original_language === 'en') {
                            element.original_language = 'gb'
                        }
                        else if (element.original_language === 'ko') {
                            element.original_language = 'kr'
                        }
                        else if (element.original_language === 'da') {
                            element.original_language = 'dk'
                        }
                        else if (element.original_language === 'ja') {
                            element.original_language = 'jp'
                        };

                        // moddifico le date
                        const newFormat = element.release_date.split('-');
                        element.release_date = `${newFormat[2]}-${newFormat[1]}-${newFormat[0]}`;

                        //Modifico i voti
                        const newVote = Math.ceil((element.vote_average  * 5 / 10));
                        element.vote_average = newVote;
                    })

                });

                
                
            
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