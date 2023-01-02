<script context="module">
    export function push(hash) {
        window.location.hash = hash;
    }

    export function querystring() {
        let hash = window.location.hash;
        if (!hash.includes("?")) {
            return "";
        }
        return hash.substring(hash.lastIndexOf("?")).substring(1);
    }

    export function location() {
        return window.location.hash.substring(1);
    }

    export function replace(hash) {
        window.location.hash = hash;
    }
</script>

<script>
    import { onMount } from 'svelte';
    export let routes = {};

    let currentComponent;
    let params;

    function hashChanged() {
        
        let hash = document.location.hash.substring(1);
        
        if (hash === "") {
            hash = "/";
        }
    

        let comp = routes[hash];
        if (!comp) {
            for (let r in routes) {
                let regex = "^" + r.replaceAll(":id", ".+") + "$";
                if (hash.match(regex)) {
                    currentComponent = routes[r];
                    if (hash.includes("?")) {
                        hash = hash.substring(0, hash.indexOf("?"));
                    }
                    params = {id: hash.substring(hash.lastIndexOf("/")+1)};
                    return;
                }
            }
            currentComponent = null;
            params = null;
        } else {
            params = null;
            currentComponent = comp;
        }
    }
    onMount(() => hashChanged());
</script>

<svelte:window on:popstate={hashChanged} />
{#if currentComponent != null}
<svelte:component this={currentComponent} params={params} />
{:else}
<section><h1>Not found</h1><p>{location()}</p></section>
{/if}
