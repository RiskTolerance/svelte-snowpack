<!-- App.svelte -->
<script>
	import { onMount } from "svelte";
	import dayjs from "dayjs";
	import mix from "mix-color";
	import SocialLinks from "./SocialLinks.svelte";
	import IntroText from "./IntroText.svelte";
	import ForestStreamLogo from "./ForestStreamLogo.svelte";

	let now = dayjs();
	let hour = now["$H"];
	let minute = now["$m"];
	let dayProgress = (((hour + minute / 60) / 24) * 100).toFixed(0);
	console.log(dayProgress);
	let hourProgress = (minute / 60).toFixed(2);

	const colorAnchors = [
		"41,40,61",
		"42,40,60",
		"50,43,61",
		"65,47,63",
		"90,53,67",
		"131,62,75",
		"189,77,85",
		"206,119,99",
		"223,193,126",
		"242,220,137",
		"250,238,142",
		"252,248,146",
		// pass noon
		"252,248,146",
		"250,238,142",
		"242,220,137",
		"223,193,126",
		"206,119,99",
		"189,77,85",
		"131,62,75",
		"90,53,67",
		"65,47,63",
		"50,43,61",
		"42,40,60",
		"41,40,61",
	];
	let backgroundColor;
	const calcBgColor = () => {
		if (hour < 24) {
			backgroundColor = mix(
				`rgb(${colorAnchors[hour]})`,
				`rgb(${colorAnchors[hour + 1]})`,
				`${hourProgress}`
			);
		} else {
			backgroundColor = `rgb(${colorAnchors[hour]})`;
		}
	};
	calcBgColor();

	let fillColor = (hour < 9) | (hour > 14) ? "white" : "black";
	let textColor = (hour < 9) | (hour > 14) ? "white" : "black";

	onMount(() => {
		const interval = setInterval(() => {
			now = dayjs();
			hour = now["$H"];
			minute = now["$m"];
			hourProgress = (minute / 60).toFixed(2);
			calcBgColor();
			fillColor = (hour < 9) | (hour > 14) ? "white" : "black";
			textColor = (hour < 9) | (hour > 14) ? "white" : "black";
			//console.log(`The time is ${hour}:${minute} and the day is ${dayProgress}% complete`);
		}, 10000);
		return () => {
			clearInterval(interval);
		};
	});
</script>

<style>
	.App-header {
		position: absolute;
		height: 100vh;
		width: 100vw;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		font-size: calc(10px + 2vmin);
		overflow: hidden;
	}

	#background-image {
		position: absolute;
		bottom: -100px;
		margin: 0;
		width: 110vw;
		opacity: 50%;
		z-index: 0;
		mix-blend-mode: overlay;
	}
</style>

<div class="App">
	<header style="background-color: {backgroundColor}" class="App-header">
		<ForestStreamLogo {fillColor} />
		<IntroText {textColor} />
		<SocialLinks />
		<img id="background-image" src="/forest.webp" alt="forest" />
	</header>
</div>
