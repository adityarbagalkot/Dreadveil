# Encounter Baselines

These existing encounters are starting inputs for the new ruleset. They have not been balanced against the fixed six-dice system.

## Mire Hound — Apprentice
- HP: 46
- Pattern: Attack 7 → Guard 8 → Attack 5 → Attack 12

## Iron-Bile Gorgon — Veteran
- HP: 52
- Pattern: Corrosive attack 6 → Guard 10 → Petrifying attack 5 → Attack 14
- Corrosion must persist through the intended later Guard calculation. Petrification needs explicit stack, threshold, damage, and expiry rules.

## Cinder-Weaver — Master
- HP: 42
- Pattern: Ignite attack 5 and add 2 embers → Flurry attack 8 → Guard 7 and add 1 ember → Detonation attack 9 plus 2 per ember
- Each die assigned to Guard quenches one ember. Quenching occurs before detonation damage; each Guard die removes at most one ember.

## Visibility
The engine may store full patterns, but the player sees only the current intent by default. Future intent is shown only when an explicit ability reveals it.

## Difficulty target
The game should be punishing without feeling arbitrary. Current threats must be legible; Strike/Guard trade-offs must matter; status effects must be understandable; invalid dice behavior and hidden rule changes are unacceptable.

Re-test all three encounters after changes to dice, rerolls, or abilities. Moving from three selected dice to six fixed dice will materially change damage and defense expectations.
