<template>
    <div class="grid md:grid-cols-2 gap-4">
        <!-- Box 1  -->
        <div class="shadow-md bg-blue-200 p-10 text-center rounded">
            <h3 class="text-3xl text-blue-500 font-bold mb-4">Cases</h3>

            <div class="text-3xl mb-2 mt-10">
                <span class="font-bold text-black">Total Cases: {{numbersWithCommas(stats.TotalConfirmed)}}</span>
            </div>
            <div class="mb-4">
                <span class="font-bold text-red-500">New Cases: {{numbersWithCommas(stats.NewConfirmed)}}</span>
            </div>
        </div>

        <!-- Box 2 -->
        <div class="shadow-md bg-purple-200 p-10 text-center rounded">
            <h3 class="text-3xl text-blue-500 font-bold mb-4">Deaths</h3>

            <div class="text-3xl mb-2 mt-10">
                <span class="font-bold text-black">Total Deaths: {{numbersWithCommas(stats.TotalDeaths)}}</span>
            </div>
            <div class="mb-4">
                <span class="font-bold text-red-500">New Deaths: {{numbersWithCommas(stats.NewDeaths)}}</span>
            </div>
        </div>
    </div>

    <div class="grid md:grid-cols-1 gap-4 mt-10 w-96 mx-auto">
        <!-- Box 1  -->
        <div class="shadow-md bg-gray-200 p-10 text-center">
            <h3 class="text-3xl text-black-500 font-bold mb-4">Statistics</h3>

            <div class="text-3xl mb-2 mt-10">
                <span class="font-bold text-black">Fatality rate: {{percentageStats}}</span>
            </div>
        </div>
    </div>
</template>

<script>

    export default {
        name: 'DataBoxes',
        props: ['stats'],
        methods: {
            numbersWithCommas(unformattedNumber) {
                return unformattedNumber.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
            }
        },
        computed: {
            //calculate chance of fatality
            percentageStats: function() {
                const rounded = (this.stats.TotalDeaths / this.stats.TotalConfirmed * 100).toFixed();

                return rounded < 0 ? 'Less than 1%' : rounded + '%';
            }
        }
    }
</script>