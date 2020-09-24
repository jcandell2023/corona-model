<script>
  import Plot from './Plot.svelte'
  export let data = null

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
  let limitData = plotData[0][1]
  let mins = []
  let minData = [...limitData]

  for (let s = 0; s < minData.length; s++) {
    let curMin = limitData[s]
    let mindex = 0
    for (let d = 0; d < 400; d++) {
      if (plotData[d][1][s] < curMin) {
        curMin = plotData[d][1][s]
        mindex = d
      }
    }
    mins.push({ min: curMin, ind: mindex })
  }

  $: {
    for (let i = 0; i < mins.length; i++) {
      if (mins[i].ind <= day) {
        minData[i] = mins[i].min
      } else {
        minData[i] = limitData[i]
      }
    }
  }

  let interval = null

  const playAnimation = () => {
    if (!interval && day < 399) {
      interval = window.setInterval(() => {
        if (day < 399) {
          day++
        } else {
          window.clearInterval(interval)
        }
      }, 100)
    }
  }

  const reset = (time) => {
    day = time
    window.clearInterval(interval)
    interval = null
  }

  const stop = () => {
    window.clearInterval(interval)
    interval = null
  }

  const toToday = () => {
    const today = new Date()
    const dif = today.getTime() - startDate.getTime()
    day = Math.floor(dif / millisDay)
    window.clearInterval(interval)
    interval = null
  }
</script>

<style>

</style>

<div id="graph" class="py-3">
  <div class="container">
    <h3 class="text-center">{date.toLocaleDateString()}</h3>
    <select name="states" id="stateSelect" multiple>
      <option value="ma">MA</option>
      <option value="ny">NY</option>
    </select>
    <Plot
      parsed
      circleData={plotData[day][0]}
      lineData={plotData[day][1]}
      {labels}
      {limitData}
      {minData} />
    <div class="row">
      <p class="col-lg-1 text-left">{date.toLocaleDateString()}</p>
      <input
        class="custom-range col-lg-8"
        type="range"
        min="0"
        max="399"
        bind:value={day}
        data-toggle="tooltip"
        data-placement="top"
        title={date.toLocaleDateString()} />
      <div class="btn-group col-lg-2" role="group">
        <button class="btn btn-outline-dark btn-sm" on:click={() => reset(0)}>
          <i class="material-icons">fast_rewind</i>
        </button>
        {#if interval}
          <button class="btn btn-outline-dark btn-sm" on:click={stop}>
            <i class="material-icons">pause</i>
          </button>
        {:else}
          <button class="btn btn-outline-dark btn-sm" on:click={playAnimation}>
            <i class="material-icons">play_arrow</i>
          </button>
        {/if}
        <button class="btn btn-outline-dark btn-sm" on:click={() => reset(399)}>
          <i class="material-icons">fast_forward</i>
        </button>
        <button class="btn btn-success btn-sm" on:click={toToday}>Today</button>
      </div>
    </div>
  </div>
</div>
