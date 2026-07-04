# Hero Defence: Shattered Crown

A 2D base-defense tower defense game with unlockable heroes, synergy bonuses,
a between-wave shop, and persistent progression. Built for mobile and desktop.

## Project Structure

```
hero guard: base defence/
├── project.godot              # Godot project config (autoloads, input, layers)
├── scenes/                    # Scene files (.tscn)
│   ├── level_select.tscn      # Level select / main menu (entry scene)
│   ├── main_game.tscn         # Main game scene (wave gameplay)
│   ├── hero.tscn              # Hero character scene
│   ├── enemy.tscn             # Enemy character scene
│   ├── base.tscn              # Base structure scene
│   ├── projectile.tscn        # Projectile scene
│   ├── health_bar.tscn        # Health bar UI scene
│   ├── damage_number.tscn     # Floating damage number scene
│   ├── death_particles.tscn   # Death particle effect scene
│   ├── upgrade_menu.tscn      # Level-up upgrade selection scene
│   ├── upgrade_option.tscn    # Individual upgrade card scene
│   ├── shop_menu.tscn         # Between-wave shop scene
│   ├── hero_stats_panel.tscn  # In-game hero stat display panel
│   ├── animated_background.tscn
│   ├── procedural_hero_sprite.tscn
│   ├── procedural_enemy_sprite.tscn
│   ├── procedural_base_sprite.tscn
│   └── procedural_projectile_sprite.tscn
├── scripts/                   # GDScript files
│   ├── game.gd                # Autoload — typed container registry
│   ├── logger.gd              # Autoload — centralised logging (GameLog)
│   ├── synergy_system.gd      # Autoload — hero proximity synergy bonuses
│   ├── save_system.gd         # Autoload — persistent progress (Save)
│   ├── level_select.gd        # Level select / main menu logic
│   ├── main_game.gd           # Main game logic + state machine
│   ├── hero.gd                # Hero stats, combat, movement, leveling, synergies
│   ├── enemy.gd               # Enemy AI, pathfinding, boss scaling
│   ├── base.gd                # Base structure logic
│   ├── projectile.gd          # Projectile movement and hit detection
│   ├── health_bar.gd          # Health bar display
│   ├── damage_number.gd       # Floating damage number animation
│   ├── death_particles.gd     # Death particle effect
│   ├── upgrade_menu.gd        # Upgrade selection menu logic
│   ├── upgrade_option.gd      # Individual upgrade card logic
│   ├── shop_menu.gd           # Between-wave shop logic
│   ├── hero_stats_panel.gd    # In-game hero stat display + hold position toggle
│   ├── hero_def.gd            # Hero data resource definition
│   ├── wave_def.gd            # Wave/faction data definition
│   ├── procedural_hero_sprite.gd
│   ├── procedural_enemy_sprite.gd
│   ├── procedural_base_sprite.gd
│   ├── procedural_projectile_sprite.gd
│   └── animated_background.gd
├── data/                      # Game data resources
│   └── heroes/
│       ├── ironclad.tres      # Tank / Fire hero
│       ├── tidecaller.tres    # Artillery / Water hero
│       └── voltex.tres        # Assassin / Electric hero
└── AGENTS.md                  # Development notes for AI assistants
```

## Autoloads

| Name | Script | Purpose |
|------|--------|---------|
| `Game` | `game.gd` | Typed container registry (projectile, enemy, hero, base, health_bar) |
| `GameLog` | `logger.gd` | Centralised logging with configurable levels |
| `Synergy` | `synergy_system.gd` | Hero proximity synergy bonus calculation |
| `Save` | `save_system.gd` | Persistent progress via ConfigFile |
| `Audio` | `audio_manager.gd` | Procedural sound effects and music |

## Controls

### Desktop
- **Left-click**: Select hero / choose upgrade card / buy shop item
- **Right-click** (when hero selected): Move hero to position
- **Space**: Deselect hero
- **H**: Toggle hold position on selected hero (default: ON — press to return to base)

### Mobile / Touch
- **Tap on hero**: Select that hero (tap selected hero again to deselect)
- **Tap on empty ground** (when hero selected): Move hero to that position
- **Deselect button** (stats panel): Deselect current hero
- **Return to Base button** (stats panel): When heroes are holding position (default), press to send them back to base. Press again to hold.
- **One-finger drag**: Pan camera
- **Two-finger pinch**: Zoom camera in/out (0.5x to 2.0x)

## Implemented Features

