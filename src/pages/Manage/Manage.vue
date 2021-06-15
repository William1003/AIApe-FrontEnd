<template>

    <div id="test" style="height: 50vh; width: 50vw">

    </div>
</template>

<script>
const echarts = require('echarts');

export default {
    data() {
        return {
            myChart: {}
        }
    },
    mounted() {
        this.myChart = echarts.init(document.getElementById('test'));
        let options = {
            xAxis: {
                type: 'category',
                data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
            },
            yAxis: {
                type: 'value'
            },
            series: [{
                data: [150, 230, 224, 218, 135, 147, 260],
                type: 'line'
            }]
        }
        this.myChart.setOption(options);
    }
}
</script>

<style scoped>

</style>
