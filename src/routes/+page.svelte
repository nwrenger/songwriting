<script lang="ts">
	import Scroller from '$lib/components/Scroller.svelte';
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
			['erwartungen.webp']
		],
		[
			2, // Gruppen- und Ideenfindung
			['ideen.webp', 'trello.webp']
		],
		[
			3, // Teamarbeit und Ablauf
			['songtext-1.webp', 'songtext-2.webp', 'finaler-songtext-1.webp', 'finaler-songtext-2.webp']
		],
		[
			4, // Aufbau
			['aufbau.webp']
		],
		[
			8, // Aufnahme
			['aufnahme-1.webp', 'aufnahme-2.webp', 'aufnahme-gitarre.webp', 'aufnahme-stimme.webp']
		],
		[
			9, // Nachbearbeitung
			['amp.webp', 'pitch.webp', 'lautstaerke.webp', 'overdrive.webp']
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
					{ name: 'Motive b mit Gesang', url: 'schlagzeug/motiv b mit gesang.mp3' },
					{ name: 'Motive c', url: 'schlagzeug/motiv c.mp3' },
					{ name: 'Motive d', url: 'schlagzeug/motiv d.mp3' },
					{ name: 'Motive e', url: 'schlagzeug/motiv e.mp3' },
					{ name: "Motive e'", url: "schlagzeug/motiv e'.mp3" },
					{ name: 'Motive f', url: 'schlagzeug/motiv f.mp3' },
					{ name: "Motive f'", url: "schlagzeug/motiv f'.mp3" }
				]
			}
		],
		[
			7, // Analyse - Bass
			{
				url: 'bass/noten.pdf',
				songSnippets: [
					{ name: 'Motiv a', url: 'bass/motiv a.mp3' },
					{ name: 'Motiv a mit Gitarre', url: 'bass/motiv a mit gitarre.mp3' },
					{ name: "Motiv a'", url: "bass/motiv a'.mp3" },
					{ name: "Motiv a' mit Gitarre", url: "bass/motiv a' mit gitarre.mp3" }
				]
			}
		]
	])}
