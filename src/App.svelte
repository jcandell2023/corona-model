<script>
  import data from './data/data'
  import Intro from './components/Intro.svelte'
  import Info from './components/Info.svelte'
  import Graph from './components/Graph.svelte'
  import Footer from './components/Footer.svelte'
</script>

<style>

</style>

<Intro />
<hr class="m-0" />
<Info />
<hr class="m-0" />
<Graph {data} />
<hr class="m-0" />
<Footer />
