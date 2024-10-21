## Project Overview
The goal of this project is to develop a machine learning model that can predict cognitive decline based on patterns in electroencephalogram (EEG) data, which records brain activity. 


## Data Acquisition

This project utilizes the EEG dataset available on OpenNeuro. To download this dataset, you can use the `@openneuro/cli` command-line tool. 

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