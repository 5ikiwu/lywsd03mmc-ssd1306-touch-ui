# Firmware Behavior

This document describes the behavior of the SSD1306 touch UI build at a high level.

## Display Path

The stock LYWSD03MMC uses a segmented LCD. This firmware build targets a modified device where that LCD has been removed and replaced with a 128x64 SSD1306 OLED.

The display code initializes the OLED controller, clears the display, and renders compact monochrome pages. The UI is intentionally simple because the Telink MCU has limited RAM and the original firmware was designed for a segmented display, not a full bitmap screen.

## Pages

The UI is designed around small pages:

- Temperature and humidity summary.
- Battery and device status.
- Comfort/status overview.
- Test/menu page for checking input and display behavior.
- In the personalized build, an `OANA` menu entry opens a small page with `OANA` and `<3` heart markers.

The exact page content may change between experimental builds. The main goal is to keep readings readable on a small OLED while avoiding overlapping text.

## Touch Navigation

The touch sensor output is connected to PA6/P8 and read as a digital input.

The firmware debounces touch transitions and treats a touch as a navigation event. The normal build expects active-high output. The active-low build inverts the input.

## BLE Behavior

The firmware remains based on ATC v58, so BLE advertising, OTA update behavior, sensor sampling, and configuration behavior come from the upstream ATC firmware. This project changes the local display and touch UI behavior.

## Power Behavior

The original LCD is extremely low power. The SSD1306 OLED uses more current, especially when many pixels are lit. For long-running installations, use an external 3.3 V supply or accept shorter battery life.

## Design Notes

The visual direction was inspired by modern monochrome OLED UI layouts and by Lopaka-style compact menu previews. The firmware does not include Lopaka code or assets.
