# Source register

Last reviewed **2026-10-30**. Original sources are linked; local review downloads and crops are excluded from publication. Independent prose and tables were compiled from the sources below.

| ID | Source | Use / limit |
| --- | --- | --- |
| WS-MODEL | [Waveshare board overview](https://docs.waveshare.com/ESP32-P4-WIFI6-POE-ETH) | Sales kits, interfaces and current module description; does not identify the owner-board assembly |
| WS-SCHEMATIC | [Schematic PDF](https://files.waveshare.com/wiki/ESP32-P4-WIFI6-POE-ETH/ESP32-P4-WIFI6-POE-ETH-Schematic.pdf) | Sheet 1: nets and components; the three-page PDF also includes layout views |
| WS-PINOUT-NEW | [Coloured header](https://docs.waveshare.com/assets/images/ESP32-P4-WIFI6-POE-ETH-details-inter-9a44d25075d91a5039181189b5e82867.webp) | Image shows 3V3 left / 5V right; manufacturer image only |
| WS-PINOUT-OLD | [Black header](https://docs.waveshare.com/assets/images/ESP32-P4-WIFI6-POE-ETH-details-inter-2-bc32d0b522f12d2743cb5eb34544484e.webp) | Image shows 5V left / 3V3 right; owner physical mapping unresolved |
| WS-DIMENSIONS | [Dimension drawing](https://docs.waveshare.com/assets/images/ESP32-P4-WIFI6-POE-ETH-details-size-3f5fd8ec650821d9a492dd8dce19bfc2.webp) | 55 × 68 mm, hole centres 48 × 33 mm; not measured on the owner boards |
| WS-3D | [Manufacturer 3D archive](https://files.waveshare.com/wiki/ESP32-P4-WIFI6-POE-ETH/ESP32-P4-WIFI6-POE-ETH-3D.zip) | Linked in the resource register; not downloaded or fit-checked here |
| WS-RESOURCES | [Resources and documents](https://docs.waveshare.com/ESP32-P4-WIFI6-POE-ETH/Resources-And-Documents) | Official source paths and KVM project links |
| WS-IDF | [ESP-IDF instructions](https://docs.waveshare.com/ESP32-P4-WIFI6-POE-ETH/ESP-IDF) | Example structure and pre-v3 / v3.0 / v3.1 configuration distinction |
| WS-FAQ | [FAQ](https://docs.waveshare.com/ESP32-P4-WIFI6-POE-ETH/FAQ) | Manufacturer permits simultaneous USB-C/PoE; no multi-board USB power-chain qualification |
| ESP-P4-DS | [ESP32-P4 Series Datasheet](https://documentation.espressif.com/esp32-p4_datasheet_en.pdf) | Retrieved version 0.7; family memory and strapping; applicability to early owner silicon must be established |
| ESP-ETH | [ESP-IDF 5.5.4 Ethernet](https://docs.espressif.com/projects/esp-idf/en/v5.5.4/esp32p4/api-reference/network/esp_eth.html) | RMII configuration, clock/data roles and PHY drivers |
| OWN-20261029 | [Published hardware summary at commit 0675f868](https://github.com/Mcgee1704/esp32-p4-llm-cluster-research/blob/0675f8687b9459fafa4545587ef14aedd118187d/docs/HARDWARE.md) | Two owner P4s; local 2026-10-29 bring-up records add startup/readout/backup evidence; raw records remain private |

## Checksums of reviewed manufacturer files

| File / source ID | Bytes | SHA-256 |
| --- | --- | --- |
| Schematic / WS-SCHEMATIC | 1734900 | `885b8f038881c6656486fea143bcf749f17c6a1ec9006cc693dcdb298018380b` |
| Coloured header / WS-PINOUT-NEW | 41258 | `9b6892a66bfadc64c9c8810d2a2dd3ac20a4ffa68ea4ac8b0dbfe929ee8d7535` |
| Black header / WS-PINOUT-OLD | 40278 | `c9b3b932465f56512c98d56e6e3a3fce89a5618a1b5fe9a3e90368522ffdfa25` |
| Dimensions / WS-DIMENSIONS | 49460 | `985a3d975b7d72f9a7996fe7354b94d661b6cb3f025e5d0072bad3c7e13b9cbb` |

The schematic downloaded on 2026-10-30 exactly matches the previously reviewed local file. Sheet 1 was inspected visually, with enlarged connector areas. Identical PDF hashes do not establish identical component populations across production batches. The [machine-readable download register](manufacturer-downloads.json) records the same provenance.

## Conflicting descriptions and their treatment

| Difference | Treatment in this reference |
| --- | --- |
| Schematic C6-MINI-1-N4 versus current C6-MINI-1U-H8 description | Preserve both sourced descriptions; owner module remains unknown |
| P4NRW32 in schematic versus P4NRW32X on product page | Do not assign an unverified package variant to the owner boards |
| 360-MHz board profile versus 400-MHz chip datasheet | Record 360 MHz as the board/experimental setting; 400 MHz is a family specification only |
| Opposite left/right columns in old/new header pictures | Keep schematic numbering explicit; identify physical pin 1 before wiring |
| FAQ allows USB-C/PoE together but owner measurements are absent | Separate manufacturer statement from measurements; USB-A power-chain qualification remains open |
| 16-MB default in a general example versus 32-MiB board | Use the identified board capacity and review the complete project configuration |

## Git sources

See the [project register](../docs/06-git-projects.md) and [machine-readable commit list](repositories.json). GitHub metadata was read and entries are pinned to specific commits. Provenance, reuse and license boundaries are described in [PUBLICATION.md](../PUBLICATION.md).

## Future review

For a new PCB revision or changed manufacturer download, first compare the hashes, pictures and nets. Record date, setup, firmware version, observation and limits for additional owner tests. A future link or branch state cannot retroactively establish a historical result. The [evidence checklist](../docs/07-evidence-checklist.md) describes the next collection steps.
