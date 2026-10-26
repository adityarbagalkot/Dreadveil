# Dreadveil Adventures — Rules

Canonical target-design reference for the UI and rules. These documents specify intended behavior; they do not imply that the game engine has implemented it.

## Documents
- [Core Dice System](core/dice-system.md)
- [Turn Flow and Resolution](core/turn-flow.md)
- [Enemy Intent and Visibility](core/enemy-intents.md)
- [Twenty-Character Roster](characters/roster.md)
- [Character Ability Contracts](characters/abilities.md)
- [Character Mechanics Audit](characters/mechanics-audit.md)
- [Character Profiles](characters/profiles.md)
- [Machine-Readable Character Data](characters/character-data.json)
- [Character Visual Standards](characters/visual-standards.md)
- [Character Balance Review](characters/balance-review.md)
- [Encounter Baselines](encounters/encounter-baselines.md)
- [Testing and Balance](testing/testing-and-balance.md)

## Locked design pillars
1. Every turn uses all six combat dice: d4, d6, d8, d10, d12, and d20.
2. Every die must be deliberately assigned to Strike or Guard.
3. One standard reroll per turn affects one selected die. The old result is discarded and the new result must be kept.
4. Only the current enemy intent is normally visible. Future intents require an ability.
5. Difficulty is punishing: several mistakes can end a run quickly.
6. The d% is a utility die, not a combat die.
7. No loadout system can replace the six standard combat dice.

## Repository boundary
This is the UI/design reference repository. Keep game source code in the implementation repository. The existing implementation is reference material, not proof that these rules are already implemented.
