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
            label: 'Line Data',
            backgroundColor: 'rgba(255,0,0,.5)',
            data: lineData,
          },
          {
            label: 'Limit',
            backgroundColor: 'rgba(0,0,255,.5)',
            data: limitData,
          },
        ],
        labels,
      },
      options: {
        animation: {
          duration: 100,
        },
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
