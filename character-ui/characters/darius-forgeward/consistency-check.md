# Darius Forgeward — Final Design Consistency Check

**Review date:** 2026-10-28  
**Scope:** Design and artwork previews only; not an implementation audit.  
**Canonical source:** `rules/characters/character-data.json`

## Canonical facts verified

| Field | Canonical value | Result |
|---|---|---|
| Name | Darius Forgeward | Pass |
| Title | The Forgeguard | Pass |
| Archetype | Forge Tank | Pass |
| Hybrid | Rhinoceros × Badger × Tortoise | Pass |
| Weapon | Anvil maul | Pass |
| HP | 44 | Pass |
| Cooldown | 3 | Pass |
| Ability | Forgeguard | Pass |
| Ability effect | Gain 10 Guard. If the current attack damages Darius, scorch the attacker for 3 damage. | Pass |

## Visual review against approved direction

- **Rhinoceros identity:** Strong, readable head and horn silhouette.
- **Badger identity:** Coarse fur, dense build, and clawed hands/feet are visible and integrated into the body.
- **Tortoise identity:** Shell structure is present across the back and shoulders; it reads as natural shell reinforced by scavenged plates rather than a complete metal suit.
- **Armor coverage:** Reduced relative to the initial direction; mismatched rusted plates, straps, chains, and worn leather remain secondary to the creature anatomy.
- **Weapon:** The full-body image includes the anvil maul.
- **Palette and mood:** Cold ruined environment, charcoal/iron/brown, restrained burgundy cloth and warm forge highlights fit the established grim painterly direction.
- **Portrait:** Portrait-oriented close-up with a muted painterly finish and restrained worn-metal frame, approved by the user.
- **Ability visual:** User selected an animal-face emblem direction and approved the painterly portrait treatment. The prepared icon currently reuses the approved face artwork as a placeholder rather than a distinct, compact ability glyph; this should be revisited if the UI needs a square/small-scale icon.

## Outstanding limitations

- The artwork files are packaged locally under `darius-forgeward-assets.zip`; they have **not** been committed as binary assets in GitHub because the available GitHub connector supports text-file commits but no binary image upload.
- The package uses JPEG exports of the generated PNG previews to reduce transfer size.
- The UI layout is specified in `ui-design.md`, but no UI implementation was changed.
- The character's separate lore panel should use approved canonical copy only: “A walking bastion who makes every blow costly.”

## Decision

**Design direction approved; character package not yet fully closed.** The UI spec and consistency review are complete. Remaining closure steps: place the packaged images in the repository asset folders, verify their URLs and rendering, and decide whether Forgeguard needs a more compact ability glyph. Do not start character two until those remaining asset steps are completed or explicitly deferred by the user.