### Core Systems
- **Game state machine**: PLAYING → WAVE_BREAK (shop) → UPGRADE_MENU → VICTORY / GAME_OVER
- **15-wave level structure** with mini-boss at wave 8 and final boss at wave 15
- **4 enemy factions** (Brute, Swarm, Tech, Stealth) rotating across waves
- **Star rating**: 3 stars (no losses) → 2 (1 loss) → 1 (multiple losses) → 0 (game over)
- **Victory screen** after wave 15 with stars, total stars, and next level button
- **Game over**: Triggers on all bases destroyed OR all heroes dead

### Hero System (6 heroes designed, 3 spawned per level)
- **6 heroes**: Ironclad (Tank/Fire), Tidecaller (Artillery/Water), Voltex (Assassin/Electric), Verdant (Support/Nature), Forge (Engineer/Earth), Pyra (Artillery/Fire)
- **5 roles** (Tank, Artillery, Support, Assassin, Engineer) — all now have heroes
- **5 affinities** (Fire, Water, Electric, Nature, Earth) — all now have heroes
- **Unique passive abilities**: Healing Aura (Verdant), Splash Builtin (Forge), Multishot Builtin (Pyra)
- **Pre-game roster screen**: Pick which 3 heroes to bring into each level
- **Hero unlock progression**: Verdant (3 stars), Forge (6 stars), Pyra (9 stars)
- Homing projectiles; multishot upgrade fans extra shots at 15° spread
- Level-up XP system; upgrade menu pauses game and serialises concurrent level-ups
- **One upgrade menu per wave** — player picks which hero gets the full upgrade
- **17 upgrade types** in 3 categories (offense, defense, utility) including: Damage, Attack Speed, Range, Crit Chance, Crit Damage, Multishot, Splash, Pierce, Chain Lightning, Max Health, Armor, Regen, Thorns, Move Speed, Lifesteal, Frost
- **Rarity system** — each upgrade roll is Common (60%, 1x), Rare (30%, 1.5x), or Epic (10%, 2x) with color-coded borders and glow
- **Procedural card icons** — each upgrade has a unique hand-drawn polygon icon (sword, lightning, shield, heart, snowflake, etc.)
- **Card animations** — staggered entrance, hover scale/glow, selection flash with particle burst
- **Hold position toggle** — heroes stay where placed for synergy setups

### Hero Synergy System
- Heroes within 300px activate passive bonuses (15 unique pair synergies — all C(6,2) combinations)
- Bonuses stack when heroes are clustered
- Visual cyan aura on heroes with active synergies
- Synergy info shown in hero stats panel
- Key synergies: Vanguard, Overdrive, Storm, Bastion, Inferno, Cataclysm, and 9 more

### Boss System
- **Mini-boss** (wave 8): 4x health, 1.5x damage, tier 1, +25 bonus XP, +20 bonus gold
- **Final boss** (wave 15): 8x health, 2x damage, tier 2, +50 bonus XP, +40 bonus gold
- Boss enemies have scaled procedural sprites and wider health bars

### Shop System (between waves)
- Gold earned from kills (2 + wave number per kill, boss bonus gold)
- 4 random items offered per shop visit from a pool of 9
- Items: Heal Heroes, Repair Bases, Damage/Health/Speed/Range/Crit/Regen/Haste Boost (permanent)
- Costs scale slightly with wave number
- **Procedural item icons** — each item has a unique polygon icon (sword, shield, heart, etc.)
- **Category-colored card borders** — offense=red, defense=blue, support=green, utility=gold
- **Purchase effects** — scale punch, white flash, colored sparks, gold coins flying out
- **Animated gold display** — coin icon pulses, gold count counts up/down smoothly
- "Continue to Next Wave" button proceeds after shopping

### End-of-Level Screens
- **Victory screen** with animated 5-pointed star ratings (pop in one by one with sparkles)
- **Gold reward** on level complete: `stars * 20 + waves * 5` gold
- **Stats summary** — waves cleared, bases/heroes survived, total gold, total stars
- **Hero unlock animation** — star pops in with sparkles when a new hero is unlocked
- **Victory particle burst** — 20 golden sparkles radiate from the panel
- **Game over screen** with dramatic red styling, wave stats, and retry button
- Both screens have entrance animations (fade + scale with back ease)

### Save System
- Persists to `user://save.cfg` via ConfigFile
- Tracks: highest unlocked level, total stars, per-level stars, unlocked heroes
- Auto-saves on victory; stars only update if new best
- Level select screen as main menu with star ratings and lock icons
- "Reset Progress" button for testing

