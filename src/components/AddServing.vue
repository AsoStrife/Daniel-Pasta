<template>

    <f7-popup class="add-serving-popup" swipe-to-close>
        <f7-page>
            <f7-navbar :title="$t('message.addServing.title')">
                <f7-nav-right>
                    <f7-link popup-close>{{$t('message.general.close')}}</f7-link>
                </f7-nav-right>
            </f7-navbar>

           
            <form>
        
                <f7-list class="mt-0" no-hairlines-md>
                    <f7-list-input
                        outline
                        :label="$t('message.addServing.name')"
                        :placeholder="$t('message.addServing.namePlaceholder')"
                        floating-label
                        type="text"
                        clear-button
                        :value="name"
                        @input="name = $event.target.value"
                    >
                    </f7-list-input>

                    <f7-list-input
                        outline
                        :label="$t('message.addServing.weight')"
                        :placeholder="$t('message.addServing.weightPlaceholder')"
                        floating-label
                        type="number"
                        clear-button
                        :value="weight"
                        @input="weight = $event.target.value"
                    >
                    </f7-list-input>

                </f7-list>

                <f7-block>
                    <f7-button fill popup-close
                        @click="addServing" 
                        :disabled="isEmpty(this.name) || isEmpty(this.weight)"> {{$t('message.general.add')}} 
                    </f7-button>
                </f7-block>

            </form>
            
        </f7-page>
    </f7-popup>

</template>

<script>
    import { f7ready, f7 } from 'framework7-vue'
    export default {
        name: "AddExamCalculator", 
        props: {
            backLink: Boolean
        },
        data() {
            return {
                name: "",
                weight: "",
            }
        },
        methods: {
            isEmpty(str) {
                return (!str || str.length === 0);
            },
            addServing() {
                f7.emit('addServing', {
                    name: this.name,
                    weight: parseInt(this.weight)
                })
                this.clearValues()
            },
            clearValues() {
                this.name = ""
                this.weight = ""
            }
        }
    }
</script>