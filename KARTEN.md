# Arcane Forge – Vollständige Kartenliste

> Diese Datei ist die zentrale Referenz für alle Karten.  
> Hier kannst du Stats, Fähigkeiten und Beschreibungen anpassen und neue Karten planen.  
> Nach Änderungen: die Werte in `index.html` (BASE_CARDS / COMBO_RECIPES / CARD_EXTRAS) entsprechend aktualisieren.

---

## Seltenheiten

| Symbol | Name | ATK/DEF Multiplikator |
|--------|------|-----------------------|
| ⚪ | Gewöhnlich (common) | ×1.0 |
| 🔵 | Selten (rare) | ×1.4 |
| 🟣 | Episch (epic) | ×1.8 |
| 🟡 | Legendär (legendary) | ×2.5 |
| 🔴 | Mythisch (mythic) | ×3.5 |

## Fähigkeits-Symbole (Badges im Kampf)

| Badge | Bedeutung |
|-------|-----------|
| `SPOTT` rot | **Taunt** – Gegner muss diese Karte zuerst angreifen |
| `🛡` blau | **Schild** – Absorbiert einmal Schaden vollständig |
| `⚡` gelb | **First Strike** – Zerstört Ziel ohne Gegenangriff zu kassieren |
| Element-Icon | **Element** – Aktiviert +3 ATK Vorteil gegen schwächeres Element |

## Element-Vorteile

```
🔥 Feuer  →  ❄ Eis     (+3 ATK)
💧 Wasser →  🔥 Feuer  (+3 ATK)
⚡ Donner →  💧 Wasser (+3 ATK)
❄ Eis    →  ⚡ Donner (+3 ATK)
```

---

## Basiskarten (16)

| ID | Name | Emoji | ATK | DEF | Seltenheit | Typ | Mana | Element | Fähigkeit | Beschreibung |
|----|------|-------|-----|-----|------------|-----|------|---------|-----------|--------------|
| `feuer` | Feuer | 🔥 | 6 | 2 | ⚪ Gewöhnlich | Element | 💎1 | 🔥 Feuer | — | Lodernde Flammen verbrennen alles. |
| `wasser` | Wasser | 💧 | 3 | 6 | ⚪ Gewöhnlich | Element | 💎2 | 💧 Wasser | — | Fließendes Wasser schützt und heilt. |
| `eis` | Eis | ❄ | 4 | 5 | ⚪ Gewöhnlich | Element | 💎2 | ❄ Eis | — | Gefrierender Atem lähmt Feinde. |
| `schatten` | Schatten | 🌑 | 7 | 2 | 🔵 Selten | Element | 💎2 | — | ⚡ First Strike | Finsternis verbirgt dunkle Kräfte. |
| `licht` | Licht | ✨ | 5 | 5 | 🔵 Selten | Element | 💎2 | — | — | Strahlendes Licht blendet alle Bösen. |
| `donner` | Donner | ⚡ | 8 | 2 | 🔵 Selten | Element | 💎2 | ⚡ Donner | ⚡ First Strike | Der Blitz schlägt schnell und vernichtend. |
| `flug` | Flug | 🦅 | 5 | 4 | ⚪ Gewöhnlich | Element | 💎2 | — | — | Schwingst du dich in die Lüfte. |
| `ritter` | Ritter | ⚔ | 5 | 7 | ⚪ Gewöhnlich | Kreatur | 💎2 | — | 🛡 Schild | Schwer gepanzert, unerbittlich im Kampf. |
| `troll` | Troll | 👹 | 7 | 6 | 🔵 Selten | Kreatur | 💎2 | — | SPOTT | Wächter der alten Brücken. |
| `drache` | Drache | 🐉 | 9 | 5 | 🟣 Episch | Kreatur | 💎3 | — | — | König der Lüfte, Meister des Feuers. |
| `geist` | Geist | 👻 | 4 | 3 | ⚪ Gewöhnlich | Kreatur | 💎1 | — | — | Ein Geist aus der anderen Welt. |
| `elfe` | Elfe | 🧝 | 5 | 5 | 🔵 Selten | Kreatur | 💎2 | — | — | Anmutig und geschickt im Bogenschuss. |
| `daemon` | Dämon | 😈 | 8 | 4 | 🟣 Episch | Kreatur | 💎2 | — | ⚡ First Strike | Aus der Unterwelt beschworen. |
| `gnom` | Gnom | 🧙 | 3 | 4 | ⚪ Gewöhnlich | Kreatur | 💎1 | — | — | Klein aber weise, Meister der Runen. |
| `draenei` | Draenei | 🌀 | 6 | 6 | 🟣 Episch | Kreatur | 💎2 | — | — | Ein Wesen aus einer fremden Dimension. |
| `lich` | Lich | 💀 | 10 | 3 | 🟡 Legendär | Kreatur | 💎3 | — | ⚡ First Strike | Der unsterbliche Nekromant, Herr der Toten. |

