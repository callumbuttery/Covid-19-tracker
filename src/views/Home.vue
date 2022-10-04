<template>
  <main v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate"/>
    <DataBoxes :stats="stats"/>
  </main>
  <main v-else class="flex flex-col align-center justify center text-center">
    <img :src="loadingImage" class="w-35 mx-auto mt-10 mb-4" />
    <div class="text-grey-500 text-3xl mt-6 mb-10">Fetching Covid-19 data</div>
  </main>
</template>

<script>
import DataTitle from '../components/DataTitle.vue';
import DataBoxes from '../components/DataBoxes.vue';

export default {
  name: "Home",
  components: {
    DataTitle,
    DataBoxes
  },
  data() {
    return {
      loading: true,
      title: "Global",
      dataDate: null,
      stats: {},
      countries: {},
      loadingImage: require("../assets/hourglass.gif"),
    };
  },
  methods: {
    async fetchCovidData() {
      try {
        const data = await fetch("https://api.covid19api.com/summary");
        return await data.json();
      } catch (error) {
        throw new Error("API fell over: ", error);
      }
    },
  },
  async created() {
    const data = await this.fetchCovidData();

    if (!data) {
      throw new Error("No data provided");
    }

    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.loading = false;
    console.log("data: ", data);
  },
};
</script>
