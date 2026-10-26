# Character Balance Review

## Purpose
This is a pre-implementation risk review, not a claim that the abilities have been playtested. The game target is punishing, but character choice should create different decisions rather than one dominant strategy.

## High-risk abilities

| Character | Risk | Recommended test / guardrail |
|---|---|---|
| Darius Forgeward | +10 Guard plus retaliation can erase an attack's value | Test high-damage and multi-hit intents; retaliation triggers once per enemy action. |
| Corven Vex | Full action cancellation can trivialize a boss turn | Test boss actions, status components, and cooldown frequency. |
| Maelis Rotvein | 12 total poison damage can be too strong against low-HP enemies | Verify exact tick count and compare delayed damage with immediate Strike. |
| Serath Oathscar | Retaliation on declared damage can be large even when fully guarded | Confirm declared-damage wording and one trigger per action. |
| Ilyra Veilseer | Extra rerolls plus foresight bundles two powerful benefits | Compare with other cooldown-3 abilities; reveal only one future intent. |
| Garruk Bloodhowl | Tripling six Strike dice can create extreme burst | Test threshold boundary, HP cost, and boss one-shot potential. |
| Vaelis Thornwake | Full action cancellation overlaps Corven | Test separately; consider distinct conditions or magnitude only after results. |
| Tovin Gearwright | +3 to one die is modest and predictable | Confirm order with natural-face rules and usefulness across assignments. |
| Elsin Mourningcall | Converting all attack damage into healing may nullify a boss action | Test overflow, attached status effects, and low-HP survival. |
| Nymor Hollowstar | Maximum values for six dice create high Strike and Guard simultaneously | Test all encounters; adjust cost/cooldown or scope if it dominates. |
| Borik Thornwall | +6 Guard and 3 retaliation overlap with Darius | Preserve smaller bonus and compare mitigation over repeated fights. |
| Kaelen Redtalon | +4 plus conditional +6 creates a 10-point damage swing | Test at 14/15/16 enemy HP; ensure no bonus after defeat. |
| Sszareth Mirefang | Direct damage plus future Guard reduction may be too efficient | Verify direct damage bypasses Guard and reduction applies only once. |
| Ormund Deepdelver | +13 Guard may make full-Guard assignments too safe | Test with exactly two, three, and four Guard dice. |
| Thalric Stormwake | +4 Strike and -4 attack damage is efficient offense and defense | Test low attacks and multi-component attacks. |
| Veyra Cindercrawl | Branch depends on hidden future intent | Ensure UI does not leak the branch; test both outcomes. |
| Rovan Blackstride | +8 Strike plus conditional Guard rewards a successful hit heavily | Test enemy HP boundaries and defensive intents. |
| Nyra Gloamveil | Attack negation plus +4 Strike may rival full cancellation | Confirm only attack damage is negated and attached effects remain. |
| Eryndor Palevein | 7/10 healing may weaken punishing difficulty | Test full, half, and critical HP. |
| Sylvius Moonrift | Two free rerolls may make dice variance too forgiving | Test against the standard reroll limit; each die only once per activation. |

## Required matchup matrix
Test each character against all three baseline encounters. Record win rate, median rounds, HP remaining, incoming and outgoing damage, ability impact, and reroll usage. Include weak-roll and strong-roll cases.

## Decision gates
1. Preserve the six-dice rule; Gear-Saint's extra-die concept is replaced with a one-die +3 modifier.
2. Do not call an ability balanced until simulations and edge-case tests exist.
3. Investigate outlier matchups and fights that feel unwinnable without foresight.
4. Keep abilities distinct: defense, action denial, retaliation, attrition, foresight, burst, healing, defense break, and reroll control should create different decisions.
5. Treat HP and cooldown values for characters 11–20 as initial targets, subject to test evidence.
