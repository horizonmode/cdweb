<script>
	import gsap from 'gsap';

	const sections = [
		{ name: 'whatwedo', color: 'var(--color-pink)' },
		{ name: 'aboutus', color: 'var(--color-green)' },
		{ name: 'work', color: 'var(--color-light-grey)' }
	];
	let sectionIndex = 0;
	$: activeSection = sections[sectionIndex] || { name: '', color: '' };

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

	const handleChange = (e, index) => {
		e.preventDefault();
		const reverse = index < sectionIndex;
		console.log(reverse);
		const nextSectionIndex = reverse ? sectionIndex - 1 : sectionIndex + 1;

		console.log(sectionIndex, nextSectionIndex);

		const nextSection = sections[nextSectionIndex];
		console.log(nextSection);

		const exitTimeline = gsap.timeline({ repeat: 0 });
		exitTimeline.add('start');

		if (!reverse) {
			exitTimeline.to(
				`#${activeSection.name}`,
				{ transform: 'translateX(-80%) rotate(349deg)', duration: 0.5, ease: 'power2.out' },
				'start'
			);
		}

		if (nextSection) {
			exitTimeline.to(
				`#${nextSection.name}`,
				{ transform: 'translateX(0) rotate(0)', top: 0, left: 0, duration: reverse ? 0.5 : 0 },
				'start'
			);
			document.documentElement.style.setProperty('--current-theme-main', nextSection.color);
		}

		sectionIndex = nextSectionIndex;

		exitTimeline.play();

		playLogoAnimation();
	};
</script>

<div class="wrapper">
	<h1 id="company-name">cotswold<br />cloud.</h1>
	<svg
		id="logo"
		xmlns="http://www.w3.org/2000/svg"
		viewBox="-5 -5 30 30"
		preserveAspectRatio="xMinYMin slice"
	>
		<defs>
			<style>
				.cls-1 {
					fill: black;
					stroke: black;
					stroke-width: 2;
				}

				.cls-2 {
					stroke: none;
					font-size: 4px;
					font-weight: 400;
					fill: none;
				}
				.active rect {
					fill: var(--current-theme-main);
				}
				.active text {
					stroke: none;
					fill: black;
				}
			</style>
		</defs>
		<g id="container" data-name="Layer 2" transform="rotate(0, 100, 50)">
			<g id="bottomleft" class={`menu-group ${activeSection.name === 'work' && 'active'}`}>
				<rect class="cls-1" y="34.7" width="98" height="65.33" rx="4.2" />
			</g>
			<g id="rightmid" class={`menu-group ${activeSection.name === 'whatwedo' && 'active'}`}>
				<rect class="cls-1" x="102" y="34.7" width="98" height="30.67" rx="4.2" />
			</g>
			<g id="bottomright" class="menu-group">
				<rect class="cls-1" x="102" y="69.3" width="98" height="30.67" rx="4.2" /></g
			>
			<g id="topleft" class={`menu-group ${activeSection.name === 'aboutus' && 'active'}`}>
				<rect class="cls-1" width="115.8" height="30.67" rx="4.2" />
			</g>
			<g id="topright" class="menu-group"
				><rect class="cls-1" x="119.3" width="80.4" height="30.67" rx="4.2" /></g
			>
		</g>
	</svg>
	<!-- <div
		class="content pink"
		id="whatwedo"
		style="--n: 0"
		on:mousedown={(e) => handleChange(e, 0)}
		on:touchstart={(e) => handleChange(e, 0)}
	>
		<div class="page-title"><h1>What we do.</h1></div>
		<div class="content-box">
			<h1>web design / ux / development.</h1>
		</div>
	</div> -->
	<div
		class="content green stack"
		id="aboutus"
		style="--n: 1"
		on:mousedown={(e) => handleChange(e, 1)}
		on:touchstart={(e) => handleChange(e, 1)}
	>
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
	<!-- <div
		class="content grey stack"
		id="work"
		style="--n: 2"
		on:mousedown={(e) => handleChange(e, 2)}
		on:touchstart={(e) => handleChange(e, 2)}
	>
		<div class="page-title"><h1>Work.</h1></div>
		<div class="content-box">
			<p>Our Work</p>
		</div>
	</div>  -->
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

	:global(body) {
		font-family: 'Spartan', sans-serif;
		overflow: hidden;
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

	.wrapper {
		width: 100vw;
		height: 100vh;
	}

	.wrapper #company-name {
		position: fixed;
		bottom: 1rem;
		left: 1rem;
		z-index: 10;
		line-height: 4rem;
		background-color: black;
		color: white;
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

	/* .content.stack::before {
		/* left: calc(3px + var(--n) * 2px);
		top: calc(8px + var(--n) * 2px);
		transform: rotate(calc(var(--n) * 2.5deg));
		left: 8px;
		transform: scaleY(calc(1 + var(--n) * 0.05)) rotate(calc(var(--n) * 1deg));
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
		height: 110%;
		border-radius: 0 0 20px 0;
		position: absolute;
		bottom: 0;
		right: 0;
		/* transform-origin: bottom left;
		transform: rotateZ(-5deg); 
		-webkit-mask: url('/mask.svg');
		mask: url('/mask.svg');
		-webkit-mask-repeat: no-repeat;
		-webkit-mask-size: 100% 100%;
		mask-size: 100% 100%;
		outline: black 2px solid;
	} */

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
		width: 100%;
	}

	svg * {
		transition: fill 0.5s ease-in-out, stroke 0.5s ease-in-out;
	}
</style>
