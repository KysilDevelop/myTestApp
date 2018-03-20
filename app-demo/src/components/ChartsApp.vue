<template>
  <div>
    <article class="article article--w50" v-for="chart in showChart">
      <vue-highcharts :options="options" ref="lineCharts"></vue-highcharts>
    </article>
  </div>
</template>
<script>
  import VueHighcharts from 'vue2-highcharts'
  const asyncData = {
    name: 'Tokyo',
    marker: {
      symbol: 'square'
    },
    data: [7.0, 6.9, 9.5, 14.5, 18.2, 21.5, 25.2, {
      y: 26.5,
      marker: {
        symbol: 'url(http://www.highcharts.com/demo/gfx/sun.png)'
      }
    }, 23.3, 18.3, 13.9, 9.6]
  }
  export default{
    components: {
      VueHighcharts
    },
    data(){
      return{
        options: {
          chart: {
//            type: 'pie'
          },
          title: {
            text: ''
          },
          subtitle: {
            text: ''
          },
          xAxis: {
            categories: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun',
              'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']
          },
          yAxis: {
            title: {
              text: 'Temperature'
            },
            labels: {
              formatter: function () {
                return this.value + '°';
              }
            }
          },
          tooltip: {
            crosshairs: true,
            shared: true
          },
          credits: {
            enabled: false
          },
          plotOptions: {
            spline: {
              marker: {
                radius: 4,
                lineColor: '#666666',
                lineWidth: 1
              }
            }
          },
          series: []
        }
      }
    },
    props: ['show-chart'],
    updated: function () {
      let count = 0;
      let lineCharts = null;
      this.$nextTick(function () {
        count = (this.showChart.length - 1);
        lineCharts = this.$refs.lineCharts[count];
        this.options.chart['type'] = this.showChart[count];
        lineCharts.delegateMethod('showLoading', 'Loading...');
        setTimeout(() => {
          lineCharts.addSeries(asyncData);
          lineCharts.hideLoading();
        }, 2000)
      })
    }
  }
</script>

