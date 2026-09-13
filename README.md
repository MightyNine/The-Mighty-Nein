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
