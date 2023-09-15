<script>
  import { onMount } from 'svelte';	import 
  { fade } from 'svelte/transition';

    let ready = false;
    onMount(() => ready = true);
</script>

<div class="w-full h-full p-6">
    <div class="w-full bg-gray-100/10 h-full flex items-center border relative">
        {#if ready}
        <div class="flex-col w-full">
            <div class="w-full text-center font-bold text-5xl text-white " in:fade>
                Nice to meet you, I'm <br />
                David Lin
            </div>
            <div class="flex sm:flex-col md:flex-row w-full items-center px-20 py-5 gap-10">
                <div class="sm:w-32 md:basis-1/3 h-12 text-white justify-center text-sm bg-teal-800 border flex items-center">Resume</div>
                <div class="sm:w-32 md:basis-1/3 h-12 text-white justify-center text-sm bg-teal-800 border flex items-center">GitHub</div>
                <div class="sm:w-32 md:basis-1/3 h-12 text-white justify-center text-sm bg-teal-800 border flex items-center">LinkedIn</div>
            </div>
        </div>
        {/if}
        <a class="absolute inset-x-0 bottom-0 text-white/50 text-lg text-center animate-bounce" href="#background">
            Scroll Down
            <br>
            \/
        </a>
    </div>
</div>
