# Flashing Guide

The included firmware files are OTA images for the LYWSD03MMC and are intended to be flashed with the pvvx Telink browser flasher.

## Requirements

- Chrome, Edge, or another browser with Web Bluetooth support.
- Bluetooth enabled on the computer or Android device.
- A stable battery or external 3.3 V power supply.
- The OLED conversion wired before flashing the OLED UI build.

For reliable flashing, pvvx recommends good battery level on LYWSD03MMC devices. Use a stable power source if the original coin cell is weak.

## Flash Main Firmware

1. Open [TelinkMiFlasher](https://pvvx.github.io/ATC_MiThermometer/TelinkMiFlasher.html).
2. Press `Connect`.
3. Select the thermometer from the Bluetooth dialog.
4. If the flasher asks for activation on stock firmware, run the activation step.
5. In the firmware selector, choose `firmware/ATC_SSD1306_oana_touch_ui_v58.bin`.
6. Press `Start Flashing`.
7. Wait until the flasher reports completion.
8. Reconnect power if the OLED does not restart automatically.

## Choose The Touch Variant

Use the normal build first:

```text
firmware/ATC_SSD1306_oana_touch_ui_v58.bin
```

If the menu changes while not touched, or the touch module behaves inverted, flash:

```text
firmware/ATC_SSD1306_oana_touch_ui_active_low_v58.bin
```

## Recovery And Display Tests

If the OLED is blank after flashing:

1. Confirm the OLED module is a 128x64 SSD1306 I2C display.
2. Confirm VCC is 3.3 V and GND is shared.
3. Confirm `SDA -> PB7/P11` and `SCL -> PD7/P7`.
4. Try `firmware/rescue/ATC_SSD1306_force_3C.bin`.
5. If that fails, try the `3D` address or swapped-pin rescue builds.

The rescue builds are for display diagnosis. They do not include the final touch UI.

## Verify Downloads

From the repository root:

```powershell
Get-FileHash -Algorithm SHA256 .\firmware\ATC_SSD1306_oana_touch_ui_v58.bin
```

Compare the result with [firmware/SHA256SUMS.txt](../firmware/SHA256SUMS.txt).

## Warnings

- Flash only on compatible LYWSD03MMC hardware.
- Keep the device powered during OTA flashing.
- This is experimental firmware for a hardware modification.
- Custom firmware is not supported by Mi Home.
