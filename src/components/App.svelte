<script>
  import * as d3 from "d3";
  import Person from "$components/Person.svelte";
  import Footer from "$components/Footer.svelte";
  import views from "$data/views.csv";
  import _ from "lodash";

  let sortBy = "yearlyTotal";
  $: data = sortData(sortBy);

  const sortData = (metric) => {
    return _.orderBy(views, (d) => parseFloat(d[metric]), "desc");
  };

  const getLineData = (raw) => {
    let timeParser = d3.timeParse("%m-%d");
    const justDates = _.omit(raw, ["yearlyTotal", "percentFebruary", "name", "februaryViews"]);
    const arr = _.keys(justDates).map((key) => ({
      date: timeParser(key),
      views: parseFloat(raw[key])
    }));
    return arr;
  };
</script>

<button on:click={() => (sortBy = "yearlyTotal")}>sort by yearly total</button>
<button on:click={() => (sortBy = "percentFebruary")}>sort by % february</button>
<button on:click={() => (sortBy = "februaryViews")}>sort by february views</button>

<div>
  {#each data as d, i}
    <Person
      {i}
      name={d.name}
      yearlyTotal={parseInt(d.yearlyTotal).toLocaleString()}
      percentFebruary={parseInt(d.percentFebruary)}
      lineData={getLineData(d)}
    />
  {/each}
</div>

<Footer />

<style>
  div {
    display: flex;
    flex-wrap: wrap;
  }
</style>
