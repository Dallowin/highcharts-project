<template>
   <div v-if="chartsData">
       <highcharts :chartsValue="chartsData" />
       <datatable :chartsValue="chartsData" />
   </div>
</template>

<script>
import Chart from "./components/Chart.vue"
import Table from "./components/Table.vue"

export default {
    name: "App",
    components: {
        highcharts: Chart,
        datatable: Table
    },
    data: () => ({
        chartsData: []
    }),
    async mounted() {
        await this.getData()
    },
    methods: {
        async getData() {
            const { data } = await this.axios.get(
                "https://test-task-for-frontend.herokuapp.com/data"
            );
            if (data.has_data) {
                
                this.chartsData = data.items.map((item) => {
                    const items = item.data.map(({ date, value }) => {
                        return [date, value];
                    });
                    return {
                        name: item.name,
                        data: items,
                    };
                })

            }
        }
    }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
