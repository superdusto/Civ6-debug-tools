# Civ6-debug-tools

`Civ6-debug-tools` is a small development helper mod for testing and troubleshooting the Unciv `Civ6-mod` ruleset.

This mod is intended for local development only. Do not merge debug buildings or debug uniques into the main `Civ6-mod` repository or include them in Civ6-mod pull requests.

## Purpose

The mod adds buildable debug buildings and optional debug uniques that make it easier to test Civ6-mod mechanics without playing through a full normal game.

Current uses include:

- Quickly adding city yields for testing production, growth, science, culture, and gold behavior.
- Adding large numbers of policy slot resources for policy/government testing.
- Granting Tier 1 Government capacity for government testing.
- Speeding up worker tile-improvement testing.

## Repository structure

For the current Unciv mod loader, `ModOptions.json` belongs inside the `jsons` folder.

```text
Civ6-debug-tools/
├── README.md
├── LICENSE
└── jsons/
    ├── ModOptions.json
    ├── Buildings.json
    └── GlobalUniques.json
```

## Installation

Install the whole `Civ6-debug-tools` folder into your local Unciv mods directory.

Expected local install path:

```text
Unciv/mods/Civ6-debug-tools/
```

Then enable both mods when creating or loading a test game:

```text
Civ6-mod
Civ6-debug-tools
```

## Current debug buildings

### Debug: Yields

Adds large city yields for general testing.

Current fields:

```json
"production": 100,
"gold": 100,
"science": 100,
"culture": 100,
"food": 100
```

Console command:

```text
city addbuilding "Debug: Yields"
```

Remove command:

```text
city removebuilding "Debug: Yields"
```

### Debug: Gold Economy

Adds a large gold yield for economy testing.

Current field:

```json
"gold": 1500
```

Console command:

```text
city addbuilding "Debug: Gold Economy"
```

Remove command:

```text
city removebuilding "Debug: Gold Economy"
```

### Debug: Food and Growth

Adds a large food yield for growth testing.

Current field:

```json
"food": 500
```

Console command:

```text
city addbuilding "Debug: Food and Growth"
```

Remove command:

```text
city removebuilding "Debug: Food and Growth"
```

### Debug: Policy Slots

Provides policy slot resources and Tier 1 Government capacity for policy/government testing.

Current uniques:

```json
"Provides [30] [Military Policy Slots]",
"Provides [30] [Economic Policy Slots]",
"Provides [30] [Diplomatic Policy Slots]",
"Provides [30] [Wildcard Policy Slots]",
"Provides [2] [Tier 1 Government]"
```

Console command:

```text
city addbuilding "Debug: Policy Slots"
```

Remove command:

```text
city removebuilding "Debug: Policy Slots"
```

## Current global debug uniques

`jsons/GlobalUniques.json` currently applies faster worker improvement construction globally whenever the mod is enabled.

Current uniques:

```json
"Can build [Land] improvements at a [+900]% rate",
"Can build [All Road] improvements at a [+900]% rate"
```

This means worker improvement speed is active even before any debug building is constructed.

If worker speed should be controlled by a building instead, move the improvement-speed unique into a building such as `Debug: Builder Speed` and remove `GlobalUniques.json`.

Verified building-style syntax from base Unciv uses this form:

```json
"Can build [all] improvements at a [+25]% rate"
```

A debug building version can use:

```json
{
  "name": "Debug: Builder Speed",
  "cost": 1,
  "maintenance": 0,
  "isNationalWonder": true,
  "uniques": [
    "Can build [all] improvements at a [+900]% rate"
  ]
}
```

Console command:

```text
city addbuilding "Debug: Builder Speed"
```

## Console command notes

Unciv console commands require quotation marks around multiword item names.

Correct:

```text
city addbuilding "Debug: Yields"
city removebuilding "Debug: Yields"
```

Incorrect:

```text
city addbuilding Debug: Yields
```

Confirmed road testing command:

```text
Tile setimprovement Road
```

The `Tile` prefix is required in the current tested Unciv build.

## Development rules

Use this workflow when adding new debug tools:

1. Add one building or unique at a time.
2. Use only verified Unciv syntax from Unciv source, Unciv docs, or Civ6-mod source.
3. Reload mods.
4. Start or load a test game with `Civ6-mod` and `Civ6-debug-tools` enabled.
5. Add the debug building with a console command.
6. Confirm behavior in-game.
7. Commit only after the change loads and works.

Do not guess unique syntax. If a unique has not been verified from source or documentation, mark it as unverified and test it separately.

## Human-only availability

AI players may build debug buildings if they are available normally.

The intended fix is to add this unique to each debug building:

```json
"Only available <for [Human player] Civilizations>"
```

Add this only after confirming it loads correctly in the current Unciv/Civ6-mod setup.

## Notes

- Keep all debug content prefixed with `Debug:`.
- Keep this repository separate from Civ6-mod.
- Do not include debug content in Civ6-mod pull requests.
- Prefer small, testable commits over large batches of unverified changes.
