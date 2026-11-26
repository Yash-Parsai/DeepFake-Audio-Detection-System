# DeepShield – Audio Deepfake Detection

Labels: 0 = REAL (bonafide), 1 = SYNTHETIC (spoof). Run everything from this folder with the venv active.

## Step 1 – Data pipeline
    python scripts/01_build_manifests.py --root "<path>\LA\LA" --workers 8

## Step 2 – Mel/MFCC front-ends + baseline Mel-CNN
    python -m pytest tests -q
    python scripts/02_train_baseline.py                  # train, then evaluate best checkpoint on dev + eval
    python scripts/02_train_baseline.py --eval-only      # re-evaluate outputs/baseline_cnn/best.pt

Outputs in outputs/baseline_cnn/: best.pt, history.csv, curves.png, roc_dev.png, roc_eval.png,
scores_dev.csv, scores_eval.csv, metrics.json (Accuracy, Precision, Recall, F1, ROC-AUC, EER, per-attack EER).

GPU PyTorch (Windows):  pip install torch --index-url https://download.pytorch.org/whl/cu130

## Notebook (for presentation) – CUDA training in Jupyter
    pip install notebook ipykernel ipywidgets
    jupyter notebook          # then open DeepShield_Training.ipynb  ->  Run All
Set TRAIN = False in the settings cell to load a saved checkpoint instead of retraining.
Outputs (checkpoint, history, scores, metrics.json, figures) go to outputs/notebook_run/.
