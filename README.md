# NOVA CORE: Protocol 51

> A cyberpunk, top-down arcade defense game in a **single HTML file**. Defend the Cosmic Eye, draft upgrades, ascend through five stages, and push toward the **God Core**.

No frameworks, no build step, no external assets. Every sprite, effect and sound is generated at runtime with the **HTML5 Canvas 2D API** and the **Web Audio API**.

---

## Play

Open `index.html` in any modern browser. That is all.

```bash
git clone <your-repo-url>
cd <your-repo>
# just open the file
open index.html          # macOS
xdg-open index.html      # Linux
start index.html         # Windows
```

You can also serve it from anywhere that hosts static files, such as GitHub Pages, Netlify or itch.io (upload `index.html` as an HTML5 game).

The game is **mobile-first** (portrait, touch drag) and also works with mouse and keyboard on desktop.

---

## Features

- **The Cosmic Eye core.** A procedurally drawn, multi-layered eye that auto-aims and evolves visually through six stages (`DORMANT`, `AWAKENING`, `DEFENSE STAR`, `FOCUS CORE`, `VOLATILITY PULSE`, `GOD CORE`).
- **Cinematic ascensions.** Each boss gate triggers a roughly 7-second sequence (tap to skip). The battlefield shatters into fragments, a glitch storm hits, the camera zooms into the eye, the new form morphs in, and you dive through the pupil into a hyperspace tunnel. A summoning sigil and a letter-by-letter title follow, all under letterbox bars with a typed terminal caption.
- **Living background.** A baked nebula and vignette, a rotating vortex, a polar radar grid and a warp starfield.
- **13 enemy types** with their own sprites, new types unlocking per stage. Small ones afterburner-dash, medium ones fire bolts, large ones fire bursts, crescent waves and homing spores. All of them telegraph attacks with charge-ups and muzzle flashes.
- **5 bosses, with two forms** at the deeper gates.
- **Rarity card drafts.** Every 3 levels you pick one of three face-down cards, with a shining edge in the rarity colour. Some cards are unstable and can be overcharged.
- **Companions.** Orbs, lancers, wisps, aegis motes and a legendary star that all change their look as they level up.
- **Meta progression.** Spend shards in the Upgrade Hub on permanent augments, skills and cosmetic FX.
- **Death penalty.** Dying keeps only 75% of your permanent augment levels.
- **Procedural audio.** SFX, plus a lookahead-scheduled music sequencer with separate menu, combat, boss and cinematic modes.
- **Local leaderboard.** Callsign login, personal high score and a Top 5, all in `localStorage`.

---

## Controls

| Action | Touch | Desktop |
| --- | --- | --- |
| Aim | Automatic. Drag to override (a gold chevron shows the manual aim) | Automatic. Click and drag to override |
| Nova Burst (ultimate) | Tap the ✸ button | `Space` or the ✸ button |
| Skip ascension cinematic | Tap | `Space` or click |
| Pause | Pause button | `Esc` or `P` |

---

## Progression

### Levels, XP and difficulty
Killing enemies drops XP. Each level gives +3% damage, and enemy health scales with your level, so you have to keep upgrading to keep up. A combo multiplier builds as you chain kills, and every 50 kills triggers **Overdrive**.

### Ascension gates

| Gate | Level | Boss |
| --- | --- | --- |
| 1 | 10 | **Sentinel** (homing fans, then swarms) |
| 2 | 25 | **Hydra** (three heads, swarms) |
| 3 | 50 | **Obelisk** (breakable solar-beam charge), then **Shattered Obelisk** |
| 4 | 75 | **Leviathan** (segmented serpent with a deflectable dash), then **Bone Leviathan** |
| 5 | 150 | **Omega Seraph** (spiral storms, judgment rings, breakable beam), then **Omega Abyss** |

Past level 150 an **Echo** boss returns every 15 levels. The deeper bosses have a second form, with a new health bar, a transformation sequence and swarm attacks.

A *Volatility Spike Detected* warning announces incoming bosses.

### Enemy unlocks by stage

| Stage | New enemies |
| --- | --- |
| Start | drone, runner, mite, tank |
| 1 | weaver, splitter |
| 2 | lancer, bulwark |
| 3 | phantom, hive |
| 4 | wraith, bomber |
| 5 | seraph |

---

## Cards and companions

Every third level you draft one card from three. Cards have rarities (common, rare, epic, legendary). Epics show up fairly often and legendaries are rare. Some cards are **unstable**: tap them 5 times to overcharge them to a higher rarity, with a chance that they stabilize instead. A legendary pick triggers a *Legendary Surge*.

| Card | Effect |
| --- | --- |
| Damage, Fire Rate, Crit, Pierce, Chain, Multishot | Core weapon upgrades |
| Shield, Hull | Survivability |
| Nova | Nova Burst upgrade |
| **Sentinel Orbs** (max 5) | Auto-firing orbs. Tiers: Spark, Prism, Halo, Pulsar, Solar |
| **Star Lancers** (max 3) | Little stars that fire piercing lances |
| **Arc Wisps** (max 3) | Chain-lightning stars |
| **Aegis Motes** (max 4) | Shoot down incoming enemy bullets |
| **Supernova Star** (legendary only) | Five tiers, fires exploding flares |

Each companion's appearance upgrades as you level it.

---

## Upgrade Hub

Shards from runs are spent in the hub between runs. Costs scale steeply, so progress is a long haul.

**CORE** (permanent augments): Core Damage, Fire Cycle, Hull Integrity, Shield Matrix, Regen Capacitor, Targeting Suite, Shard Magnet, Rail Velocity, Fortune Engine, Shard Refinery.

**SKILLS**: Sentinel Orbs, Star Lancers, Arc Wisps, Nova Amplitude, Nova Reactor.

**FX LAB** (cosmetic):

- Shot skins: Plasma Streak, Prism Lance, Inferno Rail, Void Needle, Solar Lance.
- Kill effects: Neon Burst, Glitch Pop, Supernova, Singularity.

### Death penalty
When you die, each permanent augment level is multiplied by **0.75** (rounded). Levels 1 and 2 are not affected. The Game Over screen lists what you lost. Shards and cosmetics are kept.

---

## Tech

- **Language:** vanilla HTML, CSS and JavaScript, in one file of about 3,300 lines and 240 KB
- **Rendering:** Canvas 2D with a cached additive glow sprite, pre-rendered enemy sprites, a baked static background, `shadowBlur` neon and conic gradients
- **Audio:** Web Audio API oscillators, noise bursts, waveshaper distortion and a lookahead step sequencer
- **Assets:** none. There are no images, fonts or audio files.
- **Dependencies:** none

### Persistence (`localStorage`)

| Key | Contents |
| --- | --- |
| `nova51_callsign` | Last used callsign |
| `nova51_leaderboard` | Top 5 scores |
| `nova51_mute` | SFX mute setting |
| `nova51_music` | Music setting |
| `nova51_profile_<NAME>` | Per-callsign profile: shards, high score, augments, skills and cosmetics |

To reset everything, clear the site's `localStorage`.

---

## Browser support

Any current browser with Canvas 2D and Web Audio (Chrome, Edge, Firefox, Safari). Audio starts after the first tap or click, because browsers require a user gesture. It was developed and smoke-tested in headless Chromium at a 390×844 viewport, so please report issues you find on real devices.

---

## Project layout

```
.
├── index.html   # the entire game
└── README.md
```

---

## Roadmap ideas

- Online leaderboard
- More boss forms and Echo variants
- Additional FX Lab skins
- Gamepad support

---

## License

 ## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
