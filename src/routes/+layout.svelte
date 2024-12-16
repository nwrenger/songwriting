<script lang="ts">
	import '../app.css';
	import Lightswitch from '$lib/components/Lightswitch.svelte';
	import { Avatar } from '@skeletonlabs/skeleton-svelte';

	let { children } = $props();
</script>

<div class="px-4 py-5 space-y-4">
	<!-- Header -->
	<header>
		<div class="max-w-5xl mx-auto w-full h-[48px] flex items-center justify-between">
			<Avatar size="h-full w-[48px]" name="Nils" src="favicon.webp"></Avatar>
			<Lightswitch />
		</div>
	</header>
	<!-- Main -->
	{@render children()}
</div>
