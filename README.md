# FractureDetect-MURA

A HOG-based classical machine learning pipeline for bone fracture detection in MURA radiographs, with clean visuals, comprehensive metrics, and reproducible notebook workflows.

---

## Goal

Develop an interpretable, reproducible pipeline to detect bone fractures in musculoskeletal X-ray images using classical computer vision (HOG features) and machine learning models—without deep learning—while providing robust evaluation metrics and visualizations suitable for clinical understanding and presentation.

## Dataset

**MURA (Musculoskeletal Radiographs) v1.1**  
A large dataset of upper extremity radiographs from Stanford ML Group.

- **Download**: [MURA v1.1 Dataset](https://stanfordmlgroup.github.io/competitions/mura/)
- **Size**: ~40,000 studies across 7 body parts (Elbow, Finger, Forearm, Hand, Humerus, Shoulder, Wrist)
- **Labels**: Binary classification (Normal / Abnormal - fracture present)
- **Split**: Pre-defined train/validation sets with study-level labels

**Setup**: Download and extract the dataset to `MURA-v1.1/` in your project folder. The notebook automatically strips the prefix and loads images from CSV manifests.

## Approach

### Preprocessing
1. Resize images to 128×128
2. Histogram equalization (enhance contrast)
3. Gaussian blur (reduce noise)
4. Normalization (scale pixel values to [0,1])

### Feature Extraction
- **HOG (Histogram of Oriented Gradients)**: Captures edge and texture patterns
  - 9 orientations, 8×8 pixels per cell, 2×2 cells per block
  - Produces ~3,000-dimensional feature vectors per image

### Models Evaluated
- Linear SVM (with StandardScaler)
- Logistic Regression (with StandardScaler)
- Random Forest
- K-Nearest Neighbors
- Decision Tree

### Evaluation
- Accuracy, Precision, Recall, F1-Score
- Confusion matrices for all models
- ROC curve & AUC for best model
- Decision margin histogram (confidence analysis)
- Threshold sweep (optimal F1 trade-off)
- Stratified 5-fold cross-validation

## Results

- **Best Model**: Logistic Regression (Scaled)
  - **F1-Score**: ~0.53 on validation set
  - **AUC**: Computed and visualized in ROC curve
  - **Interpretation**: Model provides reasonable separation; further improvements possible with CLAHE preprocessing, ensemble methods, or deep learning

- **Insights**:
  - Class imbalance and high intra-class variability make the task challenging
  - HOG features capture structural patterns but lack semantic understanding
  - Clear visualizations (high-confidence predictions, ambiguous cases, preprocessing steps) aid interpretability

- **Outputs**: 10+ saved figures including dataset samples, confusion matrices, metrics comparison, representative examples, preprocessing pipeline, margin histograms, ROC curves, and threshold analysis

## Repository Contents

```
├── bone_fracture_detection.ipynb   # End-to-end notebook (data → features → models → evaluation)
├── requirements.txt                # Python dependencies
├── best_model.joblib               # Saved best model (Logistic Regression pipeline)
├── .gitignore                      # Excludes dataset and caches
└── *.png                           # Generated figures (10+ visualizations)
```

## Setup & Run

### Prerequisites
- Python 3.8+
- ~40GB disk space for MURA dataset (not included in repo)

### Installation

```powershell
# Clone the repository
git clone https://github.com/Yosr-Bejaoui/FractureDetect-MURA.git
cd FractureDetect-MURA

# Create virtual environment
python -m venv .venv
.\.venv\Scripts\Activate.ps1

# Install dependencies
pip install -r requirements.txt
```

### Download Dataset
1. Visit [MURA Dataset](https://stanfordmlgroup.github.io/competitions/mura/)
2. Download and extract to `MURA-v1.1/` inside the project folder
3. Verify structure: `MURA-v1.1/train/`, `MURA-v1.1/valid/`, CSV files at root

### Run Notebook
```powershell
# Open in Jupyter or VS Code
jupyter notebook bone_fracture_detection.ipynb

# Or use VS Code Jupyter extension
code bone_fracture_detection.ipynb
```

Run all cells sequentially (top → bottom). Figures will be saved as PNGs and `best_model.joblib` will be created.

## Key Features

- **Interpretable**: HOG features and classical ML (no black-box deep learning)
- **Reproducible**: Fixed random seeds, saved models, clear notebook structure
- **Visual**: 10+ publication-quality figures for presentations and reports
- **Comprehensive**: Preprocessing visualization, margin analysis, threshold tuning, cross-validation
- **Extensible**: Easy to swap CLAHE preprocessing, add ensemble methods, or integrate deep learning baselines

## Citation

If you use MURA dataset, please cite:
```
Rajpurkar et al. "MURA: Large Dataset for Abnormality Detection in Musculoskeletal Radiographs". 
arXiv:1712.06957, 2017.
```

## Contact

**Yosr Bejaoui**  
GitHub: [@Yosr-Bejaoui](https://github.com/Yosr-Bejaoui)

---

**Star this repository** if you find it useful for your medical imaging or computer vision projects.
