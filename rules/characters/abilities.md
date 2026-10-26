# Character Ability Contracts

These are target descriptions for implementation and balancing. Every ability needs a clear activation window, duration, stacking rule, and expiry condition.

## Original ten

1. **Forge Tank — Forgeguard:** Gain +10 Guard this turn. If the enemy's current attack damages the player, deal 3 scorch damage to the enemy once for that enemy action.
2. **Raven — Void Feint:** Negate the enemy's current action. Default recommendation: cancel its complete action and all attached components.
3. **Plaguewright — Lingering Infection:** Apply poison for 3 damage at the end of each of the next four turns. Recommended: first tick occurs on a later turn, not immediately on application. Stop ticking after enemy defeat.
4. **Oathbreaker — Vengeful Oath:** If the enemy attacks, retaliate for its full declared attack damage, even if the player fully guards it.
5. **Oracle — Threadseer:** Gain two extra single-die rerolls this turn and reveal the next enemy intent, not the full pattern.
6. **Bloodhowl — Blood Frenzy:** Pay 5 HP. Double Strike dice, or triple them if HP is below one-third maximum at activation. Snapshot the multiplier at activation and reject use if the HP cost violates the minimum-HP rule.
7. **Thornwarden — Rootbind:** Prevent the enemy's current action, including secondary effects unless a specific encounter rule marks a component unavoidable. Test carefully because action denial is powerful.
8. **Gear-Saint — Clockwork Overwind:** Existing effect grants a fourth die, which conflicts with the locked six-dice pool. Do not implement the extra die. Redesign the effect to preserve exactly six combat dice.
9. **Dirgesinger — Requiem Reversal:** If the enemy attacks, convert the damage components of that action into healing, capped at maximum HP. Define treatment of status effects separately.
10. **Hollow Star — Perfected Ruin:** Pay 6 HP and set each of the six dice to its own maximum legal face value. Never set every die to the literal value 6. This effect requires careful balance testing.

## Proposed additions 11–20

11. **Borik Thornwall — Quillguard:** Gain +6 Guard. If the current enemy attack damages the player, return 3 damage once during that enemy action.
12. **Kaelen Redtalon — Execution Mark:** Gain +4 Strike damage. After normal Strike resolves, if the enemy has 15 HP or less remaining, deal another 6 damage. Do not apply the bonus if the enemy is already defeated.
13. **Sszareth Mirefang — Armor Rend:** Deal 5 direct damage that bypasses Guard, then reduce enemy Guard by 2 for its next defensive intent. The reduction expires after that defense or combat end.
14. **Ormund Deepdelver — Earthbound Fortress:** Gain +10 Guard and another +3 if at least three dice are assigned to Guard. Count dice, not their values.
15. **Thalric Stormwake — Undertow:** Gain +4 Strike damage and reduce the enemy's next attack by 4, with attack damage floored at zero.
16. **Veyra Cindercrawl — Caustic Sheath:** Reduce enemy Guard by 4 for its next defensive intent. If its next intent is not defensive, gain +4 Strike damage this turn. The engine may inspect the intent, but the UI must not leak it.
17. **Rovan Blackstride — Breakneck Charge:** Gain +8 Strike damage. If the enemy survives the player's Strike resolution, gain +4 Guard for the enemy action this turn.
18. **Nyra Gloamveil — Shadowstep:** Negate damage from the enemy's current attack. If at least three dice are assigned to Strike, gain +4 Strike damage. Default: damage negation does not remove separately described status effects.
19. **Eryndor Palevein — Abyssal Regrowth:** Heal 7 HP, or 10 if below half maximum HP at activation. Snapshot the threshold and cap healing at maximum HP.
20. **Sylvius Moonrift — Slipstream:** Reroll up to two selected dice without spending the standard reroll. Each die may be selected once per activation; new results must be kept.

## Shared contract rules
- Ability availability depends on phase, cooldown, and explicit HP restrictions.
- Distinguish prevention, damage negation, damage reduction, direct damage, retaliation, and damage-to-healing conversion.
- Define whether HP thresholds are checked at activation or resolution.
- A defeated enemy does not take another action.
- No ability silently adds, removes, or replaces any of the six standard combat dice.
- All ability values remain subject to tests and balance simulations.
