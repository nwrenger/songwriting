<script lang="ts">
	import Scroller from '$lib/components/Scroller.svelte';
	import { reveal } from 'svelte-reveal';
	import { fade, fly, scale } from 'svelte/transition';
	import { Music, Mic, PlayCircle, Headphones, Mouse } from 'lucide-svelte';

	let index: number = $state(0);
	let offset: number = $state(0);
	let progress: number = $state(0);
</script>

<Scroller
	top={0}
	bottom={0.8}
	bind:index
	bind:offset
	bind:progress
	overviewContent={[[], ['before.jpg'], ['ideas.jpg', 'trello.png']]}
>
	<div slot="background" class="h-full">
		<div
			class="absolute top-80 sm:top-60 md:top-54 inset-0 flex flex-col items-center justify-center space-y-8"
		>
			{#if index == 0}
				<div
					class="absolute top-20 left-8 music-note text-indigo-400"
					in:fly|global={{ x: -300, duration: 1000 }}
					out:fade|global={{ duration: 800 }}
				>
					<Music class="w-12 h-12 md:w-16 md:h-16" />
				</div>
				<div
					class="absolute top-16 right-16 music-note text-purple-400"
					in:fly|global={{ x: 300, duration: 1000 }}
					out:fade|global={{ duration: 800 }}
				>
					<Mic class="w-10 h-10 md:w-14 md:h-14" />
				</div>
				<div
					class="absolute bottom-10 left-20 music-note text-yellow-400"
					in:fly|global={{ x: -300, duration: 1000 }}
					out:fade|global={{ duration: 800 }}
				>
					<PlayCircle class="w-10 h-10 md:w-14 md:h-14" />
				</div>
				<div
					class="absolute bottom-20 right-12 music-note text-teal-400"
					in:fly|global={{ x: 300, duration: 1000 }}
					out:fade|global={{ duration: 800 }}
				>
					<Headphones class="w-12 h-12 md:w-16 md:h-16" />
				</div>
				<div
					class="absolute"
					in:scale|global={{ delay: 800, duration: 600 }}
					out:fade|global={{ duration: 800 }}
				>
					<Mouse class="w-12 h-12 md:w-16 md:h-16" />
				</div>
			{:else if index == 1}
				<img
					src="before.jpg"
					alt="before.jpg"
					class="absolute top-14 right-0 w-fit h-32 md:h-52 dark:opacity-20 opacity-30 object-contain shadow-md"
					in:fade|global={{ duration: 800, delay: 800 }}
					out:fly|global={{ duration: 800, x: 400 }}
				/>
			{:else if index == 2}
				<img
					src="ideas.jpg"
					alt="ideas.jpg"
					class="absolute top-14 left-0 w-fit h-32 md:h-52 dark:opacity-20 opacity-30 object-contain shadow-md"
					in:fade|global={{ duration: 800, delay: 800 }}
					out:fly|global={{ duration: 800, x: -400 }}
				/>
				<img
					src="trello.png"
					alt="trello.png"
					class="absolute top-20 right-0 w-fit h-32 md:h-52 dark:opacity-20 opacity-30 object-contain shadow-md"
					in:fade|global={{ duration: 800, delay: 800 }}
					out:fly|global={{ duration: 800, x: 400 }}
				/>
			{/if}
		</div>
	</div>

	<div slot="foreground" class="space-y-52 sr__hide pt-8 md:pt-12 pb-8 md:pb-12">
		<section use:reveal>
			<h1 class="h1 pb-3 md:pb-5">Songwriting Portfolio</h1>
			<p>Willkommen auf meinem Portfolio zum Projekt "Schreib deinen Song - Songwriting"!</p>
			<p>
				Diese Webseite wird den Leser von der ursprünglichen Ideenfindung bis hin zum finalen
				Abmischen des Songs führen und reflektieren. Dafür muss nur gescrollt werden. Unten rechts
				ist ein Button, um die Sachen auf dem aktuellen Hintergrund genau an zu schauen! Viel Spaß!
			</p>
		</section>

		<section use:reveal>
			<h2 class="h2 pb-1 md:pb-3">Meine Erwartungen</h2>
			<p>
				Im Vorhinein zur Projektarbeit habe ich gleichzeitig Sorgen und Ängste und Erwartungen zum
				Prozess und Ergebnis des Songwriting-Projekts. Zum einen, ob meine Fähigkeit dafür
				ausreichen würden, und, ob ich mich on den ganzen Möglichkeiten für einen Song
				(Ideen/Genre/Melodie) mit meiner Gruppe für eine entscheiden könnte. Zum anderen hoffe ich
				Spaß in meiner Gruppe daran zu haben. Das ist auch der ursprüngliche Grund warum ich Musik
				im 1. Semester gewählt hatte, für das Songwriting-Projekt. Nichtdestotrotz ist mir das
				Endprodukt auch wichtig, es soll wenigstens Spaß mache sich an zu hören. Das ist mein
				jetziger Anspruch.
			</p>
			<p>
				Insgesamt werden hier zwar einige Sorgen ersichtlich, jedoch wurde eher Positiv auf die
				kommende Projektarbeit geguckt. Inwiefern diese dann lief, ob es Schwierigkeiten gab, und
				würde ich es nochmal machen wollen, erkläre und reflektiere ich im Folgenden.
			</p>
		</section>
		<section use:reveal>
			<h2 class="h2 pb-1 md:pb-3">Gruppen- und Ideenfindung</h2>
			<p>
				Die Gruppenfindung, die nach Themen gehen sollte, ging relativ schnell und unkompliziert.
				Dabei habe ich mich selber nicht, wie man es sollte, auf eine Musikart fokussiert. Das liegt
				daran, dass ich einen sehr weiten Musikgeschmack habe, d.h. dass ich sehr viele
				unterschiedliche Musik von den unterschiedlichsten Genre mag und gerne höre. Wir vier Jungs,
				die ursprünglich einen Song machen wollten, waren von den Ideen des Endproduktes zu
				unterschiedlich. Daher teilten wir uns nochmal auf. Nach einem Gespräch mit meinem Partner
				Hanno, wurde schnell klar wir machen was aus den 80er. Dadurch, dass Hanno Alternative Rock
				bzw. Grunge mag, sind wir dann schließlich auf die Band Nirvana gekommen. In Bild 1 zu
				diesem Unterpunkt ist dabei die Songidee aufgeschrieben, auf die wir uns geeinigt hatten.
			</p>
			<p>
				Zudem hatten wir auch hier direkt ein Trello Board erstellt (siehe Bild 2), um besser im
				Team zu arbeiten und seine vergangene Arbeit nach zu vollziehen. In Retrospektive kann ich
				dies bestätigen, ein Trello Board war für mich zum Nachvollziehen sehr hilfreich. <a
					class="anchor"
					href="https://trello.com/invite/b/66ed638b2b0f9a01a94828e2/ATTI5f11d23bf041faf2445c032565c7a513947B6E0B/musik-12-songwriting"
					>Hier ein Einladungslink</a
				>. Wir haben dabei mit sog. "Labels" die Bearbeitungstage an den Karten hinzugefügt. So gibt
				es mehrere Karten/Unterpunkte, an denen einige Labels und somit auch Längere Zeit dran
				gearbeitet wurde.
			</p>
		</section>
		<section use:reveal>
			<h2 class="h2 pb-1 md:pb-3">Arbeitsphase/Teamarbeit</h2>
			<p>Arbeitsphase = So wie wir gearbeitet haben</p>
		</section>
		<section use:reveal class="space-y-5">
			<div>
				<h2 class="h2 pb-1 md:pb-3">Basis des Songs</h2>
				<p>Die Basis, das Schlagzeug, der Bass und kleinere E-Gitarre Ideen.</p>
			</div>
			<div>
				<h3 class="h3 pb-0.5 md:pb-2">Schlagzeug</h3>
				->> Musikalische Analyse mit Hörbeispielen (coolem Component)
			</div>
			<div>
				<h3 class="h3 pb-0.5 md:pb-2">Bass</h3>
				->> Musikalische Analyse mit Hörbeispielen (coolem Component)
			</div>
		</section>
		<section use:reveal>
			<h2 class="h2 pb-1 md:pb-3">Aufnahmen</h2>
			<p>Die Aufnahmen</p>
		</section>
		<section use:reveal>
			<h2 class="h2 pb-1 md:pb-3">Nachbearbeitung</h2>
			<p>Das Abmischen und verbessern des Songs</p>
		</section>
	</div>
</Scroller>

<style>
	@keyframes float {
		0% {
			opacity: 0.2;
		}
		30% {
			transform: translateY(0);
			opacity: 0.5;
		}
		50% {
			transform: translateY(-20px);
			opacity: 0.8;
		}
		100% {
			transform: translateY(0);
			opacity: 0.2;
		}
	}

	.music-note {
		animation: float 3s ease-in-out infinite;
	}
</style>
