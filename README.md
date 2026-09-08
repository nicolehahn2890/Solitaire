# Rex Solitär

Das klassische Tisch-Solitaire (Steckspiel) als Browser-Spiel: ein gedrechseltes Holzbrett mit Steinen aus Elfenbein, Honig, Jade und Onyx auf einer Glasscheibe über Marmor. Eine HTML-Datei plus zwei Texturen, keine Abhängigkeiten, läuft direkt auf GitHub Pages.

Live: https://nicolehahn2890.github.io/Solitaire/

## Spielregeln

- Ein Stein springt waagerecht oder senkrecht über einen Nachbarn in die freie Mulde dahinter. Der übersprungene Stein wird entfernt.
- Am Ende bleibt ein Stein. Liegt er im gestrichelt markierten Zielfeld, ist das Level perfekt gelöst.
- Das Spiel endet, sobald kein Zug mehr möglich ist.

## Modi

**Levels:** 50 Puzzles in fünf Welten (Erste Schritte, Formen, Klassiker, Fortgeschritten, Meister), von 2 bis 36 Steinen auf verschiedenen Brettformen. Drei Sterne pro Level: gelöst, letzter Stein im Zielfeld, ohne Hinweis. Ein Stern schaltet das nächste Level frei. Jedes Level ist per Solver auf Lösbarkeit geprüft.

**Freies Spiel:** Die beiden klassischen Bretter.

| Brett | Mulden | Start | Ziel |
|---|---|---|---|
| Englisch | 33 | Mitte frei | Mitte |
| Europäisch | 37 | oben links im Arm frei | oben rechts im Arm |

Das europäische Brett ist mit leerer Mitte nachweislich nicht lösbar, deshalb nutzt es die klassische Aufgabe „oben links räumen, oben rechts enden“.

## Funktionen

- Stein antippen, Zielmulde antippen. Mögliche Ziele werden markiert.
- Zurücknehmen (Chrome-Button oben rechts, auch Strg+Z), Neu legen, Zugzähler, Sterne bzw. Bestleistung.
- Hinweis: Ein Solver im Web Worker sucht eine vollständige Lösung aus der aktuellen Stellung und markiert den nächsten Zug. Folgt man dem Hinweis, bleibt die Lösung zwischengespeichert.
- Drei Themen: Jade, Alabaster und Onyx (ab 30 Sternen). Einstellungen über das Zahnrad auf der Startseite, dort lässt sich auch der Fortschritt zurücksetzen.
- Spielstand und Fortschritt werden im Browser gespeichert. „Weiterspielen“ auf der Startseite nimmt ein angefangenes Spiel wieder auf.

## Design

Die Oberfläche folgt dem Design-System „Rex Solitär“ (Claude Design): Farb-, Typografie-, Abstands- und Bewegungs-Tokens, Cormorant Garamond für Wortmarke und Zahlen, Jost für Bedienelemente, Gold als einziger Akzent, Glasflächen nur über Marmor, alles Interaktive als Pille oder Kreis, keine Emojis.

## Technik

- `index.html`: komplettes Spiel (HTML, CSS, JavaScript) inklusive eingebetteter Leveldaten und Tokens.
- `assets/marble.jpg`: neutrale Marmortextur, wird per Soft-Light über den Themen-Verlauf gelegt. `assets/wood.jpg`: Ahornmaserung fürs Brett. Beide prozedural erzeugt.
- Levelformat: Zeilen aus Zeichen, `o` Stein, `.` leere Mulde, `x` leeres Zielfeld, `X` Stein auf dem Zielfeld, Leerzeichen keine Mulde.
- Solver: Tiefensuche mit Erkennung bereits als aussichtslos bekannter Stellungen (inklusive Brettsymmetrien) und Zugsortierung „weit vom Ziel zuerst“. Suchbudget pro Anfrage begrenzt, damit die Oberfläche flüssig bleibt.
