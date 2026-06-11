# Arcane Forge – Entwicklerdokumentation

## Projektübersicht

**Arcane Forge** ist ein browserbasiertes Sammelkartenspiel (Single-Page-App).  
Entwickler: Felix Hanschke  
Deployment: GitHub Pages → `https://tcguru030-ux.github.io/Arcane-Forge/`  
Repository: `tcguru030-ux/Arcane-Forge` (Branch: `main`)

---

## Architektur

Die gesamte App besteht aus **einer einzigen Datei**: `index.html`

```
index.html
├── <style>          CSS (alle Styles inline)
├── <body>           HTML-Screens (alle als .screen divs)
└── <script>         JavaScript (alle Daten + Logik)
```

Es gibt kein Build-System, kein npm, keine externen Frameworks außer:
- **Supabase JS v2** (CDN): Auth + Cloud-Speicherung
- **GitHub Actions** (`.github/workflows/deploy.yml`): automatisches Deployment auf GitHub Pages

---

## Deployment

- Jeder Push auf `main` → GitHub Actions deployed automatisch
- Workflow: `.github/workflows/deploy.yml`
- Pages-Quelle: "GitHub Actions" (nicht "Deploy from Branch")

---

## Datenstrukturen

### Karten (`BASE_CARDS`)
```javascript
{ id, name, emoji, atk, def, rarity, type, desc }
```
- `type`: `'element'` | `'kreatur'`
- `rarity`: `'common'` | `'rare'` | `'epic'` | `'legendary'` | `'mythic'`

### Kombinationen (`COMBO_RECIPES`)
```javascript
{ id, card1, card2, name, emoji, atk, def, rarity, ability, desc }
```
- `card1`/`card2`: IDs aus `BASE_CARDS`
- Kombinations-Karten sind "Endformen" (`isEndform: true`)

### Regionen (`REGIONS`)
```javascript
{ id, name, emoji, desc, minLevel, bg, enemies: [...] }
```

### Gegner (innerhalb einer Region)
```javascript
{ id, name, emoji, hp, deck: [cardIds], reward: {xp, gold, cards}, type, diff }
```
- `type`: `'normal'` | `'elite'` | `'boss'`
- `deck`: Array aus Card-IDs (wird doubled: `[...deck, ...deck]`)

---

## Game State (`State`)

```javascript
State = {
  player: { name, hp, maxHp, level, xp, xpNext, gold, wins },
  deck: [cardIds],              // Deck des Spielers (max 35)
  collection: { cardId: count },
  discoveredCombos: [comboIds], // erforschte Kombinationen
  researchQueue: [{ id, startTime }], // laufende Lab-Erforschungen (30 min Echtzeit)
  defeatedEnemies: [regionId_enemyId],
  currentRegion: regionObj,
  currentEnemy: enemyObj,
}
```

---

## Kern-Objekte (JavaScript)

### `Game`
- `newGame()` – neues Spiel, 1 zufällige Startkombination
- `save()` – localStorage + Supabase Cloud
- `saveToCloud()` – nur Supabase
- `loadGame()` – aus localStorage oder Cloud
- `addXp(amount)` – Level-Up-Logik
- `addCard(cardId)` – Karte zur Sammlung hinzufügen
- `showModal(icon, title, body, btn1, btn2, cb1, cb2)` – universelles Modal

### `UI`
- `renderMap()` – Weltkarte rendern
- `showRegion(region)` – Gegnerliste einer Region
- `renderCollection()` – Kartensammlung mit Filtern
- `renderDeckEditor()` – Deck bearbeiten
- `renderCombo()` – Labor rendern (generiert alles via JS)
- `showCardDetail(card)` – Karten-Detailansicht
- `updateHud()` – Topbar + Settings aktualisieren
- `showToast(msg)` – kurze Benachrichtigung unten

### `Lab`
- `startResearch(id)` – Erforschung starten (30 min Timer)
- `forge(id)` – bekannte Kombination herstellen (+1 zur Sammlung)
- `checkResearch()` – abgelaufene Forschungen abschließen
- `_startTimer()` – 1s Interval für Countdown-Anzeige

### `Battle`
- `start(region, enemy)` – Kampf starten
- `playCard()` – Karte aus Hand auf Feld legen (1 pro Zug)
- `startCombo()` – Kombinations-Modus starten
- `attack()` – Angriffs-Auswahl-Modus (selectAttackerMode)
- `_selectAttacker(idx)` – angreifende Karte wählen
- `_executeAttack(enemyIdx)` – Kampfauflösung (simultane ATK vs DEF)
- `endTurn()` – Zug beenden → Gegnerzug startet
- `_enemyTurn()` – Gegner spielt Karte (smart), dann Angriffe
- `_executeEnemyAttacks()` – jede Gegner-Karte greift einmal an (sequentiell mit Delay)
- `_smartEnemyTarget(attacker)` – KI wählt optimales Ziel
- `_finishEnemyTurn()` – zurück zum Spieler-Zug

### `Auth`
- `init()` – Session prüfen beim Start
- `login()` / `register()` – E-Mail/Passwort Auth via Supabase
- `logout()` – Session beenden
- `_loadFromCloud()` – Spielstand aus Supabase laden

---

## Kampfsystem-Regeln

1. **LP**: Spieler startet mit `State.player.maxHp` (100 + 3 pro Level). Gegner mit `enemy.hp`.
2. **Runde 1**: Kein Angriff erlaubt.
3. **Pro Zug**: 1 Karte spielen ODER 1 Kombination, dann mit jeder Karte einmal angreifen.
4. **Pro-Karte-Angriff**: Jede Feldkarte hat `hasAttacked: false`, wird nach Angriff `true`. Reset am Zugbeginn.
5. **Simultaner Kampf**: `newDef = defender.def - attacker.atk`
   - `newDef <= 0` → Karte zerstört, Überschuss geht als LP-Schaden
   - `newDef > 0` → Karte überlebt mit reduzierter DEF
   - Beide Karten berechnen simultan (Angreifer kassiert auch Gegentreffer)
