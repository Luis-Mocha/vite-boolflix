<script>

export default {
    name: "SingleCard",
    props: ["info"],
    data() {
        return {
            openControl: false,
            titleControl: false,
        };
    },
    methods: {
        openCloseInfo() {
            if (this.openControl === false) {
                this.openControl = true;
            }
            else {
                this.openControl = false;
            }
        },

        getTitle() {
            if (this.info.title) {
                return this.info.title
            }
            else {
                return this.info.name
            }
        },

        getOriginalTitle() {
            if (this.info.original_title) {
                return this.info.original_title
            }
            else {
                return this.info.original_name
            }
        },

        getDate() {
            if (this.info.release_date) {
                const newFormat = this.info.release_date.split('-');
                this.info.release_date = `${newFormat[2]}-${newFormat[1]}-${newFormat[0]}`;

                return this.info.release_date
            }
            else {
                const newFormat = this.info.first_air_date.split('-');
                this.info.first_air_date = `${newFormat[2]}-${newFormat[1]}-${newFormat[0]}`;

                return this.info.first_air_date
            }
        },

        getPoster(x) {
            if (x) {
             return `https://image.tmdb.org/t/p/w342/${x}`
            } else {
             return 'img/image-placeholder.png'
            }
        },

        changeFlag() {
            if (this.info.original_language === 'en') {
                this.info.original_language = 'gb'
            }
            else if (this.info.original_language === 'ko') {
                this.info.original_language = 'kr'
            }
            else if (this.info.original_language === 'da') {
                this.info.original_language = 'dk'
            }
            else if (this.info.original_language === 'ja') {
                this.info.original_language = 'jp'
            }
            else if (this.info.original_language === 'cs') {
                this.info.original_language = 'cz'
            }
            else {
                return this.info.original_language
            } 
        },

        changeVote() {
            return Math.ceil((this.info.vote_average  * 5 / 10));
        },

    },
}
    
</script>


<template>
    <div class="my-card" @mouseover="openControl = true" @mouseleave="openControl = false"> <!--col-6 col-md-4 col-lg-2-->

        <div class="card-img" v-if="openControl === false">
            <!-- <img :src=" `https://image.tmdb.org/t/p/w342/${info.poster_path}` " :alt="info.title"> -->
            <!-- <img :src="'img/image-placeholder.png'"> -->
            <img :src="getPoster(info.poster_path)" alt="">
        </div>
        

        <div class="card-info" :class="(openControl === true) ? 'open' : '' ">

            <!-- titolo -->
            <h3 class="text-center">
                {{getTitle()}}
            </h3>

            <!-- titolo originale -->
            <!-- && info.title != info.original_title -->
            <div v-if="openControl === true ">
                <span>Titolo originale:</span>
                <div class="ms-2">
                    {{getOriginalTitle()}}
                </div>
            </div>

            <!-- lingua -->
            <div v-if="openControl === true">
                <span>Lingua Originale:</span>
                <img :src="`https://flagcdn.com/24x18/${changeFlag()}.webp`" :alt="info.original_language" class="d-block mx-auto">
            </div>

            <!-- data -->
            <div v-if="openControl === true">
                <span>Data Uscita</span>
                <div class="ms-2">
                    {{getDate()}}
                </div>
            </div>

            <!-- voto -->
            <div v-if="openControl === true">
                <span>Voto:</span>
                <span>({{changeVote()}}/5)</span>
                <br>
                <i class="fa-star" v-for="n in 5" :class="(n <= changeVote()) ? 'fa-solid' : 'fa-regular'"></i>
            </div>

            
        </div>

        <button @click="openCloseInfo()">
            <i class="fa-solid fa-chevron-up" v-if="openControl === false"></i>
            <i class="fa-solid fa-chevron-down" v-else></i>
        </button>

    </div>
</template>

<style lang="scss" scoped>

@import "../style/main.scss";

    .fa-star.fa-solid {
        color: yellow;
    }
    .fa-star.fa-regular {
        color: white;
    }

</style>