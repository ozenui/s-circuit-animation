<script>
	const CIRCUIT_WIDTH = 1100;
	const CIRCUIT_HEIGHT = 113;
	const PROGRESS_WIDTH = 64;

	let leftGradientX = $state(CIRCUIT_WIDTH / 2 - PROGRESS_WIDTH);
	let rightGradientX = $state(CIRCUIT_WIDTH / 2);
	let isAnimating = $state(false);
	let animationInterval = 0;

	function resetAnimation() {
		leftGradientX = CIRCUIT_WIDTH / 2 - PROGRESS_WIDTH;
		rightGradientX = CIRCUIT_WIDTH / 2;
		isAnimating = false;
	}

	function animateProgress() {
		isAnimating = true;
		leftGradientX = 0 - PROGRESS_WIDTH;
		rightGradientX = CIRCUIT_WIDTH + PROGRESS_WIDTH;

		if (animationInterval) {
			clearInterval(animationInterval);
		}

		animationInterval = setInterval(() => {
			if (leftGradientX <= -PROGRESS_WIDTH && rightGradientX >= CIRCUIT_WIDTH) {
				resetAnimation();
				setTimeout(animateProgress, 100);
			}
		}, 4000);
	}

	$effect(() => {
		setTimeout(animateProgress, 100);
		return () => {
			if (animationInterval) {
				clearInterval(animationInterval);
			}
		};
	});
</script>

<main class="relative h-[112px]">
	<svg
		width={CIRCUIT_WIDTH}
		height={CIRCUIT_HEIGHT}
		viewBox={`0 0 ${CIRCUIT_WIDTH} ${CIRCUIT_HEIGHT}`}
		fill="none"
		xmlns="http://www.w3.org/2000/svg"
	>
		<!-- Mask Definition -->
		<defs>
			<mask id="circuit-mask">
				<path
					d="M1100 1H926L780 73H634V72C634 64.268 627.732 58 620 58H599H578C570.268 58 564 64.268 564 72V85M1100 13H931L785 85H564M1100 25H940L790 97H634V98C634 105.732 627.732 112 620 112H599H578C570.268 112 564 105.732 564 98V85M0 1H170L320 73H466V72C466 64.268 472.268 58 480 58H501H522C529.732 58 536 64.268 536 72V85M0 13H165L315 85H564M0 25H160L310 97H466V98C466 105.732 472.268 112 480 112H501H522C529.732 112 536 105.732 536 98V85M564 85H536"
					stroke="white"
					stroke-width="2"
				/>
			</mask>
		</defs>

		<!-- Gradient Definitions -->
		<defs>
			<linearGradient
				id="leftGradient"
				gradientUnits="userSpaceOnUse"
				x1={leftGradientX}
				y1="0"
				x2={leftGradientX + PROGRESS_WIDTH}
				y2="0"
			>
				<stop offset="0%" stop-color="#F8F9F8" />
				<stop offset="100%" stop-color="#00E92F" />
			</linearGradient>

			<linearGradient
				id="rightGradient"
				gradientUnits="userSpaceOnUse"
				x1={rightGradientX}
				y1="0"
				x2={rightGradientX + PROGRESS_WIDTH}
				y2="0"
			>
				<stop offset="0%" stop-color="#00E92F" />
				<stop offset="100%" stop-color="#F8F9F8" />
			</linearGradient>
		</defs>

		<!-- Background circuit path -->
		<path
			d="M1100 1H926L780 73H634V72C634 64.268 627.732 58 620 58H599H578C570.268 58 564 64.268 564 72V85M1100 13H931L785 85H564M1100 25H940L790 97H634V98C634 105.732 627.732 112 620 112H599H578C570.268 112 564 105.732 564 98V85M0 1H170L320 73H466V72C466 64.268 472.268 58 480 58H501H522C529.732 58 536 64.268 536 72V85M0 13H165L315 85H564M0 25H160L310 97H466V98C466 105.732 472.268 112 480 112H501H522C529.732 112 536 105.732 536 98V85M564 85H536"
			stroke="#064613"
			stroke-opacity="0.04"
			stroke-width="2"
		/>

		<!-- Progress gradients with mask -->
		<g mask="url(#circuit-mask)">
			<!-- Left progress -->
			<rect
				class={isAnimating
					? `opacity-100 transition-all duration-[2000ms] ease-linear`
					: 'opacity-20'}
				x={leftGradientX}
				y="0"
				width={PROGRESS_WIDTH}
				height={CIRCUIT_HEIGHT}
				fill="url(#leftGradient)"
			/>
			<!-- Right progress -->
			<rect
				class={isAnimating
					? `opacity-100 transition-all duration-[2000ms] ease-linear`
					: 'opacity-20'}
				x={rightGradientX}
				y="0"
				width={PROGRESS_WIDTH}
				height={CIRCUIT_HEIGHT}
				fill="url(#rightGradient)"
			/>
		</g>
	</svg>
</main>
