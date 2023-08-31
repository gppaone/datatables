<script>
    import TableCell from "./TableCell.svelte";
    export let row;
</script>

<tr>
    {#each Object.values(row) as cell}
        <TableCell cell={cell} />
    {/each}
</tr>