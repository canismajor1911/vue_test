<template>
    <div class="wrapper">
        <Thumbnail v-for="(drink, id) in data" :drink="drink" :key="id" />
    </div>
</template>

<script>
    import Thumbnail from './Thumbnail';

    export default {
        name: "ResultsGrid",
        components: {
            Thumbnail
        },
        props: {
            data: {
                type: Array
            }
        }
    }
</script>

<style lang="scss" scoped>
    @import "../styles/settings.scss";

    .wrapper {
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
