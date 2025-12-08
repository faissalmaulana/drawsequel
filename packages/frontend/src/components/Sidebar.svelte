<script>
    const { sidebarWidth } = $props();
</script>

<svelte:window
    onpointermove={sidebarWidth.onMove}
    onpointerup={sidebarWidth.stopResize}
/>

<div class=" bg-green-500 relative" style:width="{sidebarWidth.width}%">
    <div
        class="absolute top-0 right-0 w-1 h-full cursor-col-resize transition-colors"
        role="separator"
        aria-label="Resize sidebar"
        onpointerdown={sidebarWidth.startResize}
    ></div>
</div>
