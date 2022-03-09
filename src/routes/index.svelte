<script>
	import gsap from 'gsap';

	let introAnimationComplete = false;
	let zoomed = false;
	let zoomTimeline;

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

	const expandItem = (item) => {
		const expandItemAnim = [
			{ transform: 'translate3D(50%, 0%, 0)' },
			{ opacity: 0.9 },
			{ transform: 'translate3D(0,0,0)', opacity: 1 }
		];

		const expandTiming = {
			easing: 'ease-out',
			duration: 2000,
			iterations: 1,
			fill: 'both'
		};

		item.animate(expandItemAnim, expandTiming);
	};

	let animations = [];

	const play = () => {
		animations = [];

		const topLeftObject = document.getElementById('topleft');
		const topLeftAnim = topLeftObject.animate(wallBuildTopLeft, wallBuildTiming);

		topLeftAnim.onfinish = () => {
			introAnimationComplete = true;
			topLeftObject.classList.add('active');
			topLeftObject.addEventListener('mousedown touchstart', () => expandItem(topLeftObject));
		};

		animations.push(topLeftAnim);

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
		if (introAnimationComplete) return;

		document.getElementById('instructions').style.opacity = '0';

		play();
	};

	const handleZoom = (width, height, x, y) => {
		if (zoomed) {
			console.log(zoomTimeline);
			zoomTimeline.reverse();
			zoomed = false;
			return;
		}

		zoomed = true;
		zoomTimeline = gsap.timeline({ repeat: 0 });
		zoomTimeline.add('start');
		zoomTimeline.to('#wall', { attr: { viewBox: `${x} ${y} ${width} ${height}` } }, 'start');
		zoomTimeline.to('#container', { transform: 'rotate(0,100,50)' }, 'start');
		zoomTimeline.play();
	};
</script>

<div class="wrapper" on:mousedown={handleStart} on:touchstart={handleStart}>
	<svg id="wall" xmlns="http://www.w3.org/2000/svg" viewBox="70 10 75 75">
		<defs>
			<style>
				.cls-1 {
					fill: black;
					stroke: black;
					stroke-width: 2;
				}

				.cls-1 {
					stroke: #1d1d1b;
				}

				.cls-2 {
					stroke: none;
					font-size: 4px;
					font-weight: 400;
					fill: none;
				}
				.active rect {
					stroke: var(--color-green);
					fill: var(--color-green);
				}
				.active text {
					stroke: none;
					fill: black;
				}
			</style>
		</defs>
		<g id="container" data-name="Layer 2" transform="rotate(-15, 100, 50)">
			<g id="bottomleft" class="menu-group">
				<rect class="cls-1" y="34.7" width="98" height="65.33" rx="4.2" />
			</g>
			<g id="rightmid" class="menu-group">
				<rect class="cls-1" x="102" y="34.7" width="98" height="30.67" rx="4.2" />
			</g>
			<g id="bottomright" class="menu-group">
				<rect class="cls-1" x="102" y="69.3" width="98" height="30.67" rx="4.2" /></g
			>
			<g
				id="topleft"
				class="menu-group"
				on:click={() => handleZoom(20, 20, -5, -5)}
				on:touchstart={() => handleZoom(20, 20, -5, -5)}
			>
				<rect class="cls-1" width="115.8" height="30.67" rx="4.2" />
				<text class="cls-2" transform="translate(92 28)">About Us</text>
			</g>
			<g id="topright" class="menu-group"
				><rect class="cls-1" x="119.3" width="80.4" height="30.67" rx="4.2" /></g
			>
		</g>
	</svg>
	<div id="instructions">
		<h1>cotswolds<br />cloud.</h1>
	</div>
</div>

<style>
	@import url('../reset.css');
	@import url('https://fonts.googleapis.com/css2?family=Spartan:wght@100;400;500;600;700;800;900&display=swap');

	:root {
		--color-grey: #979387;
		--color-light-grey: #d5d4cc;
		--color-dark-grey: #484641;
		--color-green: #245941;
		--color-light-green: #369c9b;
		--color-pink: #d28797;
	}

	:global(body) {
		font-family: 'Spartan', sans-serif;
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
		padding: 0;
	}

	@media screen and (min-width: 600px) {
		.wrapper {
			padding: 3rem;
		}
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
		height: 100%;
		width: auto;
	}

	svg * {
		transition: fill 0.5s ease-in-out, stroke 0.5s ease-in-out;
	}
	svg .menu-group {
		opacity: 0;
	}
</style>
