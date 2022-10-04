<template>
    <div class="grid md:grid-cols-2 gap-4">
        <!-- Box 1  -->
        <div class="shadow-md bg-blue-200 p-10 text-center rounded">
            <h3 class="text-3xl text-blue-500 font-bold mb-4">Cases</h3>

            <div class="text-3xl mb-2 mt-10">
                <span class="text-black">Total Cases: </span>
                <span class="text-black">{{numbersWithCommas(stats.TotalConfirmed)}}</span>
            </div>
            <div class="mb-4">
                <span class="text-red-500">New Cases: </span>
                <span class="text-red-500">{{numbersWithCommas(stats.NewConfirmed)}}</span>
            </div>
        </div>

        <!-- Box 2 -->
        <div class="shadow-md bg-purple-200 p-10 text-center rounded">
            <h3 class="text-3xl text-blue-500 font-bold mb-4">Deaths</h3>

            <div class="text-3xl mb-2 mt-10">
                <span class="text-black">Total Deaths: </span>
                <span class="text-black">{{numbersWithCommas(stats.TotalDeaths)}}</span>
            </div>
            <div class="mb-4">
                <span class="text-red-500">New Deaths: </span>
                <span class="text-red-500">{{numbersWithCommas(stats.NewDeaths)}}</span>
            </div>
        </div>
    </div>

    <div class="grid md:grid-cols-1 gap-4 mt-10 mx-auto">
        <!-- Box 1  -->
        <div class="shadow-md bg-gray-200 p-10 text-center">
            <h3 class="text-3xl text-black-500 font-bold mb-4">Statistics</h3>

            <div class="text-3xl mb-2 mt-10">
                <span class="text-black">Fatality rate: </span>
                <span class="font-bold text-black">{{percentageStats.deathRounded}}</span>
            </div>
            <div class="text-2xl mb-2 mt-2">
                <span class="text-black">Population infected at some stage: </span>
                <span class="font-bold text-black">{{percentageStats.totalInfected}}</span>
            </div>
            <div class="text-2xl mb-2 mt-2">
                <span class="text-black">Population currently infected: </span>
                <span class="font-bold text-black">{{percentageStats.currentlyInfected}}</span>
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
                const deathRounded = (this.stats.TotalDeaths / this.stats.TotalConfirmed * 100).toFixed();
                const totalInfected = ( this.stats.TotalConfirmed / 8000000000).toFixed();
                const currentlyInfected = (this.stats.NewConfirmed / 8000000000).toFixed();

                return {
                    deathRounded: deathRounded <= 0 ? 'Less than 1%' : deathRounded + '%',
                    totalInfected: totalInfected <= 0 ? 'Less than 1%' : totalInfected + '%',
                    currentlyInfected: currentlyInfected <= 0 ? 'Less than 1%' : currentlyInfected + '%',
                }
            }
        }
    }
</script>