# Reputationstool – Dessarin Banner

Enthalten:
- `reputation.html` – Oberfläche
- `reputation.json` – zentrale Startdaten

Wichtig: Eine GitHub-Pages-HTML kann `reputation.json` lesen, aber nicht sicher zurück ins GitHub-Repository schreiben.
Die HTML enthält deshalb zunächst einen lokalen Fallback. Für die gemeinsame Version braucht es einen kleinen Schreib-Endpunkt (z.B. Google Apps Script, Cloudflare Worker oder ähnliches), der `reputation.json` und den Log zentral verwaltet.

Die Oberfläche ist bereits auf diesen Endpunkt vorbereitet:
`const WRITE_URL=''`

Wenn `WRITE_URL` gesetzt wird, sendet das Tool den kompletten neuen Datenstand per POST an diesen Endpunkt.

Statusgrenzen:
- 8+ Verbündet
- 3–7 Wohlwollend
- -1–2 Neutral
- -4–-2 Skeptisch
- -5 und weniger Feindlich

Rufverfall:
- alle 30 vergangenen Tage 1 Punkt Richtung 0
- GRP selbst wird dabei nicht verändert
- effektive GRP wird aus GRP und dem letzten Änderungsdatum berechnet

Änderungen:
- Mission/Ereignis
- Datum
- gemeinsame Begründung
- beliebig viele betroffene Fraktionen
- Änderung: +3/+2/+1/0/-1/-2/-3
- Transaktion wird als ein Logeintrag gespeichert
- Rückgängig baut den Fraktionsstand aus den verbleibenden Logeinträgen neu auf
