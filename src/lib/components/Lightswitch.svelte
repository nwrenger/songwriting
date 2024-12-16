<script lang="ts">
	import { Switch } from '@skeletonlabs/skeleton-svelte';
	// Icons
	import IconMoon from 'lucide-svelte/icons/moon';
	import IconSun from 'lucide-svelte/icons/sun';
	import { onMount } from 'svelte';

	// Bind to the checked state
	let mode = $state(false);
	onMount(() => {
		mode = localStorage.getItem('theme') === 'light';
	});

	// Handle the change in state when toggled.
	function handleModeChange() {
		localStorage.setItem('theme', mode ? 'dark' : 'light');
	}

	$effect(() => {
		// On page load or when changing themes, best to add inline in `head` to avoid FOUC
		document.documentElement.classList.toggle('dark', !mode);
	});
</script>

<Switch
	name="mode"
	controlActive="bg-surface-200"
	bind:checked={mode}
	onCheckedChange={handleModeChange}
>
	{#snippet inactiveChild()}<IconMoon size="14" />{/snippet}
	{#snippet activeChild()}<IconSun size="14" />{/snippet}
</Switch>
