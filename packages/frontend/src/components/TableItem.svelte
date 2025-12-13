<script>
    import CheckIcon from "./icons/CheckIcon.svelte";
    import PenIcon from "./icons/PenIcon.svelte";
    import ColumnRow from "./ColumnRow.svelte";

    let {
        table,
        handleEditTable,
        initialEditMode = false,
        handleAddNewColumn,
    } = $props();

    /**
     * hold title input value
     * @type {string}
     */
    let titleInput = $state("");

    /**
     * state for displaying table name as form to be editable
     * @type {boolean}
     */
    let editMode = $state(false);

    /**
     * track if initial setup has been done
     * @type {boolean}
     */
    let initialized = $state(false);

    // initialize edit mode once when initialEditMode is true
    $effect(() => {
        if (initialEditMode && !initialized) {
            titleInput = table.data.title;
            editMode = true;
            initialized = true;
        }
    });

    /**
     * action to focus input when mounted
     * @param {HTMLInputElement} node
     * @param {boolean} shouldFocus
     */
    function focusInput(node, shouldFocus) {
        if (shouldFocus) {
            node.focus();
            node.select();
        }
    }

    /**
     * reference to input element
     * @type {HTMLInputElement | null}
     */
    let inputRef = $state(null);

    /**
     * to set editMode on
     */
    function switchEditMode() {
        titleInput = table.data.title;
        editMode = true;

        // focus after DOM updates
        setTimeout(() => {
            inputRef?.focus();
        }, 0);
    }

    /**
     * handle title input submission
     * @param {Event} e
     */
    function handleTitleInput(e) {
        e.preventDefault();

        handleEditTable({ title: titleInput });
        exitEditMode();
    }

    /**
     * exit edit mode
     */
    function exitEditMode() {
        editMode = false;
    }
</script>

<div class="mt-4 border">
    <div class="border p-1 px-2">
        {#if !editMode}
            <div class="flex justify-between px-1">
                <p class="text-lg">{table.data.title}</p>
                <button onclick={switchEditMode} class="cursor-pointer">
                    <PenIcon width={"16"} height={"16"} />
                </button>
            </div>
        {:else}
            <form
                class="flex justify-between align-middle"
                onsubmit={handleTitleInput}
            >
                <input
                    bind:this={inputRef}
                    use:focusInput={initialEditMode}
                    type="text"
                    bind:value={titleInput}
                    class="border px-1"
                />
                <button type="submit" class="p-0.5 text-white cursor-pointer">
                    <CheckIcon />
                </button>
            </form>
        {/if}
    </div>

    <form class="p-3">
        {#each table.data.list as column}
            <div class="py-1">
                <ColumnRow {column} />
            </div>
        {/each}
    </form>

    <div class="flex my-2 justify-end-safe pr-3">
        <button
            class="border border-green-500 p-1 font-medium text-green-500 cursor-pointer"
            onclick={() => {
                handleAddNewColumn(table.id);
            }}
        >
            Add Column
        </button>
    </div>
</div>
