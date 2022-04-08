<template>
    <table id="datatable">
        <thead><tr><th>Date</th><th>Queries</th><th>Groups</th><th>Documents</th><th>Categories</th></tr></thead>
        <tbody>
            <tr v-for="(item, index) of tableValue" :key="index">
                <th>{{ new Date(item[0]).toLocaleDateString("en-US", { timeZone: "UTC", weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' }) }}</th>
                <td> {{ getValueByName(item, 'queries') }} </td>
                <td> {{ getValueByName(item, 'groups') }} </td>
                <td> {{ getValueByName(item, 'documents') }} </td>
                <td> {{ getValueByName(item, 'categories') }} </td>
            </tr>
        </tbody>
    </table>
</template>


<script>
export default {
    name: "Table",
    props: ["chartsValue"],
    computed: {
        tableValue() {
            const dates = new Map()

            for (const dataElem of this.chartsValue) {
                for (const item of dataElem.data) {

                    if (!dates.has(item[0])) {
                        dates.set(item[0], new Set())
                    }

                    dates.get(item[0]).add({
                        value: item[1],
                        name: dataElem.name
                    })

                }
            }

            return dates
        }
    },
    methods: {
        getValueByName(dataArr, searchValue) {
            for (let dateElem of dataArr[1]) {
                if (dateElem.name === searchValue)
                return dateElem.value
            }
        }
    }
}
</script>

<style>
#datatable{font-family:Verdana,sans-serif;border-collapse:collapse;border:1px solid #ebebeb;margin:10px auto;text-align:center;width:100%;max-width:auto}#datatable caption{padding:1em 0;font-size:1.2em;color:#555}#datatable th{font-weight:600;padding:.5em}#datatable caption,#datatable td,#datatable th{padding:.5em}#datatable thead tr,#datatable tr:nth-child(2n){background:#f8f8f8}#datatable tr:hover{background:#f1f7ff}
</style>