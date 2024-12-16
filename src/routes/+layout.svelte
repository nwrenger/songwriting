<script lang="ts">
	import '../app.css';
	import Lightswitch from '$lib/components/Lightswitch.svelte';
	import { Avatar } from '@skeletonlabs/skeleton-svelte';

	let { children } = $props();
</script>

<div class="max-w-5xl mx-auto space-y-4 px-4 py-5 overflow-x-hidden">
	<!-- Header -->
	<header>
		<div class="w-full h-[48px] flex items-center justify-between">
			<Avatar size="h-full w-[48px]" name="Nils" src="favicon.webp"></Avatar>
			<Lightswitch />
		</div>
	</header>
	<!-- Main -->
	{@render children()}
</div>
