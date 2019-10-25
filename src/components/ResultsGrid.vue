<template>
    <div class="wrapper">
        <p>Here you go! Click on the cocktail that you're interested in to see more details.</p>
        <hr>
        <div class="grid">
            <Thumbnail
                    v-for="(drink, id) in data"
                    :drink="drink"
                    :key="id"
                    @click.native="handleWindowOpen(drink)"
            />
        </div>
        <DetailsWindow
                v-if="windowOpen"
                :drink="windowData"
                @closeWindow="windowOpen = false"/>
    </div>
</template>

<script>
    /* eslint-disable no-console */

    import Thumbnail from './Thumbnail';
    import DetailsWindow from './DetailsWindow';

    export default {
        name: "ResultsGrid",
        components: {
            Thumbnail,
            DetailsWindow
        },
        props: {
            data: {
                type: Array
            }
        },
        data() {
            return {
                windowOpen: false,
                windowData: {}
            }
        },
        methods: {
            handleWindowOpen(drink) {
                this.windowOpen = true;
                this.windowData = drink;
            },
            windowCls() {
                console.log('ok')
            }
        }
    }
</script>

<style lang="scss" scoped>
    @import "../styles/settings.scss";

    .wrapper {
        p {
            text-align: center;
            margin: 1em 0 0;
        }

        hr {
            border: 0;
            border-bottom: 1px solid #DDD;
            margin: 1em;
        }
    }

    .grid {
        display: grid;
        grid-template-columns: 1fr 1fr;

        @include for-phone-only {
            grid-template-columns: 1fr;
        }

        @include for-tablet-up {
            grid-template-columns: 1fr 1fr 1fr;
        }

        @include for-desktop-up {
            grid-template-columns: 1fr 1fr 1fr 1fr;
        }

        @include for-big-desktop-up {
            grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr;
        }
    }
</style>
