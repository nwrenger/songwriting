<script module lang="ts">
	export interface Score {
		url: string;
		songSnippets: SongSnippet[];
	}

	export interface SongSnippet {
		name: string;
		url: string;
	}
</script>

<script lang="ts">
	import { PdfViewer } from 'svelte-pdf-simple';
	import type { PdfLoadSuccess, PdfPageContent } from 'svelte-pdf-simple';
	import { fade } from 'svelte/transition';
	import { ArrowLeft, ArrowRight, EyeOff, Music, Pause, Play } from 'lucide-svelte';

	interface Props {
		score?: Score;
	}

	let { score }: Props = $props();

	let pdfViewer: PdfViewer | undefined = $state();
	let pageNumber = $state(0);
	let totalPages = $state(0);
	let isPdfLoaded = $state(false);

	let showPdf = $state(true);

	let innerHeight: number | undefined = $state();
	let innerWidth: number | undefined = $state();

	// Height: + 1 * 16px Border, + 36px Buttons, + 64px Musik Controls
	// Width: + 3 * 16px Border,
	const aspectRatio: number = (2 * 16 + 210) / (1 * 16 + 36 + 297 + 64);
	let width = $state(400);
	let height = $state(Math.round(400 / aspectRatio));
	const minWidth = 200;
	const minHeight = 200;

	const padding = 16 * 2;
	let possibleWidth = $derived((innerWidth || width) - padding);
	let possibleHeight = $derived((innerHeight || height) - padding);

	let resizing = false;
	let startX = 0;
	let startY;
	let startWidth = 0;
	let startHeight;

	let audioEl: HTMLAudioElement | undefined = $state();
	let paused = $state(true);

	$effect(() => {
		if (pdfViewer) pageNumber = 1;
	});

	$effect(() => {
		if (audioEl && audioEl.src) paused = true;
	});

	$effect(() => {
		width = Math.min(possibleWidth, width);
	});

	$effect(() => {
		height = Math.min(possibleHeight, height);
	});

	async function navigatePages(forward: boolean = false): Promise<void> {
		if (forward) {
			pageNumber = pageNumber === totalPages ? 1 : pageNumber + 1;
		} else {
			pageNumber = pageNumber === 1 ? totalPages : pageNumber - 1;
		}
		isPdfLoaded = false;
		await pdfViewer?.goToPage(pageNumber);
		isPdfLoaded = true;
	}

	function loadedSuccess(event: CustomEvent<PdfLoadSuccess>) {
		totalPages = event.detail.totalPages;
		isPdfLoaded = true;
	}

	function loadedFailed() {
		isPdfLoaded = true;
	}

	function pageChanged(event: CustomEvent<PdfPageContent>): void {
		pageNumber = event.detail.pageNumber;
	}

	function onDown(e: PointerEvent) {
		document.body.style.cursor = 'nesw-resize';
		resizing = true;
		startX = e.clientX;
		startY = e.clientY;
		startWidth = width;
		startHeight = height;
		window.addEventListener('pointermove', onMove);
		window.addEventListener('pointerup', onUp);
	}

	function onMove(e: PointerEvent) {
		if (!resizing) return;

		const dx = e.clientX - startX;
		const newWidth = startWidth + dx;

		const adjWidth = Math.max(minWidth, newWidth);
		const adjHeight = Math.max(minHeight, Math.round(adjWidth / aspectRatio));
		if (adjHeight < possibleHeight && adjWidth < possibleWidth) {
			width = adjWidth;
			height = adjHeight;
		}
	}

	function onUp() {
		document.body.style.cursor = '';
		resizing = false;
		window.removeEventListener('pointermove', onMove);
		window.removeEventListener('pointerup', onUp);
	}

	function togglePdfViewer() {
		showPdf = !showPdf;
	}

	function togglePlay() {
		paused = !paused;
	}

	function selectSong(e: Event) {
		let target = e.target as HTMLSelectElement;
		if (audioEl) audioEl.src = target.value;
	}
</script>

<svelte:window bind:innerWidth bind:innerHeight />

{#if score}
	<div transition:fade|global={{ duration: 600 }}>
		{#key score}
			{#if !showPdf}
				<button
					type="button"
					class="fixed bottom-4 left-4 btn-icon preset-filled-primary-500"
					onclick={togglePdfViewer}
					title="Zeige Notenübersicht"
				>
					<Music size={24} />
				</button>
			{:else}
				<div
					class="fixed touch-none bottom-4 left-4 card preset-filled-surface-100-900 border-[1px] border-surface-200-800 p-4 text-center shadow-lg rounded overflow-hidden flex flex-col gap-4"
					style="width: {width}px; height: {height}px; min-width:200px; min-height:200px;"
				>
					<button
						class="absolute top-0 right-0 w-5 h-5 bg-surface-200-800 select-none"
						onpointerdown={onDown}
						style="border-bottom-left-radius: 4px; border-top-right-radius: 4px; cursor:nesw-resize;"
						title="Ziehen um die Größe zu ändern"
						aria-label="Ziehen um die Größe zu ändern"
					></button>

					<button
						type="button"
						class="absolute top-1 left-1 btn-icon preset-tonal-surface"
						onclick={togglePdfViewer}
						title="Verstecke Notenübersicht"
					>
						<EyeOff />
					</button>

					<div class="flex items-center justify-center gap-4">
						<button
							type="button"
							class="btn-icon preset-filled"
							onclick={async () => await navigatePages(false)}
							title="Vorherige Seite"
							disabled={totalPages <= 1}
						>
							<ArrowLeft size={24} />
						</button>
						<span class="text-sm">{pageNumber}/{totalPages}</span>
						<button
							type="button"
							class="btn-icon preset-filled"
							onclick={async () => await navigatePages(true)}
							title="Nächste Seite"
							disabled={totalPages <= 1}
						>
							<ArrowRight size={24} />
						</button>
					</div>

					<div class="border border-surface-200-800 flex-1 overflow-auto">
						<a href={score.url} target="_blank" class="cursor-zoom-in">
							<PdfViewer
								bind:this={pdfViewer}
								props={{
									path: score.url,
									scale: 4.0,
									withAnnotations: true,
									withTextContent: true
								}}
								on:load_success={loadedSuccess}
								on:load_failure={loadedFailed}
								on:page_changed={pageChanged}
								class="w-full h-full"
							>
								<svelte:fragment slot="loading_failed">
									<div class="text-sm text-center p-2 text-error-500">
										Etwas ist schief gelaufen beim Laden des PDFs.
									</div>
								</svelte:fragment>
							</PdfViewer>
						</a>
						{#if !isPdfLoaded}
							<div class="h-full w-full bg-white"></div>
						{/if}
					</div>

					{#if score?.songSnippets && score.songSnippets.length > 0}
						<div class="flex flex-col items-center gap-2">
							<audio bind:this={audioEl} bind:paused src={score.songSnippets[0].url}></audio>
							<div class="grid grid-cols-[36px_auto] gap-4 w-full">
								<button
									type="button"
									class="btn-icon preset-filled"
									onclick={togglePlay}
									title="Start/Stop"
								>
									{#if paused}
										<Play size={24} />
									{:else}
										<Pause size={24} />
									{/if}
								</button>
								<select class="select w-full" onchange={selectSong}>
									{#each score.songSnippets as song}
										<option value={song.url}>{song.name}</option>
									{/each}
								</select>
							</div>
						</div>
					{/if}
				</div>
			{/if}
		{/key}
	</div>
{/if}
