# DROPZONE HD — Entwicklungsplan

**Working Title:** *IO — Dropzone* (öffentlicher Release ggf. unter Originalnamen wie *Tacheon* / *Magma Run*)
**Vorbild:** Dropzone (1984) — Archer MacLean / Arena Graphics / U.S. Gold
**Stack:** Single-File HTML5 · Canvas 2D (Logik-Layer) + WebGL (CRT-Pass) · Web Audio (SID-Style) · Pointer Events
**Plattform:** Desktop + Mobile (Querformat), eine `.html`-Datei, selbst-gehostet
**Version:** 0.1 (Plan)

---

## 0. Designphilosophie — „Treue + High-End"

Zwei Achsen, die nie kollidieren dürfen:

1. **Mechanische Treue.** Das Gameplay ist 1:1 Dropzone: Jetpack-Trägheit + Schwerkraft, bidirektionales Laserfeuer, Rettungs-Loop, Strata-Bombe, Cloak, der 6×-Planet-Scanner. Wer das Original kennt, soll es im Muskelgedächtnis wiedererkennen.
2. **Präsentations-Upgrade.** Alles *um* die Mechanik herum wird gehoben: echte CRT-Simulation, generativer SID-Soundtrack (den das Original bewusst *nicht* hatte), Partikel/Juice, ein UX-Layer auf 2025-Niveau und eine **unsichtbare** Touch-Steuerung.

> **Leitregel:** Treue schlägt Bequemlichkeit. Wenn ein „modernes" Feature die Dropzone-Physik glättet (z.B. Snap-Movement statt Impuls), kommt es als optionaler Toggle — nie als Default.

**Purist-Mode** als Settings-Toggle: SID-SFX an, generative Musik aus, harte C64-Farbzellen-Limits an → das Original-Erlebnis. Default ist „HD".

---

## 1. Original-Analyse (Dropzone 1984)

Verbindliche Spezifikation des Kerns. Quelle: C64-Wiki.

### Setting
Jahr 2085, Erde durch Roboterkriege zerstört. Der Tacheon-Antrieb braucht ionische Kristalle (mit Quarz beschossen). Die letzten Vorkommen liegen auf Jupiters Mond **IO**, ausgeworfen von drei aktiven Vulkanen. Der Spieler trägt ein Impuls-Laser-Rucksacksystem, kann **einen** Menschen tragen und sich kurz unsichtbar + unzerstörbar machen. Aufgabe: Überlebende + Kristalle zur **Dropzone** (Landeplattform) zurückbringen.

### Core Loop
Welle starten → Menschen vor Androiden schützen → einsammeln → zur Dropzone tragen → absetzen → alle Gegner + alle Menschen gerettet = Welle vorbei → Bonus → nächste Welle.

### Steuerung (Original-Mapping)
| Aktion | Original |
|---|---|
| Schießen | Feuerknopf — **jede** Auf-/Ab-Bewegung des Knopfes = ein Laserimpuls |
| Rückwärtsfeuer | Stick kurz in Gegenrichtung zur Blickrichtung halten → Schuss nach hinten (gegen Verfolger) |
| Horizontaler Schub | Links/Rechts — je länger gehalten, desto schneller; Gegenrichtung = bremsen/wenden |
| Vertikaler Schub | Vor/Zurück — Schwerkraft zieht permanent nach unten; ohne Horizontalschub landet man |
| Strata-Bombe | Space — zerstört alle Gegner in Sicht **außer Androiden** |
| Cloak | jede andere Taste — unzerstörbarer Schild, solange Energie reicht |

### Bestiarium (jeweils eigenes Verhalten)
- **Menschen** — laufen langsam zur Basis, tragen Kristalle, **pfeifen um Hilfe** wenn ein Android angreift.
- **Planters + Androiden** — Planter driften über die Oberfläche, steigen über Vulkanen/Basis, suchen Menschen. Beim Angriff senkt der Android sich zur Jagd ab; der Planter wird zum **Nemesite**.
- **Nemesites** — zielsuchende Killerrakete, weicht Laserfeuer aus bis sie nah genug ist. Warnton beim Eintritt in die Sicherheitszone.
- **Antimatter** — entsteht, wenn **alle** Menschen tot sind: Planter+Androiden verschmelzen zu einem kreisenden, anziehenden Knoten. Erdbeben, Mond instabil, Vulkane spucken tödliche weißglühende Felsen.
- **Spores** — harmlos bis getriggert, setzen dann **4 Trailer** frei.
- **Trailer** — unberechenbare Bahnen, manche verfolgen hartnäckig, nur am „Kopf" zerstörbar. Haben „Persönlichkeiten".
- **Blunderstorms** — lautlose Stürme in der oberen Atmosphäre; Säureregen oder Protonenblitze nach ~1 s Grollen (Vorwarnung!).
- **Nmeyes** — kommen, wenn man eine Welle zu lange überlebt: beobachten jede Bewegung, blitzen, irregulär & schneller als der Spieler, werfen Bomben. Sequenzierte schwerer zerstörbar.
- **Vulkane** — normal: kleine Magmabälle; bei „alle Menschen verloren": tödliche weißglühende Felsen.
- **Bombs** — von Planters/Nemesites/Antimatter/Nmeyes; zerstörbar, indem man mit gleicher Geschwindigkeit fliegt.

