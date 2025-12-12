<script>
    import { Background, Controls, SvelteFlow } from "@xyflow/svelte";
    import "@xyflow/svelte/dist/style.css";
    import Node from "./Node.svelte";

    let { nodes = $bindable(), edges = $bindable() } = $props();

    const nodeTypes = { tableNode: Node };
</script>

<div class="w-5/6 bg-blue-500">
    <SvelteFlow bind:nodes bind:edges {nodeTypes}>
        <Controls />
        <Background />
    </SvelteFlow>
</div>
