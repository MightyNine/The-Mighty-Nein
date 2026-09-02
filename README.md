# GAN Testing and Evaluation

## Overview

This code extends the existing GAN model by adding functionality for testing and evaluating the trained discriminator using the `test.csv` dataset from CICIoT2023.

The purpose of these additions is to determine how effectively the trained GAN can identify anomalous IoT network traffic and to provide visual representations of the model's performance.

## Features Added

### Test Dataset Loading
- Loads the CICIoT2023 `test.csv` dataset.
- Displays the number and types of network traffic labels contained in the dataset.

### Binary Classification
The original CICIoT2023 labels are converted into two categories:

- `0` = Benign traffic
- `1` = Anomalous / malicious traffic

This allows the GAN to be evaluated as a binary anomaly detection system.

### Test Data Preprocessing
- Removes the original text-based label column.
- Keeps numerical network traffic features.
- Handles missing and infinite values.
- Scales the numerical features.
- Formats the data into the `16 × 16` input structure expected by the existing GAN discriminator.

### GAN Anomaly Detection
The processed test data is passed through the trained GAN discriminator.

The discriminator produces a score for each network traffic sample. A detection threshold is then used to classify the sample as either:

- Benign
- Anomalous

### Model Evaluation

The predicted classifications are compared against the actual labels from `test.csv`.

The following performance metrics are calculated:

- Accuracy
- Precision
- Recall
- F1 Score
- Classification Report

### Data Visualisation

Three visualisations are generated to make the GAN's performance easier to analyse:

1. **Confusion Matrix** – Shows correct and incorrect benign/anomaly classifications.
2. **Performance Metrics Graph** – Displays accuracy, precision, recall and F1 score.
3. **Discriminator Score Distribution** – Compares discriminator scores for benign and anomalous network traffic.

## Purpose

These additions allow the existing GAN model to be tested against previously unseen IoT network traffic rather than only being trained on the training dataset.

The evaluation results can be used to analyse the effectiveness of the GAN approach and support comparison with the LSTM model being developed as part of the THEIA IoT anomaly detection project.
