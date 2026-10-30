# Power and electrical limits

Updated 2026-10-30. Based on the [schematic](https://files.waveshare.com/wiki/ESP32-P4-WIFI6-POE-ETH/ESP32-P4-WIFI6-POE-ETH-Schematic.pdf), [manufacturer FAQ](https://docs.waveshare.com/ESP32-P4-WIFI6-POE-ETH/FAQ) and existing local review. These findings describe the schematic; the owner-board assembly has not been fully matched to it.

## Supply paths

| Path | Schematic finding | Limit |
| --- | --- | --- |
| USB-C | `Type_C_5V` to `VCC_5V` through Q2 AO3401, controlled by U13 MMDT3906DW | Controlled path; reverse-current behaviour not measured for every supply state |
| USB-A | `VCC_5V` through U2 DIO7003HEST5 to `VBUS_OUT`; R12 shown as parallel NC/0R | Board 1: reference R12 footprint unpopulated in photos, U2 top code P3HE; exact switch/current limit unresolved. Board 2: owner reports no differences, without independent component inspection |
| PoE | RJ45 centre taps / supply pairs through BD1/BD2 to a separate module; module output feeds `VCC_5V` | Standard, input range, power, isolation and module revision not fully established by this baseboard schematic |
| 3.3 V | U3 MP1658GTF-Z, marked “3A MAX” in the plan | Not a 3-A USB-A or expansion-header allowance |
| P4 core | U4 MP1605GTF-Z and P4 internal regulators | Not general-purpose expansion supply outputs |
| Audio | U9 RT9193-33PB generates A3V3 | Not a general peripheral supply |
| J6 | Pin 1 GND, pin 2 VCC_5V | Manufacturer identifies this as a 5-V supply connector; check polarity and the proposed supply combination |

This does not establish suitability for passive PoE or an arbitrary replacement module. The baseboard schematic omits the module's full internal converter circuit. No protection class or certified system isolation voltage is established here.

## USB-C and PoE together

The manufacturer FAQ retrieved on 2026-10-30 explicitly permits simultaneous **USB Type-C and PoE power**. This is a manufacturer statement. It does not provide owner measurements of load sharing or reverse current, or a defined power budget for a chain of boards.

Existing owner tests used USB-C from a computer and Ethernet without PoE. The proposed USB-A-to-USB-C connection between neighbouring boards has not been electrically qualified. Continued operation from a neighbour's USB supply when PoE is removed is accepted behaviour for that proposed setup. Disconnect all supplying paths to fully power a board down.

Current direction, maximum USB-A load, load sharing, voltage drop, temperature and source-loss transitions remain unmeasured. An illuminated LED or successful boot cannot establish these limits.

## Board 1 U2 marking and current budget

The schematic names DIO7003HEST5. The reviewed [DIOO revision-1.4 datasheet, page 2](https://www.dioo.com/uploads/product/20210527/39809ef9c4aeae798493447426d5dd7c.pdf) lists W3HE for that ordering part; the Board 1 photo is read as P3HE. The exact ordering part is therefore unresolved by this evidence. Do not transfer a component-level continuous-current figure into a guaranteed board or USB-chain budget. The empty R12 reference footprint also does not establish measured reverse-current protection.

## H5 and logic levels

H5 is shown as pin 1 = `ESP_3V3`, pin 2 = `OUT_LE`, pin 3 = `VCC_5V`. `OUT_LE` feeds pin 1 of both H1 and H2. Board 1 photographs show a component marked 0 bridging VCC to the 3V3 side, with the 5V selection position unbridged. This is visual evidence of the existing link; actual H1/H2 output voltage has not been measured. The owner reports no differences for Board 2; its H5 link has not been independently inspected or its output measured. See the [Board 2 comparison](09-board2-owner-comparison.md). Establish the voltage before using a voltage-sensitive accessory; connector shape and wire colour do not establish it. See the [Board 1 visual record](08-board1-visual-record.md).

Selecting this supply does **not** change the logic levels of GPIO7/8 or GPIO37/38. They are 3.3-V board signals. Keep 5-V signals away from GPIO inputs. Use appropriate level shifting and a common reference where required, and prevent signal-line back-powering of an unpowered board.

GPIO0/1 are also connected to the 32-kHz crystal path; GPIO36/37/38 are P4 boot-strapping signals. Review the [GPIO conflicts](02-pinout.md) before adding loads.

## Speaker and MIPI

H4 carries amplifier outputs `PA_OUTL-` and `PA_OUTL+`; neither is ground. Connect the speaker between the intended outputs and do not short either output to GND. The manufacturer's 8 Ω / 2 W description is not a measured output-power result from this documentation task.

MIPI connectors require matching contact orientation, lanes, supply and display/camera hardware. Make connections with the equipment powered down.

## Evidence required for a future power chain

First identify the actual PoE module and populated power-path components. Establish their permissible limits before selecting a measurement method. Later measurements need supply voltage, current with identifiable direction, and temperature for each relevant combination: a single source, both sources, a powered/unpowered neighbour, swapped board roles and realistic load. A two-board result does not qualify a larger chain. No such measurements were performed for this documentation task. See the [evidence checklist](07-evidence-checklist.md).
