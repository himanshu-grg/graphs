<template>
  <div>
    <canvas id="mychart" width="550" height="300"></canvas>
    <button @click="changeLabel()">click</button>
  </div>
</template>

<script>

export default {
  name: 'Chart',
  props: ['date','dates', 'challenge', 'data1', 'data2'],
  data: () => (
    {Chart_2:""},
    {portfolio1:""},
    {portfolio2:""},
    {total:''},
    {labell:""},
    {i:0}
   
  ),
  methods : {
    changeLabel(){
      let list= [this.portfolio1, this.portfolio2, this.total]
      let labels = ["Portfolio 1", "Portfolio 2", "Total"]
      this.Chart_2.data.datasets[0].data = list[this.i]
      this.labell = labels[this.i]
      console.log(this.i)
      console.log(this.labell)
      console.log(this.Chart_2.data.datasets[0].data)
      this.i= this.i + 1
      if(this.i==3){this.i=0}
    }
  },
  mounted () {
    // eslint-disable-next-line no-unused-vars
    // const data1 = this.date.map((date, index) => ({
    //   x: new Date(date * 1000),
    //   y: this.challenge[index]
    // }))
    this.portfolio1 = this.dates.map((dates, index) => ({
      x: new Date(dates),
      y: this.data1[index]
    }))
    this.portfolio2 = this.dates.map((dates, index) => ({
      x: new Date(dates),
      y: this.data2[index]
    }))
    this.total = this.dates.map((dates, index) => ({
      x: new Date(dates),
      y: this.data1[index] + this.data2[index] + this.challenge[index]
    }))
    const ctx = document.getElementById('mychart').getContext('2d')
    // eslint-disable-next-line no-undef,no-unused-vars
    this.Chart_2 = new Chart(ctx, {
      type: 'line',
      data: {
        datasets: [
          // {
          //   data: data1,
          //   label: 'Chart from API ',
          //   borderColor: '#7367F0'
          // },
          {
            data: this.total,
            label: this.labell || "Default",
            borderColor: '#F25207'
          }
          //
          // {
          //   data: data3,
          //   label: 'Local Data 2',
          //   borderColor: 'yellow',
          // },
          // {
          //   data:total,
          //   label:"Total",
          //   borderColor:"red"
          // }
        ]
      },
      options: {
        scales: {
          xAxes: [
            {
              type: 'time',
              time: {
                unit: 'month',
                displayFormats: {
                  years: 'MMM YYYY'
                }
              },
              gridLines: {
                display: false
              }
            }
          ],
          yAxes: [{
              gridLines: {
                display: true
              }
            }],
          // yAxes: [
          //   {
          //     ticks: {
          //       // eslint-disable-next-line no-unused-vars
          //       // callback (value, index, values) {
          //       //   return `${value}`
          //       // }

          //     }
          //   }
          //]
        },
        legend: {
            display: true
          },
        responsive: true,
        maintainAspectRatio: false
      }
    })
  }
}
</script>