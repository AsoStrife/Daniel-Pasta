<template>
    <f7-block class="mt-0 mb-0">
        <f7-row>
            <f7-col>
                <f7-card>
                    <f7-card-header>{{$t('message.quantity.initialWeight')}}</f7-card-header>
                    <f7-card-content>
                        {{initialWeight}}
                    </f7-card-content>
                </f7-card>
            </f7-col>
            <f7-col>
                <f7-card>
                    <f7-card-header>{{$t('message.quantity.newWeight')}}</f7-card-header>
                    <f7-card-content>
                        {{newWeight == 0 ? "&nbsp;" : newWeight}} 
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
        name: "Ratings", 
        props: {
            initialWeight: {
                type: Number, 
                default: 0
            },
            newWeight: {
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