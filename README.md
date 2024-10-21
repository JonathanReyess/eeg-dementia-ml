
# Cognitive Decline Prediction Using EEG Data and Machine Learning

## Project Overview

The goal of this project is to develop a machine learning model that can predict cognitive decline based on patterns in electroencephalogram (EEG) data, which records brain activity. 

## Data Acquisition

This project utilizes the EEG dataset available on OpenNeuro. 

The dataset contains EEG resting state recordings from individuals diagnosed with Alzheimer's disease (AD), Frontotemporal Dementia (FTD), and healthy controls (CN).

To download this dataset, you can use the `@openneuro/cli` command-line tool. 

### Installation
First, ensure you have Node.js installed on your machine. You can download it from [nodejs.org](https://nodejs.org/).

Then, install the OpenNeuro CLI globally by running:
```bash
npm install -g @openneuro/cli
```

### Authentication

Before running the download command, you will need to log in to your OpenNeuro account to obtain an API key. Use the following command to log in:

```bash
openneuro login
```

### Downloading the Dataset 

To download the dataset, execute the following command in your terminal:

```bash
openneuro download --snapshot 1.0.7 ds004504 ds004504-download/
```

## Results

The performance of the model was evaluated using precision, recall, and F1-score metrics across the different classes. 

The following table summarizes the results:

| Class | Precision | Recall | F1-Score | Support |
|-------|-----------|--------|----------|--------|
| A (Alzheimer's Disease) | 0.67      | 0.75   | 0.71     | 8      |
| F (Frontotemporal Dementia) | 0.75      | 0.38   | 0.50     | 8      |
| C (Healthy Control) | 0.40      | 1.00   | 0.57     | 2      |

Overall accuracy of the model was **61%**. 

### Summary of Performance Metrics
- **Macro Average**:
  - Precision: 0.61
  - Recall: 0.71
  - F1-Score: 0.59
- **Weighted Average**:
  - Precision: 0.67
  - Recall: 0.61
  - F1-Score: 0.60

### Class Label Definitions
- **A** = Alzheimer's Disease (Class 0)
- **F** = Frontotemporal Dementia (Class 1)
- **C** = Healthy Control (Class 2)

These results indicate varying performance across different classes, with the model showing stronger precision and recall for Alzheimer's Disease and weaker performance for Healthy Control.


## Next Steps

### Hyperparameter Tuning

To enhance the performance of our model, the next step involves conducting a systematic search for optimal hyperparameters. This can be achieved through techniques such as Grid Search or Randomized Search. 

By identifying which parameters have the most significant impact on model performance, we aim to refine our model further and improve its predictive accuracy.

## Related Research

This project is built upon methodologies and insights presented in the research paper titled [“EEG Features for Cognitive Load Classification: A Systematic Review”](https://www.mdpi.com/2306-5729/8/6/95). The paper explores various EEG features and their effectiveness in cognitive load classification, providing a foundation for the feature selection and analysis conducted in this project. By leveraging the techniques outlined in this study, we aim to enhance our understanding of cognitive load through EEG signal processing.
