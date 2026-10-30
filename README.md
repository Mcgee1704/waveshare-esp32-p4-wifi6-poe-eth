# Waveshare ESP32-P4-WIFI6-POE-ETH

Technical reference for the P4 board with Ethernet, a PoE module interface and an ESP32-C6 wireless coprocessor. Updated **2026-10-30**. Manufacturer specifications, schematic findings and existing tests on two owner boards are identified separately.

| Topic | Document |
| --- | --- |
| Model, variants, memory, components and dimensions | [Hardware](docs/01-hardware.md) |
| 40-pin header, additional connectors, GPIO assignments and conflicts | [Pinout](docs/02-pinout.md) |
| USB-C, USB-A, PoE, voltage selection and current budgets | [Power](docs/03-power.md) |
| USB, boot mode, chip revision and ESP-IDF configuration | [Programming](docs/04-firmware.md) |
| Existing evidence and unresolved items for both owner boards | [Owner boards](docs/05-own-boards.md) |
| Board 1 PCB/module identification and H5/R12/U2 photo findings | [Board 1 visual record](docs/08-board1-visual-record.md) |
| Board 2 owner comparison and remaining verification limits | [Board 2 record](docs/09-board2-owner-comparison.md) |
| Manufacturer examples, ESP-Hosted, KVM and cluster research | [Git projects](docs/06-git-projects.md) |
| Photos, equipment information and tests needed to resolve open items | [Evidence checklist](docs/07-evidence-checklist.md) |
| Sources, checksums and conflicting descriptions | [Source register](sources/README.md) |
| Reusable data | [Board JSON](data/board.json), [connector CSV](data/pinout.csv), [GPIO usage](data/gpio-usage.csv) |

## Quick reference

- Model family: ESP32-P4-WIFI6-POE-ETH; Basic kit SKU 32832, C/D kits SKU 32833/32834. The exact accessory kit of the owner boards has not been established.
- Two HP RISC-V cores; **360 MHz** is the documented board profile and existing experimental configuration. One LP core runs at up to 40 MHz. The 400 MHz family specification in the current P4 datasheet does not establish suitability for the owner's revision-1.3 chips.
- **32 MiB flash and 32 MiB PSRAM** documented on both owner P4s; PSRAM startup tests passed.
- Ethernet: IP101GRI, RMII; MDC 31, MDIO 52, reset 51, reference clock 50, TX_EN 49, TXD0/1 34/35, CRS_DV 28, RXD0/1 29/30.
- **USB-C connects to the CH343P UART bridge**; USB-A connects to the native P4 USB HS OTG interface.
- I2C: SDA 7, SCL 8. UART0: TX 37, RX 38. SD: CMD 44, CLK 43, D0–D3 39/40/41/42.
- 40-pin header with 28 GPIO nets; MIPI-DSI, MIPI-CSI, microphone, ES8311 codec and speaker connector.

References: [Waveshare overview](https://docs.waveshare.com/ESP32-P4-WIFI6-POE-ETH), [schematic](https://files.waveshare.com/wiki/ESP32-P4-WIFI6-POE-ETH/ESP32-P4-WIFI6-POE-ETH-Schematic.pdf), [owner evidence](docs/05-own-boards.md).

## Before connecting peripherals

**The manufacturer's black-header and coloured-header pictures show opposite left/right columns.** The CSV and numbered table follow P6 in the reviewed schematic. Identify pin 1, ground and supply contacts on the actual board; image orientation or header colour alone does not verify the wiring.

H1/H2 use the H5-selectable supply `OUT_LE`; their signal levels remain 3.3 V. The manufacturer FAQ allows USB-C and PoE together. A multi-board USB-A-to-USB-C power chain has no established current budget. [Details](docs/03-power.md).

Existing functional results used USB-C power and Ethernet **without PoE**. They do not establish operation of WLAN/BLE, audio, camera, display or SD. The [Board 1 photo review](docs/08-board1-visual-record.md) identifies PCB Rev2.0, a coloured header and an ESP32-C6-MINI-1U with an antenna cable, plus the visible H5/R12/U2 assembly. Exact component variants and electrical behaviour remain open. The owner now reports no differences between Board 2 and Board 1; the [Board 2 record](docs/09-board2-owner-comparison.md) attributes that comparison without claiming an independent photo review. The [checklist](docs/07-evidence-checklist.md) records the remaining work.

This repository contains independent technical notes and source references. It is not an official Waveshare publication. Original PDFs, manufacturer images, private flash backups and raw device logs are kept separately. [Publication scope and rights](PUBLICATION.md).

[Board catalog](https://github.com/Mcgee1704/board-katalog)
