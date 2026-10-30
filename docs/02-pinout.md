# Pinbelegung und GPIO-Nutzung

Stand: 30.10.2026. Quelle: WS-SCHEMATIC, SHA-256 `885b8f038881c6656486fea143bcf749f17c6a1ec9006cc693dcdb298018380b`, Blatt 1. Kontakte wurden aus dem Schaltplan visuell übertragen. [Quellenregister](../sources/README.md).

## Zuerst Orientierung und Revision klären

Die [neue farbige Headeransicht](https://docs.waveshare.com/assets/images/ESP32-P4-WIFI6-POE-ETH-details-inter-9a44d25075d91a5039181189b5e82867.webp) zeigt oben links 3V3 und rechts 5V. Die [ältere schwarze Headeransicht](https://docs.waveshare.com/assets/images/ESP32-P4-WIFI6-POE-ETH-details-inter-2-bc32d0b522f12d2743cb5eb34544484e.webp) zeigt dort links 5V und rechts 3V3. Die weiteren Spalten sind ebenfalls vertauscht.

Die folgende Nummerierung entspricht ausschließlich dem **Schaltplansymbol P6**. Daraus wird keine ungeprüfte Links-/Rechts-Position am eigenen Board abgeleitet. Vor dem Verdrahten Pin 1, Versorgungen, GND, Aufdruck und Platinenrevision abgleichen. Die 40-polige Form bedeutet keine Raspberry-Pi-Pinkompatibilität.

## P6: alle 40 Kontakte

| Pin im Plan | Signal | Pin im Plan | Signal |
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

Damit sind 28 verschiedene GPIO-Netze, zweimal 3,3 V, zweimal 5 V und acht Massekontakte erfasst. Ein herausgeführter GPIO ist nicht automatisch frei: mehrere Kontakte sind bereits mit Peripherie verbunden.

## Zusatzanschlüsse

Alle folgenden Zahlen sind Schaltplankontakte. Befestigungs-/Schirmkontakte mit Nummer 0 sind ausgenommen. H1/H2 sind laut Hersteller SH1.0; H4 ist MX1.25. Physische Steckrichtung am eigenen Exemplar ist nicht bestätigt.

| Anschluss | Kontaktfolge im Plan |
| --- | --- |
| H1 | 1: OUT_LE; 2: GND; 3: GPIO7; 4: GPIO8 |
| H2 | 1: OUT_LE; 2: GND; 3: GPIO38; 4: GPIO37 |
| H4 | 1: PA_OUTL-; 2: PA_OUTL+ |
| H5 | 1: ESP_3V3; 2: OUT_LE; 3: VCC_5V |
| H7 | 1: C6_U0TXD; 2: C6_U0RXD; 3: GND; 4: C6_IO9 |
| J6 | 1: GND; 2: VCC_5V |
| PoE | 1: VDD; 2: VSS; 3: PGND; 4: VCC_5V; 5: GND |

H1 = I2C, H2 = P4-UART, H4 = Lautsprecher, H5 = Versorgungsauswahl, H7 = C6-UART/Boot, J6 = 5-V-Versorgung. OUT_LE ist keine Logikpegelwandlung. H4 hat keinen Massekontakt für den Lautsprecher. Der PoE-Anschluss ist ein interner Modulanschluss. [Versorgungsdetails](03-power.md).

## MIPI: J1 und J3

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

CSI_IO0 wird im Plan über R46 (10 kΩ) an 3,3 V gelegt; der entsprechende R47-Pfad an CSI_IO1 ist NC. Das sind keine zugewiesenen P4-GPIOs. SDA/SCL sind GPIO7/8; R50/R48 bilden Pull-ups mit je 2,2 kΩ nach 3,3 V. DSI führt an Pin 14 und 15 jeweils 3,3 V; nur Pin 13 ist dort GND. Stecker, Kontaktseite, Versorgung und Panel-/Sensortreiber müssen zum Zubehör passen.

## Belegte GPIO-Gruppen

| Bereich | P4-GPIOs und Funktion |
| --- | --- |
| Ethernet | MDC31, MDIO52, Reset51, REF_CLK50, TX_EN49, TXD0/1 34/35, CRS_DV28, RXD0/1 29/30 |
| SD | CMD44, CLK43, DAT0/1/2/3 39/40/41/42; Q1-Versorgungssteuerung45 |
| Audio | Codec-Daten hinein9 / heraus11, LRCK10, BCLK12, MCLK13; PA_CTRL53 |
| I2C | SDA7, SCL8; gemeinsam für Codec, Erweiterung und MIPI-Steueranschlüsse |
| C6-SDIO-Verbindung | P4 14/15/16/17 ↔ C6 20/21/22/23; P4 18/19 ↔ C6 18/19 |
| C6-Nebensignale | P4 6 ↔ C6_IO2; P4 54 ↔ C6_CHIP_PU |
| UART | P4 TX37, RX38; gleichzeitig am CH343 und H2/P6 |
| 32-kHz-Quarz | GPIO0/1 an Y2; nicht als unbelastete Pins behandeln |
| Boot / Reset | BOOT GPIO35; Reset ESP_EN; P4-Strapping GPIO34–38 |

Die C6-Zeile bezeichnet die physischen Verbindungen im geprüften Plan, nicht die P4-GPIO-Nummern des C6. Für SDIO zusätzlich CLK/CMD/Datenrollen aus der passenden Host-/C6-Firmware abgleichen.

GPIO35 teilt BOOT mit Ethernet-TXD1; GPIO45 beeinflusst die SD-Versorgung, GPIO53 den Verstärker und GPIO54 den C6-Reset. Lasten an UART-/Strappingpins können den Start verhindern. Auch GPIO6 ist bereits mit dem C6 verbunden. P4-GPIO24/25 sind dagegen im geprüften Plan nicht mit C6_IO13/12 verbunden; die ähnlich platzierten Textlabels sind keine Netzverbindung. Die vollständige Zuordnung für GPIO0 bis GPIO54 steht in [gpio-usage.csv](../data/gpio-usage.csv).

USB-A nutzt die dedizierten HS-Signale USBD_N/P. USB-C geht über USB_DBG_D_N/P zum CH343 und von dort zum P4-UART. USB-C ist damit kein direkt herausgeführter P4-USB-HS-Port.

## CSV-Umfang

Die [Anschlussliste](../data/pinout.csv) enthält **94 nummerierte Kontakte** von P6, H1, H2, H4, H5, H7, J6, J1, J3 und PoE. Ausgenommen sind einzelne USB-/RJ45-/SD-Slotkontakte, Modul-Lötpads und Schirm-/Befestigungskontakte. Die Busfunktionen dieser Schnittstellen sind oben dokumentiert. Es wird weder eine vollständige Platinen-Netzliste noch eine am Exemplar durchgemessene Pinbelegung behauptet.
