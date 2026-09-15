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

## Aktives Projekt: inselraub-prototyp

`/inselraub-prototyp/index.html` ist das Spiel, an dem aktuell tatsächlich
gearbeitet wird (nicht das Wellen-Experiment oben, das ist ein separater,
älterer Prototyp). Eine einzige HTML-Datei (Canvas 2D + JS, kein
Build-Schritt): Insel-Basis bauen, Gegnerwellen abwehren, Ressourcen
sammeln. Branch: `claude/chat-session-0308oj`.

### Bereits gebaute Systeme (nicht neu erfinden/doppeln)
- Grid-basierter Basis-Bau mit progressivem Freischalten, wachsendem Raster
  (5x5 → 7x7 → 9x9 je nach Basis-Level).
- Turm/Mauer mit HP, mehrere Waffentypen (Bogen/Kanone/Mörser) mit echten
  Kontern (Kanone durchdringt Rüstung, Mörser Flächenschaden mit
  Mindestreichweite). Dual-Condition-Unlock-Gating (Basis-Level UND
  Turm-Level nötig) ist ein bewusstes Anti-Exploit-Muster – wurde zweimal
  als Bug gemeldet, als nur EINE Bedingung geprüft wurde.
- Gegner-Wellen pathfinden per Dijkstra zur Base und beschädigen NUR
  Gebäude, die wirklich auf dem günstigsten Weg liegen (kein wahlloses
  Nächstes-Gebäude-Ziel mehr).
- Spielercharakter: Joystick-Steuerung, Rucksack-Sammel-Mechanik
  (Kapazität, Auto-Rückkehr, Auto-Entleeren an der Base), eigene HP –
  Gegner in der Nähe greifen ihn an, bei 0 HP geht der Rucksack-Inhalt
  verloren.
- Eigenständiges Spieler-Level/EXP-System (**getrennt vom Basis-Level!**):
  XP kommt aus Wellen überstehen + irgendwas verbessern (Basis- oder
  Gebäude-Upgrade).
- NPC-System (Kaserne/Krankenhaus/Reparatur-Trupp/Angreifer).
- Hafen-Struktur ab Level 7 (Steg mit zwei 3x3-Bootsplätzen) – nur
  Optik/Struktur bisher.

### Offene Fragen, noch nicht vom Nutzer beantwortet
- Was soll das erste Boot am Hafen konkret tun (Funktion völlig offen)?
- Laser-Turm / X-Bogen wurden nur als Idee genannt – welche Rolle/welchen
  Konter sollen sie haben (analog Bogen-vs-Kanone), bevor sie gebaut werden?

### Grafik/Design – Verlauf und Entscheidungen
Der Nutzer will explizit **"modern, nicht kindisch"** – keine hellen
Candy-Farben. Wichtig für zukünftige Design-Arbeit:
- **Kein** Anime-Fantasy-Gold-Rahmen ums HUD – wurde einmal gebaut und vom
  Nutzer explizit wieder rausgenommen.
- HUD-Profilblock ist 1:1 an einem vom Nutzer geschickten
  Sword-x-Staff-Screenshot orientiert: Avatar (dünner heller Ring, kein
  Gold) → Name (eigene Zeile) → Level-Chip (hängt unten am Avatar,
  überlappt ihn) → EXP-Leiste (dick, gelb-grün, dunkler Navy-Rand) →
  Kraft-Pille (dunkles Navy/Slate, Schwert-Icon). Kein umschließendes
  Panel um den ganzen Block.
- Weltgrafik: prozedurale Texturen (Value-Noise/FBM, einmalig in
  Offscreen-Canvases gerendert, dann als Pattern wiederverwendet) statt
  flacher Farbflächen für Gras/Stein/Holz/Wasser. Ein Licht-/Grading-Pass
  über die fertige Szene (warmes Sonnenlicht + kühler Gegenschatten +
  Vignette + Körnung über Blend-Modes) macht den größten Unterschied
  zwischen "gezeichnet" und "gerendert" wirkend.
- Insel hat eine organische Küstenlinie (Superellipse mit Rausch-Wobble),
  kein perfektes Quadrat mehr.
- Sand/Strand-Textur wurde ausprobiert und vom Nutzer explizit wieder
  entfernt ("Der Sand soll weg") – Küstenlinie/Schaumsaum bleiben, aber
  ohne sichtbaren Sandstreifen.
- Bewusst **kein** `ctx.filter()` im Zeichencode (iOS-Safari-Kompatibilität
  lange fehlend) – stattdessen Blend-Modes (multiply/screen/soft-light/
  overlay) und gestapelte Alpha-Ebenen. CSS-`filter` auf dem
  `<canvas>`-Element selbst (saturate/contrast/brightness) ist dagegen
  unproblematisch und wird genutzt.
- Echte "fotorealistische" 3D-Grafik ist mit dieser Technik (Canvas 2D,
  kein Bildgenerator, keine 3D-Engine) technisch nicht erreichbar – dem
  Nutzer offen kommuniziert. Nächster Schritt wäre entweder echte
  Bild-/Textur-Assets einbinden (braucht Bilddateien vom Nutzer oder ein
  Bildgenerierungs-Tool, das aktuell nicht zur Verfügung steht) oder
  Umstieg auf eine 3D-Engine – beides ein eigenes Projekt, kein
  inkrementeller Umbau.

### Technische Konventionen
- `SAVE_KEY`-Version in `defaultState()` bei JEDER Änderung der State-Form
  hochzählen (kein Migrations-Code – alte Saves werden dann sauber
  zurückgesetzt statt kaputt zu laden).
- Testing vor jedem Commit: Kopie nach `scratchpad/`, dort kurz vor dem
  schließenden `})();` einen `window.__test = {...}`-Hook einfügen, dann
  gezielt per Playwright prüfen (`NODE_PATH=/opt/node22/lib/node_modules
  node <script>.js`, `chromium.launch({executablePath:
  '/opt/pw-browsers/chromium'})`), plus Screenshot-Review bei visuellen
  Änderungen. Erst danach ins echte File committen und pushen.
- Der Nutzer reagiert sehr direkt/frustriert, wenn Design-Vorschläge ohne
  Rückfrage in die falsche Richtung gehen (siehe Gold-Rahmen, HUD-Layout).
  Bei größeren visuellen Richtungsentscheidungen lieber vorher eine kurze
  Vorschau/Nachfrage, statt durchzuarbeiten und zu hoffen, dass es passt.
