# Smart Server-Guard
**LF7 Projektarbeit | Fach: Cyber-physische Systeme (CPS)** **Heinrich-Hertz-Schule Karlsruhe**

![Status](https://img.shields.io/badge/Status-Autonom-green) 
![Hardware](https://img.shields.io/badge/Hardware-ESP8266-blue)
![Firmware](https://img.shields.io/badge/Firmware-Tasmota-orange)

## Projektübersicht
Der **Smart Server-Guard** ist ein autonomes Überwachungssystem für Serverschränke. Das System arbeitet nach dem **Edge-Computing-Prinzip**: Daten werden lokal erfasst, verarbeitet und visualisiert, ohne auf eine externe Cloud-Anbindung angewiesen zu sein. 

Ziel ist die Kontrolle von Temperatur und unbefugtem Zugriff (Bewegung) sowie die automatische Steuerung eines Kühlsystems.

### Kernfunktionen
* **FA-01: Temperaturmanagement:** DS18B20 misst alle 30 Sek. das Klima. Das Relay schaltet den Lüfter bei >30°C EIN und bei <28°C AUS.
* **FA-02: Sicherheit:** Ein PIR-Sensor erkennt Bewegungen. Die LED-Matrix (TM1640) signalisiert Warnungen (Ausrufezeichen) und das Dashboard zeigt einen Alarmstatus.
* **FA-03: Lokales Dashboard:** Visualisierung der Echtzeitdaten (Temperatur, Lüfterstatus, Bewegung) über ein Web-Interface.

---

## Hardware & Architektur
Das Projekt basiert auf der **Wemos D1 Mini (ESP8266)** Plattform und nutzt diverse Shields zur Datenerfassung.

| Komponente | Funktion |
| :--- | :--- |
| **Wemos D1 Mini** | Zentraler Mikrocontroller (ESP8266) |
| **DS18B20 Shield** | Temperaturmessung |
| **PIR Shield** | Bewegungserkennung |
| **Relay Modul** | Steuerung des 5V Lüfters |
| **TM1640 8x8 Matrix** | Lokale optische Statusanzeige |
| **Raspberry Pi** | Zentraler MQTT-Broker & Node-Red Instanz |

---

## Software-Stack
* **Firmware:** Tasmota (Spezial-Build für TM1640 Unterstützung)
* **Kommunikation:** MQTT-Protokoll (Broker: Mosquitto auf Raspberry Pi)
* **Logik & Steuerung:** Node-Red
* **Datenhaltung:** InfluxDB (Persistente Speicherung der Messwerte)
* **Visualisierung:** Grafana & Node-Red Dashboard

---

## Troubleshooting & Log (System Boot Log)
Während der Entwicklung wurden folgende Herausforderungen gelöst:
* **LED-Matrix:** Standard-Tasmota unterstützt TM1640 nicht -> Wechsel auf `tasmota-display.bin`. [ERFOLGREICH]
* **Relay-Steuerung:** Korrektur der Spannungsversorgung auf den 5V-Pin. [ERFOLGREICH]
* **Sensorfehler (-127°C):** D2-Pin korrekt als `DS18x20` zugewiesen. [ERFOLGREICH]
* **Netzwerk:** Instabilitäten durch Vergabe einer statischen IP behoben. [ERFOLGREICH]

---

## Projektteam
* **Samuel Klassen:** Dokumentation, Pflichtenheft, Präsentation
* **Nico Renner:** Node-Red Konfiguration
* **Yannik Dressler:** Projektteam / Hardware-Setup
* **Sven Kolpack:** Projektteam / Testläufe

---
**Betreuende Lehrkraft:** Frau Perez  
**Stand:** 07.05.2026
