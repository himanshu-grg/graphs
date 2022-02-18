<template>
  <div>
    <canvas id="mychart" width="550" height="300"></canvas>
    <button class="button-role"  @click="port1()">Portfolio 1</button>
    <button  class="button-role" @click="port2()">Portfolio 2</button>
    <button class="button-role" @click="netVal()">Total</button>
  </div>
</template>

<script>

export default {
  name: 'Chart',
  props: ['date','dates', 'challenge', 'data1', 'data2', 'def'],
  data: () => (
    {Chart_2:""},
    {portfolio1:""},
    {portfolio2:""},
    {total:""}
  ),
  methods : {
    port1(){
      this.Chart_2.data.datasets[0].data =  this.portfolio1
      this.Chart_2.data.datasets[0].label = "Portfolio 1"
      this.Chart_2.update()
    },
    port2(){
      this.Chart_2.data.datasets[0].data =  this.portfolio2
      this.Chart_2.data.datasets[0].label = "Portfolio 2"
      this.Chart_2.update()
    },
    netVal(){
      this.Chart_2.data.datasets[0].data = this.total
      this.Chart_2.data.datasets[0].label ="Total"
      this.Chart_2.update()
    },
    makeGraph(){
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
        y: this.data1[index] + this.data2[index]
        }))
        let defData = this.dates.map((dates, index) => ({
        x: new Date(dates),
        y: this.def[index]
        }))
        const ctx = document.getElementById('mychart').getContext('2d')
        this.Chart_2 = new Chart(ctx, {
        type: 'line',
        data: {
            datasets: [
            {
                data: defData,
                label: "Default",
                borderColor: '#F25207'
            }
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
            },
            legend: {
                display: true
            },
            responsive: true,
            maintainAspectRatio: false
        }
        })
    }
  },
  mounted () {
    this.makeGraph()    
  }
}
</script>

<style scoped>
 .button-role{  padding: 1rem 2rem;
    text-align: center;
    font-size: 16px;
    text-transform: uppercase;
    cursor: pointer;
    background: linear-gradient(90deg, #288eec 0%, rgba(229, 20, 247, 0.63) 100%);
    border-radius: 53px;
    border: none;
    color: #fff;
    font-weight: bold;
    letter-spacing: 1px;
    margin-left: 10px;}   
</style>