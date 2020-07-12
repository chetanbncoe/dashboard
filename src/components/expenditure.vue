<script>
import { Bar } from 'vue-chartjs'

export default {
  extends: Bar,
  data: () => ({
    chartdata: {
      labels: ['POInProcess', 'POInDone', 'POCheckDone', 'PORecheck', 'POApproved', 'POLocked', 'Invalid'],
      datasets: [
        {
          backgroundColor: [
            'yellow',
            'red',
            'green',
            'orange',
            'purple',
            'blue',
            'gray'
          ],
          data: [11, 12, 13, 14, 15, 16, 17]
        }
      ]
    },
    options: {
      responsive: true,
      maintainAspectRatio: false
    }
  }),

  mounted () {
    this.renderChart(this.chartdata, this.options)
  }
}
</script>
