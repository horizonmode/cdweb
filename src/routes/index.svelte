<script>
	import gsap from 'gsap';
	import { onMount } from 'svelte';

	const sections = [
		{ name: 'about', color: 'var(--color-light-grey)' },
		{ name: 'contact', color: 'var(--color-light-green)' },
		{ name: 'work', color: 'var(--color-green)' },
		{ name: 'services', color: 'var(--color-pink)' },
		{ name: 'recognition', color: 'var(--color-grey)' }
	];

	let sectionIndex = -1;
	$: activeSection = sections[sectionIndex] || { name: '', color: '' };
	let zoomed = false;

	let mostRecentZoom;

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

	const playLogoAnimation = () => {
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

	const setViewBox = (e, zoomValues) => {
		e.preventDefault();
		// create timeline

		if (zoomed) {
			// zoom out
			zoomed = false;
			mostRecentZoom.reverse();
		} else {
			// zoom in
			zoomed = true;
			const tl = gsap.timeline({ repeat: 0 });
			tl.add('start');
			tl.to('#logo', { attr: { viewBox: zoomValues }, duration: 1 }, 'start');
			tl.to('#container', { transform: 'rotate(0,100,50)', duration: 1 }, 'start');
			tl.play();
			mostRecentZoom = tl;
		}
	};

	const setActiveSection = (sectionName) => {
		console.log(sectionName);
		const index = sections.findIndex((s) => s.name === sectionName);
		sectionIndex = index;
		document.documentElement.style.setProperty('--current-theme', sections[sectionIndex].color);
	};

	// when page loads
	onMount(async () => {
		playLogoAnimation();
	});
</script>

<div class="wrapper">
	<h1 id="company-name">cotswold<br />cloud.</h1>

	<svg
		id="logo2"
		xmlns="http://www.w3.org/2000/svg"
		viewBox="75 10 75 75"
		preserveAspectRatio="xMidYMid meet"
	>
		<defs>
			<style>
				.brick {
					fill: black;
					stroke: black;
					stroke-width: 2;
				}

				.active .brick {
					fill: var(--current-theme);
					stroke: var(--current-theme);
					pointer-events: all;
				}
			</style>
		</defs>

		<g data-name="Layer 2" transform="rotate(-15, 100, 50)">
			<g class={`menu-group ${activeSection.name === 'work' && 'active'}`}>
				<rect class="brick" y="34.7" width="98" height="65.33" rx="4.2" />
			</g>

			<g class={`menu-group ${activeSection.name === 'whatwedo' && 'active'}`}>
				<rect class="brick" x="102" y="34.7" width="98" height="30.67" rx="4.2" />
			</g>

			<g class="menu-group">
				<rect class="brick" x="102" y="69.3" width="98" height="30.67" rx="4.2" />
			</g>

			<g class={`menu-group ${activeSection.name === 'aboutus' && 'active'}`}>
				<rect class="brick" width="115.8" height="30.67" rx="4.2" />
			</g>

			<g class="menu-group">
				<rect class="brick" x="119.3" width="80.4" height="30.67" rx="4.2" />
			</g>
		</g>
	</svg>

	<svg
		id="logo"
		xmlns="http://www.w3.org/2000/svg"
		viewBox="75 10 75 75"
		preserveAspectRatio="xMidYMid meet"
	>
		<defs>
			<style>
				.brick {
					fill: black;
					stroke: black;
					stroke-width: 2;
				}

				text {
					display: none;
					pointer-events: none;
				}

				.active .brick {
					fill: var(--current-theme);
					stroke: var(--current-theme);
				}

				.active text {
					display: block;
				}
			</style>
		</defs>

		<g id="container" data-name="Layer 2" transform="rotate(-15, 100, 50)">
			<g id="bottomleft" class={`menu-group ${activeSection.name === 'work' && 'active'}`}>
				<rect
					class="brick"
					y="34.7"
					width="98"
					height="65.33"
					rx="4.2"
					on:mousedown={(e) => setViewBox(e, '50,50,1,1')}
					on:touchstart={(e) => setViewBox(e, '50,50,1,1')}
					on:mouseover={() => setActiveSection('work')}
					on:focus={() => setActiveSection('work')}
				/>
				<text x="84" y="40" font-size="4" fill="white">work</text>
			</g>

			<g id="rightmid" class={`menu-group ${activeSection.name === 'services' && 'active'}`}>
				<rect
					class="brick"
					x="102"
					y="34.7"
					width="98"
					height="30.67"
					rx="4.2"
					on:mousedown={(e) => setViewBox(e, '190 40 1 1')}
					on:touchstart={(e) => setViewBox(e, '190 40 1 1')}
					on:mouseover={() => setActiveSection('services')}
					on:focus={() => setActiveSection('services')}
				/>
				<text x="105" y="40" font-size="4" fill="white">services</text>
			</g>

			<g id="bottomright" class={`menu-group ${activeSection.name === 'recognition' && 'active'}`}>
				<rect
					class="brick"
					x="102"
					y="69.3"
					width="98"
					height="30.67"
					rx="4.2"
					on:mousedown={(e) => setViewBox(e, '180 80 1 1')}
					on:touchstart={(e) => setViewBox(e, '180 80 1 1')}
					on:mouseover={() => setActiveSection('recognition')}
					on:focus={() => setActiveSection('recognition')}
				/>
				<text x="105" y="75" font-size="4" fill="white">recognition</text>
			</g>

			<g id="topleft" class={`menu-group ${activeSection.name === 'about' && 'active'}`}>
				<rect
					class="brick"
					width="115.8"
					height="30.67"
					rx="4.2"
					on:mousedown={(e) => setViewBox(e, '100 1 1 1')}
					on:touchstart={(e) => setViewBox(e, '100 1 1 1')}
					on:mouseover={() => setActiveSection('about')}
					on:focus={() => setActiveSection('about')}
				/>
				<text x="99" y="29" font-size="4" fill="white">about</text>
			</g>

			<g id="topright" class={`menu-group ${activeSection.name === 'contact' && 'active'}`}>
				<rect
					class="brick"
					x="119.3"
					width="80.4"
					height="30.67"
					rx="4.2"
					on:mousedown={(e) => setViewBox(e, '180 1 1 1')}
					on:touchstart={(e) => setViewBox(e, '180 1 1 1')}
					on:mouseover={() => setActiveSection('contact')}
					on:focus={() => setActiveSection('contact')}
				/>
				<text x="122" y="29" font-size="4" fill="white">contact</text>
			</g>
		</g>
	</svg>
</div>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Spartan:wght@100;400;500;600;700;800;900&display=swap');

	:root {
		--color-grey: #979387;
		--color-light-grey: #d5d4cc;
		--color-dark-grey: #484641;
		--color-green: #245941;
		--color-light-green: #369c6b;
		--color-pink: #d28797;

		--current-theme: var(--color-grey);
		--current-theme-offset: var(--color-white);
	}

	:global(body) {
		font-family: 'Spartan', sans-serif;
		overflow: hidden;
	}

	h1 {
		white-space: pre-line;
		font-weight: 800;
		text-align: left;
		letter-spacing: -0.4rem;
		font-size: 4rem;
	}

	.wrapper {
		width: 100vw;
		height: 100vh;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.wrapper #company-name {
		position: fixed;
		bottom: 1rem;
		right: 1rem;
		z-index: 10;
		line-height: 4rem;
		color: black;
		border-radius: 5px;
	}

	.wrapper,
	.wrapper * {
		user-select: none;
		cursor: default;
		overflow: hidden;
	}

	.content {
		width: 100%;
		height: 100%;
		position: absolute;
		filter: drop-shadow(1px 1px 4px rgba(0, 0, 0, 0.75));
		z-index: calc(3 - var(--n));
		top: 0;
		left: 0;
	}

	.content-box {
		text-align: center;
		position: absolute;
		left: 50%;
		top: 50%;
		transform: translate(-50%, -50%);
		font-family: 'Spartan', sans-serif;
		transition: opacity 1s;
		color: white;
	}

	.page-title {
		display: none;
	}

	@media only screen and (min-width: 600px) {
		.page-title {
			position: absolute;
			right: 12rem;
			top: 1rem;
			color: white;
			text-decoration: underline;
			display: block;
		}
	}

	svg#logo {
		height: 100%;
		width: auto;
	}

	@media only screen and (max-width: 600px) {
		svg#logo {
			height: 50%;
			width: auto;
		}
	}

	svg#logo2 {
		height: 100px;
		width: 100px;
		top: 1rem;
		left: 1rem;
		position: absolute;
	}

	@media only screen and (max-width: 600px) {
		svg#logo {
			margin-top: 170px;
			height: 100%;
			width: auto;
			transform: scale(1.4);
		}
		svg#logo2 {
			display: none;
		}

		h1 {
			transform: scale(0.7);
			text-align: right;
			right: -1rem !important;
		}
	}

	@media only screen and (max-width: 376px) {
		svg#logo {
			margin-top: 40px;
			height: 100%;
			width: auto;
			transform: scale(1.2);
		}
		svg#logo2 {
			display: none;
		}

		h1 {
			transform: scale(0.7);
			text-align: right;
			right: -1rem !important;
		}
	}

	@media only screen and (max-width: 361px) {
		svg#logo {
			margin-top: 140px;
			height: 100%;
			width: auto;
			transform: scale(1.4);
		}
		svg#logo2 {
			display: none;
		}

		h1 {
			transform: scale(0.7);
			text-align: right;
			right: -1rem !important;
		}
	}

	svg * {
		transition: fill 0.2s ease-in-out, stroke 0.2s ease-in-out;
	}
</style>
