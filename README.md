# Bone Fracture Detection (MURA v1.1)

Classical ML pipeline for musculoskeletal X-ray fracture detection using HOG features.

## Contents
- `bone_fracture_detection.ipynb`: end-to-end notebook (preprocessing → HOG → models → evaluation)
- `presentation_prompt.md`: ready prompt to generate a PPTX deck
- Generated figures (PNG): confusion matrices, metrics comparison, preprocessing steps, examples

## Setup
```powershell
# From project folder
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

## Run
Open `bone_fracture_detection.ipynb` and run all cells (top → bottom). Figures will be saved in the folder and `best_model.joblib` will be created.

## Requirements
See `requirements.txt`.

## Notes
- Dataset path is configured to `c:\Users\user\Desktop\DIP Project\MURA-v1.1` in the notebook.
- Models: Linear SVM (scaled), Logistic Regression (scaled), Random Forest, KNN, Decision Tree.
- Evaluation includes confusion matrices, ROC/AUC (if scores available), decision margin histogram, threshold sweep, and 5-fold CV.
