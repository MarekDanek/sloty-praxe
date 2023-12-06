<script>
  import { onMount } from 'svelte';

  export let headers;
  export let rows;

  const renderFunctions = {
    name: (value) => `${value}`,
    level: (value) => `<strong>${value}</strong>`,
    type: (value) => `<strong>${value}</strong>`,
    ability: (value) => `<strong>${value}</strong>`,
  };

  let minLevel;
  let maxLevel;

  let sortKey = 'level'; 

  let visibleRows = [];
  let sortedRows = [];

  onMount(() => {
    minLevel = Math.min(...rows.map(row => row.level));
    maxLevel = Math.max(...rows.map(row => row.level));
    visibleRows = rows.slice();
  });

  $: sortedRows = [...visibleRows].sort((a, b) => {
    if (sortKey === 'level') {
      return b.level - a.level;
    } else {
     
      return a[sortKey].localeCompare(b[sortKey]);
    }
  });
</script>

<style>
  table {
    border: solid black 2px;
    border-collapse: collapse;
    width: 100%;
  }

  th, td {
    border: solid black 1px;
    padding: 8px;
    text-align: left;
  }

  th {
    background-color: grey;
    cursor: pointer;
  }
</style>

<!-- <table>
  <thead>
    <tr>
      {#each headers as { key, value }}
        <th on:click={() => sortKey = key}>{value}</th>
      {/each}
    </tr>
  </thead>
  <tbody>
    {#each sortedRows as row (row.id)}
      <tr>
        {#each headers as { key }}
          <td>
            {#if renderFunctions[key]}
              {@html renderFunctions[key](row[key])}
            {:else}
              {#if slot[key]}
                {#if slot[key] === 'name'}
                  {@html slot[key](row[key])}
                {/if}
              {:else}
                {slot[key]}
              {/if}
            {/if}
          </td>
        {/each}
      </tr>
    {/each}
  </tbody>
</table> -->


<table>
  <thead>
    <tr>
      {#each headers as { key, value }}
        <th on:click={() => sortKey = key }>{value}</th>
      {/each}
    </tr>
  </thead>
  <tbody>
    {#each rows as row, i (i)}
      <tr>
        {#each headers as item}
          {#if item.slot}
            <td></td>
          {:else}
            <td>{row[item.key]}</td>
          {/if}
        {/each}
      </tr>
    {/each}
  </tbody>
</table>
