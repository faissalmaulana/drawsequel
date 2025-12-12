<script>
    let { data } = $props();
</script>

<div class="shadow bg-white border border-gray-200">
    <div class="px-2 py-1 bg-green-700">
        <p class="text-white text-sm font-semibold">{data.title}</p>
    </div>

    {#each data.list as menu}
        <div
            class="grid grid-cols-[28px_1fr_auto] items-center px-2 py-1 text-xs"
        >
            <p class="text-gray-400">
                {menu.constraint}
            </p>

            <p>
                {menu.name}
            </p>

            <p class="text-gray-400 whitespace-nowrap pl-4">
                {menu.type}
            </p>
        </div>
    {/each}
</div>
