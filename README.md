# 🌾 Krushak Hithaishi (ಕೃಷಕ ಹಿತೈಷಿ)
### *AI-Powered Multimodal Crop Disease Diagnosis & Farmer Advisory Ecosystem*

[![FastAPI](https://img.shields.io/badge/Backend-FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![TensorFlow Lite](https://img.shields.io/badge/ML-TensorFlow_Lite-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white)](https://www.tensorflow.org/lite)
[![React Native](https://img.shields.io/badge/Mobile-React_Native_/_Expo-61DAFB?style=for-the-badge&logo=react&logoColor=black)](https://reactnative.dev/)
[![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

---

## 📌 Overview

**Krushak Hithaishi** is an end-to-end smart agriculture platform engineered to bridge the gap between advanced computer vision diagnostics and actionable agronomic assistance for Indian farmers. 

The system combines **lightweight on-device edge AI (MobileNetV3 + TFLite)** with **real-time micro-climate weather telemetry** to deliver accurate disease identification, visual explainability heatmaps (Grad-CAM), regional multilingual voice advisories, and geo-located agricultural retailer lookup.

```
                  ┌────────────────────────────────────────┐
                  │          React Native Mobile App       │
                  │   (Camera + GPS + Regional TTS Player) │
                  └───────────────────┬────────────────────┘
                                      │  Multipart HTTP/REST
                                      ▼
                  ┌────────────────────────────────────────┐
                  │            FastAPI REST Server         │
                  └─────────┬───────────────────┬──────────┘
                            │                   │
            ┌───────────────▼────────┐  ┌───────▼─────────────────┐
            │   TFLite Multimodal    │  │  Live Weather Telemetry │
            │      Fusion Model      │  │      (Open-Meteo API)   │
            │  (MobileNetV3 + Env)   │  └─────────────────────────┘
            └───────────────┬────────┘
                            │
            ┌───────────────▼─────────────────────────────────────┐
            │                  Diagnostic Outputs                 │
            │  • Disease Classification & Severity Rating         │
            │  • Grad-CAM Visual Explainability Saliency Map      │
            │  • Indic Multilingual Audio Advisory (KN / HI / TE) │
            │  • Geo-Proximity Retailer Search (Haversine Matrix) │
            └─────────────────────────────────────────────────────┘
```

---

## ✨ Key Features

- 🔬 **Edge-Optimized Multimodal ML**: Deep Convolutional MobileNetV3 architecture fused with auxiliary environmental inputs (temperature, relative humidity, precipitation, crop growth stage).
- 📊 **Visual Explainability (Grad-CAM)**: Generates localized heatmap overlays highlighting leaf lesion zones to ensure transparent and trustworthy predictions.
- 🗣️ **Multilingual Voice Advisory**: Auto-generates spoken audio advisories in regional languages (**Kannada, Hindi, Telugu, and English**) for accessibility.
- 💊 **Actionable Treatment Protocols**: Provides curated chemical remedies, exact dosage per acre, and organic alternatives.
- 🏪 **Geo-Proximity Retailer Search**: Calculates real-time distance to verified agricultural input stores stocking the recommended medicines using the Haversine formula.

---

## 🚀 Benchmark Performance Highlights

| Metric | Result | Description |
| :--- | :--- | :--- |
| **Severity Classification Accuracy** | **90.0%** | Categorizes infection severity (Low / Medium / High) |
| **Edge Inference Latency** | **1.3 ms** | Ultra-fast execution on standard mobile/edge CPU |
| **Quantized Model Size** | **~2.0 MB** | Lightweight float16 TFLite footprint for zero-lag mobile deployment |
| **Supported Diseases** | **10 Classes** | Covers major fungal, bacterial, viral infections & healthy crops |

---

## 🏗️ Repository Architecture

```
KRUSHAK_HITHAISHI_AI_SYSTEM/
├── backend/                  # FastAPI Application Core
│   ├── main.py               # REST API entrypoint & middleware configuration
│   ├── routes/
│   │   ├── detect.py         # Multi-input detection & Grad-CAM pipeline
│   │   ├── advisory.py       # Agronomic protocols & chemical advisories
│   │   └── shops.py          # Proximity-based agri-store query endpoint
│   ├── utils/
│   │   ├── model.py          # TFLite interpreter inference engine
│   │   ├── gradcam.py        # Occlusion saliency heatmap generator
│   │   ├── weather.py        # Real-time Open-Meteo API connector
│   │   ├── voice.py          # Multilingual TTS synthesizer
│   │   └── distance.py       # Haversine geo-distance calculator
│   ├── db/                   # SQLAlchemy ORM models & database seeder
│   └── models/               # Quantized TFLite binaries & class label mappings
│
├── mobile/                   # React Native (Expo) Frontend
│   ├── screens/
│   │   ├── HomeScreen.js     # Dashboard with quick actions
│   │   ├── ScanScreen.js     # Live camera viewfinder with framing reticle
│   │   ├── ResultScreen.js   # Heatmap viewer, voice player, and treatment card
│   │   └── ShopsScreen.js    # Nearby retailer listings and dialer trigger
│   ├── components/           # Reusable UI widgets (SeverityBadge, ShopCard)
│   └── services/api.js       # Client API service
│
└── model_training/           # Deep Learning Pipeline
    ├── data_prep_final.py    # Dataset extraction, normalization, and packaging
    ├── train_model_final.py  # MobileNetV3 multimodal fusion network training
    ├── convert_concrete.py   # Concrete function tracing & TFLite converter
    └── evaluate_final.py     # Latency, model footprint, and accuracy benchmarking
```

---

## 🛠️ Quickstart & Local Setup

### 1. Backend Server Setup

```powershell
# Navigate to backend directory
cd backend

# Activate virtual environment
.\.venv\Scripts\Activate.ps1

# Install dependencies
pip install -r requirements.txt

# Seed sample database
python -c "from db.seed_shops import seed_shops; seed_shops('db/shops_sample.csv')"

# Start FastAPI server
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

- **Interactive Swagger Docs**: [http://localhost:8000/docs](http://localhost:8000/docs)
- **Health Check**: [http://localhost:8000/health](http://localhost:8000/health)

---

### 2. Mobile App Setup

```powershell
# Navigate to mobile directory
cd mobile

# Install dependencies
npm install

# Start development server
npm start
```

- Press `a` to run on Android Emulator.
- Press `w` to run on Web Browser.
- Scan the QR code using the **Expo Go** mobile app on physical devices.

---

### 3. Model Training & Export

```powershell
# Run data prep (10 tomato disease classes)
python -c "import sys; sys.path.insert(0, 'model_training'); from data_prep_final import build_dataset; build_dataset('model_training/data', 'model_training/dataset.npz', image_size=224, max_per_class=300)"

# Train Multimodal Fusion Model
python -c "import sys; sys.path.insert(0, 'model_training'); from train_model_final import train; train('model_training/dataset.npz', 'model_training/model.keras', 'model_training', image_size=224, frozen_epochs=5)"

# Convert to TFLite
python model_training/convert_concrete.py
```

---

## 🛡️ License

This project is open-source and available under the [MIT License](LICENSE).
