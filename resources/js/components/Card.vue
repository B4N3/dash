<template>
    <div class="flex-card card-overflow light-bordered light-raised">
        <div class="icon-header">
            <i class="notification" :class="[service.icon, service.color]"></i>
        </div>
        <div class="content">
            <div class="card-title has-text-right">
                <h5 v-text="service.title"></h5>
            </div>

            <div class="card-content" style="padding-left: 0; padding-right: 0">
                <div class="buttons is-pulled-right">
                    <!--<button v-if="service.toggle" @click="clickService('toggle', service)" class="button"-->
                            <!--:class="[service.started ? 'is-success' : 'is-danger']">-->
                        <!--<i class="fa-circle" :class="[service.started ? 'fas' : 'fal']" aria-hidden="true"></i>-->
                    <!--</button>-->
                    <!--<button v-if="service.restart" @click="clickService('restart', service)" class="button is-warning" :disabled="!service.started">-->
                        <!--<i class="fas fa-undo-alt" aria-hidden="true"></i>-->
                    <!--</button>-->
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            service: Object
        }
    }
</script>

<style scoped>

    .flex-card .icon-header i {
        box-shadow: 0 14px 26px -12px rgba(0,209,178,0.42),0 4px 23px 0px rgba(0,0,0,0.12),0 8px 10px -5px rgba(0,209,178,0.2) !important;
    }

    .flex-card.light-raised {
        box-shadow: 0 3px 10px 4px rgba(0,0,0,0.04);
    }

    .flex-card.light-bordered {
        border: 1px solid #e5e5e5 !important;
    }

    .flex-card .content {
        padding: 20px !important;
    }

    .flex-card .icon-header i {
        padding: 22px;
        font-size: 24px;
        font-weight: normal;
        border-radius: 3px;
        position: absolute;
        left: 10px;
        top: -20px;
    }

    .flex-card {
        position: relative;
        background-color: #fff;
        border: 1px solid #fcfcfc;
        border-radius: 0.1875rem;
        display: inline-block;
        overflow: hidden;
        width: 100%;
        margin-bottom: 20px;
        transition: all 0.5s;
    }

    .flex-card.card-overflow {
        overflow: visible !important;
    }

</style>