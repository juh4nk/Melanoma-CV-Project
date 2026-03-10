# Training Pipeline

Binary melanoma classification pipeline built with TensorFlow and EfficientNetB0.  
This is an educational portfolio project — **not a clinical tool**.

---

## Structure

```
training/
├── data/
│   └── dataset_loader.py       # Loads ISIC 2017 dataset → tf.data pipelines
├── preprocessing/
│   └── image_preprocessing.py  # Image decode, resize, normalize, augmentation
├── models/
│   └── model_builder.py        # EfficientNetB0 backbone + classification head
├── evaluation/
│   └── metrics.py              # Confusion matrix, sensitivity, F1, ROC-AUC
├── train.py                    # Entry point — runs the full pipeline
└── requirements.txt            # Python dependencies
```

---

## Pipeline Flow

```
ISIC 2017 dataset (disk)
        │
        ▼
data/dataset_loader.py          — reads CSVs, builds tf.data pipelines
        │   calls
        ▼
preprocessing/image_preprocessing.py  — decode → resize → normalize → augment
        │
        ▼
models/model_builder.py         — EfficientNetB0 + head, two-phase training
        │
        ▼
evaluation/metrics.py           — test set evaluation, plots, metrics JSON
        │
        ▼
.tflite export                  — for Android app deployment
```

---

## Quickstart

```bash
pip install -r requirements.txt
python train.py
```

> **Note:** The dataset is not included in this repository.  
> Download ISIC 2017 from [isic-archive.com](https://isic-archive.com) and place it under `data/`.

---

## Modules

### `data/dataset_loader.py`
Reads the ISIC 2017 ground-truth CSVs, pairs image file paths with binary labels (1 = melanoma, 0 = non-melanoma), and produces `tf.data.Dataset` objects for train, val, and test splits.

### `preprocessing/image_preprocessing.py`
All image transforms used inside the `tf.data` pipeline. Base preprocessing (decode, resize, normalize) is applied to all splits. Augmentation (flips, rotation, brightness jitter) is applied to the training split only.

### `models/model_builder.py`
Assembles the EfficientNetB0 backbone with a custom classification head. Manages the two-phase training strategy: backbone frozen for warm-up, top layers unfrozen for fine-tuning.

### `evaluation/metrics.py`
Runs inference on the test set and computes sensitivity, precision, F1, ROC-AUC, and specificity. Saves a confusion matrix heatmap and ROC curve as PNG files. **Sensitivity is the primary metric** — false negatives are more harmful than false positives in melanoma screening.

### `train.py`
Entry point. Calls each module in order to run the full pipeline from data loading through model export.

---

## Key Design Decisions

| Decision | Rationale |
|---|---|
| EfficientNetB0 backbone | Strong accuracy-to-parameter ratio; built-in normalization; clean TFLite export |
| Transfer learning | ISIC 2017 is small (~2000 images); training from scratch would overfit |
| Two-phase training | Warm-up protects pretrained weights; fine-tuning adapts backbone to skin lesion domain |
| Sensitivity as primary metric | False negatives (missed melanoma) are more harmful than false positives |
| Class weights | Melanoma is ~20% of ISIC 2017; weighted loss prevents the model from ignoring it |

---

## Status

> v1 — Structure defined. Functions are stubbed with docstrings.  
> Implementation of each module is the next step.