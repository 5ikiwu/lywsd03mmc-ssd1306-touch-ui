# Build From Source Notes

This repository currently publishes prebuilt binaries and implementation notes for the SSD1306 touch UI firmware. A cleaned source patch is not included in this release.

The binaries were produced from a local modification of ATC v58 for LYWSD03MMC. To create a reproducible source release, start from:

- Upstream repository: <https://github.com/pvvx/ATC_MiThermometer>
- Base target: LYWSD03MMC / `ATC_v58.bin`
- Display replacement: SSD1306 128x64 I2C OLED
- OLED bus: `SDA -> PB7/P11`, `SCL -> PD7/P7`
- Touch input: `PA6/P8`

## Expected Source Changes

A clean source patch should include:

- SSD1306 initialization and command/data write routines.
- A minimal framebuffer or direct page renderer for 128x64 monochrome output.
- Replacement of the LYWSD03MMC segmented LCD render path.
- Page state for temperature, humidity, battery, status, and test/menu views.
- Touch input initialization on PA6/P8.
- Debounce and fast tap handling for page/menu navigation.
- A compile-time option for active-high and active-low touch polarity.

## Reproducibility Checklist

Before claiming a reproducible source build:

1. Rebase the SSD1306 changes onto a tagged upstream commit or commit hash.
2. Commit the patch or source branch.
3. Document the exact toolchain version.
4. Build both touch polarity variants from source.
5. Compare binary hashes with the release files or publish new hashes.
6. Test OTA flashing with TelinkMiFlasher.

## Suggested Build Names

```text
ATC_SSD1306_lopaka_touch_ui_v58.bin
ATC_SSD1306_lopaka_touch_ui_active_low_v58.bin
```

Keep derived build names distinct from official upstream firmware so users do not confuse this project with the pvvx release binaries.
