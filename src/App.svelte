<script>
  import Chart from 'chart.js'
  import { onMount, afterUpdate } from 'svelte'
  import data from './data/data'
  import Plot from './components/Plot.svelte'

  let day = 1
  let dotData = []
  let lineData = []
  for (let d = 0; d < 400; d++) {
    let dayData1 = []
    let dayData2 = []
    for (let i = 0; i < data.length; i++) {
      //dayData.push({ x: i + 1, y: 1 / (1 - data[i][1][d]) })
      dayData1.push(1 / (1 - data[i][1][d]))
      dayData2.push(data[i][2][d])
    }
    dotData.push(dayData1)
    lineData.push(dayData2)
  }

  let labels = []
  let limits = []
  for (let i = 0; i < data.length; i++) {
    labels.push(data[i][0])
    limits.push(data[i][2][0])
  }

  let limitData = []

  $: {
    for (let i = 0; i < data.length; i++) {
      limitData[i] = limits[i] - lineData[day - 1][i]
    }
  }

  let interval

  const playAnimation = () => {
    interval = window.setInterval(() => {
      if (day < 400) {
        day++
      } else {
        window.clearInterval(interval)
      }
    }, 50)
  }

  const reset = () => {
    day = 1
    window.clearInterval(interval)
  }

  const stop = () => {
    window.clearInterval(interval)
  }
</script>

<style>

</style>

<div class="container">
  <Plot circleData={dotData[day - 1]} lineData={lineData[day - 1]} {labels} {limitData} />
  <input class="custom-range" type="range" min="1" max="400" bind:value={day} />
  <p>{day}</p>
  <button class="btn btn-success" on:click={playAnimation}>Play</button>
  <button class="btn btn-warning" on:click={stop}>Stop</button>
  <button class="btn btn-danger" on:click={reset}>Reset</button>
</div>
