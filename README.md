# Solitaire

Das klassische Tisch-Solitaire (Steckspiel) mit Glaskugeln als Browser-Spiel. Eine einzige HTML-Datei, keine Abhängigkeiten, läuft direkt auf GitHub Pages.

## Spielregeln

- Eine Kugel springt waagerecht oder senkrecht über eine Nachbarkugel in die freie Mulde dahinter. Die übersprungene Kugel wird entfernt.
- Ziel: Am Ende bleibt nur eine Kugel übrig. Liegt sie im Zielfeld, ist das Spiel perfekt gelöst.
- Das Spiel endet, sobald kein Sprung mehr möglich ist.

## Bretter

| Brett | Mulden | Start | Ziel |
|---|---|---|---|
| Englisch | 33 | Mitte frei | Mitte |
| Europäisch | 37 | oben links im Arm frei | oben rechts im Arm (gestrichelt markiert) |

Das europäische Brett ist mit leerer Mitte nachweislich nicht lösbar, deshalb nutzt es die klassische Aufgabe „oben links räumen, oben rechts enden“.

## Funktionen

- Kugel antippen, Zielmulde antippen. Mögliche Ziele leuchten auf.
- Rückgängig (auch mit Strg+Z), Neustart, Zugzähler, Bestleistung pro Brett.
- Hinweis: Ein Solver im Web Worker sucht eine vollständige Lösung aus der aktuellen Stellung und markiert den nächsten Zug. Folgt man dem Hinweis, bleibt die Lösung zwischengespeichert.
- Der Spielstand wird im Browser gespeichert und beim nächsten Öffnen wiederhergestellt.

## Technik

- `index.html`: komplettes Spiel (HTML, CSS, JavaScript).
- Solver: Tiefensuche mit Erkennung bereits als aussichtslos bekannter Stellungen (inklusive Brettsymmetrien) und Zugsortierung „weit vom Ziel zuerst“. Suchbudget pro Anfrage begrenzt, damit die Oberfläche flüssig bleibt.
