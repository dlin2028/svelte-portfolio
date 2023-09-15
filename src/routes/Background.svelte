<script>
	let currSelected = 1;
	import { base } from '$app/paths';
</script>

<div class="h-full w-full bg-white p-10">
	<div class="text-center">My Experience</div>
	<div class="flex flex-col gap-2 w-full">
		<div class="w-full h-20 {currSelected == 1 ? "h-72" : ""} p-0 border border-black group transition-all">
			<button class="w-full h-20 bg-black flex justify-center" on:click={() => {currSelected = 1}}>
				<img class="h-20" src="{base}/elc-logo.jpg" alt="elc logo" />
			</button>
		{#if currSelected == 1}
			<div class="text-xl">
				Full Stack Developer Intern <br> <i>Jun - Aug 2023</i> <br>
				In an Agile team, I contributed to ideating and developing a generative AI chatbot projected to generate $11 billion. Conducted focus groups, liaised with experts, and secured project clearances. Successfully pitched the MVP to the global brand president, securing approval for further development—a first for an internship project.
			</div>
		{/if}
		</div>
		<div class="w-full border border-black">
			<button class="w-full flex justify-center" on:click={() => {currSelected = 2}}>
				<img class="h-20" src="{base}/oppo-logo.png" alt="oppo logo" />

			</button>
			{#if currSelected == 2}
				<div class="text-xl">
					STG Research Intern <br> <i>Jun - Aug 2022</i> <br>
					Developed and ported software for advanced hardware on various platforms, managing both local and overseas teams. Acquired skills in media streaming, hardware optimization, UI/UX design, and cross-compiling for Android, Linux, and Windows. Additionally, authored documentation for these processes.
				</div>
			{/if}
		</div>
		<div class="w-full border border-black">
			<button class="w-full h-20 bg-black flex justify-center" on:click={() => {currSelected = 3}}>
				<img class="h-20" src="{base}/pap-logo.png" alt="pap logo" />
			</button>

			{#if currSelected == 3}
			<div class="text-xl">
				Independent Contractor <br> <i>Jun - Aug 2021</i> <br>
				Developed a demo app enabling users at specific locations to view AR recreations of historical objects with real-world accuracy. Secured a contract for its future enhancement. The design, documented using Unity Engine and C# with ARFoundation, serves as the foundation for the final product.
			</div>
			{/if}
		</div>
		<div class="w-full border border-black ">
			<button class="w-full h-20 bg-black flex justify-center" on:click={() => {currSelected = 4}}>
				<img class="h-20" src="{base}/ece-logo.jpg" alt="ece logo" />
			</button>

			{#if currSelected == 4}
				<div class="text-xl">
					University of Illinois at Urbana-Champaign <br>
					<i>Aug. 2020 - May 2024</i> <br>
					Bachelor of Science in Computer Engineering 
				</div>
			{/if}
		</div>
	</div>
</div>
