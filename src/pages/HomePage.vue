<template>
    <f7-page name="home">
        
        <!-- Top Navbar -->
        <f7-navbar>
            <f7-nav-title>Daniel Pasta</f7-nav-title>
        </f7-navbar>
        
        <!-- Toolbar-->
        <f7-toolbar bottom>
            <f7-link @click="addServingPopup()">{{$t('message.toolbar.addServing')}}</f7-link>
            <f7-link @click="addTotalWeightPopup()">{{$t('message.toolbar.addTotalWeight')}}</f7-link>
        </f7-toolbar>
        <Quantity :initialWeight="initialWeight" :newWeight="newWeight"/>
        <AddServing />
        <AddTotalWeight />
        <ServingsTable :servings="servings"/>

    </f7-page>
</template>

<script>
    import { f7ready, f7 } from 'framework7-vue'
    import AddServing from '../components/AddServing.vue'
    import AddTotalWeight from '../components/AddTotalWeight.vue'
    import ServingsTable from '../components/ServingsTable.vue'
    import Quantity from '../components/Quantity.vue'

    export default {
        name: "HomePage",
        data() {
            return {
                servings: [
                    {
                        "name": "Andrea", 
                        "weight": 100
                    }
                ], 
                initialWeight: 0,
                newWeight: 0
            };
        },
        components: {
            AddServing,
            ServingsTable,
            AddTotalWeight,
            Quantity
        },
        methods: {
            addServingPopup(){
                f7.popup.open('.add-serving-popup')
            },
            addTotalWeightPopup(){
                f7.popup.open('.add-total-weight-popup')
            },
            calculateNewAvg() {
                this.newTotalCfu = parseInt(this.initialTotalCfu) + this.newExams.reduce(function (acc, e) { return acc + parseInt(e.examCfu) }, 0)
                let newExamsWeightedSum = this.newExams.reduce(function (acc, e) { return acc + (parseInt(e.examCfu) * parseInt(e.examGrade)) }, 0)
                let initialExamWeightedSum = this.initialWeightedAvg * this.initialTotalCfu
                this.newWeightedAvg = parseFloat((initialExamWeightedSum + newExamsWeightedSum) / this.newTotalCfu).toFixed(2)
                this.newWeightedAvg = parseFloat(this.newWeightedAvg)
                this.textColor = this.newWeightedAvg > this.initialWeightedAvg ? "text-success" : (this.newWeightedAvg < this.initialWeightedAvg ? "text-danger" : "")
            }
        },
        mounted() {
            var self = this
            f7ready(async () => {
                f7.on('addServing', function(data){
                    self.servings.push(data)
                    self.calculateNewAvg()
                })
                f7.on('deleteExamFromCalulator', function(data) {
                    self.newExams.splice(data, 1)
                    self.calculateNewAvg()
                })
                f7.on('deleteAllExamFromCalulator', function() {
                    self.newExams = []
                    self.calculateNewAvg()
                })
            });
        } 
        
    }
</script>