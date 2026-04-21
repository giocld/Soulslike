# Software Design Description (SDD)

## 1. Overview

This SDD describes a Unity-based Souls-like prototype. The architecture centers around gameplay subsystems that coordinate through shared data models (player stats, stamina, inventory) and event-driven animation logic.

## 2. Architecture

### 2.1 High-Level Components

- **Player Controller**: input handling, locomotion, jump/roll/sprint.
- **Combat System**: attack chains, stamina usage, damage resolution.
- **Camera System**: follow/orbit camera and collision handling.
- **Targeting System**: lock-on selection and camera alignment.
- **Inventory & Equipment**: item data, equip slots, usage logic.
- **UI System**: HUD, quick slots, inventory and equipment screens.
- **Enemy AI**: perception, navigation, combat state machine.
- **Boss System**: event triggers, phase logic, boss UI.
- **Progression**: souls currency and level-up flow.
- **Saving System**: serialization and restore.
- **VFX/SFX**: feedback effects for hits and actions.

### 2.2 Data Flow

1. Player input updates controller state and animation parameters.
2. Animation events trigger hit windows, stamina drains, and damage application.
3. Combat events update health, poise, and status effects.
4. UI reads from shared player/enemy state to render HUD and menus.
5. Saving serializes player stats, inventory, equipment, and world state.

## 3. Component Design

### 3.1 Player Controller

Responsibilities:
- Read input and map to movement/roll/sprint/jump.
- Apply movement with animation blending.
- Gate actions based on stamina and states.

Key data:
- Movement speed, sprint speed, stamina cost.
- Grounded/falling states.
- Animation parameters.

### 3.2 Combat System

Responsibilities:
- Manage attack combos and timing windows.
- Apply stamina costs for attacks and blocks.
- Resolve damage using attack data and defense stats.
- Support parry/riposte and guard break.

Key data:
- Attack definitions (damage, stamina cost, animation).
- Damage modifiers by attack type.
- Poise and absorption stats.

### 3.3 Camera System

Responsibilities:
- Orbit and follow player.
- Detect collision and adjust distance.
- Cooperate with lock-on system.

### 3.4 Targeting System

Responsibilities:
- Find nearby targets.
- Maintain lock-on state and update camera focus.

### 3.5 Inventory & Equipment

Responsibilities:
- Store item data and quantities.
- Equip/unequip weapons and armor.
- Provide item actions and consumable effects.

Key data:
- Item definitions and stats.
- Equipment slots and load calculations.

### 3.6 UI System

Responsibilities:
- Render health, stamina, and status bars.
- Provide inventory and equipment screens.
- Present item/weapon/armor stats.

### 3.7 Enemy AI

Responsibilities:
- Perception using FOV checks.
- Navigation via navmesh pathfinding.
- State machine transitions (idle, patrol, chase, attack).
- Advanced behaviors (strafe, pivot, combos).

### 3.8 Boss System

Responsibilities:
- Boss event triggers.
- Phase management with behavior changes.
- Boss health bar integration.

### 3.9 Progression

Responsibilities:
- Track souls and leveling thresholds.
- Apply stat increases.
- Integrate with bonfire checkpoints.

### 3.10 Saving System

Responsibilities:
- Serialize player stats, equipment, inventory, and world flags.
- Load data to restore game state.

## 4. Data Models (Conceptual)

### 4.1 PlayerData

- Health, stamina, stats
- Equipped weapons and armor
- Current souls
- Position (x, y, z)

### 4.2 ItemData

- Type (weapon, armor, consumable)
- Stats and effects
- Icon and description
- Unique item ID for saving

### 4.3 EnemyData

- Health, poise, AI state
- Attack set and behaviors

### 4.4 WeaponData

- Damage values by attack type
- Stamina costs
- Animation references
- Damage absorption values

### 4.5 ArmorData

- Defense/absorption values
- Poise bonus
- Weight

### 4.6 SaveData

- PlayerData
- Inventory list
- World state flags
- Equipped item IDs

## 5. Entity relationships (conceptual)

- PlayerData 1—1 PlayerStats
- PlayerData 1—1 Inventory
- Inventory 1—* ItemData
- PlayerData 1—1 Equipment
- Equipment 1—* EquipmentSlot
- WeaponData and ArmorData extend ItemData
- SaveData references ItemData by ID

## 6. Error Handling

- Invalid item references are ignored and logged.
- Save file read failures fall back to defaults.
- Targeting system clears lock if target is invalid.

## 7. Testing Considerations

- Verify each combat action consumes stamina appropriately.
- Validate AI transitions under different distances and states.
- Ensure save/load restores equipment, stats, and position.
- UI tests for item stats and slot updates.
