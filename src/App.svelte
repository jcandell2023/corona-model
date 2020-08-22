<script>
  import Chart from 'chart.js'
  import data from './data/newData'
  import Plot from './components/Plot.svelte'
  import { onMount } from 'svelte'

  const millisDay = 86400000
  let day = 0
  const startDate = new Date(2020, 1, 15)
  let date = new Date()
  $: {
    date.setTime(startDate.getTime() + millisDay * day)
    date = date
  }

  let plotData = data[1]
  let labels = data[0]
  let limits = plotData[0][1]
  let min = []
  let minData = [...limits]

  for (let s = 0; s < 20; s++) {
    let curMin = limits[s]
    let mindex = 0
    for (let d = 0; d < 400; d++) {
      if (plotData[d][1][s] < curMin) {
        curMin = plotData[d][1][s]
        mindex = d
      }
    }
    min.push({ min: curMin, ind: mindex })
  }

  $: {
    for (let i = 0; i < min.length; i++) {
      if (min[i].ind <= day) {
        minData[i] = min[i].min
      } else {
        minData[i] = limits[i]
      }
    }
  }

  let interval = null

  const playAnimation = () => {
    if (!interval) {
      interval = window.setInterval(() => {
        if (day < 399) {
          day++
        } else {
          window.clearInterval(interval)
        }
      }, 100)
    }
  }

  const reset = () => {
    day = 0
    window.clearInterval(interval)
    interval = null
  }

  const stop = () => {
    window.clearInterval(interval)
    interval = null
  }
</script>

<style>
  .img-container {
    padding: 0;
  }
</style>

<div class="container">
  <h1 class="display-4 text-center">Corona Virus Model</h1>
  <div class="row" />

  <h3 class="text-center">{date.toLocaleDateString()}</h3>

  <div class="row">
    <div class="col-md-3 img-container">
      <img src="img/R0_params.png" alt="Explanation" class="img-fluid" />
    </div>

    <Plot
      circleData={plotData[day][0]}
      lineData={plotData[day][1]}
      {labels}
      min={minData}
      limitData={limits} />
  </div>
  <div class="row">
    <p class="col-lg-1 text-left">{date.toLocaleDateString()}</p>
    <input
      class="custom-range col-lg-8"
      type="range"
      min="0"
      max="399"
      bind:value={day} />
    <div class="btn-group col-lg-2" role="group">
      <button class="btn btn-success btn-sm" on:click={playAnimation}>Play</button>
      <button class="btn btn-warning btn-sm" on:click={stop}>Pause</button>
      <button class="btn btn-danger btn-sm" on:click={reset}>Reset</button>
    </div>
  </div>

</div>
