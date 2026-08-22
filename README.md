# Pathfinder 2e (Remaster) Plugin

## Status

**Community / as-is.** Not part of the main Ares code release. CLI-only as shipped; helpers are decoupled so a web portal can be added later without rewriting sheet or policy logic.

## Maintenance

I'm not going to maintain or update this. If you want to take over development, email me at bodyhorrorandcupcakes@gmail.com.

## Overview

Mechanical Pathfinder 2e Remaster support for AresMUSH:

- Character sheets (`sheet`, `sheet/combat`)
- Chargen (`cg/*`) with data-driven `chargen_open` gates
- Advancement (`adv/*`)
- Rolls (`roll`, `roll/job`)
- Money, inventory, and shops
- Spells, focus, and rituals
- Staff tools (`pf2e/set`, `pf2e/reset`, `pf2e/review`)

Catalogs include Player Core, Player Core 2, and Secrets of Magic material under `plugin/data/` (source-split YAML).

## Installation

1. In the game, run:

       plugin/install https://github.com/bodyhorrorandcupcakes/ares-pf2e-plugin

   Replace with the real GitHub URL once the repo is published.

2. Grant permissions on your roles as needed (typical: `manage_pf2e`, `view_sheet`).

3. Ensure the plugin loads so `plugin/data/*.yml` is deep-merged on boot.

4. Optional: edit `game/config/pf2e.yml` for starting wealth, XP, vendor level lock, and shortcuts.

This release has **no webportal** package. The supported surface is in-game CLI.

## Chargen options

Player-visible ancestry, heritage, class, background, and subclass options are gated by:

```yaml
chargen_open: true
```

Missing or non-true = closed for players (staff can still assign via `pf2e/set`). Community data ships with options open; set `chargen_open: false` on any entry you want to hide for your game, then reload.

## Adding books / catalogs

Feats and spells are split by source so files stay manageable:

- `data/feats.yml`, `feats_pc2.yml`, `feats_som.yml`
- `data/spells_*.yml`, `spells_pc2.yml`, `spells_som.yml`

To add another book, drop a new `data/*.yml` with top-level `spells:` or `feats:`, include `source:` and `chargen_open: true` where appropriate, and reload.

## Commands (summary)

| Area | Roots |
|------|--------|
| Chargen | `cg/start`, `cg/ancestry`, `cg/heritage`, `cg/background`, `cg/class`, `cg/commit`, `cg/boost`, `cg/skill`, `cg/feat`, subclass options, … |
| Advancement | `adv/start`, `adv/skill`, `adv/boost`, `adv/feat`, `adv/finish` |
| Sheet / rolls | `sheet`, `sheet/combat`, `roll`, `roll/job` |
| Wealth / gear | `money`, `gear` / `inv`, `shop` |
| Magic | `spells`, `focus`, `refocus`, `rituals` |
| Staff | `pf2e/set`, `pf2e/reset`, `pf2e/review` |

See in-game help under `plugin/help/en/` (`help pf2e`, etc.).

## Config knobs

`game/config/pf2e.yml`:

- `starting_wealth` / `starting_wealth_to` (`purse` or optional `society` ledger)
- `use_encumbrance`
- `xp_to_level`, `scene_xp_enabled`, `scene_xp`
- `vendor_level_lock`, `vendor_level_offset`

## License

Same as [AresMUSH](https://aresmush.com/license). Pathfinder 2e is a trademark of Paizo; this plugin is an unofficial mechanical aid for play on a MUSH and is not affiliated with Paizo.

## Repo layout (Ares installer)

```
ares-pf2e-plugin/
  README.md
  plugin/          # installed as plugins/pf2e/
  game/config/     # merged into game/config/
```

No `webportal/` folder in this release (optional per Ares contribution guidelines).
