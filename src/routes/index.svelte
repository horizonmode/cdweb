<script>
	const wallBuildTopLeft = [
		{ transform: 'translate3D(-50%, -50%, 0)' },
		{ opacity: 0.9 },
		{ transform: 'translate3D(0,0,0)', opacity: 1 }
	];

	const wallBuildTopRight = [
		{ transform: 'translate3D(50%, -50%, 0)' },
		{ opacity: 0.9 },
		{ transform: 'translate3D(0,0,0)', opacity: 1 }
	];

	const wallBuildBottomLeft = [
		{ transform: 'translate3D(-50%, 50%, 0)' },
		{ opacity: 0.9 },
		{ transform: 'translate3D(0,0,0)', opacity: 1 }
	];
	const wallBuildBottomRight = [
		{ transform: 'translate3D(50%, 50%, 0)' },
		{ opacity: 0.9 },
		{ transform: 'translate3D(0,0,0)', opacity: 1 }
	];
	const wallBuildMidRight = [
		{ transform: 'translate3D(50%, 0%, 0)' },
		{ opacity: 0.9 },
		{ transform: 'translate3D(0,0,0)', opacity: 1 }
	];
	const wallBuildTiming = {
		easing: 'ease-out',
		duration: 2000,
		iterations: 1,
		fill: 'both'
	};

	let animations = [];

	const play = () => {
		animations = [];

		animations.push(document.getElementById('topleft').animate(wallBuildTopLeft, wallBuildTiming));

		animations.push(
			document.getElementById('topright').animate(wallBuildTopRight, wallBuildTiming)
		);

		animations.push(
			document.getElementById('bottomleft').animate(wallBuildBottomLeft, wallBuildTiming)
		);

		animations.push(
			document.getElementById('bottomright').animate(wallBuildBottomRight, wallBuildTiming)
		);

		animations.push(
			document.getElementById('rightmid').animate(wallBuildMidRight, wallBuildTiming)
		);
	};

	const handleStart = (e) => {
		e.preventDefault();
		document.getElementById('instructions').style.opacity = '0.1';
		animations.forEach((a) => a.cancel());
		play();
	};

	const handleStop = (e) => {
		document.getElementById('instructions').style.opacity = '1';
		animations.forEach((a) => a.reverse());
	};
</script>

<div
	class="wrapper"
	on:mousedown={handleStart}
	on:touchstart={handleStart}
	on:mouseup={handleStop}
	on:touchend={handleStop}
>
	<svg id="wall" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100">
		<defs>
			<style>
				.cls- 1 {
					fill: #1d1d1b;
				}
			</style>
		</defs>
		<g id="Layer1">
			<path id="topleft" class="cls-1" d="M0,0V31.84L59.31,21.68a3.92,3.92,0,0,0,3-4.52L59.82,0Z" />
			<path
				id="bottomleft"
				class="cls-1"
				d="M0,35l38.58-6.61a3.69,3.69,0,0,1,4.19,3.27L52.88,100H0Z"
			/>
			<path id="topright" class="cls-1" d="M62,0l2.7,16.76A3.7,3.7,0,0,0,68.89,20L100,14.74V.07Z" />
			<path
				id="rightmid"
				class="cls-1"
				d="M45.22,31l5.13,34.68a3.69,3.69,0,0,0,4.19,3.27L100,61.15V17.61L48.27,26.48A3.92,3.92,0,0,0,45.22,31Z"
			/>
			<path
				id="bottomright"
				class="cls-1"
				d="M51.9,76.17,55.42,100H99.28L100,63.93,54.94,71.65A3.92,3.92,0,0,0,51.9,76.17Z"
			/>
		</g>
	</svg>
	<div id="instructions">
		<h1>cotswolds<br />digital.</h1>
		<h2>(press and hold)</h2>
	</div>
</div>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Spartan:wght@100;800&display=swap');

	:root {
		--color-grey: #979387;
		--color-light-grey: #d5d4cc;
		--color-dark-grey: #484641;
		--color-green: #245941;
		--color-light-green: #369c9b;
		--color-pink: #d28797;
	}

	h1 {
		white-space: pre-line;
		font-weight: 800;
		text-align: left;
		letter-spacing: -0.4rem;
		font-size: 4rem;
	}

	h2 {
		font-weight: 100;
		font-size: 0.8rem;
	}

	.wrapper {
		width: 100vw;
		height: 100vh;
		display: flex;
		align-items: center;
		justify-content: center;
		position: relative;
	}

	.wrapper,
	.wrapper * {
		user-select: none;
		cursor: default;
	}

	#instructions {
		text-align: center;
		position: absolute;
		left: 50%;
		top: 50%;
		transform: translate(-50%, -50%);
		font-family: 'Spartan', sans-serif;
		transition: opacity 2s;
	}

	svg {
		width: 100%;
		max-width: 6000px;
	}

	svg path {
		opacity: 0;
	}
</style>
