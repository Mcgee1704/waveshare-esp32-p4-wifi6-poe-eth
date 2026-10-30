# Owner boards: evidence and limits

Updated 2026-10-30 from historical bring-up/research records, a visual review of Board 1 and a subsequent owner comparison for Board 2. **No new device access or electrical test was performed.** Software records describe earlier operation; photographs add visible assembly identification. The two units remain Board 1 and Board 2. The owner has reopened Board 2 documentation and reports no differences from Board 1. That general statement is recorded separately from independent photo identification.

| Item | Board 1 | Board 2 | Evidence scope |
| --- | --- | --- | --- |
| Model | ESP32-P4-WIFI6-POE-ETH, visible on PCB | Owner-reported same model as Board 1 | Board 1 photographs; Board 2 owner comparison |
| PCB revision | **Rev2.0** | Owner reports no differences; no independent revision reading | Board 1 photo and Board 2 owner report dated 2026-10-30 |
| Header version | Coloured, row markers 1/2 visible | Owner reports no differences; no independent header inspection | Board 1 photo / Board 2 owner report; no full continuity check |
| Chip revision | P4 v1.3 | P4 v1.3 | Historical readout dated 2026-10-29; distinct from PCB revision |
| Flash | 32 MiB | 32 MiB | Historical readout and private backup; Board 1 shield also marked Flash 32MB |
| PSRAM | 32 MiB | 32 MiB | Earlier detection and successful SPI-SRAM startup test |
| CPU / PSRAM settings | 360 / 200 MHz | 360 / 200 MHz | Earlier firmware configuration; not an external clock measurement |
| Bring-up SDK | ESP-IDF 5.5.4 | ESP-IDF 5.5.4 | Revision-1.x firmware booted in the documented setup |
| Experimental power | USB-C from computer | USB-C from computer | Earlier Ethernet experiments without PoE |
| Ethernet | DHCP and application communication | DHCP and application communication | Successful standalone/two-board runs documented previously |
| C6 assembly | ESP32-C6-MINI-1U visible, antenna cable attached | Owner reports no differences; no independent module reading | Exact memory suffix/capacity and installed C6 firmware unresolved |
| C6 wireless | Not functionally tested | Not functionally tested | C6 was not used in the recorded experiments |
| H5 selector | Visible 0-ohm link on VCC/3V3 side | Owner reports no differences; no independent link inspection | Actual output voltage unmeasured |
| R12 / U2 | Reference R12 footprint unpopulated; U2 top code P3HE | Owner reports no differences; no independent population/top-code reading | Layout-correlated photo observation; exact U2 ordering part unresolved |
| Speaker | Connected speaker/enclosure and lead visible | Owner reports no differences; no independent accessory inspection | Accessory rating and audio operation unverified |
| Flash preservation | Original kept privately | Original kept privately | Restoration not practically qualified |
| Secure boot / flash encryption | Disabled at bring-up | Disabled at bring-up | Historical record; no eFuse changes in the documented work |

## Existing functional evidence

Earlier experiments booted the owner firmware, initialized PSRAM/Ethernet, stored a model package and generated text. The model loaded after restart. Later normal LAN firmware/model updates are documented. These findings establish a P4/memory/Ethernet path in the recorded configuration; the current photo review adds no new functional result.

Selected published evidence is in the [cluster repository at reviewed commit 0675f868](https://github.com/Mcgee1704/esp32-p4-llm-cluster-research/tree/0675f8687b9459fafa4545587ef14aedd118187d). Current firmware/model versions must be checked again when a future task depends on them.

## Board 1 visual evidence

The [dedicated visual record](08-board1-visual-record.md) documents the 18-photo review, visible markings, source boundaries and the U2 top-code comparison. Manufacturer statements, visual identification, software readout and electrical measurement remain different evidence types. Raw photographs and their provenance/hash index are kept locally.

## Board 2 owner comparison

Source **OWN-REPORT-20261030-B2**, dated 2026-10-30, records the owner's statement that Board 2 has no differences from Board 1. The [dedicated Board 2 record](09-board2-owner-comparison.md) completes descriptive documentation with that attribution. No independent Board 2 photo review, per-component marking transcription or new test is claimed. The 18 photographs remain Board 1 evidence.

## Remaining work

- Both boards: exact P4 flash device, C6 memory variant/firmware, exact U2 ordering part, complete PoE module identity, switch/injector model and supply/cable arrangement.
- Both boards: measured H1/H2 voltage, current budgets, reverse-current behaviour, load sharing and thermal qualification. No suitable instruments were identified for this review.
- WLAN/BLE, SD, USB OTG application use, audio, MIPI camera/display, complete GPIO coverage, long-duration load and recovery remain untested by this task.
- Original-flash restoration, deliberate OTA interruption and automatic factory-neighbour installation require separate planning.
- Physical revision-3.x evidence requires a suitable unit; the recorded chips are revision 1.3.
- Board 2: independent assembly/marking verification remains open. The descriptive entry is complete as an owner-reported comparison; Board 1 photographs are not reattributed to Board 2.

The [evidence checklist](07-evidence-checklist.md) tracks what is complete and what remains open. Catalog inclusion does not require every peripheral to be tested. Device IDs, private network information, credentials, original images, flash backups and raw logs remain outside publication.
