<script>
  import Plot from './Plot.svelte'

  const testBaseline = [3, 2.5, 2.2, 2, 1.75]
  const testCurrent = [
    [3, 2.5, 2.2, 2, 1.75],
    [2, 1.75, 1.2, 2, 1.5],
    [1, 1.1, 1.4, 1.8, 0.9],
    [1.5, 1.6, 1.6, 1.3, 1.1],
    [2, 1.5, 1.8, 1.6, 1.3],
  ]

  const testMin = [1, 1.1, 1.2, 1.3, 0.9]

  const testCircle = [
    [1, 1, 1, 1, 1],
    [1.05, 1.03, 1.17, 1.03, 1.13],
    [1.12, 1.09, 1.31, 1.11, 1.21],
    [1.26, 1.21, 1.37, 1.25, 1.25],
    [1.33, 1.29, 1.45, 1.32, 1.28],
  ]

  const labels = ['State 1', 'State 2', 'State 3', 'State 4', 'State 5']

  let day = 0
</script>

<style>

</style>

<div id="examplePlot">
  <h1 class="display-4 text-center">Example Graph</h1>
  <h3 class="text-center">Day {day + 1}</h3>
  <Plot
    circleData={testCircle[day]}
    lineData={testCurrent[day]}
    {labels}
    limitData={testBaseline}
    minData={testMin}
    id="exampleChart"
    parsed={true} />
  <!-- <canvas id="exampleChart" /> -->
  <input type="range" class="custom-range" min="0" max="4" bind:value={day} />
</div>
