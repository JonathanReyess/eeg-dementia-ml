
# Cognitive Decline Prediction Using EEG Data and Machine Learning.

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