# Projektkontext für Claude

## Vorgeschichte (wichtig für Design-Entscheidungen)

Der Nutzer hat vor diesem Projekt zwei andere Spiele gebaut, die beide am selben
strukturellen Problem gescheitert sind:

1. **Running Island** (gelöscht) – Idle-Sammelspiel: sammeln, aufwerten,
   schneller sammeln. Feedback von Testspielern: langweilig, es "passiert nichts".
2. **Wellensystem** (gelöscht) – Aufbau-Tower-Defense: Basis bauen, Wellen
   abwehren. Probleme:
   - Schwierigkeit wurde nur über Zahlen skaliert (mehr HP/Schaden), keine
     unterschiedlichen Gegnertypen mit echten Kontern → Wellen wurden irgendwann
     unfair stark.
   - Gegner angreifen hat 2-3 Mal Spaß gemacht, danach langweilig (keine Vielfalt).
   - Wenn nach "mehr Inhalt" gefragt wurde, kam immer nur Deko (Skins, neue
     Pflanzensorten) statt neuer Spielmechanik.

Aktuell im Repo: ein Raid-Rush-artiger Klon (`Spiel js`, `Index`, `style.css`,
`Js Aufgaben`) – Pflanzen setzen, Beeren einsammeln, Skilltree, Pets, Kisten,
Quests. Der Nutzer mag dieses Spiel nicht (gleiches Grundproblem: viele Systeme,
aber alle sind nur Multiplikatoren auf denselben Sammel-Loop).

## Leitprinzip: Entscheidungen vor Dekoration

Bevor neue Grafik, Skins oder Inhalte hinzugefügt werden: Der nackte
Spiel-Loop muss auch ohne Kunst (nur Formen/Farben) über mehrere Runden
interessant bleiben, weil der Spieler echte **Entscheidungen** trifft
(Trade-offs, Konter, begrenzte Ressourcen) – nicht nur Fortschrittsbalken
beim Wachsen zusieht.

Konkret heißt das für zukünftige Systeme:
- Schwierigkeit steigt durch **Zusammensetzung/Varianz**, nicht nur durch
  höhere Zahlen (z. B. neue Gegner-/Situationstypen statt nur mehr HP).
- Ressourcen/Bauplätze/Auswahl sind **begrenzt**, damit man nicht einfach
  alles gleichzeitig haben kann.
- Neue Anfragen nach "mehr Content" zuerst kritisch hinterfragen: Ist das
  eine neue Entscheidung oder nur Deko? Deko ist okay, aber erst NACHDEM
  der Kern-Loop nachweislich mehrere Spielsitzungen lang trägt.

## Laufendes Experiment

`/wellen-prototyp/index.html` – eigenständiger, kunstfreier Prototyp zum
Testen des Wellen-Verteidigungs-Kerns: 4 Gegnertypen mit echten Schwächen
(Panzerung, Schwarm, Luft), 4 Turmtypen mit klaren Vor-/Nachteilen, begrenzte
Bauplätze, Wellen mit wechselnder Zusammensetzung statt reiner Zahlen-Skalierung.
Ziel: erst prüfen, ob DIESER Kern beim Testspielen trägt, bevor irgendeine
Grafik reinkommt. Direkt im Browser öffnen (keine Installation nötig).

Nächste Schritte hängen vom Feedback des Nutzers zu diesem Prototyp ab –
nicht vorschnell mit Grafik/Content weitermachen, ohne dass der Loop bestätigt
wurde.
