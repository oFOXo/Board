# Converting the Markdown Schematic into a Real KiCad Schematic

The Markdown file is a schematic specification, not an EDA schematic. To turn it into a real schematic, use it as the source of truth for symbols, nets, values, and placement rules, then implement those items in KiCad.

## Files Added for the Conversion

- `hardware/kicad/minimal-rp2040-esp32c3/minimal-rp2040-esp32c3.kicad_pro` — KiCad project stub.
- `hardware/kicad/minimal-rp2040-esp32c3/minimal-rp2040-esp32c3.kicad_sch` — A0 schematic sheet carrying the design intent, major nets, and subsystem notes from the Markdown schematic.

## Manual KiCad Conversion Workflow

1. Open `hardware/kicad/minimal-rp2040-esp32c3/minimal-rp2040-esp32c3.kicad_pro` in KiCad.
2. Open the schematic editor and use the A0 sheet notes as a checklist.
3. Place real symbols for these blocks:
   - RP2040 QFN-56.
   - ESP32-C3-MINI-1 or the exact ESP32-C3 module selected for purchase.
   - 3.3 V regulator.
   - USB-C receptacle.
   - QSPI NOR flash.
   - Crystal, buttons, headers, resistors, capacitors, TVS, and fuse.
4. Replace each note with actual wires and net labels:
   - `VBUS`, `VBUS_FUSED`, `+3V3`, and `GND`.
   - `USB_DP` and `USB_DM`.
   - `QSPI_SS_N`, `QSPI_SCLK`, and `QSPI_SD0` through `QSPI_SD3`.
   - `ESP_TXD`, `ESP_RXD`, `ESP_EN_CTL`, `ESP_BOOT_CTL`, and optional `ESP_GPIO_IRQ`.
5. Assign footprints after the schematic symbols are wired.
6. Run KiCad annotation and Electrical Rules Check.
7. Fix all ERC errors before moving to PCB layout.
8. Create the PCB from the schematic and apply the layout notes from the Markdown file, especially the ESP32-C3 antenna keep-out and RP2040 flash/crystal placement constraints.

## Why the First KiCad File Is Note-Driven

A note-driven KiCad sheet is safer than pretending the schematic is complete: the exact USB-C connector, regulator, ESP32-C3 module variant, flash package, and footprints still need selection. Once those parts are chosen, the notes can be replaced one block at a time with verified symbols and footprints.
