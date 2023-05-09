<script>

export default {
    name: 'SingleMovie',
    props: ['infoMovies' , 'infoIndex'] ,
    methods: {
    }
}
    
</script>


<template>
    <div class="movie-card">
        <div>
            {{infoMovies.title}}
        </div>
        <div>
            {{infoMovies.original_title}}
        </div>
        <div>
            {{infoMovies.original_language}}
        </div>
        <div>
            {{infoMovies.vote_average}}
        </div>

    </div>
</template>

<style lang="scss" scoped>

</style>