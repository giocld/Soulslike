# Data Dictionary (Draft)

This dictionary maps key entities to fields referenced by the tutorial transcripts.

## PlayerData

- `playerId`: unique identifier
- `position`: world position (x, y, z)
- `currentSouls`: current currency amount
- `statsId`: link to PlayerStats
- `inventoryId`: link to Inventory
- `equipmentId`: link to Equipment

## PlayerStats

- `maxHealth`: maximum HP
- `maxStamina`: maximum stamina
- `currentStamina`: current stamina value
- `poiseValue`: resistance to stagger
- `levelAttributes`: strength/dexterity/faith/intelligence/etc.

## Inventory

- `inventoryId`: unique identifier
- `items`: list of ItemData references

## Equipment

- `equipmentId`: unique identifier
- `rightWeapon`: WeaponData reference
- `leftWeapon`: WeaponData reference
- `headArmor`: ArmorData reference
- `torsoArmor`: ArmorData reference
- `legArmor`: ArmorData reference
- `handArmor`: ArmorData reference

## ItemData

- `itemId`: unique item ID
- `itemName`: display name
- `itemType`: weapon/armor/consumable
- `icon`: UI sprite reference
- `description`: UI text

## WeaponData

- `physicalDamage`: base physical damage
- `magicDamage`: base magic damage
- `staminaCost`: stamina used per attack
- `attackAnimations`: animation references
- `damageAbsorption`: defensive values when blocking
- `poiseBreak`: poise damage or stagger value

## ArmorData

- `defenseValues`: physical/magic/fire/etc.
- `poiseBonus`: poise contribution
- `weight`: equipment load contribution

## EnemyData

- `enemyId`: unique identifier
- `health`: current HP
- `poise`: current poise
- `state`: AI state
- `attackSet`: list of AttackData

## AttackData

- `attackId`: unique identifier
- `animation`: animation reference
- `damage`: damage value
- `staminaCost`: stamina cost for AI (if any)
- `minRange`: minimum distance
- `maxRange`: maximum distance
- `minAngle`: minimum angle to target
- `maxAngle`: maximum angle to target
- `weight`: selection weight

## Bonfire

- `bonfireId`: unique identifier
- `isLit`: activation state
- `position`: world position

## SaveData

- `slotId`: save slot identifier
- `playerData`: embedded PlayerData snapshot
- `inventoryData`: embedded inventory snapshot
- `equipmentData`: embedded equipment snapshot
- `worldFlags`: boss/bonfire/quest progress
- `bonfireStates`: lit/unlit map