### Enemy System
- **4 factions** (Brute, Swarm, Tech, Stealth) with faction rotation across 15 waves
- **Enemy variety**: ~15% heavy elites (bigger, tankier), ~15% runners (smaller, faster) from wave 3+
- Pathfinding to nearest active base; retargets on base destruction
- Slow effect (from Frost upgrade)
- Boss enemies with scaled stats and visuals
- Stats scale with both wave number AND level number (+15% per level)

### Base System
- **3 base types** (Mountain, River, City) with type bonuses applied to hero damage
- 3 bases per level at fixed positions

### Visual Systems
- Procedural sprites for all entity types (no external art assets required)
- **Detailed hero characters** — each hero is drawn as a unique character with head, body, arms, weapons, and accessories:
  - **Ironclad**: armored knight with helmet, visor, pauldrons, shield, and fire-enchanted sword
  - **Pyra**: fire mage with hood, flowing robe, and staff with flame orb
  - **Tidecaller**: water caster with wave-patterned robe, trident, and water tiara
  - **Verdant**: nature druid with flower crown, leafy robe, and wooden staff with sprouting leaves
  - **Voltex**: electric assassin with ninja mask, hood, dual daggers, and lightning emblem
  - **Forge**: earth engineer with goggles, rocky beard, tool belt, and large hammer
- **Drop shadows** beneath all entities (heroes, enemies, bases) for depth
- **Gradient shading** — vertex colors create top-to-bottom light/dark gradient on all shapes
- **Outlines** — darker outline polygons behind every shape for definition
- **Glow halos** — heroes have a pulsing colored glow based on their affinity
- **Multi-layered affinity auras** — animated element-specific effects (fire wisps, water ripples, electric sparks, nature leaves, earth rocks)
- **Boss auras** — pulsing red (final boss) or orange (mini-boss) glow around boss enemies
- **Hit flash** — enemies flash white when damaged
- **Muzzle flash** — bright flash at hero position when attacking
- **Selection ring** — pulsing golden ellipse under selected hero
- **Move target marker** — expanding golden ring at move destination
- **Synergy lines** — glowing cyan connection lines between synergizing heroes
- **Vignette overlay** — dark screen border for atmospheric depth
- **Ambient particles** — floating firefly-like motes for atmosphere
- **Health bars** — gradient fill, dark border, "ghost" damage delay bar, color-coded by health %
- Floating damage numbers (yellow = normal, red + scaled = critical hit)
- **Floating gold popups** on enemy kills with gold label pulse
- Death particle effects
- **Screen shake** on boss spawns, base destruction, game over, and victory
- **Heal pulse** — green flash on heroes being healed by Verdant's aura
- Hero XP bar and level indicator
- In-game hero stats panel (toggle detailed view, shows synergies + hold position)
- Synergy aura visual feedback
- **Enemy variety visuals** — heavy elites are 1.4x scale, runners are 0.7x scale
- **Improved background** — gradient ground, organic polygon patches, polygon-based clouds, flowers with petals, grass tufts, bushes, horizon line
- **10 unique level biomes** — each level has a completely different background theme:
  1. **Grassland** — green hills, blue sky, fireflies, grass/flowers/bushes
  2. **Desert** — sandy dunes, orange sky, blowing sand, cacti/dead bushes
  3. **Snow** — frozen tundra, pale sky, falling snowflakes, pine trees/ice crystals
  4. **Volcanic** — lava fields, dark red sky, rising embers, volcanic rocks/lava pools
  5. **Forest** — dense woodland, green canopy, green fireflies, trees/mushrooms/ferns
  6. **Ocean** — coastal cliffs, blue sky, sea spray, seashells/coral/driftwood
  7. **Mountain** — rocky peaks, grey sky, falling gravel, rocks/pine trees
  8. **Swamp** — murky marsh, green-grey sky, drifting fog, dead trees/lily pads
  9. **Sky** — floating islands, pink sunset, wind wisps, floating rocks/cloud puffs
  10. **Underworld** — dark cavern, purple glow, soul flames, crystals/bones/dark rocks
