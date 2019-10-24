<template>
    <div id="app">
        <Search />
    </div>
</template>

<script>
    import Search from './components/Search';

    export default {
        name: 'app',
        components: {
            Search
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
    }

    body {
        font-family: Arial, Helvetica, sans-serif;
        line-height: 1.5;
    }
</style>
