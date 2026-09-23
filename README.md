These were all written and tested fully in Foundry VTT version 13, however I have upgraded to version 14 and haven't run into any problems in several sessions. 
I'm providing these as is, I will likely only update them if a major version change breaks something.

# SRA2 - Distances
This is adapted from `daggerheart-distances` for use with the `sra2` system.

## Range bands

The module uses the range thresholds present in the SRA2 system roll dialog:

- **Close:** under 2m
- **Short:** 2–15m
- **Medium:** 16–60m
- **Long:** beyond 60m

Because Long has no finite upper boundary, the module draws the three finite cutoff rings: 2m, 15m, and 60m. Hover labels report Long for targets beyond 60m.

## Main behavior

- Select a token to automatically show its SRA2 range rings.
- Deselect the token to remove selection-created rings.
- Press **R** or use the Token HUD button to manually toggle rings.
- GMs can use **Shift+R** to broadcast rings to all clients temporarily.
- Select multiple tokens and press **M** or run `DHDistances.MassMeasurement()` to measure from the group center.

## Settings

In Foundry’s module settings you can configure visual style, color palette, line thickness, fill style, highlighting, and whether rings appear automatically when a token is selected.

## Compatibility

- Foundry VTT: v13
- System: `sra2` / Shadowrun Anarchy 2

## Macro API

```js
DHDistances.Toggle();                 // Toggle rings for selected/hovered token
DHDistances.Toggle({ remote: true }); // GM: broadcast rings to all players
DHDistances.MassMeasurement();        // Rings from center of selected tokens
DHDistances.Toggle({ mode: '2d' });   // Ignore elevation
DHDistances.Toggle({ mode: '3d' });   // Account for elevation
DHDistances.Toggle({ mode: 'both' }); // Show both 3D and 2D distances
```

## Credits

Original module: `daggerheart-distances` by Mestre Digital / Bruno Calado, itself forked from `foundry_combat_distances`.

**SRA2 - Host Links**

This module adds persistent visual links between Host/server tokens on a Scene.

## Workflow

1. Log in as GM.
2. Place two or more SRA2 Host/server actors on a Scene.
3. Select a Host/server token.
4. Click the Host Link button in the token HUD.
5. Select another Host/server token to complete the link.
6. Optionally enter a label.
7. The module draws a persistent arrow between the two Host/server tokens.

Links are stored as Scene flags, so they persist with the Scene and redraw when tokens move or the Scene reloads.

## Features

- Targets SRA2 actor type `server`; also supports `host` if present.
- Adds a token HUD control to start a Host link.
- Adds a token HUD control to clear all links attached to a Host token.
- Draws arrows between linked Host tokens on the canvas.
- Optional labels appear near the middle of a link.
- Links automatically redraw when linked tokens move.
- Broken links are skipped if one of the linked tokens no longer exists.
- Players can see links; link editing is GM-only.

## Install layout

The ZIP is packaged with `module.json` at the root. After installation, the target folder should look like:

```text
Data/modules/sra2-host-links/module.json
Data/modules/sra2-host-links/scripts/main.mjs
Data/modules/sra2-host-links/styles/main.css
```

**SRA2 - Combat Turn Checkboxes**

## Features

- Splits the Combat Encounters / Combat Tracker list into **Unclaimed** and **Claimed** sections.
- All combatants start each new round as **Unclaimed**.
- Clicking the hand icon on an Unclaimed combatant moves that combatant to **Claimed** and makes it Foundry's active turn.
- Clicking the hand icon on an already Claimed combatant makes it Foundry's active turn again.
- Adds a checkbox to each combatant row so the table can mark whether that combatant has taken their turn.
- Lets any connected player click any combatant row checkbox or hand button.
- Stores checkbox and claim state on the Combatant as module flags.
- Hides the per-combatant roll initiative button.
- Clears all checkboxes and claims automatically when the combat round changes by default.

## Player actions

Non-GM players usually cannot directly update Combat and Combatant documents. This module relays player checkbox and hand-button clicks through a hidden blind-whisper chat message to the active GM client. The GM client applies the actual Combat change, then the relay message is deleted so it does not clutter chat.

A GM user must be logged in for player clicks to update the encounter for everyone.

## Settings

- **Hide individual roll initiative buttons**: Enabled by default.
- **Reset turn state on new round**: Enabled by default. Clears checkboxes and moves every combatant back to Unclaimed.
- **Split combat tracker into Claimed and Unclaimed sections**: Enabled by default.

## Install layout

The ZIP is packaged with `module.json` at the root. After installation, the target folder should look like:

```text
Data/modules/sra2-turn-checkbox/module.json
Data/modules/sra2-turn-checkbox/scripts/main.mjs
Data/modules/sra2-turn-checkbox/styles/main.css
```
