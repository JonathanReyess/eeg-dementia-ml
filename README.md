# Advanced EEG-Based Classification of Alzheimer's Disease and Frontotemporal Dementia

## Project Overview

This project extends the foundational work of Miltiadous et al. (2023) by developing advanced machine learning classifiers for distinguishing between Alzheimer's Disease (AD), Frontotemporal Dementia (FTD), and healthy controls using EEG data. The study implements comprehensive feature engineering, class imbalance handling, and rigorous validation techniques.

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
- **Systematic Resampling Evaluation**: Tested 9 different techniques for handling class imbalance
- **Rigorous Validation**: Conservative cross-validation prioritizing generalization over peak performance
- **Binary Classification Approach**: Developed disease vs. healthy screening model

## Results

### Multi-Class Classification (AD vs. FTD vs. Controls)
- **Cross-Validation Accuracy**: 52.6%
- **Conclusion**: Insufficient for reliable AD/FTD discrimination

### Binary Classification (Disease vs. Healthy)
- **Cross-Validation Accuracy**: 73.3% ± 5.5%
- **Test Accuracy**: 77.8%
- **Sensitivity**: 77.8% (disease detection)
- **Specificity**: 77.8% (healthy identification)

| Metric | Disease | Healthy |
|--------|---------|---------|
| Precision | 0.88 | 0.64 |
| Recall | 0.78 | 0.78 |
| F1-Score | 0.82 | 0.70 |

## Performance Comparison

| Study | Classification | Method | Accuracy |
|-------|---------------|--------|----------|
| Miltiadous et al. (2023) | AD vs. Controls | RBP + Random Forests | 77.0% |
| Miltiadous et al. (2023) | FTD vs. Controls | RBP + MLP | 73.1% |
| **Our Study** | **Multi-class** | **Enhanced Features + XGBoost** | **52.6%** |
| **Our Study** | **Binary Screening** | **Enhanced Features + XGBoost** | **73.3%** |

## Key Findings

- **Multi-class limitation**: Current resting-state EEG approaches cannot reliably distinguish between specific dementia types
- **Binary screening potential**: 73% accuracy shows promise for preliminary disease detection
- **Dataset constraints**: 88 subjects insufficient for complex feature engineering
- **Methodological insights**: Conservative validation essential for realistic clinical assessment

## Clinical Implications

The binary classification approach shows moderate potential for preliminary screening but requires larger validation studies before clinical deployment. The study demonstrates both the promise and limitations of EEG-based dementia classification.

## Files Structure

```
├── analyze.ipynb                 # Main analysis notebook
├── data/
│   ├── participants.tsv         # Subject demographics
│   ├── extracted_features.csv   # Engineered features
│   └── performance_comparison.csv
├── train_test_splits/           # Data splits
└── models/                      # Trained models
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
