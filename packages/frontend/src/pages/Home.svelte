<script>
    import Sidebar from "../components/Sidebar.svelte";
    import Editor from "../components/Editor.svelte";
    import Navbar from "../components/Navbar.svelte";

    let nodes = $state.raw([]);
    let edges = $state.raw([]);
</script>

<main>
    <Navbar />
    <div class="flex h-screen gap-x-2 mt-3">
        <Sidebar />
        <Editor bind:nodes bind:edges />
    </div>
</main>
