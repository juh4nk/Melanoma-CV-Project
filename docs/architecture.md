# System Architecture (Planned)

This document outlines the intended high-level architecture of the melanoma CV system.

## 1. Training Pipeline (Python)

Components:
- Dataset loading and preprocessing
- Stratified splitting with leakage checks
- Model training
- Evaluation metrics and plots
- Model export (e.g., TFLite conversion for mobile deployment)

Output:
- Trained model artifact
- Evaluation report

---

## 2. Deployment Pipeline (Android)

Components:
- Mobile UI (Java)
- On-device model inference
- Image input handling
- Immediate disposal of user-uploaded images (no storage)

Model:
- Converted lightweight format suitable for mobile inference

---

## 3. Separation of Concerns

- Training code does not depend on Android code.
- Android code does not contain training logic.
- Shared interface is the exported model file only.

---

## 4. Future Extensions (Optional)

- Explainability visualisations (e.g., Grad-CAM)
- Model comparison experiments
- Performance benchmarking across devices
