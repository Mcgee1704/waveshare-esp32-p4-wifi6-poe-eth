# Evidence needed from the two owner boards

Prepared 2026-10-30. This checklist turns the unresolved items in [Owner boards](05-own-boards.md) into concrete collection steps. It does not report new tests. Use the stable names **Board 1** and **Board 2** throughout.

## Current collection status

Board 1 identification photos have been collected and reviewed. The [visual record](08-board1-visual-record.md) closes the descriptive gaps for PCB Rev2.0, coloured header, P4-Core shield marking, C6-MINI-1U family/antenna cable, H5 link and R12/U2 assembly observations. A speaker is visibly connected. Actual voltage/current behaviour and exact component variants remain open. No suitable measurement equipment has been identified; switch/injector model and complete PoE identity are still unknown. The owner has reopened Board 2 documentation and reports no differences from Board 1. Its [descriptive record](09-board2-owner-comparison.md) is complete with that attribution; independent Board 2 assembly inspection remains unperformed.

The photo list below remains a reference for missing markings or future units; it is not a request to repeat the completed Board 1 photographs or to supply a second set merely to record the Board 2 owner comparison.

## 1. Start with identification photos

If independent identification is needed for a future question, collect a sharp full front view, full back view and relevant close-ups. The following list describes what those images can establish. Disconnect PoE, USB and powered peripherals before handling or repositioning the board. Keep modules and jumpers in their existing positions. If a marking is hidden, record it as unreadable; do not remove RF shields or soldered parts to obtain a picture.

| Photo / information | Must be visible | Gap it can help resolve |
| --- | --- | --- |
| Front and back | Entire PCB, model name, revision/date markings, connectors | PCB identity, assembly differences and fitted accessories |
| P4-Core module | All externally visible module/part markings | Module version; an obscured flash part may remain unidentified |
| C6 module and antenna area | Full module name, suffix such as N4/H8, antenna socket/path and fitted antenna | C6-MINI-1 versus MINI-1U, memory variant indicated by the module and antenna assembly |
| PoE module | Readable module name, label and connector orientation | Exact converter model and the correct power/isolation specifications to look up |
| USB power path | R12 location and nearby U2 marking, as far as accessible | Whether the optional bypass is populated; photo evidence may still require continuity confirmation |
| H5 supply selector | All three positions and existing bridge/link | Intended OUT_LE selection for H1/H2; voltage measurement may still be required |
| P6 header | Both ends, pin-1 marking and nearby silkscreen in one clear orientation | Header version and correspondence between physical contacts and the schematic |

Keep original photos local until a separate publication scope is agreed. Public documentation can usually use a sanitized finding rather than the raw photo. Crop or redact serial numbers, MAC-address labels, Wi-Fi credentials and unrelated surroundings before proposing any public image.

## 2. Provide the current setup and available equipment

- Exact PoE switch or injector model, its power adapter/model if relevant, the port power rating and any documented per-port or total power budget. A model label is more useful than “PoE switch”.
- A simple drawing or description of which Ethernet and USB cable connects to which board, including any existing USB-A-to-USB-C link. Identify cable type and approximate length.
- Any known modifications, replaced modules, solder bridges, jumpers or changes since the recorded 2026-10-29 experiments.
- Installed SD card model/capacity and all attached accessories, with exact camera, display, speaker, USB device or sensor model names where available.
- Whether a multimeter, a USB meter that passes data, a direction-sensitive current measurement method and a temperature probe are available; include their model numbers. Instrument suitability is assessed after the actual supply paths are identified.
- Whether the boards are needed for ongoing work, and when a restart or temporary test firmware would be acceptable. Record the current P4/C6 firmware versions if already known, without resetting or flashing anything to obtain them.

These details let us choose tests that match the installed hardware. A normal USB power meter alone may not establish reverse current or every simultaneous-supply condition.

## 3. Plan local readouts after identification

If current device information is required, first match the physical board, USB interface and intended target chip. A local read-only identification session can then confirm current P4 silicon/flash information and collect boot/firmware version evidence, subject to an agreed connection/reset plan. Reading C6 information is a separate target-specific step; its current firmware is not assumed to be replaceable.

Keep device IDs, network addresses, security state details, backups and raw logs in excluded local storage. Add only the necessary sanitized findings to the catalog. A reported version string and successful startup test remain distinct evidence types.

## 4. Optional functional coverage

These tests can fill additional capability gaps once the required accessories and a recovery path are available. They are not prerequisites for a factual catalog entry.

| Area | What is needed before testing | Evidence to record |
| --- | --- | --- |
| Wi-Fi / BLE | Identified C6 module, compatible known host/C6 firmware, local wireless counterpart and a plan preserving the existing installation | Connection/discovery result, firmware versions, duration and limits; omit credentials and device addresses |
| SD | Identified card and a backed-up or disposable test volume | Mount, write/read verification and persistence; no automatic format of an unknown card |
| USB OTG | A specified compatible USB device/cable and verified supply budget | Enumeration and the actual intended data function; keep this separate from USB-C UART operation |
| Audio | Correct speaker/load and a defined microphone/playback test | Recorded capture/playback result, configuration and limits |
| MIPI display / camera | Exact accessory models, matching FPC orientation and board-specific configuration | Detected sensor/panel, actual capture/display result and operating mode |
| Expansion GPIO | Confirmed physical pin mapping, compatible test fixtures and a conflict-aware pin plan | Pin-by-pin result without disturbing Ethernet, C6 reset, audio or SD supply paths |
| Long-duration operation | Representative workload and temperature measurement | Test duration, conditions, temperatures, resets/errors and firmware configuration |

## 5. Electrical qualification is a separate measurement task

Photos can identify the relevant components but cannot establish current capacity, backfeed behaviour or isolation ratings. First identify the PoE module, R12/U2 path and cable setup, then obtain their specifications and agree measurable limits. Only after that can an appropriate voltage/current/temperature test plan cover individual sources, simultaneous sources, source loss, swapped board roles and realistic load. No multi-board power-chain approval follows from this checklist.

If suitable instruments are unavailable, complete the descriptive identification and keep the electrical result explicitly open. Do not infer safe current sharing from a boot or LED indication. A larger chain requires its own load budget and verification.

## 6. Recovery and other revisions

Original-flash restoration, deliberate OTA interruption and factory-neighbour installation belong to a separately planned recovery/installation task. They require verified backups, an agreed recovery procedure and a suitable test unit or maintenance window. They should not be performed merely to remove an “untested” label from the catalog.

P4 revision-3.x operation requires an actual revision-3.x unit. The two documented revision-1.3 boards cannot supply that evidence. Report that item as outside the available hardware if no such unit is present.

## Collection order

For Board 1, start from the completed [photo review](08-board1-visual-record.md). The next missing information is the exact switch/injector model, actual supply/cable layout and complete PoE identification. Electrical measurements remain open until a suitable method and equipment are available. Board 2's owner comparison is now recorded; no extra photo collection is requested for that descriptive entry. Independent inspection is a separate follow-up if a future question requires it. Review the available evidence before deciding on any firmware change or electrical test. For each later result record the board label, date, supply/peripheral configuration, firmware/tool versions, observed result and remaining limits. Preserve the distinction between manufacturer specification, owner report, visual identification, software readout and measured behaviour.
