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

	const exitAnim = [{ transform: 'translateX(-100%)' }];

	const exitAnimTiming = {
		easing: 'ease-out',
		duration: 1000,
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
			//topLeftObject.addEventListener('mousedown touchstart', () => expandItem(topLeftObject));
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

		const exitTimeline = gsap.timeline({ repeat: 0 });
		exitTimeline.add('start');
		exitTimeline.to(
			'.stack1',
			{ transform: 'translateX(-80%) rotate(349deg)', duration: 0.5, ease: 'power2.out' },
			'start'
		);
		exitTimeline.to(
			'.stack2',
			{ transform: 'translate3D(0,0,0)', top: 0, left: 0, duration: 0.5 },
			'start'
		);
		exitTimeline.play();

		document.documentElement.style.setProperty('--current-theme-main', 'var(--color-green)');
		document.getElementById('rightmid').classList.remove('active');

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
	<h1 id="company-name">cotswold<br />cloud.</h1>
	<svg xmlns="http://www.w3.org/2000/svg" viewBox="70 10 75 75" preserveAspectRatio="xMinYMid meet">
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
			<g id="rightmid" class="menu-group active">
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
	<div class="content pink stack1" id="instructions">
		<div class="page-title"><h1>What we do.</h1></div>
		<div class="content-box">
			<h1>web design / ux / development.</h1>
		</div>
	</div>
	<div class="content green stack2" id="instructions">
		<div class="page-title"><h1>About Us.</h1></div>
		<div class="content-box">
			<p>
				Cotswolds Digital is a creative digital agency founded by Seb and Andrew – friends, who met
				as classmates during their MSc studies at Imperial College London in 2009. With more than 30
				years of combined web development and digital experience, the pair have led and delivered
				exciting projects for well-known organisations and brands all around the world. Now living
				at opposite ends of the green and hilly Cotswolds, Seb and Andrew created Cotswolds Digital
				to provide the same level of exceptional service they’ve become known for in their
				professional careers, for local organisations. Our drive and competitiveness comes from our
				love of web design, coupled with the buzz we get from making a real and lasting impact for
				our clients. We’re nerds at heart, but sociable too. Why not drop us a line to see how we
				could help you and your business?
			</p>
		</div>
	</div>
	<div class="content grey stack3" id="instructions">
		<div class="page-title"><h1>Work.</h1></div>
		<div class="content-box">
			<p>Our Work</p>
		</div>
	</div>
</div>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Spartan:wght@100;400;500;600;700;800;900&display=swap');

	:root {
		--color-grey: #979387;
		--color-light-grey: #d5d4cc;
		--color-dark-grey: #484641;
		--color-green: #245941;
		--color-light-green: #369c9b;
		--color-pink: #d28797;
		--current-theme-main: var(--color-pink);
		--current-theme-offset: var(--color-white);
	}

	.green {
		color: var(--color-green);
	}

	.grey {
		color: var(--color-light-grey);
	}

	:global(body) {
		font-family: 'Spartan', sans-serif;
	}

	@media only screen and (max-width: 600px) {
		:root {
			font-size: 12px;
		}
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

	.wrapper #company-name {
		position: fixed;
		top: 1rem;
		left: 1rem;
		z-index: 10;
		line-height: 4rem;
	}

	.wrapper,
	.wrapper * {
		user-select: none;
		cursor: default;
		overflow: hidden;
	}

	.content {
		width: 100vw;
		height: 100vh;
		display: flex;
		align-items: center;
		justify-content: center;
		position: relative;
		padding: 0;

		filter: drop-shadow(1px 1px 4px rgba(0, 0, 0, 0.75));
	}

	.content.stack1 {
		z-index: 3;
	}

	.content.stack2 {
		z-index: 2;
		position: relative;
		left: 5px;
		top: 10px;
		transform: rotate(2deg);
	}

	.content.stack3 {
		z-index: 1;
		position: relative;
		left: 8px;
		top: 12.5px;
		transform: rotate(5deg);
	}

	.content.pink::before {
		background-color: var(--color-pink);
	}

	.content.green::before {
		background-color: var(--color-green);
	}

	.content.grey::before {
		background-color: var(--color-light-grey);
	}

	.content::before {
		content: '';
		width: 100%;
		height: 100%;
		border-radius: 0 0 20px 0;
		position: absolute;
		top: 0;
		right: 0;
		/* transform-origin: bottom left;
		transform: rotateZ(-5deg); */
		-webkit-mask: url('/mask.svg');
		mask: url('/mask.svg');
		-webkit-mask-repeat: no-repeat;
		-webkit-mask-size: 100% 100%;
		mask-size: 100% 100%;
	}

	.content-box {
		text-align: center;
		position: absolute;
		left: 50%;
		top: 50%;
		transform: translate(-50%, -50%);
		font-family: 'Spartan', sans-serif;
		transition: opacity 2s;
		color: white;
	}

	#instructions {
		text-align: center;
		position: absolute;
		font-family: 'Spartan', sans-serif;
		transition: opacity 2s;
		color: var(--current-theme-offset);
	}

	.page-title {
		position: absolute;
		right: 12rem;
		top: 1rem;
		font-weight: 800;
		font-size: 2rem;
		color: white;
		text-decoration: underline;
	}

	svg {
		height: 10rem;
		width: auto;
		position: fixed;
		bottom: 1rem;
		left: 1rem;
		z-index: 10;
	}

	svg .menu-group rect {
		stroke: white;
		fill: white;
	}

	svg .menu-group.active#rightmid rect {
		fill: var(--color-pink);
	}

	svg .menu-group.active#topleft rect {
		fill: var(--color-green);
	}

	svg * {
		transition: fill 0.5s ease-in-out, stroke 0.5s ease-in-out;
	}
	svg .menu-group {
		/* opacity: 0; */
	}
</style>
