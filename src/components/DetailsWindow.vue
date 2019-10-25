<template>
    <div class="window-wrapper">
        <div class="window">
            <div class="header">
                <h2>{{ drink.name }}</h2>
                <h3>{{ drink.category }}, {{ drink.alcoholic }}</h3>
                <div class="closeButton" @click="$emit('closeWindow')"></div>
            </div>
            <div class="details">
                <div class="image-container">
                    <img :src="drink.image" :alt="drink.name">
                </div>
                <div class="description">
                    <div class="ingredients">
                        <h4>Ingredients:</h4>
                        <ul>
                            <li v-for="(ingredient) in drink.ingredients" :key="ingredient.name" >
                                {{ ingredient.name }}<span v-if="ingredient.amount"> - </span>{{ ingredient.amount }}
                            </li>
                        </ul>
                    </div>
                    <div class="instructions">
                        <h4>Instructions:</h4>
                        <p>
                            {{ drink.instructions }}
                        </p>
                    </div>
                </div>
                <p class="drink-responsibly" v-if="drink.alcoholic === 'Alcoholic'">Drink responsibly!</p>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "DetailsWindow",
        props: {
            drink: {
                type: Object
            }
        }
    }
</script>

<style lang="scss" scoped>
    .window-wrapper {
        position: fixed;
        background: rgba(0, 0, 0, 0.6);
        display: flex;
        flex-direction: column;
        justify-content: center;
        width: 100%;
        height: 100%;
        padding: 1em;
        top: 0;
        left: 0;
        right: 0;

        .window {
            position: relative;
            background: white;
            display: flex;
            flex-direction: column;
            justify-content: center;
            width: 100%;
            max-width: 1000px;
            margin: 0 auto;
            padding: 1em;

            .header {
                h2, h3 {
                    letter-spacing: 0.1em;
                    text-align: center;
                }

                h3 {
                    font-weight: normal;
                    margin-bottom: 0.5em;
                }

                .closeButton {
                    position: absolute;
                    cursor: pointer;
                    width: 17px;
                    height: 17px;
                    top: 12px;
                    right: 12px;

                    &::after,
                    &::before {
                        position: absolute;
                        display: block;
                        content: '';
                        width: 18px;
                        height: 2px;
                        top: 7px;
                        background-color: black;
                    }

                    &::after {
                        transform: rotate(45deg);
                    }
                    &::before {
                        transform: rotate(-45deg);
                    }
                }
            }

            .image-container {
                text-align: center;

                img {
                    width: 100%;
                    max-width: 400px;
                    height: auto;
                }
            }

            li {
                list-style: none;
            }

            h4 {
                margin: 1em 0.5em 0.5em;
            }

            .details {
                .drink-responsibly {
                    text-align: center;
                    margin-top: 1em;
                    font-size: 0.7em;
                    letter-spacing: 0.1em;
                    font-style: italic;
                }
            }
        }
    }
</style>
