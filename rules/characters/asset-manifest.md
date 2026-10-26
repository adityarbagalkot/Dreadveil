# Character Asset Manifest

**Status:** Asset planning reference. This manifest defines intended asset names and requirements; it does not claim the assets already exist or approve new artwork.

## 1. Naming and folder conventions

Use stable character IDs from `character-data.json`. IDs should not change when display names or art versions change.

Suggested directory layout:

```text
assets/
  characters/
    <character-id>/
      portrait-v001.webp
      fullbody-v001.webp
      ability-v001.webp
      metadata.json
  shared/
    character-placeholder.webp
    ability-placeholder.webp
```

These are proposed paths, not a statement that these files or folders currently exist.

### Asset names

| Asset type | Filename pattern | Purpose |
|---|---|---|
| Portrait | `portrait-v001.webp` | Character selection card and compact combat identity |
| Full-body | `fullbody-v001.webp` | Expanded profile or character detail |
| Ability icon | `ability-v001.webp` | Ability button and tooltip |
| Metadata | `metadata.json` | Art direction, version, approvals, and source references |
| Shared portrait fallback | `character-placeholder.webp` | Fallback when a character portrait is missing |
| Shared ability fallback | `ability-placeholder.webp` | Fallback when an ability icon is missing |

Prefer WebP for raster art where supported by the asset pipeline. If transparency, animation, or engine constraints require another format, record that decision in metadata instead of silently changing naming conventions.

## 2. Asset requirements

### Portrait
- Clearly distinguish the face/head silhouette at card scale.
- Include one dominant animal trait and a readable weapon cue where practical.
- Use a consistent crop, lighting direction, and background treatment across the roster.
- Leave safe space around the head and weapon so UI framing does not obscure identifying features.
- Maintain contrast against the dark Forbidden Manuscript interface.

### Full-body artwork
- Show the full two-arm, two-leg combat-capable humanoid silhouette.
- Make the primary animal trait, weapon, and pose readable.
- Use secondary hybrid traits as supporting details rather than competing focal points.
- Avoid cropping hands, weapon ends, feet, or key anatomical features unless the asset is intentionally designed as a crop.
- Keep the pose and silhouette distinct from other characters.

### Ability icon
- Communicate the ability's main action at small sizes.
- Use one primary symbol, strong value contrast, and limited detail.
- Avoid embedding the ability name in the artwork; render names as UI text for localization and accessibility.
- Keep the same canvas, padding, and visual weight across all 20 icons.
- Do not expose hidden future enemy intent through conditional icon states.

## 3. Shared art direction

All character art follows **The Forbidden Manuscript**:
- Gothic dark fantasy, occult relics, ruined-cathedral atmosphere, aged materials.
- Restrained palette with enough contrast for readability.
- Purposeful wear and asymmetry; avoid random spikes or decorative clutter.
- Hybrid species should shape anatomy, posture, texture, and movement rather than appearing as a human body with an animal head pasted on.
- The weapon and primary silhouette must remain legible at thumbnail size.
- Character art should feel like one coherent world while preserving a distinct identity per character.

## 4. Character-by-character asset plan

Filename stem for each entry is the stable ID. Full asset paths are planned under `assets/characters/<id>/`.

