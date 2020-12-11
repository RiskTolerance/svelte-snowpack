<script>
    import { onMount } from 'svelte';
    import { fade } from 'svelte/transition';
    
    let loaded = false;
    onMount(() => {
        setTimeout(() => {
            loaded = true;
        },1000)
	});
</script>

<style>

#intro-text {
    display: flex;
    justify-content: end;
    text-align: center;
    color: white;
    width: 60vmin;
    height: 100px;
    padding: 25px 0;
    border-bottom: 4px solid white;
    font-size: calc(10px + 1vmin);
    z-index: 1;
}

p {
    text-shadow: 0px 0px 2px black;
}
</style>


<div id="intro-text">
    {#if loaded}
    <p transition:fade="{{ duration: 2000 }}">Welcome to Forest Stream Studios! Our site is still a work in progress, but you can follow our socials to keep in touch while we get things sorted here!</p>
    {/if}
</div>