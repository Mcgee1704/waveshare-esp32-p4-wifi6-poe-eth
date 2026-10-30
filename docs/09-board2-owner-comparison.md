# Board 2: owner-reported comparison

Recorded **2026-10-30**. Source ID: **OWN-REPORT-20261030-B2**.

The owner reopened Board 2 documentation and stated that there are **no differences between Board 2 and Board 1**. This English summary records that general comparison as an owner statement. It completes the descriptive catalog record within that evidence scope.

## What the comparison covers

The reference is the [Board 1 visual record](08-board1-visual-record.md). That record identifies PCB Rev2.0, a coloured header, the P4-Core shield marking, the C6-MINI-1U family and antenna cable, the H5 link, R12/U2 assembly observations, the visible PoE area and the connected speaker. Board 2 is reported by the owner to have no differences from that board.

This is a general owner comparison, not a separate transcription of each Board 2 marking. No independent Board 2 photo review was performed. The existing 18 photographs retain their Board 1 attribution; they are not relabelled or counted as a second photo set. No additional photographs are required merely to record the owner's statement.

## Evidence for Board 2

| Evidence | Recorded result | Limit |
| --- | --- | --- |
| Earlier P4 readout | Silicon revision 1.3; 32 MiB flash and 32 MiB PSRAM; PSRAM startup test passed | Historical evidence dated 2026-10-29; no fresh readout |
| Earlier configuration | ESP-IDF 5.5.4; CPU 360 MHz and PSRAM 200 MHz configured | No independent clock measurement; no claim about present firmware |
| Earlier Ethernet use | DHCP and application communication with USB-C power and Ethernet without PoE | Does not establish C6, PoE, audio or other peripheral operation |
| Owner comparison | No differences reported relative to Board 1 | Owner statement dated 2026-10-30; no independent Board 2 assembly inspection |

Historical sources remain under **OWN-20261029** in the [source register](../sources/README.md). The [two-board summary](05-own-boards.md) keeps the evidence types separate.

## What remains unresolved

The general comparison does not resolve questions already open on Board 1: the exact U2 ordering part, complete PoE module identity/rating, C6 memory suffix/capacity and firmware, hidden flash-device identity, antenna/accessory ratings, measured H1/H2 voltage, physical pin mapping, current budgets, reverse current, load sharing or temperature. It supplies no new peripheral, endurance or recovery test result.

Board 2 markings and component population have not been independently read or measured. The Board 1 U2 top-code discrepancy and manufacturer variant differences remain unresolved; no exact part or guaranteed electrical rating is inferred from the owner's comparison.

## Data representation and completion boundary

In [board.json](../data/board.json), Board 2 retains its historical readout fields. The new `owner_comparison` object records the reference board, date, source and absence of independent verification. Existing `pcb_revision` and `header_version` fields remain `null` because they were not independently established for Board 2; the owner-reported comparison is recorded separately rather than discarded.

The earlier deferral is lifted for this documentation task. **The descriptive record is complete with an attributed owner report.** Independent Board 2 assembly verification and the remaining component/electrical/functional questions stay open. They are separate follow-up work, not prerequisites for this factual catalog entry. No new device access, reset, firmware installation, eFuse change, wiring change or electrical test was performed.

[Owner boards](05-own-boards.md) · [Remaining evidence checklist](07-evidence-checklist.md) · [Source register](../sources/README.md)
