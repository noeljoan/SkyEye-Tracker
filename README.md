# 🌌 SkyEye-Tracker
> **KI-gestütztes Edge-AI System zur autonomen Luftraumüberwachung und visuellen Objektnachführung.**

[![License: MIT](LICENSE)
[![Platform: Raspberry Pi 5](https://shields.io)](https://raspberrypi.com)
[![Framework: YOLOv8](https://shields.io)](https://github.com)

SkyEye-Tracker ist ein ziviles, mechatronisches Open-Source-Forschungsprojekt. Es demonstriert, wie günstige Edge-Hardware (Raspberry Pi 5 & Arduino) kombiniert mit modernen neuronalen Netzen genutzt werden kann, um Flugobjekte (wie Drohnen oder Vögel) autonom im Luftraum zu detektieren, via Kamera zu verfolgen und zeitgleich meteorologische Echtzeitdaten sowie präzise Laser-Abstandsdaten zu erfassen.

---

## 🛰️ System-Architektur & Sensor-Fusion

Das System teilt sich die Rechenlast intelligent auf zwei Hardware-Ebenen auf:

[ Infrarot-Kamera ] ➔ [ Raspberry Pi 5 (YOLOv8 KI) ] ➔ Berechnung Achsenfehler (X/Y)⬇ (Serielle USB-Daten)
[ Zaweliyo Wind-S.] ➔ [ Arduino Nano Every ] ➔ Mechanische Pan-Tilt-Servos (0-180°)[ TOFFUTURE LiDAR ] ➔

1. **Edge AI Core (Raspberry Pi 5):** Verarbeitet das Videosignal der Infrarot-Kamera, führt ein performantes YOLOv8-Modell im optimierten ONNX-Format aus, zeichnet das Heads-Up-Display (HUD) und berechnet die mathematische Winkelkorrektur.
2. **Hardware I/O Core (Arduino Nano Every):** Steuert in Millisekunden die Schwenk-Neige-Servos an und liest zeitgleich die analoge Windgeschwindigkeit sowie die digitale Laser-Entfernung (LiDAR) aus.

---

## 🛠️ Hardware-Komponenten & Budget (Bill of Materials)

Das gesamte System ist so optimiert, dass es vollständig mit **5V Spannung** betrieben werden kann und somit zu 100% mobil über eine handelsübliche Powerbank läuft.

| Komponente | Spezifikation / Modell | Zweck | Budget (ca.) |
| :--- | :--- | :--- | :--- |
| **SBC** | Raspberry Pi 5 (4GB RAM) | KI-Zentrale & Bildverarbeitung | 75,00 € |
| **MCU** | Arduino Nano Every (Pins montiert) | Sensor-Schnittstelle & Servomotorik | 15,00 € |
| **Kamera** | V BESTLIFE Infrarot-Kameramodul | Nachtflugtaugliches optisches Auge | 17,00 € |
| **Display** | Waveshare 3.5" HDMI Touchscreen | Mobiles Echtzeit-Fadenkreuz (HUD) | 40,00 € |
| **LiDAR** | TOFFUTURE XT-S1e Solid-State | 100 Hz Laser-Entfernungsmesser | 35,00 € |
| **Wind** | Zaweliyo Schalen-Anemometer | Messung der meteorologischen Abdrift | 20,00 € |
| **Aktuator** | 2x TowerPro SG90 Micro Servo | 2-Achsen Schwenk-Neige-Nachführung | 8,00 € |
| **Akku** | USB-C Powerbank (PD 25W+) | Mobile Gesamt-Stromversorgung | 30,00 € |

---

## 📁 Repository-Struktur

```text
SkyEye-Tracker/
│
├── .gitignore                 # Blockiert Systemdaten und große KI-Modelle
├── LICENSE                    # Rechtlich sichere MIT-Lizenz
├── README.md                  # System-Dokumentation
│
├── raspberry_pi/              # Software für das Edge-AI-System
│   ├── hud.py                 # Hauptprogramm (KI-Tracking & HUD-Anzeige)
│   └── export.py              # Skript zur ONNX-Modell-Optimierung
│
└── arduino_telemetry/         # Firmware für den Mikrocontroller
    └── arduino_telemetry.ino  # Servo-Steuerung, LiDAR- & Wind-Auswertung
```

---

## 🚀 Schnellstart-Anleitung

### 1. Vorbereitung des Raspberry Pi 5
Flashen Sie das offizielle **Raspberry Pi OS (64-bit) mit Desktop** via Raspberry Pi Imager. Aktivieren Sie SSH, WiFi und die **I2C-Schnittstelle** in den Voreinstellungen.

Öffnen Sie das Terminal auf dem Pi und installieren Sie alle Abhängigkeiten mit einem Befehl:
```bash
sudo apt update && sudo apt install -y python3-opencv python3-numpy python3-serial && pip3 install ultralytics --break-system-packages
```

### 2. Modell-Optimierung für maximale FPS
Führen Sie im `raspberry_pi/` Ordner das Export-Skript aus, um das YOLO-Modell auf die Prozessorarchitektur des Pi 5 anzupassen:
```bash
python3 export.py
```
*Dadurch entsteht die ultraschnelle Datei `yolov8n.onnx`.*

### 3. Firmware auf den Arduino flashen
1. Öffnen Sie die **Arduino IDE**.
2. Installieren Sie im Board-Verwalter das Paket **"Arduino megaAVR Boards"**.
3. Wählen Sie den **Arduino Nano Every** aus (Registers Emulation auf "None").
4. Laden Sie das Skript `arduino_telemetry.ino` auf das Board.

---

## ⚠️ Disclaimer / Rechtlicher Hinweis

Dieses Projekt ist eine reine Software- und Elektronik-Demonstration zur zivilen, optischen Objektnachführung (Kamera-Tracking), Wildtierbeobachtung und Luftraumforschung. Es enthält keinerlei Schnittstellen, Steuerungen oder Funktionen für mechanische Einwirkungen, Projektile, Waffen oder aktive Signalstörungen (Jamming). Die Nutzung des Codes erfolgt ausschließlich im Rahmen der gesetzlichen Bestimmungen für zivile Bildverarbeitung und Sensorik. Autoren und Mitwirkende übernehmen keine Haftung für Missbrauch.
