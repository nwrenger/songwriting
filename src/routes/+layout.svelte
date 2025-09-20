<script lang="ts">
	import '../app.css';

	let { children } = $props();
	const year = new Date().getFullYear();
</script>

<div class="py-5 space-y-4">
	{@render children()}
</div>

<footer class="border-surface-200-800 border-t">
	<div class="mx-auto flex max-w-5xl flex-row items-center justify-between gap-3 px-4 py-6 text-sm">
		<p class="text-surface-600 text-center text-xs sm:text-sm">
			<span class="opacity-80">© {year}</span> · <span class="font-medium">Nils Wrenger</span>
		</p>

		<div class="flex flex-wrap items-center gap-4">
			<a href="https://nwrenger.dev/privacy-policy" class="anchor text-center">Privacy Policy</a>
		</div>
	</div>
</footer>