>
	<div slot="background" class="relative h-full max-w-5xl mx-auto">
		<div transition:fade={{ duration: 600 }}>
			{#if index == 0}
				<div
					class="absolute top-80 sm:top-60 md:top-54 w-full h-full flex flex-col items-center justify-center space-y-8"
				>
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
			<p>
				Willkommen auf meinem Portfolio zum Projekt „Schreib deinen Song – Songwriting“! Auf dieser
				Webseite begleite ich Sie Schritt für Schritt durch den gesamten Entstehungsprozess meines
				Songs – von den ersten Ideen hin zum finalen Abmischen. Folgen Sie einfach dem Verlauf nach
				unten, um alle Entwicklungsschritte nachzuvollziehen.
			</p>
			<br />
			<p>
				Unten rechts befindet sich eine Bilderübersicht (derzeit unsichtbar). Klicken Sie auf das
				angezeigte Bild, um es in einem neuen Tab zu öffnen. Sie können die Bilderübersicht auch
				ausblenden, indem Sie auf den Button mit dem durchgestrichenen Auge klicken. Ebenso gibt es
				unten links einen Notenübersicht (ebenfalls derzeit unsichtbar), der auf die gleiche Weise
				funktioniert. Nur können Sie in der Notenübersicht auch die einzelnen Motive anhören.
			</p>
			<br />
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
				Prozess und Ergebnis des Songwriting-Projekts. Zum einen, ob meine Fähigkeiten dafür
				ausreichen würden, und ob ich mich in den ganzen Möglichkeiten für einen Song
				(Ideen/Genre/Melodie) mit meiner Gruppe entscheiden könnte. Zum anderen hoffe ich Spaß in
				meiner Gruppe daran zu haben. Das ist auch der ursprüngliche Grund, warum ich Musik im 1.
				Semester gewählt hatte, für das Songwriting-Projekt. Nichtsdestotrotz ist mir das Endprodukt
				auch wichtig, es soll wenigstens Spaß machen es sich anzuhören. Das ist mein jetziger
				Anspruch. Insgesamt werden hier zwar einige Sorgen ersichtlich, jedoch wurde eher positiv
				auf die kommende Projektarbeit geguckt (im Vorhinein verfasst, siehe Bild 1).
			</p>
			<br />
			<p>
				Inwiefern diese dann lief, ob es Schwierigkeiten gab, und würde ich es nochmal machen
				wollen, erkläre und reflektiere ich im Folgenden.
			</p>
		</section>
		<section class="py-14">
			<h2 class="h2 pb-1 md:pb-3">Gruppen- und Ideenfindung</h2>
			<p>
				Die Gruppenfindung, die nach Themen gehen sollte, ging relativ schnell und unkompliziert.
				Dabei habe ich mich selbst nicht, wie man es sollte, auf eine Musikart fokussiert. Das liegt
				daran, dass ich einen sehr weiten Musikgeschmack habe, d.h. dass ich sehr viele
				unterschiedliche Musik von den unterschiedlichsten Genres mag und gerne höre. Wir vier
				Jungs, die ursprünglich einen Song machen wollten, waren von den Ideen des Endprodukts zu
				unterschiedlich. Daher teilten wir uns nochmal auf. Nach einem Gespräch mit meinem Partner
				Hanno wurde schnell klar, wir machen was aus den 80er. Dadurch, dass Hanno Alternative Rock
				bzw. Grunge mag, sind wir dann auf die Band Nirvana gekommen. In Bild 1 dabei die konkrete
				Songidee aufgeschrieben, auf die wir uns geeinigt hatten.
			</p>
			<br />
			<p>
				Zudem hatten wir auch hier direkt ein Trello Board erstellt (siehe Bild 2), um besser im
				Team zu arbeiten und seine vergangene Arbeit nachzuvollziehen. In Retrospektive kann ich
				dies bestätigen, ein Trello Board war für mich zum Nachvollziehen sehr hilfreich. <a
					class="anchor"
					href="https://trello.com/invite/b/66ed638b2b0f9a01a94828e2/ATTI5f11d23bf041faf2445c032565c7a513947B6E0B/musik-12-songwriting"
					>Hier ein Einladungslink</a
				>. Wir haben dabei mit sog. "Labels" die Bearbeitungstage an den Karten hinzugefügt. So gibt
				es mehrere Karten/Unterpunkte, an denen einige Labels und somit auch längere Zeit dran
				gearbeitet wurde.
			</p>
		</section>
		<section class="py-14">
			<h2 class="h2 pb-1 md:pb-3">Teamarbeit und Ablauf</h2>
			<p>
				Unsere Teamarbeit war insgesamt immer sehr produktiv. Man kann den Prozess auch gut mit dem
				englischen Ausdruck "Trial-and-Error" beschreiben. Wir haben viel ausprobiert und sind so
				einem auch von uns umsetzbaren Endprodukt immer näher gekommen. Dabei haben wir auch viele
				Ideen verworfen, wir müssen ja nicht 5, sondern einen Song schreiben. Auch war es für uns
				Anfangs schwierig Rhythmen und Melodien zu finden, die zusammenpassten und nach unserem
				subjektiven Eindruck auch gut klangen.
			</p>
			<br />
			<p>
				Wir haben direkt mit der Basis des Songs begonnen, den Instrumenten. Im Vergleich zu andren
				Gruppen, welche erst angefangen hatten ihren Songtext zu schreiben, haben wir direkt damit
				angefangen Songs der Band "Nirvana" anzuhören und ein Schlagzeug und Bass mit MIDI
				Werkzeugen von GarageBand zu erstellen. Dies war viel leichter als einen Songtext aus dem
				Nichts zu schreiben, trotzdem hätte man sich da retrospektiv schon auf ein generelles Thema
				einigen können, um den Song in eine gewisse Richtung zu bewegen.
			</p>
			<br />
			<p>
				Ab ca. Ende November/Anfang Dezember, als das generelle Gerüst des Songs bestehend aus
				Schlagzeug, Bass und E-Gitarre (zu dem Zeitpunkt noch alles mit MIDI-Instrumenten umgesetzt)
				stand, teilten wir uns immer mehr auf. Z.B. beim Schreiben des Songtextes schrieb jeder
				einzeln sich Texte beim auf und ab Hören des "Gerüsts" auf (siehe Bild 1-2, Bild 3-4 ist der
				finale Text mit Titel). Nach ca. 20 minütigen Intervallen tauschten wir uns aus. Der Gedanke
				war, dass wir schnell einen Text benötigen, wobei die jeweilige Einzelarbeit sich als eine
				optimale Methode herausstellte. Das Resultat war ein, auch Nirvana typisch, eher
				"verrückter" Text innerhalb von 90 Minuten (2 getrennten Stunden), siehe z.B. "Paper Cuts",
				wobei über Missbrauch und mentale Qualen gesungen wird. Dieser wurde zwar noch 2-3 mal
				angepasst, aber der generelle Inhalt war vergleichsweise zu anderen Gruppen schnell fertig.
				Alleinig der Name des Songs, das Coverbild und das Hinzufügen einer weiteren Strophe hat
				diesen Teil in die Länge gezogen. Ab diesen Zeitpunkt waren wir schon mitten in den
				Aufnahmen und diese Sachen wurden in Stunden, wo keine Aufnahmen gemacht wurde, erledigt.
			</p>
			<br />
			<p>
				In diesen Einzelarbeitsphasen haben wir öfter Rückmeldung an die jeweils andere Person
				seines Fortschritts gegeben. Wir wollten etwas erschaffen, was uns beiden gefällt. Das hat
				zum Anderen auch, obwohl wir nun meistens getrennt an etwas arbeiteten, uns manchmal
				verlangsamt. Auch, weil wir an dem Punkt auch noch nach unserer "Trial-and-Error"
				Arbeitsweise nachgingen.
			</p>
			<br />
			<p>
				So ist es gekommen, dass wir die letzte Aufnahme und das Abmischen bei mir zu Hause, einem
				Tag vor Abgabe, machen mussten. Ein strikterer Zeitplan und mehr Geradlinigkeit hätte dies
				verhindert.
			</p>
		</section>
		<section class="py-14">
			<h2 class="h2 pb-1 md:pb-3" id="aufbau">Aufbau</h2>
			<p>
				Unser Song selbst ist dabei in einem Tempo von 111 BPM geschrieben, ein typisches Tempo für
				Nirvana inspirierte Songs. Die sind in dem Bereich von 92 bis 138 BPM. Zudem ist der Song in
				einem 4/4-Takt und G-Dur verfasst. Dies mit einer Melodiefolge von G-Dur (Tonika), e-Moll
				(Tonikaparallele), a-Moll (Subdominanten-Parallele) und C-Dur (Subdominante) in Strophen und
				im Pre Chorus. Und im Chorus mit einer simpleren Folge von G-Dur (Tonika) und E-Moll
				(Tonikaparallele).
			</p>
			<p class="pb-1 md:pb-3">
				Aufgebaut ist dieser dabei wie in Bild 1 im Arrangement ersichtlich. Dabei gibt es einige
				Einzelheiten, die dort nicht eingetragen werden konnten:
			</p>
			<ul class="list-inside list-disc space-y-2">
				<li>
					Intro Takt 1-8: Ab Takt 1 Gitarren Solo, ab Takt 5 Bass kommt dazu, ab Takt 7 Schlagzeug
					Intro
				</li>
				<li>Takt 23-24: Bridge für Pre Chorus und Strophe</li>
				<li>Takt 39-40: Überleitung Pre Chorus zu Chorus</li>
				<li>Takt 63-64: Überleitung Pre Chorus zu Chorus</li>
				<li>Takt 73-76: Chorus mit Instrumenten Solo</li>
				<li>Takt 77-84: Bridge zwischen Chorusse</li>
				<li>Outro Takt 93: Gitarren Outro, Schlagzeug Cutoff, Bass Solo bis Takt 97</li>
			</ul>
			<br />
			<p>
				Mit einem gestaffelten Anfang und Ende, und spezifischen Intros und Outros wollten wir die
				einzelnen Stimmen hervorheben. Am Anfang die E-Gitarre und das Schlagzeug und am Ende den
				Bass, der eher Struktur gibt und bis dahin nie im Vordergrund stand. Insgesamt wurde das
				Stück mit 98 Takten bzw. 3:28 Minuten länger als anfänglich antizipiert und nur möglich, da
				wir viel mit Wiederholungen gearbeitet haben. Jede Strophe, Pre Chorus und Chorus waren
				instrumental 1 zu 1 gleich und wurden kopiert, nur die Bridges, Überleitungen und
				Intros/Outros waren unterschiedlich.
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
			<h3 class="h3 pb-0.5 md:pb-2" id="schlagzeug-analyse">Schlagzeug</h3>
			<p>
				Für das Schlagzeug ist die Tonart irrelevant. Bitte beachten Sie, dass die Noten von
				GarageBand exportiert sind und GarageBand digitale Schlagzeuge mit Notenwerten beschreibt.
			</p>
			<br />
			<p>
				Das Intro (dunkelgrün markiert) zeichnet sich durch durchgehende 8-tel Hi-Hats (h) aus. In
				Takt 8, Zählzeit 3 (Zz. 3), wird dieses Muster durch eine punktierte 32tel Snare Drum (D)
				ergänzt. Im Anschluss folgt eine 64tel Tom (C), bevor in Zz. 3,5 eine 16tel Hi-Hat erklingt.
				Diese wird anschließend von einer Snare Drum in Zz. 4 abgelöst, die von zwei Toms umspielt
				wird: einer 16tel Tom in Zz. 3,75 und einer 8-tel Tom in Zz. 4,5.
			</p>
			<br />
			<p>
				Das aufgestellte Pattern von durchgehend 8-tel Hi-Hats und teilweise durchgehenden 8-tel
				Toms mit zwei Umspielungen von Achtel Snare Drums in Zz. 2 und 4, wie im Intro in Zz. 4
				eingeleitet, geht hier in Takt 9 weiter und bildet das Motiv a (rot markiert), wobei das
				Intro einleitend für Motiv a wirken soll. In bspw. Takt 13 ist dabei eine Variation von
				Motiv a, Motiv a' (rot markiert), zu sehen. In Zz 4,5 wird dafür die umspielte Tom mit einer
				32tel Snare Drum wiederholt und in Zz. 4,75 verfrüht auf eine 64tel Snare Drum
				zurückgeführt. Diese Variation soll das eher monotone Schlagzeug leicht spannender machen.
				Motiv a und a' wurden insgesamt bei den jeweiligen Strophen verwendet. Dafür wurden
				hauptsächlich die Motive hintereinander wiederholt, Motiv a' weit weniger als Motiv a.
			</p>
			<br />
			<p>
				Darauf folgt Motiv b (blaue markiert) in Takt 17-18. Dieser ein 2-Takter und wiederholt im
				1. Takt des Motivs Motiv a und im 2. Takt eine starke Variation von Motiv a. Hier bleibt die
				durchgehende 8-tel Hi-Hat bestehen, während die Tom-Pattern in Zz. 2,75 und 3,5 durch eine
				Snare-Betonung in den Vordergrund treten. Diese Veränderung hebt Motiv b als eigenständigen
				Abschnitt hervor. Die Zwischenspiele in Takt 2 des Motivs sind in den Teilen des Gesangs, wo
				ein Ton, das 'ry' von Imaginary, länger gehalten wird. Damit sollte die Aufmerksamkeit durch
				den eher monotonen Rhythmus des Schlagzeugs auf den nächsten Takt erhöht werden. Dieses
				Motiv wird im Pre-Chorus genutzt und kommt im Anschluss von Strophen.
			</p>
			<br />
			<p>
				Motiv c (violett markiert) in Takt 23-24 folgt in den Teilen zwischen Motiv b und a als
				Bridge für Pre Chorus und Strophe 2 des Songs und bricht die Struktur der vorherigen Motive.
				Statt durchgehenden 8-tel Hi-Hats wird ein langsamerer Rhythmus mit punktierten Viertelnoten
				auf der Hi-Hat gespielt. Dies wird ergänzt durch synkopische Snare- und Tom-Patterns, die
				für eine kontrastierende Dynamik sorgen. Ziel dieser Gestaltung war es, den Spannungsbogen
				des Songs zu verstärken und den Übergang zurück zu den Strophen motivisch vorzubereiten.
			</p>
			<br />
			<p>
				Nach Strophe 2 (Motiv a) und Pre-Chorus (Motiv b) folgt in Takt 39-40 Motiv d (helllila
				markiert). In Takt 1 des Motivs ist, wie auch in Motiv b, Motiv a vorhanden. Eine
				aufbauende/Crescendo-artige Dynamik wird durch zwei gleichzeitig spielenden Toms in Takt 2
				des Motivs erzeugt, siehe Zz. 1, 2, 3 und 4. Dies soll den Hörer auf den kommenden Chorus
				vorbereiten - vom Pre Chorus zum Chorus überzuleiten - und den Spannungsbogen des Songs
				verstärken.
			</p>
			<br />

			<p>
				Im darauffolgenden Chorus, dargestellt durch Motiv e (orange markiert), erreicht der Song
				einen bis jetzt einen unerreichten Höhepunkt. Die Schlagzeugbegleitung wechselt zu einem
				kraftvollen und eingängigen Rhythmus. Die generelle Struktur aus Motiv a bleibt in Takt 1
				bestehen, nur wird Zz. 1 ein Crash (a) hinzugefügt und in Zz. 2 anstatt einem 8-tel Tom zwei
				16tel Tom gespielt. Takt 2 beginnt in Zz. 1 auch auf einem Crash und Hi-Hat, nur wird die
				Snare-Drum mit einer darauffolgenden 16tel Tom in Zz. 1,75 umspielt. Insgesamt zwei starke
				Variationen von Motiv a. Dieses Motiv wird im Chorus weiter wiederholt und soll diesen
				hervorheben und dem Hörer einen einprägsamen und mitreißenden Abschnitt bieten.
			</p>
			<br />
			<p>
				Nach der dritten Strophe, dem Pre-Chorus und Chorus folgt in den Takten 73–74 das Motiv e'
				(orange markiert), eine Variation von Motiv e, bei der der Crash jede nun in jedem -4-tel
				zusätzlich gespielt wird. Diese Passage, die ohne Gesang gestaltet ist, rückt die
				Instrumente in den Fokus und bildet den finalen Höhepunkt des Songs. Die Pause im Gesang und
				das instrumentale Solo sollen die Energie und Intensität verstärken, dabei aber auch zum
				Nachdenken über die Wirkung des Inhalts im vorherigen Chorus einladen.
			</p>
			<br />

			<p>
				Auf diesen Höhepunkt folgt eine Bridge mit Motiv f (lila markiert) in Takt 77, welche sich
				rhythmisch in vollem Maße von den anderen Motiven abgrenzt. Keine durchgehende 8-tel Hi-Hat
				mehr und ein synkopischer Rhythmus bestehend aus einer punktierten 8-tel und 16tel Tom.
				Darauf folgt eine 8-tel Pause und eine gleichzeitige 8-tel aus Ride-Becken (c) und einer
				Snare Drum. In Zz. 3 und 4 wiederholt sich dieser Rhythmus. Hier wird weiterhin etwas
				Ähnliches zum Crash durch ein eher leiseres Ride-Becken verwendet, um die Spannung aufgebaut
				durch Motiv e' nicht komplett zu verlieren.
			</p>
			<br />
			<p>
				Um wie bei Motiv a' das Hauptmotiv der aktuellen Sektion zu variieren, wurde in Takt 79 und
				83 eine Variation von Motiv f, Motiv f', (lila markiert) verwendet. Einzig Zz. 1 wurde
				verändert, indem die punktierte 8-tel Hi-Hat in eine 16tel und 8-tel Hi-Hat aufgeteilt
				wurde. Auch spielt in Zz. 1,75 nicht nur die Tom, sondern auch die in der im Chorus
				verwendete Crash.
			</p>
			<br />

			<p>
				Nach der Bridge folgt ein weiterer Chorus, bestehend nur aus Motiv e Wiederholungen, und der
				Song endet nach einem Cutoff des Schlagzeugs in Takt 93 und einem Bass Solo bis Takt 97.
			</p>
			<br />

			<p>
				Insgesamt wurde sich beim Schlagzeug stark an Nirvana orientiert. Die hauptsächlichen
				Element, wie in Motiv a/b/c/d/e, die 8-tel Hi-Hats, und die Idee für Motiv e und e', die
				Crash auf die Ganzen und dann auf die 4-tel zu legen, sind aus Smells Like Teen Spirit. Der
				Rest ist durch eigenes Komponieren bzw. Ausprobieren entstanden. Im Nachhinein betrachtet
				wäre es eine gute Idee gewesen, nach Grundstrukturen des Schlagzeugs im Grunge, Rock der
				80er und Alternative Rock sich zu orientieren, da so das Schlagzeug weniger monoton und
				spannender geworden wäre. Der Song würde auch besser zur ursprünglich angestrebten Vorlage,
				Nirvana, passen.
			</p>
		</section>
		<section class="pb-14">
			<h3 class="h3 pb-0.5 md:pb-2">Bass</h3>
			<p>
				Der Bass ist hingegen deutlich einfacher gehalten. Wie bereits in Motiv a (dunkelgrün
				markiert) in Takt 5 erkennbar, orientiert er sich ausschließlich am jeweiligen Grundton der
				aktuellen Melodie (<a class="anchor" href="#aufbau">siehe Aufbau</a>). Rhythmisch setzt der
				Bass mit einer 4-tel Note ein, gefolgt von einer punktierten 8-tel und einer 16tel. Danach
				folgen eine 16tel Pause, eine weitere punktierte 8-tel Note und schließlich zwei 8-tel.
				Dieser Rhythmus weist durch die Verschiebung der Betonungen synkopische Elemente auf, womit
				die E-Gitarre unterstützt wird.
			</p>
			<br />

			<p>
				Eine melodische Variation davon bildet jedoch Motiv a' (dunkelgrün markiert) in Takt 8.
				Anstatt den Grundton C der Subdominante von G-Dur zu nutzen, wird ein G# verwendet, welcher
				auf den folgenden G-Dur Akkord vorbereiten soll. Wir sind darauf zufällig gestoßen und dabei
				geblieben, da es damit geheimnisvoller und spannender klingt.
			</p>
			<br />

			<p>
				Das Motiv a und seine Variante für den Grundton C (Subdominante), Motiv a', werden
				durchgehend wiederholt und orientieren sich dabei stets an der aktuellen Melodik. Lediglich
				in der Bridge (Takte 77–84) pausiert der Bass, um die Dynamik zu reduzieren.
			</p>
			<br />

			<p>
				Insgesamt arbeitet der Bass unterstützend für die E-Gitarre (siehe Hörbeispiele Bass mit
				E-Gitarre) und steht eher im Hintergrund. Im Nachhinein hätte ich gerne auch noch einen
				komplexeren Bass schreiben wollen. Dies hat aber zeitlich nicht mehr gepasst und deswegen
				sind wir dabei geblieben und haben uns auf die Aufnahmen konzentriert.
			</p>
		</section>
		<section class="py-14 space-y-5">
			<div>
				<h2 class="h2 pb-1 md:pb-3">Aufnahmen</h2>
				<p>
					Unsere Aufnahmen waren strukturiert und produktiv. Mein MacBook war dabei an einem
					Interface angeschlossen (siehe Bild 1-2). Dies musste jeweils für die E-Gitarren und das
					Mikrofon nachjustiert werden. Die E-Gitarre haben wir in der Schule am 22.11., eine Woche
					vor Abgaben, und den Gesang bei mir zu Hause am 30.11., ein Tag vor Abgabe, aufgenommen.
					Diese liefen immer sehr gut, wir hatten dabei den Song in GarageBand so vorbereitet, dass
					man auf die Instrumente direkt singen bzw. spielen konnte. Auch hilfreich waren
					GarageBands Virtual Amps, womit wir die Gitarre aufnehmen konnten und dann im Nachhinein
					Effekte und Pedale hinzufügen konnte (siehe Bild 3). Auch beim Aufnehmen der Stimme hat
					uns die Tuner Funktion (siehe Bild 4) sehr geholfen, so wusste ich bzw. derjenige, der den
					Teil aufnahm, ob der Singende auch gerade singt.
				</p>
				<br />
				<p>
					Jedoch gab es bei beiden Aufnahmen kleinere Probleme bei den Fähigkeiten der jeweiligen
					Person. Die Gitarrenaufnahmen, die wir schon eine halbe Woche vor dem 22.11. begannen,
					waren eher weniger produktiv, da Hanno Schwierigkeiten beim Greifen der Töne hatte. Nach
					einer halben Woche Übung war das aber kein Problem mehr.
				</p>
				<p>
					Auch hat Hanno zwar eine schöne tiefe Stimme, jedoch kann er gar nicht hoch singen. Dieses
					hohe Singen wollten wir bei dem Chorus machen, was dann aber nicht möglich war. Deswegen
					bin ich als zweite Stimme, als sog. Adlips, dazu gekommen.
				</p>
			</div>
		</section>
		<section class="py-14">
			<h2 class="h2 pb-1 md:pb-3">Nachbearbeitung</h2>
			<p>
				Wie schon angesprochen haben wir in der Nachbearbeitung die Gitarre im Chorus und den
				anderen Teilen getrennt und jeweils mit einigen Effekten, wie Hall und Reverb und einer
				spezifischen Verstärkereinstellung, bestückt (siehe Bild 1).
			</p>
			<br />
			<p>
				Auch haben wir auf die Stimme einige Effekte wie Pitch Correction, ein Effekt der versucht
				gesungene Töne gerade zu halten, und Hall und Reverb gelegt (siehe Bild 2).
			</p>
			<br />
			<p>
				Zudem wurden auch stark mit der Lautstärke gearbeitet, da einige Aufnahme/einzelnen Stimmen
				lauter bzw. leiser waren als andere und um einen leichten FadeOut am Ende des Songs auf den
				Bass zu setzten (siehe Bild 3).
			</p>
			<br />
			<p>
				Zuletzt wurde nach der Weihnachtsvorstellung der Song verbessert: Das 4. "Imaginary" im Pre
				Chorus wurde gelöscht, da dieses sehr schief gesungen war und so unbrauchbar war. Es wurde
				mit einem Schlagzeug Solo ersetzt, bekannt als Motiv c (<a
					class="anchor"
					href="#schlagzeug-analyse">siehe Schlagzeug Analyse</a
				>). Auch wurde der Overdrive in der Chorus-Gitarre verringert (siehe Bild 4, von 25dB Drive
				auf 10dB Drive), da das sonst in vielen Fällen zu Übersteuerung geführt hat. Auch kann man
				die Stimme so besser verstehen.
			</p>
		</section>
		<section class="pt-14 pb-8 md:pb-14 xl:pb-28">
			<h2 class="h2 pb-1 md:pb-3">Fazit</h2>
			<p>
				Im Großen und Ganzen bin ich zufrieden mit unserem Endprodukt und mir hat auch insgesamt die
				Arbeit an einem eigenen Song sehr gefallen. Ich würde es auch nochmal machen wollen.
				Natürlich hätte noch einiges verbessert werden können, nur war die Zeit dafür nicht mehr da.
				Auch die Zeit nach dem Weihnachtskonzert war zu wenig, da man auch noch ein Portfolio
				schreiben muss. Man hätte z.B. einen komplexeren Bass, eine neue Aufnahme für die Stimme im
				Pre Chorus usw. machen können.
			</p>
			<br />
			<p>
				Mir hat es auch gezeigt, wie mit Deadlines umzugehen ist: Immer stetig dran zu arbeiten und
				sich dann auch mal früher aufzuteilen, wie wir es zum Ende immer mehr gemacht hatten.
			</p>
			<br />
			<p>
				Musikalisch ist es auf jeden Fall kein Meisterwerk. Man hätte sich mehr in die Materie
				einlesen können. Jedoch sind wir so zu einem relativ einzigartigem Endprodukt hingekommen,
				worauf Hanno und auch ich sehr stolz sind.
			</p>
			<br />
			<p>
				Als Gruppe hatten wir so viel Freude an diesem Projekt, dass wir in Zukunft planen, erneut
				etwas gemeinsam zu kreieren.
			</p>
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
