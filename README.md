# Rex Solitär

Das klassische Tisch-Solitaire (Steckspiel) als Browser-Spiel: ein gedrechseltes Holzbrett mit Steinen aus Bone, Honig, Jade und Onyx auf einer Glasscheibe über Marmor. Eine HTML-Datei plus zwei Texturen, keine Abhängigkeiten, läuft direkt auf GitHub Pages.

Live: https://nicolehahn2890.github.io/Solitaire/

## Stand

- 50 verifizierte Levels in fünf Welten, freies Spiel auf zwei Bretter, Solver-Hinweise, Sterne, Fortschritt, drei Themen.
- Design nach dem Design-System „Rex Solitär“ (Claude Design), siehe Abschnitt Design.
- Brett mit erhabenem Rand, versenkter Rinne und erhabener Spielfläche. Geschlagene Steine rollen aus der Fläche in die Rinne und bleiben dort liegen, beim Zurücknehmen rollen sie zurück.

## Spielregeln

- Ein Stein springt waagerecht oder senkrecht über einen Nachbarn in die freie Mulde dahinter. Der übersprungene Stein wird entfernt und rollt in die Rinne.
- Am Ende bleibt ein Stein. Liegt er im gestrichelt markierten Zielfeld, ist das Level perfekt gelöst.
- Das Spiel endet, sobald kein Zug mehr möglich ist.

## Bedienung

- Stein antippen, dann eine markierte Mulde. Eine leere Mulde direkt antippen zieht den passenden Stein hinein, wenn er eindeutig ist. Können mehrere Steine dorthin, leuchten sie auf.
- Ein Stein, der nicht springen kann, zeigt beim Antippen die Steine, die es können.
- Zurücknehmen über den runden Button oben rechts (auch Strg+Z), „Neu legen“ startet das Brett neu, „Hinweis“ fragt den Solver.
- In den ersten drei Levels steht ein Einstiegshinweis unter dem Brett.

## Modi

**Levels:** 50 Puzzles in fünf Welten (Erste Schritte, Formen, Klassiker, Fortgeschritten, Meister), von 2 bis 36 Steinen auf verschiedenen Brettformen. Drei Sterne pro Level: gelöst, letzter Stein im Zielfeld, ohne Hinweis. Ein Stern schaltet das nächste Level frei. Jedes Level ist per Solver auf Lösbarkeit geprüft.

**Freies Spiel:** Die beiden klassischen Bretter, Bestleistung pro Brett wird gespeichert.

| Brett | Mulden | Start | Ziel |
|---|---|---|---|
| Englisch | 33 | Mitte frei | Mitte |
| Europäisch | 37 | oben links im Arm frei | oben rechts im Arm |

Das europäische Brett ist mit leerer Mitte nachweislich nicht lösbar, deshalb nutzt es die klassische Aufgabe „oben links räumen, oben rechts enden“.

## Startseite

Vier Karten: Levels mit Fortschrittsbalken und Sternen, Weiterspielen (nur bei offenem Spiel, mit Level und Zügen), Freies Spiel mit den Bestleistungen pro Brett, Thema mit Farbmuster. Der Goldbutton ist immer die nächste sinnvolle Aktion: Weiterspielen, das nächste offene Level oder Levels.

## Themen und Einstellungen

Zahnrad oben links auf der Startseite oder Karte „Thema“. Drei Themen: Jade (Standard), Alabaster, Onyx (ab 30 Sternen). Das Thema färbt Marmor und Glas, Brett und Steine bleiben. Dort lässt sich auch der Fortschritt zurücksetzen (zwei Klicks als Sicherung).

## Hinweis-Solver

Ein Solver im Web Worker sucht eine vollständige Lösung aus der aktuellen Stellung und markiert den nächsten Zug. Folgt man dem Hinweis, bleibt die Lösung zwischengespeichert. Tiefensuche mit Erkennung bereits als aussichtslos bekannter Stellungen (inklusive Brettsymmetrien) und Zugsortierung „weit vom Ziel zuerst“, Suchbudget pro Anfrage begrenzt. Wer den Hinweis nutzt, verliert den dritten Stern des Levels.

## Design

Die Oberfläche folgt dem Design-System „Rex Solitär“: Farb-, Typografie-, Abstands- und Bewegungs-Tokens, Cormorant Garamond für Wortmarke, Überschriften und Zahlen (Versalziffern), Jost für Bedienelemente, Gold als einziger Akzent und höchstens einmal pro Screen, Glasflächen nur über Marmor, alles Interaktive als Pille oder Kreis, keine Emojis, ruhige Textsprache ohne Ausrufezeichen.

Aufbau: Glas-Slab mit Krone und Wortmarke, deren Unterzeile pro Screen wechselt (SOLITÄR, LEVELS, LEVEL 12, FREIES SPIEL), zwei runde Chrome-Buttons in den oberen Ecken, HUD als Glas-Panel mit drei Werten, darunter zwei Pillen-Buttons.

## Technik

- `index.html`: komplettes Spiel (HTML, CSS, JavaScript) inklusive eingebetteter Leveldaten und Tokens.
- `assets/marble.jpg`: neutrale Marmortextur, per Soft-Light über den Themen-Verlauf gelegt. `assets/wood.jpg`: Ahornmaserung für Rand, Rinne und Fläche. Beide prozedural erzeugt.
- Levelformat: Zeilen aus Zeichen, `o` Stein, `.` leere Mulde, `x` leeres Zielfeld, `X` Stein auf dem Zielfeld, Leerzeichen keine Mulde.
- Brettgeometrie: Die Spielfläche ist der innere Bereich des Bretts (74 Prozent des Radius), die Zellgröße wird pro Brettform so berechnet, dass alle Mulden hineinpassen. Die Rinne hat 36 Ablageplätze, geschlagene Steine wandern zum nächsten freien Platz in Richtung ihres Austritts.
- Gespeichert wird im Browser (localStorage): Fortschritt, aktuelles Spiel inklusive Rinnenbelegung, Bestleistungen, Thema.
