# Pinout and GPIO usage

Updated 2026-10-30. Source: WS-SCHEMATIC, SHA-256 `885b8f038881c6656486fea143bcf749f17c6a1ec9006cc693dcdb298018380b`, sheet 1. Contacts were transcribed from the visually reviewed schematic. [Source register](../sources/README.md).

## Establish orientation and revision first

The [new coloured-header picture](https://docs.waveshare.com/assets/images/ESP32-P4-WIFI6-POE-ETH-details-inter-9a44d25075d91a5039181189b5e82867.webp) shows 3V3 at the upper left and 5V at the upper right. The [older black-header picture](https://docs.waveshare.com/assets/images/ESP32-P4-WIFI6-POE-ETH-details-inter-2-bc32d0b522f12d2743cb5eb34544484e.webp) shows 5V on the left and 3V3 on the right. The other columns are reversed as well.

The numbering below follows **schematic symbol P6** only. It does not establish an unverified left/right position on an owner board. Check pin 1, supplies, GND, silkscreen and PCB revision before wiring. A 40-pin shape does not establish Raspberry Pi pin compatibility.

## P6: all 40 contacts

| Schematic pin | Signal | Schematic pin | Signal |
| --- | --- | --- | --- |
| 1 | VCC_5V | 2 | ESP_3V3 |
| 3 | VCC_5V | 4 | GPIO7 |
| 5 | GND | 6 | GPIO8 |
| 7 | GPIO37 | 8 | GPIO23 |
| 9 | GPIO38 | 10 | GND |
| 11 | GPIO22 | 12 | GPIO21 |
| 13 | GND | 14 | GPIO20 |
| 15 | GPIO5 | 16 | GPIO6 |
| 17 | GPIO4 | 18 | ESP_3V3 |
| 19 | GND | 20 | GPIO3 |
| 21 | GPIO1 | 22 | GPIO2 |
| 23 | GPIO36 | 24 | GPIO0 |
| 25 | GPIO32 | 26 | GND |
| 27 | GPIO25 | 28 | GPIO24 |
| 29 | GND | 30 | GPIO33 |
| 31 | GPIO54 | 32 | GPIO26 |
| 33 | GND | 34 | GPIO48 |
| 35 | GPIO46 | 36 | GPIO53 |
| 37 | GPIO27 | 38 | GPIO47 |
| 39 | GPIO45 | 40 | GND |

This accounts for 28 different GPIO nets, two 3.3-V contacts, two 5-V contacts and eight grounds. An exposed GPIO is not automatically available; several contacts already connect to onboard peripherals.

## Additional connectors

All numbers are schematic contacts. Mounting/shield contacts numbered 0 are excluded. The manufacturer identifies H1/H2 as SH1.0 and H4 as MX1.25. Physical plug orientation has not been electrically verified. Board 1 photographs identify the coloured header and its row markers; its H5 link is documented in the [visual record](08-board1-visual-record.md). Board 2 is deferred.

| Connector | Schematic contact sequence |
| --- | --- |
| H1 | 1: OUT_LE; 2: GND; 3: GPIO7; 4: GPIO8 |
| H2 | 1: OUT_LE; 2: GND; 3: GPIO38; 4: GPIO37 |
| H4 | 1: PA_OUTL-; 2: PA_OUTL+ |
| H5 | 1: ESP_3V3; 2: OUT_LE; 3: VCC_5V |
| H7 | 1: C6_U0TXD; 2: C6_U0RXD; 3: GND; 4: C6_IO9 |
| J6 | 1: GND; 2: VCC_5V |
| PoE | 1: VDD; 2: VSS; 3: PGND; 4: VCC_5V; 5: GND |

H1 = I2C, H2 = P4 UART, H4 = speaker, H5 = supply selector, H7 = C6 UART/boot, J6 = 5-V supply. OUT_LE does not provide logic-level conversion. Neither H4 speaker contact is ground. The PoE connector is an internal module interface. [Power details](03-power.md).

## MIPI: J1 and J3

| Pin | J1 / DSI | J3 / CSI |
| --- | --- | --- |
| 1 | GND | GND |
| 2 | DSI_D1_N | CSI_D0_N |
| 3 | DSI_D1_P | CSI_D0_P |
| 4 | GND | GND |
| 5 | DSI_CLK_N | CSI_D1_N |
| 6 | DSI_CLK_P | CSI_D1_P |
| 7 | GND | GND |
| 8 | DSI_D0_N | CSI_CLK_N |
| 9 | DSI_D0_P | CSI_CLK_P |
| 10 | GND | GND |
| 11 | ESP_I2C_SCL | CSI_IO0 |
| 12 | ESP_I2C_SDA | CSI_IO1 |
| 13 | GND | ESP_I2C_SCL |
| 14 | ESP_3V3 | ESP_I2C_SDA |
| 15 | ESP_3V3 | ESP_3V3 |

CSI_IO0 connects to 3.3 V through R46 (10 kΩ); the corresponding R47 path on CSI_IO1 is NC. These are not assigned P4 GPIOs. SDA/SCL are GPIO7/8; R50/R48 are 2.2-kΩ pull-ups to 3.3 V. DSI pins 14 and 15 both carry 3.3 V; pin 13 is GND. Connector orientation, supply and panel/sensor drivers must match the accessory.

## Assigned GPIO groups

| Area | P4 GPIOs and functions |
| --- | --- |
| Ethernet | MDC31, MDIO52, reset51, REF_CLK50, TX_EN49, TXD0/1 34/35, CRS_DV28, RXD0/1 29/30 |
| SD | CMD44, CLK43, DAT0/1/2/3 39/40/41/42; Q1 supply control45 |
| Audio | Codec input9 / output11, LRCK10, BCLK12, MCLK13; PA_CTRL53 |
| I2C | SDA7, SCL8; shared by codec, expansion and MIPI control connectors |
| C6 SDIO wiring | P4 14/15/16/17 ↔ C6 20/21/22/23; P4 18/19 ↔ C6 18/19 |
| C6 control signals | P4 6 ↔ C6_IO2; P4 54 ↔ C6_CHIP_PU |
| UART | P4 TX37, RX38; also connected to CH343 and H2/P6 |
| 32-kHz crystal | GPIO0/1 connect to Y2; account for that load |
| Boot / reset | BOOT GPIO35; reset ESP_EN; P4 strapping GPIO34–38 |

The C6 row identifies physical connections in the reviewed schematic. P4 and C6 GPIO numbers belong to separate chips. Match the SDIO CLK/CMD/data roles against the actual host/C6 firmware as well.

GPIO35 shares BOOT with Ethernet TXD1; GPIO45 affects SD power, GPIO53 the amplifier and GPIO54 C6 reset. Loads on UART/strapping pins can affect boot. GPIO6 is already connected to the C6. P4 GPIO24/25 have no schematic connection to C6_IO13/12; neighbouring text labels do not establish a net connection. The full GPIO0–54 assignment is in [gpio-usage.csv](../data/gpio-usage.csv).

USB-A uses dedicated HS signals USBD_N/P. USB-C reaches the CH343 through USB_DBG_D_N/P and then the P4 UART. It is not a direct P4 USB-HS connection.

## CSV scope

The [connector list](../data/pinout.csv) contains **94 numbered contacts** across P6, H1, H2, H4, H5, H7, J6, J1, J3 and PoE. Individual USB/RJ45/SD-slot contacts, module solder pads and shield/mounting contacts are excluded. Their bus functions are documented above. This is neither a complete PCB netlist nor a continuity measurement of the owner boards. The [evidence checklist](07-evidence-checklist.md) describes the remaining physical identification work.
