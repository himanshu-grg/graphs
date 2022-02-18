<script>
  import { Line } from 'vue-chartjs'

  export default {
    extends: Line,
    data () {
      return {
        dat:'',
        datacollection: {
          labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'],
          datasets: [
            {
              label: 'Data One',
              pointBackgroundColor: '#F25207',
              borderWidth: 5,
              fill:false,
              pointBorderColor: '#F25207',
              data: [60, 40, 20, 50, 90, 10, 20, 40, 50, 70, 90, 100]
            },
            {
              label: 'Data Two',
              pointBackgroundColor: 'white',
              borderWidth: 1,
              backgroundColor:"#F2D707",
              pointBorderColor: '#249EBF',
              data: [20, 60, 10, 80, 30, 50, 60, 20, 30, 40, 70, 20]
            }
          ]
        },
        options: {
          scales: {
            yAxes: [{
              ticks: {
                beginAtZero: true
              },
              gridLines: {
                display: true
              }
            }],
            xAxes: [ {
              gridLines: {
                display: false
              }
            }]
          },
          legend: {
            display: true
          },
          responsive: true,
          maintainAspectRatio: false
        }
      }
    },
    mounted () {
      this.renderChart(this.datacollection, this.options)
      // fetch('https://covid19.mathdro.id/api/confirmed')
      //   .then(
      //     function(response) {
      //       if (response.status !== 200) {
      //         // eslint-disable-next-line
      //         console.log('Looks like there was a problem. Status Code: ' +
      //           response.status);
      //         return;
      //       }
      //   // Examine the text in the response
      //   response.json().then(function(data) {
      //         let dat = data.slice(0, 7);
      //         // eslint-disable-next-line
      //         console.log(dat);
      //       });
      //     }
      //   )
    }
  }
</script>