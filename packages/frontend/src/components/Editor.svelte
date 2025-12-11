<script>
    import { Background, Controls, SvelteFlow } from "@xyflow/svelte";
    import "@xyflow/svelte/dist/style.css";

    let { nodes = $bindable(), edges = $bindable(), occupiedWidth } = $props();
</script>

<div class=" bg-blue-500" style:width="{100 - occupiedWidth}%">
    <SvelteFlow bind:nodes bind:edges fitView>
        <Controls />
        <Background />
    </SvelteFlow>
</div>
