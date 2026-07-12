# soundslikewhat Manager

Werkzeug zum Verwalten der Spotify-Playlist **soundslikewhat**: Sample-Familien markieren,
Rollen (Original / enthält Sample) setzen, auf Redundanz prüfen, umsortieren – und die
Reihenfolge direkt in Spotify zurückschreiben. Läuft komplett im Browser, ohne KI.

## Dateien
- **index.html** – das Tool (identisch mit `soundslikewhat-manager.html`; über `index.html`
  ist die Seite unter der kurzen Ordner-URL erreichbar).
- **soundslikewhat-manager.html** – gleiche App unter sprechendem Namen.
- **README.md** – diese Anleitung.

## Deine URLs (GitHub Pages)
- Kurz:  `https://komputremk02.github.io/soundslikewhat/`
- Lang:  `https://komputremk02.github.io/soundslikewhat/soundslikewhat-manager.html`

> Beide funktionieren. Entscheide dich für **eine** und nutze sie dauerhaft – die
> Markierungen werden pro URL im Browser gespeichert. Empfehlung: die kurze Root-URL.

## Änderungen veröffentlichen
Nach dem Ablegen der Dateien im Repo:
```
git add index.html README.md
git commit -m "Add tool as index.html + readme"
git push
```
Nach ~1 Minute ist die Seite aktualisiert.

## Einmalige Spotify-Einrichtung
1. `developer.spotify.com/dashboard` → **Create app** (Web API ankreuzen).
2. **Redirect URI** exakt eintragen – am besten die, die das Tool selbst anzeigt
   (Reiter **Spotify** → sie entspricht der URL, unter der du das Tool geöffnet hast),
   also z. B. `https://komputremk02.github.io/soundslikewhat/`.
3. **Settings → User Management** → deine eigene Spotify-E-Mail hinzufügen.
   (Diese E-Mail steht nur im Spotify-Dashboard – **nicht** in diesem Repo.)
4. **Client ID** kopieren.

## Nutzung
1. Tool-URL öffnen → Reiter **Spotify** → Client-ID einfügen → **Mit Spotify verbinden**.
2. **Playlist laden ⤓** – holt alle Titel in Reihenfolge.
3. **Markieren-Modus**: Rollen setzen, Familien bilden (mehrere anhaken → „Auswahl → neue Familie“).
4. **Prüfen**: findet Rollen ohne Familie, unvollständige/verstreute Familien, Doppel-Einträge.
5. **Sortieren**: per Drag & Drop.
6. **Reihenfolge speichern ⤒**: schreibt die aktuelle Reihenfolge in die Spotify-Playlist zurück.

## Sicherheit / Datenschutz
- In diesen Dateien stehen **keine** Zugangsdaten: kein Passwort, kein Token, keine E-Mail.
- Die Client-ID ist bei diesem Login-Verfahren (PKCE) öffentlich und wird ohnehin nur im
  Browser gespeichert, nicht im Code.
- Login und Zugriff laufen direkt über Spotify; nur dein im Dashboard freigeschaltetes
  Konto kann die Playlist laden/ändern.

## Backup
Vor dem ersten Zurückschreiben im Tool **Export → JSON/CSV** ziehen (sichert die
Original-Reihenfolge). Markierungen zusätzlich über **Speichern / Laden → Markierungen
exportieren** sichern.

## Funktionen (Kurzüberblick)
- **Zwei Themes:** Standard (dunkel, 2D-Graph) und **EVA** (retrofuturistisch, CRT, 3D-Graph
  mit orbitierender Kamera). Umschalten oben rechts oder per URL `#eva` / `#std`.
- **Beziehungs-Graph:** Familien = Farbe, Original = großer „Planet", Sampler = kleine „Monde".
  Verbindungen (Sample-Ketten) im Graph editierbar; Kräfte über Regler einstellbar.
- **Spalten-Layout:** Playlist links, offener Tab (Familien/Graph/…) rechts – jede Spalte
  scrollt einzeln, nichts läuft über den Bildschirm hinaus.
- **Cloud-Sync (GitHub Gist):** Tags, Familien, Verbindungen & Reihenfolge geräteübergreifend
  in einem **privaten** Gist. Reiter *Speichern / Laden* → klassischen Token (`ghp_…`, Scope
  `gist`) einfügen → *Neuen Gist erstellen*; auf weiteren Geräten dieselbe **Gist-ID**.
- **Auto-Backup** zusätzlich in eine lokale Datei (Chrome/Edge) und als JSON-Export.

## Zurückschreiben nach Spotify
Nach dem Umsortieren im Tool schreibst du die Reihenfolge mit **„Reihenfolge speichern ⤒“**
direkt zurück in deine Playlist. Voraussetzungen: die Playlist gehört dir, dein Konto ist in
der Spotify-App unter *User Management* eingetragen, du bist mit Schreibrechten verbunden
(sonst „Trennen“ und neu verbinden) und dein Konto hat aktiv **Spotify Premium**. Technisch
läuft es über `PUT /playlists/{id}/items` (erste 100 Titel) plus `POST /playlists/{id}/items`
(weitere in 100er-Blöcken) – seit der Feb-2026-Migration heißen die Endpunkte `/items` statt
`/tracks`, das Umsortieren eigener Playlists bleibt aber erlaubt.

> Vor dem ersten Zurückschreiben einmal **Export → JSON/CSV** ziehen – so ist jeder Stand wiederherstellbar.