6. **Direktangriff**: Wenn gegnerisches Feld leer → volles ATK als LP-Schaden
7. **Kombis im Kampf**: Nur wenn Kombination in `State.discoveredCombos` vorhanden

---

## Labor-System

- Beim Start: 1 zufällige Kombination aus `COMBO_RECIPES` ist bekannt
- Neue Kombis erforschen: beide Basiskarten müssen in Sammlung sein
- Erforschung dauert **30 Minuten Echtzeit** (`1800000 ms`)
- Timer läuft auch wenn nicht im Labor; beim nächsten Öffnen wird abgeschlossen
- Bekannte Kombis können im Labor hergestellt werden (+1 zur Sammlung)
- Im Kampf-Kombinations-Hinweisstreifen: nur bekannte Kombis

---

## Supabase

- **Projekt-URL**: `https://ebpndnpiuummplxyhqai.supabase.co`
- **Anon Key**: im Code (`SUPA_KEY`)
- **Tabellen**:
  - `profiles`: `id` (uuid, FK → auth.users), `username`
  - `game_saves`: `user_id` (uuid), `save_data` (jsonb)
- **RLS**: aktiviert; jeder Nutzer sieht nur seine eigenen Daten
- **Auth**: Supabase E-Mail/Passwort Auth

---

## CSS-Konventionen

- CSS-Variablen in `:root` für alle Farben (`--accent`, `--purple`, `--red`, etc.)
- Screens: `.screen` divs, nur `.active` ist sichtbar (`display: flex`)
- Animationen: `.animate-fadein`, `.animate-slideup`, `.animate-pulse`, `.animate-shake`, `.animate-combo`
- Seltenheits-Farben: `--common`, `--rare`, `--epic`, `--legendary`, `--mythic`
- Mobile-first, `overflow: hidden` auf body, kein Scrolling auf Root-Ebene

---

## Screen-IDs

| Screen | ID |
|--------|----|
| Login | `screen-login` |
| Hauptmenü | `screen-menu` |
| Weltkarte | `screen-map` |
| Gegnerliste | `screen-enemies` |
| Kampf | `screen-battle` |
| Sammlung | `screen-collection` |
| Deck-Editor | `screen-deck` |
| Labor | `screen-combo` |
| Einstellungen | `screen-settings` |

Overlays: `overlay-modal`, `overlay-carddetail`, `overlay-cardpick`

---

## Neue Features hinzufügen

### Neue Karte
→ Objekt in `BASE_CARDS` Array eintragen.

### Neue Kombination
→ Objekt in `COMBO_RECIPES` Array eintragen (`card1`, `card2` müssen IDs aus `BASE_CARDS` sein).

### Neue Region / Gegner
→ Objekt in `REGIONS` Array. Gegner-`deck` aus `BASE_CARDS` + `COMBO_RECIPES` IDs.

### Neue Fähigkeit im Kampf
→ In `Battle.playCard()` nach dem Spielen prüfen (`c.ability.includes(...)`), oder in `_executeAttack()` für Kampf-Trigger.

### Neuer Screen
1. HTML: `<div id="screen-XYZ" class="screen">...</div>` in Body
2. JS: `showScreen('screen-XYZ')` aufrufen
3. Optional: Nav-Button in der Navbar ergänzen

---

## Implementierte Fähigkeits-Mechaniken

### CARD_EXTRAS Objekt
Jede Karte kann folgende Extra-Felder haben (definiert in `CARD_EXTRAS`):
- `cost: number` – Mana-Kosten (1–6)
- `element: 'fire'|'water'|'ice'|'thunder'` – für Element-Vorteile
- `taunt: true` – Gegner muss diese Karte zuerst angreifen
- `firstStrike: true` – Bei Zerstörung: kein Gegenangriff
- `shield: true` – Absorbiert einmal Schaden vollständig

### Mana-System
- Zug 1: 1 Mana, Zug 2: 2 Mana, ... max 8 Mana
- Karten kosten Mana beim Spielen
- Anzeige im Battle: `💎 X/X`
- Zu teure Karten werden gedimmt angezeigt
- Gegner hat ebenfalls Mana und spielt nur was er sich leisten kann

### Element-Vorteile (`ELEMENT_ADVANTAGE`)
`fire→ice, water→fire, thunder→water, ice→thunder` → +3 ATK Bonus
- Funktion: `elementBonus(attacker, defender)` gibt 0 oder 3 zurück

### Schilde (`shieldActive`)
- Beim Platzieren: `shieldActive = c.shield ? true : false`
- Bei Angriff: wenn `target.shieldActive`, wird Angriff blockiert + `shieldActive = false`
- Auch von KI genutzt

### Taunt
- In `_renderField()`: wenn feindliches Feld Taunt-Karten hat → nur diese als Ziel wählbar
- In `_executeEnemyAttacks()`: KI muss Taunt-Karte angreifen wenn vorhanden

### First Strike
- In `_executeAttack()` und `_executeEnemyAttacks()`: Wenn Angreifer First Strike hat UND Ziel zerstört wird → Angreifer nimmt keinen Gegenangriff

## Offene Feature-Vorschläge (noch nicht implementiert)

5. **DoT (Vergiftung/Brennen)** – Schaden pro Runde
6. **Defensiv-Modus** – +50% DEF, kein Angriff

---

## Version

`v4.0` – Mana-System, Taunt, First Strike, Schilde, Element-Vorteile, Labor-Erforschung, Per-Karte-Angriff, Smart-KI