| # | Stable ID | Portrait focus | Full-body focus | Ability icon concept |
|---:|---|---|---|---|
| 1 | `darius-forgeward` | Horned brow and battered faceplate | Heavy rhino/badger/tortoise frame; anvil maul | Anvil shield with a scorched edge |
| 2 | `corven-vex` | Raven profile and hooked beak | Feathered shadow duelist with octopus-like flexibility; hooked blades | Broken enemy silhouette dissolving into ink |
| 3 | `maelis-rotvein` | Hyena muzzle and axolotl gills | Diseased plaguewright with leech-like skin details and blight staff | Spore or infected drop with four tick marks |
| 4 | `serath-oathscar` | Stag antlers, carrion-feather mantle | Scorpion-tail accents and broken oath-glaive | Cracked oath seal with a retaliatory blade |
| 5 | `ilyra-veilseer` | Owl eyes, moth textures, restrained lure glow | Veilseer holding a lantern sceptre | Single eye inside a thread-ring, one forward marker |
| 6 | `garruk-bloodhowl` | Boar tusks and wolf-like stare | Bat-membrane accents and bloodied great-axe | Blood-marked axe with a rising force motif |
| 7 | `vaelis-thornwake` | Mantis facial profile and deer crown | Pangolin scales and thorn glaive | Roots binding a single hostile silhouette |
| 8 | `tovin-gearwright` | Frog-like face and beetle plating | Armadillo armour and chronometer hammer | One gear with a single highlighted die |
| 9 | `elsin-mourningcall` | Fox face framed by peacock/cicada textures | Resonance war-lyre and layered display feathers | War-lyre emitting a reversed wave |
| 10 | `nymor-hollowstar` | Hare ears against an abyssal silhouette | Eel-like lines, lure detail, void scythe | Six-pointed die burst collapsing into a dark star |
| 11 | `borik-thornwall` | Wolverine jaw and quilled brow | Musk-ox mass, porcupine mantle, barbed war-pick | Quill shield with three reflected sparks |
| 12 | `kaelen-redtalon` | Secretary-bird crest and caracal ear tufts | Tall executioner stance with shoebill beak and glaive | Glaive crossing a marked low-health target |
| 13 | `sszareth-mirefang` | Gharial snout and horned-lizard ridges | Monitor-lizard musculature and serrated cleaver | Cleaver cutting through a guard plate |
| 14 | `ormund-deepdelver` | Aardvark muzzle and echidna spines | Heavy tapir-like frame with earthbreaker hammer | Hammer striking a rooted stone shield |
| 15 | `thalric-stormwake` | Severe seabird profile | Broad albatross-like silhouette, dark plumage, tide-splitter spear | Spear and a receding wave |
| 16 | `veyra-cindercrawl` | Velvet-worm texture and trap-jaw mandibles | Segmented centipede accents and caustic twin-blades | Corroded shield with a split path |
| 17 | `rovan-blackstride` | Cassowary casque and forward gaze | Powerful running-bird legs, feather mass, rupture lance | Lance with a forward burst and recoil mark |
| 18 | `nyra-gloamveil` | Genet markings and civet facial mask | Long binturong-influenced tail and shadow hook-blades | Dark crescent passing through an attack arc |
| 19 | `eryndor-palevein` | Pale amphibian face and translucent details | Salamander folds, caecilian rings, ossuary staff | Pale growth rings closing around a wound |
| 20 | `sylvius-moonrift` | Glider facial markings and alert eyes | Membranes, compact gliding pose, crescent daggers | Two crescent paths with two reroll marks |

## 5. Metadata template

Each character's `metadata.json` should eventually record:

```json
{
  "characterId": "darius-forgeward",
  "displayName": "Darius Forgeward",
  "assetVersion": 1,
  "status": "planned",
  "assets": {
    "portrait": "portrait-v001.webp",
    "fullBody": "fullbody-v001.webp",
    "abilityIcon": "ability-v001.webp"
  },
  "artDirection": "The Forbidden Manuscript",
  "approval": {
    "approved": false,
    "approvedBy": null,
    "approvedAt": null
  },
  "sourceReference": null,
  "notes": []
}
```

The example is a template only. Copy it per character and replace its ID/name and source references. Do not mark an asset approved until the owner explicitly approves that specific version.

## 6. Versioning and approval rules

- Increment the version when a visual change materially affects silhouette, anatomy, weapon, composition, or approved appearance.
- Minor exports that do not alter the approved artwork may keep the same art version but should be traceable in the build pipeline.
- Never overwrite approved canonical art without explicit permission.
- Keep generated drafts, review candidates, and approved assets distinct.
- Record the source prompt or source file reference for every generated or edited image.
- If a design changes, update the manifest first and then update the asset; do not silently diverge from the roster's hybrid species or weapon.
- An asset marked planned or draft must not be represented as final artwork.

## 7. Delivery checklist

For each character, verify:
- [ ] Portrait is readable at the smallest card size.
- [ ] Full-body art shows the weapon and combat-capable silhouette.
- [ ] Ability icon communicates the ability without text.
- [ ] Art matches the shared world and the character's hybrid species.
- [ ] No accidental duplicate silhouette or weapon concept.
- [ ] Filename matches the stable character ID.
- [ ] Version and source reference are recorded.
- [ ] Approval state reflects actual approval.
- [ ] Missing assets fall back gracefully.
- [ ] UI does not imply an unimplemented asset exists.

## 8. Current status

This manifest is a plan. It does not create artwork, create asset files, or modify the game implementation. The next art-production step should be to review a small representative set (one tank, one control character, and one agile character) before producing the full 20-character set.
