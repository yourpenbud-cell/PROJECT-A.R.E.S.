@@ -1,2 +1,103 @@
# PROJECT A.R.E.S. 2.0

**Advanced Resource & Environment Simulator — Starship Manifest**

An astronaut trainer built for kids: a single-file, browser-based Mars mission
survival game. Players manifest cargo against a strict mass/volume budget,
configure the ship's interior like a real deck plan, then survive 30 Sols on
the surface of Arcadia Planitia while managing oxygen, water, food, power,
radiation shielding, and crew morale.

## Play

No build step, no dependencies. Open the HTML file in any modern browser:

```
A.R.E.S_2.0
```

Or serve it locally:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000/ares_2_1%20(2).html
```

## How the Mission Works

The game runs in three phases:

1. **Manifest & Mass Budget (Pre-Flight)** — Select hardware from a catalog of
   ~25 items (solar arrays, fission units, electrolyzers, hydroponics, radiation
   shields, EVA gear, bulk reserves). Every item deducts mass (24,000 kg budget)
   and cargo volume (60 m³), and feeds live telemetry: power net, O₂, water,
   food, shielding, and morale. Bulk reserves fill tanks directly.
   *Warning: baseline consumables last only 10 Sols — you must manifest
   production systems or reserves to survive the 30-Sol return window.*
2. **Interior Configuration** — Place each crate into a slot on one of three
   decks (Habitat, Science/Greenhouse, Utility/EVA Yard), matching deck zones
   and utility ports (PWR / H₂O / O₂ / LIGHT / DATA / AIR / CH₄). The middle
   aisle must stay clear except for slim gear. Crates can be returned to the
   queue or left on Earth (refunding mass & volume). An auto-place button is
   available.
3. **Surface Operations** — Seal the manifest, land, and run the Sol clock
   (one tick every 3 seconds). Each Sol consumes crew needs and produces
   resources based on installed hardware. Random problems strike — CO₂ scrubber
   saturation, water recycler rupture, dust storms, micrometeorite punctures,
   payload overweight, low morale — and must be solved before the mission ends.
   Collect samples by EVA, analyze them with the spectrometer, and optionally
   confirm a biosignature ("First Contact") via the comms relay.

Win by surviving 30 Sols; your rank (Survivor → Commander, First Contact)
depends on how many mission objectives you complete.

## Training Modes

- **CADET (Easy)** — Guided multiple-choice responses to each crisis, with
  locked options that require specific hardware.
- **FLIGHT DIRECTOR (Hard)** — Free-text solutions judged by AI. With a Gemini
  API key, `gemini-2.5-flash` acts as a "ruthless but fair" mission engineering
  judge (with prompt-injection guardrails); without a key, a local keyword
  judge takes over.

## Live Space Weather (NASA DONKI)

On load, the game queries the NASA DONKI API for solar flares, CMEs, and
solar energetic particles from the past 30 days. Real events seed in-game
hazards (power loss, dust storms, radiation spikes). Falls back to simulated
space weather if offline.

## Optional API Keys

Click the keys button in-game (stored in `localStorage`, never sent anywhere
but the official Google/NASA endpoints):

- **Gemini API key** — enables the AI solution judge, AI-generated mission
  objectives tailored to your manifest, and the AI xenobiology specimen
  generator. All features degrade gracefully to local generators without it.
- **NASA API key** — raises DONKI rate limits (defaults to `DEMO_KEY`).

## Features at a Glance

- Single self-contained HTML file (vanilla JS + CSS, no frameworks)
- Realistic resource interdependencies (e.g., electrolyzers make O₂ from water
  but draw power; a power failure cascades into life support)
- Live telemetry bars, per-Sol operations report, and scrolling mission log
- Text-to-speech voice mode for critical announcements
- Pause/resume and reset controls; keyboard-accessible slots and catalog
- Dust storms, solar particle events, and consequence-driven "follow-up"
  complications caused by your own fixes

## Repository Contents

| File | Description |
| --- | --- |
| `ares_2_1 (2).html` | The complete game (markup, styles, logic) |
| `README.md` | This document |

## Notes for Educators

A.R.E.S. 2.0 teaches trade-off reasoning: every tonne of ascent fuel is a
tonne of greenhouse left on Earth. There is no single correct manifest —
students learn to balance short-term buffers (reserves) against long-term
systems (ISRU, recycling, farming), and every solution carries a cost.