---

## Kombinationskarten (31)

> Format: `Karte1-ID` + `Karte2-ID` → Ergebnis

### Feuer-Kombinationen

| ID | Name | Rezept | ATK | DEF | Seltenheit | Mana | Element | Fähigkeiten | Fähigkeits-Text | Beschreibung |
|----|------|--------|-----|-----|------------|------|---------|-------------|----------------|--------------|
| `flammenOger` | Flammenoger | 🔥 + 👹 | 18 | 14 | 🟣 Episch | 💎5 | 🔥 Feuer | — | Feuerstoß: Fügt 3 Bonusschaden zu | Ein Oger, den die Flammen des Vulkans geformt haben. |
| `feuerDrache` | Feuerdrachenlord | 🔥 + 🐉 | 24 | 12 | 🟡 Legendär | 💎6 | 🔥 Feuer | — | Flammeninferno: Verbrennt alle Feinde gleichzeitig | Der uralte Feuerdrache, Zerstörer von Königreichen. |
| `feuerElfe` | Flammenelfe | 🔥 + 🧝 | 18 | 12 | 🟣 Episch | 💎5 | 🔥 Feuer | — | Feuerpfeil: Verursacht 2 direkten Schaden | Eine Elfe, deren Pfeile in Flammen stehen. |
| `feuerGnom` | Pyromant | 🔥 + 🧙 | 16 | 8 | 🔵 Selten | 💎4 | 🔥 Feuer | — | Feuerbombe: Verursacht 3 Schaden beim Erscheinen | Ein kleiner Gnom mit großer Leidenschaft für Feuer. |

### Wasser-Kombinationen

| ID | Name | Rezept | ATK | DEF | Seltenheit | Mana | Element | Fähigkeiten | Fähigkeits-Text | Beschreibung |
|----|------|--------|-----|-----|------------|------|---------|-------------|----------------|--------------|
| `tiefseeDrache` | Tiefseedrache | 💧 + 🐉 | 18 | 16 | 🟡 Legendär | 💎5 | 💧 Wasser | — | Tidenwelle: Weist 2 Schaden pro Zug ab | Aus den tiefsten Ozeanen der Urzeit aufgestiegen. |
| `wasserElfe` | Meeresnymphe | 💧 + 🧝 | 13 | 17 | 🔵 Selten | 💎5 | 💧 Wasser | — | Heilstrom: Heilt 3 LP wenn sie das Feld betritt | Eine anmutige Elfe der Ozeane und Flüsse. |
| `wasserGeist` | Wassergeist | 💧 + 👻 | 10 | 15 | 🔵 Selten | 💎4 | 💧 Wasser | 🛡 Schild | Spiegelung: Reflektiert 1 Schaden | Ein Geist, der in stillen Wassern lebt. |
| `wasserRitter` | Meeresritter | 💧 + ⚔ | 14 | 21 | 🟣 Episch | 💎5 | 💧 Wasser | 🛡 Schild | Wellenpanzer: Halbiert eingehenden Schaden einmal | Ein Ritter der Meere, sein Schild ist aus Korallenriff. |

### Eis-Kombinationen

| ID | Name | Rezept | ATK | DEF | Seltenheit | Mana | Element | Fähigkeiten | Fähigkeits-Text | Beschreibung |
|----|------|--------|-----|-----|------------|------|---------|-------------|----------------|--------------|
| `eisRitter` | Eisritter | ❄ + ⚔ | 14 | 20 | 🟣 Episch | 💎5 | ❄ Eis | SPOTT | Eispanzer: +3 DEF für 2 Runden | In Eis gehüllt, unzerstörbar wie ein Gletscher. |
| `eisGeist` | Frostgeist | ❄ + 👻 | 12 | 12 | 🔵 Selten | 💎4 | ❄ Eis | — | Einfrieren: Feind überspringt nächsten Zug | Ein Geist aus dem ewigen Frost, der alles erstarren lässt. |
| `eisDaemon` | Frostdämon | ❄ + 😈 | 20 | 14 | 🟡 Legendär | 💎5 | ❄ Eis | ⚡ First Strike | Absoluter Frost: Verringert alle feindlichen ATK um 2 | Ein Dämon aus den tiefsten Eisgrotten der Unterwelt. |
| `eisDrache` | Gletscherdrache | ❄ + 🐉 | 20 | 19 | 🟡 Legendär | 💎6 | ❄ Eis | SPOTT | Eishauch: Friert Feinde für 1 Runde ein | Ein uralter Drache aus dem ewigen Eis der Polarregion. |

