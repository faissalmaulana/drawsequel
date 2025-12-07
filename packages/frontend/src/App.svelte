<script>
    import { Router, Route } from "svelte5-router";
    import Home from "./pages/Home.svelte";
    import "./app.css";
</script>

<Router url="">
    <Route path="/" component={Home} />
</Router>
