# APCDS — Ad-hoc Passive Crowd Detection and Safety System

A tri-modal, real-time crowd monitoring system that fuses **RF sensing**, **computer vision**, and **acoustic analysis** to detect crowd density, movement patterns, and early signs of panic or unsafe crowd behavior — without relying on any single point of failure.

## Overview

Most crowd-monitoring systems rely on a single sensing modality (usually cameras alone), which struggles in low-visibility conditions, occluded views, or when privacy constraints limit camera coverage. **APCDS** addresses this by combining three independent, complementary sensing streams into a single fused risk assessment:

- 📡 **RF Sensing** — passive Wi-Fi/Bluetooth scanning for device-free crowd presence estimation
- 🎥 **Computer Vision** — real-time human detection, counting, and movement tracking
- 🔊 **Acoustic Analysis** — crowd sound classification to detect panic, cheering, or agitation

By fusing these signals, APCDS can flag abnormal crowd conditions even when one modality alone would miss it — e.g., detecting rising RF device density and a spike in acoustic agitation *before* a camera feed shows visible overcrowding.

## Features

- **Passive RF crowd estimation** via ESP32 edge nodes scanning Wi-Fi probe requests and BLE advertisements (RSSI, hashed device ID, timestamp) — no user participation or app required
- **YOLOv8-based real-time person detection and tracking**, including per-person trajectory tracking, flow speed/direction analysis, and crowd growth rate over time
- **Real-time acoustic feature extraction** (RMS energy, spectral centroid, zero-crossing rate, MFCCs) feeding a classifier trained to distinguish normal chatter, cheering, and panic/agitation
- **Multi-modal sensor fusion** combining all three signal streams into a unified crowd risk score
- Designed for **beginner-accessible deployment** using widely available, low-cost hardware

## Tech Stack

| Component | Technology |
|---|---|
| RF Sensing | ESP32 (promiscuous Wi-Fi + BLE scanning) |
| Computer Vision | YOLOv8 (Ultralytics), OpenCV |
| Acoustic Analysis | Librosa, scikit-learn |
| Communication | MQTT (device-to-fusion-engine messaging) |
| Fusion Engine | Python |

## System Architecture

```
┌─────────────┐     ┌──────────────┐     ┌───────────────┐
│  RF Sensing │     │Computer Vision│     │Acoustic Analysis│
│  (ESP32)    │     │ (YOLOv8+CV)  │     │  (Librosa)     │
└──────┬──────┘     └──────┬───────┘     └───────┬───────┘
       │                   │                     │
       └───────────────────┼─────────────────────┘
                            │  MQTT
                            ▼
                  ┌───────────────────┐
                  │   Fusion Engine    │
                  │ (risk score + alert)│
                  └───────────────────┘
```

## Project Status

🚧 **In active development** — this is a final-year academic project. Individual modules (RF, CV, acoustic) are being built and validated independently before integration into the full fusion pipeline.

## Getting Started

### Prerequisites
- Python 3.11
- ESP32 development board(s)
- Webcam (for CV module testing)
- Microphone (for acoustic module testing)

### Installation
```bash
# Clone the repository
git clone <your-repo-url>
cd apcds

# Create and activate a virtual environment
python -m venv venv
venv\Scripts\Activate.ps1   # Windows
source venv/bin/activate     # macOS/Linux

# Install dependencies
python -m pip install -r requirements.txt
```

## Academic Context

This project is developed as a final-year B.Tech Computer Science Engineering project, proposing **tri-modal sensor fusion (RF + CV + Acoustic)** as a novel approach to passive, privacy-conscious crowd safety monitoring.

