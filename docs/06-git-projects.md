# Git-Projekte und Anwendungsbeispiele

Stand: 30.10.2026. Die folgenden sieben Originalrepositories wurden gelesen beziehungsweise über ihre Metadaten abgeglichen. Commitstände sind in [repositories.json](../sources/repositories.json) festgehalten. Eine Verlinkung ist kein Kompatibilitäts- oder Abnahmetest.

| Projekt / geprüfter Stand | Zweck | Grenze |
| --- | --- | --- |
| [waveshareteam/ESP32-P4-Platform](https://github.com/waveshareteam/ESP32-P4-Platform/tree/6f78fa810ec505048c1941e3d09cefc9f29129bd) · `6f78fa81` | Herstellerbeispiele und Board-/Revisionskonfiguration; Basistests, Ethernet, SD, Audio, MIPI und UI. | Nur passend konfigurierte Beispiele verwenden; einzelne Defaults setzen 16 MB Flash. |
| [espressif/esp-idf](https://github.com/espressif/esp-idf/tree/735507283d5b2f9fb363a1901172dbd9e847945d) · `73550728` | SDK des vorhandenen Prüfstands; Ethernet-, Speicher- und Gerätetreiber. | v5.5.4 ist der hier belegte Prüfstand, keine Aussage über die neueste Version. |
| [espressif/esp-hosted](https://github.com/espressif/esp-hosted/tree/a0422923d01fa5cd5f4987885fe743656398b7c5) · `a0422923` | Übersichtsrepository der Hosted-Familie. | Aktive MCU-Implementierung inzwischen in esp-hosted-mcu; Lizenzdateien der verwendeten Teile prüfen. |
| [espressif/esp-hosted-mcu](https://github.com/espressif/esp-hosted-mcu/tree/78b1c1c43c02b0c4e898cf87f94679278b1ddaff) · `78b1c1c4` | Funkanbindung eines MCU-Hosts über einen Espressif-Coprozessor. | Host und C6 müssen zueinander passen; eigene Funkprüfung fehlt. Lizenzdateien der konkreten Komponenten prüfen. |
| [espkvm/espkvm](https://github.com/espkvm/espkvm/tree/39273c3db6fc2d02dacf596d635938c666af836c) · `39273c3d` | IP-KVM-Anwendungsbeispiel; vom Hersteller für dieses Board verlinkt. | Zusätzliche HDMI-CSI-Hardware; revisionsgerechter Build und eigene elektrische Prüfung erforderlich. Hier nicht installiert. |
| [jrowny/p4kvm](https://github.com/jrowny/p4kvm/tree/18e0b85735d9569d4264fe4d5b58f6659c148680) · `18e0b857` | Früher Ethernet-KVM-Prototyp mit TC358743 für P4 vor Revision 3. | README nennt fehlenden Schutz und POC-Status; hier keine Betriebsfreigabe. Lizenzdateien vor Übernahme prüfen. |
| [Mcgee1704/esp32-p4-llm-cluster-research](https://github.com/Mcgee1704/esp32-p4-llm-cluster-research/tree/0675f8687b9459fafa4545587ef14aedd118187d) · `0675f868` | Eigene veröffentlichte Experimente zu P4-Speicher, Ethernet und verteilter Textinferenz. | Funktionsnachweis für den dokumentierten Aufbau; keine komplette Boardabnahme. Gemischte Herkunft: LICENSE und THIRD_PARTY beachten. |

## Auswahl für Folgeprojekte

Für die erste Peripherieprüfung bieten sich die Herstellerbeispiele an; das Boardprofil und die Siliziumrevision müssen zuvor feststehen. Der vorhandene eigene P4-Prüfstand belegt IDF 5.5.4, 32 MiB Flash, 32 MiB PSRAM und den IP101-Ethernetpfad. Die Funkerweiterung ist ein eigenes Paket mit passender C6-Firmware. KVM, Kamera, Display und Audio benötigen jeweils zusätzliche Prüfungen.

Die Waveshare-Dokumentation ordnet die Beispiele nach Basistest, Schnittstelle und Anwendung. In diesem Repository werden keine fremden Beispiele oder Binärimages kopiert. Die offiziellen [Ressourcen](https://docs.waveshare.com/ESP32-P4-WIFI6-POE-ETH/Resources-And-Documents) und [ESP-IDF-Hinweise](https://docs.waveshare.com/ESP32-P4-WIFI6-POE-ETH/ESP-IDF) sind der Einstieg.

## Lizenzen und Nachweisgrenzen

Die GitHub-Lizenzkennung `NOASSERTION` bedeutet, dass die API keine eindeutige SPDX-Gesamtlizenz ausweist. Sie bedeutet weder gemeinfrei noch automatisch unlizenziert. Vor Codeübernahme die konkreten LICENSE-Dateien, Dateiköpfe, Unterkomponenten und Drittanbieterhinweise prüfen. Das Forschungsrepository enthält mehrere Herkunfts- und Lizenzbereiche.

Keines dieser Projekte wurde im Rahmen der Katalogaufnahme installiert, gebaut, geflasht oder im Netzwerk bereitgestellt. Historische eigene Funktionsnachweise stehen unter [Eigene Boards](05-own-boards.md).
