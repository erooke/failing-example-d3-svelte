<script>
  import {scaleLinear, extent} from 'd3';
  import * as d3 from 'd3';

  let entries = []

  function addEntry() {
    const i = entries.length + 1
    entries = [ ...entries, {x: i, y: i * 10} ]
  }

  // D3 Logic
  const width = 800;
  const height = 300;

  let svg;

  $: if (svg) {
    const xScale = scaleLinear()
      .domain(extent(entries, (e) => e.x))
      .range([0, width])

    const yScale = scaleLinear()
      .domain(extent(entries, (e) => e.y))
      .range([height,0])

    d3.select(svg)
      .selectAll("circle")
      .data(entries, d => d)
      .join("svg:circle")
      .attr("cx", (e) => xScale(e.x))
      .attr("cy", (e) => yScale(e.y))
      .attr("r", 5)
  }
</script>

<main>
  <h1>D3 Example</h1>
  <button on:click={addEntry}> Add Entry </button>
  <div>
  <svg bind:this={svg} {width} {height}>
  </svg>
  </div>
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
