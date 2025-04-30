# SE6014project_fingerprinting
IoT Device Fingerprinting via Network-Flow Based Fingerprinting and Learning

Overview

This repository contains a reproduction of the methodology described in "IoT Device Identification via Network-Flow Based Fingerprinting and Learning". We extract payload- and flow-based features from network traffic captures (PCAPs) and train machine learning models to accurately identify IoT devices based solely on their communication patterns.

Features

Entropy Calculation: Compute Shannon entropy of packet payloads to distinguish encrypted vs. plaintext communications.

Flow-Based Features: Extract statistical and temporal features (e.g., packet lengths, inter-arrival times) for each network flow.

Batch PCAP Processing: Support processing one or multiple PCAP files in a single run.

Automated Labeling: Associate each feature vector with the correct device label.

Model Training: Train and evaluate classifiers (e.g., Random Forest, SVM) on the extracted feature set.

Installation

Clone this repository:

git clone https://github.com/yourusername/iot-fingerprinting.git
cd iot-fingerprinting

(Optional) Create a virtual environment:

python3 -m venv venv
source venv/bin/activate


Usage

Place your PCAP files in data/pcaps/.

Launch the Jupyter notebook:

jupyter notebook main.ipynb

Step through the notebook cells to:

Load and preprocess PCAP data

Extract payload and flow features

Generate labeled feature vectors

Train and evaluate classification models

Project Structure

├── data/                  # Folder for input PCAPs and processed datasets
├── notebooks/
│   └── main.ipynb         # Primary analysis and implementation notebook
├── features.py            # Functions for entropy and packet-feature extraction
├── preprocess.py          # PCAP reader and label maker
├── train.py               # Model training and evaluation scripts
├── requirements.txt       # Python dependencies
└── README.md              # Project documentation

Results

Model performance (example):

Random Forest: 95% accuracy on device identification task

SVM: 93% accuracy

Full evaluation metrics and plots are available in the notebook.

References

Ibrahim, et al., "IoT Device Identification via Network-Flow Based Fingerprinting and Learning", IEEE Transactions on Information Forensics and Security, 2020.
