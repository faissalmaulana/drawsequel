<script>
    import AddIcon from "./icons/AddIcon.svelte";
    import TableItem from "./TableItem.svelte";

    let { tables = $bindable() } = $props();

    function handleCreateTable() {
        const totalTables = tables.length;

        const newTable = {
            id: crypto.randomUUID(),
            type: "tableNode",
            position: { x: 0, y: 0 },
            data: {
                title: `Tables ${totalTables + 1}`,
                list: [
                    {
                        name: "",
                        type: "",
                        constraint: "",
                    },
                ],
            },
        };

        tables = [...tables, newTable];
    }

    /**
     * creates a table editor function bound to a specific table ID
     *
     * @param {string} id - The table ID to bind the editor to
     * @returns {(newData: Object) => void} Editor function that updates table.data
     *
     * @example
     * // Bind editor to specific table
     * <TableItem handleEditTable={handleEditTable(table.id)} />
     *
     * // Then use inside TableItem
     * handleEditTable({ title: "Updated Title" })
     */
    function handleEditTable(id) {
        return function (newData) {
            // remove 'id' from newData to prevent it from being updated
            const { id: _, ...safeData } = newData;

            tables = tables.map((table) =>
                table.id === id
                    ? { ...table, data: { ...table.data, ...safeData } }
                    : table,
            );
        };
    }
</script>

<div class="w-1/4 shadow-lg">
    <header class="flex justify-between align-middle p-3 shadow-sm">
        <h4 class="text-2xl font-medium">Tables</h4>
        <button class="cursor-pointer" onclick={handleCreateTable}>
            <AddIcon />
        </button>
    </header>

    {#each tables as table}
        <TableItem {table} handleEditTable={handleEditTable(table.id)} />
    {/each}
</div>