### Wellen & Progression
- Start: **8 Menschen**, **15 s** Schildzeit, **3** Strata-Bomben.
- Extra-Leben + Strata-Bombe **alle 10.000 Punkte**; **+7 s** Schildzeit pro Welle; Stopp ab 1.000.000.
- Welle endet: alle Planters/Spores/Trailers/Blunderstorms zerstört **und** alle (lebenden) Menschen in der Basis.
- Bonus: gerettete Menschen × Wellennummer, **max. 500/Mensch**.
- Jede **5. Welle**: neue Menschen-Lieferung — aber davor eine **Trailer-Invasions-Welle**.
- Wellen 1–99, danach Wiederholung 95–99. Jede Welle zufällig in Ablauf & Startpunkt.
- Tod beim Tragen → Mensch wird auf der Oberfläche neu platziert.
- Alle 8 gerettet + gelandet → keine weiteren Android-Angriffe in der Welle. Weniger → ein Android infiltriert die Basis über die Plattform.

### Punkte
Menschen gerettet/überlebt 100–500 · zerstört 0 · Android (senkend/folgend) 50, (fallend nach zerstörtem Planter) 500 · Planter 250 · Nemesite 150 · Antimatter 150 · Blunderstorm 250 · **Spore 750** · Trailer 250 · Nmeye 100 · Leben verloren 10.

### HUD-Layout (Original, verbindlich nachzubauen)
Hauptansicht oben (Echtzeit-Zone über IO: Schluchten, Lavagräben, Vulkane, ionischer See, Krater). Unten Instrumente: Anzahl Menschen · gerettete · **Angriffs-Richtungspfeil** (zeigt kürzesten Weg zum angegriffenen Menschen) · Schild-Restzeit · Leben · Strata-Bomben · Punkte · **Planet-Scanner** (Radar, **6× Hauptbildbreite**, jedes Crew-Mitglied eigene Farbe/Größe, Landeplattform = **weißes Kreuz**).

### Charakter des Originals
Extrem **flüssiges Scrolling**, sehr **hohe Geschwindigkeit**, **keine Musik** aber sehr gute SFX, Parallax-Scrolling, meiste Elemente als Bitmap (nicht Sprites) → manche Effekte überlappen Gegner.

---

## 2. Technische Architektur

### Grundgerüst
- **Eine** `.html`-Datei. CSS + JS + Font (Base64-`@font-face`) inline → echtes Single-File, offline lauffähig.
- **Fixed-Timestep-Loop** (z.B. 60 Hz Logik, entkoppelt vom Render via Accumulator). Dropzones „insane speed" verlangt deterministische Physik — kein variabler dt im Gameplay.
- **State Machine:** `BOOT → ATTRACT → MENU → PLAY → PAUSE → WAVE_TRANSITION → GAME_OVER → HIGHSCORE_ENTRY`.

### Logische Auflösung & Welt
- Internes Render-Target in C64-naher Auflösung (z.B. **384 × 272** logisch; Hauptansicht ~320×176 + HUD-Band unten ~96px). Integer-Upscaling auf das nächste ganzzahlige Vielfache, dann CRT-Pass.
- **Welt-Breite ≈ 6 × Bildbreite**, horizontal **wraparound** (passt zum 6×-Scanner). Spieler in der Mitte, Kamera folgt mit Vorhalt in Flugrichtung (wie Defender/Original).

