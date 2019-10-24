<template>
    <div id="app">
        <CommentList />
    </div>
</template>

<script>
    import CommentList from './components/CommentList';

    export default {
        name: 'app',
        components: {
            CommentList
        }
    }

</script>

<style>
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
