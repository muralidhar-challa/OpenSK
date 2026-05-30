# <img alt="OpenSK logo" src="../img/OpenSK.svg" width="200px">

## Seeed Studio XIAO nRF52840

![XIAO nRF52840](https://files.seeedstudio.com/wiki/XIAO-nRF52840/img/2.png)

The [Seeed Studio XIAO nRF52840](https://wiki.seeedstudio.com/XIAO_BLE/)
is a tiny (21×17.8mm) development board powered by the Nordic nRF52840 SoC.

### Pin Mapping

| Function | Pin    | Notes                        |
|----------|--------|------------------------------|
| LED 0    | P0.26  | Red channel of onboard LED   |
| LED 1    | P0.30  | Green channel (used for status) |
| LED 2    | P0.06  | Blue channel                 |
| Button   | P0.02  | External button (active low) |

> **⚠️ Important:** The XIAO nRF52840 does not have a built-in user button.
> You must connect a tactile switch between **D0 (P0.02)** and **GND** for
> FIDO2 user presence confirmation. A wire to GND works for testing.

### Flashing

To flash OpenSK, first put the XIAO into DFU/bootloader mode:

1. **Double-tap** the reset button quickly (two rapid presses)
2. The onboard LED should fade in/out, indicating bootloader mode
3. The board appears as a USB mass storage device named `XIAO52840` or `XIAO-SENSE`

If the board doesn't enter bootloader mode:
- Connect to a computer via USB-C
- Hold the **BOOT** button (if present) while connecting, or
- Double-tap the reset button more quickly

Then run:

```sh
./flash.sh nrf52840_xiao
```

This compiles OpenSK, merges the bootloader, converts to UF2 format, and flashes.

To update without erasing stored credentials:

```sh
./flash.sh --update nrf52840_xiao
```

### Customization

To enable additional features like debug logging:

```sh
./flash.sh --features=ctap1,config-command,debug nrf52840_xiao
```

### LEDs

| Pattern                      | Cause                  |
|------------------------------|------------------------|
| Green slow blinking          | Asking for touch       |
| Green fast blinking for 5s   | Wink (just saying Hi!) |

### Notes

- The XIAO nRF52840 has 1MB of internal flash, same as the nRF52840 Dongle
- The `led-1` feature is automatically enabled, using LED 1 (green) for status
- If your board has a different LED configuration, adjust the pin mappings in
  `third_party/wasefire/crates/runner-nordic/src/main.rs`
