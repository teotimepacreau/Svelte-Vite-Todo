<script>
    let filters = ['All', 'Active', 'Completed']

    export let setFilter
    export let selectedFilter
</script>

<div class="filters">
    {#each filters as filter}
        <button on:click={()=>setFilter(filter)} 
        class:selected={selectedFilter === filter}>{filter}</button>
    {/each}
</div>

<style>
    /* Filters */

  .filters {
    display: flex;
  }

  .filter {
    text-transform: capitalize;
    padding: var(--spacing-4) var(--spacing-8);
    border: 1px solid transparent;
    border-radius: var(--radius-base);
  }

  .filter:hover {
    border: 1px solid var(--color-highlight);
  }

  .selected {
    border-color: var(--color-highlight);
  }
</style>