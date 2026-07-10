# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

A collection of Home Assistant automation blueprints (YAML) shared publicly, plus links to related tips in the README. There is no build system, test suite, or linter — changes are validated by importing the blueprint into a Home Assistant instance.

## Blueprints

- `blueprints/enocean_ptm_215z.yaml` — Controller blueprint for the EnOcean PTM 215Z (Friends of Hue) switch via Zigbee2MQTT v2.0 `event` entities. Implements press vs. hold detection: after a button press trigger, it waits `hold_delay_ms` for a release event (short press) and otherwise loops the "held" action every `tick_ms` until release, breaking out of the repeat loop with a `stop` action. Requires 'Elapsed' enabled in Zigbee2MQTT advanced settings. Uses `mode: restart`.
- `blueprints/tradfri_remote_control.yaml` — Controller blueprint for the Tradfri remote control switch via Zigbee2MQTT v2.0 `event` entities. Implements press vs. hold detection: after a button press trigger, it waits `hold_delay_ms` for a release event (short press) and otherwise loops the "held" action every `tick_ms` until release, breaking out of the repeat loop with a `stop` action. Requires 'Elapsed' enabled in Zigbee2MQTT advanced settings. Uses `mode: restart`.
- `blueprints/intelligent_motion_light_trigger.yaml` — Motion-activated light gated on three conditions: a dusk/dawn indicator sensor (a `sensor` whose state is the string `"True"`, not a binary_sensor — this is deliberate so it can be a template sensor adjustable from the dashboard), a LUX threshold, and an activation blocker binary_sensor that must be `off` or `unavailable` to allow the light to turn on.

## Conventions

- Each blueprint carries a version number in its `name` or `description`; bump it when making changes.
- Blueprints reference their published location via `source_url` pointing to this repo on GitHub (`https://github.com/cbos/home-assistant`).
- The EnOcean blueprint uses the modern `trigger:` key syntax inside trigger lists (Zigbee2MQTT v2.0 / recent HA style); keep new triggers consistent with that.