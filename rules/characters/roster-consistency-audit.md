# Roster Consistency Audit

**Status:** Audit report only. No canonical character data, mechanics, or UI decisions were changed by this audit. Findings distinguish objective consistency issues from decisions that remain unapproved.

## Scope

Compared the roster, ability contracts, character profiles, machine-readable character data, visual standards, UI specification, asset manifest, shared dice/turn-flow/enemy-intent rules, and mechanics audit in this repository.

## Summary

- **20/20** characters are represented in the roster, JSON dataset, ability contracts, profile document, and asset manifest.
- The JSON dataset has **20 unique stable IDs** and the character ordering aligns with the roster.
- Roster HP, cooldown, hybrid species, weapon, and ability names are broadly aligned with the machine-readable data.
- The six-dice constraint and hidden-future-intent rule are consistently reinforced across the core rules and UI documentation.
- The principal actionable inconsistency is **ability timing**: some contracts require a pre-assignment activation, while the shared turn-flow currently presents a single Ability phase after assignment.
- Character profile epithets differ from the roster's archetype/title labels. The profile document describes its creative details as proposed, so this is a naming decision rather than a confirmed data error.

## Findings

### ROSTER-01 — Ability timing conflicts with the shared turn flow

**Severity:** High  
**Type:** Confirmed documentation inconsistency

The shared turn flow orders phases as Roll → Reroll → Assign → Ability → Resolve. However, the contracts for Threadseer and Perfected Ruin require use before assignment is locked, and Clockwork Overwind says “after rolling.” The mechanics audit also proposes named timing windows, but labels that proposal unapproved.

**Impact:** A UI or implementation cannot faithfully enforce both the current shared phase order and the stated activation windows without a clarified rule.

**Recommendation:** Approve named activation windows and then update the shared turn flow, ability contracts, and UI specification together. Keep the mechanics-audit recommendations explicitly marked as proposals until approved.

### ROSTER-02 — Character profiles introduce a second epithet system

**Severity:** Medium  
**Type:** Editorial choice requiring confirmation; not necessarily a mismatch

The roster and JSON use titles such as “The Forgeguard” and “The Raven.” The profiles use different epithets such as “The Last Anvil” and “The Unwritten Omen.” The profiles explicitly identify their narrative details as proposed creative additions.

**Impact:** It is unclear whether the UI should show the archetype/title, the profile epithet, or both. This can create inconsistent character cards and art metadata.

**Recommendation:** Decide the display hierarchy before designing the final character UI. A possible rule is **personal name → archetype/title → optional lore epithet**, but this is a recommendation, not an approved change.

### ROSTER-03 — Ability cancellation has encounter-specific exceptions

**Severity:** Medium  
**Type:** Proposed rule requiring confirmation

Void Feint and Rootbind cancel the current enemy action, including its components, except where an encounter explicitly marks a component unavoidable. The shared enemy-intent document warns not to imply an intent resolves unchanged if it can be prevented, negated, redirected, or modified. The mechanics audit's cancellation wording is still a proposal.

**Impact:** Encounter authors and UI designers need a consistent way to identify unavoidable components and communicate the exception.

**Recommendation:** Approve one shared cancellation contract and require encounter data to explicitly label any unavoidable component. Do not invent an exception in UI copy.

### ROSTER-04 — Cooldown counting is not yet approved as a single rule

**Severity:** Medium  
**Type:** Unresolved rules decision

The roster and JSON agree on listed cooldown values, but the shared turn-flow says cooldowns update at the next-turn boundary without defining exact decrement semantics. The mechanics audit recommends setting the listed value on use, not decrementing in that same turn, and decrementing after subsequent completed turns; it clearly labels this as a proposal.

**Impact:** Ability readiness can differ by a turn depending on interpretation, affecting both combat balance and UI states.

**Recommendation:** Approve the cooldown counting convention and add tests for cooldowns 1–4 before treating the UI readiness states as final.

### ROSTER-05 — Profile epithet and card-copy fields are not represented in the JSON schema

**Severity:** Low  
**Type:** Data-model choice

The JSON has displayName, archetype, title, and cardCopy; the profiles separately contain lore, motivation, flaw, strength, weakness, and a profile-specific epithet/card-copy line. The JSON does not define fields for all of those profile details.

