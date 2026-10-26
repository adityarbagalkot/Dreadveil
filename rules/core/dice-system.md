# Core Dice System

## Combat pool

Every turn provides exactly one of each standard combat die.

| Die | Faces | Rule |
|---|---:|---|
| d4 | 4 | When assigned to Guard, adds +1 Guard after its rolled value. |
| d6 | 6 | No inherent modifier. |
| d8 | 8 | No inherent modifier. |
| d10 | 10 | No inherent modifier. |
| d12 | 12 | No inherent modifier. |
| d20 | 20 | Natural 1 contributes 0; natural 20 contributes 25. |

The d% is a utility die and is never part of the combat pool.

## Valid rolls
- A normal result is an integer from 1 through that die's face count.
- Keep the die identity attached to its result.
- Apply the d20 special rule when calculating its contribution; do not rewrite its stored roll.
- Reject missing, extra, fractional, or out-of-range results. Never silently coerce invalid rolls.

## Assignment
Each die must be deliberately assigned to exactly one role:
- **Strike** contributes to the player's attack total.
- **Guard** contributes to the player's defense total.

No die can fill both roles or remain unassigned at resolution. Assignment must be explicit; do not treat a default Strike assignment as a completed player choice. No dice loadout or equipment system may replace these six dice.

## Rerolls
- Each turn grants one standard reroll.
- A standard reroll targets exactly one selected die.
- Discard the old result and replace it with a fresh legal roll.
- The new result must be kept; the discarded result cannot be restored.
- Abilities may grant explicitly defined additional rerolls.
- Oracle grants two extra single-die rerolls this turn.
- Sylvius Moonrift may reroll up to two selected dice without spending the standard reroll.

## Totals
Calculate each die's contribution using its own rules, then sum by assignment. Apply ability modifiers in their specified timing window. The d20 natural 1 contributes zero and natural 20 contributes 25 in either role. Guard is floored at zero after penalties.

## UI requirements
Show all six dice, their types and results, assignment controls, remaining rerolls, and assignment completeness. Prevent resolution until every die has an explicit role. Do not show a loadout picker or imply the dice can be swapped.
