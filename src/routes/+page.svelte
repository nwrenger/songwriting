<script lang="ts">
	import Scroller from '$lib/components/Scroller.svelte';
	import { reveal } from 'svelte-reveal';
	import { fade, fly, scale } from 'svelte/transition';
	import { Music, Mic, PlayCircle, Headphones, Mouse } from 'lucide-svelte';

	let index: number = $state(0);
	let offset: number = $state(0);
	let progress: number = $state(0);
</script>

<svelte:head>
	<title>Songwriting Portfolio</title>
	<meta
		name="description"
		content="Hi, dies ist mein Songwriting Portfolio für den Song `crazed self`."
	/>
</svelte:head>

<Scroller
	top={0}
	bottom={0.75}
	threshold={0.4}
	bind:index
	bind:offset
	bind:progress
	overviewContent={[
		[],
		['before.jpg'],
		['ideas.jpg', 'trello.png'],
		['songtext-1.jpeg', 'songtext-2.jpeg', 'final-songtext-1.png', 'final-songtext-2.png']
	]}
	pdfContent={[undefined, undefined, undefined, undefined, undefined, 'Schlagzeug.pdf', 'todo.pdf']}
>
	<div slot="background" class="relative h-full max-w-5xl mx-auto">
		<div
			class="absolute top-80 sm:top-60 md:top-54 w-full h-full flex flex-col items-center justify-center space-y-8"
		>
			{#key index}
				<div transition:fade={{ duration: 600 }}>
					{#if index == 0}
						<div
							class="absolute top-20 left-8 music-note text-indigo-400"
							in:fly|global={{ x: -300, duration: 1000 }}
						>
							<Music class="w-12 h-12 md:w-16 md:h-16" />
						</div>
						<div
							class="absolute top-16 right-16 music-note text-purple-400"
							in:fly|global={{ x: 300, duration: 1000 }}
						>
							<Mic class="w-10 h-10 md:w-14 md:h-14" />
						</div>
						<div
							class="absolute bottom-10 left-20 music-note text-yellow-400"
							in:fly|global={{ x: -300, duration: 1000 }}
						>
							<PlayCircle class="w-10 h-10 md:w-14 md:h-14" />
						</div>
						<div
							class="absolute bottom-20 right-12 music-note text-teal-400"
							in:fly|global={{ x: 300, duration: 1000 }}
						>
							<Headphones class="w-12 h-12 md:w-16 md:h-16" />
						</div>
						<div class="absolute" in:scale|global={{ delay: 1600, duration: 600 }}>
							<Mouse class="w-12 h-12 md:w-16 md:h-16 dark:text-gray-500 text-gray-300" />
						</div>
					{:else if index == 1}
						<img
							src="before.jpg"
							alt="before.jpg"
							class="absolute top-14 right-0 w-auto h-32 md:h-52 dark:opacity-20 opacity-30 object-contain shadow-md"
						/>
					{:else if index == 2}
						<img
							src="ideas.jpg"
							alt="ideas.jpg"
							class="absolute top-14 left-0 w-auto h-32 md:h-52 dark:opacity-20 opacity-30 object-contain shadow-md"
						/>
						<img
							src="trello.png"
							alt="trello.png"
							class="absolute top-20 right-0 w-auto h-32 md:h-52 dark:opacity-20 opacity-30 object-contain shadow-md"
						/>
					{:else if index == 3}
						<img
							src="final-songtext-2.png"
							alt="final-songtext-2.png"
							class="absolute top-48 right-12 w-auto h-32 md:h-52 dark:opacity-20 opacity-30 object-contain shadow-md"
						/>
						<img
							src="final-songtext-1.png"
							alt="final-songtext-1.png"
							class="absolute top-0 right-0 w-auto h-32 md:h-52 dark:opacity-20 opacity-30 object-contain shadow-md"
						/>
						<img
							src="songtext-1.jpeg"
							alt="songtext-1.jpeg"
							class="absolute top-32 left-20 w-auto h-32 md:h-52 dark:opacity-20 opacity-30 object-contain shadow-md"
						/>
						<img
							src="songtext-2.jpeg"
							alt="songtext-2.jpeg"
							class="absolute top-[-20px] left-2 w-auto h-32 md:h-52 dark:opacity-20 opacity-30 object-contain shadow-md"
						/>
					{/if}
				</div>
			{/key}
		</div>
	</div>

	<div slot="foreground" class="sr__hide max-w-5xl mx-auto overflow-x-hidden">
		<section use:reveal class="pb-28 pt-8 md:pt-12">
			<h1 class="h1 pb-3 md:pb-5">Songwriting Portfolio</h1>
			<p>Willkommen auf meinem Portfolio zum Projekt „Schreib deinen Song – Songwriting“!</p>
			<p>
				Auf dieser Webseite begleite ich Sie Schritt für Schritt durch den gesamten
				Entstehungsprozess meines Songs – von den ersten Ideen bis hin zum finalen Abmischen. Folgen
				Sie einfach dem Verlauf nach unten, um alle Entwicklungsschritte nachzuvollziehen.
			</p>
			<p>
				Unten rechts befindet sich ein Button (aktuell noch unsichtbar), mit dem Sie die
				Hintergründe genauer betrachten können. Klicken Sie auf das angezeigte Bild, um es in einem
				neuen Tab zu öffnen. Ebenso gibt es unten links einen PDF-Viewer (ebenfalls derzeit
				unsichtbar), der auf die gleiche Weise funktioniert.
			</p>
			<p>
				Außerdem finden Sie in den jeweiligen oberen und unteren Ecken der Bild- und PDF-Viewer ein
				Draghandle, mit dem sich das angezeigte Fenster ganz nach Ihren Wünschen vergrößern oder
				verkleinern lässt. Viel Freude beim Erkunden!
			</p>
		</section>

		<section use:reveal class="py-28">
			<h2 class="h2 pb-1 md:pb-3">Meine Erwartungen</h2>
			<p>
				Im Vorhinein zur Projektarbeit habe ich gleichzeitig Sorgen und Ängste und Erwartungen zum
				Prozess und Ergebnis des Songwriting-Projekts. Zum einen, ob meine Fähigkeit dafür
				ausreichen würden, und, ob ich mich on den ganzen Möglichkeiten für einen Song
				(Ideen/Genre/Melodie) mit meiner Gruppe für eine entscheiden könnte. Zum anderen hoffe ich
				Spaß in meiner Gruppe daran zu haben. Das ist auch der ursprüngliche Grund warum ich Musik
				im 1. Semester gewählt hatte, für das Songwriting-Projekt. Nichtdestotrotz ist mir das
				Endprodukt auch wichtig, es soll wenigstens Spaß mache sich an zu hören. Das ist mein
				jetziger Anspruch. Insgesamt werden hier zwar einige Sorgen ersichtlich, jedoch wurde eher
				Positiv auf die kommende Projektarbeit geguckt (im Vorhinein verfasst, siehe Bild 1).
			</p>
			<p>
				Inwiefern diese dann lief, ob es Schwierigkeiten gab, und würde ich es nochmal machen
				wollen, erkläre und reflektiere ich im Folgenden.
			</p>
		</section>
		<section use:reveal class="py-28">
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
			<br />
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
		<section class="py-28">
			<div use:reveal>
				<h2 class="h2 pb-1 md:pb-3">Teamarbeit und Ablauf</h2>
				<p>
					Unsere Teamarbeit war insgesamt immer sehr produktiv. Man kann den Prozess auch gut mit
					dem englischen Ausdruck "Try and Error" beschreiben. Wir haben viel ausprobiert und sind
					so einem auch von uns umsetzbaren Endprodukt immer näher gekommen. Dabei haben wir auch
					viele Ideen verworfen, wir müssen ja nicht 5, sondern einen Song schreiben. Auch war es
					für uns Anfangs schwierig Rhythmen und Melodien zu finden, die zusammenpassten und nach
					unserem subjektiven Eindruck auch gut klangen.
				</p>
				<br />
				<p>
					Wir haben direkt mit der Basis des Songs begonnen, den Instrumenten. Im Vergleich zu
					andren Gruppen, welche erst angefangen hatten ihren Songtext zu schreiben, haben wir
					direkt damit angefangen Songs der Band "Nirvana" anzuhören und ein Schlagzeug und Bass mit
					Midi Werkzeugen von GarageBand zu erstellen. Dies war viel leichter als einen Songtext aus
					dem Nichts zu schreiben, trotzdem hätte man sich da retrospektiv schon auf ein generelles
					Thema einigen können, um den Song in eine gewisse Richtung zu bewegen.
				</p>
				<br />
			</div>
			<div use:reveal>
				<p>
					Wir saßen dabei anfangs, als man noch dachte, man hätte viel Zeit, am Midi-Keyboard und
					hat viel ausprobiert. Ab ca. Ende November/Anfang Dezember, als das generelle Gerüst des
					Songs bestehend aus Schlagzeug, Bass und E-Gitarre (zu dem Zeitpunkt noch alles mit
					Midi-Instrumenten umgesetzt) stand, teilten wir uns immer mehr auf. Z.B. beim Schreiben
					des Songtextes schrieb jeder einzeln sich Texte beim auf und ab Hören des "Gerüsts" auf
					(siehe Bild 1-2, Bild 3-4 ist der finale Text mit Titel). Nach ca. 20 minütigen
					Intervallen tauschten wir uns aus. Der Gedanke war, dass wir schnell einen Text brauchten,
					wobei die jeweilige Einzelarbeit sich als eine sehr gute Methode herausstellte. Das
					Resultat war ein, auch Nirvana typisch, eher "verrückter" Text innerhalb von 90 Minuten (2
					getrennten Stunden), siehe z.B. "Paper Cuts", wobei über Missbrauch und mentale Qualen
					gesungen wird. Dieser wurde zwar noch 2-3 mal angepasst, aber der generelle Inhalt war
					vergleichsweise zu anderen Gruppen schnell fertig. Alleinig der Name des Songs, das
					Coverbild und das Hinzufügen einer weiteren Strophe von Hanno hat diesen Teil in die Länge
					gezogen. Ab diesen Zeitpunkt waren wir schon mitten in den Aufnahmen und diese Sachen
					wurden in Stunden, wo keine Aufnahmen gemacht wurde, erledigt.
				</p>
				<br />
			</div>
			<div use:reveal>
				<p>
					In diesen Einzelarbeitsphasen war Rückmeldung an die jeweilig andere Person seines
					Fortschritts ein a und o, wir wollten etwas erschaffen, was uns beiden gefällt, nicht NUR
					Hanno oder NUR mir. Das hat zum Anderen auch, obwohl wir nun meistens getrennt an etwas
					arbeiteten, uns manchmal verlangsamt. Auch, weil wir an dem Punkt auch noch nach unserer
					"Try and Error" arbeitsweise nachgingen.
				</p>
				<br />
				<p>
					So ist es gekommen, dass wir die letzten Aufnahmen und das Abmischen bei mir zu Hause,
					einem Tag vor Abgabe, machen mussten. Ein strikterer Zeitplan und mehr Geradlinigkeit
					hätte dies verhindert.
				</p>
			</div>
		</section>
		<section use:reveal class="pt-28 pb-5">
			<h2 class="h2 pb-1 md:pb-3">Analyse</h2>
			<p>
				Ich habe überwiegend Schlagzeug- und Bassparts komponiert, während Hanno vor allem für die
				E-Gitarre und den Songtext verantwortlich war. Aus diesem Grund werde ich im Folgenden nur
				diese beiden Elemente – die bereits beschriebene Grundstruktur – musikalisch analysieren.
			</p>
		</section>
		<section use:reveal class="pb-5">
			<h3 class="h3 pb-0.5 md:pb-2">Schlagzeug</h3>
			<p>
				Unser Song selber ist dabei in einem Tempo von 111 bpm (grüne Markierung), ein typisches
				Tempo bei dem Vergleich zu anderen Nirvana Songs, welche in dem Bereich von 92 bis 138 bpm
				liegen. Dies passt jedoch besser zum Inhalt des Songs. Zudem ist der Song in einem 4/4-Takt
				und G-Dur verfasst. Für das Schlagzeug ist die Tonart irrelevant. Bitte beachten Sie, dass
				die Noten von GarageBand exportiert sind und GarageBand digitale Schlagzeuge mit Notenwerten
				beschreibt.
			</p>

			<p>
				Dieser startet mit einem Intro, welches von Takt 1 bis Takt 2 Zz. 3 aus 8-tel h's, hier eine
				Hi-Hat, besteht.
			</p>

			<br />
			<p>
				Insgesamt wurde sich beim Schlagzeug stark an Nirvana orientiert. Die hauptsächlichen
				Element, wie in Motiv ?, die 8-tel Hi-Hats und (siehe/beschreibe Motivenstruktur) die
				generelle Struktur, sind aus Smells Like Teen Spirit.
			</p>
		</section>
		<section use:reveal class="pb-28">
			<h3 class="h3 pb-0.5 md:pb-2">Bass</h3>
			<p>->> Musikalische Analyse mit Hörbeispielen (coolem Component)</p>
		</section>
		<section use:reveal class="py-28 space-y-5">
			<div>
				<h2 class="h2 pb-1 md:pb-3">Aufnahmen</h2>
				<p>
					<!-- todo -->
				</p>
			</div>
			<div>
				<h3 class="h3 pb-0.5 md:pb-2">E-Gitarre</h3>
				<!-- todo -->
			</div>
			<div>
				<h3 class="h3 pb-0.5 md:pb-2">Gesang</h3>
				<!-- todo -->
			</div>
		</section>
		<section use:reveal class="py-28">
			<h2 class="h2 pb-1 md:pb-3">Nachbearbeitung</h2>
			<p>
				Das Abmischen und verbessern des Songs (schiefer Hanno im Pre-Chorus (-> Schlagzeug),
				Gitarre weniger Overdrive)
			</p>
		</section>
	</div>
</Scroller>

<style>
	@keyframes float {
		0% {
			opacity: 1;
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
			opacity: 1;
		}
	}

	.music-note {
		animation: float 3s ease-in-out infinite;
		animation-delay: 1.8s;
	}
</style>
