<script>
    import data from "../assets/data.json";
    import TableRow from "./TableRow.svelte";
    let headings = [
            {
            "name":"Port",
            "field":"port",
            "sort":true
            },
            {
            "name":"Patch To",
            "field":"patch_to",
            "sort":false
            },
            {
            "name":"VLAN",
            "field":"vlan",
            "sort":false
            },
            {
            "name":"Power",
            "field":"power",
            "sort":false
            },
            {
            "name":"Status",
            "field":"status",
            "sort":false
            },
            {
            "name":"Jack",
            "field":"jack",
            "sort":false
            },
            {
            "name":"Outlet",
            "field":"outlet",
            "sort":false
            },
            {
            "name":"Room",
            "field":"room",
            "sort":false
            },
            {
            "name":"Floor",
            "field":"floor",
            "sort":false
            }
        ];
        let sortBy = {col: "id", ascending: true};
        let datasorted = data;
        $: sort = (column) => {
            
            if (sortBy.col == column) {
                sortBy.ascending = !sortBy.ascending
            } else {
                sortBy.col = column
                sortBy.ascending = true
            }
            
            // Modifier to sorting function for ascending or descending
            let sortModifier = (sortBy.ascending) ? 1 : -1;
            
            let sort = (a, b) => 
                (a[column] < b[column]) 
                ? -1 * sortModifier 
                : (a[column] > b[column]) 
                ? 1 * sortModifier 
                : 0;
            
            datasorted = data.sort(sort);
        }
</script>

<table class="table table-striped" id="table1">
    <thead>
        {#each headings as column, i}
            <th data-sort={column.sort} class="tableheader" on:click={()=>sort(column.field)}>{column.name}</th>
        {/each}
    </thead>
    <tbody>
        {#each datasorted as row, i}
            <TableRow {row} />
        {/each}
    </tbody>
</table>
<ul><li><button class="flex items-center font-medium h-10 px-4 text-base border text-gray-500 bg-white hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white rounded-l-lg"><span class="sr-only" data-svelte-h="svelte-z31jm6">Previous</span> <svg xmlns="http://www.w3.org/2000/svg" fill="none" class="shrink-0 w-3 h-3" role="img" aria-label="chevron-left-outline" viewBox="0 0 6 11">   <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="m5 1.549-4 3.79 4 3.792"></path>  </svg></button></li><li><a>1</a></li><li><a>2</a></li><li><a>3</a></li><li><a>4</a></li></ul>