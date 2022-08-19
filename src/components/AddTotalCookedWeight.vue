<template>

    <f7-popup class="add-total-weight-popup" swipe-to-close>
        <f7-page>
            <f7-navbar :title="$t('message.addTotalCookedWeight.title')">
                <f7-nav-right>
                    <f7-link popup-close>{{$t('message.general.close')}}</f7-link>
                </f7-nav-right>
            </f7-navbar>
           
            <form>
        
                <f7-list class="mt-0" no-hairlines-md>
                    <f7-list-input
                        outline
                        :label="$t('message.addTotalCookedWeight.totalCookedWeightLabel')"
                        :placeholder="$t('message.addTotalCookedWeight.totalCookedWeightPlaceholder')"
                        floating-label
                        type="number"
                        clear-button
                        :value="this.totalCookedWeight <= 0 ? '' : this.totalCookedWeight"
                        @input="this.totalCookedWeight = $event.target.value"
                    >
                    </f7-list-input>

                </f7-list>

                <p class="block text-color-red" v-if="showErrorMessage">{{$t('message.addTotalCookedWeight.errorMessage')}}</p>

                <f7-block>
                    <f7-button fill popup-close
                        @click="addTotalCookedWeight" 
                        :disabled="isEmpty(this.totalCookedWeight) || (showErrorMessage)"> {{$t('message.general.add')}} 
                    </f7-button>
                </f7-block>

            </form>
            
        </f7-page>
    </f7-popup>

</template>

<script>
    import { f7 } from 'framework7-vue'
    export default {
        name: "AddTotalCookedWeight", 
        props: {
            defaultTotalCookedWeight: {
                type: Number, 
                default: ""
            }, 
            totalRawWeight: {
                type: Number, 
                default: 0
            }
        },
        data() {
            return {
                totalCookedWeight: 0,
                showErrorMessage: false
            }
        },
        methods: {
            isEmpty(str) {
                return (!str || str.length === 0)
            },
            addTotalCookedWeight() {
                f7.emit('addTotalCookedWeight', parseInt(this.totalCookedWeight))
                this.clearValues()
            },
            clearValues() {
                this.totalCookedWeight = ""
            }
        },
        mounted() {
            this.totalCookedWeight = this.defaultTotalCookedWeight

            this.$watch(
                (vm) => [this.defaultTotalCookedWeight],
                (val) => {
                    this.totalCookedWeight = this.defaultTotalCookedWeight
                },
                {
                    immediate: true,
                    deep: true,
                }
            )

            this.$watch(
                (vm) => [this.totalCookedWeight],
                (val) => {
                    this.showErrorMessage = parseInt(this.totalCookedWeight) < parseInt(this.totalRawWeight) ? true : false
                },
                {
                    immediate: true,
                    deep: true,
                }
            )
        }
    }
</script>