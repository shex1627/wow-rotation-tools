# WoW Class Tools

Guides and interactive rotation trainers for World of Warcraft specs, built for patch 12.1 (Midnight Season 2).

**Live site:** enable GitHub Pages (Settings → Pages → Deploy from branch → `main`, folder `/docs`) and the site serves from `https://<username>.github.io/wow-class-tools/`.

## What's here

```
docs/
  index.html                    # landing page
  frost-dk/
    guide.html                  # beginner guide (multi-source validated)
    rotation-quiz.html          # Cooldown Manager configurator + rotation quiz
```

### Frost Death Knight guide
Cross-checked against four sources: Method.gg, Icy Veins, Obli's Season 2 YouTube guide, and real Warcraft Logs data (top parses across 3 Mythic+ dungeons and all 5 heroic-logged raid bosses). Disagreements between sources are flagged inline rather than silently resolved.

### Rotation quiz
- Mirrors Blizzard's in-game Cooldown Manager UI (added 11.1.5): buffs row, rune grid, Runic Power bar, ability row with resource/cooldown shading, cooldown swipes, and WoW-style tooltips.
- Ability icons come from Warcraft Logs' own `gameData.ability(id).icon` API field, served via the Wowhead icon CDN (same Blizzard filenames).
- Quiz scenarios are drawn from a weighted distribution calibrated against real cast counts from top-ranked logs (single-target: heroic raid parse; AoE: #1 Mythic+ parse), so correct answers appear at roughly real-play frequencies.
- Target selector: 1 / 2 / 5, with correct threshold handling (Frostscythe at 2+, Glacial Advance at 3+).
- Burst-window coherence: Reaper's Mark teaches "cast before Pillar"; Pillar + Breath accept either click when macro'd together; mid-Pillar states gray both out and show Pillar as an active buff with remaining duration.

## Adding a new spec

1. Create `docs/<spec-slug>/` with `guide.html` and (optionally) `rotation-quiz.html`.
2. For a quiz: copy `frost-dk/rotation-quiz.html` as the template. The pieces to replace:
   - `ABILITIES` table — pull icon filenames from the Warcraft Logs GraphQL API (`gameData { ability(id: X) { name icon } }`).
   - `COST` / `CD_DEF` — the spec's resource model.
   - `correctAbility()` — the priority list, from Method/Icy Veins, ideally sanity-checked against a top log's actual cast sequence.
   - `SCENARIO_WEIGHTS` — cast counts from a representative top parse per bracket (query the `Casts` table filtered to rotational ability IDs).
3. Add a card to `docs/index.html`.

## Data sources & disclaimers

Ability icons and names are property of Blizzard Entertainment. Guide content synthesized from public guides (Method.gg, Icy Veins, YouTube) with per-section attribution inside the pages. Log data via the Warcraft Logs public API. Not affiliated with Blizzard, Method, or Warcraft Logs.
