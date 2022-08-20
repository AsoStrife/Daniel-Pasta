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
                        :label="$t('message.addServing.personName')"
                        :placeholder="$t('message.addServing.personNamePlaceholder')"
                        floating-label
                        type="text"
                        clear-button
                        :value="personName"
                        @input="personName = $event.target.value"
                    >
                    </f7-list-input>

                    <f7-list-input
                        outline
                        :label="$t('message.addServing.rawWeight')"
                        :placeholder="$t('message.addServing.rawWeightPlaceholder')"
                        floating-label
                        type="number"
                        clear-button
                        :value="rawWeight == 0 ? '' : rawWeight"
                        @input="rawWeight = $event.target.value"
                    >
                    </f7-list-input>

                </f7-list>

                <f7-block>
                    <f7-button fill popup-close
                        @click="addServing" 
                        :disabled="isEmpty(this.personName) || isEmpty(this.rawWeight)"> {{$t('message.general.add')}} 
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
                personName: "",
                rawWeight: 0
            }
        },
        methods: {
            isEmpty(str) {
                return (!str || str.length === 0);
            },
            addServing() {
                f7.emit('addServing', {
                    personName: this.personName,
                    rawWeight: parseInt(this.rawWeight),
                    cookedWeight: parseInt(this.rawWeight)
                })
                this.clearValues()
            },
            clearValues() {
                this.personName = ""
                this.rawWeight = 0
            }
        }
    }
</script>