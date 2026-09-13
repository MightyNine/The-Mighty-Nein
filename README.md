# GAN Testing and Evaluation

## Overview

This code extends the existing GAN model by adding functionality for testing and evaluating the trained discriminator using the `test.csv` dataset from CICIoT2023.

The purpose of these additions is to determine how effectively the trained GAN can identify anomalous IoT network traffic and to provide visual representations of the model's performance.

The code has also been updated to allow the training and testing datasets to be accessed through a shared Google Drive folder. This allows multiple team members to run the same Google Colab notebook without manually uploading the datasets whenever a new runtime session is started.

## Features Added

### Shared Dataset Access

The code mounts Google Drive in Google Colab and accesses the training and testing datasets from a shared folder named `Theia_Data`.

The expected dataset locations are:

```text
/content/drive/MyDrive/Theia_Data/train.csv
/content/drive/MyDrive/Theia_Data/test.csv
