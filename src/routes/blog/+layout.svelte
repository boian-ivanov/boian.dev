<script lang="ts">
	import Particles from '$lib/components/Particles.svelte';
	interface Props {
		children?: import('svelte').Snippet;
	}

	let { children }: Props = $props();
</script>

<Particles className="absolute inset-0 overflow-x-hidden" />

<div class="bg-black">
	<div
		class="relative z-10 mx-auto min-h-screen max-w-2xl bg-black px-6 py-12 font-sans antialiased sm:py-24"
	>
		{@render children?.()}
	</div>
</div>
