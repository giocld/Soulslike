# Entity Diagram (Text)

This is a textual ER-style diagram derived from the transcript content.

```
PlayerData
  - playerId
  - position (x, y, z)
  - currentSouls
  - statsId -> PlayerStats
  - inventoryId -> Inventory
  - equipmentId -> Equipment

PlayerStats
  - maxHealth
  - maxStamina
  - currentStamina
  - poiseValue
  - levelAttributes (str, dex, int, faith, etc.)

Inventory
  - inventoryId
  - items[] -> ItemData

Equipment
  - equipmentId
  - rightWeapon -> WeaponData
  - leftWeapon -> WeaponData
  - headArmor -> ArmorData
  - torsoArmor -> ArmorData
  - legArmor -> ArmorData
  - handArmor -> ArmorData

ItemData
  - itemId
  - itemName
  - itemType (weapon, armor, consumable)
  - icon
  - description

WeaponData (extends ItemData)
  - physicalDamage
  - magicDamage
  - staminaCost
  - attackAnimations[]
  - damageAbsorption
  - poiseBreak

ArmorData (extends ItemData)
  - defenseValues
  - poiseBonus
  - weight

EnemyData
  - enemyId
  - health
  - poise
  - state
  - attackSet[] -> AttackData

AttackData
  - attackId
  - animation
  - damage
  - staminaCost
  - minRange
  - maxRange
  - minAngle
  - maxAngle
  - weight

Bonfire
  - bonfireId
  - isLit
  - position

SaveData
  - slotId
  - playerData
  - inventoryData
  - equipmentData
  - worldFlags
  - bonfireStates
```

## Relationship Summary

- PlayerData 1—1 PlayerStats
- PlayerData 1—1 Inventory
- PlayerData 1—1 Equipment
- Inventory 1—* ItemData
- Equipment 1—* ItemData (Weapons and Armor)
- EnemyData 1—* AttackData
- SaveData embeds PlayerData, Inventory, Equipment, and Bonfire states
