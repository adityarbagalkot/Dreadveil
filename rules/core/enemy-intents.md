# Enemy Intent and Telegraphing

## Visibility contract
- Reveal only the current enemy intent by default.
- Do not display the future intent queue, future attack values, or future status effects.
- An ability may reveal future intent only when its contract explicitly permits it.
- Oracle's proposed foresight reveals the next intent, not the full encounter pattern.
- Do not leak future intents through previews, tooltips, animation, labels, accessibility text, or other UI surfaces.

Encounter data may store the full deterministic pattern for engine resolution. Stored data is not permission to show it to the player.

## Intent presentation
- **Attack:** show the current attack and its known value when the encounter rules make that value telegraphed.
- **Guard:** indicate defense and show its known Guard value.
- **Status or special:** explain the visible effect and its current trigger condition.
- **Multi-effect:** show the known components of the current action without exposing later actions.

Do not imply an intent will resolve unchanged if a character ability can prevent, negate, redirect, or modify it.

## Oracle foresight
The current intent is already visible. Oracle's ability reveals the next intent as a separate temporary information effect. The final ability contract must define how long the revealed information remains visible. Never reveal the whole sequence unless the ability is explicitly redesigned to do so.