### Interne Modulstruktur (innerhalb der einen Datei)
```
core/      Loop, Zeit, RNG (seedbar), State-Machine, Input-Router
render/     PaletteBuffer (Indexed→RGBA), Layer-Compositor, CRT-Shader
world/      Heightmap-Terrain, Parallax-Layer, Wraparound-Mathe, Scanner
entities/   Player, Human, Planter, Android, Nemesite, Antimatter,
            Spore, Trailer, Blunderstorm, Nmeye, Volcano, Bomb, Laser, Particle
systems/    Physics, Collision, SpawnDirector, WaveManager, Scoring, FX
audio/      SIDVoice (AudioWorklet), SFXBank, MusicEngine
ui/         HUD, Menu, AttractAI, HighscoreTable, ToastPopups
input/      KeyboardJoystick, GamepadAdapter, InvisibleTouch, Haptics
```

### Performance
- Indexed-Color-Framebuffer: ein `Uint8Array` (Palettenindex pro Pixel), einmal pro Frame → `ImageData` (RGBA) via Lookup. Hält den C64-Look „echt" und ist schnell.
- Object-Pooling für Laser/Partikel/Bomben (hohe Spawn-Raten).
- Spatial-Hash/Grid für Kollisionen statt O(n²).
- Mobile: dynamische Partikel-Caps, optionaler Half-Res-CRT-Pass.

---

## 3. Rendering & GFX (authentisch + original)

### Palette — C64 „Colodore"/Pepto (verbindlich)
```
0  Black       #000000     8  Orange      #8E5029
1  White       #FFFFFF     9  Brown       #553800
2  Red         #813338    10  Light Red   #C46C71
3  Cyan        #75CEC8    11  Dark Grey   #4A4A4A
4  Purple      #8E3C97    12  Grey        #7B7B7B
5  Green       #56AC4D    13  Light Green #A9FF9F
6  Blue        #2E2C9B    14  Light Blue  #706DEB
7  Yellow      #EDF171    15  Light Grey  #B2B2B2
```
Gesamtes Spiel zeichnet **nur** aus diesen 16 Werten. CRT-Pass darf danach interpolieren/bloomen, der Quell-Buffer bleibt indexed.

**Farbzellen-Authentizität (Toggle):** Optional echte Multicolor-Beschränkung (begrenzte Farben pro 8×8/4×8-Zelle). Default für „HD" gelockert (Palette-only-Freiheit), Purist-Mode = harte Limits.