**Impact:** If the profile document is expected to drive UI or asset metadata, the source of truth for those fields is unclear. If it is only editorial reference, no data-model change is necessary.

**Recommendation:** Decide whether profile-only fields are narrative documentation or intended UI data. Do not expand the JSON schema unless those fields are needed by an approved experience.

### ROSTER-06 — Shared turn-flow resolution order needs reconciliation with ability triggers

**Severity:** High  
**Type:** Confirmed cross-document ambiguity

The shared turn-flow lists player Strike and direct/ongoing effects before the enemy action, then enemy action resolution, then retaliation, damage conversion, and status effects. Ability contracts describe several effects with their own trigger points: Darius and Borik retaliate only if an attack causes HP loss; Serath retaliates based on declared attack damage; Elsin converts attack damage into healing; Nyra negates attack damage while preserving attached status effects. The mechanics audit proposes more exact terms and order but remains unapproved.

**Impact:** It is not possible to infer one deterministic ordering for all edge cases from the shared turn-flow alone.

**Recommendation:** Approve the damage vocabulary and trigger order in the mechanics audit, then update the shared resolution order and affected ability contracts in one coordinated change.

### ROSTER-07 — Exact threshold and status lifecycle rules remain partly proposed

**Severity:** Medium  
**Type:** Unresolved rules decisions

The contracts use thresholds such as “below one-third maximum” and “below half maximum,” while the mechanics audit flags boundary tests and status lifecycle details. The UI specification itself says the exact one-third boundary remains subject to approval. Poison tick timing and Armor Rend duration are described in character contracts, but shared status rules still call for standardized application, tick, expiry, and combat-end behavior.

**Impact:** UI previews, test expectations, and engine behavior could diverge at exact HP boundaries or effect expiry.

**Recommendation:** Approve the boundary conventions and status lifecycle rules, then encode them as testable examples. Do not silently infer whether an exact threshold is included.

## Confirmed matches

- Roster and JSON cover the same 20 characters in the same numbered order.
- Stable IDs in the JSON align with the suggested ID list in visual standards and the 20 entries in the asset manifest.
- Character names, HP, cooldown values, hybrid species, weapons, and ability names are consistent across the main roster and JSON at the field level.
- The ability-contract document contains one contract for each of the 20 roster entries.
- The asset manifest includes one asset-plan row for each of the 20 stable IDs. These are planned assets, not existing or approved artwork.
- The six standard combat dice, explicit Strike/Guard assignment, d% utility-only status, and prohibition on adding a seventh combat die are consistent across the core dice rules and character UI documentation.
- The default hidden-future-intent rule is consistent across the enemy-intent rules, Oracle contract, Veyra contract, and UI specification.
- The dataset and UI specification both identify the JSON as design-reference data rather than proof of implementation.

## Items deliberately not treated as errors

- Character 11–20 HP and cooldown values are explicitly starting balance targets, not tested results.
- The replacement of Tovin's extra-die concept with a +3 contribution modifier is intentional and preserves the six-dice rule.
- Profile-specific epithets are explicitly proposed creative details; their difference from archetype/title labels needs a display decision, not automatic rewriting.
- Proposed cooldown, timing, cancellation, damage-order, simultaneous-defeat, and status-lifecycle rulings in mechanics-audit.md remain unapproved.
- This repository is the UI/design reference. Stable IDs must still be reconciled with implementation IDs before integration.

## Decision and correction checklist

- [ ] Approve the ability timing windows and align the shared turn-flow with them.
- [ ] Choose the character-card label hierarchy: archetype/title, profile epithet, or both.
- [ ] Approve the shared action-cancellation contract and unavoidable-component exception.
- [ ] Approve cooldown decrement semantics and tests for cooldowns 1–4.
- [ ] Approve the damage terminology and deterministic resolution order.
- [ ] Approve HP threshold boundaries and standard status lifecycle rules.
- [ ] Decide whether profile-only narrative fields should remain editorial or be added to the JSON data model.
- [ ] After decisions are approved, update the affected canonical documents together and re-run this audit.
- [ ] Only then finalize character UI design with the user; do not implement UI or game-source changes without explicit approval.

## Audit boundary

This report documents consistency risks and recommended decisions. It does not change the roster, character abilities, JSON data, proposed mechanics, art direction, or UI implementation. No game source code or UI implementation was modified.
