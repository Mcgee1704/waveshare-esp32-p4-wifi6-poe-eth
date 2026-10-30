# Programmierung und Projektprofil

Stand: 30.10.2026. Dies ist eine Referenz; während dieser Boardaufnahme wurde keine Firmware installiert oder verändert.

## USB und Boot

USB-C dient dem P4-UART über CH343P. P4-TX GPIO37 und P4-RX GPIO38 werden auch an H2/P6 herausgeführt. Externe Teilnehmer dürfen den USB-UART nicht gleichzeitig gegeneinander treiben. USB-A gehört zum nativen HS-OTG-Port; die beiden Schnittstellen sind nicht austauschbar.

BOOT liegt im Schaltplan an **GPIO35**, RESET an `ESP_EN`. Der Hersteller beschreibt: BOOT beim Einschalten beziehungsweise Reset gedrückt halten, um den Downloadmodus zu erreichen. Anders als bei zahlreichen anderen ESP32-Boards ist hier nicht GPIO0 der BOOT-Taster. DTR/RTS des CH343 steuern über U6 den automatischen Einstieg.

GPIO35–38 beeinflussen den Bootmodus; GPIO34 die JTAG-Quelle. GPIO35 ist zudem Ethernet-TXD1. Daher BOOT nicht während laufendem Ethernet als freien Anwendungstaster verwenden. Externe Lasten auf GPIO36–38 müssen die Bootbedingungen einhalten. Quellen: [Chipdatenblatt, Kapitel 3](https://documentation.espressif.com/esp32-p4_datasheet_en.pdf), WS-SCHEMATIC.

## Revisionsgerechtes Bauen

Für beide vorhandenen Chips wurde **Revision 1.3** dokumentiert. ESP-IDF **5.5.4** und ein Rev-1.x-Profil sind in den bisherigen Inbetriebnahmen belegt. Ein Build für 3.x wurde separat gebaut, aber nicht auf einem physischen 3.x-Board geprüft. P4-Revision und Platinenrevision sind getrennte Angaben.

Waveshare führt inzwischen eigene Konfigurationsdateien für vor-v3, v3.0 und v3.1. Bei einer Meldung über eine unpassende Chiprevision das passende Profil neu bauen; `--force` ist keine Reparatur. Bestehende `sdkconfig`-Werte können neue Defaults übersteuern. Die genaue Anleitung steht im [ESP-IDF-Kapitel des Herstellers](https://docs.waveshare.com/ESP32-P4-WIFI6-POE-ETH/ESP-IDF).

Vorhandenes, lokal erfolgreich verwendetes Profil (keine vollständige Firmware):

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

Diese Namen beziehen sich auf das vorhandene IDF-5.5.4-Profil. Die Portierung auf andere IDF-Versionen benötigt einen neuen Konfigurationsabgleich. Insbesondere enthalten manche allgemeinen Waveshare-Beispiele 16-MB-Flashdefaults; daraus folgt nicht, dass dieses Board nur 16 MB hat. Partitionstabelle und Flashgröße zusammen prüfen.

## Ethernet

| Parameter | Zuordnung |
| --- | --- |
| MAC / PHY | Interner P4-EMAC / IP101GRI |
| Management | MDC GPIO31, MDIO GPIO52 |
| PHY-Reset | GPIO51 |
| RMII-Referenztakt | GPIO50, externer Eingang vom PHY |
| Senden | TX_EN 49, TXD0 34, TXD1 35 |
| Empfangen | CRS_DV 28, RXD0 29, RXD1 30 |
| PHY-Adresse | Bisherige Firmware verwendet automatische Erkennung (`-1`); keine ungeprüfte Adresse 0 oder 1 festschreiben |

In ESP-IDF Takt, Datenpins, Managementpins und PHY-Typ konsistent konfigurieren. Link-Up allein belegt noch keine IP-Kommunikation; die vorhandenen Tests umfassen DHCP und Anwendungsverkehr. [Espressif-Ethernetreferenz](https://docs.espressif.com/projects/esp-idf/en/v5.5.4/esp32p4/api-reference/network/esp_eth.html).

## C6, SD und Audio

WLAN/BLE erfordert passende Host- und C6-Firmware. Der aktuelle Einstieg für MCU-Hosts ist [ESP-Hosted-MCU](https://github.com/espressif/esp-hosted-mcu); `esp-hosted` ist inzwischen ein Wegweiser zu den getrennten Implementierungen. Vorhandene C6-Firmware ist hier unbekannt und wurde nicht ersetzt. Allgemeine Fähigkeiten eines C6 belegen keine in dieser Firmware freigeschaltete Thread-/Zigbee-Funktion.

SDMMC verwendet CMD44, CLK43 und D0–D3 39/40/41/42. GPIO45 steuert Q1 der Kartenversorgung; die Ansteuerung und Betriebsspannung mit der Boardimplementierung abgleichen. Eine automatische Formatierungsoption kann vorhandene Kartendaten löschen.

ES8311 nutzt I2C7/8 und I2S: MCLK13, BCLK12, LRCK10, Codec-ASDOUT11, Codec-DSDIN9. GPIO53 steuert den Verstärker. SDA/SCL sind mit Erweiterung und MIPI-Steueranschlüssen geteilt; Busadressen, Pull-ups und gemeinsame Initialisierung im konkreten Projekt abstimmen.

## Projektprofil für Folgearbeiten

Vor einer Installation festhalten: Modell/Platinenrevision, Chiprevision, C6-Modul, Versorgung, angeschlossene Peripherie, Pinbelegung, IDF-/Komponentenstände, Flashgröße, Partitionen, erwartete Bootausgabe und messbare Abnahmekriterien. Vorhandenen Flashzustand sichern und Rückweg prüfen. Geheimnisse gehören in lokale, ausgeschlossene Konfigurationen. Sicherheits-eFuses sind dauerhaft; sie sind kein Bestandteil einer normalen Boarderfassung.

Dieses Repository liefert keine fertigen Firmwareimages, keine Flashautomatik und keine Freigabe für automatische Nachbarinstallation. Geeignete Ausgangsprojekte stehen im [Projektregister](06-git-projects.md).
