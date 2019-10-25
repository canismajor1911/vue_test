<template>
    <div class="wrapper" :class="{ small: state === 1 }">
        <h1>Cocktailopedia</h1>
        <h3>let's find a drink!</h3>
        <input
                name="search"
                title="search"
                placeholder="e.g. margarita"
                v-model="value"
                @input="handleInput"
        />
        <p v-if="state === 2">Nothing found, sorry :(</p>
    </div>
</template>

<script>
    /* eslint-disable no-console,no-unused-vars */

    import debounce from 'lodash.debounce';

    export default {
        name: "Search",
        data() {
            return {
                state: 0, // 0 - before search, 1 - after search, 2 - no results
                value: '',
                results: []
            }
        },
        methods: {
            handleInput: debounce(function () {
                let results = [];
                if (this.value && this.value !== '') {
                    fetch(`https://www.thecocktaildb.com/api/json/v1/1/search.php?s=${this.value}`)
                        .then(response => response.json())
                        .then(response => {
                            const drinks = response['drinks'];
                            if (drinks) {
                                for (const drinkJson of drinks) {
                                    let ingredients = [];
                                    for (let i = 1; i <= 15; i++) {
                                        const ingredient = drinkJson['strIngredient' + i];
                                        const measure = drinkJson['strMeasure' + i];
                                        if (ingredient) {
                                            ingredients.push({
                                                name: ingredient,
                                                amount: measure
                                            });
                                        } else {
                                            break;
                                        }
                                    }
                                    const drink = {
                                        id: drinkJson['idDrink'],
                                        name: drinkJson['strDrink'],
                                        category: drinkJson['strCategory'],
                                        ingredients: ingredients,
                                        instructions: drinkJson['strInstructions'],
                                        glass: drinkJson['strGlass'],
                                        alcoholic: drinkJson['strAlcoholic'],
                                        image: drinkJson['strDrinkThumb']
                                    };
                                    results.push(drink);
                                }
                                this.results = results;
                                this.state = 1;
                                this.$emit('resultsLoaded', this.results);
                            } else {
                                this.state = 2;
                                this.$emit('resultsDeleted');
                            }
                        })
                        .catch(err => {
                            alert('Ops! Something went wrong :(\n' + err);
                        });
                } else {
                    this.state = 0;
                    this.$emit('resultsDeleted');
                }
            }, 500)
        }
    }
</script>

<style lang="scss" scoped>
    @import "../styles/settings.scss";

    .wrapper {
        width: 100vw;
        height: 100vh;
        padding: 1em;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        background: url('../assets/bg.jpg') no-repeat center;
        -webkit-background-size: cover;
        background-size: cover;
        transition: height 500ms ease-in-out;

        * {
            color: white;
        }

        h1 {
            font-size: 2.5em;
            letter-spacing: 0.1em;
            transition: font-size 500ms ease-in-out,
                        letter-spacing 500ms ease-in-out;

            @include for-tablet-up {
                font-size: 4em;
            }
        }

        h3 {
            margin-bottom: 2em;
            font-weight: normal;
            letter-spacing: 0.1em;
            font-size: 1em;
            transition: font-size 500ms ease-in-out,
                        margin-bottom 500ms ease-in-out,
                        letter-spacing 500ms ease-in-out;

            @include for-tablet-up {
                font-size: 2em;
            }
        }

        input {
            background: none;
            border: none;
            padding: 0.3em;
            font-size: 1.5em;
            text-align: center;
            border-bottom: 2px solid white;

            &::placeholder {
                color: rgba(255, 255, 255, 0.5);
            }
        }
    }

    .wrapper.small {
        height: 150px;

        h1 {
            font-size: 1.8em;
        }

        h3 {
            font-size: 0.8em;
            margin-bottom: 1em;
        }
    }

</style>
