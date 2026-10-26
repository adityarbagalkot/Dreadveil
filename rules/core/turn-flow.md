# Turn Flow and Combat Resolution

## Turn phases
1. **Roll:** roll all six standard combat dice.
2. **Reroll:** optionally use available reroll effects within their limits.
3. **Assign:** explicitly assign every die to Strike or Guard.
4. **Ability:** optionally activate an available character ability in its permitted timing window.
5. **Resolve:** calculate Strike and Guard, resolve player damage, ongoing effects, and the enemy's current intent.
6. **Outcome:** determine victory, defeat, or continuation.
7. **Next turn:** if combat continues, roll a fresh six-die pool, restore the standard reroll, advance intent, and update cooldowns and durations.

The UI must show the active phase and prevent invalid actions.

## Resolution order
1. Validate all six dice, reroll state, and completed assignments.
2. Snapshot ability conditions that depend on HP or assignment count at activation.
3. Apply ability modifiers to Strike, Guard, enemy Guard, or attack outcomes.
4. Resolve player Strike against the enemy's active defense.
5. Apply direct damage and ongoing effects at their defined timing.
6. If the enemy reaches 0 HP, declare victory before it takes another action.
7. Apply encounter-specific interactions, such as Guard dice quenching Cinder-Weaver embers.
8. Resolve the enemy's current intent against player Guard and defensive abilities.
9. Apply retaliation, damage conversion, and status effects in documented order.
10. Check player defeat and other terminal conditions.
11. If combat continues, advance the round and intent, update durations and cooldowns, and reset per-turn resources.

When effects share a timing window, use a deterministic documented order, not incidental code order.

## Damage and Guard
Strike dice contribute to Strike; Guard dice contribute to Guard. Enemy Guard reduces Strike and player Guard reduces incoming attack damage according to encounter rules. Direct damage explicitly bypasses Guard. Guard cannot fall below zero after penalties.

## Cooldowns
Cooldowns are measured in turns. Using an ability starts its listed cooldown. Cooldown reduction must occur at one consistent documented point. Tests must prove the earliest turn the ability becomes available again; a cooldown of 3 must not vary by ability due to update order.

## HP and status effects
HP costs occur at activation. Reject use if the cost violates the ability's minimum-HP restriction. Healing cannot exceed maximum HP. HP thresholds must specify whether they are checked at activation or resolution; Bloodhowl's multiplier is snapshotted at activation.

Every status effect defines start timing, effect, duration, whether the application turn counts, stacking or refresh behavior, removal, and behavior after either combatant reaches 0 HP. Corrosion must persist through the intended subsequent Guard calculation instead of expiring immediately.

## Determinism
Given the same initial state, rolls, assignments, ability, and enemy intent, resolution must be deterministic. Randomness should be provided through explicit roll inputs so tests and replays are reproducible.
