<!-- App.svelte -->
<script>
	import { onMount } from 'svelte';
	import dayjs from 'dayjs';
	import mix from 'mix-color';

	//time variables
	let now = dayjs();
	let hour = now['$H'];
	let minute = now["$m"];
	let dayProgress = (((hour + minute / 60) / 24) * 100).toFixed(0);
	let hourProgress = (minute/60).toFixed(2);
	console.log(`hour progress = ${hourProgress}`)
	console.log(now);
	//console.log(`day progress = ${dayProgress}`)
	//color variables
	const colorAnchorsAM = ["41,40,61","42,40,60","50,43,61","65,47,63","90,53,67","131,62,75","189,77,85","206,119,99","223,193,126","242,220,137","250,238,142","252,248,146"];
	const colorAnchorsPM = [...colorAnchorsAM.reverse()];
	console.log(colorAnchorsPM);
	let backgroundcolor = mix(`rgb(${colorAnchorsPM[5]})`,`rgb(${colorAnchorsPM[7]})`, 0.15);

	onMount(() => {
		const interval = setInterval(() => {
			now = dayjs();
			hour = now['$H'];
			minute = now["$m"];
			console.log(`The time is ${hour}:${minute} and the day is ${dayProgress}% complete`);
		}, 10000);
		return () => {
			clearInterval(interval);
		};
	});
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
<header style="background-color: {backgroundcolor}" class="App-header">
		<img src="/logo.svg" class="App-logo" alt="logo" />
	</header>
</div>
