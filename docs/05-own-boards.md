# Owner boards: evidence and limits

Consolidated on 2026-10-30 from existing bring-up and research records. **No new device access was performed for this catalog entry or its English translation.** These are historical findings, not a live query. The two units are identified only as Board 1 and Board 2.

| Item | Board 1 | Board 2 | Evidence scope |
| --- | --- | --- | --- |
| Owner-reported model | ESP32-P4-WIFI6-POE-ETH | ESP32-P4-WIFI6-POE-ETH | Exact PCB revision still requires visual identification |
| Chip revision | P4 v1.3 | P4 v1.3 | Readout dated 2026-10-29 |
| Flash | 32 MiB | 32 MiB | Read out and fully backed up locally before installation |
| PSRAM | 32 MiB | 32 MiB | Detection and successful SPI-SRAM startup test |
| CPU / PSRAM settings | 360 / 200 MHz | 360 / 200 MHz | Firmware configuration, not an external clock measurement |
| Bring-up SDK | ESP-IDF 5.5.4 | ESP-IDF 5.5.4 | Revision-1.x firmware booted |
| Experimental power | USB-C from computer | USB-C from computer | Ethernet without PoE |
| Ethernet | DHCP and application communication | DHCP and application communication | Successful standalone and two-board runs documented |
| C6 wireless | Not used | Not used | WLAN/BLE remain untested |
| Flash preservation | Original kept privately | Original kept privately | Restoration not practically qualified |
| Secure boot / flash encryption | Disabled at bring-up | Disabled at bring-up | No eFuse changes in the documented work |

## What the existing experiments establish

The boards booted the owner firmware, initialized PSRAM and Ethernet, stored a model package in flash and generated text locally. After restart, the model loaded again. Later normal LAN firmware and model updates are documented. These results establish a working P4/memory/Ethernet path in the described setup.

Selected published evidence is available in the [cluster repository at reviewed commit 0675f868](https://github.com/Mcgee1704/esp32-p4-llm-cluster-research/tree/0675f8687b9459fafa4545587ef14aedd118187d). This catalog does not track live model or firmware versions. Determine the installed versions again when a future task depends on them.

## Unresolved items

- PCB revision, black/coloured header version and physical pin-1 assignment.
- Exact P4 flash component, C6 module, C6 firmware and antenna assembly.
- PoE module type, R12 population, H5 position, current budgets and electrical qualification of the proposed PoE/USB chain.
- WLAN, BLE, SD card, USB OTG application use, audio, MIPI display and camera.
- Complete testing of all 28 expansion GPIOs, long-duration load and temperature limits.
- Practical original-flash restoration and deliberately interrupted OTA/rollback cases.
- Automatic installation on factory-state neighbours and real hardware tests on P4 revision 3.x.

The [evidence checklist](07-evidence-checklist.md) identifies the photos and owner information needed first. Functional coverage and electrical qualification are separate follow-up work; catalog inclusion does not require every peripheral to be tested.

Complete local records contain device-specific data and remain private. This summary omits MAC addresses, serial numbers, local network addresses, credentials, flash images and raw logs. An untested item is recorded as unresolved, not as a fault.
