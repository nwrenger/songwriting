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
	pictures={new Map([
		[
			1, // Meine Erwartungen
			['erwartungen.jpg']
		],
		[
			2, // Gruppen- und Ideenfindung
			['ideen.jpg', 'trello.png']
		],
		[
			3, // Teamarbeit und Ablauf
			['songtext-1.jpeg', 'songtext-2.jpeg', 'finaler-songtext-1.png', 'finaler-songtext-2.png']
		],
		[
			4, // Aufbau
			['aufbau.png']
		]
	])}
	score={new Map([
		[
			6, // Analyse - Schlagzeug
			{
				url: 'schlagzeug/noten.pdf',
				songSnippets: [
					{ name: 'Intro', url: 'schlagzeug/intro.mp3' },
					{ name: 'Motive a', url: 'schlagzeug/motiv a.mp3' },
					{ name: "Motive a'", url: "schlagzeug/motiv a'.mp3" },
					{ name: 'Motive b', url: 'schlagzeug/motiv b.mp3' },
					{ name: 'Motive c', url: 'schlagzeug/motiv c.mp3' },
					{ name: 'Motive d', url: 'schlagzeug/motiv d.mp3' },
					{ name: 'Motive e', url: 'schlagzeug/motiv e.mp3' },
					{ name: "Motive e'", url: "schlagzeug/motiv e'.mp3" },
					{ name: 'Motive f', url: 'schlagzeug/motiv f.mp3' },
					{ name: "Motive f'", url: "schlagzeug/motiv f'.mp3" }
				]
			}
		]
		// todo!
		// [
		// 	6, // Analyse - Bass
		// 	{ url: '', songSnippets: [] }
		// ]
	])}
