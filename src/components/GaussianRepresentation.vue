<template>
    <div class="bar-class">
        <BarChart v-if="loaded" :bar-data="randomData"/>
        <BarChart v-if="loaded" :bar-data="frequencyData"/>
    </div>
</template>

<script>
import axios from 'axios'
import BarChart from '@/components/BarChart.vue'

export default {
    name: 'GaussianRepresentationComponent',
    components: {
        BarChart
    },
    data() {
        const numbers = []
        for (let i = 1; i <= 100; i++) {
            numbers.push(i)
        }
        const randomData = {
            labels: [...numbers
            ],
            datasets: [
                {
                    label: 'Random Data',
                    backgroundColor: '#41b884',
                    data: undefined
                }
            ]
        }
        const frequencyData = {
            labels: [...numbers
            ],
            datasets: [
                {
                    label: 'Frequency data',
                    backgroundColor: '#41b884',
                    data: undefined
                }
            ]
        }
        const options = {
            responsive: true,
            maintainAspectRatio: false
        }
        console.log("Line 29")
        let dataFromFetch = []
        return {
            randomData,
            frequencyData,
            options,
            dataFromFetch, 
            loaded: false
        }
    },
    methods: {
        async getGaussianData() {
            try {
                const response = await axios.get('http://localhost:5000/gaussian-dist')
                this.randomData.datasets.data = response.data.rawData
                this.frequencyData.datasets.data = response.data.freqArray
                this.loaded = true
            } catch (error) {
                console.error("Error fetching Gaussian data: ", error)
            }
        }
    },
    mounted() {
        this.getGaussianData();
    }
}
</script>
<style>
.bar-class {
    background-color: #ccf;
    width: 1000px;
    height: 500px;
}
</style>