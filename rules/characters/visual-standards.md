# Character Visual Standards

## Art direction
The roster belongs to **The Forbidden Manuscript**: gothic dark fantasy, occult relics, ruined-cathedral atmosphere, aged materials, and restrained but striking silhouettes. Characters should feel like dangerous beings from one world, not unrelated fantasy skins.

## Shared anatomy and readability
- Default anatomy: upright humanoid stance, two arms, two legs, and a readable weapon.
- Animal traits must influence anatomy, posture, surface texture, silhouette, and movement—not merely appear as a head pasted onto a human body.
- Preserve a clear head silhouette and weapon silhouette at character-card scale.
- Keep the character readable against a dark background; avoid burying important forms in smoke, sparks, feathers, tendrils, or decorative armor.
- Use asymmetry and purposeful wear. Avoid random clutter and generic piles of spikes.
- Hands or equivalent grips must plausibly hold the weapon.
- The body plan should remain combat-capable and compatible with the game camera.

## Original ten and new ten
- The original ten keep their established hybrid species and archetype identity.
- Characters 11–20 should not reuse any species from the original ten.
- Multi-species hybrids should have a clear hierarchy: one dominant silhouette, one or two supporting traits, and a few fine details.
- Avoid duplicating weapon silhouettes or poses across several characters.
- Each character's face, weapon, and signature animal trait should remain distinguishable in a small roster portrait.

## Suggested visual hierarchy
1. Primary silhouette and head profile.
2. Weapon silhouette.
3. Dominant animal trait.
4. Secondary animal traits.
5. Armor, cloth, relics, and surface detail.
6. Small particles or magical effects.

## Character-card presentation
Each card should show personal name, archetype/title, HP, cooldown, one-sentence role identity, ability name, and concise effect. Detailed ability rules belong in a help panel or expanded details view rather than tiny card text.

## Asset consistency checklist
- [ ] Anatomy and weapon are readable at thumbnail size.
- [ ] Hybrid species are recognizable without needing a label.
- [ ] Design fits the Forbidden Manuscript palette and materials.
- [ ] Pose communicates the combat role.
- [ ] No unrelated character's signature silhouette or weapon is copied.
- [ ] Art leaves enough contrast for UI overlays.
- [ ] Filename, character ID, and version are documented.
- [ ] Canonical artwork is approved explicitly and never overwritten without permission.

## Character-by-character design method

Use the following sequence for all 20 characters. Complete and explicitly approve one character before beginning the next.

1. **Read the canonical profile first.** Pull the exact name, archetype/title, hybrid species, weapon, HP, cooldown, ability effect, role, and visual signature from `rules/characters/character-data.json` and the supporting character documents. Do not invent or silently alter gameplay facts.
2. **Establish the identity hierarchy.** Decide which animal or body-plan trait dominates the silhouette, which traits support it, and which details remain subtle. Hybrid anatomy must be part of the body—head, torso, limbs, surface, posture, and movement—not just a head or armor decorations.
3. **Draft a reference sheet.** Include front, side, and back views, a readable silhouette, face/head study, each defining anatomy trait, weapon studies, armor/material details, and a restrained palette. Generated text is provisional and never overrides canonical data.
4. **Review against concrete questions.** Does the character read as one coherent creature? Are all hybrid species integrated naturally? Is the weapon correct and legible? Does the silhouette fit the combat role? Is the armor appropriate to the character rather than generic or overly ornate? Are important natural features hidden by gear?
5. **Iterate only on the feedback given.** For Darius Forgeward, the key iterations were: identify the badger and tortoise traits as insufficiently integrated; reduce armor coverage; then make the tortoise shell more organic and grown from the body. Keep this reasoning pattern for other characters, but derive each character's actual anatomy and gear decisions from their own canonical profile.
6. **Approve the reference before making final assets.** Do not treat a generated draft as final until the user approves its design direction.
7. **Create the asset set.** After approval, create the full-body illustration, close-up roster portrait, and ability icon as separate assets. Maintain consistent lighting, texture, palette, and identity across them.
8. **Run a canonical consistency check.** Confirm name, species, weapon, ability name/effect, and any displayed stats against the source data. Remove accidental invented lore and incorrect generated labels.
9. **Record the outcome.** Store design decisions, feedback, asset versions, and approval status in the character's folder under `character-ui/characters/<character-id>/`.
10. **Move to the next character only after the current character's agreed deliverables are complete.**

### Darius Forgeward — approved direction to carry forward
- Hybrid: Rhinoceros × Badger × Tortoise.
- Make the badger's coarse fur, broad build, and digging claws natural parts of the anatomy.
- Make the tortoise shell organic and visibly grown from the back/shoulders; use a few salvaged plates as reinforcement, not as a substitute for the shell.
- Reduce armor coverage. Concentrate mismatched scavenged metal on selected vulnerable areas; preserve natural hide, fur, and shell as visible design features.
- Keep the horned rhino structure, anvil maul, grim hand-painted fantasy treatment, cold dark palette, restrained rust-red accent, and Forbidden Manuscript framing.
- Canonical ability: **Forgeguard**. Canonical values remain in `character-data.json`; concept-sheet labels and extra prose are not authoritative.

## Suggested stable design IDs
Use kebab-case IDs that do not change when display names are edited: darius-forgeward, corven-vex, maelis-rotvein, serath-oathscar, ilyra-veilseer, garruk-bloodhowl, vaelis-thornwake, tovin-gearwright, elsin-mourningcall, nymor-hollowstar, borik-thornwall, kaelen-redtalon, sszareth-mirefang, ormund-deepdelver, thalric-stormwake, veyra-cindercrawl, rovan-blackstride, nyra-gloamveil, eryndor-palevein, sylvius-moonrift.

These are design IDs only; reconcile them with implementation IDs before game code uses them.
