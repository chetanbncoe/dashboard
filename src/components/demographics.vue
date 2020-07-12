<script>
import { Doughnut } from 'vue-chartjs'

export default {
  extends: Doughnut,
  props: ['income', 'locality'],
  mounted () {
    debugger
    this.renderChart({
      labels: [this.locality],
      datasets: [
        {
          backgroundColor: [
            'purple'
          ],
          data: [this.income]
        }
      ]
    },
    {
      responsive: true,
      maintainAspectRatio: false
    })
  }
}
</script>
