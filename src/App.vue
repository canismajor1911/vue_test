<template>
    <div id="app">
        <Search
                @resultsLoaded="showResultsGrid"
                @resultsDeleted="hideResultsGrid"/>
        <ResultsGrid v-if="loaded" :data="results"/>
    </div>
</template>

<script>
    import Search from './components/Search';
    import ResultsGrid from './components/ResultsGrid';

    export default {
        name: 'app',
        components: {
            Search,
            ResultsGrid
        },
        data() {
            return {
                loaded: false,
                results: []
            }
        },
        methods: {
            showResultsGrid(results) {
                this.results = results;
                this.loaded = true;
            },
            hideResultsGrid() {
                this.results = [];
                this.loaded = false;
            }
        }
    }

</script>

<style lang="scss">
    * {
        -webkit-box-sizing: border-box;
        -moz-box-sizing: border-box;
        box-sizing: border-box;
        margin: 0;
        padding: 0;
        outline: none !important;
    }

    body {
        font-family: Arial, Helvetica, sans-serif;
        line-height: 1.5;
    }
</style>
