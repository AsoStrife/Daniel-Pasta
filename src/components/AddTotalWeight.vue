<template>

    <f7-popup class="add-total-weight-popup" swipe-to-close>
        <f7-page>
            <f7-navbar :title="$t('message.addTotalWeight.title')">
                <f7-nav-right>
                    <f7-link popup-close>{{$t('message.general.close')}}</f7-link>
                </f7-nav-right>
            </f7-navbar>

           
            <form>
        
                <f7-list class="mt-0" no-hairlines-md>
                    <f7-list-input
                        outline
                        :label="$t('message.addTotalWeight.totalWight')"
                        :placeholder="$t('message.addTotalWeight.totalWightPlaceholder')"
                        floating-label
                        type="text"
                        clear-button
                        :value="totalWeight"
                        @input="totalWeight = $event.target.value"
                    >
                    </f7-list-input>

                </f7-list>

                <f7-block>
                    <f7-button fill popup-close
                        @click="addTotalWeight" 
                        :disabled="isEmpty(this.totalWeight)"> {{$t('message.general.add')}} 
                    </f7-button>
                </f7-block>

            </form>
            
        </f7-page>
    </f7-popup>

</template>

<script>
    import { f7 } from 'framework7-vue'
    export default {
        name: "AddTotalWeight", 
        props: {
            backLink: Boolean
        },
        data() {
            return {
                totalWeight: "",
            }
        },
        methods: {
            isEmpty(str) {
                return (!str || str.length === 0);
            },
            addTotalWeight() {
                f7.emit('addTotalWeight', totalWeight)
                this.clearValues()
            },
            clearValues() {
                this.totalWeight = ""
            }
        }
    }
</script>