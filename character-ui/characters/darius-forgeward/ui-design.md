# Darius Forgeward — Character UI Specification

**Status:** Layout direction documented; visual art concepts approved in conversation.  
**Implementation status:** Design-only. No game UI or implementation code has been changed.  
**Canonical source:** `rules/characters/character-data.json`

## 1. Purpose and visual direction

Present Darius as the first complete character showcase in Dreadveil. Use the established **Forbidden Manuscript** direction: oppressive grim fantasy, aged parchment used sparingly, distressed bronze details, charcoal shadows, worn materials, and restrained burgundy/forge-orange accents. The art treatment is painterly rather than a high-effects graphic.

## 2. Approved desktop composition

Use a balanced three-column character showcase:

1. **Left rail — roster**
   - Narrow vertical roster of portrait thumbnails.
   - Darius's portrait is selected and visibly distinguished.
   - Other roster portraits are placeholders until their individual artwork is approved.
   - Keep names readable; avoid cluttering each thumbnail with full stats.

2. **Center — character showcase**
   - Largest area of the screen.
   - Show the approved full-body Darius illustration, preserving its aspect ratio and avoiding aggressive cropping.
   - Keep enough negative space around the silhouette for the character to read clearly.
   - Display name and title as a restrained overlay or adjacent heading, not baked into the artwork.

3. **Right panel — information**
   - Tabs: **Stats**, **Abilities**, **Lore**.
   - Default tab: Stats.
   - Keep the panel width sufficient for readable labels and ability descriptions.
   - Tab changes must not change the selected character.

## 3. Canonical content

Display only values from the canonical character data:

- **Name:** Darius Forgeward
- **Title:** The Forgeguard
- **Archetype:** Forge Tank
- **HP:** 44
- **Cooldown:** 3
- **Weapon:** Anvil maul
- **Ability:** Forgeguard
- **Ability effect:** Gain 10 Guard. If the current enemy attack damages Darius, scorch the attacker for 3 damage.

Do not add invented attributes, rarity, level, damage values, or lore to fill empty space. If the game has an authoritative source for additional stats, integrate those only after they are verified.

## 4. Tab content

### Stats
- HP: 44
- Cooldown: 3
- Role tags: Tank, Counterattack
- Weapon: Anvil maul

### Abilities
- Ability name: Forgeguard
- Effect text: “Gain 10 Guard. If the current attack damages Darius, scorch the attacker for 3 damage.”
- Keep the ability icon separate from the rules text and ensure the text remains readable at common desktop sizes.

### Lore
- Use approved canonical lore only. The character data provides the card copy: “A walking bastion who makes every blow costly.”
- Do not use generated concept-sheet prose as canon without explicit review.

## 5. Artwork usage

Planned asset locations:
- `assets/full-body/darius-forgeward-full-body.png`
- `assets/portrait/darius-forgeward-portrait.png`
- `assets/ability/forgeguard-icon.png`

Portrait treatment: portrait orientation, close-up face, muted painterly texture, restrained worn-bronze frame. Ability icon direction: Darius's animal face as the primary symbol, with restrained effects and no excessive graphic bursts.

These are target filenames only. Do not consider the assets committed until the files are actually present and verified in the repository.

## 6. Responsive behavior

- At medium widths, allow the roster rail to collapse to a compact strip while retaining the selected portrait.
- At narrow widths, stack the character showcase and information panel; provide an accessible way to open the roster.
- Avoid cropping Darius's horn or shell silhouette when the image container changes size.
- Tabs must remain keyboard accessible and have clear selected states.

## 7. Acceptance checklist

- [ ] Layout follows left roster / center artwork / right tabbed panel.
- [ ] Portrait, full-body artwork, and ability icon files are present and verified.
- [ ] Displayed name, title, HP, cooldown, weapon, and ability effect match canonical data.
- [ ] Art is not stretched; focal anatomy remains visible at desktop and mobile sizes.
- [ ] Stats, Abilities, and Lore tabs work in implementation when implementation is separately authorized.
- [ ] No implementation changes are made as part of this design-only task.
