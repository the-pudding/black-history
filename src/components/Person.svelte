<script>
  import Line from "./Line.svelte";

  export let i;
  export let name;
  export let yearlyTotal;
  export let percentFebruary;
  export let lineData;
</script>

<div>
  <p>{i + 1}. {name}</p>
  <Line data={lineData} />
</div>

<style>
  div {
    /* background: steelblue;
    color: white; */
  }
</style>
