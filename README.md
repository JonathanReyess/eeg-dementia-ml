# Advanced EEG-Based Classification of Alzheimer's Disease and Frontotemporal Dementia

## Project Overview

This project extends the foundational work of Miltiadous et al. (2023) by developing advanced machine learning classifiers for distinguishing between Alzheimer's Disease (AD), Frontotemporal Dementia (FTD), and healthy controls using EEG data. The study implements comprehensive feature engineering, class imbalance handling, and rigorous validation techniques that reveal both the potential and fundamental limitations of current EEG-based approaches.

## Dataset

**Source**: Miltiadous et al. (2023) EEG dataset from OpenNeuro (ds004504)
- **Participants**: 88 subjects (36 AD, 23 FTD, 29 controls)
- **Recording**: 19-channel resting-state EEG, eyes-closed condition
- **Format**: BIDS-compliant preprocessed data

### Downloading the Dataset

```bash
# Install OpenNeuro CLI
npm install -g @openneuro/cli

# Login to OpenNeuro
openneuro login

# Download dataset
openneuro download --snapshot 1.0.7 ds004504 ds004504-download/
```

## Key Contributions

- **Advanced Feature Engineering**: Extended beyond basic spectral features to include connectivity measures and hemispheric asymmetry
- **Systematic Resampling Evaluation**: Tested 7 different techniques for handling class imbalance
- **Rigorous Validation**: Conservative cross-validation with stratified k-fold approach
- **MLflow Integration**: Comprehensive experiment tracking for reproducibility
- **Limitation Documentation**: Quantified fundamental challenges in multi-class dementia classification
- **Binary Classification Approach**: Developed clinically-oriented disease vs. healthy screening model

## Results

### Multi-Class Classification (AD vs. FTD vs. Controls)
- **Cross-Validation Accuracy**: 65.2% ± 8.4%
- **Test Accuracy**: 67.7%
- **Generalization**: Good (2.6% gap between CV and test)
- **FTD Detection**: 12.5% recall (critical limitation)
- **Conclusion**: Clinically unsuitable due to poor FTD discrimination, despite good generalization

| Metric | Alzheimer's | Frontotemporal | Control |
|--------|-------------|----------------|---------|
| Precision | 0.80 | 0.33 | 0.62 |
| Recall | 0.92 | 0.12 | 0.80 |
| F1-Score | 0.86 | 0.18 | 0.70 |

![Multiclass Confusion Matrix](results/figures/confusion_matrix_multiclass.png)

**Key Insight**: The multiclass model generalizes well but has fundamentally insufficient accuracy for clinical use. The confusion matrix reveals the model's critical failure in FTD detection, with most FTD cases misclassified as Alzheimer's or controls.

### Binary Classification (Disease vs. Healthy)
- **Cross-Validation Accuracy**: 74.6% ± 9.0%
- **Test Accuracy**: 77.8%
- **Generalization**: Excellent (3.1% gap)
- **Sensitivity**: 77.8% (disease detection)
- **Specificity**: 77.8% (healthy identification)

| Metric | Disease | Healthy |
|--------|---------|---------|
| Precision | 0.88 | 0.64 |
| Recall | 0.78 | 0.78 |
| F1-Score | 0.82 | 0.70 |

![Binary Confusion Matrix](results/figures/confusion_matrix_binary.png)

The binary classifier shows balanced performance across both classes, making it suitable for preliminary screening applications.

## Performance Comparison

| Study | Classification | Method | CV Accuracy | Generalization |
|-------|---------------|--------|-------------|----------------|
| Miltiadous et al. (2023) | AD vs. Controls | RBP + Random Forests | 77.0% | Not reported |
| Miltiadous et al. (2023) | FTD vs. Controls | RBP + MLP | 73.1% | Not reported |
| **This Study** | **AD vs. FTD vs. Controls** | **Enhanced Features + XGBoost** | **65.2%** | **Good (2.6% gap)** |
| **This Study** | **Disease vs. Controls** | **Enhanced Features + XGBoost** | **74.6%** | **Excellent (3.1% gap)** |

## Key Findings

- **Multi-class limitation**: Poor FTD detection (12.5% recall) demonstrates fundamental limitations of resting-state EEG for dementia type discrimination
- **Binary screening potential**: 74.6% CV accuracy with excellent generalization shows promise for preliminary disease detection
- **Resampling analysis**: Original (no resampling) performed best for multiclass; SMOTE optimal for binary classification
- **Feature engineering impact**: Binary model benefited from 31 engineered features reduced to 25 selected features
- **Good generalization**: Both models show strong generalization (< 3.2% gaps), indicating adequate regularization

## Clinical Implications

The binary classification approach shows moderate potential for preliminary screening with robust generalization. The multi-class model's failure to distinguish dementia types (particularly FTD) represents an important negative result: the limitation is not model architecture or overfitting, but rather the fundamental challenge of using resting-state EEG alone for dementia subtype classification.

## MLflow Experiment Tracking

This project uses MLflow for comprehensive experiment tracking:

```bash
# Launch MLflow UI
mlflow ui
```

## Files Structure

```
├── analyze.ipynb                 # Main analysis notebook with MLflow integration
├── data/
│   ├── participants.tsv         # Subject demographics
│   ├── extracted_features.csv   # Engineered features
│   └── performance_comparison.csv
├── train_test_splits/           # Data splits
├── mlruns/                      # MLflow tracking data
├── models/                      # Trained models
│   ├── multiclass_xgb_model_20250929.pkl
│   └── binary_xgb_model_20250929.pkl
└── README.md
```

## Requirements

- Python 3.8+
- MNE-Python
- XGBoost
- scikit-learn
- imbalanced-learn
- mlflow
- pandas, numpy, matplotlib, seaborn

## Citation

Built upon the dataset from:
Miltiadous, A., et al. (2023). A Dataset of Scalp EEG Recordings of Alzheimer's Disease, Frontotemporal Dementia and Healthy Subjects from Routine EEG. *Data*, 8(6), 95.

