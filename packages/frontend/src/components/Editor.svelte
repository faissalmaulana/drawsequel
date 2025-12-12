<script>
    import { Background, Controls, SvelteFlow } from "@xyflow/svelte";
    import "@xyflow/svelte/dist/style.css";

    let { nodes = $bindable(), edges = $bindable() } = $props();
</script>

<div class="w-5/6 bg-blue-500">
    <SvelteFlow bind:nodes bind:edges fitView>
        <Controls />
        <Background />
    </SvelteFlow>
</div>
