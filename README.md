# Civ6-debug-tools

A small local development helper mod for testing the Unciv `Civ6-mod` ruleset.

This repository is intended for troubleshooting and development only. It should not be included in pull requests to the main Civ6-mod repository.

## Purpose

`Civ6-debug-tools` adds buildable debug buildings that can be used to speed up testing in local games.

Current debug buildings:

- `Debug: Yields`
- `Debug: Food and Growth`
- `Debug: Policy Slots`
- `Debug: Gold Economy`
- `Debug: Great People`

## Installation

Place this folder in your local Unciv mods directory:

```text
Unciv/mods/Civ6-debug-tools/
```

Then enable it alongside `Civ6-mod` when starting or loading a test game.

## Console testing

Useful commands:

```text
city addbuilding Debug: Yields
city removebuilding Debug: Yields
city addbuilding Debug: Policy Slots
city removebuilding Debug: Policy Slots
```

Road testing command confirmed in the current test build:

```text
Tile setimprovement Road
```

## Development policy

Keep all debug content prefixed with `Debug:`.

Do not merge this repository into Civ6-mod. This is a separate local helper mod for development troubleshooting.

## Notes

Some uniques may require adjustment depending on current Unciv support and Civ6-mod resource naming. Test each building individually before adding more debug tools.
