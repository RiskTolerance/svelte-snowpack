<!-- App.svelte -->
<script>
	import { onMount } from 'svelte';
	import dayjs from 'dayjs';
	import mix from 'mix-color';

	let now = dayjs();
	let hour = now['$H'];
	let minute = now['$m'];
	//let dayProgress = (((hour + minute / 60) / 24) * 100).toFixed(0);
	let hourProgress = (minute / 60).toFixed(2);

	const colorAnchors = [
		'41,40,61',
		'42,40,60',
		'50,43,61',
		'65,47,63',
		'90,53,67',
		'131,62,75',
		'189,77,85',
		'206,119,99',
		'223,193,126',
		'242,220,137',
		'250,238,142',
		'252,248,146',
		// pass noon
		'252,248,146',
		'250,238,142',
		'242,220,137',
		'223,193,126',
		'206,119,99',
		'189,77,85',
		'131,62,75',
		'90,53,67',
		'65,47,63',
		'50,43,61',
		'42,40,60',
		'41,40,61',
	];
	let backgroundColor = `rgb(${colorAnchors[hour]})`;

	onMount(() => {
		const interval = setInterval(() => {
			now = dayjs();
			hour = now['$H'];
			minute = now['$m'];
			backgroundColor = mix(
				`rgb(${colorAnchors[hour]})`,
				`rgb(${colorAnchors[hour + 1]})`,
				`${hourProgress}`
			);
			//console.log(`The time is ${hour}:${minute} and the day is ${dayProgress}% complete`);
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
	<header style="background-color: {backgroundColor}" class="App-header">
		<img src="/logo.svg" class="App-logo" alt="logo" />
	</header>
</div>
