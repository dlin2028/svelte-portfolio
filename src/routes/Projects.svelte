<script>
	import { fade } from 'svelte/transition';
	import { fly } from 'svelte/transition';
	import { elasticOut } from 'svelte/easing';

	function typewriter(node, { speed = 1 }) {
		const valid = node.childNodes.length === 1 && node.childNodes[0].nodeType === Node.TEXT_NODE;

		if (!valid) {
			throw new Error(`This transition only works on elements with a single text node child`);
		}

		const text = node.textContent;
		const duration = text.length / (speed * 0.01);

		return {
			duration,
			tick: (t) => {
				const i = Math.trunc(text.length * t);
				node.textContent = text.slice(0, i);
			}
		};
	}

	function project(node, { duration }) {
		return {
			duration,
			css: (t) => {
				const eased = t;

				return `
                    height: ${eased * 100 < 50 ? 5 : (eased - 50) * 2}%;
                    width: ${eased * 200 > 100 ? 100 : eased * 200}%;
                    `;
			}
		};
	}

	let transmissionVisible = false;
	let cardVisible = false;
	let textVisible = false;

	function actionWhenInViewport(e) {
		const observer = new IntersectionObserver((entries) => {
			if (entries[0].isIntersecting) {
				transmissionVisible = true;
				setTimeout(() => {
					transmissionVisible = false;
					cardVisible = true;
					setTimeout(() => {
						textVisible = true;
					}, 1500);
				}, 1500);
			} else {
				transmissionVisible = false;
				cardVisible = false;
				textVisible = false;
			}
		});

		observer.observe(e);
	}
</script>

<div class="w-full bg-[url('/background-large.jpg')] h-full flex items-center">
	<div class="w-full bg-[url('/glow.png')] h-full flex items-center">
		{#if transmissionVisible}
			<div class="w-full text-center text-5xl text-cyan-400" in:typewriter={{speed:3}}>
				INCOMING TRANSMISSION...
			</div>
		{/if}

		{#if cardVisible}
			<div class="w-full h-screen p-6 items-center justify-center flex">
				<div
					class="relative flex h-full w-full items-center bg-cyan-500/20"
					in:project={{ duration: 1500 }}
				>
					{#if textVisible}
						<div class="flex-col w-full p-6 h-full">
							<div
								class="w-full text-center font-bold text-5xl text-white"
								in:typewriter={{ speed: 3.5 }}
							>
								My Projects
							</div>

                            <div class="border-cyan-500 border bg-gray-400 w-full h-20 text-lg">
                                <img class="h-full object-contain" src="/ece-logo.jpg" alt="ece logo" />
                                <div>B.S. In Computer Engineering</div>
                            </div>

							<div class="xs:flex-col sm:flex sm:h-3/4 relative align-middle">
								<div class="basis-1/3 px-4 relative bg-black text-white">
									<img class="h-full object-contain" src="/elc-logo.jpg" alt="elc logo" />
									<div
										class="border-cyan-500 border-l-2 border-t-2 absolute left-1 top-1 h-4 w-4"
									/>
									<div
										class="border-cyan-500 border-t-2 border-r-2 absolute top-1 right-1 h-4 w-4"
									/>
									<div
										class="border-cyan-500 border-b-2 border-l-2 absolute bottom-1 left-1 h-4 w-4"
									/>
									<div
										class="border-cyan-500 border-b-2 border-r-2 absolute bottom-1 right-1 h-4 w-4"
									/>
								</div>
								<div class="relative basis-1/3 px-4 bg-white text-white">
									<img class="h-full object-contain" src="/oppo-logo.png" alt="oppo logo" />
									<div
										class="border-cyan-500 border-l-2 border-t-2 absolute left-1 top-1 h-4 w-4"
									/>
									<div
										class="border-cyan-500 border-t-2 border-r-2 absolute top-1 right-1 h-4 w-4"
									/>
									<div
										class="border-cyan-500 border-b-2 border-l-2 absolute bottom-1 left-1 h-4 w-4"
									/>
									<div
										class="border-cyan-500 border-b-2 border-r-2 absolute bottom-1 right-1 h-4 w-4"
									/>
								</div>
								<div class="basis-1/3 relative bg-black text-white">
									<img class="h-full object-contain" src="/pap-logo.png" alt="pap logo" />
									<div
										class="border-cyan-500 border-l-2 border-t-2 absolute left-1 top-1 h-4 w-4"
									/>
									<div
										class="border-cyan-500 border-t-2 border-r-2 absolute top-1 right-1 h-4 w-4"
									/>
									<div
										class="border-cyan-500 border-b-2 border-l-2 absolute bottom-1 left-1 h-4 w-4"
									/>
									<div
										class="border-cyan-500 border-b-2 border-r-2 absolute bottom-1 right-1 h-4 w-4"
									/>
								</div>
								<div class="w-full h-full absolute bg-cyan-400/10" />
							</div>
						</div>
					{/if}
					<div class="border-cyan-500 border-l-2 border-t-2 absolute -left-1 -top-1 h-4 w-4" />
					<div class="border-cyan-500 border-t-2 border-r-2 absolute -top-1 -right-1 h-4 w-4" />
					<div class="border-cyan-500 border-b-2 border-l-2 absolute -bottom-1 -left-1 h-4 w-4" />
					<div class="border-cyan-500 border-b-2 border-r-2 absolute -bottom-1 -right-1 h-4 w-4" />
				</div>
			</div>
		{/if}
	</div>
	<div use:actionWhenInViewport />
</div>