### Donner-Kombinationen

| ID | Name | Rezept | ATK | DEF | Seltenheit | Mana | Element | Fähigkeiten | Fähigkeits-Text | Beschreibung |
|----|------|--------|-----|-----|------------|------|---------|-------------|----------------|--------------|
| `sturmAdler` | Sturmadler | ⚡ + 🦅 | 22 | 9 | 🟣 Episch | 💎5 | ⚡ Donner | ⚡ First Strike | Blitzangriff: Trifft zuerst in jeder Runde | Ein majestätischer Vogel, der Blitze schleudert. |
| `donnerTroll` | Gewittertroll | ⚡ + 👹 | 22 | 16 | 🟣 Episch | 💎6 | ⚡ Donner | SPOTT | Donnerbrülle: Reduziert feindliche DEF um 2 | Ein Troll, der von Blitzen durchzuckt wird. |
| `donnerDrache` | Sturmdrache | ⚡ + 🐉 | 26 | 14 | 🔴 Mythisch | 💎6 | ⚡ Donner | ⚡ First Strike | Blitzsturm: Greift alle Feinde auf dem Feld an | Der mächtigste Drache des Himmels. |
| `donnerGnom` | Gewittergnom | ⚡ + 🧙 | 18 | 10 | 🔵 Selten | 💎4 | ⚡ Donner | — | Statikfeld: Feindliche ATK -1 für 2 Runden | Ein Gnom, der die Kraft des Blitzes kanalisiert. |

### Schatten-Kombinationen

| ID | Name | Rezept | ATK | DEF | Seltenheit | Mana | Element | Fähigkeiten | Fähigkeits-Text | Beschreibung |
|----|------|--------|-----|-----|------------|------|---------|-------------|----------------|--------------|
| `phantomFuerst` | Phantomfürst | 🌑 + 👻 | 20 | 10 | 🟡 Legendär | 💎5 | — | ⚡ First Strike | Schattenschritt: Angriffe können nicht geblockt werden | Eine Seele aus reiner Dunkelheit, kaum wahrnehmbar. |
| `schattendaemon` | Schattendämon | 🌑 + 😈 | 26 | 10 | 🔴 Mythisch | 💎6 | — | ⚡ First Strike | Seelenraub: Zieht 1 Karte extra | Ein Dämon der obersten Finsternis, gefürchtet in allen Welten. |
| `schattengnom` | Dunkelgnom | 🌑 + 🧙 | 16 | 11 | 🔵 Selten | 💎4 | — | — | Unsichtbarkeit: Kann nicht als Ziel gewählt werden | Ein Gnom der dunklen Künste, Meister der Illusion. |
| `schattenFlug` | Nachtfalke | 🌑 + 🦅 | 19 | 9 | 🔵 Selten | 💎4 | — | ⚡ First Strike | Nachttaucher: Greift zweimal an | Ein Vogel des ewigen Schattens, schnell wie die Dunkelheit. |

### Licht-Kombinationen

| ID | Name | Rezept | ATK | DEF | Seltenheit | Mana | Element | Fähigkeiten | Fähigkeits-Text | Beschreibung |
|----|------|--------|-----|-----|------------|------|---------|-------------|----------------|--------------|
| `lichtElfe` | Lichtelfe | ✨ + 🧝 | 15 | 15 | 🔵 Selten | 💎4 | — | — | Heilung: Regeneriert 2 LP des Spielers | Von heiligem Licht umhüllt, eine Hüterin des Waldes. |
| `lichtRitter` | Paladin des Lichts | ✨ + ⚔ | 17 | 18 | 🟣 Episch | 💎5 | — | 🛡 Schild | Heiliger Schild: Absorbiert einmal Schaden vollständig | Ein heiliger Krieger, gesegnet vom Gott des Lichts. |
| `lichLicht` | Heiliger Verderber | 💀 + ✨ | 22 | 16 | 🔴 Mythisch | 💎6 | — | — | Heilige Vernichtung: Zerstört eine feindliche Karte sofort | Eine Paradoxie aus Leben und Tod, allein sein Anblick tötet. |

