# Character UI Specification

**Status:** Design specification for the Dreadveil UI repository. This document describes intended presentation and interaction; it does not assert that the implementation already exists.

## 1. Goals

The character interface must let a player:
- Identify each character quickly from name, silhouette, archetype, and role.
- Compare HP, cooldown, and ability effects without opening every profile.
- Understand whether an ability is ready, available to activate now, active, or cooling down.
- See activation costs and threshold requirements before committing.
- Understand which effects are temporary and when they expire.
- Make decisions without receiving information about hidden future enemy intents.

## 2. Character selection card

### Required information hierarchy

1. Character portrait or approved silhouette.
2. Personal name.
3. Archetype/title.
4. One-sentence role identity.
5. Current/max HP, when in combat; base HP during selection.
6. Ability name and concise effect.
7. Cooldown value and availability state, when applicable.
8. A clear selection control.

### Selection states

- **Unselected:** neutral card styling; no selected border.
- **Selected:** unmistakable border or marker and a visible selected label/state.
- **Unavailable:** only use when the character truly cannot be selected under the current game rules; show a short reason.
- **Locked:** use only if a separate unlock system exists. No unlock system is defined by this document set, so do not invent unlock requirements.
- **Loading/error:** if character data or artwork fails, preserve the name and text details and show a fallback silhouette.

### Selection behavior

- Selecting a card must not activate the character's ability.
- Selection should be reversible before the player confirms the choice.
- Keyboard and touch users must be able to select and confirm.
- Do not use color alone to communicate selection or availability.
- Do not show combat-only controls on the pre-combat selection card.

## 3. In-combat character panel

Display:
- Character portrait and personal name.
- Archetype/title.
- Current HP and maximum HP.
- A readable HP bar with numeric values; do not rely on the bar alone.
- Active status effects and remaining duration.
- Ability name, concise effect, cooldown, cost, and current eligibility.
- Any active temporary modifier with its expiry checkpoint.

HP must be clamped to the valid range from zero through maximum HP. Healing must never display HP above maximum. If the character is defeated, show the defeat state and disable actions that cannot be taken after defeat.

## 4. Ability states

Every ability uses a clear state model:

| State | Meaning | UI behavior |
|---|---|---|
| Ready | Cooldown is zero and all activation requirements are met | Enable activation in the allowed timing window |
| Cooling down | Remaining cooldown is greater than zero | Disable activation and show remaining cooldown |
| Unavailable now | Cooldown may be ready, but a phase, HP, assignment, or encounter requirement is not met | Disable activation and show the exact reason |
| Active | A temporary effect has been activated and is awaiting resolution or expiry | Show the active effect and when it expires |
| Resolved | The effect has completed for its defined timing window | Remove the active indicator; retain a log entry if combat history exists |
| Defeated | Character is at zero HP | Disable ability activation |

Do not use “ready” to imply “usable at this exact moment” if the current phase forbids activation. Prefer separate readiness and current eligibility indicators when needed.

## 5. Ability activation interaction

For abilities requiring a player decision:
1. The player selects the ability.
2. The UI shows its effect, activation cost, threshold check, timing window, and any target/selection required.
3. The player confirms or cancels.
4. On confirmation, validate current state again before applying the effect.
5. If the state changed and activation is invalid, do not consume the ability or its cost; show the reason.

Do not require a confirmation modal for simple abilities with no cost, target choice, or irreversible selection unless usability testing shows it is needed. HP-cost abilities must require clear confirmation.

### HP-cost confirmation

For Blood Frenzy and Perfected Ruin, show:
- Current HP / maximum HP.
- HP cost.
- HP after cost.
- The threshold or multiplier used, where applicable.
- A clear warning and disabled confirmation if the cost would reduce HP to zero or below.

Blood Frenzy's multiplier is based on the HP threshold at activation. Display the multiplier the game will use before confirmation. The exact one-third boundary remains subject to approval in the mechanics audit.

Perfected Ruin should preview that each die is set to its own maximum face. Its preview must retain the special d20 contribution rule: natural 20 contributes 25.

## 6. Ability tooltip and detail panel

Each ability detail view should contain:
- Ability name.
- One-sentence summary.
- Exact mechanical effect.
- Activation timing.
- Cooldown.
- HP cost, if any.
- Requirements and threshold conditions.
- Duration and expiry timing.
- Relevant exceptions (for example, attached status effects remaining after Shadowstep).
- A short explanation of why activation is currently unavailable, when applicable.

Keep the card summary short. Put exact timing and edge cases in the expanded view. Tooltip text must use the same wording and terminology as the ability contract; avoid paraphrases that change mechanics.

