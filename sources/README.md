# Quellenregister

Letzter Abgleich: **30.10.2026**. Originalquellen werden verlinkt; lokale Prüfladungen und Ausschnitte sind kein Bestandteil des veröffentlichten Repositorys. Eigene Texte und Tabellen wurden aus den folgenden Quellen zusammengeführt.

| ID | Quelle | Verwendung / Grenze |
| --- | --- | --- |
| WS-MODEL | [Waveshare Boardübersicht](https://docs.waveshare.com/ESP32-P4-WIFI6-POE-ETH) | Verkaufsvarianten, Schnittstellen und aktuelle Modulbeschreibung; keine Identifikation eigener Bestückung |
| WS-SCHEMATIC | [Schaltplan PDF](https://files.waveshare.com/wiki/ESP32-P4-WIFI6-POE-ETH/ESP32-P4-WIFI6-POE-ETH-Schematic.pdf) | Blatt 1: Netze und Bauteile; PDF hat drei Seiten einschließlich Layoutdarstellungen |
| WS-PINOUT-NEW | [Farbiger Header](https://docs.waveshare.com/assets/images/ESP32-P4-WIFI6-POE-ETH-details-inter-9a44d25075d91a5039181189b5e82867.webp) | Darstellung links 3V3 / rechts 5V; nur Herstellerbild |
| WS-PINOUT-OLD | [Schwarzer Header](https://docs.waveshare.com/assets/images/ESP32-P4-WIFI6-POE-ETH-details-inter-2-bc32d0b522f12d2743cb5eb34544484e.webp) | Darstellung links 5V / rechts 3V3; physische Zuordnung der eigenen Boards offen |
| WS-DIMENSIONS | [Maßzeichnung](https://docs.waveshare.com/assets/images/ESP32-P4-WIFI6-POE-ETH-details-size-3f5fd8ec650821d9a492dd8dce19bfc2.webp) | 55 × 68 mm, Lochmitten 48 × 33 mm; keine eigene Vermessung |
| WS-3D | [Hersteller-3D-Archiv](https://files.waveshare.com/wiki/ESP32-P4-WIFI6-POE-ETH/ESP32-P4-WIFI6-POE-ETH-3D.zip) | Im Ressourcenregister verlinkt; hier nicht heruntergeladen oder auf Passung geprüft |
| WS-RESOURCES | [Ressourcen und Dokumente](https://docs.waveshare.com/ESP32-P4-WIFI6-POE-ETH/Resources-And-Documents) | Offizielle Quellenwege und KVM-Projektverweise |
| WS-IDF | [ESP-IDF-Anleitung](https://docs.waveshare.com/ESP32-P4-WIFI6-POE-ETH/ESP-IDF) | Beispielstruktur und Trennung vor-v3 / v3.0 / v3.1 |
| WS-FAQ | [FAQ](https://docs.waveshare.com/ESP32-P4-WIFI6-POE-ETH/FAQ) | Hersteller erlaubt gleichzeitige USB-C-/PoE-Versorgung; keine USB-Boardkettenabnahme |
| ESP-P4-DS | [ESP32-P4 Series Datasheet](https://documentation.espressif.com/esp32-p4_datasheet_en.pdf) | Abgerufene Version 0.7; Chipfamilie, Speicher und Strapping; nicht pauschal alle Aussagen auf eigenes frühes Silizium übertragen |
| ESP-ETH | [ESP-IDF 5.5.4 Ethernet](https://docs.espressif.com/projects/esp-idf/en/v5.5.4/esp32p4/api-reference/network/esp_eth.html) | RMII-Konfiguration, Takt-/Datenpinrollen und PHY-Treiber |
| OWN-20261029 | [Veröffentlichte Hardware-Zusammenfassung, Commit 0675f868](https://github.com/Mcgee1704/esp32-p4-llm-cluster-research/blob/0675f8687b9459fafa4545587ef14aedd118187d/docs/HARDWARE.md) | Zwei eigene P4s; lokale Inbetriebnahmedokumente vom 29.10.2026 ergänzen Starttest, Auslesung und Flashsicherung; private Rohbelege bleiben lokal |

## Prüfsummen der gelesenen Herstellerdateien

| Datei / Quellen-ID | Bytes | SHA-256 |
| --- | --- | --- |
| Schaltplan / WS-SCHEMATIC | 1734900 | `885b8f038881c6656486fea143bcf749f17c6a1ec9006cc693dcdb298018380b` |
| Farbiger Header / WS-PINOUT-NEW | 41258 | `9b6892a66bfadc64c9c8810d2a2dd3ac20a4ffa68ea4ac8b0dbfe929ee8d7535` |
| Schwarzer Header / WS-PINOUT-OLD | 40278 | `c9b3b932465f56512c98d56e6e3a3fce89a5618a1b5fe9a3e90368522ffdfa25` |
| Maße / WS-DIMENSIONS | 49460 | `985a3d975b7d72f9a7996fe7354b94d661b6cb3f025e5d0072bad3c7e13b9cbb` |

Der am 30.10.2026 neu geladene Schaltplan stimmt bytegenau mit der bereits lokal untersuchten Fassung überein. Blatt 1 wurde als Bild gelesen, die Anschlussbereiche vergrößert geprüft. Ein identischer PDF-Hash belegt keine identische Bestückung verschiedener Lieferchargen.

## Widersprüche und Entscheidung

| Unterschied | Behandlung in dieser Referenz |
| --- | --- |
| Schaltplan C6-MINI-1-N4 gegenüber aktueller C6-MINI-1U-H8-Beschreibung | Beide Angaben mit Quelle führen; eigene Modulvariante unbekannt |
| P4NRW32 im Schaltplan gegenüber P4NRW32X auf der Produktseite | Keine unbestätigte Package-Umbenennung am eigenen Board |
| 360 MHz Boardprofil gegenüber 400 MHz Chipdatenblatt | 360 MHz als dokumentierten Board-/Versuchsstand führen; 400 MHz nur als Chipfamilienangabe |
| Linke/rechte Spalte in alter/neuer Headergrafik | Keine stille Übertragung; Pinliste nach Schaltplansymbol, physische Pin-1-Prüfung erforderlich |
| Positive Hersteller-FAQ zu USB-C plus PoE gegenüber fehlender eigener Messung | Herstellerangabe und eigene Abnahme getrennt; USB-A-Versorgungskette bleibt offen |
| 16-MB-Default in einem allgemeinen Herstellerbeispiel gegenüber 32-MiB-Board | Ausgelesene Boardgröße und vollständige Projektkonfiguration verwenden |

## Git-Quellen

Siehe [Projektregister](../docs/06-git-projects.md) und [maschinenlesbare Commitliste](repositories.json). Die Metadaten wurden über GitHub gelesen; die Einträge sind auf konkrete Commits bezogen. Für Herkunft, Übernahme und Lizenzen gilt [PUBLICATION.md](../PUBLICATION.md).

## Erneute Prüfung

Bei neuer Platinenrevision oder geändertem Herstellerdownload zuerst Hash, Bild und Netze vergleichen. Bei zusätzlichen eigenen Prüfungen Datum, Aufbau, Firmwarestand, beobachtetes Ergebnis und Grenzen dokumentieren. Ein zukünftiger Link oder Branchstand ersetzt keine rückwirkende Bestätigung eines früheren Tests.