- **UI panels** — wave counter, gold label, and star rating have semi-transparent dark panels with rounded borders and text outlines for readability
- **Projectile impact explosions** — expanding shockwave ring + spark particles with gravity on hit
- **Projectile speed stretching** — projectiles stretch in direction of travel based on velocity
- **Improved projectile trails** — circular particles that shrink and fade, positioned in world space
- **Hero attack recoil** — role-specific: tank (heavy kickback), artillery (cannon recoil), support (gentle), assassin (forward lunge), engineer (mechanical kick with rotation)
- **Affinity-specific muzzle flashes** — fire (orange burst + sparks), water (blue splash + droplets), electric (yellow lightning bolt), nature (green bloom + leaves), earth (brown dust + rock chips)
- **Affinity-colored projectiles** — fire=flame shape, water=droplet shape, electric=lightning bolt shape, nature=leaf shape, earth=boulder shape (each with unique colors and gradients)
- **Enemy death animation** — enemies scale down and fade out before disappearing
- **Improved death particles** — 16 varied shapes (diamonds, triangles, squares) with rotation, gravity, drag, and faction-matched colors
- **Base damage states** — bases show cracks and rising smoke when damaged (>60% = clean, >30% = cracked, <30% = critical with dark smoke)
- **Base health bars** — each base has a wide health bar with numeric HP display above it, color-coded (green/yellow/red) with pulsing effect when critical
- **Castle explosion** — bases explode dramatically when destroyed: 3 expanding shockwave rings, central fireball, 20 debris chunks with gravity, 8 rising smoke clouds, white flash. Then the base burns for 5 seconds (6 flickering fire sources + 4 rising smoke plumes + glowing ember patch) before collapsing into a rubble pile (scorched earth, 12 dark rocks, 4 charred chunks, lingering smoke wisps)
- **Affinity-themed bases** — each base visually represents the hero defending it: fire=volcanic fortress with lava, water=island sanctuary with waterfalls, electric=storm spire with lightning rods, nature=ancient tree fortress, earth=mountain stronghold with crystals
- **Arc formation layout** — 3 bases arranged in a defensive arc (center base further back, sides forward), heroes spawn near their corresponding base
- **City windows** — buildings and skyscrapers have grids of lit/unlit windows with gradient shading
- **Animated flag** — mountain base flag waves with sine deformation

### Audio System
- Procedural sound effects — all synthesized in code, no external audio files
- **27 SFX** including:
  - **5 affinity-based attack sounds** — fire (fireball whoosh + crackling embers), water (splash + bubbles + glug), electric (lightning crack + arc buzz), nature (magical chime + leaf whisper), earth (boulder rumble + grinding)
  - Combat: hit impact, projectile whoosh, enemy death, hero hurt, hero death
  - UI: hero select, hero move, button click, button hover
  - Events: level-up, upgrade, shop purchase, boss spawn, elite spawn, synergy activate, wave start, wave complete, victory, game over, base destroyed, base under attack, low health warning
- **Rich sound design** — each SFX uses multiple layers (fundamental + harmonics + sub-bass + noise)
- **Pitch variation** — attack sounds randomize pitch ±15% to avoid repetition
- **Cooldown limiting** — hit_impact, hero_hurt, base_under_attack, projectile_whoosh use rate limiting to prevent audio spam
- **Dynamic music** — 3 intensity levels: calm (between waves), combat (normal waves), boss (faster, darker, G minor with tension layer)
- **Multi-layer music** — bass line + arpeggio melody + pad + percussion per track
- **UI button sounds** — automatically connected to all buttons via `Audio.connect_button_sounds()`
- Volume controls on level select screen (SFX and Music sliders + music toggle)
- Settings persisted via Save system

### Logging System
- Centralised `GameLog` autoload with DEBUG/INFO/WARNING/ERROR/NONE levels
- Per-module filtering (Game, Wave, Spawn, Upgrade, Shop, Hero, Base, Synergy, Save)
- Default level: INFO

## Architecture

- **Autoloads**: Game, GameLog, Synergy, Save, Audio (see table above)
- **Collision layers**: L1=Player, L2=Enemy, L3=Base, L4=Projectile, L5=Structure
- **Data-driven heroes**: Hero stats defined in `data/heroes/*.tres` Resource files
- **Data-driven waves**: Faction rotation and wave templates in `wave_def.gd`

## Planned / Not Yet Implemented

- Co-op multiplayer
- IAP for hero unlocks (server-side receipt validation required)

## Development Notes

- Engine: Godot 4.7, GDScript, GL Compatibility renderer
- Target platforms: Mobile (iOS/Android), Desktop
- Resolution: 1920×1080, canvas_items stretch mode
- No third-party addons currently used
- All UI interactions must work with touch (mobile-first design)
- See `AGENTS.md` for detailed system documentation