### Original-Pixel-Art (deine Assets, kein Rip)
- Eigene Sprites im 16-Farb-Raster. **Keine** Original-Grafiken von MacLean extrahieren (IP) — du wolltest ohnehin originale GFX. Im Abspann „Inspired by Dropzone (1984), Archer MacLean" als Hommage.
- Asset-Liste: Astronaut (Idle/Schub-Frames/Explosion „Wizball-style"), Mensch (laufend + getragen), Kristall, alle Gegnertypen + Animationen, Laser/Bombe/Partikel, Vulkan-Eruption, Magmabälle, Terrain-Tiles (Schluchten/Lava/ionischer See/Krater), Landeplattform mit weißem Kreuz, Scanner-Blips.
- Empfehlung: Sprites als kompaktes JSON (Palettenindizes) **im Code** generieren oder inline-Base64-PNG-Atlas → bleibt Single-File.

### Terrain & Parallax
- Prozedural generierte **Heightmap** für die IO-Oberfläche (seedbar pro Welle), gerendert als zerklüftete Silhouette mit Lavagräben + ionischem See.
- 3 Layer: Sternenfeld/Hintergrund (langsam) → Bergsilhouette (mittel) → Vordergrund-Krater (schnell). Alle wraparound.
- Vulkane an festen Welt-Positionen, periodische Eruptionen.

### CRT-Simulation (WebGL-Post-Pass)
Offscreen-Game-Canvas → Textur → Fullscreen-Shader:
- **Aperture-/Slot-Mask** (RGB-Phosphor-Subpixel)
- **Scanlines** (Intensität regelbar)
- **Barrel-Distortion** + Vignette (dezent)
- **Bloom** auf hellen Pixeln (Laser, Explosionen, weißglühende Felsen leuchten)
- leichtes **Chromatic-Aberration** an den Rändern; kurzer Spike bei Treffer (zur CRT konsistent)
- Alles über Settings dimmbar (inkl. Komplett-Aus für Pixel-pur).

### Font
**Retro Gaming** (Daymarius, dafont, „100% Free", Bitmap 11px, 319 Glyphen inkl. ä/ö/ü/ß) als Base64-`@font-face` inline. Für scharfe Pixel: ganzzahlige Font-Größen + `image-rendering: pixelated` auf Canvas, `font-smooth: never`. Eigener Bitmap-Renderer für HUD-Zahlen (Score/Timer) für perfekte Ausrichtung; CSS-Font für Menü-Text.

---

## 4. Generativer Sound (SID-Style)

Das **High-End-Upgrade**: Das Original hatte keine Musik. Wir bauen einen **generativen SID-Soundtrack**, der auf den Spielzustand reagiert — und behalten die authentischen SFX.

### SID-Voice (AudioWorklet)
Nachbau der MOS 6581/8580-Charakteristik, weil `OscillatorNode` allein (kein echtes PWM/Ringmod) zu „clean" klingt:
- 3 Stimmen, je: **Triangle / Sawtooth / Pulse (variable Pulsweite, PWM) / Noise**
- **ADSR**-Hüllkurve pro Stimme
- **Ring-Modulation** & **Oscillator-Sync** (die klassischen SID-Tricks)
- gemeinsamer **Multimode-Filter** (LP/BP/HP) mit Resonanz
- Sample-genaue Erzeugung im Worklet → echte Pulsweiten-Modulation
- **Fallback:** Standard-`OscillatorNode` + `BiquadFilter` + Noise-Buffer, falls AudioWorklet nicht verfügbar.

### Prozedurale SFX (event-getriggert, alle SID-synthetisiert)
Laserimpuls · Explosion (Spielertod, „Wizball"-Charakter) · **Hilfe-Pfeifen** der Menschen · Strata-Bombe · Cloak-An/Aus + Summen · Mensch aufgenommen · Mensch abgeliefert · **Nemesite-Warnton** · Bombe abgefeuert · Vulkan-Eruption · Blunderstorm-Grollen (1 s Vorwarnung) · Extra-Leben-Jingle · Wellen-Bonus-Sound. Jeder Effekt parametrisch (leichte Zufallsvariation → nie monoton).

### Generative Music-Engine
- Tracker-artiger Sequencer mit kleinem Patch-Set (Bass, Lead, Arp, Drums — alles SID).
- **Reaktive Intensität:** Layer-Anzahl, Tempo und Aggressivität skalieren mit Wellennummer + aktueller Gefahr (Anzahl/Nähe Gegner, Schild-Status, Antimatter-Phase).
- Generative Arrangement: probabilistische Pattern-Auswahl + Variation auf festem harmonischem Gerüst → endlos, kohärent, nie loop-müde.
- **Stinger** bei Schlüssel-Events (Welle clear, Antimatter-Trigger, letzter Mensch).
- Toggle „No Music (Purist)" respektiert das Original.

---

## 5. Gameplay-Systeme

### Physik (Herzstück)
Impuls-basiert, **nicht** geschwindigkeits-direkt:
- Horizontal: Schub-Input addiert Beschleunigung; Geschwindigkeit baut sich auf/ab (Trägheit). Gegenrichtung bremst. Soft-Cap auf Maxspeed.
- Vertikal: **konstante Schwerkraft** zieht nach unten; Schub-Input wirkt dagegen. Ohne Horizontalschub → kontrollierte Landung auf der Heightmap.
- Tuning-Konstanten zentral (`accel`, `gravity`, `drag`, `maxVel`) → exakt am Original-Feel kalibrieren (Referenz: Longplay-Video).

### Spieler-Aktionen
- **Laser:** diskreter Impuls pro Feuer-Event (kein Dauerstrahl). Standard in Blickrichtung; **Rückwärtsfeuer** wenn Bewegungs-Input kurz entgegen der Blickrichtung gehalten wird.
- **Cloak:** Energiebudget (Sekunden), zählt nur während aktiv runter; +7 s pro Welle. Macht unzerstörbar.
- **Strata-Bombe:** vernichtet alles in Sicht außer Androiden. Begrenzter Vorrat. **Anti-Spam:** zu viele in Folge → Gegner schicken Nmeyes (Original-Verhalten).

### Gegner-KI (pro Typ, gemäß §1)
- **SpawnDirector:** orchestriert Welle nach Typ-Quoten + Timing, seedbar, „totally random in plot and start point".
- **Eskalations-Timer:** Welle zu lange offen → Nmeye-Spawn.
- **Antimatter-Phase:** alle Menschen tot → Verschmelzung, Vulkane gehen in „tödlich"-Modus, globales Erdbeben-Shake.
- **Trailer-Invasion** vor jeder 5. Welle als eigener Modus.

### Rettungs-Loop
- Mensch laufen-Logik zur Basis; Aufnahme bei Kollision (max. 1 gleichzeitig); Abgabe nur auf der Plattform.
- **Hilfe-Pfeifen** + **Richtungspfeil** (kürzester Weg, wraparound-korrekt) wenn ein Android einen Menschen jagt.
- Tod beim Tragen → Mensch respawnt auf Oberfläche.
- Android-Infiltration der Basis wenn < 8 gerettet.

### Scanner / Radar
- Eigener Render-Pass: gesamte 6×-Welt komprimiert, farbcodierte Blips (Spieler, Menschen, Gegnertypen), Plattform als weißes Kreuz. Live-Sync mit Welt-State.

### Scoring & Progression
Punkte/Boni/Extra-Leben/Wellen-Struktur exakt nach §1. Score-Popups als UX-Juice.

---

## 6. UX / UI (High-End)

- **Attract-Mode:** KI-Demospiel + animierter Titel (laufender Scanner, Sternenfeld, Retro-Gaming-Font, generativer Track) — startet nach Idle.
- **Menü:** Start · Settings · Highscores · Credits. Settings: CRT-Intensität, Scanlines, Audio-Mix (Musik/SFX getrennt), Steuerungs-Hinweise, Haptik, Reduced-Motion, Purist-Mode, Sprache (DE/EN).
- **HUD:** exakt §1-Layout. Eigener Pixel-Zahlen-Renderer, Schild als ablaufende Leiste, Bomben/Leben als Icons, Richtungspfeil prominent.
- **Juice (CRT-konsistent):** Screenshake (Explosion/Bombe/Erdbeben), Palette-Flash, Partikelbursts, Score-Popups, Wellen-Übergangs-Banner mit Bonus-Aufschlüsselung, Treffer-Aberration-Spike.
- **Highscore:** 3-Zeichen-Eingabe wie Original (60 s), aber persistent.
  - **Persistenz-Hinweis:** im claude.ai-Artifact-Preview ist `localStorage` gesperrt → dort nur In-Memory. In deinem **selbst-gehosteten** Single-File-Build (GitHub Pages etc.) funktioniert `localStorage` normal → echte persistente Bestenliste. Optional später ein kleines Server-Backend für globale Liste.
- **Accessibility:** Reduced-Motion (weniger CRT/Shake), farbblind-sichere Scanner-Option, Remapping, Pause (F1).

---

## 7. Unsichtbare Mobile Touch-Steuerung

Kernidee: **Keine** sichtbaren D-Pads/Buttons auf dem Retro-Screen. Eingaben werden aus dem Touch-Verhalten *abgeleitet* — und die Dropzone-Physik (analoger Impuls) ist dafür ideal, weil ein gezogener Vektor direkt auf Schub mappt.

### Zonen (per `pointerId` unabhängig, echtes Multitouch)
- **Linke Zone (~55%) — schwebender Analog-Stick.** Touch-Down setzt den Ursprung; Ziehen erzeugt einen Vektor → **horizontaler + vertikaler Schub** (analog, mit Trägheit). Bei Loslassen kein Schub (Schwerkraft übernimmt → realistische Landung). Optional ein nur *während Berührung* dezent eingeblendeter Geister-Ring; im Ruhezustand komplett unsichtbar.
- **Rechte Zone (~45%) — Feuer.** Tap = ein Laserimpuls (matcht „jede Knopfbewegung = ein Impuls"); Halten = Auto-Impuls-Strom. Rückwärtsfeuer automatisch, wenn der linke Vektor entgegen der Blickrichtung zeigt (spiegelt die Original-Mechanik).

### Gesten für Spezial-Aktionen
- **Cloak** = beide Daumen gleichzeitig drücken/halten („Schild hoch" — schnell erreichbar, Lebensretter).
- **Strata-Bombe** = Zwei-Finger-Swipe nach unten (bewusst & destruktiv → kein Versehen).
- (Alternativen evaluieren: rechter Doppel-Tap für Cloak, falls Zwei-Daumen-Halten mit Bewegung kollidiert.)

### Haptik (verkauft die unsichtbaren Controls)
`navigator.vibrate`: winziger Tick bei Feuer · mittel bei Aufnahme/Abgabe · stark bei Bombe · Doppel-Tick bei Cloak An/Aus · Schaden. Taktiles Feedback ersetzt die fehlende visuelle Button-Bestätigung.

### Onboarding & Komfort
- Einmaliges, animiertes Tutorial-Overlay beim ersten Start (zeigt die Zonen als „Ghost"), danach unsichtbar. Settings: „Zonen-Hinweise einblenden" für Accessibility.
- **Querformat-Lock**-Prompt (breites Spielfeld). Safe-Area-Insets (Notch). Pointer-Capture gegen verlorene Touches. Performance-Tuning (Partikel-Caps, optional Half-Res-CRT).

---

## 8. Projektstruktur (Single-File)

```
dropzone-hd.html
 ├─ <style>  reset · @font-face(Base64 Retro Gaming) · canvas pixelated · safe-area
 ├─ <canvas id="game">              (offscreen logical render target)
 ├─ <canvas id="crt">               (WebGL display pass)
 └─ <script type="module">
      ├─ ASSETS    inline Sprite-JSON / Base64-Atlas, Palette
      ├─ core/render/world/entities/systems/audio/ui/input  (siehe §2)
      └─ boot()    AudioContext-Unlock bei erstem Input
```
Build-Option: in Dev als mehrere Module entwickeln, per kleinem Inline-Bundler (oder manuell) für Release zu **einer** Datei zusammenführen — passt zu deinem Single-File-Workflow.

---

## 9. Roadmap / Meilensteine

| Phase | Inhalt | Ergebnis |
|---|---|---|
| **0 — Skeleton** | Loop (fixed-step), State-Machine, indexed Framebuffer + Palette, WebGL-CRT-Pass, Font inline | Schwarzer CRT-Screen, Test-Pixel, stabile 60 Hz |
| **1 — Flug** | Player-Physik (Trägheit+Schwerkraft), Kamera, Wraparound-Welt, prozedurale Heightmap, 3 Parallax-Layer | Astronaut fliegt sich „wie Dropzone" über IO |
| **2 — Kampf** | Laser (bidirektional), Planter→Android→Nemesite, Kollision (Spatial-Grid), Explosionen/Partikel | Erste Gegner abschießbar |
| **3 — Rettung** | Menschen, Aufnahme/Abgabe, Dropzone-Plattform, **Scanner**, Richtungspfeil, Hilfe-Pfeifen | Kompletter Core-Loop spielbar |
| **4 — Bestiarium** | Spores/Trailer, Antimatter-Phase, Blunderstorms, Nmeyes, Vulkane, Bomben | Volle Gegner-Vielfalt |
| **5 — Wellen** | WaveManager, 5.-Welle-Lieferung, Trailer-Invasion, Boni, Extra-Leben, Punkte exakt | Endlos-Progression 1–99→95–99 |
| **6 — Audio** | SID-AudioWorklet, SFX-Bank, generative reaktive Musik | Klanglich „high end" |
| **7 — UX** | Menüs, Attract/Demo-KI, Highscore, Juice, Übergänge | Rundes Gesamtprodukt |
| **8 — Mobile** | Unsichtbare Touch-Controls, Haptik, Orientierung, Tutorial, Perf | Voll mobil spielbar |
| **9 — Polish** | Balancing (Feel am Longplay kalibrieren), Accessibility, Purist-Mode, Ship | Release |

---

## 10. Stack-Zusammenfassung & offene Entscheidungen

**Stack:** Single-File HTML5 · Canvas-2D-Indexed-Framebuffer · WebGL-CRT-Shader · Web-Audio-AudioWorklet (SID) · Pointer-Events + Vibration-API · Retro-Gaming-Font (Base64-inline).

**Vor Phase 0 bitte bestätigen:**
1. **Farbzellen-Authentizität** — gelockerte Palette-Freiheit (Default HD) **oder** harte C64-Multicolor-Limits als Default?
2. **Logische Auflösung** — 384×272 vorgeschlagen; alternativ strikt 320×200-Region?
3. **Titel** — Arbeitstitel *IO — Dropzone* behalten, oder gleich originaler Name für Public-Release?
4. **Musik-Default** — generativer SID-Track an (HD) oder Original-treu „keine Musik" als Default mit Toggle?
5. **Mobile Spezial-Gesten** — Cloak via Zwei-Daumen-Halten testen, oder lieber rechter Doppel-Tap?

> **IP-Hinweis:** Originale GFX/Sound (deine), Mechanik-Hommage. „Dropzone" ist ein bestehender Titel — für einen öffentlichen Release eigener Name + Credit „Inspired by Dropzone (1984), Archer MacLean" empfohlen.
