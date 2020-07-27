<script>

import {Doughnut} from 'vue-chartjs';

export default {
  props:[
    'chartData',
  ],

  extends:Doughnut,
  

  mounted () {
    this.renderChart(this.chartData.chartdata, this.chartData.options)
  }
}

</script>
