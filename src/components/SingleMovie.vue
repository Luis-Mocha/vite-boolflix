<script>
import { defineComponent } from 'vue';


export default {
    name: "SingleMovie",
    props: ["infoMovies", "infoIndex"],
    data() {
        return {
            infoControl: false,
        };
    },
    created() {
    },
    methods: {
        openCloseInfo() {
            if (this.infoControl === false) {
                this.infoControl = true;
            }
            else {
                this.infoControl = false;
            }
        },
    },
}
    
</script>


<template>
    <div class="movie-card col-6 col-md-4 col-lg-2" @mouseover="infoControl = true" @mouseleave="infoControl = false">

        <div class="card-img" v-if="infoControl === false">
            <img :src=" `https://image.tmdb.org/t/p/w500/${infoMovies.poster_path}` " :alt="infoMovies.title">
        </div>
        

        <div class="card-info" :class="(infoControl === true) ? 'open' : '' ">

            <!-- titolo -->
            <h3 class="text-center">
                {{infoMovies.title}}
            </h3>

            <!-- titolo originale -->
            <div v-if="infoControl === true && infoMovies.title != infoMovies.original_title " >
                <span>Titolo originale:</span>
                <div class="ms-2">
                    {{infoMovies.original_title}}
                </div>
            </div>

            <!-- lingua -->
            <div v-if="infoControl === true">
                <span>Lingua Originale:</span>
                <span class="ms-2">
                    {{infoMovies.original_language}}
                </span>
            </div>

            <!-- voto -->
            <div v-if="infoControl === true">
                <span>Voto:</span>
                <div>
                    {{infoMovies.vote_average}}
                </div>
            </div>

            
        </div>

        <button @click="openCloseInfo()">
            <i class="fa-solid fa-chevron-up" v-if="infoControl === false"></i>
            <i class="fa-solid fa-chevron-down" v-else></i>
        </button>

    </div>
</template>

<style lang="scss" scoped>
    .movie-card {
        // border: 1px solid white;
        padding: 0 20px;
        height: 100%;
        cursor: pointer;
        
        display: flex;
        flex-direction: column;

        .card-img {
            height: 70%;
            display: flex;
            justify-content: center;

            img {
                height: 100%;
                display: block;
                cursor: pointer;
            }
        }

        .card-info {
            padding-top: 10px;
            height: 20%;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: space-evenly;
            color: white;
            
            h3 {
                overflow: hidden;
            }

            div {
                text-align: center;
            }

        }

        button {
            height: 10%;
            color: white;
            background-color: black;
            border: none;
            font-size: 22px;
            &:hover {
                color: red;
            }
        }

        //quando le info sono aperte
        .card-info.open {
            height: 90%;
            border: 1px solid red;
        }

    }

</style>