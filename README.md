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
- **Rigorous Validation**: Conservative cross-validation revealing significant overfitting challenges
- **Limitation Documentation**: Quantified fundamental challenges in multi-class dementia classification
- **Binary Classification Approach**: Developed clinically-oriented disease vs. healthy screening model

## Results

### Multi-Class Classification (AD vs. FTD vs. Controls)
- **Cross-Validation Accuracy**: 65.1% ± 8.4%
- **Test Accuracy**: 67.7%
- **Overfitting Gap**: 22.2% (severe overfitting)
- **FTD Detection**: 12.5% accuracy (worse than random)
- **Conclusion**: Clinically unsuitable due to poor FTD discrimination and overfitting

| Metric | Alzheimer's | Frontotemporal | Control |
|--------|-------------|----------------|---------|
| Precision | 0.80 | 0.33 | 0.62 |
| Recall | 0.92 | 0.12 | 0.80 |
| F1-Score | 0.86 | 0.18 | 0.70 |

### Binary Classification (Disease vs. Healthy)
- **Cross-Validation Accuracy**: 74.6% ± 9.0%
- **Test Accuracy**: 77.8%
- **Overfitting Gap**: 9.7% (acceptable)
- **Sensitivity**: 77.8% (disease detection)
- **Specificity**: 77.8% (healthy identification)

| Metric | Disease | Healthy |
|--------|---------|---------|
| Precision | 0.88 | 0.64 |
| Recall | 0.78 | 0.78 |
| F1-Score | 0.82 | 0.70 |

## Performance Comparison

| Study | Classification | Method | Accuracy | Overfitting |
|-------|---------------|--------|----------|-------------|
| Miltiadous et al. (2023) | AD vs. Controls | RBP + Random Forests | 77.0% | Not reported |
| Miltiadous et al. (2023) | FTD vs. Controls | RBP + MLP | 73.1% | Not reported |
| **This Study** | **AD vs. FTD vs. Controls** | **Enhanced Features + XGBoost** | **65.1%** | **Severe (22.2%)** |
| **This Study** | **FTD + AD vs. Controls** | **Enhanced Features + XGBoost** | **74.6%** | **Acceptable (9.7%)** |

## Key Findings

- **Multi-class limitation**: Severe overfitting and FTD detection failure (12.5%) demonstrate fundamental limitations of resting-state EEG for dementia type discrimination
- **Binary screening potential**: 74.6% accuracy shows moderate promise for preliminary disease detection with acceptable generalization
- **Dataset constraints**: 88 subjects insufficient for complex feature engineering without severe overfitting

## Clinical Implications

The binary classification approach shows moderate potential for preliminary screening but requires larger validation studies before clinical deployment. The multi-class model's failure to distinguish dementia types represents an important negative result that contributes to understanding current EEG-based classification limitations.

## Files Structure

```
├── analyze.ipynb                 # Main analysis notebook
├── data/
│   ├── participants.tsv         # Subject demographics
│   ├── extracted_features.csv   # Engineered features
│   └── performance_comparison.csv
├── train_test_splits/           # Data splits
├── models/                      # Trained models
│   ├── multiclass_xgb_model.pkl
│   └── binary_xgb_model.pkl
└── README.md
```

## Requirements

- Python 3.8+
- MNE-Python
- XGBoost
- scikit-learn
- imbalanced-learn
- pandas, numpy, matplotlib, seaborn

## Citation

Built upon the dataset from:
Miltiadous, A., et al. (2023). A Dataset of Scalp EEG Recordings of Alzheimer's Disease, Frontotemporal Dementia and Healthy Subjects from Routine EEG. *Data*, 8(6), 95.
