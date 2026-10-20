# Wissensduell

Grundwissen-Quiz zum Gegeneinanderspielen, direkt im Browser. Keine Installation, keine Anmeldung, läuft auf Handy, Tablet und PC.

## Spielmodi

**Duell (2 Spieler, 1 Gerät):** Das Handy liegt flach zwischen beiden Spielern, jeder hat seine eigene Bildschirmhälfte. Nach der Frage werden die Antworten kurz darauf freigegeben. Wer zuerst richtig tippt, bekommt den Punkt. Wer falsch tippt, ist für diese Frage gesperrt.

**Reihum (2–6 Spieler, 1 Gerät):** Das Handy wird weitergegeben. Jeder bekommt eigene Fragen und 20 Sekunden Zeit. Eine richtige Antwort bringt 10 Punkte plus bis zu 10 Punkte Zeitbonus. Am Ende gibt es für jeden eine Schulnote.

**Online (2 Spieler, 2 Geräte):** Einer wählt „Online“ und tippt auf **Raum erstellen**. Er bekommt einen 4-stelligen Raumcode und einen Link. Der andere öffnet den Link oder tippt den Code bei **Beitreten** ein. Danach bekommen beide gleichzeitig dieselbe Frage und haben 20 Sekunden Zeit. Richtig gibt 10 Punkte plus bis zu 10 Punkte Zeitbonus. Man sieht live, ob der Gegner schon geantwortet hat, und nach jeder Frage, was er getippt hat. Am Ende kann man direkt eine Revanche starten.

Am PC geht es auch per Tastatur: Im Duell spielt unten mit `1` bis `4`, oben mit `7`, `8`, `9` und `0`. Online antwortet man mit `1` bis `4`.

## Inhalt

157 Fragen in sechs Fächern:

| Fach | Kürzel |
|---|---|
| Erdkunde | `geo` |
| Geschichte | `ges` |
| Naturwissenschaft | `nat` |
| Sprache & Kunst | `kul` |
| Sport | `spo` |
| Mathe & Alltag | `all` |

Vor dem Spiel lassen sich Fächer und Anzahl der Fragen (10, 15 oder 20) auswählen. Online legt das fest, wer den Raum erstellt. Fragen, die gerade erst dran waren, kommen so schnell nicht wieder.

## Online stellen mit GitHub Pages

1. Auf GitHub ein neues, **öffentliches** Repository anlegen, z. B. `wissensduell`.
2. **Add file → Upload files**, dann `index.html` und `README.md` hochladen und mit **Commit changes** bestätigen. Die `index.html` muss direkt im Hauptordner liegen, nicht in einem Unterordner.
3. Im Repository **Settings → Pages** öffnen. Bei **Source** „Deploy from a branch“ wählen, Branch `main` und Ordner `/ (root)`, dann **Save**.
4. Nach ein bis zwei Minuten ist das Spiel erreichbar unter
   `https://DEIN-NAME.github.io/wissensduell/`

Tipp: Den Link auf dem Handy öffnen und „Zum Home-Bildschirm hinzufügen“, dann startet das Quiz wie eine App.

Der Online-Modus braucht die veröffentlichte Seite, damit der Einladungslink auf dem anderen Gerät funktioniert. Die beiden anderen Modi laufen auch, wenn man die `index.html` einfach im Browser öffnet.

## Eigene Fragen hinzufügen

Alle Fragen stehen in `index.html` in der Liste `Q`. Jede Zeile hat dieses Format:

```js
['geo','Was ist die Hauptstadt von Australien?','Canberra','Sydney','Melbourne','Perth'],
```

1. Fach-Kürzel (siehe Tabelle oben)
2. Frage
3. **richtige Antwort** (immer an dieser Stelle)
4. bis 6. drei falsche Antworten

Die Reihenfolge der Antworten wird beim Spielen automatisch gemischt. Innerhalb der Texte keine geraden Apostrophe (`'`) verwenden, sonst bricht die Zeile. Typografische Anführungszeichen wie „so“ sind kein Problem.

## Technik

- Eine einzige HTML-Datei, kein Build-Schritt, kein eigener Server.
- **Online-Modus:** Die Geräte verbinden sich direkt miteinander (WebRTC) über die Bibliothek [PeerJS](https://peerjs.com). Für den Verbindungsaufbau wird kurz der kostenlose öffentliche PeerJS-Server genutzt, danach laufen die Spieldaten von Gerät zu Gerät. Es werden keine Spielstände auf einem Server gespeichert.
- Wer den Raum erstellt, wählt die Fragen aus und rechnet die Punkte. Jedes Gerät misst seine Antwortzeit selbst, damit eine langsamere Internetverbindung keinen Nachteil bringt.
- Falls die Verbindung nicht klappt: Manche Firmen- oder Schul-WLANs blockieren direkte Verbindungen. Dann hilft es meist, auf mobile Daten zu wechseln.
- Einstellungen und zuletzt gespielte Fragen werden nur lokal im Browser gespeichert.
- Die Schriften (Bricolage Grotesque, Atkinson Hyperlegible) werden von Google Fonts geladen. Wer das nicht möchte, löscht die drei `<link>`-Zeilen zu `fonts.googleapis.com` und `fonts.gstatic.com` im Kopf der Datei. Dann werden die Systemschriften verwendet.
- Hell- und Dunkelmodus folgen automatisch der Einstellung des Geräts.
