<script>
	import '../app.css';
	import { dev } from '$app/environment';
	import { inject } from '@vercel/analytics';
	import { onNavigate } from '$app/navigation';
	import { setupViewTransition } from 'sveltekit-view-transition';

	/** @type {{children?: import('svelte').Snippet}} */
	let { children } = $props();

	setupViewTransition();

	onNavigate((navigation) => {
		if (!document.startViewTransition) return;

		return new Promise((resolve) => {
			document.startViewTransition(async () => {
				resolve();
				await navigation.complete;
			});
		});
	});

	inject({ mode: dev ? 'development' : 'production' });
</script>

{@render children?.()}

<style>
	/* Disable default crossfade. */
	:root {
		view-transition-name: none;
	}

	/* Or, just modify the duration. */
	:global(::view-transition-old(root)),
	:global(::view-transition-new(root)) {
		animation-duration: 2s;
	}
</style>
