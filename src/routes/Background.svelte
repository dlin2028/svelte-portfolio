<script>
	import { fade } from 'svelte/transition';
	import { fly } from 'svelte/transition';
	import { elasticOut } from 'svelte/easing';
    import {flip} from 'svelte/animate'

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

    let tileClicked = 0;

	/**
     * @type {(number | undefined)[]}
     */
	var timeouts = [];

	function actionWhenInViewport(e) {
		const observer = new IntersectionObserver((entries) => {
			if (entries[0].isIntersecting) {
				transmissionVisible = true;
				timeouts.push(setTimeout(() => {
					transmissionVisible = false;
					cardVisible = true;
					timeouts.push(setTimeout(() => {
						textVisible = true;
					}, 0));
				}, 0));
			} else {
				transmissionVisible = false;
				cardVisible = false;
				textVisible = false;
                tileClicked = 0;

				for (var i=0; i<timeouts.length; i++) {
					clearTimeout(timeouts[i]);
				}
			}
		});

		observer.observe(e);
	}
</script>

<div class="w-full bg-white h-full flex items-center">
	<div class="w-full bg-white h-full flex items-center">
		{#if cardVisible}
			<div class="w-full h-screen p-6 items-center justify-center flex">
				<div
					class="relative flex h-full w-full items-center"
					in:project={{ duration: 0 }}
				>
					{#if textVisible}
						<div class="flex-col w-full h-full">
							<div
								class="w-full text-center font-bold text-5xl text-black"
								in:typewriter={{ speed: 200.5 }}
							>
								My Experience
							</div>

                            <hr class="h-px my-8 bg-gray-200 border-0 dark:bg-gray-700">

                            <div class="xs:flex-col sm:flex w-full relative align-middle">
								<div class="text-3xl basis-1/3 text-center">
									2023
                                </div>
								<div class="text-3xl basis-1/3 text-center">
									2022
								</div>
								<div class="text-3xl basis-1/3 text-center">
									2021
								</div>
							</div>

                            <div class="border bg-indigo-950 w-full h-20 text-lg">
                                <div class="flex w-full h-full justify-center hover:justify-start text-transparent hover:text-white ">
                                    <img class="h-full object-contain " src="/ece-logo.jpg" alt="ece logo" transition:fly />
                                    <div class="absolute text-sm text-right w-full px-5 ">
                                        University of Illinois at Urbana Champaign <br>
                                        BS in Computer Engineering <br>
                                        Graduating May 2024 <br>
                                    </div>
                                </div>
                            </div>

							<div class="xs:flex-col sm:flex sm:h-1/2 relative align-middle">
								<button class="{tileClicked == 1 ? "basis-2/3" : (tileClicked == 0 ? "basis-1/3 hover:basis-2/5" : "basis-1/6")} basis-1/3 relative flex bg-black text-white transition-all duration-500" on:click={() => {tileClicked = 1}}>
									<img class="h-full w-full object-contain" src="/elc-logo.jpg" alt="elc logo" />
                                    {#if tileClicked == 1}
                                        <div class="w-full bg-black text-sm">
                                            Estee Lauder Companies Inc. Jun. 2023 - Aug. 2023
Full Stack Developer Intern New York, New York
• Worked in an Agile team to ideate and develop a generative AI chatbot which was projected to drive $11 billion
• Held focus groups, contacted experts, got clearance to proceed development
• Presented final MVP to global brand president, where permission was granted for further development, a first for
an internship projec
                                        </div>
                                    {/if}
								</button>
								<button class="{tileClicked == 2 ? "basis-2/3" : (tileClicked == 0 ? "basis-1/3 hover:basis-2/5" : "basis-1/6")} relative basis-1/3 flex px-4 bg-white text-white transition-all duration-500" on:click={() => {tileClicked = 2}}>
									<img class="object-contain" src="/oppo-logo.png" alt="oppo logo" />
                                    {#if tileClicked == 2}
                                        <div class="w-full bg-white text-sm text-black">
                                            Estee Lauder Companies Inc. Jun. 2023 - Aug. 2023
Full Stack Developer Intern New York, New York
• Worked in an Agile team to ideate and develop a generative AI chatbot which was projected to drive $11 billion
• Held focus groups, contacted experts, got clearance to proceed development
• Presented final MVP to global brand president, where permission was granted for further development, a first for
an internship projec
                                        </div>
                                    {/if}
								</button>
								<button class="{tileClicked == 3 ? "basis-2/3" : (tileClicked == 0 ? "basis-1/3 hover:basis-2/5" : "basis-1/6")} relative bg-black flex text-white transition-all duration-500" on:click={() => {tileClicked = 3}}>
									<img class="h-full object-contain" src="/pap-logo.png" alt="pap logo" />
                                    {#if tileClicked == 3}
                                    <div class="w-full bg-black text-sm text-white">
                                        Estee Lauder Companies Inc. Jun. 2023 - Aug. 2023
Full Stack Developer Intern New York, New York
• Worked in an Agile team to ideate and develop a generative AI chatbot which was projected to drive $11 billion
• Held focus groups, contacted experts, got clearance to proceed development
• Presented final MVP to global brand president, where permission was granted for further development, a first for
an internship projec
                                    </div>
                                {/if}
								</button>
							</div>
						</div>
					{/if}
				</div>
			</div>
		{/if}
	</div>
	<div use:actionWhenInViewport />
</div>
