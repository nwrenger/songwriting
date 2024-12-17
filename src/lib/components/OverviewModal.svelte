<script lang="ts">
	import { Modal } from '@skeletonlabs/skeleton-svelte';
	import { ArrowLeft, ArrowRight, Fullscreen } from 'lucide-svelte';

	interface Props {
		pictureContent: string[];
	}

	let { pictureContent = [] }: Props = $props();

	let openState = $state(false);
	let elemMovies: HTMLDivElement;
	let disabled = $derived(pictureContent.length == 0);

	function modalClose() {
		openState = false;
	}

	/** Handles the left scroll event. */
	function multiColumnLeft() {
		if (!elemMovies) return;
		let x = elemMovies.scrollWidth;
		if (elemMovies.scrollLeft !== 0) x = elemMovies.scrollLeft - elemMovies.clientWidth;
		elemMovies.scroll(x, 0);
	}

	/** Handles the right scroll event. */
	function multiColumnRight() {
		if (!elemMovies) return;
		let x = 0;
		// -1 is used because different browsers use different methods to round scrollWidth pixels.
		if (elemMovies.scrollLeft < elemMovies.scrollWidth - elemMovies.clientWidth - 1)
			x = elemMovies.scrollLeft + elemMovies.clientWidth;
		elemMovies.scroll(x, 0);
	}
</script>

<Modal
	bind:open={openState}
	triggerBase="btn-icon preset-filled-secondary-500 fixed bottom-5 right-5 {disabled
		? 'pointer-events-none opacity-40'
		: ''}"
	contentBase="card bg-surface-100-900 p-4 space-y-4 shadow-xl max-w-screen-md"
	backdropClasses="backdrop-blur-sm"
>
	{#snippet trigger()}<Fullscreen size="24" />{/snippet}
	{#snippet content()}
		<header class="">
			<h2 class="h2">Bilderüberblick</h2>
			<p>
				Klick auf ein Bild, um es in einem neuen Tab zu öffnen und so dieses vergrößert sehen zu
				können.
			</p>
		</header>
		<div class="w-ful">
			<div class="grid grid-cols-[auto_1fr_auto] gap-4 items-center">
				<!-- Button: Left -->
				<button
					type="button"
					class="btn-icon preset-filled"
					data-multi-column-left
					onclick={multiColumnLeft}
				>
					<ArrowLeft size={16} />
				</button>
				<!-- Carousel -->
				<div
					bind:this={elemMovies}
					class="snap-x snap-mandatory scroll-smooth flex gap-2 pb-2 overflow-x-auto"
				>
					{#each pictureContent as picture_src}
						<a
							href={picture_src}
							target="_blank"
							class="rounded-container-token object-cover h-auto max-h-[300px] shrink-0"
						>
							<img
								class="rounded-container-token object-cover h-auto max-h-[300px] shrink-0"
								src={picture_src}
								alt={picture_src}
								loading="lazy"
							/>
						</a>
					{/each}
				</div>
				<!-- Button-Right -->
				<button
					type="button"
					class="btn-icon preset-filled"
					data-multi-column-right
					onclick={multiColumnRight}
				>
					<ArrowRight size={16} />
				</button>
			</div>
		</div>
		<footer class="flex justify-end gap-4">
			<button type="button" class="btn preset-tonal" onclick={modalClose}>Schließen</button>
		</footer>
	{/snippet}
</Modal>
