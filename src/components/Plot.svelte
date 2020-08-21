<script>
  import { afterUpdate, onMount } from 'svelte'
  export let circleData = null
  export let lineData = null
  export let labels = null
  export let limitData = null

  $: circleData = circleData.map((val) => 1 / (1 - val))

  const circleColor = []
  const lineColor = []
  for (let i = 0; i < 20; i++) {
    circleColor.push('blue')
    lineColor.push('green')
  }

  let ctx
  let chart

  onMount(() => {
    ctx = document.getElementById('chart')
    renderChart()
  })

  const changeColors = () => {
    const [current, limit, circle] = chart.data.datasets
    for (let i = 0; i < circle.data.length; i++) {
      if (current.data[i] < 1.15) {
        current.pointBorderColor[i] = 'red'
      } else if (current.data[i] < limit.data[i]) {
        current.pointBorderColor[i] = 'orange'
      } else {
        current.pointBorderColor[i] = 'green'
      }
    }
  }

  const renderChart = () => {
    if (chart) chart.destroy()
    chart = new Chart(ctx, {
      type: 'bar',
      data: {
        datasets: [
          {
            label: 'Current R\u2080',
            pointBorderColor: lineColor,
            pointBackgroundColor: lineColor,
            pointRadius: 10,
            pointHoverRadius: 9,
            pointHoverBorderWidth: 2,
            borderWidth: 3,
            backgroundColor: 'rgba(255,255,255,0)',
            borderColor: 'rgba(255,255,255,0)',
            data: lineData,
            pointStyle: 'line',
            type: 'line',
          },
          {
            label: 'Old Normal R\u2080',
            pointBackgroundColor: 'green',
            pointBorderColor: 'green',
            pointRadius: 10,
            pointHoverRadius: 9,
            pointHoverBorderWidth: 2,
            borderWidth: 3,
            backgroundColor: 'rgba(255,255,255,0)',
            borderColor: 'rgba(255,255,255,0)',
            data: limitData,
            pointStyle: 'line',
            type: 'line',
          },
          {
            label: 'Susceptible %',
            pointBackgroundColor: circleColor,
            pointRadius: 10,
            pointHoverRadius: 9,
            backgroundColor: 'rgba(255,255,255,0)',
            borderColor: 'rgba(255,255,255,0)',
            data: circleData,
            pointStyle: 'circle',
            type: 'line',
          },
        ],
        labels,
      },
      options: {
        tooltips: {
          mode: 'index',
          callbacks: {
            label: (item, data) =>
              data['datasets'][item.datasetIndex]['data'][item['index']].toFixed(2),
          },
        },
        legend: { position: 'top', labels: { usePointStyle: true } },
        scales: {
          xAxes: [
            {
              type: 'category',
              position: 'bottom',
              labels,
              scaleLabel: { labelString: 'State', display: true },
            },
          ],
          yAxes: [
            {
              type: 'linear',
              position: 'left',
              scaleLabel: { labelString: 'R\u2080', display: true },
              ticks: {
                suggestedMax: 4,
                suggestedMin: 0,
                stepSize: 0.5,
              },
            },
            {
              position: 'right',
              scaleLabel: { labelString: '% Susceptible', display: true },
              ticks: {
                min: 0,
                max: 4,
                stepSize: 0.5,
                callback: (label, index, labels) => {
                  switch (label) {
                    case 1:
                      return 100
                    case 1.5:
                      return 66.7
                    case 2:
                      return 50
                    case 2.5:
                      return 40
                    case 3:
                      return 33.3
                    case 4:
                      return 25
                  }
                },
              },
            },
          ],
        },
      },
    })
  }

  afterUpdate(() => {
    chart.data.datasets[2].data = circleData
    chart.data.datasets[0].data = lineData
    changeColors()
    chart.update()
  })
</script>

<canvas id="chart" class="col-md-9" />
