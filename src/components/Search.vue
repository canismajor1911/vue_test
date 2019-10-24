<template>
    <div class="wrapper">
        <h1>Drink-o-pedia</h1>
        <h3>let's find a drink!</h3>
        <input
                name="search"
                title="search"
                placeholder="e.g. margarita"
                v-model="value"
                @input="handleInput"
        />
    </div>
</template>

<script>
    /* eslint-disable no-console,no-unused-vars */

    export default {
        name: "Search",
        data() {
            return {
                value: ''
            }
        },
        methods: {
            handleInput() {
                fetch(`https://www.thecocktaildb.com/api/json/v1/1/search.php?s=${this.value}`)
                    .then(response => response.json())
                    .then(response => {
                        const drinks = response['drinks'];
                        if (drinks) {
                            drinks.forEach(drinkJson => {
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
                                console.log(drink);
                            });
                        }
                    })
                    .catch(err => {
                        alert('Ops! Something went wrong:(\n' + err);
                    });
            }
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

        * {
            color: white;
        }

        h1 {
            font-size: 2.5em;
            letter-spacing: 0.1em;

            @include for-tablet-landscape-up {
                font-size: 4em;
            }
        }

        h3 {
            margin-bottom: 2em;
            font-size: 1em;

            @include for-tablet-landscape-up {
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

</style>
