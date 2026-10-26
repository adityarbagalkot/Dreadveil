# Character Mechanics Audit

**Status:** Review document — proposed rulings, not yet approved as final gameplay decisions.

This audit compares the character ability contracts with the shared dice and turn-flow rules. Its purpose is to expose ambiguity before UI or engine implementation. It does not claim the mechanics have been implemented or playtested.

## Executive findings

The roster has 20 defined ability concepts, but several shared timing rules need to be made explicit before implementation:

1. The documented turn flow puts the Ability phase after assignment, while Perfected Ruin says it activates before assignment is locked and Clockwork Overwind says it activates after rolling.
2. The turn-flow resolution order places direct and ongoing damage before the enemy action, but character-specific effects sometimes trigger after an attack or at end of turn. Their relationship to victory and defeat needs one consistent rule.
3. “Declared attack damage” and “attack damage” must be distinct from actual damage after Guard and other reductions.
4. Cooldown duration needs an exact start and decrement rule.
5. Status effects need standard rules for application, ticking, expiry, stacking, and combat end.
6. Multiple effects can modify the same attack, Guard value, or Strike total. Their ordering must not depend on implementation order.

## Proposed shared rulings

The following are recommendations for review, not silently adopted rules.

### A. Use named ability timing windows

Replace the single broad Ability phase with explicit activation windows while preserving the six-die combat pool:

- **Post-roll / pre-assignment:** after all six dice are rolled and rerolls are complete, before assignments are locked.
- **Post-assignment / pre-resolution:** after every die has a declared Strike or Guard assignment, before totals and outcomes are resolved.
- **Resolution trigger:** an automatic effect that fires at a named point; it is not a new player activation.
- **End-of-turn trigger:** an ongoing effect that fires at the documented end-of-turn checkpoint.

Recommended mappings:
- **Clockwork Overwind:** post-roll / pre-assignment or post-assignment / pre-resolution. Choose one consistently; post-assignment is preferable if the +3 should not influence assignment decisions.
- **Perfected Ruin:** post-roll / pre-assignment, as already described.
- **Earthbound Fortress:** post-assignment / pre-resolution, because its bonus checks the number of Guard-assigned dice.
- **Blood Frenzy:** post-assignment / pre-resolution, so the Strike dice are known before its multiplier is applied.
- **Threadseer:** post-roll / pre-assignment; reveal only the next intent in the current planning window.
- **All other manually activated abilities:** post-assignment / pre-resolution unless their design explicitly requires an earlier window.

If an ability is used in a pre-assignment window, the UI must clearly show which choices remain open and prevent resolution until assignment is complete.

### B. Distinguish declared, mitigated, and actual damage

Use these terms consistently:

- **Declared attack damage:** the attack's printed/base damage before player Guard, damage reduction, or damage negation.
- **Mitigated attack damage:** damage remaining after Guard and reductions, before any explicit negation or conversion effect.
- **Actual HP loss:** the amount that reduces the player's HP after all applicable effects.

Recommended mappings:
- **Vengeful Oath:** retaliation equals declared attack damage, as its current contract states.
- **Forgeguard / Quillguard:** trigger only if the player loses at least 1 HP from the current attack; retaliation triggers once per enemy action, not once per hit component.
- **Undertow:** reduce declared attack damage by 4 before player Guard, floored at zero. Confirm whether multi-component attacks count as one attack total or several separately reducible components.
- **Shadowstep:** set current attack damage to zero, but do not remove attached status effects unless separately specified.
- **Requiem Reversal:** convert the attack's would-be HP damage after Guard and reductions into healing. Healing is capped at maximum HP. Attached status effects remain unless explicitly defined as damage.

These choices intentionally distinguish retaliation based on the enemy's declared threat from actual HP loss. Confirm this is the desired design.

### C. Define action cancellation precisely

Recommended shared cancellation contract:

- Cancellation occurs before the enemy action begins.
- It suppresses every component of that action, including its damage, status effects, and action-specific secondary effects.
- It does not remove persistent status effects already applied on earlier turns.
- It does not automatically skip or erase the enemy's next intent; intent advancement follows the encounter's normal sequence.
- If an encounter marks a component as unavoidable, that exception must be declared in the encounter data and visible in the relevant rules.

This applies to **Void Feint** and **Rootbind**. They currently overlap mechanically; keep both only if their cooldowns, costs, or other constraints create a meaningful choice.

### D. Define cooldown counting

The current rules say cooldowns are measured in turns but do not fully specify the exact decrement point.

Recommended rule:
1. When an ability is used, set its remaining cooldown to the listed value.
2. Do not decrement that cooldown during the same turn it was activated.
3. At the end of each subsequent completed turn, decrement the remaining cooldown by one.
4. The ability becomes ready when the remaining cooldown reaches zero, at the start of the next player planning phase.

Write tests for cooldowns 1, 2, 3, and 4. Confirm whether the listed value means the number of full turns the player must wait or the turn number on which the ability returns. The recommendation above treats it as full turns to wait.

### E. Standardize status-effect lifecycle

Every status should carry:
- source
- target
- appliedAt
- firstTickAt
- remainingTicks or a clearly defined expiry
- stackingRule (refresh, stack, or replace)
- tickPhase
- removalConditions

