<script>
    import Sidebar from "../components/Sidebar.svelte";
    import Editor from "../components/Editor.svelte";
    import Navbar from "../components/Navbar.svelte";

    // percentage
    const MAX_SIZE = 20;
    const MIN_SIZE = 10;

    class SidebarWidth {
        #width = $state(0); // percentage
        isResizing = $state(false);

        constructor(width) {
            this.#width = width;
        }

        get width() {
            return this.#width;
        }

        set width(value) {
            if (typeof value !== "number" || Number.isNaN(value)) {
                return;
            }

            // clamp
            this.#width = Math.max(MIN_SIZE, Math.min(value, MAX_SIZE));
        }

        startResize = (e) => {
            this.isResizing = true;
        };

        onMove = (e) => {
            if (!this.isResizing) return;

            const percent = (e.clientX / window.innerWidth) * 100;

            // update with setter
            this.width = percent;
        };

        stopResize = () => {
            this.isResizing = false;
        };
    }

    const sidebarWidth = new SidebarWidth(MAX_SIZE);
</script>

<main>
    <Navbar />
    <div class="flex h-screen gap-x-2 mt-3">
        <Sidebar {sidebarWidth} />
        <Editor occupiedWidth={sidebarWidth.width} />
    </div>
</main>
