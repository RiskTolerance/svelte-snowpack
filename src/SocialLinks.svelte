<script>
	import { onMount } from 'svelte';
	import { fade } from 'svelte/transition';
	import tilt from './tilt.js';

	let loaded = false;
	let reverse = false;
	onMount(() => {
		setTimeout(() => {
			loaded = true;
		}, 1500);
	});
</script>

<style>
	#social-links {
		width: 50vmin;
		height: 8vmin;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		padding-top: 30px;
		z-index: 1;
	}
	.icon {
		height: 7vmin;
		width: auto;
		margin: 0 15px;
	}
	.icon:hover {
		scale: 1.1;
	}
</style>

<div use:tilt={{ scale: 1.1, reverse }} id="social-links">
	{#if loaded}
		<a href="https://discord.gg/cB777Db" target="_blank"><img
				transition:fade={{ duration: 2000 }}
				class="icon"
				alt="Discord Logo"
				src="/discord_icon.svg" /></a>
		<a
			href="https://www.instagram.com/foreststreamstudios/"
			target="_blank"><img
				transition:fade={{ duration: 2000 }}
				class="icon"
				alt="Instagram Logo"
				src="/instagram_icon.svg" /></a>
		<a
			href="https://www.facebook.com/pg/foreststreamstudios/about/"
			target="_blank"><img
				transition:fade={{ duration: 2000 }}
				class="icon"
				alt="Facebook Logo"
				src="/facebook_icon.svg" /></a>
		<a href="https://twitter.com/FStreamStudios" target="_blank"><img
				transition:fade={{ duration: 2000 }}
				class="icon"
				alt="Twitter Logo"
				src="/twitter_icon.svg" /></a>
	{/if}
</div>
