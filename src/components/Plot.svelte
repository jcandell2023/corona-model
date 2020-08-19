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
            pointRadius: 10,
            pointHitRadius: 0,
            backgroundColor: 'rgba(255,255,255,0)',
            borderColor: 'rgba(255,255,255,0)',
            data: circleData,
            type: 'line',
          },
          {
            label: 'Current Threshold',
            data: lineData,
            backgroundColor: 'rgba(0,0,0,0)',
            borderWidth: { left: 0, right: 0, bottom: 0, top: 1 },
            borderColor: 'rgba(255,0,0,1)',
          },
          {
            label: 'Normal Threshold',

            data: limitData,
            backgroundColor: 'rgba(0,0,0,0)',
            borderWidth: { left: 0, right: 0, bottom: 0, top: 1 },
            borderColor: 'rgba(0,200,0,1)',
          },
        ],
        labels,
      },
      options: {
        legend: { position: 'top', labels: { usePointStyle: true } },
        scales: {
          xAxes: [
            {
              type: 'category',
              position: 'bottom',
              labels,
              stacked: true,
            },
          ],
          yAxes: [
            {
              type: 'linear',
              position: 'left',
              stacked: true,
              ticks: {
                suggestedMax: 5,
                suggestedMin: 0,
                stepSize: 0.5,
              },
            },
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
