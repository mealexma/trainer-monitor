# Pedal Fantasy — Design Document

> Living design notes. Personal prototype; playtest-first, not a commercial roadmap.
> Last updated: 2026-11-08.

## Vision

A first-person dark-fantasy cycling RPG where riding a smart trainer is how the player explores, fights, and completes adventures. The goal is for the player to enjoy the fantasy adventure while naturally getting a satisfying, personally appropriate workout.

Design principles:
- **Fun first.** Exercise should feel embedded in play rather than layered on top.
- **Workout intent is respected.** Surprise in story and encounters must not unexpectedly exceed the player's selected training intensity.
- **Progress through fantasy.** Travel, enemies, quests, gear, and bosses should form a coherent journey.
- **Personal project, iterated by real rides.** Keep the prototype small and validate its feel rather than prematurely building a huge RPG.
- **Preserve the art direction.** Richly detailed AI fantasy, retro first-person framing, intentionally stepped/pixel-art movement.

## Current playtest foundation (implemented or in progress)

- CycleOps Magnus power input and opt-in resistance control.
- Map traversal between fights; travel segments use different durations and low rolling inclines.
- Generated hill profiles for fights, currently up to 3.5% resistance.
- Five-second combat exchanges based on average wattage within each window.
- Riding near the baseline inflicts damage; pushing above it adds damage; dropping below it can cost HP.
- Focus gained from early victories; Arcane Shield spends 50 Focus to protect against HP loss for 10 seconds.
- Layered backgrounds and enemy idle/hurt/attack sprites. The village and swamp are the first art sets.
- A debug phase skip, floating controls, and fullscreen game view.

These are prototype behaviors, not settled balance targets.

## Adventure and story structure (planned)

A **crawl** is a short, authored fantasy adventure with a defined theme, beginning, destination, and finale. Examples: a village overcome by undead, goblins scaling castle battlements, monster rats in sewers, or dangerous caves and ravines.

The same background should support multiple encounters. A zone might contain two or three themed enemies with different generated hills before the route moves on. Story beats are authored, but individual travel lengths, hills, events, and encounter slots vary between runs.

Example storyline — **Village of the Damned**:
1. Straight road into village outskirts.
2. Skeleton encounters around abandoned homes.
3. Village center and ruined church.
4. Sewer or crypt passage beneath the settlement.
5. Castle approach and final boss (the Grave King).

Potential random story beats: patrol, ambush, shrine, treasure, elite encounter, and an unexpected route change. Randomness changes the fictional experience, but overall workload is constrained by the player's training selection.

## Workout-directed adventure generation (planned)

**Central decision:** the player chooses their desired training experience **before** the adventure begins; the game adapts the same story, terrain, enemy pacing, and combat incentives to that choice. A particular crawl should be playable in different workout styles without needing separately authored storylines.

### Player selections

| Setting | Options | Purpose |
|---|---|---|
| **Training style** | Interval / Endurance / Balanced | Determines effort and recovery pattern |
| **Session duration** | 15 / 30 / 45 minutes | Shapes how much story and how many encounters fit |
| **Personal intensity** | Easy / Moderate / Challenging | Scales effort to the rider's ability rather than using fixed universal watts |

Personal intensity must be derived from a rider-appropriate baseline or calibration, with adjustable safeguards. The current 250 W default is only a prototype setting, not a prescribed target.

### Three training styles

#### Interval — Intense Combat
- More frequent, shorter fights with clearly telegraphed hard efforts.
- Real recovery between bursts; easy travel should not demand constant high power.
- Initial illustration: **30–60 s encounters**, **60–120 s easy travel**.
- Encourage short controlled pushes, then allow the player to back off.
- Avoid random consecutive hard hills without adequate recovery.

#### Endurance — The Long Journey
- Longer scenic travel, fewer fights, sustained comfortable effort and gentle resistance changes.
- Bosses reward consistency over explosive over-target riding.
- Initial illustration: **3–6 min travel**, **90–180 s fights**.
- High wattage should not be required for meaningful progression.

#### Balanced — Adventure (default)
- Mix of exploration, manageable encounters, and occasional harder enemies.
- Preserve the current combat principle: baseline effort can win, extra effort can finish early and earn Focus.
- Initial illustration: **1–3 min travel**, **45–90 s fights**.
- Use as the initial tuning reference when adapting the other styles.

All durations above are *design exploration*, not final workout prescriptions.

### How one story changes

For **Village of the Damned**:
- **Interval:** several skeleton patrols, a short ambush, frequent easy travel, and a boss with short intense windows.
- **Endurance:** longer roads through the village, fewer encounters, longer controlled climbs, and a consistency-oriented Grave King fight.
- **Balanced:** a varied middle ground with travel, patrols, surprise events and a conventional boss encounter.

The storyline and key locations remain recognizable across modes.

### Workout director and safety constraints

An adventure generator should use three layers:
1. **Authored story structure:** named locations, enemy families, story beats, and boss.
2. **Randomized encounter slots:** variant enemies, event types, terrain shapes, travel durations and small route differences.
3. **Workout director:** keeps the session within its chosen time, intensity, effort distribution and recovery budget.

The workout director is authoritative over randomness: no surprise event should force an unexpectedly intense effort. Model effort relative to the user's baseline, cap resistance/intensity appropriately, preserve easy recovery, and make stopping or reducing effort safe. Difficulty should not require overexertion.

## Combat interpretation by training style (planned)

The existing five-second evaluation is a useful base, but scoring can vary by mode:
- **Interval:** telegraphed burst windows, rewards for controlled efforts and adequate recovery.
- **Endurance:** rewards consistency near a comfortable target; pushing hard above target provides little or no advantage.
- **Balanced:** stay on target to defeat foes; push above target to finish faster and earn Focus, with shield as a strategic recovery option.

Keep enemy animations and damage numbers synchronized to the evaluated combat exchange. Calibrate enemy HP, hill length and difficulty together so on-target riding remains viable.

## Exploration and visual presentation

Use a lightweight route map for longer stretches, advancing a marker with cycling effort; this avoids the need for dozens of first-person travel backgrounds. Switch to richly authored first-person backgrounds during battles and important story beats. Reuse scene backgrounds across multiple themed enemies and hills.

Different crawls may give maps distinct designs (castle ramparts, dungeon corridors, cave networks) while sharing the same underlying traversal mechanic.

## Playtest order

1. Continue validating the current five-second combat rhythm, terrain, recovery, shield, and controls during real rides.
2. Build one polished ~20–30 minute crawl with coherent visuals, pacing, events, and a memorable boss.
3. Introduce selectable workout styles in the generator, with **Balanced** as the reference and then Interval/Endurance variants.
4. Add more themes, gear choices, quest lines, and persistent progression only once the core loop remains fun across repeated sessions.

## Open design questions

- How should personal watt/intensity calibration work?
- Should session duration be approximate or tightly bounded?
- How should an interrupted ride or early stop affect story progression?
- How can gear modify strategy without overpowering the workout?
- How will the game safely adapt if a rider is struggling or chooses to ease off?
