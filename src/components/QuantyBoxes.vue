<template>
    <f7-block class="mt-0 mb-0">
        <f7-row>
            <f7-col>
                <f7-card>
                    <f7-card-header>{{$t('message.quantity.totalRawWeight')}}</f7-card-header>
                    <f7-card-content>
                        {{totalRawWeight}}
                    </f7-card-content>
                </f7-card>
            </f7-col>
            <f7-col>
                <f7-card>
                    <f7-card-header>{{$t('message.quantity.totalCookedWeight')}}</f7-card-header>
                    <f7-card-content>
                        {{totalCookedWeight}} 
                    </f7-card-content>
                </f7-card>
            </f7-col>
        </f7-row>
    </f7-block>
</template>

<style scoped>
    .card-content {
         text-align: center;
    }
</style>

<script>
    import { f7ready, f7 } from 'framework7-vue'

    export default {
        name: "QuantityBoxes", 
        props: {
            totalRawWeight: {
                type: Number, 
                default: 0
            },
            totalCookedWeight: {
                type: Number, 
                default: 0
            }

        },
        methods: {
        },
        mounted() {
            var self = this
            f7ready(() => {
            })
        }
        
    }
</script>