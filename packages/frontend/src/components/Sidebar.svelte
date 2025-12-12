<script>
    import AddIcon from "./icons/AddIcon.svelte";

    let type = $state(""); // raw type state
    let showTypePopup = $state(false);

    const types = [
        "bigint",
        "boolean",
        "blob",
        "varchar(255)",
        "date",
        "datetime",
    ];

    const typeCtrl = {
        get value() {
            return type;
        },
        set value(v) {
            type = v;
        },
    };

    function selectType(t) {
        typeCtrl.value = t; // use controller
        showTypePopup = false;
    }
</script>

<div class="w-1/4 shadow-lg">
    <header class="flex justify-between align-middle p-3 shadow-sm">
        <h4 class="text-2xl font-medium">Tables</h4>
        <button>
            <AddIcon />
        </button>
    </header>

    <div class="border">
        <div class="border p-1 px-2">
            <form action="">
                <input type="text" value="Table Name" />
                <button class="bg-green-400 p-0.5 text-white cursor-pointer">
                    Done
                </button>
            </form>
        </div>

        <form class="p-3">
            <div
                class="grid grid-cols-5 gap-1 items-center border p-1 rounded-lg"
            >
                <input
                    type="text"
                    placeholder="column"
                    class="col-span-2 px-2 py-1 border rounded-md text-sm"
                />

                <!-- ================= TYPE FIELD WITH POPUP ================= -->
                <div class="relative col-span-1 type-wrapper">
                    <input
                        readonly
                        bind:value={typeCtrl.value}
                        placeholder="type"
                        class="w-full px-2 py-1 border rounded-md text-sm cursor-pointer"
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

                <div class="bg-green-400 rounded-md text-xs p-1 text-center">
                    block 3
                </div>
                <div class="bg-red-400 rounded-md text-xs p-1 text-center">
                    block 4
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
</div>
