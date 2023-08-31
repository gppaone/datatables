<script>
    export let headings;


</script>

{#each headings as column}
    <th data-sort={column.sort} class="tableheader" on:click={}>{column.name}</th>
{/each}
