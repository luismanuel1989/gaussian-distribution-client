<template>
    <div class="bar-class">
        <Bar :data="data" :options="options" />
    </div>
</template>

<script>
import {
    Chart as ChartJS,
    Title,
    Tooltip,
    Legend,
    BarElement,
    CategoryScale,
    LinearScale
} from 'chart.js'
import { Bar } from 'vue-chartjs'

ChartJS.register(CategoryScale, LinearScale, BarElement, Title, Tooltip, Legend)

export default {
    name: 'GaussianRepresentationComponent',
    props: ['barData'],
    components: {
        Bar
    },
    mounted(){
        console.log("Mounted line 30")
    },
    data() {
        console.log("Data line 33-9")
        console.log(this.barData)
        const numbers = []
        for (let i = 1; i <= 100; i++) {
            numbers.push(i)
        }
        const data = {
            labels: [...numbers
            ],
            datasets: [
                {
                    label: this.barData.datasets[0].label,
                    backgroundColor: '#41b884',
                    data: this.barData.datasets.data
                }
            ]
        }
        const options = {
            responsive: true,
            maintainAspectRatio: false
        }
        let dataFromFetch = []
        return {
            data,
            options,
            dataFromFetch
        }
    },

}
</script>
<style>
.bar-class {
    width: 1000px;
    height: 500px;
}
</style>