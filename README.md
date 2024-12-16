# sv

Everything you need to build a Svelte project, powered by [`sv`](https://github.com/sveltejs/cli).

## Creating a project

If you're seeing this, you've probably already done this step. Congrats!

```bash
# create a new project in the current directory
npx sv create

# create a new project in my-app
npx sv create my-app
```

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

## Building

To create a production version of your app:

```bash
npm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://svelte.dev/docs/kit/adapters) for your target environment.

pastebin:
<!-- {#snippet introContent()}
	<p>Jooo!</p>
{/snippet}

{#snippet someSubContent()}
	<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
		<div
			class="card preset-filled-surface-100-900 border-[1px] border-surface-200-800 w-full max-w-md p-4 text-center"
			in:fly|global={{ x: -50, duration: 600 }}
			out:fly|global={{ x: 50, duration: 600 }}
		>
			<h4 class="font-bold">Subsection 1</h4>
			<p>Details über Subsection 1.</p>
		</div>
		<div
			class="card preset-filled-surface-100-900 border-[1px] border-surface-200-800 w-full max-w-md p-4 text-center"
			in:fly|global={{ x: 50, duration: 600 }}
			out:fly|global={{ x: -50, duration: 600 }}
		>
			<h4 class="font-bold">Subsection 2</h4>
			<p>Details über Subsection 2.</p>
		</div>
		<div
			class="card preset-filled-surface-100-900 border-[1px] border-surface-200-800 w-full max-w-md p-4 text-center"
			in:fly|global={{ x: -50, duration: 600 }}
			out:fly|global={{ x: 50, duration: 600 }}
		>
			<h4 class="font-bold">Subsection 3</h4>
			<p>Details über Subsection 3.</p>
		</div>
		<div
			class="card preset-filled-surface-100-900 border-[1px] border-surface-200-800 w-full max-w-md p-4 text-center"
			in:fly|global={{ x: 50, duration: 600 }}
			out:fly|global={{ x: -50, duration: 600 }}
		>
			<h4 class="font-bold">Subsection 4</h4>
			<p>Details über Subsection 4.</p>
		</div>
	</div>
{/snippet} -->
