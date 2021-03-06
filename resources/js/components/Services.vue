<template>
    <div class="hero-body">
        <div class="container">
            <div v-if="orderedServices.length" class="columns is-multiline">
                <div v-for="service in orderedServices" :key="service.key" class="column is-4-tablet is-3-desktop">
                    <card :service="service"></card>
                </div>
            </div>
            <div v-else class="loading"></div>
        </div>
    </div>
</template>

<script>
    import echo from '../echo'
    import Card from './Card'
    import axios from 'axios'
    import store from '../store'
    import { mapState, mapMutations, mapGetters } from 'vuex'

    export default {
        store,
        components: {
            Card,
        },
        computed: {
            ...mapGetters(['orderedServices']),
        },
        methods: {
            ...mapMutations(['flushServices', 'updateService']),
        },
        mounted() {
            echo.channel('availability')
                .listen('Availability', (e) => {
                    this.updateService(e);
                });

            echo.connector.socket.on('connect', () => {
                axios.head('/api/services');
            });

            echo.connector.socket.on('reconnecting', () => {
                axios.head('/api/services');
            });

            echo.connector.socket.on('disconnect', this.flushServices);
        }
    }
</script>

<style scoped>
    .loading {
        height: 2em;
        width: 2em;
        overflow: visible;
        margin: auto;
    }

    .loading:before {
        content: '';
        display: block;
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
    }

    .loading:not(:required) {
        font: 0/0 a;
        color: transparent;
        text-shadow: none;
        background-color: transparent;
        border: 0;
    }

    .loading:not(:required):after {
        content: '';
        display: block;
        font-size: 10px;
        width: 1em;
        height: 1em;
        margin-top: -0.5em;
        animation: spinner 1500ms infinite linear;
        border-radius: 0.5em;
        box-shadow:
                rgba(0, 0, 0, 0.75) 1.5em 0 0 0,
                rgba(0, 0, 0, 0.75) 1.1em 1.1em 0 0,
                rgba(0, 0, 0, 0.75) 0 1.5em 0 0,
                rgba(0, 0, 0, 0.75) -1.1em 1.1em 0 0,
                rgba(0, 0, 0, 0.75) -1.5em 0 0 0,
                rgba(0, 0, 0, 0.75) -1.1em -1.1em 0 0,
                rgba(0, 0, 0, 0.75) 0 -1.5em 0 0,
                rgba(0, 0, 0, 0.75) 1.1em -1.1em 0 0;
    }

    /* Animation */

    @-webkit-keyframes spinner {
        0% {
            transform: rotate(0deg);
        }
        100% {
            transform: rotate(360deg);
        }
    }
    @-moz-keyframes spinner {
        0% {
            transform: rotate(0deg);
        }
        100% {
            transform: rotate(360deg);
        }
    }
    @-o-keyframes spinner {
        0% {
            transform: rotate(0deg);
        }
        100% {
            transform: rotate(360deg);
        }
    }
    @keyframes spinner {
        0% {
            transform: rotate(0deg);
        }
        100% {
            transform: rotate(360deg);
        }
    }
</style>
