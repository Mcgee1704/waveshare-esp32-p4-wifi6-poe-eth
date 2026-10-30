# Programming and project profile

Updated 2026-10-30. This is a reference. No firmware was installed or modified during this board-documentation task.

## USB and boot

USB-C reaches the P4 UART through CH343P. P4 TX GPIO37 and RX GPIO38 also appear on H2/P6. Avoid conflicting drivers when attaching an external UART device. USB-A is the native HS OTG port; it serves a different interface.

The schematic connects BOOT to **GPIO35** and RESET to `ESP_EN`. The manufacturer describes holding BOOT during power-up or reset to enter download mode. GPIO0 is not this board's BOOT button. CH343 DTR/RTS drive automatic boot/reset through U6.

GPIO35–38 affect boot mode; GPIO34 selects the JTAG source. GPIO35 is also Ethernet TXD1, so BOOT cannot serve as an independent application button while Ethernet uses that signal. Loads on GPIO36–38 must respect boot requirements. Sources: [chip datasheet, chapter 3](https://documentation.espressif.com/esp32-p4_datasheet_en.pdf), WS-SCHEMATIC.

## Building for the correct revision

Both owner P4s are documented as **revision 1.3**. Existing bring-up records establish **ESP-IDF 5.5.4** with a revision-1.x profile. A 3.x build was checked separately but not tested on physical 3.x hardware. Silicon revision and PCB revision are separate identifiers.

Waveshare provides configuration files for pre-v3, v3.0 and v3.1 chips. Rebuild using the matching profile if a revision mismatch is reported; bypassing it with `--force` does not correct the configuration. An existing `sdkconfig` can override new defaults. See the [manufacturer ESP-IDF chapter](https://docs.waveshare.com/ESP32-P4-WIFI6-POE-ETH/ESP-IDF).

Excerpt from the existing working profile; this is not complete firmware:

```ini
CONFIG_IDF_TARGET="esp32p4"
CONFIG_ESPTOOLPY_FLASHSIZE_32MB=y
CONFIG_ESPTOOLPY_FLASHMODE_QIO=y
CONFIG_SPIRAM=y
CONFIG_SPIRAM_SPEED_200M=y
CONFIG_ESP32P4_SELECTS_REV_LESS_V3=y
CONFIG_ESP32P4_REV_MIN_100=y
CONFIG_ETH_USE_ESP32_EMAC=y
```

These option names refer to the existing IDF-5.5.4 profile. Other IDF versions need a fresh configuration review. Some general Waveshare examples default to 16-MB flash; that does not identify this board's capacity. Check flash size and the full partition layout together.

## Ethernet

| Parameter | Assignment |
| --- | --- |
| MAC / PHY | Internal P4 EMAC / IP101GRI |
| Management | MDC GPIO31, MDIO GPIO52 |
| PHY reset | GPIO51 |
| RMII reference clock | GPIO50, external input from the PHY |
| Transmit | TX_EN 49, TXD0 34, TXD1 35 |
| Receive | CRS_DV 28, RXD0 29, RXD1 30 |
| PHY address | Existing firmware uses autodetection (`-1`); do not assume address 0 or 1 without evidence |

Configure the clock, data pins, management pins and PHY type consistently in ESP-IDF. Existing tests cover DHCP and application traffic, beyond link-up alone. [Espressif Ethernet reference](https://docs.espressif.com/projects/esp-idf/en/v5.5.4/esp32p4/api-reference/network/esp_eth.html).

## C6, SD and audio

WLAN/BLE needs compatible host and C6 firmware. The current MCU-host implementation is [ESP-Hosted-MCU](https://github.com/espressif/esp-hosted-mcu); `esp-hosted` now directs readers to separate implementations. The installed owner C6 firmware is unknown and was not replaced. C6 family capabilities do not establish enabled Thread/Zigbee support in a particular firmware.

SDMMC uses CMD44, CLK43 and D0–D3 39/40/41/42. GPIO45 controls the Q1 card-supply path; check its operation and supply voltage against the board implementation. Automatic formatting can erase existing card contents.

ES8311 uses I2C7/8 and I2S: MCLK13, BCLK12, LRCK10, codec ASDOUT11 and DSDIN9. GPIO53 controls the amplifier. SDA/SCL are shared with expansion and MIPI control connectors; coordinate addresses, pull-ups and initialization in each project.

## Profile for a future project

Before installation, record model/PCB revision, chip revision, C6 module, supply setup, peripherals, pin assignments, IDF/component versions, flash size, partitions, expected boot output and measurable acceptance criteria. Preserve the existing flash state and plan recovery. Keep secrets in excluded local configuration. Security eFuses are permanent and outside ordinary board documentation.

This reference contains no firmware images or automatic flashing procedure. Suitable starting projects appear in the [project register](06-git-projects.md). The [evidence checklist](07-evidence-checklist.md) separates information collection from later tests requiring a planned firmware change.
