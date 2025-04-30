# IoT Device Fingerprinting via Network-Flow Based Fingerprinting and Learning

## Problem Motivation

IoT ecosystems consist of highly diverse devices with varying capabilities and security mechanisms. Traditional cryptographic authentication can be resource-intensive, often exceeding the memory and processing constraints of many IoT devices. Consequently, these methods struggle to provide universal device identification and authentication across heterogeneous networks. Lightweight, behavior-based fingerprinting offers a scalable alternative to prevent unauthorized access and enhance overall network security. 

## Technical Approach

This project implements a passive fingerprinting methodology inspired by the referenced paper. Key aspects include:

- **Network-Flow Data:** Capturing sequences of packets (PCAP files) without active probing.
- **Feature Extraction:** Deriving both header- and payload-based features to characterize device behavior.
- **Behavioral Fingerprints:** Constructing unique binary vectors and statistical summaries that serve as device fingerprints. 

## Dataset

The original dataset comprises multiple PCAP files exceeding 4 GB each, containing comprehensive network flow records of IoT devices. These captures can be inspected using tools like Wireshark for verification and exploratory analysis. citeturn0file0

## Feature Extraction

A total of 20 features are extracted per packet:

- **17 Binary Flags:** Indicate presence of specific protocols or header characteristics (e.g., TCP, UDP, DNS).
- **3 Continuous Metrics:** Include packet length statistics, inter-arrival times, and payload entropy.  

## Fingerprint Generation

Post-extraction, feature vectors across all PCAPs are aggregated into a CSV dataset containing over 1 million rows. Due to memory limitations when opening large CSVs, downstream processing must be optimized or filtered before loading. 

## Data Filtering

To manage resource constraints and focus on meaningful patterns, device entries with fewer than 100 occurrences are removed. This threshold balances the dataset size against the need to capture sufficiently representative behavior samples. 

## Model Training

Using the filtered dataset, a Random Forest classifier is trained to identify device types. While the original study evaluated multiple algorithms (KNN, SVM, Decision Trees), Random Forest yielded the best performance in this reproduction. 

## Results and Observations

- **Initial Run:** Directly using the folder-structured labels led to overly granular classification and ~50% accuracy.
- **Paper-Aligned Labels:** Consolidating status and behavior labels per the original methodology improved accuracy to ~90%. This is satisfactory for our replication, though the paper reports up to 99.9% accuracy. citeturn0file0

## Project Structure

```
├── data/                  # Raw PCAP captures and filtered CSVs
├── features.py            # Header and payload feature extraction logic
├── preprocess.py          # Data aggregation and filtering utilities
├── train.py               # Training and evaluation scripts for Random Forest
├── notebooks/             # Jupyter analyses and exploratory code
│   └── main.ipynb         # Step-by-step implementation and results
├── requirements.txt       # Python dependencies
└── README.md              # Project documentation
```

## Installation

```
git clone https://github.com/yourusername/iot-fingerprinting.git
cd iot-fingerprinting
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

## Usage

1. Place PCAP files in `data/pcaps/`.

2. Run preprocessing and feature extraction:

   ```
   python preprocess.py --pcap-dir data/pcaps --output data/features.csv
   ```

3. Train and evaluate the model:

   ```
   python train.py --data data/features_filtered.csv
   ```

4. Review results in `notebooks/main.ipynb`.

