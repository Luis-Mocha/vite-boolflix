<script>

import SearchComp from './SearchComp.vue';

export default {
    name: "AppHeader",
    components: {
        SearchComp,
    }
}
    
</script>


<template>

    <header>
        <div class="contenitore-90 h-100 d-flex">
            <!-- <div id="headerLogo" class="h-100"> -->
                <img src="https://image.tmdb.org/t/p/original/wwemzKWzjKYJFfCeiB57q3r4Bcm.svg" alt="Logo Netflix" class="h-100 py-4">
            <!-- </div> -->

            <nav id="headerNav">
                <ul>
                    <li>
                        <a href="#">
                            Home
                        </a>
                    </li>
                    <li>
                        <a href="#">
                            Serie Tv
                        </a>
                    </li>
                    <li>
                        <a href="#">
                            Film
                        </a>
                    </li>
                    <li>
                        <a href="#">
                            Nuovi e Popolari
                        </a>
                    </li>
                    <li>
                        <a href="#">
                            La mia lista
                        </a>
                    </li>
                </ul>

            </nav>

            <SearchComp/>
            
        </div>

    </header>

</template>

<style lang="scss" scoped>

@import "../style/main.scss";

    header {
        height: 100px;
        background-color: black;
        color: white;

        nav{
            width: 100%;
            margin-left:  40px;
            display: flex;
            align-items: center;

            ul {
                display: flex; 

                li{
                    margin-right: 1rem;
                }
            }
        }
        
    }
</style>