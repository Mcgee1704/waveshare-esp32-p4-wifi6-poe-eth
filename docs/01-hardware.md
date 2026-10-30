# Hardware

Updated 2026-10-30. Source identifiers are resolved in the [register](../sources/README.md).

## Identification and revisions

| Item | Documented finding | Source |
| --- | --- | --- |
| Manufacturer / model | Waveshare ESP32-P4-WIFI6-POE-ETH | WS-MODEL |
| Sales kits | Basic 32832, C 32833, D 32834; owner accessories not established | WS-MODEL |
| P4 module | ESP32-P4-Core; schematic U7 ESP32-P4NRW32, current product description ESP32-P4NRW32X | WS-SCHEMATIC, WS-MODEL |
| Owner silicon revision | Both P4s v1.3; this is separate from PCB revision | OWN-20261029 |
| PCB revision | Not identified on the physical boards | OWN-20261029 |
| C6 in the schematic | U1 ESP32-C6-MINI-1-N4 | WS-SCHEMATIC |
| C6 in the current product description | ESP32-C6-MINI-1U-H8, external antenna | WS-MODEL |
| Owner C6 / antenna path | Exact module marking and C6 firmware not verified | OWN-20261029 |

N4 and H8 must remain separate assembly descriptions. The current sales page does not identify the C6 flash size or antenna variant of the owner boards.

## Processing and memory

| Component / function | Specification | Evidence limit |
| --- | --- | --- |
| HP CPU | Two 32-bit RISC-V cores; 360 MHz in the documented board profile | WS-MODEL, OWN-20261029 |
| LP CPU | One RISC-V core, up to 40 MHz | ESP-P4-DS |
| Internal memory | HP ROM 128 KB, LP ROM 16 KB, HP L2MEM 768 KB, LP SRAM 32 KB, SPM 8 KB | ESP-P4-DS; not all available as free application memory |
| PSRAM | 32 MiB in the P4 package; existing firmware configured for 200 MHz | OWN-20261029; startup test, no complete long-duration stress test |
| P4 flash | 32 MiB SPI NOR; schematic U12 GD25Q256EYIGR | Capacity read out; exact component marking on the owner boards unresolved |
| P4 crystals in the schematic | Y1 40 MHz; Y2 32.768 kHz on GPIO0/1 | Schematic assembly, not measured |
| Ethernet crystal | Y3 25 MHz on IP101GRI | Schematic |

The current ESP32-P4 v0.7 datasheet lists up to 400 MHz CPU and 250 MHz PSRAM clocks. These family specifications do not replace a revision-appropriate board configuration. Existing owner experiments use 360/200 MHz; this documentation task did not change those settings.

## Interfaces and components

| Area | Documented implementation |
| --- | --- |
| Ethernet | U11 IP101GRI, RMII, 100-Mbit/s RJ45 RJ1; no Gigabit Ethernet |
| PoE | BD1/BD2 input bridges and a separate five-pin module interface; see [power](03-power.md) |
| Wireless | ESP32-C6 over SDIO; Wi-Fi 6 and Bluetooth LE. The P4 has no integrated Wi-Fi radio |
| USB-C | Power and UART download/debug through U5 CH343P; U6 EMH4T2R drives reset/boot from DTR/RTS |
| USB-A | Native P4 USB 2.0 HS OTG; `USBD_N/P` are dedicated signals |
| SD | MicroSD/TF SD1; GPIO39–44 data/control bus, Q1 supply switch controlled by GPIO45 |
| Display | J1, 15 contacts, two MIPI-DSI data lanes and a clock lane; matching panel parameters and power budget required |
| Camera | J3, 15 contacts, two MIPI-CSI data lanes and a clock lane; check sensor supply and control bus |
| Audio | U10 ES8311, U8 NS4150B, MIC1, H4 differential speaker output |
| Speaker | Manufacturer specifies 8 Ω / 2 W and an MX1.25 two-pin connector; no owner audio function test |
| I2C / UART | H1/H2, four contacts each, SH1.0; shared supply selection H5 |
| Expansion | P6, 2×20 contacts; 28 GPIO nets, four supply contacts and eight ground contacts |
| Other SoC functions | SPI, I2S, ADC, PWM, RMT, TWAI and others; no CAN or RS485 transceiver in this schematic |

Practical use of P4 MIPI and image acceleration depends on chip revision, drivers, sensor and display. A successful LAN test does not validate camera operation or H.264 encoding.

## Mechanical information

The current manufacturer drawing specifies **55 × 68 mm**, with mounting-hole centres **48 × 33 mm** apart. USB/RJ45 protrusions, installed height, hole diameter, header pitch and enclosure clearances were not measured on the owner boards. For enclosure design, compare the original [3D archive](https://files.waveshare.com/wiki/ESP32-P4-WIFI6-POE-ETH/ESP32-P4-WIFI6-POE-ETH-3D.zip) with the actual board and perform a fit check.

## Information still required

PCB markings, header version, P4/C6 module markings, PoE module, R12 population, H5 position, antenna, accessories and permissible current budgets. Unknown values remain `null` in the [board data](../data/board.json). The [evidence checklist](07-evidence-checklist.md) explains what to collect first.
