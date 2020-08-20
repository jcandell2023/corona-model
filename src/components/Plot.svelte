<script>
  import { afterUpdate, onMount } from 'svelte'
  export let circleData = null
  export let lineData = null
  export let labels = null
  export let limitData = null

  let ctx
  let chart

  onMount(() => {
    ctx = document.getElementById('chart')
    renderChart()
  })

  const renderChart = () => {
    if (chart) chart.destroy()
    chart = new Chart(ctx, {
      type: 'bar',
      data: {
        datasets: [
          {
            label: 'Circle Data',
            pointBackgroundColor: 'blue',
            pointBorderColor: 'blue',
            pointRadius: 10,
            backgroundColor: 'rgba(255,255,255,0)',
            borderColor: 'rgba(255,255,255,0)',
            data: circleData,
            pointStyle: 'circle',
            type: 'line',
          },
          {
            label: 'Current Threshold',
            pointBackgroundColor: 'rgba(255,0,0,1)',
            pointBorderColor: 'rgba(255,0,0,1)',
            pointRadius: 15,
            borderWidth: 3,
            backgroundColor: 'rgba(255,255,255,0)',
            borderColor: 'rgba(255,255,255,0)',
            data: lineData,
            pointStyle: 'line',
            type: 'line',
          },
          {
            label: 'Normal Threshold',
            pointBackgroundColor: 'rgba(0,200,0,1)',
            pointBorderColor: 'rgba(0,200,0,1)',
            pointRadius: 15,
            borderWidth: 3,
            backgroundColor: 'rgba(255,255,255,0)',
            borderColor: 'rgba(255,255,255,0)',
            data: limitData,
            pointStyle: 'line',
            type: 'line',
          },
        ],
        labels,
      },
      options: {
        //tooltips: { enabled: false, custom: (tooltipModel) => {} },
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
              scaleLabel: { labelString: 'R0', display: true },
              ticks: {
                suggestedMax: 5,
                suggestedMin: 0,
                stepSize: 0.5,
              },
            },
            /*{
              type: 'linear',
              position: 'right',
              scaleLabel: { labelString: '% Susceptible', display: true },
            },*/
          ],
        },
      },
    })
  }

  afterUpdate(() => {
    chart.data.datasets[0].data = circleData
    chart.data.datasets[1].data = lineData
    chart.update()
  })
</script>

<canvas id="chart" />
