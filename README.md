# AI-Based Drone Detection & Optical Tracking System

Dieses Open-Source-Projekt demonstriert eine rein softwarebasierte und zivile Lösung zur optischen Erkennung und Verfolgung von Flugobjekten (wie Drohnen oder Vögeln) am Himmel mittels Computer Vision. 

## 🎯 Projektziel
Das System dient zu Forschungs- und Bildungszwecken im Bereich der künstlichen Intelligenz (Edge AI). Es zeigt, wie man mit kompakter Hardware (Raspberry Pi 5) und leichtgewichtigen neuronalen Netzen (YOLOv8) Objekte in Echtzeit visuell isolieren und deren Koordinaten für ein Kamerasystem (z. B. für automatisierte Filmaufnahmen oder Wildtierbeobachtung) bereitstellen kann.

## 🛠️ System-Architektur
- **Raspberry Pi 5:** Übernimmt die optische KI-Erkennung (YOLOv8 im ONNX-Format) über den Kamera-Videostream und berechnet das visuelle Fadenkreuz (HUD).
- **Arduino Nano:** Simuliert in dieser Basis-Software die Schnittstelle für optionale Umweltsensoren (wie Telemetriedaten oder Windmessung).

## ⚠️ Disclaimer / Rechtlicher Hinweis
Dieses Projekt ist eine reine Software-Demonstration zur visuellen Objektnachführung (Kamera-Tracking). Es enthält keinerlei Schnittstellen, Steuerungen oder Funktionen für mechanische Einwirkungen, Projektile oder Abwehrmechanismen. Die Nutzung des Codes erfolgt ausschließlich im Rahmen der gesetzlichen Bestimmungen für zivile Bildverarbeitung.
