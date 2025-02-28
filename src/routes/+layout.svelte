<script lang="ts">
	import '../app.css';
	let { children } = $props();
</script>

<div class="px-4 py-5 space-y-4">
	{@render children()}
</div>
