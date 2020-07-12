<script>
import { Bar } from 'vue-chartjs'

export default {
  extends: Bar,
  props: ['expenditurearr'],
  mounted () {
    this.renderChart({
      labels: [
        'Apparel',
        'Education',
        'Entertainment',
        'Finance',
        'Food',
        'Health',
        'House',
        'Other',
        'Teansport'
      ],
      datasets: [
        {
          backgroundColor: [
            'yellow',
            'red',
            'green',
            'orange',
            'purple',
            'blue',
            'gray',
            'yellow',
            'red'
          ],
          data: [
            this.expenditurearr[0].apparel,
            this.expenditurearr[0].education,
            this.expenditurearr[0].entertainment,
            this.expenditurearr[0].finance,
            this.expenditurearr[0].food,
            this.expenditurearr[0].health,
            this.expenditurearr[0].house,
            this.expenditurearr[0].other,
            this.expenditurearr[0].teansport
          ]
        }
      ]
    }, {
      responsive: true,
      maintainAspectRatio: false
    })
  }
}
</script>
