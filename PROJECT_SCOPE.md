# Project Scope

## A) One-Line Pitch
A conservative, engineering-focused, end-to-end melanoma screening prototype designed to demonstrate reproducible machine learning training, structured evaluation, secure deployment, and collaborative software development — strictly for educational and portfolio purposes.

---

## B) Audience & Use-Case
- Primary audience: machine learning and software engineering recruiters.
- Purpose: demonstrate an end-to-end ML system, from data handling and model training to evaluation, inference, and application integration.
- Use-case: educational exploration of melanoma detection, not medical diagnosis.

---

## C) Dataset
- Planned datasets: ISIC / HAM10000.
- Task framing: binary classification (melanoma vs non-melanoma).
- Data considerations:
  - Class imbalance awareness.
  - Patient-level data leakage prevention.
  - Stratified train/validation/test splits.
- Raw datasets will not be committed to the repository.

---

## D) Model Approach
- Initial approach: training a baseline CNN model from scratch.
- Focus: clarity, correctness, and reproducibility over architectural complexity.
- Advanced architectures (e.g. Vision Transformers) are considered optional stretch goals if time permits.

---

## E) Evaluation Plan
- Primary metric: sensitivity (recall for melanoma class).
- Secondary metrics:
  - F1 score
  - ROC-AUC
- Evaluation artefacts:
  - Confusion matrix
  - ROC curve
  - Metric summary table
- Explicit discussion of false negatives vs false positives.
- Qualitative error analysis of misclassified samples.

---

## F) Deliverables
- A clean, well-documented public GitHub repository.
- Reproducible environment setup.
- Model training pipeline.
- Inference pipeline.
- Evaluation report with plots and tables.
- Optional explainability (e.g. Grad-CAM).
- Android application demo with on-device inference (model exported for mobile use).

---

## G) Guardrails
- This project is strictly for educational and portfolio purposes.
- It is not intended for clinical or diagnostic use.
- Results must not be relied upon in real-world medical decision-making.
- No patient-identifiable data will be stored.
- Raw datasets will not be committed to the repository.
- If image input is supported in the demo, inputs will be discarded immediately or stored securely and locally.
- Reproducibility and transparency are prioritised over state-of-the-art performance claims.
