# Text Adventure Game — Rebuilt

A web-based RPG rebuilt from scratch. Pick a class, explore locations, fight turn-based combat, gather resources, craft gear, and prestige for permanent progression. Uses Pyscript, HTML, CSS, and a little bit of JS.

**Legacy version:** [text-adventure-game-legacy](https://github.com/Heatthunder/text-adventure-game-legacy)

---

## Quick Start

```bash
python main.py
```

Requires Python 3.11+. No external dependencies.

New players: type `guide` at the travel menu for a full in-game reference covering every system.

---

## Commands (from the travel menu)

| Command | What it does |
|---|---|
| `1`–`10` | Travel to a location |
| `stats` | View character stats and active effects |
| `inventory` | View inventory and use potions |
| `equipment` | View and equip gear |
| `craft` | Craft potions from herbs or weapons from ores |
| `skills` | Spend prestige points on the skill tree |
| `prestige` | Prestige at level 100 (cap: 200) |
| `pshop` | Visit the prestige shop (Prestige 1+) |
| `guide` | Full in-game guide (also accepts `tutorial`) |
| `save` | Save your game |
| `quit` | Save and quit |

---

## Combat

| Action | What it does |
|---|---|
| `attack` | Strike the enemy — verb matches your weapon |
| `defend` | Brace: +50% DEF this turn |
| `dodge` | Agility roll (AGI ÷ 100) to evade the hit |
| `potion` | Use a potion from inventory |
| `1`–`4` | Use a class ability (costs MP) |
| `escape` | Flee the fight (see Escape rules below) |

**Attack verbs** reflect your weapon: *slash* (sword), *stab* (dagger), *shoot* (ranged), *bash* (shield), *punch/kick/elbow* (unarmed). You start unarmed — your fists work fine until you buy a weapon.

**Escape rules:**
- *Overworld* — Agility roll (AGI/100). Success escapes free. Failure still escapes but costs HP, currency, or both (never lethal).
- *Dungeon* — No free roll. Escaping always costs and exits the entire dungeon run.

---

## Locations

| Location | What's there |
|---|---|
| Village | Shop (tier 1), Bank, Rest area, Weapon Chest, Armor Chest, Blacksmith |
| Fields | Herb gathering (1/3/5/10/20 searches), doggie events |
| Forest | Goblins, Bandits, Wolves, Dark Elves, mystery events |
| Mines | Mining minigame (1/3/5/10/20 swings), underground enemies |
| Cave | Orcs, Trolls, Cave Spiders, Stone Golems, mystery events |
| Mountains | Orcs, Trolls, Harpies, Ice Wolves, mystery events |
| Port | Shop (tier 2), Bank, Rest area, Weapon Chest, Armor Chest, Blacksmith, Pirates |
| Dungeon | Gauntlet (requires Mysterious Key) or Endless mode (free) |

**Rest areas** at the Village and Port restore 40% HP and 40% MP for free.

---

## Classes

| Class | HP | MP | ATK | DEF | AGI | Playstyle |
|---|---|---|---|---|---|---|
| Knight | 200 | 35 | 15 | 25 | 8 | Tank — high defense, crowd control |
| Rogue | 110 | 45 | 20 | 10 | 20 | Burst — high attack, mobility |
| Mage | 100 | 100 | 25 | 5 | 10 | Glass cannon — powerful abilities |
| Archer | 120 | 50 | 18 | 15 | 18 | Ranged — balanced with burst potential |

Each class has weapon and armor **proficiencies** that grant bonus stats. Using off-class gear applies a quality-scaled penalty to Agility (and ATK for weapons) — higher quality means a smaller penalty.

---

## Item Quality System

Every weapon and armor piece has a quality tier that multiplies base stats and may add side effects.

| Tier | Qualities | Multiplier | Side Effects |
|---|---|---|---|
| Trash | Worthless, Broken, Terrible | 0×–0.4× | Debuffs |
| Low | Bad, Usable, Normal | 0.6×–1.0× | Minor / none |
| Mid | Good, Great | 1.2×–1.5× | Minor buffs |
| Top | Perfect, Masterwork, Legendary | 1.8×–3.0× | Strong buffs |

**Acquisition sources:** Shops (up to Great) → Blacksmith reforge (up to Perfect) → Dungeon drops (up to Legendary) → Boss / Chest pity (Masterwork/Legendary) → Prestige shop (fixed high quality).

### Universal Items
Items tagged **[Universal]** can be equipped by any class without penalty. They have weaker base stats but carry unique utility bonuses — bonus HP, Agility, or reduced ability costs — that class-specific items don't provide.

### Shields
Shields occupy the weapon slot and provide DEF bonus + damage reduction instead of ATK.
- **Knights** receive a proficiency bonus on shields.
- **Other classes** take an Agility penalty instead of a Defense penalty.
- **Universal bucklers** can be used by anyone with no penalty (weaker DEF than class shields).

---

## Crafting

Use the `craft` command from the travel menu at any time.

### Potions (from herbs gathered in the Fields)

| Herb | Potion |
|---|---|
| Pure Arlife Herb | Health Potion |
| Arcane Blue Flower | Mana Potion |
| Interesting Mutated Flower | Suspicious Potion |

Crafted potions receive a **craft quality** (Bad → Pure) rolled at brew time. Higher quality = stronger effect and better Suspicious Potion odds. Pure quality gives 85% chance of a positive outcome. Crafted potions cannot be sold.

### Weapons (from ores mined in the Mines)

| Ore | Craftable weapons |
|---|---|
| Stone | Tier 1 class weapons |
| Copper Ore | Tier 1 universal weapons |
| Iron Ore | Tier 2 class weapons |
| Maglite Copper | Tier 2 universal weapons |
| Maglite Iron | Tier 2 heavy weapons |
| Pure Maglite | Tier 3 weapons |

Crafted weapon quality is rolled from the `craft_weapon` table (can reach Perfect).

---

## Currency

**100 Copper = 1 Silver | 100 Silver = 1 Gold | 100 Gold = 1 Platinum**

The Bank accepts deposits and earns **0.3% interest** per visit. Convert between denominations individually or in bulk in either direction.

---

## Death & Respawn

The game auto-saves a **checkpoint** every time you enter a location. When you die:
- You're offered the chance to respawn from your last checkpoint.
- Respawning restores full HP and MP.
- **80% chance** to lose a small amount of currency (5–15% of wallet) — someone went through your pockets.
- If no checkpoint exists or you decline, it's a permanent game over, and the save is deleted.

---

## Prestige System

Reach level 100 to prestige (level cap is 200; you can prestige again after re-reaching 100 each time).

**What resets:** Level and base stats.  
**What carries over:** Currency, inventory, equipment, skill ranks.

Each prestige:
- Awards prestige points to spend on the skill tree
- Makes the world harder (+15% enemy stats per prestige rank)
- Unlocks higher dungeon tiers

### Skill Tree Categories
- **Combat** — Crit chance, lifesteal, bonus damage
- **Defense** — Damage reduction, HP regen between fights, max HP
- **Economy** — Better loot quality, shop discounts
- **Utility** — XP bonus, dungeon reward upgrades

### Dungeon Tiers

| Tier | Unlock | Floors | Boss examples | Loot |
|---|---|---|---|---|
| 1 — Challenge | Always | 3 | King Skeleton, King Ogre | Dungeon quality |
| 2 — Veteran | Prestige 1 | 4 | Bone Dragon, Lich King | Dungeon quality |
| 3 — Elite | Prestige 3 | 5 | Ancient Lich, Stone Giant | Boss quality |
| 4 — Legendary | Prestige 5 | 6 | Ancient Dragon, Void God | Boss quality |
| Endless | Always | ∞ | No boss | Scales with depth |

Dungeon enemies are level-scaled with a 15% chance to be **Elite** (1.5× stats, 2× XP). Bosses scale an additional 1.3×. Floor events can occur between floors — helpful, harmful, or neutral.

**Endless Dungeon** requires no key, has no boss, and scales enemy strength by 5% per floor. Events appear frequently and platinum rewards drip in every 5 floors.

---

## Save Files

Saves are stored in `saves/` as named JSON files. Checkpoint files live alongside them as `slotname_checkpoint.json`. Multiple save slots are supported. The folder is created automatically on first save.

**Current save version: 3**

> Save version 3 is not compatible with version 2 or earlier saves. Delete the `saves/` directory before loading an old save.

---

## Planned / Up Next

See [`changelogs/main-changelog.md`](changelogs/main-changelog.md) for the full milestone tracker.

**Milestone 5 — Web:**
- PyScript + HTML/CSS UI replacing terminal display
- Browser input events replacing `input()` calls
- Save data via localStorage

**Future content (no milestone set):**
- Rare world events at higher prestige ranks
- Skill-tree upgrades for crafting quality
- Enemy variants with unique abilities per enemy type
- Additional locations: Ancient Ruins, Cursed Forest

## License Summary

This project uses a custom **Community Copyleft License** (`LICENSE.md`), not an OSI open-source license.

- The project is fully copyrighted by default; no rights are granted except what the license explicitly allows.
- You may read, study, and run the game for personal, non-commercial use, and you may create private derivative works that you do not distribute.
- If you distribute a mod/derivative, distribution is limited to the license's **Approved Spaces** (official Discord and official itch.io community page).
- Shared derivative works must always be free, use the same license terms, include source form (or a free written source offer), and clearly state your changes.
- Attribution is required: credit the original author (Heatthunder), keep existing notices, and do not imply your version is official or endorsed.
- You may not use the project commercially, relicense/sublicense it, claim authorship of the original work, or distribute outside Approved Spaces without prior written permission.
- The license includes an "as-is" no-warranty / limited-liability clause.
- Rights terminate automatically on license violation, and all rights not explicitly granted are reserved by the author.

For full legal terms, read [`LICENSE.md`](LICENSE.md).
