<script>
  import * as d3 from "d3";

  export let data;

  let width = 300;
  let height = 200;
  let margin = { top: 0, right: 0, bottom: 0, left: 0 };

  $: xScale = d3
    .scaleTime()
    .domain(d3.extent(data, (d) => d.date))
    .range([0, width]);
  $: yScale = d3
    .scaleLinear()
    .domain([0, d3.max(data, (d) => d.views)])
    .range([height, 0]);
  $: lineGenerator = d3
    .line()
    .x((d) => xScale(d.date))
    .y((d) => yScale(d.views));

  console.log({ data });
</script>

<svg {width} {height}>
  <g transform={`translate(${margin.left}, ${margin.top})`}>
    <path d={lineGenerator(data)} />
  </g>
</svg>

<style>
  path {
    stroke: steelblue;
    fill: none;
  }
</style>
