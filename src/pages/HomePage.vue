<template>
    <f7-page name="HomePage">
        
        <!-- Top Navbar -->
        <f7-navbar :title="$t('message.general.appName')">
            <f7-nav-title></f7-nav-title>
        </f7-navbar>
        
        <!-- Toolbar-->
        <f7-toolbar bottom>
            <f7-link @click="addServingPopup()">{{$t('message.toolbar.addServing')}}</f7-link>
            <f7-link @click="addTotalCookedWeightPopup()">{{$t('message.toolbar.addTotalCookedWeight')}}</f7-link>
        </f7-toolbar>

        <QuantityBoxes :totalRawWeight="totalRawWeight" :totalCookedWeight="totalCookedWeight"/>

        <AddServing />

        <AddTotalCookedWeight :totalRawWeight="totalRawWeight" :defaultTotalCookedWeight="totalCookedWeight"/>

        <ServingsTable :servings="servings"/>

    </f7-page>
</template>

<script>
    import { f7ready, f7 } from 'framework7-vue'
    import AddServing from '../components/AddServing.vue'
    import AddTotalCookedWeight from '../components/AddTotalCookedWeight.vue'
    import ServingsTable from '../components/ServingsTable.vue'
    import QuantityBoxes from '../components/QuantyBoxes.vue'

    export default {
        name: "HomePage",
        data() {
            return {
                servings: [], 
                totalRawWeight: 0,
                totalCookedWeight: 0
            };
        },
        components: {
            AddServing,
            ServingsTable,
            AddTotalCookedWeight,
            QuantityBoxes
        },
        methods: {
            addServingPopup(){
                f7.popup.open('.add-serving-popup')
            },
            addTotalCookedWeightPopup(){
                f7.popup.open('.add-total-weight-popup')
            },
            doMath() {
                this.totalRawWeight = this.servings.reduce( (a, b) => a + b.rawWeight, 0)
                
                if(this.totalRawWeight > this.totalCookedWeight)
                    this.totalCookedWeight = this.totalRawWeight

                let proportion = this.totalCookedWeight / this.totalRawWeight 
                this.servings = this.servings.map( serving => ({
                    ...serving, cookedWeight: serving.rawWeight * proportion
                }))
            },
            resetWeights() {
                this.totalRawWeight = 0
                this.totalCookedWeight = 0
            }
        },
        mounted() {
            var self = this
            f7ready(async () => {
                f7.on('addServing', function(data){
                    self.servings.push(data)
                    self.doMath()
                })
                f7.on('addTotalCookedWeight', function(totalCookedWeight) {
                    self.totalCookedWeight = totalCookedWeight
                    self.doMath()
                })
                f7.on('deleteExamFromCalulator', function(data) {
                    self.servings.splice(data, 1)

                    if(self.servings.length == 0)
                        self.resetWeights()

                    self.doMath()
                })
                f7.on('deleteAllExamFromCalulator', function() {
                    self.servings = []
                    self.resetWeights()
                })
                
            })
        } 
        
    }
</script>