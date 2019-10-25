<template>
    <div class="item">
        <h2>{{ drink.name }}</h2>
        <h3>{{ drink.category }}, {{ drink.alcoholic }}</h3>
        <img :src="drink.image" :alt="drink.name" />
        <p>
            <template v-for="(ingredient, index) in drink.ingredients"><template v-if="index > 0">, </template>{{ ingredient.name }}</template>
        </p>
    </div>
</template>

<script>
    export default {
        name: "Thumbnail",
        props: {
            drink: {
                type: Object,
                required: true
            }
        }
    }
</script>

<style lang="scss" scoped>
    .item {
        padding: 0.5em;
        border: 1px solid #DDD;
        margin: 1em;
        cursor: pointer;

        img {
            max-width: 100%;
            height: auto;
            margin-top: 5px;
        }

        h2, h3, p {
            text-align: center;
            letter-spacing: 0.1em;
        }

        h2 {
            text-transform: uppercase;
            font-size: 1em;
        }

        h3, p {
            font-weight: normal;
            font-size: 0.8em;
        }
    }

</style>
