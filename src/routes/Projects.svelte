<script lang="js">
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

	/**
     * @type {(number | undefined)[]}
     */
	let timeouts = [];

	function actionWhenInViewport(e) {
		const observer = new IntersectionObserver((entries) => {
			if (entries[0].isIntersecting) {
				transmissionVisible = true;
				timeouts.push(setTimeout(() => {
					transmissionVisible = false;
					cardVisible = true;
					timeouts.push(setTimeout(() => {
						textVisible = true;
					}, 1500));
				}, 1500));
			} else {
				transmissionVisible = false;
				cardVisible = false;
				textVisible = false;

				for (var i=0; i<timeouts.length; i++) {
					clearTimeout(timeouts[i]);
				}
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
					class="relative flex p-6 gap-8 flex-col h-full w-full items-center bg-cyan-500/20"
					in:project={{ duration: 2500 }}
				>
					{#if textVisible}
							<div
								class="w-full text-center font-bold text-5xl text-white"
								in:typewriter={{ speed: 2.5 }}
							>
								My Projects
							</div>

							<div class="grid grid-rows-2 grid-cols-2 gap-2 h-full w-full">
								<div class="bg-[url(/hok.png)] bg-cover w-full h-full relative group flex align-middle">
									<div class="bg-cyan-900/80 group-hover:bg-cyan-900/95 w-full h-full absolute transition-all">
										<div class="w-full h-full flex items-center justify-center absolute p-6">
											<div class="text-cyan-500 text-6xl w-full text-center">HOK
											<div class="text-cyan-500 group-hover:block hidden transition-all text-base w-full text-center">HOK offers an online platform for buying and selling sneakers locally. We team up with city sneaker stores for authentication. Sellers drop off, stores verify, and buyers pick up, ensuring safe transactions. This model also boosts store traffic and potential sales.</div>
											</div>
										</div>
									</div>
									<div class="border-cyan-500 border-l-2 border-t-2 absolute transition-all left-8 top-8 group-hover:left-2 group-hover:top-2 h-2 w-2" />
									<div class="border-cyan-500 border-t-2 border-r-2 absolute transition-all top-8 right-8 group-hover:top-2 group-hover:right-2 h-2 w-2" />
									<div class="border-cyan-500 border-b-2 border-l-2 absolute transition-all bottom-8 left-8 group-hover:bottom-2 group-hover:left-2 h-2 w-2" />
									<div class="border-cyan-500 border-b-2 border-r-2 absolute transition-all bottom-8 right-8 group-hover:bottom-2 group-hover:right-2 h-2 w-2" />
								</div>
								<div class="bg-[url(/nolai.png)] bg-cover w-full h-full relative group flex align-middle">
									<div class="bg-cyan-900/80 group-hover:bg-cyan-900/95 w-full h-full absolute transition-all">
										<div class="w-full h-full flex items-center justify-center absolute p-6">
											<div class="text-cyan-500 text-6xl w-full text-center">NOLAI
											<div class="text-cyan-500 group-hover:block hidden transition-all text-base w-full text-center">NOLAI is an AI shopping assistant for helping customers find products from the ORIGINS product catalog. It is intended to be the digital analog of an in-store salesperson. These assistants have been proven to decrease customer churn, and increase satisfaction, average purchase price, and purchase rate</div>
											</div>
										</div>
									</div>
									<div class="border-cyan-500 border-l-2 border-t-2 absolute transition-all left-8 top-8 group-hover:left-2 group-hover:top-2 h-2 w-2" />
									<div class="border-cyan-500 border-t-2 border-r-2 absolute transition-all top-8 right-8 group-hover:top-2 group-hover:right-2 h-2 w-2" />
									<div class="border-cyan-500 border-b-2 border-l-2 absolute transition-all bottom-8 left-8 group-hover:bottom-2 group-hover:left-2 h-2 w-2" />
									<div class="border-cyan-500 border-b-2 border-r-2 absolute transition-all bottom-8 right-8 group-hover:bottom-2 group-hover:right-2 h-2 w-2" />
								</div>
								<div class="bg-[url(/ebay.png)] bg-cover w-full h-full relative group flex align-middle">
									<div class="bg-cyan-900/80 group-hover:bg-cyan-900/95 w-full h-full absolute transition-all">
										<div class="w-full h-full flex items-center justify-center absolute p-6">
											<div class="text-cyan-500 text-6xl w-full text-center">EBAY-UMLC
											<div class="text-cyan-500 group-hover:block hidden transition-all text-base w-full text-center">I competed in a challenge focused on Named Entity Recognition (NER), a key task in NLP, specifically targeting eBay listing titles. The goal was to extract and label various aspects, like "Brand name", from item titles. Not all titles contained every aspect, adding to the complexity. I secured the 9th place.</div>
											</div>
										</div>
									</div>
									<div class="border-cyan-500 border-l-2 border-t-2 absolute transition-all left-8 top-8 group-hover:left-2 group-hover:top-2 h-2 w-2" />
									<div class="border-cyan-500 border-t-2 border-r-2 absolute transition-all top-8 right-8 group-hover:top-2 group-hover:right-2 h-2 w-2" />
									<div class="border-cyan-500 border-b-2 border-l-2 absolute transition-all bottom-8 left-8 group-hover:bottom-2 group-hover:left-2 h-2 w-2" />
									<div class="border-cyan-500 border-b-2 border-r-2 absolute transition-all bottom-8 right-8 group-hover:bottom-2 group-hover:right-2 h-2 w-2" />
								</div>
								<div class="bg-[url(/sped.png)] bg-cover w-full h-full relative group flex align-middle">
									<div class="bg-cyan-900/80 group-hover:bg-cyan-900/95 w-full h-full absolute transition-all">
										<div class="w-full h-full flex items-center justify-center absolute p-6">
											<div class="text-cyan-500 text-6xl w-full text-center">SUPERSPED
											<div class="text-cyan-500 group-hover:block hidden transition-all text-base w-full text-center">A racing game built in Unity Engine</div>
											</div>
										</div>
									</div>
									<div class="border-cyan-500 border-l-2 border-t-2 absolute transition-all left-8 top-8 group-hover:left-2 group-hover:top-2 h-2 w-2" />
									<div class="border-cyan-500 border-t-2 border-r-2 absolute transition-all top-8 right-8 group-hover:top-2 group-hover:right-2 h-2 w-2" />
									<div class="border-cyan-500 border-b-2 border-l-2 absolute transition-all bottom-8 left-8 group-hover:bottom-2 group-hover:left-2 h-2 w-2" />
									<div class="border-cyan-500 border-b-2 border-r-2 absolute transition-all bottom-8 right-8 group-hover:bottom-2 group-hover:right-2 h-2 w-2" />
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
