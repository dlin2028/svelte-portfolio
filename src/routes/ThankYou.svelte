<script>
	import { fade } from 'svelte/transition';
	import { elasticOut } from 'svelte/easing';

	function spin(node, { duration }) {
		return {
			duration,
			css: (t) => {
				const eased = elasticOut(t);

				return `
					transform: scale(${eased}) rotate(${eased * 1080}deg);
					color: hsl(
						${Math.trunc(t * 360)},
						${Math.min(100, 1000 * (t))}%,
						${Math.min(50, 500 * (t))}%
					);`;
			}
		};
	}

    let visible = false;

    function actionWhenInViewport(e) {

        const observer = new IntersectionObserver(entries => {
            if(entries[0].isIntersecting) {
                visible = true;
            }
            else
            {
                visible = false;
            }
        });

        observer.observe(e);
    }

</script>


<div class="w-full h-full flex items-center">
{#if visible}
    <div class="w-full text-center font-bold text-5xl text-white"  in:spin={{ duration: 8000 }}
    out:fade>
        Thank You!
    </div>
{/if}
<div use:actionWhenInViewport></div>
</div>

