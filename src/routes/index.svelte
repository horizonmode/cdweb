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

		sectionIndex = nextSectionIndex;

		exitTimeline.play();
		playLogoAnimation();
	};

</script>


<div class="wrapper">

	<h1 id="company-name">cotswold<br />cloud.</h1>

	<svg
		id="logo2"
		xmlns="http://www.w3.org/2000/svg"
		viewBox="75 10 75 75"
		preserveAspectRatio="xMinYMin slice"
	>

<script type="text/JavaScript">

            <![CDATA[
					function setViewBox(zoomValues){ 
						var mySVG = document.getElementById('logo');
						mySVG.setAttribute("viewBox", zoomValues);  
					}
 			]]>
</script>

		<defs>
			<style>
			.cls-about {
					fill: black;
					stroke: black;
					stroke-width: 2;
				}

				.cls-about:hover {
					fill: #245941;
					stroke: #245941;
				}

				.cls-work {
					fill: black;
					stroke: black;
					stroke-width: 2;
					pointer-events: all;
				}

				.cls-work:hover {
					fill: #d28797;
					stroke: #d28797;
				}

				.cls-services {
					fill: black;
					stroke: black;
					stroke-width: 2;
					pointer-events: all;
				}

				.cls-services:hover {
					fill: #484641;
					stroke: #484641;
				}

				.cls-contact {
					fill: black;
					stroke: black;
					stroke-width: 2;
					pointer-events: all;
				}

				.cls-contact:hover {
					fill: #979387;
					stroke: #979387;
				}

				.cls-recog {
					stroke: black;
					stroke-width: 2;
					font-size: 4px;
					font-weight: 400;
					fill: black;
				}

				.cls-recog:hover {
					fill: #369c6b;
					stroke: #369c6b;
				}
				
			</style>
		</defs>


		<g id="container" data-name="Layer 2" transform="rotate(-15, 100, 50)">

			<g id="bottomleft" class={`menu-group ${activeSection.name === 'work' && 'active'}`}>
				<rect class="cls-about" y="34.7" width="98" height="65.33" rx="4.2" onClick="setViewBox('50 50 1 1')"></rect>
			</g>

			<g id="rightmid" class={`menu-group ${activeSection.name === 'whatwedo' && 'active'}`}>
				<rect class="cls-work" x="102" y="34.7" width="98" height="30.67" rx="4.2" onClick="setViewBox('190 40 1 1')" />
			</g>

			<g id="bottomright" class="menu-group">
				<rect class="cls-services" x="102" y="69.3" width="98" height="30.67" rx="4.2" onClick="setViewBox('180 80 1 1')"/>
			</g>

			<g id="topleft" class={`menu-group ${activeSection.name === 'aboutus' && 'active'}`}>
				<rect class="cls-contact" width="115.8" height="30.67" rx="4.2" onClick="setViewBox('100 1 1 1')"/>
			</g>

			<g id="topright" class="menu-group">
			<rect class="cls-recog" x="119.3" width="80.4" height="30.67" rx="4.2" onClick="setViewBox('180 1 1 1')"/>
				</g>
		</g>
	</svg>

	<svg
		id="logo"
		xmlns="http://www.w3.org/2000/svg"
		viewBox="75 10 75 75"
		preserveAspectRatio="xMinYMin meet"
	>

<script type="text/JavaScript">

            <![CDATA[
					function setViewBox(zoomValues){ 
						var mySVG = document.getElementById('logo');
						mySVG.setAttribute("viewBox", zoomValues);  
					}
 			]]>
</script>

		<defs>
			<style>
			.cls-about {
					fill: black;
					stroke: black;
					stroke-width: 2;
				}

				.cls-about:hover {
					fill: #245941;
					stroke: #245941;
				}

				.cls-work {
					fill: black;
					stroke: black;
					stroke-width: 2;
					pointer-events: all;
				}

				.cls-work:hover {
					fill: #d28797;
					stroke: #d28797;
				}

				.cls-services {
					fill: black;
					stroke: black;
					stroke-width: 2;
					pointer-events: all;
				}

				.cls-services:hover {
					fill: #484641;
					stroke: #484641;
				}

				.cls-contact {
					fill: black;
					stroke: black;
					stroke-width: 2;
					pointer-events: all;
				}

				.cls-contact:hover {
					fill: #979387;
					stroke: #979387;
				}

				.cls-recog {
					stroke: black;
					stroke-width: 2;
					font-size: 4px;
					font-weight: 400;
					fill: black;
				}

				.cls-recog:hover {
					fill: #369c6b;
					stroke: #369c6b;
				}
				
			</style>
		</defs>


		<g id="container" data-name="Layer 2" transform="rotate(-15, 100, 50)">

			<g id="bottomleft" class={`menu-group ${activeSection.name === 'work' && 'active'}`}>
				<rect class="cls-about" y="34.7" width="98" height="65.33" rx="4.2" onClick="setViewBox('50 50 1 1')"></rect>
				<text x="84" y="40" font-size="4" fill="white">work</text>
			
			</g>

			<g id="rightmid" class={`menu-group ${activeSection.name === 'whatwedo' && 'active'}`}>
				<rect class="cls-work" x="102" y="34.7" width="98" height="30.67" rx="4.2" onClick="setViewBox('190 40 1 1')"></rect>
				<text x="105" y="40" font-size="4" fill="white">services</text>
			</g>

			<g id="bottomright" class="menu-group">
				<rect class="cls-services" x="102" y="69.3" width="98" height="30.67" rx="4.2" onClick="setViewBox('180 80 1 1')"></rect>
				<text x="105" y="75" font-size="4" fill="white">recognition</text>
			</g>

			<g id="topleft" class={`menu-group ${activeSection.name === 'aboutus' && 'active'}`}>
				<rect class="cls-contact" width="115.8" height="30.67" rx="4.2" onClick="setViewBox('100 1 1 1')"></rect>
				<text x="99" y="29" font-size="4" fill="white">about</text>
			</g>

			<g id="topright" class="menu-group">
			<rect class="cls-recog" x="119.3" width="80.4" height="30.67" rx="4.2" onClick="setViewBox('180 1 1 1')"></rect>
			<text x="122" y="29" font-size="4" fill="white">contact</text>
				</g>
		</g>
	</svg>
	

</div>


<style>
	@import url('https://fonts.googleapis.com/css2?family=Spartan:wght@100;400;500;600;700;800;900&display=swap');

	#bottomleft text {display: none;}
	#bottomleft:hover text {display: block;}

	#rightmid text {display: none;}
	#rightmid:hover text {display: block;}

	#bottomright text {display: none;}
	#bottomright:hover text {display: block;}

	#topleft text {display: none;}
	#topleft:hover text {display: block;}

	#topright text {display: none;}
	#topright:hover text {display: block;}

	:root {
		--color-grey: #979387;
		--color-light-grey: #d5d4cc;
		--color-dark-grey: #484641;
		--color-green: #245941;
		--color-light-green: #369c9b;
		--color-pink: #d28797;
	
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
		display: flex;
		justify-content: center; 

	}

	.wrapper #company-name {
		position: fixed;
		bottom: 1rem;
		right: 1rem;
		z-index: 10;
		line-height: 4rem;
		background-color: white;
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
		width: auto;
	}

	svg#logo2 {
		height: 100px;
		width: 100px;
		margin-top:50px;
		margin-left:50px;
		position: absolute;
		left: 0px;
	}

	



	svg * {
		transition: fill 0.5s ease-in-out, stroke 0.5s ease-in-out;
	}
</style>
