# Character Ability Contracts

These are the intended gameplay contracts for the UI/design project. They resolve known contradictions where possible, but all values remain subject to tests and balance simulations. An ability card should summarize the effect; the engine contract must preserve the timing and restrictions below.

## Shared timing rules
- Every turn uses exactly six combat dice: d4, d6, d8, d10, d12, and d20.
- Ability activation is permitted only in the documented phase, when cooldown is ready and any HP conditions are met.
- HP thresholds are snapshotted at activation where specified.
- An enemy at 0 HP does not take another action.
- “Cancel an action,” “negate attack damage,” “reduce attack damage,” “direct damage,” “retaliate,” and “convert damage into healing” are distinct effects.
- Damage conversion and healing cannot raise HP above maximum.
- Future enemy intent remains hidden from the player unless an ability explicitly reveals it.

## Original ten

### 1. Darius Forgeward — Forgeguard
**Effect:** Gain +10 Guard this turn. If the enemy's current attack damages Darius, deal 3 scorch damage to the enemy once for that action.
**Timing:** Guard bonus applies to this turn's enemy action. Scorch triggers after incoming attack damage is calculated.
**Limit:** Does not trigger from non-attack damage.

### 2. Corven Vex — Void Feint
**Effect:** Negate the enemy's current action.
**Timing:** Mark the current action as cancelled before its components resolve.
**Limit:** Cancel attached components too unless an encounter explicitly defines an unavoidable component. Does not reveal future intents.

### 3. Maelis Rotvein — Lingering Infection
**Effect:** Apply poison that deals 3 damage at the end of each of the next four turns.
**Timing:** First tick occurs at the end of the next turn, not immediately on application.
**Limit:** Stop ticking when the enemy is defeated. Poison duration and tick count must be tracked separately if refresh/stack behavior is later introduced.

### 4. Serath Oathscar — Vengeful Oath
**Effect:** If the enemy attacks this turn, deal retaliation damage equal to its declared attack damage.
**Timing:** Retaliation uses the attack's declared damage before player Guard reduction.
**Limit:** Triggers once per enemy action; does not trigger on a Guard or other non-attack intent.

### 5. Ilyra Veilseer — Threadseer
**Effect:** Gain two extra single-die rerolls this turn and reveal the enemy's next intent.
**Timing:** Extra rerolls are available during the reroll phase. Foresight reveals only the next intent for the current turn's planning window.
**Limit:** Each reroll replaces one die result and the new result must be kept. Never reveal the full pattern.

### 6. Garruk Bloodhowl — Blood Frenzy
**Effect:** Pay 5 HP. Strike dice are doubled, or tripled if HP is below one-third of maximum at activation.
**Timing:** Snapshot the multiplier at activation; apply it to Strike-die contributions before additive Strike bonuses.
**Limit:** Reject activation if paying the cost would reduce HP to 0 or below. The UI must show the cost and current threshold before confirmation.

### 7. Vaelis Thornwake — Rootbind
**Effect:** Prevent the enemy's current action.
**Timing:** Resolve cancellation before the enemy action begins.
**Limit:** Cancel all components unless the encounter explicitly defines one as unavoidable. This is a powerful effect and needs dedicated boss and cooldown testing.

### 8. Tovin Gearwright — Clockwork Overwind
**Effect:** After rolling, select one die and add +3 to its contribution for this turn.
**Timing:** Apply the +3 after that die's natural-face rule and before totals are finalized.
**Limit:** The die pool remains exactly six; no fourth die is created. The modifier is applied once to one die and cannot be moved after resolution begins.

### 9. Elsin Mourningcall — Requiem Reversal
**Effect:** If the enemy attacks this turn, convert the damage components of that action into healing.
**Timing:** Resolve conversion when the current enemy attack would damage Elsin.
**Limit:** Healing is capped at maximum HP. Status effects attached to the attack still apply unless the encounter defines them as part of the converted damage itself.

### 10. Nymor Hollowstar — Perfected Ruin
**Effect:** Pay 6 HP and set each of the six combat dice to its own maximum legal face value.
**Timing:** Activate after rolling and before assignment is locked.
**Limit:** Reject activation if the HP cost would reduce HP to 0 or below. d4 becomes 4, d6 becomes 6, d8 becomes 8, d10 becomes 10, d12 becomes 12, and d20 becomes 20 (which then contributes 25 under the natural-20 rule). This is a high-risk, high-power effect requiring balance review.

## Proposed additions 11–20

### 11. Borik Thornwall — Quillguard
Gain +6 Guard. If the current enemy attack damages Borik, return 3 damage once during that enemy action. Does not trigger on non-attack damage.

### 12. Kaelen Redtalon — Execution Mark
Gain +4 Strike damage. After normal Strike damage resolves, if the enemy remains alive with 15 HP or less, deal another 6 damage. Do not apply the bonus if normal Strike already defeated the enemy.

### 13. Sszareth Mirefang — Armor Rend
Deal 5 direct damage that bypasses Guard. Reduce enemy Guard by 2 for its next defensive intent. The reduction expires after that defense or at combat end.

### 14. Ormund Deepdelver — Earthbound Fortress
Gain +10 Guard, plus +3 Guard if at least three dice are assigned to Guard. Count assigned dice, not die values. Determine the assignment threshold when the ability is activated.

### 15. Thalric Stormwake — Undertow
Gain +4 Strike damage and reduce the enemy's next attack by 4, to a minimum of zero. Apply the reduction once to the next attack intent only.

### 16. Veyra Cindercrawl — Caustic Sheath
Reduce enemy Guard by 4 for its next defensive intent. If the next intent is not defensive, gain +4 Strike damage this turn instead. The engine can use the encounter state to resolve the branch; player-facing UI must not disclose hidden future intent.

### 17. Rovan Blackstride — Breakneck Charge
Gain +8 Strike damage. If the enemy survives the player's Strike resolution, gain +4 Guard for the enemy action this turn. Evaluate survival after all normal Strike damage and before the enemy acts.

### 18. Nyra Gloamveil — Shadowstep
Negate damage from the enemy's current attack. If at least three dice are assigned to Strike, gain +4 Strike damage. Attack-associated status effects remain unless separately specified as damage.

### 19. Eryndor Palevein — Abyssal Regrowth
Heal 7 HP, or 10 HP if current HP is below half maximum at activation. Snapshot the threshold and cap healing at maximum HP. Cannot activate after defeat.

### 20. Sylvius Moonrift — Slipstream
Reroll up to two selected dice without spending the standard reroll. Each selected die may be selected once during the activation; discard the old result and keep the new result.

## UI requirements for every ability
- Show name, concise effect, cooldown, activation cost, and eligibility state.
- Show HP cost and threshold conditions before the player confirms.
- Distinguish ready, unavailable, active, and cooling-down states.
- Explain which effect is temporary and when it expires.
- Do not display future enemy intent unless the selected ability has revealed it.
- Do not use ambiguous copy such as “this turn” if the duration actually extends into later turns.
