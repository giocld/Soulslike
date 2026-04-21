# Software Requirements Specification (SRS)

## 1. Introduction

### 1.1 Purpose

Define the functional and non-functional requirements for a Unity-based Souls-like prototype derived from the tutorial series. This SRS supports implementation planning and evaluation.

### 1.2 Scope

The product is a third-person, single-player action RPG prototype with stamina-based combat, lock-on targeting, enemy AI, inventory/equipment systems, UI, progression, and saving.

### 1.3 Definitions

- Souls: in-game currency used for leveling.
- Lock-on: target focus system for camera and movement.
- Poise: resistance to stagger.
- Bonfire: checkpoint system.

## 2. Overall Description

### 2.1 Product Perspective

Standalone Unity project. Systems interact through shared state: player stats, equipment load, stamina/health, and combat events.

### 2.2 Product Functions

- Player movement: walk, sprint, roll, jump, fall detection.
- Combat: light/heavy attacks, combos, stamina costs, parry, riposte, blocking, guard break.
- Targeting: lock-on to enemies.
- Inventory and equipment: pick up, equip, consume items, manage armor.
- UI: quick slots, inventory/equipment screens, HUD bars.
- Enemy AI: perception, navigation, combat behaviors, advanced tactics.
- Boss encounters: phase-based behavior, boss UI.
- Progression: souls currency, leveling, checkpoints.
- Saving: persist player/world state.

### 2.3 User Classes

- Player: end user controlling the character.
- Developer/Instructor: uses Unity editor to build systems.

### 2.4 Operating Environment

- Unity (2019+ assumed by tutorials)
- Desktop platforms (Windows/macOS/Linux)

### 2.5 Design and Implementation Constraints

- Unity physics and animation systems drive movement and combat.
- Inputs mapped to standard controller/keyboard setup.

## 3. Functional Requirements

FR-1 Player Movement
- FR-1.0 The player controller shall use vector-based movement input and camera input to drive locomotion.
- FR-1.1 The player shall move in 3D space with animation-driven locomotion.
- FR-1.2 The player shall sprint while input is held and stamina is sufficient.
- FR-1.3 The player shall roll, consuming stamina and granting temporary invulnerability.
- FR-1.3.1 The roll input shall trigger a backstep when move input is below a threshold.
- FR-1.4 The player shall jump and transition into a landing state on contact.
- FR-1.5 The player shall detect falling and trigger fall/land responses.
- FR-1.6 The system shall gate roll/attack actions while the player is interacting.

FR-2 Camera and Targeting
- FR-2.1 The camera shall follow the player with orbit controls.
- FR-2.2 The camera shall prevent clipping through geometry.
- FR-2.3 The system shall support lock-on to nearby enemies.

FR-3 Combat
- FR-3.1 The player shall perform light and heavy attacks.
- FR-3.2 The system shall support attack combos using timing windows.
- FR-3.3 Damage shall be applied via animation timing events.
- FR-3.4 Stamina shall be consumed for attacks and regenerated over time.
- FR-3.5 The player shall block incoming damage, reducing or negating it.
- FR-3.6 The system shall support guard break when blocking thresholds are exceeded.
- FR-3.7 The system shall support parry and riposte actions.
- FR-3.8 Two-handing shall modify attack behavior and damage.
- FR-3.9 Damage modifiers shall apply based on attack type and stats.
- FR-3.10 Weapon slots shall support cycling through equipped items and skipping empty slots.

FR-4 Items and Inventory
- FR-4.1 The player shall pick up items in the world.
- FR-4.2 The player shall open lootable chests.
- FR-4.3 The inventory shall display items and allow equipping.
- FR-4.4 The player shall consume items (e.g., healing flask).
- FR-4.5 Item-based actions shall be assignable to quick slots.

FR-5 Equipment and Stats
- FR-5.1 The player shall equip armor pieces (head, torso, legs, hands).
- FR-5.2 Equipment shall affect defensive stats and damage absorption.
- FR-5.3 Equipment load shall affect movement performance.

FR-6 UI
- FR-6.1 The UI shall include quick slots and interaction prompts.
- FR-6.2 The UI shall include inventory and equipment screens.
- FR-6.3 The UI shall show enemy and boss health bars.
- FR-6.4 The UI shall show item/weapon/armor stats panels.
- FR-6.5 The UI shall show status effect buildup and damage feedback.
- FR-6.6 UI windows shall be organized as menu panels (HUD vs menu windows).

FR-7 Enemy AI
- FR-7.1 Enemies shall detect the player using field-of-view checks.
- FR-7.2 Enemies shall navigate using pathfinding.
- FR-7.3 Enemies shall attack and use combo behaviors.
- FR-7.4 Enemy behavior shall be managed with a state machine.
- FR-7.5 Advanced behaviors shall include strafing, pivoting, and patrol paths.
- FR-7.6 Enemy attack selection shall use weighted randomness and range/angle constraints.

FR-8 Boss Encounters
- FR-8.1 Boss fights shall trigger event sequences.
- FR-8.2 Bosses shall support phase transitions.
- FR-8.3 Boss UI shall show a dedicated health bar.

FR-9 Progression
- FR-9.1 The player shall collect souls as currency.
- FR-9.2 The player shall level up and increase stats.
- FR-9.3 Bonfires shall act as checkpoints.

FR-10 Saving
- FR-10.1 The game shall save player and world state.
- FR-10.2 The game shall load saved data on startup.
- FR-10.3 Save data shall serialize basic types and item IDs instead of GameObjects.
- FR-10.4 Save slots shall allow multiple character files.

FR-11 Audio
- FR-11.1 Combat and interaction SFX shall play via animation events.

## 4. Non-Functional Requirements

NFR-1 Performance
- The game shall maintain real-time responsiveness (target 60 FPS on desktop).

NFR-2 Usability
- Controls shall be consistent with standard third-person action games.

NFR-3 Maintainability
- Systems should be modular: movement, combat, AI, UI, inventory, saving.

NFR-4 Reliability
- Saving and loading must not corrupt player state.

## 5. Acceptance Criteria (Samples)

- A player can lock on to an enemy and the camera remains focused during combat.
- Rolling grants temporary invulnerability and consumes stamina.
- Enemy AI transitions between idle, chase, and attack states.
- Inventory UI lists items and equips armor/weapons.
- A save created at a bonfire restores player position and stats on load.
