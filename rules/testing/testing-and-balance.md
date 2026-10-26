# Testing and Balance Plan

## Core rules
- Exactly six combat dice per turn: d4, d6, d8, d10, d12, d20.
- d% never enters the combat pool.
- Every die is explicitly assigned to exactly one role before resolution.
- No loadout path replaces or changes the standard pool.
- Die results are legal integers within each die's range.
- d20 natural 1 contributes zero; natural 20 contributes 25.
- d4 receives +1 only when assigned to Guard.
- One standard reroll targets exactly one die; the replacement result must be kept.
- Oracle's extra rerolls and Sylvius's multi-die reroll obey their own limits.
- Future intent remains hidden unless explicitly revealed by an ability.

## Resolution and status effects
Test exact resolution order, enemy defeat before enemy action, cooldown boundaries, HP-cost restrictions, terminal HP checks, healing caps, poison tick count, corrosion duration, and all ability start/expiry timing. Test cancellation, retaliation, direct damage, damage reduction, and damage conversion separately.

## Every character
For all twenty characters, test data/schema validity, eligibility, successful activation, HP and assignment thresholds, enemy intent branches, each encounter's special mechanic, cooldowns, and status-effect expiry. Run every character against all three encounters.

## Balance metrics
Track win rate by character and encounter, rounds to victory or defeat, HP remaining, damage dealt and received per turn, ability impact, reroll usage, unavoidable-looking defeats, and encounters that a particular ability trivializes or makes nearly impossible.

Test both poor decisions and strong play. The target is punishing, but defeats should be understandable and players should be able to improve.

## Readiness gates
1. All core tests pass.
2. All twenty ability contracts have tests.
3. All encounter special mechanics have tests.
4. No future intent leaks through any UI surface by default.
5. Invalid rolls and incomplete assignments cannot resolve a turn.
6. Simulation outliers have been reviewed.
7. UI wording matches actual engine behavior.
