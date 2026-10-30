# Versorgung und elektrische Grenzen

Stand: 30.10.2026. Grundlage: [Schaltplan](https://files.waveshare.com/wiki/ESP32-P4-WIFI6-POE-ETH/ESP32-P4-WIFI6-POE-ETH-Schematic.pdf), [aktuelle Hersteller-FAQ](https://docs.waveshare.com/ESP32-P4-WIFI6-POE-ETH/FAQ) und vorhandene lokale Untersuchung. Die folgende Zuordnung ist eine Schaltplanauswertung; die Bestückung der eigenen Boards wurde noch nicht vollständig abgeglichen.

## Versorgungspfade

| Pfad | Schaltplanbefund | Grenze |
| --- | --- | --- |
| USB-C | `Type_C_5V` über Q2 AO3401 und Ansteuerung U13 MMDT3906DW nach `VCC_5V` | Gesteuerter Pfad; kein gemessener Nachweis aller Rückstromfälle |
| USB-A | `VCC_5V` über U2 DIO7003HEST5 nach `VBUS_OUT`; R12 parallel als NC/0R eingezeichnet | Tatsächliche R12-Bestückung und Ausgangsstromgrenze offen |
| PoE | RJ45-Mittelabgriffe / Versorgungspaare über BD1/BD2 zum separaten Modul, dessen Ausgang `VCC_5V` speist | Norm, Eingangsspannungsbereich, Leistung, Isolation und Modulrevision nicht aus diesem Basisplan vollständig belegt |
| 3,3 V | U3 MP1658GTF-Z, Planbeschriftung „3A MAX“ | Kein 3-A-Budget für USB-A oder den Erweiterungsheader |
| P4-Kern | U4 MP1605GTF-Z und P4-interne Versorgungsregler | Nicht mit frei belastbaren Erweiterungsausgängen verwechseln |
| Audio | U9 RT9193-33PB erzeugt A3V3 | Kein allgemeiner Peripherie-Stromausgang |
| J6 | Pin 1 GND, Pin 2 VCC_5V | Hersteller bezeichnet den Anschluss als 5-V-Versorgung; Polarität und Einspeisekombination vorher prüfen |

Eine passive PoE-Spannung oder ein beliebiges PoE-Modul wird damit nicht freigegeben. Der Basisschaltplan zeigt keine vollständige interne PoE-Wandlerschaltung. Auch eine Schutzklasse oder zertifizierte Isolationsspannung wird hier nicht behauptet.

## USB-C und PoE gleichzeitig

Die am 30.10.2026 abgerufene Hersteller-FAQ beantwortet die gleichzeitige Versorgung über **USB Type-C und PoE positiv**. Diese Aussage wird als Herstellerangabe aufgenommen. Sie ist kein eigener Belastungs- oder Rückstromtest und sagt nichts Konkretes über eine Kette mehrerer Boards aus.

Die vorhandenen eigenen Funktionstests verwendeten USB-C vom Rechner sowie LAN ohne PoE. Eine vorgesehene Verbindung USB-A von Board A zu USB-C von Board B wurde elektrisch noch nicht abgenommen. Das Weiterlaufen eines Boards über USB bei abgeschaltetem PoE ist dabei erwartbares und akzeptiertes Verhalten. Zum vollständigen Abschalten müssen alle versorgenden Verbindungen getrennt sein.

Offen sind insbesondere Stromrichtung, maximale USB-A-Last, Lastaufteilung, Spannungsabfälle, Erwärmung und Verhalten beim Wegfall einzelner Quellen. LED-Licht oder ein erfolgreicher Boot reichen dafür nicht als Messnachweis.

## H5 und Logikpegel

H5 führt laut Plan Pin 1 = `ESP_3V3`, Pin 2 = `OUT_LE`, Pin 3 = `VCC_5V`. `OUT_LE` liegt jeweils an Pin 1 von H1 und H2. Die tatsächliche Brücke/Bestückung ist nicht erfasst. Deshalb die Ausgangsspannung vor dem Anschluss eines Sensors oder UART-Adapters feststellen; nicht aus Steckerform oder Kabelfarbe ableiten.

Die Auswahl der Versorgungsleitung verändert **nicht** die Logikpegel von GPIO7/8 oder GPIO37/38. Diese sind im Board als 3,3-V-Signale ausgeführt. Keine 5-V-Signale an GPIOs anlegen. Pegelwandler und gemeinsame Masse bei Bedarf passend vorsehen; Rückspeisung über Signalleitungen bei ausgeschaltetem Board vermeiden.

GPIO0/1 liegen außerdem am 32-kHz-Quarzpfad; GPIO36/37/38 gehören zu den Boot-Strapping-Signalen des P4. Die [GPIO-Konflikte](02-pinout.md) vor einer Zusatzbeschaltung prüfen.

## Lautsprecher und MIPI

H4 führt zwei Verstärkerausgänge `PA_OUTL-` und `PA_OUTL+`. Keiner ist ein Masseanschluss. Den Lautsprecher zwischen den beiden vorgesehenen Ausgängen anschließen; keinen Ausgang mit GND kurzschließen. Die Herstellerangabe 8 Ω / 2 W ist kein gemessener Ausgangsleistungsnachweis dieser Erfassung.

MIPI-Stecker sind keine universellen GPIO-Stecker. Kontaktseite, Lane-Belegung, Versorgung und Display-/Kameramodell müssen zusammenpassen. Verbindungen im stromlosen Zustand herstellen.

## Abnahmestand für eine spätere Versorgungskette

Erst Bestückung und Daten des tatsächlich eingesetzten PoE-Moduls erfassen. Danach pro Versorgungskombination Spannung, gerichteten Strom und Temperatur messen: einzelne Quelle, beide Quellen, ausgeschalteter Nachbar, vertauschte Boardrollen und realistische Last. Vorher zulässige Grenzwerte festlegen. Ein bestandener Zweieraufbau belegt keine größere Kette. Für diese Dokumentation wurde kein solcher Test ausgeführt.