### Kreatur-Kombinationen

| ID | Name | Rezept | ATK | DEF | Seltenheit | Mana | Element | Fähigkeiten | Fähigkeits-Text | Beschreibung |
|----|------|--------|-----|-----|------------|------|---------|-------------|----------------|--------------|
| `runengnom` | Runengnom | 🧙 + ✨ | 11 | 13 | 🔵 Selten | 💎4 | — | — | Runenmagie: Nächste Karte kostet kein Tempo | Ein erleuchteter Gnom mit magischen Runen an den Händen. |
| `trollDaemon` | Höllenoger | 👹 + 😈 | 24 | 18 | 🟡 Legendär | 💎6 | — | SPOTT | Dämonenwut: +5 ATK wenn HP unter 15 | Ein Troll, der dem Teufel seine Seele verkauft hat. |
| `trollRitter` | Urkrieger | 👹 + ⚔ | 19 | 19 | 🟣 Episch | 💎6 | — | SPOTT | Unzerbrechlich: Erleidet nie mehr als 6 Schaden pro Treffer | Ein Troll, der die Kriegskunst der Menschen erlernt hat. |
| `flugLich` | Todesgreif | 🦅 + 💀 | 24 | 10 | 🟡 Legendär | 💎5 | — | ⚡ First Strike | Seelenernter: Tötet eine weitere feindliche Karte | Halb Greif, halb Toter, eine Kreatur des Endes. |
| `draeneiLich` | Lichfürst Draenei | 🌀 + 💀 | 30 | 18 | 🔴 Mythisch | 💎6 | — | ⚡ First Strike | Untod: Wird beim ersten Besiegen wiederbelebt | Der mächtigste Untote, der je existiert hat. |
| `draeneiElfe` | Sternenweberin | 🌀 + 🧝 | 17 | 16 | 🟣 Episch | 💎5 | — | — | Sternenmagie: Zieht 2 Karten | Eine Elfe aus einer anderen Welt, Meisterin der Sternmagie. |
| `flugElfe` | Himmelselfe | 🦅 + 🧝 | 16 | 14 | 🔵 Selten | 💎5 | — | — | Luftstoß: Schiebt Feinde zurück, überspringen einen Zug | Eine Elfe, die auf Adlern durch die Wolken reitet. |

---

## Neue Karte hinzufügen

### Schritt 1: Basiskarte
Füge ein Objekt in `BASE_CARDS` ein:
```javascript
{ id:'MEINE_ID', name:'Name', emoji:'🔮', atk:6, def:4, rarity:'rare', type:'element', desc:'Beschreibung.' }
```

### Schritt 2: Extras definieren
Füge in `CARD_EXTRAS` ein:
```javascript
meine_id: { cost:2, element:'fire', taunt:true, firstStrike:true, shield:true }
// Nur die Felder angeben, die relevant sind
```

### Schritt 3: Kombination definieren (optional)
Füge in `COMBO_RECIPES` ein:
```javascript
{ id:'meineKombi', card1:'id1', card2:'id2', name:'Kombiname', emoji:'🔥💧',
  atk:20, def:15, rarity:'epic', ability:'Fähigkeitstext', desc:'Beschreibung.' }
```
Dazu in `CARD_EXTRAS`:
```javascript
meineKombi: { cost:5, element:'fire', shield:true }
```

### Schritt 4: Kartenbild hochladen
- Datei benennen: `MEINE_ID.png` (exakt die ID aus Schritt 1)
- Format: **PNG, 512×512px** (quadratisch) oder **400×560px** (Karten-Format)
- Hochladen unter: **Supabase Dashboard → Storage → card-images**
- Das Bild erscheint automatisch im Spiel

---

## Statistiken

| Kategorie | Anzahl |
|-----------|--------|
| Basiskarten gesamt | 16 |
| Kombinationen gesamt | 31 |
| Mögliche Kombis | 120 (16×15÷2) |
| Noch nicht verwendet | 89 Kombinationen |
| Mythische Karten | 4 |
| Legendäre Karten | 8 |
| Epische Karten | 10 |
| Seltene Karten | 16 |
| Gewöhnliche Karten | 9 |
