<script>
    import Background from "./Background.svelte";
	import Contact from "./Contact.svelte";
    import Hello from "./Hello.svelte";
	import Projects from "./Projects.svelte";
	import ThankYou from "./ThankYou.svelte";

</script>
<body class="bg-gradient-to-r from-teal-900 to-cyan-900 p-0">
	<div class="w-full h-full grid gap-4">
		<div class="w-full h-screen items-center">
			<section id="home" class="py-6 flex-col">
                <header class="w-full text-gray-700 body-font border-b border-gray-200">
                    <div class="container mx-auto flex flex-col flex-wrap p-5 md:flex-row items-center">
                        <a
                            class="flex title-font font-medium items-center text-gray-900 mb-4 md:mb-0"
                            href="#home"
                            target="_blank"
                        >
                            <span class="ml-3 text-white text-xl">DAVID LIN</span>
                        </a>
                        <nav class="md:ml-auto flex flex-wrap items-center text-base justify-center">
                            <a href="#home" class="mr-5 text-white hover:text-gray-900">Home</a>
                            <a href="#background" class="mr-5 text-white hover:text-gray-900">Background</a>
                            <a href="#projects" class="mr-5 text-white hover:text-gray-900">Projects</a>
                            <a href="#contact" class="mr-5 text-white hover:text-gray-900">Contact</a>
                        </nav>
                    </div>
                </header>
                <Hello></Hello>
			</section>
			<section id="background">
                <Background></Background>
			</section>
			<section id="projects">
                <Projects></Projects>
			</section>
			<section id="contact" class="p-10">
                <Contact></Contact>
			</section>
            <section class="text-white">
                <ThankYou></ThankYou>
            </section>
		</div>
	</div>
</body>