>
	<div slot="background" class="relative h-full max-w-5xl mx-auto">
		<div
			class="absolute top-80 sm:top-60 md:top-54 w-full h-full flex flex-col items-center justify-center space-y-8"
		>
			{#if index == 0}
				<div transition:fade={{ duration: 600 }}>
					<div
						class="absolute top-20 left-8 music-note opacity-50 text-indigo-400"
						in:fly|global={{ x: -300, duration: 1000 }}
					>
						<Music class="w-12 h-12 md:w-16 md:h-16" />
					</div>
					<div
						class="absolute top-16 right-16 music-note opacity-50 text-purple-400"
						in:fly|global={{ x: 300, duration: 1000 }}
					>
						<Mic class="w-10 h-10 md:w-14 md:h-14" />
					</div>
					<div
						class="absolute bottom-10 left-20 music-note opacity-50 text-yellow-400"
						in:fly|global={{ x: -300, duration: 1000 }}
					>
						<PlayCircle class="w-10 h-10 md:w-14 md:h-14" />
					</div>
					<div
						class="absolute bottom-20 right-12 music-note opacity-50 text-teal-400"
						in:fly|global={{ x: 300, duration: 1000 }}
					>
						<Headphones class="w-12 h-12 md:w-16 md:h-16" />
					</div>
					<div
						class="absolute inset-0 flex items-center justify-center"
						in:scale|global={{ delay: 1600, duration: 600 }}
					>
						<Mouse class="w-12 h-12 md:w-16 md:h-16 dark:text-gray-500 text-gray-300" />
					</div>
				</div>
			{/if}
		</div>
	</div>

	<div slot="foreground" class="sr__hide max-w-5xl mx-auto overflow-x-hidden">
		<section class="pb-14 pt-8 md:pt-12">
			<h1 class="h1 pb-3 md:pb-5">Songwriting Portfolio</h1>
			<p>Willkommen auf meinem Portfolio zum Projekt „Schreib deinen Song – Songwriting“!</p>
			<p>
				Auf dieser Webseite begleite ich Sie Schritt für Schritt durch den gesamten
				Entstehungsprozess meines Songs – von den ersten Ideen bis hin zum finalen Abmischen. Folgen
				Sie einfach dem Verlauf nach unten, um alle Entwicklungsschritte nachzuvollziehen.
			</p>
			<p>
				Unten rechts befindet sich eine Bilderübersicht (derzeit unsichtbar). Klicken Sie auf das
				angezeigte Bild, um es in einem neuen Tab zu öffnen. Sie können die Bilderübersicht auch
				ausblenden, indem Sie auf den Button mit dem durchgestrichenen Auge klicken. Ebenso gibt es
				unten links einen Notenübersicht (ebenfalls derzeit unsichtbar), der auf die gleiche Weise
				funktioniert. Nur können Sie in der Notenübersicht auch die einzelnen Motive anhören.
			</p>
			<p>
				Außerdem finden Sie in den jeweiligen oberen Ecken der Bild- und Notenübersicht eine
				andersfarbige Fläche, mit dem sich das angezeigte Fenster ganz nach Ihren Wünschen
				vergrößern oder verkleinern lässt. Viel Freude beim Erkunden!
			</p>
		</section>

		<section class="py-14">
			<h2 class="h2 pb-1 md:pb-3">Meine Erwartungen</h2>
			<p>
				Im Vorhinein zur Projektarbeit habe ich gleichzeitig Sorgen und Ängste und Erwartungen zum
				Prozess und Ergebnis des Songwriting-Projekts. Zum einen, ob meine Fähigkeit dafür
				ausreichen würden, und, ob ich mich on den ganzen Möglichkeiten für einen Song
				(Ideen/Genre/Melodie) mit meiner Gruppe für eine entscheiden könnte. Zum anderen hoffe ich
				Spaß in meiner Gruppe daran zu haben. Das ist auch der ursprüngliche Grund warum ich Musik
				im 1. Semester gewählt hatte, für das Songwriting-Projekt. Nichtsdestotrotz ist mir das
				Endprodukt auch wichtig, es soll wenigstens Spaß mache sich an zu hören. Das ist mein
				jetziger Anspruch. Insgesamt werden hier zwar einige Sorgen ersichtlich, jedoch wurde eher
				Positiv auf die kommende Projektarbeit geguckt (im Vorhinein verfasst, siehe Bild 1).
			</p>
			<p>
				Inwiefern diese dann lief, ob es Schwierigkeiten gab, und würde ich es nochmal machen
				wollen, erkläre und reflektiere ich im Folgenden.
			</p>
		</section>
		<section class="py-14">
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
		<section class="py-14">
			<h2 class="h2 pb-1 md:pb-3">Teamarbeit und Ablauf</h2>
			<p>
				Unsere Teamarbeit war insgesamt immer sehr produktiv. Man kann den Prozess auch gut mit dem
				englischen Ausdruck "Try and Error" beschreiben. Wir haben viel ausprobiert und sind so
				einem auch von uns umsetzbaren Endprodukt immer näher gekommen. Dabei haben wir auch viele
				Ideen verworfen, wir müssen ja nicht 5, sondern einen Song schreiben. Auch war es für uns
				Anfangs schwierig Rhythmen und Melodien zu finden, die zusammenpassten und nach unserem
				subjektiven Eindruck auch gut klangen.
			</p>
			<br />
			<p>
				Wir haben direkt mit der Basis des Songs begonnen, den Instrumenten. Im Vergleich zu andren
				Gruppen, welche erst angefangen hatten ihren Songtext zu schreiben, haben wir direkt damit
				angefangen Songs der Band "Nirvana" anzuhören und ein Schlagzeug und Bass mit Midi
				Werkzeugen von GarageBand zu erstellen. Dies war viel leichter als einen Songtext aus dem
				Nichts zu schreiben, trotzdem hätte man sich da retrospektiv schon auf ein generelles Thema
				einigen können, um den Song in eine gewisse Richtung zu bewegen.
			</p>
			<br />
			<p>
				Wir saßen dabei anfangs, als man noch dachte, man hätte viel Zeit, am Midi-Keyboard und hat
				viel ausprobiert. Ab ca. Ende November/Anfang Dezember, als das generelle Gerüst des Songs
				bestehend aus Schlagzeug, Bass und E-Gitarre (zu dem Zeitpunkt noch alles mit
				Midi-Instrumenten umgesetzt) stand, teilten wir uns immer mehr auf. Z.B. beim Schreiben des
				Songtextes schrieb jeder einzeln sich Texte beim auf und ab Hören des "Gerüsts" auf (siehe
				Bild 1-2, Bild 3-4 ist der finale Text mit Titel). Nach ca. 20 minütigen Intervallen
				tauschten wir uns aus. Der Gedanke war, dass wir schnell einen Text brauchten, wobei die
				jeweilige Einzelarbeit sich als eine sehr gute Methode herausstellte. Das Resultat war ein,
				auch Nirvana typisch, eher "verrückter" Text innerhalb von 90 Minuten (2 getrennten
				Stunden), siehe z.B. "Paper Cuts", wobei über Missbrauch und mentale Qualen gesungen wird.
				Dieser wurde zwar noch 2-3 mal angepasst, aber der generelle Inhalt war vergleichsweise zu
				anderen Gruppen schnell fertig. Alleinig der Name des Songs, das Coverbild und das
				Hinzufügen einer weiteren Strophe von Hanno hat diesen Teil in die Länge gezogen. Ab diesen
				Zeitpunkt waren wir schon mitten in den Aufnahmen und diese Sachen wurden in Stunden, wo
				keine Aufnahmen gemacht wurde, erledigt.
			</p>
			<br />
			<p>
				In diesen Einzelarbeitsphasen haben wir öfter Rückmeldung an die jeweilig andere Person
				seines Fortschritts gegeben. Wir wollten etwas erschaffen, was uns beiden gefällt. Das hat
				zum Anderen auch, obwohl wir nun meistens getrennt an etwas arbeiteten, uns manchmal
				verlangsamt. Auch, weil wir an dem Punkt auch noch nach unserer "Try and Error" arbeitsweise
				nachgingen.
			</p>
			<br />
			<p>
				So ist es gekommen, dass wir die letzten Aufnahmen und das Abmischen bei mir zu Hause, einem
				Tag vor Abgabe, machen mussten. Ein strikterer Zeitplan und mehr Geradlinigkeit hätte dies
				verhindert.
			</p>
		</section>
		<section class="py-14">
			<h2 class="h2 pb-1 md:pb-3">Aufbau</h2>
			<p>
				Unser Song selber ist dabei in einem Tempo von 111 bpm (grüne Markierung), ein typisches
				Tempo für Nirvana inspirierte Songs. Die sind in dem Bereich von 92 bis 138 bpm geschrieben.
				Zudem ist der Song in einem 4/4-Takt und G-Dur verfasst.
			</p>
			<p class="pb-1 md:pb-3">
				Aufgebaut ist dieser dabei wie folgt (orientieren bitte an Bild 1):
			</p>
			<ul class="list-inside list-disc space-y-2">
				<li>Ab Takt 1: Gitarren Intro</li>
				<li>Ab Takt 5: Bass Intro</li>
				<li>Ab Takt 7: Schlagzeug Intro</li>
				<li>Takt 9-16: Strophe 1</li>
				<li>Takt 17-22: Pre Chorus</li>
				<li>Takt 23-24: Bridge für Pre Chorus und Strophe</li>
				<li>Takt 25-32: Strophe 2</li>
				<li>Takt 33-38: Pre Chorus</li>
				<li>Takt 39-40: Überleitung Pre Chorus zu Chorus</li>
				<li>Takt 41-48: Chorus</li>
				<li>Takt 49-56: Strophe 3</li>
				<li>Takt 57-62: Pre Chorus</li>
				<li>Takt 63-64: Überleitung Pre Chorus zu Chorus</li>
				<li>Takt 65-73: Chorus</li>
				<li>Takt 73-76: Chorus - Schlagzeug Solo</li>
				<li>Takt 77-84: Bridge zwischen Chorusse</li>
				<li>Takt 85-92: Chorus</li>
				<li>Takt 93: Gitarren Outtro</li>
				<li>Takt 93: Schlagzeug Cutoff</li>
				<li>Takt 93-97: Bass Solo</li>
				<li>Takt 98: Bass Cutoff-Ende</li>
			</ul>
			<br />
			<p>
				Mit einem gestaffelten Anfang und Ende, und spezifischen Intros und Outtros wollten wir die
				einzelnen Stimmen hervorheben. Am Anfang die E-Gitarre und das Schlagzeug und am Ende den
				Bass, der eher Struktur gibt und bis dahin nie im Vordergrund stand. Insgesamt wurde das
				Stück mit 98 Takten bzw. 3:28 Minuten länger als Anfänglich antizipiert und nur möglich, da
				wir viel mit Wiederholungen gearbeitet haben. Jede Strophe, Pre Chorus und Chorus waren
				Instrumental 1 zu 1 gleich und wurden kopiert, nur die Bridges, Überleitungen und
				Intros/Outtros waren unterschiedlich.
			</p>
		</section>
		<section class="pt-14 pb-5">
			<h2 class="h2 pb-1 md:pb-3">Analyse</h2>
			<p>
				Ich habe überwiegend Schlagzeug- und Bassparts komponiert, während Hanno vor allem für die
				E-Gitarre und den Songtext verantwortlich war. Aus diesem Grund werde ich im Folgenden nur
				diese beiden Elemente – die bereits beschriebene Grundstruktur – musikalisch analysieren.
			</p>
		</section>
		<section class="pb-5">
			<h3 class="h3 pb-0.5 md:pb-2">Schlagzeug</h3>
			<p>
				Für das Schlagzeug ist die Tonart irrelevant. Bitte beachten Sie, dass die Noten von
				GarageBand exportiert sind und GarageBand digitale Schlagzeuge mit Notenwerten beschreibt.
			</p>
			<br />
			<p>
				Das Intro (dunkelgrüne Markierung) zeichnet sich durch durchgehende 8tel Hi-Hats (h) aus. In
				Takt 8, Zählzeit 3 (Zz. 3), wird dieses Muster durch eine punktierte 32tel Snare Drum (D)
				ergänzt. Im Anschluss folgt eine 64tel Tom (C), bevor in Zz. 3,5 eine 16tel Hi-Hat erklingt.
				Diese wird anschließend von einer Snare Drum in Zz. 4 abgelöst, die von zwei Toms umspielt
				wird: einer 16tel Tom in Zz. 3,75 und einer 8tel Tom in Zz. 4,5.
			</p>
			<br />
			<p>
				Das aufgestellte Pattern von durchgehend 8tel Hi-Hats und teilweise durchgehenden 8tel Toms
				mit zwei Umspielungen von Achtel Snare Drums in Zz. 2 und 4, wie im Intro in Zz. 4
				eingeleitet, geht hier in Takt 9 weiter und bildet das Motiv a (rote Markierung), wobei das
				Intro einleitend für Motiv a wirkt, was auch der angestrebte Effekt war. In bspw. Takt 13
				ist dabei eine Variation von Motiv a, Motiv a' (rote Markierung), zu sehen. In Zz 4,5 wird
				dafür die ungespielte Tom mit einer 32tel Snare Drum wiederholt und in Zz. 4,75 verfrüht auf
				eine 64tel Snare Drum zurückgeführt. Diese Variation soll das eher monotone Schlagzeug
				leicht spannender machen. Motiv a und a' wurden insgesamt bei den jew. Strophen verwendet.
				Dafür wurden hauptsächlich die Motive hintereinander wiederholt, Motiv a' weit weniger als
				Motiv a.
			</p>
			<br />
			<p>
				Darauf folgt Motiv b (blaue Markierung) in Takt 17-18 ist ein 2-Takter und wiederholt im 1.
				Takt des Motivs Motiv a und im 2. Takt eine starke Variation von Motiv a. Hier bleibt die
				durchgehende 8tel Hi-Hat bestehen, während die Tom-Pattern in Zz. 2,75 und 3,5 durch eine
				Snare-Betonung in den Vordergrund treten. Diese Veränderung hebt Motiv b als eigenständigen
				Abschnitt hervor. Die Zwischenspiele in Takt 2 des Motivs sind in den Gesangspausen, womit
				das Schlagzeug als rhythmisch und komplex hervorhebt werden sollte. Dieses Motiv wird im
				Pre-Chorus genutzt und kommt im Anschluss von Strophen.
			</p>
			<br />
			<p>
				Motiv c (violette Markierung) in Takt 23-24 folgt in den Teilen zwischen Motiv b und a als
				Bridge für Pre Chorus und Strophe 2 des Songs und bricht mit der Struktur der vorherigen
				Motive. Statt durchgehenden 8tel Hi-Hats wird ein langsamerer Rhythmus mit punktierten
				Viertelnoten auf der Hi-Hat gespielt. Dies wird ergänzt durch synkopische Snare- und
				Tom-Patterns, die für eine kontrastierende Dynamik sorgen. Ziel dieser Gestaltung war es,
				den Spannungsbogen des Songs zu verstärken und den Übergang zurück zu den Strophen motivisch
				vorzubereiten.
			</p>
			<br />
			<p>
				Nach Strophe 2, bzw. Motiv a, und Pre-Chorus, bzw. Motiv b, folgt in Takt 39-40 Motiv d
				(helllila Markierung). In Takt 1 des Motivs ist, wie auch in Motiv b, Motiv a vorhanden.
				Eine aufbauende/Crescendo-artige Dynamik wird durch zwei gleichzeitig spielenden Toms in
				Takt 2 des Motivs erzeugt, siehe Zz. 1, 2, 3 und 4. Dies soll den Hörer auf den kommenden
				Chorus vorbereiten - vom Pre Chorus zum Chorus überzuleiten - und den Spannungsbogen des
				Songs verstärken.
			</p>
			<br />

			<p>
				Im darauffolgenden Chorus, dargestellt durch Motiv e (orangene Markierung), erreicht der
				Song einen bis jetzt einen unerreichten Höhepunkt. Die Schlagzeugbegleitung wechselt zu
				einem kraftvollen und eingängigen Rhythmus. Die generelle Struktur aus Motiv a bleibt in
				Takt 1 bestehen, nur wird Zz. 1 ein Crash (a) hinzugefügt und in Zz. 2 anstatt einem 8tel
				Tom zwei 16tel Tom gespielt. Takt 2 beginnt in Zz. 1 auch auf einem Crash und Hi-Hat, nur
				wird die Snare-Drum mit einer darauffolgenden 16tel Tom in Zz. 1,75 umspielt. Insgesamt eine
				starke Variation von a Motiven hintereinander. Dieses Motiv wird im Chorus weiter wiederholt
				und soll diesen hervorheben und dem Hörer einen einprägsamen und mitreißenden Abschnitt
				bieten.
			</p>
			<br />
			<p>
				Nach einer weiteren Strophe, Strophe 3, und einem Pre Chorus und Chorus folgt in Takt 73-74
				Motiv e' (orangene Markierung), einer Variation von Motiv e, wobei der Crash von Zz. 1 zu
				jeder vollen Zz. hinzugefügt wurde. Dieses Motiv wird ein weiteres Mal wiederholt und bildet
				den energischen Höhepunkt des Songs. Zudem wird hier nicht Gesungen, was dies noch mehr
				verstärken sollte.
			</p>
			<br />

			<p>
				Auf diesen Höhepunkt folgt eine Bridge mit Motiv f (lila Markierung), welche sich rhythmisch
				in vollem Maße von den anderen Motiven abgrenzt. Keine durchgehende 8tel Hi-Hat mehr und ein
				synkopischer Rhythmus bestehend aus einer punktierten 8tel und 16tel Tom. Darauf folgt eine
				8tel Pause und eine gleichzeitiger 8tel aus Ride-Becken (c) und einer Snare Drum. In Zz. 3
				und 4 wiederholt sich dieser Rhythmus. Hier wird weiterhin etwas ähnliches zum Crash
				verwendet, um die Spannung aufgebaut durch Motiv e' nicht komplett zu verlieren.
			</p>
			<br />
			<p>
				Um wie bei Motiv a' das Hauptmotiv der aktuellen Sektion zu variieren, wurde in Takt 79 und
				83 eine Variation von Motiv f, Motiv f', (lila Markierung) verwendet. Einzig Zz. 1 wurde
				verändert, indem die punktierte 8tel Hi-Hat in eine 16tel und 8tel Hi-Hat auf geteilt wurde.
				Auch spielt in Zz. 1,75 nicht nur die Tom, sondern auch die in der im Chorus verwendete
				Crash.
			</p>
			<br />

			<p>
				Nach der Bridge folgt ein weitere Chorus, nur aus Motiv e Wiederholungen, und der Song
				endet.
			</p>
			<br />

			<p>
				Insgesamt wurde sich beim Schlagzeug stark an Nirvana orientiert. Die hauptsächlichen
				Element, wie in Motiv a/b/c/d/e, die 8-tel Hi-Hats, und die Idee für Motiv e und e', die
				Crash auf die Ganzen und dann 4tel zu legen, sind aus Smells Like Teen Spirit. Der Rest ist
				durch eigenes komponieren bzw. ausprobieren entstanden. Im Nachhinein betrachtet wäre es
				eine gute Idee gewesen nach Grundstrukturen des Schlagzeugs im Grunge, Rock der 80er und
				Alternative Rock zu orientieren, da so das Schlagzeug weniger Monoton und spannender
				geworden wäre. Der Song würde auch besser zur ursprünglich angestrebten Vorlage, Nirvana,
				passen.
			</p>
		</section>
		<section class="pb-14">
			<h3 class="h3 pb-0.5 md:pb-2">Bass</h3>
			<p>
				Der Bass war hingegen um einiges simpler.
				<!-- todo: 2 Motive beschreiben, Grundton der jew. Harmonie, außer 4. Ton (siehe Harmonie),  -->
			</p>
		</section>
		<section class="py-14 space-y-5">
			<div>
				<h2 class="h2 pb-1 md:pb-3">Aufnahmen</h2>
				<p>
					<!-- Generelle Vorgehensweise -->
				</p>
			</div>
			<div>
				<h3 class="h3 pb-0.5 md:pb-2">E-Gitarre</h3>
				<!-- Gut/Schlecht? -> Meine Sicht als Producer, Hanno hat gespielt, Ideen on the fly -->
			</div>
			<div>
				<h3 class="h3 pb-0.5 md:pb-2">Gesang</h3>
				<!-- Gut/Schlecht? -> Meine Sicht als Producer und Sänger, Ideen on the fly -->
			</div>
		</section>
		<section class="py-14">
			<h2 class="h2 pb-1 md:pb-3">Nachbearbeitung</h2>
			<p>Stimme (-> Pitch Correction, Hall), Lautstärke Variationen</p>
			<p>
				Verbessern des Songs (schiefer Hanno im Pre-Chorus (-> Schlagzeug), Gitarre weniger
				Overdrive,)
			</p>
		</section>
		<section class="py-14">
			<h2 class="h2 pb-1 md:pb-3">Endprodukt</h2>
			<!-- todo: put song here -->
		</section>
	</div>
</Scroller>

<style>
	@keyframes float {
		0% {
			opacity: 0.5;
		}
		30% {
			transform: translateY(0);
			opacity: 0.5;
		}
		50% {
			transform: translateY(-20px);
			opacity: 0.65;
		}
		100% {
			transform: translateY(0);
			opacity: 0.5;
		}
	}

	.music-note {
		animation: float 3s ease-in-out infinite;
		animation-delay: 1.8s;
	}
</style>
