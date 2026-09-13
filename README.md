
# GAN Testing and Evaluation

## Overview

This code extends the existing GAN model by adding functionality for dataset access, test data preparation, anomaly detection, model evaluation and result visualisation.

The purpose of these additions is to allow the trained GAN discriminator to be tested against previously unseen IoT network traffic from the CICIoT2023 `test.csv` dataset and determine how effectively it can distinguish benign traffic from anomalous or malicious traffic.

The code also supports shared access to the training and testing datasets through Google Drive, allowing multiple team members to run the same Google Colab notebook without repeatedly uploading the datasets for each runtime session.

## Features Added

### Shared Dataset Access

The code mounts Google Drive in Google Colab and accesses the project datasets from a shared folder named `Theia_Data`.

The expected dataset locations are:

```text
/content/drive/MyDrive/Theia_Data/train.csv
/content/drive/MyDrive/Theia_Data/test.csv
```

Each team member can add the shared `Theia_Data` folder as a shortcut inside their own `My Drive`, allowing the same notebook and file paths to be used by the whole team.

### Training Dataset Preparation

The training dataset is prepared for use with the GAN by:

* Selecting benign network traffic for GAN training.
* Keeping the numerical network traffic features.
* Handling missing and infinite values.
* Calculating median, minimum and maximum values from the training data.
* Scaling the numerical features into the range required by the GAN.
* Formatting the network traffic data into a `16 × 16` input structure.

The training preprocessing values are retained so that the same preparation method can be applied consistently to the test dataset.

### Test Dataset Loading

The code loads the CICIoT2023 `test.csv` dataset separately from the training dataset.

The test dataset contains previously unseen benign and malicious network traffic and is used to evaluate how effectively the trained GAN can identify anomalies.

### Binary Classification

The original CICIoT2023 traffic labels are converted into two categories:

* `0` = Benign traffic
* `1` = Anomalous / malicious traffic

This allows the GAN to be evaluated as a binary anomaly detection system rather than requiring the model to classify every individual attack type.

### Test Data Preprocessing

The test dataset is prepared using the same structure used for the training data.

The preprocessing:

* Removes the original text-based label column from the model input.
* Keeps the same numerical features used during training.
* Handles missing and infinite values.
* Uses the median values calculated from the training dataset.
* Uses the training dataset's minimum and maximum values for scaling.
* Formats the data into the same `16 × 16` input structure used by the GAN.

Using the training data's preprocessing values ensures that the training and testing datasets are processed consistently.

### GAN Anomaly Detection

The processed test data is passed through the trained GAN discriminator.

The discriminator produces a score for each network traffic sample. These scores represent how closely the sample resembles the normal traffic patterns learned during training.

A detection threshold of `0.5` is used to classify each sample as either:

* Benign
* Anomalous

Higher discriminator scores are treated as more similar to normal traffic, while lower scores are treated as potentially anomalous.

### Model Evaluation

The predicted classifications are compared against the actual labels contained in `test.csv`.

The following performance metrics are calculated:

* Accuracy
* Precision
* Recall
* F1 Score
* Classification Report

These metrics provide different measures of the GAN's performance and help identify both correct detections and incorrect classifications.

### Data Visualisation

Three visualisations are generated to make the GAN's anomaly detection performance easier to analyse:

1. **Confusion Matrix** – Shows the number of correct and incorrect benign and anomaly classifications.
2. **Performance Metrics Graph** – Displays the model's accuracy, precision, recall and F1 score.
3. **Discriminator Score Distribution** – Compares the discriminator scores produced for benign and anomalous traffic and displays the detection threshold.

## Purpose

These additions extend the existing GAN model beyond training by providing a complete testing and evaluation process.

The trained discriminator can be evaluated against previously unseen IoT network traffic, its anomaly detection performance can be measured using recognised classification metrics, and the results can be presented through visualisations that make the model's behaviour easier to understand.

The evaluation results can also be used to identify strengths and weaknesses in the GAN approach and support comparison with the LSTM model being developed as part of the THEIA IoT anomaly detection project.
