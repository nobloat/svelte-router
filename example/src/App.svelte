<script>
    import Router from "../../Router.svelte"
    import Component1 from "./Component1.svelte";
    import Component2 from "./Component2.svelte";

    let routes = {
        "/comp1": Component1,
        "/comp2/:id": Component2,
    }
</script>

<h1>This is the main App</h1>
<nav>
    <a href="#/comp1">Link to component 1</a>
    <a href="#/comp2/someid">Link to component 2 (parameter)</a>
</nav>
<hr>



<Router routes={routes} />

<footer>
    <hr>
    <a href="https://github.com/nobloat/svelte-router/">GitHub of nobloat/svelte-router</a>
</footer>