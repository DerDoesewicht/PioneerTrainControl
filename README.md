# Pioneer Train Control 1.0.0

<img src="PioneerTrainControl/Resources/Icon128.png" alt="Pioneer Train Control logo" width="160">

**Your trains. Your rules.**

Per-wagon departure rules, paired departures and a live transport overview for **Satisfactory**.

[Deutsch](README.de.md) · [Quick start](#quick-start) · [Report a problem](https://github.com/DerDoesewicht/PioneerTrainControl/issues)

![Pioneer Train Control rule editor](docs/images/edit-rules.png)

*Gameplay screenshots show test build r30. Version 1.0.0 includes the graphite UI redesign and the new logo in the menu header.*

> **1.0.0 · Beta.** A remaining loading issue can leave a wagon short of its target after a top-up attempt. See [Current limitations](#current-limitations) before choosing exact-full departure rules.

## Control each wagon at each stop

Configure the freight wagons that matter at a particular timetable stop. One wagon can wait to fill while another must unload. Every selected condition must be satisfied before normal PTC release.

| Wagon mode | Departure condition | Example |
| --- | --- | --- |
| **Ignore** | This wagon contributes no condition. | A wagon used at another stop. |
| **Full** | Reach a minimum fill level of 1–100%. At 100%, the wagon must be fully loaded. | Leave with at least 70% cargo. |
| **Empty** | Reach a maximum remaining fill of 0–100%. At 0%, the wagon must be empty. | Leave with no more than 10% remaining. |
| **Amount** | Hold at least the chosen number of a specific solid item. | Carry at least 2,000 Steel Beams. |

These are **departure conditions**, not transfer limits. A normal game transfer cycle can move more than the configured target. Item quantities apply to the selected solid item; percentage targets are available for cargo fill levels.

![Individual wagon targets](docs/images/wagon-settings.png)

## Choose when transfers begin

Departure targets and transfer timing are separate settings.

| Loading policy | Behavior |
| --- | --- |
| **First load immediately, then remaining capacity** | Allow the first load. Later cycles wait for enough matching cargo to fill the wagon's remaining capacity. |
| **Only when the platform is full** | Each loading platform waits for its own inventory to be full before a cycle. |
| **Any available partial load** | Allow partial loading as matching cargo becomes available. |

For unloading, choose **first unload immediately, then wait for room for the rest**, or **any possible partial unload**. Platform load/unload settings, item filters and available space still apply. The remainder policy tracks each wagon and station visit separately.

A lower departure target does not reduce the amount required by the “remaining capacity” loading policy. For example, a 70% target can still wait for a full remainder batch if the first transfer did not reach 70%.

![Loading and unloading policies](docs/images/load-unload.png)

## Depart together

Link a stop on one train to a stop on another train. When both trains are at their linked stops and satisfy their wagon rules and minimum waits, PTC releases both together.

1. Configure, enable and save the rules on both trains.
2. Open **Synchronized departure** on one stop and enable **Wait with partner**.
3. Select the partner train and stop, then save. PTC links both stops.

The two waiting stops must be at different stations so both trains can dock. Pairing controls departure permission; signals and route availability still determine when the trains physically move.

While linked, the normal timeout is replaced by the **emergency timeout**. Its value applies to both stops, but each train measures it from its own arrival. When it expires, only that train is released. Manual release also affects only the selected train. An emergency timeout of **0** means indefinite waiting.

![Synchronized departure settings](docs/images/synchronized-departure.png)

## See what is holding up your trains

The **Transport overview** shows trains, their current station or destination, average wagon fill, elapsed PTC waiting time, the current wait reason and the last recorded release reason. Search by name or filter for PTC-controlled or automatically driven trains. Select a train to open its rules.

The overview refreshes about every **5 seconds**; selected train details refresh about every **second** while the menu is open. Fill is the average of freight-wagon fill percentages. Release history covers the current game session.

![Live transport overview](docs/images/live-overview.png)

## Reuse your rules

Open **Copy and templates** to copy a stop configuration, paste it into another stop or save a named template. Templates are shared within the current world.

Rules map by **freight-wagon position**, so source and destination must have the same wagon count. The destination stop keeps its activation state and partner link. Pasting creates a draft: review it and **Save** to apply. To create a saved template, save the stop rule first. Deleting a template does not remove rules already applied to stops.

## Quick start

1. Install an available beta build with **Satisfactory Mod Manager**, then launch your modded game. The source archive in this repository is for development, not a compiled mod-manager package.
2. Give your train a timetable and configure the station platforms for the intended loading or unloading.
3. Open the in-game chat and enter **`/ptc`**. **`/traincontrol`** is an alias.
4. Select the train, then the timetable stop.
5. Set each freight wagon to **Full**, **Empty**, **Amount** or **Ignore**. Choose transfer policies and the minimum wait or timeout if needed.
6. Enable the rule and **Save**. Newly enabled rules take effect on the next docking at that stop.
7. Close the panel with **Esc**. Check the overview when you want to see why a train is waiting.

The interface follows the game's language: **German or English**.

For an independent train, set the normal timeout to **0** to wait without a time limit. For a linked pair, set the emergency timeout to **0**. A timeout or manual release can allow departure with unmet cargo targets.

## Example: unload two wagons, load two wagons

| Wagon | Rule at this stop |
| --- | --- |
| 01 | Empty · maximum remaining 0% |
| 02 | Empty · maximum remaining 0% |
| 03 | Full · minimum fill 100% |
| 04 | Full · minimum fill 70% |

Configure the corresponding platforms to unload wagons 01–02 and load wagons 03–04. PTC checks all four conditions together. Add a partner stop if both trains should wait for each other.

## Current limitations

- **Top-ups:** a supplied r30 screenshot reports 39 missing items and “Last top-up made no progress”. Exact-full top-ups remain under investigation. The 1.0.0 branding update does not change that loading logic.
- **Validation:** paired departure has been confirmed in play. The r31 graphical redesign has been shown in game; the 1.0.0 logo integration still needs its native build and visual check. Multiplayer, dedicated servers, mixed cargo, fluid behavior and persistence of the new templates/targets have not completed release validation.
- **Targets:** PTC does not stop a transfer at an exact item count or partial-fill threshold.

If a train becomes stuck, inspect its wait reason and platform settings. The manual-release action is available when PTC is holding that stop; it does not count as satisfying its cargo conditions.

## Development and feedback

See [build and test instructions](BUILD.md) for the source package and [test details](docs/TESTMATRIX.md) for the checks still required. [Release notes](CHANGELOG.md) describe the latest changes.

When [reporting a problem](https://github.com/DerDoesewicht/PioneerTrainControl/issues), include the displayed mod version, the game log, the train/stop rules, platform filters, expected behavior and what actually happened. For loading issues, include wagon and platform counts before and after a complete transfer cycle.

Created by **Doesewicht**. An unofficial Satisfactory mod.

## Network usage

Pioneer Train Control does not create external network connections, contact third-party web APIs or collect telemetry. In multiplayer, it uses Satisfactory's existing game connection to exchange train and station information, wagon cargo status, departure rules, paired-stop settings and reusable templates between the player and the host/server. This includes player-entered search text, train/station names and template names where needed by these features. Menu data is requested while the panel is open; edits are sent when the player performs an action. Rules and templates are stored with the world save on the host/server. The mod does not upload them to an external service. This statement covers Pioneer Train Control itself, not the base game, platform services or other mods.

## AI usage

Generative AI (ChatGPT/Codex) was used extensively during development to generate and revise C++ source code, UI implementation, build and installation scripts, automated tests, debugging suggestions, German/English translations, documentation, mod-page descriptions and changelogs. The mod logo was generated with an AI image-generation tool. Feature direction and in-game feedback were provided by the developer. The supplied gameplay screenshots are actual in-game captures, not AI-generated images. Pioneer Train Control does not run a generative AI model or call an AI service during gameplay, and it does not send gameplay data to an AI provider at runtime.
