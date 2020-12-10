<!-- App.svelte -->
<script>
	import { onMount } from 'svelte';
	import dayjs from 'dayjs';

	let now = dayjs();
	let hour = now['$H'];
	let minute = now["$m"];
	let count = 0;
	let dayProgress = Math.round(((hour + minute / 60) / 24) * 100);

	onMount(() => {
		const interval = setInterval(() => {
			count++;
			now = dayjs();
			hour = now['$H'];
			minute = now["$m"];
			console.log(`The time is ${hour}:${minute} and the day is ${dayProgress}% complete`);
		}, 10000);
		return () => {
			clearInterval(interval);
		};
	});

	let clicker = 0;
	$: doubled = clicker * 2;
	function handleClick() {
		if (clicker > 49) {
			alert(`no going over 100!`);
			clicker = 0;
			doubled = 0;
			return;
		}
		clicker += 1;
	}
</script>

<style>
	.App-header {
		background-color: #f9f6f6;
		color: #333;
		min-height: 100vh;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		font-size: calc(10px + 2vmin);
	}
	.App-logo {
		height: 36vmin;
		pointer-events: none;
		margin-bottom: 3rem;
		animation: App-logo-pulse infinite 1.6s ease-in-out alternate;
	}
	@keyframes App-logo-pulse {
		from {
			transform: scale(1);
		}
		to {
			transform: scale(1.06);
		}
	}
</style>

<div class="App">
	<header class="App-header">
		<img src="/logo.svg" class="App-logo" alt="logo" />
		<p>Page has been open for <code>{count}</code> seconds.</p>
		<button on:click={handleClick}>Clicked
			{clicker}
			{count === 1 ? 'time' : 'times'}</button>
		<p>{clicker} doubled is {doubled}</p>
	</header>
</div>
