<script>
  import { afterUpdate, onMount } from 'svelte'
  import Chart from 'chart.js'
  import { text } from 'svelte/internal'
  export let circleData = null
  export let lineData = null
  export let labels = null
  export let limitData = null
  export let minData = null
  export let id = 'chart'
  export let parsed = false

  $: if (!parsed) {
    circleData = circleData.map((val) => 1 / (1 - val))
  }

  const textWrap = (text, length) => {
    if (text.length <= length) {
      return text
    }

    let wrap = []
    text = text.split(' ')
    let line = []
    let lineLen = 0

    for (let i = 0; i < text.length; i++) {
      if (lineLen + text[i].length < length) {
        line.push(text[i])
        lineLen += text[i].length + 1
      } else {
        wrap.push(line.join(' '))
        line = []
        lineLen = 0
        line.push(text[i])
        lineLen += text[i].length
      }
    }
    wrap.push(line.join(' '))
    return wrap
  }

  const circleColor = []
  const lineColor = []
  for (let i = 0; i < circleData.length; i++) {
    circleColor.push('blue')
    lineColor.push('green')
  }

  let ctx
  let chart

  onMount(() => {
    ctx = document.getElementById(id)
    renderChart()
  })

  const changeColors = () => {
    const [, current] = chart.data.datasets
    for (let i = 0; i < current.data.length; i++) {
      if (lineData[i] === minData[i]) {
        current.pointBorderColor[i] = 'red'
      } else if (lineData[i] < limitData[i]) {
        current.pointBorderColor[i] = 'orange'
      } else {
        current.pointBorderColor[i] = 'green'
      }
    }
  }

  const renderChart = () => {
    chart = new Chart(ctx, {
      type: 'bar',
      data: {
        datasets: [
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
            label: 'New Normal R\u2080',
            pointStyle: 'line',
            type: 'line',
            pointBorderColor: 'orange',
            pointBorderWidth: 3,
          },
          {
            label: 'Crisis R\u2080',
            pointStyle: 'line',
            type: 'line',
            pointBorderColor: 'red',
            pointBackgroundColor: 'red',
            pointBorderWidth: 3,
            data: minData,
            pointRadius: 10,
            pointHoverRadius: 9,
            pointHoverBorderWidth: 2,
            borderWidth: 3,
            backgroundColor: 'rgba(255,255,255,0)',
            borderColor: 'rgba(255,255,255,0)',
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
          position: 'nearest',
          titleAlign: 'center',
          footerAlign: 'center',
          filter: (item, data) => {
            if (item.datasetIndex == 1) {
              return lineData[item.index] !== minData[item.index]
            } else if (item.datasetIndex === 3) {
              return minData[item.index] !== limitData[item.index]
            }
            return true
          },
          callbacks: {
            label: (item, data) => {
              if (item.datasetIndex == 4) {
                return (
                  (
                    100 / data['datasets'][item.datasetIndex]['data'][item['index']]
                  ).toFixed(2) + '%'
                )
              }
              return data['datasets'][item.datasetIndex]['data'][item['index']].toFixed(2)
            },
            footer: (items, data) => {
              const ind = items[0].index
              if (circleData[ind] < lineData[ind]) {
                let text = `The current effective R for this outbreak is ${
                  lineData[ind]
                }*${(1 / circleData[ind]).toFixed(2)} = ${(
                  lineData[ind] / circleData[ind]
                ).toFixed(
                  2
                )}. Since this number is above 1, this location is still predicted to have exponential spread.`
                return textWrap(text, 42)
              } else if (
                circleData[ind] >= lineData[ind] &&
                circleData[ind] < limitData[ind]
              ) {
                let text = `The current effective R for this outbreak is ${
                  lineData[ind]
                }*${(1 / circleData[ind]).toFixed(2)} = ${(
                  lineData[ind] / circleData[ind]
                ).toFixed(
                  2
                )}. Since this number is below 1, this location is expected to be past its peak in new cases. However, if we went back to “old normal” interactions, the effective R would still be greater than 1.`
                return textWrap(text, 42)
              } else if (circleData[ind] >= limitData[ind]) {
                let text = `In this location, even if “old normal” interactions were resumed, the effective R, ${
                  limitData[ind]
                }*${(1 / circleData[ind]).toFixed(2)} = ${(
                  limitData[ind] / circleData[ind]
                ).toFixed(
                  2
                )} is less than 1. This location has passed the herd immunity threshold and can move toward interactions similar to those during pre-pandemic times without risking a new exponential growth in cases.`
                return textWrap(text, 46)
              }
              return ''
            },
          },
        },
        legend: {
          position: 'top',
          display: true,
          labels: {
            filter: (item, ind, data) => item.text != 'Current R\u2080',
            usePointStyle: true,
          },
        },
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

  $: {
    chart.data.datasets[4].data = circleData
    chart.data.datasets[1].data = lineData
    chart.data.datasets[3].data = minData
    changeColors()
    chart.update()
  }
</script>

<canvas {id} class="col-xl-10 offset-xl-1" />
