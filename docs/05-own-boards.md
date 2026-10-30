# Eigene Boards: Nachweise und Grenzen

Zusammengeführt am 30.10.2026 aus vorhandenen Inbetriebnahme- und Forschungsunterlagen. **Für diese Katalogaufnahme fand kein neuer Zugriff auf die Geräte statt.** Die Angaben sind dokumentierte frühere Befunde, keine Live-Abfrage des heutigen Zustands. Beide Exemplare werden nur als Board 1 und Board 2 bezeichnet.

| Merkmal | Board 1 | Board 2 | Aussagekraft |
| --- | --- | --- | --- |
| Vom Besitzer zugeordnetes Modell | ESP32-P4-WIFI6-POE-ETH | ESP32-P4-WIFI6-POE-ETH | Exakte Platinenrevision noch ohne Sichtnachweis |
| Chiprevision | P4 v1.3 | P4 v1.3 | Auslesung vom 29.10.2026 |
| Flash | 32 MiB | 32 MiB | Ausgelesen und vor Installation vollständig lokal gesichert |
| PSRAM | 32 MiB | 32 MiB | Erkennung und erfolgreicher SPI-SRAM-Starttest |
| CPU-/PSRAM-Konfiguration | 360 / 200 MHz | 360 / 200 MHz | Firmwarekonfiguration, keine externe Taktmessung |
| SDK der Inbetriebnahme | ESP-IDF 5.5.4 | ESP-IDF 5.5.4 | Rev-1.x-Firmware gestartet |
| Versorgung der Versuche | USB-C vom Rechner | USB-C vom Rechner | Ethernet jeweils ohne PoE |
| Ethernet | DHCP und Anwendungskommunikation | DHCP und Anwendungskommunikation | Erfolgreiche Solo- und Zweierläufe dokumentiert |
| C6-Funk | Nicht benutzt | Nicht benutzt | WLAN/BLE damit ungetestet |
| Flashzustand | Original privat gesichert | Original privat gesichert | Wiederherstellung nicht praktisch abgenommen |
| Secure Boot / Flashverschlüsselung | Bei Inbetriebnahme deaktiviert | Bei Inbetriebnahme deaktiviert | Keine eFuse-Änderung in den dokumentierten Arbeiten |

## Was die bisherigen Versuche bestätigen

Die Boards starteten die eigene Firmware, initialisierten PSRAM und Ethernet, nahmen ein Modellpaket im Flash auf und führten lokale Textgenerierung aus. Nach Neustart wurde das Modell wieder geladen. Spätere normale LAN-Firmwareupdates und Modellupdates sind dokumentiert. Diese Ergebnisse belegen einen nutzbaren P4-/Speicher-/Ethernet-Pfad im beschriebenen Aufbau.

Ausgewählte bereits veröffentlichte Forschungsnachweise stehen im [Cluster-Repository, geprüfter Stand 0675f868](https://github.com/Mcgee1704/esp32-p4-llm-cluster-research/tree/0675f8687b9459fafa4545587ef14aedd118187d). Der Katalog übernimmt keine laufende Modell- oder Firmwareversionsverwaltung; deren aktuelle Version muss bei einer Folgearbeit am jeweiligen Gerät neu festgestellt werden.

## Nicht bestätigt

- Platinenrevision, schwarze/farbige Headerausführung und physische Pin-1-Zuordnung.
- Exakter P4-Flashbaustein, C6-Modul, C6-Firmware und Antennenbestückung.
- PoE-Modultyp, R12-Bestückung, H5-Stellung, Strombudgets und elektrische PoE-/USB-Kettenabnahme.
- WLAN, BLE, SD-Karte, USB-OTG-Anwendungsbetrieb, Audio, MIPI-Display und Kamera.
- Vollständige Prüfung aller 28 Erweiterungs-GPIOs, Langzeitlast und Grenztemperaturen.
- Praktische Abnahme einer Originalflash-Wiederherstellung, absichtlich unterbrochener OTA-Vorgänge und aller Rollbackfälle.
- Automatisches Flashen fabrikneuer Nachbarboards und reale Hardwaretests mit P4-Revision 3.x.

Die vollständigen lokalen Nachweise enthalten gerätebezogene Daten und bleiben privat. Diese Zusammenfassung veröffentlicht keine MAC-Adressen, Seriennummern, lokalen Netzadressen, Zugangsdaten, Flashabbilder oder Rohprotokolle. Die Aufnahme eines Boards verlangt keine zusätzlichen Peripherietests; fehlende Tests werden als offen geführt.