Recommended baseline:
- Poison from Lingering Infection first ticks at the end of the next turn and deals 3 damage on four separate end-of-turn checkpoints.
- If the enemy reaches 0 HP before a later tick, no additional tick is needed.
- Armor Rend's Guard penalty is active for exactly the next defensive intent, then expires even if that defense is cancelled, unless the encounter explicitly says otherwise.
- Corrosion/ember-like encounter statuses must define their order relative to player Strike, Guard assignment, and enemy intent resolution.

### F. Specify zero-HP and simultaneous defeat

Recommended rule:
- After each damage packet, clamp HP to a minimum of zero and check for defeat.
- If the enemy reaches zero from player Strike or a pre-action effect, the enemy does not take its action.
- If a delayed effect defeats the enemy before its action begins, skip that action.
- If a retaliation or damage-over-time effect could defeat both combatants in the same resolution sequence, define one global priority. Recommended priority: resolve the current action's already-started consequences, then evaluate both combatants; if both are at zero, treat the result as a mutual defeat unless the game design explicitly prefers player defeat or victory.

The mutual-defeat policy is a design choice requiring approval.

## Character-specific audit queue

| Character | Unresolved point | Recommended test |
|---|---|---|
| Darius Forgeward | Whether multi-hit attacks trigger one scorch or several | One multi-hit intent; damage on first hit only vs multiple hits |
| Corven Vex | Whether cancellation blocks status and secondary effects | Enemy action with damage plus status plus follow-up |
| Maelis Rotvein | Refresh/stack behavior if poison is reapplied | Apply poison twice before the first tick |
| Serath Oathscar | Declared damage vs actual HP loss for retaliation | High Guard, damage reduction, and negation cases |
| Ilyra Veilseer | Whether foresight remains visible after a reroll or phase transition | Reveal one next intent, advance turn, verify it does not expose the full pattern |
| Garruk Bloodhowl | Exact one-third HP boundary and whether cost is paid before threshold check | HP at one-third minus 1, exactly one-third, and one-third plus 1; reject lethal cost |
| Vaelis Thornwake | Distinction from Corven's cancellation | Same tests as Corven; compare cooldown and constraints |
| Tovin Gearwright | Whether +3 applies before or after the d20 natural-face rule | d20 natural 1, natural 20, and ordinary result; each assignment |
| Elsin Mourningcall | Whether healing is based on damage before or after Guard | Attack partially or fully blocked; healing overflow; attached status |
| Nymor Hollowstar | Six maximum dice and d20 natural-20 contribution | Confirm d20 contributes 25; test Strike-heavy and Guard-heavy assignments; reject lethal cost |
| Borik Thornwall | Trigger on any HP loss vs any attack resolution | Fully blocked attack, 1 HP loss, multi-hit attack |
| Kaelen Redtalon | Meaning of “after normal Strike damage” with enemy Guard and overkill | Enemy at 14, 15, and 16 HP after normal Strike |
| Sszareth Mirefang | Whether direct damage occurs before or after Strike | Enemy Guard present; enemy defeated by direct damage; next defense cancelled |
| Ormund Deepdelver | Guard-die count snapshot timing | Exactly two, three, and four Guard-assigned dice |
| Thalric Stormwake | Whether -4 applies to total attack or each component | Single-hit and multi-component attack; damage floor at zero |
| Veyra Cindercrawl | Hidden branch condition and expiry | Next intent defensive vs non-defensive; verify no intent leak in UI |
| Rovan Blackstride | Whether Guard applies if Strike defeats enemy | Enemy survives, reaches 0 HP, or is defeated by a secondary effect |
| Nyra Gloamveil | Negation vs status application | Attack with damage plus a status effect |
| Eryndor Palevein | Exact below-half threshold | HP just below half, exactly half, just above half; healing overflow |
| Sylvius Moonrift | Interaction with standard reroll and reroll order | Same die selected twice, two different dice, free reroll plus standard reroll |

## Boundary tests required before implementation sign-off

- **Garruk:** below one-third means strictly less than one-third, unless a different rule is approved.
- **Eryndor:** below half means strictly less than half, unless a different rule is approved.
- **Kaelen:** “15 HP or less” is inclusive at exactly 15 HP.
- **Guard penalties:** Guard cannot fall below zero.
- **Healing:** HP cannot exceed maximum HP.
- **HP costs:** reject activation if the cost would reduce HP to zero or below, per the existing ability contracts.
- **Rerolls:** every reroll discards the old result; the replacement is kept. A die cannot be rerolled twice by the same ability activation.
- **Dice identity:** the d20's stored roll remains its natural face; the special contribution is applied during calculation.
- **Hidden intent:** conditional resolution may inspect encounter state internally, but UI text, animation, and preview must not reveal a future intent before an ability permits it.

## Exit criteria

Do not mark the character mechanics as implementation-ready until:
- [ ] The proposed timing windows are approved or replaced.
- [ ] Cooldown counting is explicit and tested.
- [ ] Damage terminology is used consistently in ability contracts.
- [ ] Cancellation and status lifecycle rules are approved.
- [ ] The 20-character boundary-test matrix has expected outcomes.
- [ ] Balance tests have been run and their results recorded.
