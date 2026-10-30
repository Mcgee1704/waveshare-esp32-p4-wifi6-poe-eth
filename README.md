# Waveshare ESP32-P4-WIFI6-POE-ETH

Technische Referenz zum P4-Board mit Ethernet, PoE-Anbindung und ESP32-C6-Funkcoprozessor. Stand: **30.10.2026**. Die Dokumentation trennt Herstellerangaben, Schaltplanbefunde und bereits vorliegende Prüfungen an zwei eigenen Exemplaren.

| Thema | Dokument |
| --- | --- |
| Modell, Varianten, Speicher, Bauteile, Maße | [Hardware](docs/01-hardware.md) |
| 40-poliger Header, Zusatzanschlüsse, GPIO-Belegung und Konflikte | [Pinbelegung](docs/02-pinout.md) |
| USB-C, USB-A, PoE, Spannungswahl und offene Strombudgets | [Versorgung](docs/03-power.md) |
| USB, Bootmodus, Chiprevision und ESP-IDF-Konfiguration | [Programmierung](docs/04-firmware.md) |
| Nachweise und offene Punkte der beiden eigenen Boards | [Eigene Boards](docs/05-own-boards.md) |
| Herstellerbeispiele, ESP-Hosted, KVM und Cluster-Forschung | [Git-Projekte](docs/06-git-projects.md) |
| Quellen, Prüfsummen und widersprüchliche Angaben | [Quellenregister](sources/README.md) |
| Wiederverwendbare Daten | [Board-JSON](data/board.json), [Anschluss-CSV](data/pinout.csv), [GPIO-Nutzung](data/gpio-usage.csv) |

## Kurzreferenz

- Modellfamilie: ESP32-P4-WIFI6-POE-ETH; Basispaket SKU 32832, Pakete C/D SKU 32833/32834. Das Zubehörpaket der eigenen Exemplare ist nicht belegt.
- Zwei HP-RISC-V-Kerne; für dieses Board dokumentiert und im bisherigen Aufbau konfiguriert: **360 MHz**. Dazu ein LP-Kern bis 40 MHz. Die allgemeinen 400 MHz im aktuellen P4-Chipdatenblatt sind keine Freigabe für die eigenen Rev-1.3-Exemplare.
- **32 MiB Flash und 32 MiB PSRAM** an beiden eigenen P4s dokumentiert; PSRAM-Starttest erfolgreich.
- Ethernet: IP101GRI, RMII; MDC 31, MDIO 52, Reset 51, Referenztakt 50, TX_EN 49, TXD0/1 34/35, CRS_DV 28, RXD0/1 29/30.
- **USB-C führt zum CH343P-UART-Wandler**, USB-A zum nativen P4-USB-HS-OTG. Die Buchsen erfüllen verschiedene Aufgaben.
- I2C: SDA 7, SCL 8. UART0: TX 37, RX 38. SD: CMD 44, CLK 43, D0–D3 39/40/41/42.
- 40-poliger Header mit 28 GPIO-Netzen; MIPI-DSI, MIPI-CSI, Mikrofon, ES8311-Codec und Lautsprecheranschluss vorhanden.

Grundlagen: [Waveshare-Übersicht](https://docs.waveshare.com/ESP32-P4-WIFI6-POE-ETH), [Schaltplan](https://files.waveshare.com/wiki/ESP32-P4-WIFI6-POE-ETH/ESP32-P4-WIFI6-POE-ETH-Schematic.pdf), [eigene Nachweise](docs/05-own-boards.md).

## Vor dem Anschließen

**Die Herstellerbilder der schwarzen und farbigen Header zeigen die Spalten vertauscht.** Die CSV und nummerierte Tabelle beziehen sich ausdrücklich auf P6 im geprüften Schaltplan. Pin 1, Masse und Versorgung am eigenen Exemplar identifizieren; eine Fotoseite oder Headerfarbe ist kein ausreichender Verdrahtungsnachweis.

H1/H2 führen eine über H5 wählbare Versorgung `OUT_LE`; die Signale bleiben 3,3-V-Logik. Die Hersteller-FAQ erlaubt USB-C plus PoE. Eine USB-A-zu-USB-C-Kette mit mehreren Boards hat jedoch kein nachgewiesenes Strombudget. [Einzelheiten](docs/03-power.md).

Die vorhandenen Funktionsergebnisse stammen aus einem Aufbau mit USB-C-Versorgung und Ethernet **ohne PoE**. WLAN/BLE, Audio, Kamera, Display und SD wurden damit nicht abgenommen. Platinenrevision und konkrete C6-Bestückung bleiben offen.

Dieses Repository enthält eigene technische Notizen und Quellenverweise. Es ist keine offizielle Waveshare-Veröffentlichung. Original-PDFs, Herstellerbilder, private Flashsicherungen und rohe Geräteprotokolle werden nicht mitgeführt. [Veröffentlichungsumfang und Rechte](PUBLICATION.md).

[Zurück zum Board-Katalog](https://github.com/Mcgee1704/board-katalog)
