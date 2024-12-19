<script lang="ts">
	import { ArrowLeft, ArrowRight, EyeOff, Images } from 'lucide-svelte';
	import { fade } from 'svelte/transition';

	interface Props {
		pictures: string[] | undefined;
	}

	let { pictures = [] }: Props = $props();

	let showImages = $state(true);

	let innerHeight: number | undefined = $state();
	let innerWidth: number | undefined = $state();

	let pictureIndex = $state(0);
	let totalImages = $derived(pictures?.length);
	let currentImage = $derived(pictures[pictureIndex]);

	let width = $state(600);
	let height = $state(400);
	const minWidth = 200;
	const minHeight = 200;

	let resizing = false;
	let startX = 0;
	let startY = 0;
	let startWidth = 0;
	let startHeight = 0;

	$effect(() => {
		if (pictures) pictureIndex = 0;
	});

	$effect(() => {
		width = Math.min((innerWidth || width) - 16, width);
	});

	$effect(() => {
		height = Math.min((innerHeight || height) - 20, height);
	});

	function onDown(e: PointerEvent) {
		resizing = true;
		startX = e.clientX;
		startY = e.clientY;
		startWidth = width;
		startHeight = height;
		document.body.style.cursor = 'nwse-resize';
		window.addEventListener('pointermove', onMove);
		window.addEventListener('pointerup', onUp);
	}

	function onMove(e: PointerEvent) {
		if (!resizing) return;

		const dx = e.clientX - startX;
		const dy = e.clientY - startY;

		const newWidth = startWidth - dx;
		const newHeight = startHeight - dy;

		width = Math.max(minWidth, newWidth);
		height = Math.max(minHeight, newHeight);
	}

	function onUp() {
		resizing = false;
		document.body.style.cursor = '';
		window.removeEventListener('pointermove', onMove);
		window.removeEventListener('pointerup', onUp);
	}

	function toggleView() {
		showImages = !showImages;
	}

	function nextImage() {
		if (totalImages < 2) return;
		pictureIndex = (pictureIndex + 1) % totalImages;
	}

	function prevImage() {
		if (totalImages < 2) return;
		pictureIndex = (pictureIndex - 1 + totalImages) % totalImages;
	}
</script>

<svelte:window bind:innerWidth bind:innerHeight />

{#if pictures?.length > 0}
	<div transition:fade|global={{ duration: 600 }}>
		{#if !showImages}
			<button
				type="button"
				class="fixed bottom-4 right-4 btn-icon preset-filled-secondary-500"
				onclick={toggleView}
				title="Zeige Bilderübersicht"
			>
				<Images size={24} />
			</button>
		{:else}
			<div
				class="fixed touch-none bottom-4 right-4 card bg-surface-100-900 border-[1px] border-surface-200-800 p-4 shadow-xl rounded flex flex-col gap-4"
				style="width: {width}px; height: {height}px; min-width: {minWidth}px; min-height: {minHeight}px;"
			>
				<button
					class="absolute top-0 left-0 w-5 h-5 bg-surface-200-800 select-none"
					style="border-bottom-right-radius:4px; cursor:nwse-resize;"
					onpointerdown={onDown}
					title="Ziehen um die Größe zu ändern"
					aria-label="Ziehen um die Größe zu ändern"
				></button>

				<button
					type="button"
					class="absolute top-1 right-1 btn-icon preset-tonal-surface"
					onclick={toggleView}
					title="Verstecke Bilderübersicht"
				>
					<EyeOff />
				</button>

				<div class="flex items-center justify-center gap-4">
					<button
						type="button"
						class="btn-icon preset-filled"
						onclick={prevImage}
						title="Vorheriges Bild"
						disabled={totalImages <= 1}
					>
						<ArrowLeft size={24} />
					</button>
					<span class="text-sm">{pictureIndex + 1}/{totalImages}</span>
					<button
						type="button"
						class="btn-icon preset-filled"
						onclick={nextImage}
						title="Nächstes Bild"
						disabled={totalImages <= 1}
					>
						<ArrowRight size={24} />
					</button>
				</div>

				<div class="flex items-center justify-center h-full overflow-hidden">
					{#if currentImage}
						<a
							href={currentImage}
							class="cursor-zoom-in flex items-center justify-center w-full h-full"
							target="_blank"
							title="Bild in neuen Tab öffnen"
						>
							<img
								src={currentImage}
								alt={currentImage}
								class="max-w-full max-h-full object-contain"
								loading="lazy"
							/>
						</a>
					{/if}
				</div>
			</div>
		{/if}
	</div>
{/if}
