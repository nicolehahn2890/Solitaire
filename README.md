# Solitaire

Das klassische Tisch-Solitaire (Steckspiel) mit Glaskugeln als Browser-Spiel. Eine einzige HTML-Datei, keine Abhängigkeiten, läuft direkt auf GitHub Pages.

Live: https://nicolehahn2890.github.io/Solitaire/

## Spielregeln

- Eine Kugel springt waagerecht oder senkrecht über eine Nachbarkugel in die freie Mulde dahinter. Die übersprungene Kugel wird entfernt.
- Ziel: Am Ende bleibt nur eine Kugel übrig. Liegt sie im gestrichelt markierten Zielfeld, ist das Level perfekt gelöst.
- Das Spiel endet, sobald kein Sprung mehr möglich ist.

## Modi

**Levels:** 50 Puzzles in fünf Welten (Erste Schritte, Formen, Klassiker, Fortgeschritten, Meister), von 2 bis 36 Kugeln auf verschiedenen Brettformen. Drei Sterne pro Level: gelöst, letzte Kugel im Zielfeld, ohne Hinweis. Ein Stern schaltet das nächste Level frei. Jedes Level ist per Solver auf Lösbarkeit geprüft.

**Freies Spiel:** Die beiden klassischen Bretter.

| Brett | Mulden | Start | Ziel |
|---|---|---|---|
| Englisch | 33 | Mitte frei | Mitte |
| Europäisch | 37 | oben links im Arm frei | oben rechts im Arm |

Das europäische Brett ist mit leerer Mitte nachweislich nicht lösbar, deshalb nutzt es die klassische Aufgabe „oben links räumen, oben rechts enden“.

## Funktionen

- Kugel antippen, Zielmulde antippen. Mögliche Ziele leuchten auf.
- Zug zurück (auch Strg+Z), Neustart, Zugzähler, Sterne bzw. Bestleistung.
- Hinweis: Ein Solver im Web Worker sucht eine vollständige Lösung aus der aktuellen Stellung und markiert den nächsten Zug. Folgt man dem Hinweis, bleibt die Lösung zwischengespeichert.
- Konfetti beim Levelsieg.
- Spielstand und Fortschritt werden im Browser gespeichert. „Weiterspielen“ auf der Startseite nimmt ein angefangenes Spiel wieder auf.

## Technik

- `index.html`: komplettes Spiel (HTML, CSS, JavaScript) inklusive eingebetteter Leveldaten.
- Levelformat: Zeilen aus Zeichen, `o` Kugel, `.` leere Mulde, `x` leeres Zielfeld, `X` Kugel auf dem Zielfeld, Leerzeichen keine Mulde.
- Solver: Tiefensuche mit Erkennung bereits als aussichtslos bekannter Stellungen (inklusive Brettsymmetrien) und Zugsortierung „weit vom Ziel zuerst“. Suchbudget pro Anfrage begrenzt, damit die Oberfläche flüssig bleibt.
