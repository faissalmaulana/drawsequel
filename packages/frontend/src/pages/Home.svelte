<script>
    import Sidebar from "../components/Sidebar.svelte";
    import Editor from "../components/Editor.svelte";
    import Navbar from "../components/Navbar.svelte";
    import { SvelteFlowProvider } from "@xyflow/svelte";

    let nodes = $state.raw([
        {
            id: "1",
            type: "tableNode",
            position: { x: 100, y: 100 },
            data: {
                title: "Table Name ",
                list: [
                    {
                        name: "column",
                        type: "int",
                        constraint: "I",
                    },
                    {
                        name: "column",
                        type: "string",
                        constraint: "",
                    },
                    {
                        name: "column",
                        type: "string",
                        constraint: "",
                    },
                    {
                        name: "column",
                        type: "string",
                        constraint: "",
                    },
                ],
            },
        },
        {
            id: "2",
            type: "tableNode",
            position: { x: 400, y: 100 },
            data: {
                title: "Table Name ",
                list: [
                    {
                        name: "column",
                        type: "int",
                        constraint: "I",
                    },
                    {
                        name: "column",
                        type: "string",
                        constraint: "",
                    },
                    {
                        name: "column",
                        type: "string",
                        constraint: "",
                    },
                    {
                        name: "column",
                        type: "string",
                        constraint: "",
                    },
                ],
            },
        },
    ]);

    let edges = $state.raw([{ id: "e1-2", source: "1", target: "2" }]);
</script>

<main>
    <Navbar />
    <div class="flex h-screen gap-x-2">
        <SvelteFlowProvider>
            <Sidebar bind:tables={nodes} />
            <Editor bind:nodes bind:edges />
        </SvelteFlowProvider>
    </div>
</main>
