<script>
  import Chart from 'chart.js'
  import data from './data/newData'
  import Plot from './components/Plot.svelte'
  import { onMount } from 'svelte'

  const millisDay = 86400000
  let day = 1
  const startDate = new Date(2020, 1, 15)
  let date = new Date()
  $: {
    date.setTime(startDate.getTime() + millisDay * (day - 1))
    date = date
  }

  let plotData = data[1]
  let labels = data[0]
  let limits = plotData[0][1]

  let interval = null

  const playAnimation = () => {
    if (!interval) {
      interval = window.setInterval(() => {
        if (day < 400) {
          day++
        } else {
          window.clearInterval(interval)
        }
      }, 50)
    }
  }

  const reset = () => {
    day = 1
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
      circleData={plotData[day - 1][0]}
      lineData={plotData[day - 1][1]}
      {labels}
      limitData={limits} />
  </div>
  <div class="row">
    <p class="col-lg-1 text-center">{date.toLocaleDateString()}</p>
    <input
      class="custom-range col-lg-8"
      type="range"
      min="1"
      max="400"
      bind:value={day} />
    <div class="btn-group col-lg-2" role="group">
      <button class="btn btn-success btn-sm" on:click={playAnimation}>Play</button>
      <button class="btn btn-warning btn-sm" on:click={stop}>Pause</button>
      <button class="btn btn-danger btn-sm" on:click={reset}>Reset</button>
    </div>
  </div>

</div>
