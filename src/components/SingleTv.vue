<script>
import { defineComponent } from 'vue';


export default {
    name: "SingleTv",
    props: ["infoTv"],
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
            <img :src=" `https://image.tmdb.org/t/p/w500/${infoTv.poster_path}` " :alt="infoTv.title">
        </div>


        <div class="card-info" :class="(infoControl === true) ? 'open' : '' ">

            <!-- titolo -->
            <h3 class="text-center">
                {{infoTv.title}}
            </h3>

            <!-- titolo originale -->
            <div v-if="infoControl === true && infoTv.title != infoTv.original_title " >
                <span>Titolo originale:</span>
                <div class="ms-2">
                    {{infoTv.original_title}}
                </div>
            </div>

            <!-- lingua -->
            <div v-if="infoControl === true">
                <span>Lingua Originale:</span>
                <!-- <span class="ms-2">
                    {{infoTv.original_language}}
                </span> -->
                <img :src="`https://flagcdn.com/24x18/${infoTv.original_language}.webp`" alt="Icona lingua originale" class="d-block mx-auto">
            </div>

            <!-- data -->
            <div v-if="infoControl === true">
                <span>Data Uscita</span>
                <div class="ms-2">
                    {{infoTv.first_air_date}}
                </div>
            </div>

            <!-- voto -->
            <div v-if="infoControl === true">
                <span>Voto:</span>
                <span>({{infoTv.vote_average}})</span>
                <br>
                <i class="fa-solid fa-star" style="color: #ffd22e;" v-for="n in infoTv.vote_average"></i>
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
        //border: 1px solid white;
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