## 7. Dice and assignment relationship

Character UI must respect the core dice rules:
- Exactly six standard combat dice: d4, d6, d8, d10, d12, and d20.
- Every die must be explicitly assigned to Strike or Guard.
- No die may be unassigned at resolution or assigned to both.
- The d% is a utility die and must not appear as a combat die.
- Character abilities cannot add a seventh combat die or replace the standard pool.
- The d4 Guard bonus and d20 natural-face rules must be represented in totals and detail text without changing the stored roll.
- Standard and ability-provided rerolls must show the remaining count and enforce their own limits.

The character selection and character detail views must not imply a character has a unique dice loadout.

## 8. Hidden enemy intent and ability previews

Default rule: only the current enemy intent is visible. Future intents stay hidden unless an ability explicitly reveals one.

- Threadseer may reveal only the next intent within its defined planning window.
- Conditional effects such as Caustic Sheath may resolve using encounter state internally, but the player-facing UI must not leak the future intent through text, color, icons, animation, tooltips, or preview values.
- Do not display a hidden intent as a disabled, blurred, locked, or question-marked row if the existence or structure of that row reveals the pattern.
- If intent is revealed temporarily, clearly identify it as revealed information and remove or refresh it at the defined end of its visibility window.

## 9. Status and temporary-effect presentation

Every active effect should display:
- Effect name and a recognizable icon or text label.
- Who or what it affects.
- Remaining ticks or the exact future checkpoint at which it expires.
- A concise explanation of its impact.

Do not rely only on iconography; provide accessible text labels. Do not decrement displayed duration at arbitrary times: it must match the mechanics contract's timing checkpoints.

Examples:
- Lingering Infection: show poison and remaining ticks; first tick is at the end of the next turn.
- Armor Rend: show that enemy Guard is reduced for its next defensive intent only.
- Undertow: show that the next enemy attack is reduced once.
- Breakneck Charge: show its temporary Guard bonus only if the enemy survives the player's Strike resolution.
- Shadowstep: distinguish damage negation from status-effect immunity; the ability does not automatically remove attached status effects.

## 10. Combat log and feedback

Where a combat log is available, record discrete events with consistent terminology:
- Dice rolled and rerolled (including old result discarded and new result kept).
- Dice assignments and totals.
- Ability activation, cost paid, and eligibility check.
- Strike, Guard, direct damage, retaliation, damage reduction, negation, and healing as distinct events.
- Status application, tick, refresh, and expiry.
- Cooldown start and decrement.
- Enemy action cancelled or resolved.
- Victory, defeat, or mutual-defeat outcome if that rule is approved.

Feedback must not claim an effect occurred before validation succeeds. Avoid redundant notifications when the panel itself clearly communicates a state change.

## 11. Accessibility and responsive behavior

- All interactive controls must have accessible names.
- Keyboard focus must be visible and follow a logical order.
- Touch targets must be large enough to activate reliably.
- Text must remain readable at small screen widths.
- Do not communicate state through color alone.
- Respect reduced-motion preferences for effects that animate.
- Tooltips must be available by keyboard and touch, not hover only.
- If portrait art is missing, preserve the character's name, stats, ability, and selection controls.
- On narrow layouts, prioritize character identity, HP, ability readiness, and activation action over decorative art.

## 12. Data contract

The UI should render from `rules/characters/character-data.json` as the design-reference dataset. Before connecting it to implementation:
- Reconcile stable design IDs with implementation IDs.
- Validate that every character has a unique ID and a valid ability record.
- Validate HP and cooldown as non-negative numeric values.
- Keep the JSON as reference data until a deliberate implementation integration is approved.
- Do not infer missing mechanics from visual copy.
- Do not treat proposed HP/cooldown values as playtested balance results.

## 13. Acceptance checklist

- [ ] All 20 characters have consistent card hierarchy.
- [ ] Name, archetype/title, HP, cooldown, ability name, and concise effect are legible.
- [ ] Selection state is explicit and reversible before confirmation.
- [ ] Ready, cooling down, unavailable, active, resolved, and defeated states are distinct.
- [ ] HP-cost abilities show the cost and post-cost HP before confirmation.
- [ ] Activation is disabled outside its allowed timing window.
- [ ] Exact ability rules are available in a detail view.
- [ ] Six-dice constraints are preserved.
- [ ] Hidden future enemy intents are not leaked by UI.
- [ ] Temporary effects show correct duration and expiry.
- [ ] Missing artwork does not break character selection.
- [ ] No claim is made that this specification is implemented until verified in the implementation repository.
