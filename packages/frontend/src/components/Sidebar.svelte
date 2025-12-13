<script>
    import AddIcon from "./icons/AddIcon.svelte";
    import AlphabetsIcon from "./icons/AlphabetsIcon.svelte";
    import CheckIcon from "./icons/CheckIcon.svelte";
    import CloseIcon from "./icons/CloseIcon.svelte";
    import DotsIcon from "./icons/DotsIcon.svelte";
    import KeyIcon from "./icons/KeyIcon.svelte";
    import PenIcon from "./icons/PenIcon.svelte";

    let { tables = $bindable() } = $props();

    /**
     * hold input value field type
     *
     * @type {string}
     */
    let type = $state("");

    /**
     * state for displaying pop up
     * of list value input field type
     *
     * @type {boolean}
     */
    let showTypePopup = $state(false);

    /**
     * state for displaying dots popup
     *
     * @type {boolean}
     */
    let showDotsPopup = $state(false);

    /**
     * state for displaying table name
     * as form to be editable
     * @type {boolean}
     */
    let editMode = $state(false);

    /**
     * reference to dots popup container
     * @type {HTMLElement | null}
     */
    let dotsPopupContainer = $state(null);

    /**
     * to set editMode on
     */
    function switchEditMode() {
        editMode = true;
    }

    /**
     * list values avaible to be setting in field type
     * @type {string[]}
     */
    const types = [
        "bigint",
        "boolean",
        "blob",
        "varchar(255)",
        "date",
        "datetime",
    ];

    /**
     * State controller to getting and setting
     * value from input field type
     */
    const typeCtrl = {
        get value() {
            return type;
        },
        set value(v) {
            type = v;
        },
    };

    /**
     * handler to setting value to type state
     * it also will close popup component after
     * setting value
     *
     * @param t {string}
     * @retuns {void}
     */
    function selectType(t) {
        // use controller setter
        typeCtrl.value = t;

        showTypePopup = false;
    }

    /**
     * handle click outside to close popup dots
     * @param e {MouseEvent}
     */
    function handleClickOutsideDots(e) {
        if (
            showDotsPopup &&
            dotsPopupContainer &&
            e.target instanceof Node &&
            !dotsPopupContainer.contains(e.target)
        ) {
            showDotsPopup = false;
        }
    }
</script>

<svelte:window onclick={handleClickOutsideDots} />

<div class="w-1/4 shadow-lg">
    <header class="flex justify-between align-middle p-3 shadow-sm">
        <h4 class="text-2xl font-medium">Tables</h4>
        <button class="cursor-pointer">
            <AddIcon />
        </button>
    </header>

    {#each tables as table}
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
                    <form class="flex justify-between align-middle" action="">
                        <input
                            type="text"
                            value="Table Name"
                            class="border px-1"
                        />
                        <button class=" p-0.5 text-white cursor-pointer">
                            <CheckIcon />
                        </button>
                    </form>
                {/if}
            </div>

            <form class="p-3">
                <div class="grid grid-cols-8 gap-1 items-center">
                    <input
                        type="text"
                        placeholder="column"
                        class="col-span-3 px-2 py-1 rounded-md text-sm shadow-sm"
                    />

                    <!-- ================= TYPE FIELD WITH POPUP ================= -->
                    <div class="relative col-span-2 type-wrapper">
                        <input
                            readonly
                            bind:value={typeCtrl.value}
                            placeholder="type"
                            class="w-full px-2 py-1 rounded-md text-sm cursor-pointer shadow-sm"
                            onclick={() => (showTypePopup = !showTypePopup)}
                        />

                        <!-- Popup -->
                        {#if showTypePopup}
                            <div
                                class="absolute left-0 top-full mt-1 w-40 bg-gray-900 text-white
                                       rounded-lg shadow-xl p-2 z-50"
                            >
                                <p class="text-xs text-gray-300 px-2 mb-1">
                                    DATA TYPE
                                </p>

                                {#each types as t}
                                    <button
                                        class="px-2 py-1 rounded cursor-pointer hover:bg-gray-700"
                                        onclick={() => selectType(t)}
                                    >
                                        {t}
                                    </button>
                                {/each}
                            </div>
                        {/if}
                    </div>

                    <div
                        class="text-xs text-center hover:bg-gray-200 rounded-sm"
                    >
                        <AlphabetsIcon letter="N" width="32" height="32" />
                    </div>

                    <div
                        class="text-xs p-1 text-center hover:bg-gray-200 rounded-sm"
                    >
                        <KeyIcon />
                    </div>

                    <!-- ================= DOTS WITH POPUP ================= -->
                    <div
                        bind:this={dotsPopupContainer}
                        class="relative text-xs p-1 text-center hover:bg-gray-200 rounded-sm"
                    >
                        <button
                            type="button"
                            onclick={() => (showDotsPopup = !showDotsPopup)}
                            class="cursor-pointer"
                        >
                            <DotsIcon />
                        </button>

                        <!-- Dots Popup -->
                        {#if showDotsPopup}
                            <div
                                class="absolute left-full top-0 ml-2 w-80 bg-gray-800 text-white
                                       rounded-lg shadow-xl p-4 z-50"
                            >
                                <div class="flex flex-col gap-4">
                                    <div
                                        class="flex justify-between items-center"
                                    >
                                        <h3
                                            class="text-sm font-semibold uppercase tracking-wide"
                                        >
                                            Column Attributes
                                        </h3>
                                        <button
                                            type="button"
                                            onclick={() =>
                                                (showDotsPopup = false)}
                                            class="text-gray-400 hover:text-white cursor-pointer"
                                        >
                                            <CloseIcon />
                                        </button>
                                    </div>
                                </div>
                            </div>
                        {/if}
                    </div>
                </div>
            </form>

            <div class="flex my-2 justify-end-safe pr-3">
                <button
                    class="border border-green-500 p-1 font-medium text-green-500 cursor-pointer"
                >
                    Add Column
                </button>
            </div>
        </div>
    {/each}
</div>
