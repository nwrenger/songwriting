<script lang="ts">
	import { PdfViewer } from 'svelte-pdf-simple';
	import type { PdfException, PdfLoadSuccess, PdfPageContent } from 'svelte-pdf-simple';
	import { fade } from 'svelte/transition';
	import { ArrowLeft, ArrowRight, EyeOff, NotebookPen } from 'lucide-svelte';

	interface Props {
		pdfContent?: string;
	}

	let { pdfContent }: Props = $props();

	let pdfViewer: PdfViewer | undefined = $state();
	let pageNumber = $state(0);
	let totalPages = $state(0);
	let isPdfLoaded = $state(false);
	let password = $state('');

	let showPdf = $state(true);

	let innerHeight: number | undefined = $state();
	let innerWidth: number | undefined = $state();

	let width = $state(300);
	let height = $state(300);
	const minWidth = 200;
	const minHeight = 200;
	const aspectRatio: number = 210 / 297;

	let possibleWidth = $derived((innerWidth || width) - 16);
	let possibleHeight = $derived((innerHeight || height) - 20);

	let resizing = false;
	let startX = 0;
	let startY = 0;
	let startWidth = 0;
	let startHeight = 0;

	$effect(() => {
		if (pdfViewer) pageNumber = 1;
	});

	$effect(() => {
		width = Math.min(possibleWidth, width);
	});

	$effect(() => {
		height = Math.min(possibleHeight, height);
	});

	function navigatePages(forward: boolean = false): void {
		if (forward) {
			pageNumber = pageNumber === totalPages ? 1 : pageNumber + 1;
		} else {
			pageNumber = pageNumber === 1 ? totalPages : pageNumber - 1;
		}
		pdfViewer?.goToPage(pageNumber);
	}

	function handlePageChanged(event: CustomEvent<PdfPageContent>): void {
		pageNumber = event.detail.pageNumber;
	}

	function handleLoadedSuccess(event: CustomEvent<PdfLoadSuccess>) {
		totalPages = event.detail.totalPages;
		pageNumber = 1;
		isPdfLoaded = true;
		height = Math.round(width / aspectRatio);
	}

	function handleLoadFailure(event: CustomEvent<PdfException>) {
		console.error('Failed to load PDF:', event.detail);
	}

	function onMouseDown(e: MouseEvent) {
		// styles for the cursor
		document.body.style.cursor = 'nesw-resize';
		resizing = true;
		startX = e.clientX;
		startY = e.clientY;
		startWidth = width;
		startHeight = height;
		window.addEventListener('mousemove', onMouseMove);
		window.addEventListener('mouseup', onMouseUp);
	}

	function onMouseMove(e: MouseEvent) {
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

	function onMouseUp() {
		// styles for the cursor
		document.body.style.cursor = '';
		resizing = false;
		window.removeEventListener('mousemove', onMouseMove);
		window.removeEventListener('mouseup', onMouseUp);
	}

	function togglePdfViewer() {
		showPdf = !showPdf;
	}
</script>

<svelte:window bind:innerWidth bind:innerHeight />

{#if pdfContent}
	<div transition:fade|global={{ duration: 600 }}>
		{#key pdfContent}
			{#if !showPdf}
				<button
					type="button"
					class="fixed bottom-4 left-4 btn-icon preset-filled-primary-500"
					onclick={togglePdfViewer}
					title="Zeige PDF Viewer"
				>
					<NotebookPen />
				</button>
			{:else}
				<div
					class="fixed bottom-4 left-4 card preset-filled-surface-100-900 border-[1px] border-surface-200-800 p-4 text-center shadow-lg rounded overflow-hidden flex flex-col gap-4"
					style="width: {width}px; height: {height}px; min-width:200px; min-height:200px;"
				>
					<button
						class="absolute top-0 right-0 w-4 h-4 bg-surface-200-800 select-none"
						onmousedown={onMouseDown}
						style="border-bottom-left-radius: 4px; cursor:nesw-resize;"
						title="Drag to resize"
						aria-label="Drag to resize"
					></button>

					<button
						type="button"
						class="absolute top-1 left-1 btn-icon preset-tonal-surface"
						onclick={togglePdfViewer}
						title="Verstecke PDF Viewer"
					>
						<EyeOff />
					</button>

					{#if isPdfLoaded}
						<div class="flex items-center justify-center gap-4">
							<button
								type="button"
								class="btn-icon preset-filled"
								onclick={() => navigatePages(false)}
								title="Vorherige Seite"
							>
								<ArrowLeft size={16} />
							</button>
							<span class="text-sm">{pageNumber}/{totalPages}</span>
							<button
								type="button"
								class="btn-icon preset-filled"
								onclick={() => navigatePages(true)}
								title="Nächste Seite"
							>
								<ArrowRight size={16} />
							</button>
						</div>
					{/if}

					<div class="border border-surface-200-800 flex-1 overflow-auto">
						<a href={pdfContent} class="cursor-zoom-in">
							<PdfViewer
								bind:this={pdfViewer}
								props={{
									path: pdfContent,
									scale: 5.0,
									withAnnotations: true,
									withTextContent: true
								}}
								on:load_success={handleLoadedSuccess}
								on:load_failure={handleLoadFailure}
								on:page_changed={handlePageChanged}
								class="w-full h-full"
							>
								<svelte:fragment slot="loading">
									<div class="text-sm text-center p-2">Loading PDF...</div>
								</svelte:fragment>
								<svelte:fragment slot="loading_failed">
									<div class="text-sm text-center p-2 text-red-500">
										Something went wrong loading the PDF.
									</div>
								</svelte:fragment>
								<svelte:fragment slot="password_required">
									<p class="text-sm mb-2">
										This PDF is password protected. Please enter the password:
									</p>
									<div class="flex gap-2 justify-center">
										<input
											class="border border-gray-300 rounded p-1 text-sm"
											type="password"
											bind:value={password}
										/>
										<button
											type="button"
											class="btn preset-filled-primary-500"
											onclick={() => pdfViewer?.openWithPassword(password)}
										>
											Unlock
										</button>
									</div>
								</svelte:fragment>
							</PdfViewer>
						</a>
					</div>
				</div>
			{/if}
		{/key}
	</div>
{/if}
