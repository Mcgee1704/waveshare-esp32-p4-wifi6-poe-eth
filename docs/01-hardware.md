# Hardware

Stand: 30.10.2026. Quellenkennungen werden im [Register](../sources/README.md) aufgelöst.

## Identifikation und Revisionen

| Merkmal | Belegter Stand | Quelle |
| --- | --- | --- |
| Hersteller / Modell | Waveshare ESP32-P4-WIFI6-POE-ETH | WS-MODEL |
| Verkaufspakete | Basic 32832, C 32833, D 32834; Zubehör der eigenen Exemplare nicht erfasst | WS-MODEL |
| P4-Modul | ESP32-P4-Core; Schaltplan U7 ESP32-P4NRW32, aktuelle Produktbeschreibung ESP32-P4NRW32X | WS-SCHEMATIC, WS-MODEL |
| Eigene Siliziumrevision | Beide P4s v1.3; nicht mit Platinenrevision gleichsetzen | OWN-20261029 |
| Platinenrevision | Nicht am Exemplar festgestellt | OWN-20261029 |
| C6 im Schaltplan | U1 ESP32-C6-MINI-1-N4 | WS-SCHEMATIC |
| C6 in aktueller Produktbeschreibung | ESP32-C6-MINI-1U-H8, externe Antenne | WS-MODEL |
| Eigener C6 / Antennenweg | Genaue Modulaufschrift und C6-Firmware nicht verifiziert | OWN-20261029 |

N4 und H8 dürfen nicht zu einer vermeintlich einheitlichen Bestückung zusammengeführt werden. Insbesondere werden weder C6-Flashgröße noch Antennenvariante der eigenen Boards aus der aktuellen Verkaufsseite abgeleitet.

## Rechen- und Speicheraufbau

| Baustein / Funktion | Angabe | Nachweisgrenze |
| --- | --- | --- |
| HP-CPU | Zwei 32-Bit-RISC-V-Kerne; 360 MHz im dokumentierten Boardprofil | WS-MODEL, OWN-20261029 |
| LP-CPU | Ein RISC-V-Kern, bis 40 MHz | ESP-P4-DS |
| Interner Speicher | HP-ROM 128 KB, LP-ROM 16 KB, HP-L2MEM 768 KB, LP-SRAM 32 KB, SPM 8 KB | ESP-P4-DS; nicht komplett als freier Anwendungsspeicher verfügbar |
| PSRAM | 32 MiB im P4-Package; bisherige Firmwarekonfiguration 200 MHz | OWN-20261029; Starttest, kein vollständiger Langzeit-Stresstest |
| P4-Flash | 32 MiB SPI-NOR; U12 im Plan GD25Q256EYIGR | Größe ausgelesen, genaue Bauteilaufschrift am Exemplar offen |
| P4-Quarze im Plan | Y1 40 MHz; Y2 32,768 kHz an GPIO0/1 | Schaltplanbestückung, nicht nachgemessen |
| Ethernet-Quarz | Y3 25 MHz am IP101GRI | Schaltplan |

Das aktuelle Chipdatenblatt ESP32-P4 v0.7 nennt bis 400 MHz und PSRAM-Takte bis 250 MHz. Diese Chipfamilienwerte ersetzen keine revisionsgerechte Boardkonfiguration. Die eigenen Messreihen verwenden 360/200 MHz; eine Umstellung wurde für diese Erfassung nicht vorgenommen.

## Schnittstellen und Bauteile

| Bereich | Aufbau laut Quellen |
| --- | --- |
| Ethernet | U11 IP101GRI, RMII, 100-Mbit/s-RJ45 RJ1; kein Gigabit-Ethernet |
| PoE | Zwei Eingangsbrücken BD1/BD2 und separater fünfpoliger PoE-Modulanschluss; Moduldetails siehe [Versorgung](03-power.md) |
| Funk | ESP32-C6 über SDIO; Wi-Fi 6 und Bluetooth LE. Der P4 selbst besitzt kein WLAN-Funkteil |
| USB-C | Versorgung und UART-Download/Debug über U5 CH343P; U6 EMH4T2R steuert Reset/Boot aus DTR/RTS |
| USB-A | Nativer USB 2.0 HS OTG des P4; `USBD_N/P` sind dedizierte Signale |
| SD | MicroSD/TF SD1; Datenbus GPIO39–44, Versorgungsschalter Q1 mit GPIO45 |
| Anzeige | J1, 15 Kontakte, zwei MIPI-DSI-Datenlanes und Taktlane; passende Panelparameter und Strombedarf erforderlich |
| Kamera | J3, 15 Kontakte, zwei MIPI-CSI-Datenlanes und Taktlane; Sensorversorgung und Steuerbus beachten |
| Audio | U10 ES8311, U8 NS4150B, MIC1, H4 mit differenziellem Lautsprecherausgang |
| Lautsprecher | Hersteller nennt 8 Ω / 2 W und MX1.25-Zweipolanschluss; kein Audiofunktionstest am eigenen Board |
| I2C / UART | H1/H2, SH1.0 mit jeweils vier Kontakten; gemeinsame Versorgungsauswahl H5 |
| Erweiterung | P6, 2×20 Kontakte; 28 GPIO-Netze, 4 Versorgungskontakte und 8 Massekontakte |
| Weitere SoC-Funktionen | SPI, I2S, ADC, PWM, RMT, TWAI u. a.; kein CAN- oder RS485-Transceiver in diesem Schaltplan |

Die MIPI- und Beschleunigerfunktionen des P4 erlauben Bildverarbeitung, ihre praktische Nutzbarkeit hängt von Chiprevision, Treiber, Sensor und Display ab. Ein erfolgreicher LAN-Test belegt weder Kamera noch H.264.

## Mechanik

Die aktuelle Herstellermaßzeichnung nennt **55 × 68 mm**, Lochmittenabstände **48 × 33 mm**. USB- und RJ45-Überstände, Einbauhöhe, Lochdurchmesser, Header-Raster und Gehäusefreiräume sind hier nicht am eigenen Board vermessen. Für ein Gehäuse die originale [3D-Datei](https://files.waveshare.com/wiki/ESP32-P4-WIFI6-POE-ETH/ESP32-P4-WIFI6-POE-ETH-3D.zip) und das tatsächliche Exemplar abgleichen. Maße ersetzen keine Passprobe.

## Noch zu erfassen

Platinenaufdruck, Headerausführung, P4-/C6-Modulaufschrift, PoE-Modul, R12-Bestückung, H5-Stellung, Antenne, eingebautes Zubehör und zulässige Strombudgets. Unbekannt bleibt unbekannt; die [Boarddaten](../data/board.json) verwenden dafür `null`.
