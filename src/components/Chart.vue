<template>
  <div>
    <highcharts
      :constructor-type="'stockChart'"
      ref="chart"
      :options="chartOptions"
    />
  </div>
</template>

<script>
import { Chart } from "highcharts-vue";
import Highcharts from "highcharts";
import exportingInit from "highcharts/modules/exporting";
import stockInit from "highcharts/modules/stock";

stockInit(Highcharts);
exportingInit(Highcharts);

export default {
    name: "Chart",
    components: {
        highcharts: Chart,
    },
    props: ['chartsValue'],
    data() {
        return {
            chartOptions: {
                credits: {
                    enabled: false
                },
                plotOptions: {
                    series: {
                        marker: {
                        radius: 4,
                        lineColor: "#666666",
                        lineWidth: 1
                        }
                    }
                },
                series: [],
                rangeSelector: {
                    buttons: [
                        {
                            count: 1,
                            type: "month",
                            text: "Month"
                        },
                        {
                            count: 1,
                            type: "year",
                            text: "Year"
                        },
                        {
                            type: "all",
                            text: "All"
                        }
                    ]
                }
            },
        };
    },
    watch: {
        'chartsValue'(newValue) {
            this.chartOptions.series = newValue
        }
    }
};
</script>