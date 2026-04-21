# Full Documentation: Unity Souls-Like Guide

This document summarizes the gameplay systems and development steps described by the Unity tutorial transcripts. It is intended as a comprehensive, plain-language explanation of what the game does and how the major systems work together.

## Overview

The project is a third-person, single-player Souls-like prototype built in Unity. Core pillars include deliberate player movement, stamina-based combat, lock-on targeting, enemy AI with state-driven behaviors, inventory and equipment management, a souls/leveling progression loop, and checkpoint-based persistence. The series incrementally builds each feature, starting with basic locomotion and camera setup and extending into advanced AI, equipment stats, buffs, and saving.

## Core gameplay loop

1. The player explores a 3D environment with a responsive third-person controller.
2. Combat revolves around timing: attacks, blocks, parries, and dodges consume stamina and require careful spacing.
3. Enemies detect the player, pursue using navigation, and attack using animation-driven state machines.
4. The player gains souls (currency) to level up, improve stats, and equip better gear.
5. Checkpoints (bonfires) provide recovery and progression pacing, while saving preserves the game state.

## Player movement

Movement includes walking, sprinting, rolling, jumping, and falling detection. Rolling uses invulnerability windows and consumes stamina. Jumping and falling include detection to trigger appropriate animations and landing logic. Later improvements refine responsiveness and blending to feel closer to Souls-like locomotion.

Key behaviors:

- Grounded movement with animation-driven locomotion.
- Sprint and roll actions with stamina drain.
- Jump input leading to a jump animation and landing handling.
- Falling detection when leaving ground and recovery on landing.
- Movement improvements to reduce jitter and improve control.

## Camera and targeting

The camera is third-person and follows the player. Camera collision prevents clipping into walls. Lock-on targeting lets the player focus on an enemy, altering movement and camera orientation to keep the target in frame.

Key behaviors:

- Camera orbit around player with collision checks.
- Lock-on toggle to select nearby enemies.
- Target switching and lock-on state management.

## Combat system

Combat uses light/heavy attacks, weapon combos, stamina costs, and animation-driven damage windows. Player and enemy health, poise, and damage absorption influence combat outcomes. Defensive mechanics include blocking, guard break, parry, and riposte. Two-handed weapon modes change move sets and damage.

Key behaviors:

- Light and heavy attack chains with combo timing.
- Damage application based on animation events.
- Stamina drain per action and regeneration rules.
- Rolling invulnerability windows.
- Parry and riposte for high-risk, high-reward counterplay.
- Guard breaking when stamina or block thresholds are exceeded.
- Attack-type modifiers and poise damage.
- Animation canceling for responsiveness (restricted to approved windows).

## Weapons and equipment

Weapons exist as item assets and can be equipped, switched, and used in one- or two-handed modes. Armor pieces (helmet, torso, legs, hands) provide defensive stats and contribute to equipment load, which affects movement. Weapon buffs apply temporary modifiers.

Key behaviors:

- Item-based weapon definitions and stats.
- Equipment slots for weapon and armor pieces.
- Equipment load impacts movement performance.
- Weapon buffs and effect timers.

## Items, inventory, and interactions

Players can pick up items, open lootable chests, consume healing items, and perform item-based actions. Inventory UI displays item lists and stats, while equipment screens manage loadouts.

Key behaviors:

- Item pickup with world interaction prompts.
- Inventory and equipment menus with slot UI.
- Consumable usage (e.g., healing flask).
- Item actions bound to quick slots.

## UI and HUD

The UI includes quick slots, inventory screens, equipment management, and combat HUD elements like enemy and boss health bars. Additional panels present item and weapon stats, and status effects.

Key behaviors:

- Quick slot UI for consumables and actions.
- Inventory and equipment screens with item comparisons.
- Enemy and boss health bars.
- Secondary bars for status buildup and damage indicators.

## Enemy AI

Enemy AI uses perception (field-of-view detection), navigation, and attack behaviors. State machines drive transitions between idle, patrol, chase, attack, and special states (ambush or sleep). Advanced AI features add strafing, pivoting, combos, and patrol paths.

Key behaviors:

- Field-of-view detection and chase initiation.
- Navmesh-based movement and pathfinding.
- Attack selection and combo execution.
- State machines for behavior orchestration.
- Advanced tactics (strafing, pivoting, patrol routes).

## Boss systems

Boss encounters introduce event-driven fights, unique health bars, and multi-phase behaviors. Phase transitions modify attack sets and behavior parameters.

Key behaviors:

- Boss fight trigger events.
- Phase-based behavior changes.
- Dedicated boss health bar UI.

## Progression and currency

Souls act as the primary currency for leveling up. Leveling increases stats and affects combat and survivability. Bonfires act as checkpoints and progression anchors.

Key behaviors:

- Souls collection and spending.
- Level-up flow with stat allocation.
- Checkpoint interaction and recovery.

## Effects and feedback

Visual effects include weapon trails, blood splats, and status effects (poison). Character effects communicate buffs, debuffs, and damage feedback.

Key behaviors:

- Weapon trail VFX on attacks.
- Blood effects on hit.
- Poison buildup and damage over time.
- Character effect handling and display.

## Saving and persistence

Saving uses multiple parts to serialize player state, inventory, equipment, and world progression. Save slots restore the game state on load.

Key behaviors:

- Save data structure for character and world state.
- Load pipeline to restore scene state.
- Integration with checkpoints and progression.

## Audio

Sound effects provide feedback for attacks, impacts, footsteps, and UI interactions.

Key behaviors:

- SFX playback tied to animation events.
- Basic audio manager integration.

## System integration summary

The systems combine into a deliberate combat experience: player input drives movement and combat actions; stamina and poise regulate pacing; AI state machines create readable enemy behaviors; UI surfaces information about status, health, and equipment; and progression systems (souls/leveling) provide long-term motivation. Saving and checkpoints ensure a consistent loop across sessions.

## System-by-system appendix

### Movement and input

- Uses a vector-based movement input and camera input to drive a third-person controller.
- Rolling/backstep share input; if move amount is low, a backstep is triggered instead of a roll.
- Actions are gated by an interaction flag to avoid conflicting animations.

### Combat and stamina

- Light/heavy attacks are animation-driven with damage windows.
- Stamina cost is enforced per action; regen restores stamina over time.
- Defensive mechanics include block, guard break, parry, and riposte.

### Camera and lock-on

- Orbiting camera follows player with collision avoidance.
- Lock-on focuses the camera and movement around a selected enemy.

### Inventory, items, and equipment

- Inventory displays items by type and uses slot UI for selection.
- Weapons can be swapped between left/right hand slots.
- Armor pieces equip to separate slots; equipment load affects movement.

### UI and HUD

- HUD provides health, stamina, and enemy/boss bars.
- Menus provide inventory, equipment, and stat panels.
- Quick slots allow item actions without opening full menus.

### Enemy AI

- Perception uses a detection radius with FOV constraints.
- Behavior is driven by a state machine with attack selection.
- Advanced movement includes pivoting, strafing, and patrol paths.

### Progression and saving

- Souls are collected and spent at level-up screens.
- Bonfires act as checkpoints and saving triggers.
- Save data uses item IDs and serialized stat values.
