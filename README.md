# Midea — HA Core 2026.11.1 repackaged as a custom component

This repository contains the **built-in `midea` integration from
Home Assistant Core 2026.11.1**, copied verbatim from
[home-assistant/core](https://github.com/home-assistant/core) (tag `2026.11.1`,
path `homeassistant/components/midea/`), and repackaged as a custom component
so it can be installed through the Home Assistant Marketplace.

## Why this exists

The target Home Assistant instance carries a pre-core custom copy of this same
integration (domain `midea`, the midea_ac_lan / midea-local lineage) in
`config/custom_components/midea/`. HA 2026.11 removed the `EntityCategory`
re-export from `homeassistant.components.sensor`, so that old copy's
`sensor.py` dies on import:

```
ImportError: cannot import name 'EntityCategory' from
'homeassistant.components.sensor'
```

…and the whole config entry fails to set up
(`Error setting up entry Midea Air for midea`).

Installing this repository replaces the stale copy with the current Core code
for the same domain. Entity `unique_id`s (`<device_id>_<entity_key>`), the
config-entry data format, and the `midea-local==15.0.0` requirement are
identical to Core, so the existing config entry and all of its entities carry
over unchanged.

## Changes vs. upstream Core

- `manifest.json`: reduced to the classic custom-integration field set and a
  `"version": "2026.11.1"` key added (custom components require one).
  Everything else — all Python code, `strings.json`, `icons.json` — is
  byte-identical to Core 2026.11.1.
- `quality_scale.yaml` (Core-internal metadata) is not included.

## License & attribution

All integration code is © the Home Assistant Core contributors and the Midea
integration authors (@chemelli74, @rokam), licensed under the Apache License
2.0 — see `LICENSE`. This repack is a personal-use maintenance copy, not an
official release. Once the stale custom copy is no longer needed, the built-in
Core integration should be preferred.
