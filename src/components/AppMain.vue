<script>

    import { store } from '../store';

    export default {
        name: 'AppMain',
        data() {
            return {
                store
            }
        },
    }
    
</script>


<template>

    <main class="border">
        <h2>AppMain</h2>
    </main>
    
</template>

<style lang="scss" scoped>
    @import "../style/main.scss";

    main {
        background-color: black;
        min-height: calc(100vh - 100px);
    }
</style>