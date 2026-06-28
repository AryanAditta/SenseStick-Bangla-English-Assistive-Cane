# SenseStick: Bangla-English Edge-AI Assistive Cane

SenseStick is a low-cost edge-AI assistive cane prototype for visually impaired and elderly users. The system integrates camera-based perception, Bangla-English audio feedback, OCR, QR/barcode recognition, color detection, staircase detection, road-sign detection, zebra-crossing detection, biomedical sensing, fall/stick-recovery alerting, TinyML-based biomedical reliability filtering, and caregiver-side IoT monitoring.

## Key Features

* Bangla and English contextual audio feedback
* YOLOv8-based object detection
* Approximate object-distance estimation from bounding-box geometry
* Left/center/right spatial feedback
* OCR-based English text reading
* QR/barcode recognition and URL/text summarization
* HSV-based color detection
* Staircase, road-sign, and zebra-crossing detection
* MAX30102-based physiological sensing support
* MPU6050-based fall/stick-recovery alerting
* DS18B20-based temperature sensing
* ESP32 caregiver-dashboard communication
* TinyML biomedical reliability gate for stable-versus-motion-affected physiological windows

## System Overview

SenseStick follows a modular edge-AI architecture:

1. **Perception Layer:** A webcam attached to Raspberry Pi captures video frames for object detection, OCR, QR/barcode recognition, color detection, and road-safety perception.
2. **Decision and Control Layer:** Arduino-based logic handles rule-based safety events such as fall or stick-recovery alerts.
3. **Biomedical Reliability Layer:** A TinyML reliability gate uses PPG, temperature, and IMU-derived features to determine whether physiological readings are stable or motion-affected.
4. **Feedback Layer:** Bangla-English audio templates generate localized user feedback.
5. **IoT Layer:** ESP32 sends selected health and alert data to a caregiver dashboard.

## Repository Structure

```text
SenseStick-Bangla-English-Assistive-Cane/
│
├── README.md
├── LICENSE
├── requirements.txt
├── .gitignore
│
├── src/
│   ├── object_detection/
│   │   ├── object_audio_bn.py
│   │   └── object_audio_en.py
│   │
│   ├── color_detection/
│   │   ├── color_audio_bn.py
│   │   └── color_audio_en.py
│   │
│   ├── ocr/
│   │   └── ocr_english.py
│   │
│   ├── qr_barcode/
│   │   └── qr_audio_summary.py
│   │
│   ├── road_sign/
│   │   ├── road_sign_bn.py
│   │   └── road_sign_en.py
│   │
│   ├── zebra_crossing/
│   │   ├── zebra_bn.py
│   │   └── zebra_en.py
│   │
│   ├── biomedical_tinyml/
│   │   ├── feature_extraction.py
│   │   ├── train_reliability_gate.py
│   │   └── model_profile.md
│   │
│   └── arduino_esp32/
│       ├── arduino_fall_detection.ino
│       └── esp32_caregiver_dashboard.ino
│
├── models/
│   ├── README.md
│   ├── road_sign_model_note.md
│   ├── zebra_crossing_model_note.md
│   └── tinyml_reliability_gate_note.md
│
├── assets/
│   ├── prototype/
│   ├── demo_outputs/
│   └── figures/
│
├── docs/
│   ├── hardware_components.md
│   ├── dataset_links.md
│   ├── setup_guide.md
│   └── safety_and_limitations.md
│
└── paper/
    └── README.md
```

## Hardware Components

The prototype uses commonly available low-cost embedded components:

* Raspberry Pi 4
* Webcam
* Arduino Uno
* ESP32
* MAX30102 PPG sensor
* MPU6050 accelerometer/gyroscope
* DS18B20 temperature sensor
* Buzzer
* Audio output unit
* 20,000 mAh power bank

## Installation

Clone the repository:

```bash
git clone https://github.com/AryanAditta/SenseStick-Bangla-English-Assistive-Cane.git
cd SenseStick-Bangla-English-Assistive-Cane
```

Install Python dependencies:

```bash
pip install -r requirements.txt
```

## Example Usage

Run Bangla object-detection feedback:

```bash
python src/object_detection/object_audio_bn.py
```

Run English object-detection feedback:

```bash
python src/object_detection/object_audio_en.py
```

Run Bangla color-detection feedback:

```bash
python src/color_detection/color_audio_bn.py
```

Run English OCR:

```bash
python src/ocr/ocr_english.py
```

Run QR/barcode recognition:

```bash
python src/qr_barcode/qr_audio_summary.py
```

Run Bangla road-sign detection:

```bash
python src/road_sign/road_sign_bn.py
```

Run Bangla zebra-crossing detection:

```bash
python src/zebra_crossing/zebra_bn.py
```

## Datasets

The full datasets are not redistributed in this repository. Please download them from their original sources:

* Stairs Dataset: Kaggle Stairs Dataset
* Zebra Crossing Dataset: CDSet-3434
* Road Sign Dataset: German Traffic Sign Detection Benchmark, GTSDB
* Biomedical Reliability Dataset: public PPG, temperature, and IMU dataset used for TinyML reliability-gate evaluation

Dataset links and preprocessing notes are provided in `docs/dataset_links.md`.

## Model Artifacts

Selected model artifacts or model notes may be provided in the `models/` directory when redistribution is allowed. Large trained weights and third-party datasets may be excluded if licensing or file-size restrictions apply.

## Safety and Limitations

SenseStick is a research prototype. It is not a certified medical device, clinical monitor, or fully field-validated navigation system. The biomedical TinyML module is used only as a reliability filter for stable-versus-motion-affected physiological windows. It does not diagnose disease or validate clinical-grade heart-rate or SpO₂ accuracy.

Vision-based outputs depend on camera placement, lighting, occlusion, viewpoint, and dataset-domain similarity. Road-safety perception results should be interpreted as dataset-level feasibility evidence until tested in real deployment conditions.

## Code Availability

This repository provides implementation files, representative demo assets, and selected model documentation for the SenseStick research prototype. Sensitive credentials, private dashboard tokens, Wi-Fi details, and full third-party datasets are not included.

## Citation

If you use this repository, please cite the associated SenseStick paper after publication.

```bibtex
@inproceedings{sensestick2026,
  title={SenseStick: A Bangla-English Edge-AI Cane for Road-Safety and Biomedical Reliability Monitoring},
  author={Author information removed for review},
  booktitle={Proceedings of the accepted conference},
  year={2026}
}
```

## License

This repository is released under the MIT License for research and educational use.
