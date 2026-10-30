# Board 1: visual identification record

Reviewed **2026-10-30** from 18 owner-provided photographs. The owner assigned this photo set to **Board 1** in the current documentation task. Original files and their byte/hash manifest are retained privately. This page contains sanitized observations only; it does not publish photos, QR codes, device identifiers or private Drive links.

## Confirmed visual findings

| Item | Observed on Board 1 | Evidence limit |
| --- | --- | --- |
| Manufacturer / model | Waveshare ESP32-P4-WIFI6-POE-ETH printed on the PCB | Visual model identification |
| PCB revision | **Rev2.0** printed above the RJ45 connector | PCB revision; separate from the earlier software-reported P4 silicon revision 1.3 |
| Expansion header | Coloured 40-contact header; row markers 1 and 2 visible | No electrical pin-by-pin continuity check |
| P4 module | ESP32-P4-Core shield, marked ESP32-P4NRW32 and Flash 32MB | Shield marking; the discrete flash device underneath has not been identified |
| C6 module | **ESP32-C6-MINI-1U** marking; antenna cable attached at its RF connector | Module family and cable assembly identified; exact memory suffix/capacity and installed firmware remain unverified |
| H5 selector | Component marked **0** bridging the VCC/3V3 side; 5V selection position unbridged | Visual evidence of the fitted 0-ohm link; actual H1/H2 output voltage not measured |
| R12 reference footprint | Two exposed solder pads with no resistor body bridging them | Position matched against the manufacturer layout; no continuity or reverse-current measurement |
| U2 reference position | Five-pin device, top marking read as **P3HE** | Observed top code; exact ordering part not confirmed |
| PoE area | Transformer/package marking **2613** and adjacent capacitors visible | Does not identify the complete PoE module or establish its power/isolation rating |
| Speaker | Rear speaker/enclosure and red/black lead connected at SPK visible | Physical accessory present; impedance, power rating and audio function untested |

The [owner-board summary](05-own-boards.md) retains the earlier software/functional evidence separately. These photographs do not add a new silicon/flash readout or prove present firmware versions.

## How the evidence was checked

All 18 files were reviewed in an overview, then the relevant originals were enlarged for module markings, H5 and the R12/U2 area. Existing component placement was compared with sheets 2 and 3 of the [manufacturer schematic/layout PDF](https://files.waveshare.com/wiki/ESP32-P4-WIFI6-POE-ETH/ESP32-P4-WIFI6-POE-ETH-Schematic.pdf).

| Evidence role | Finding supported |
| --- | --- |
| Front overview and revision close-ups | Model, Rev2.0 and coloured header |
| P4/C6 module close-ups | Visible shield/module markings and attached antenna cable |
| H5 close-ups | Existing 0-ohm bridge on the 3V3 side |
| Rear USB-area close-ups | Unpopulated R12 reference footprint and U2 top code |
| PoE-area close-ups | Visible transformer/package marking, without a complete module identification |
| Rear overview and audio-area close-ups | Speaker assembly and connected lead |

Original filenames, private source references and SHA-256 values are retained in an excluded local evidence index. Their omission from this public page does not turn visual observations into measured results.

## U2 marking cross-check

The schematic names **DIO7003HEST5**. The manufacturer's [DIO7003 revision-1.4 datasheet](https://www.dioo.com/uploads/product/20210527/39809ef9c4aeae798493447426d5dd7c.pdf), ordering table on page 2, lists **W3HE** for that part. The photographed code is read as **P3HE**. The reviewed document therefore does not by itself resolve the exact ordering part. An alternative marking or different device cannot be settled from this comparison alone.

Component-level current/protection specifications are not an established USB-A or board-chain rating. R12 appearing unpopulated removes no requirement to identify the fitted switch and check the full supply arrangement. Reverse-current behaviour, load sharing and thermal limits remain unmeasured.

## What can be closed for Board 1

The descriptive record now identifies the PCB revision, coloured header, P4-Core shield marking, C6-MINI-1U family and antenna-cable assembly, visible H5 link and R12 population, U2 top code and presence of a speaker. The available photographs are sufficient for those observations; another photograph of the same areas is not currently required.

## What remains open

- Exact switch/injector model, actual PoE supply state and full cable arrangement.
- Complete PoE module identity/specification beyond the visible 2613 marking.
- Exact U2 ordering part, current budget and electrical behaviour under the intended supply combinations.
- Measured H1/H2 voltage, current direction, load sharing and temperature. No suitable measurement equipment was identified for this review.
- Exact C6 memory variant/readout, installed C6 firmware and wireless function.
- Exact P4 flash component, accessory ratings, peripheral function, complete GPIO coverage, long-duration operation and recovery tests.

No reset, firmware installation, component/jumper change, voltage/current/continuity measurement or new functional test was performed. No RF shield or soldered part needs to be removed to complete this descriptive record. Board 2 is deferred at the owner's request; these observations apply only to Board 1.

[Remaining evidence checklist](07-evidence-checklist.md) · [Source register](../sources/README.md)
