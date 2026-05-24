# Multimodal Pig Behavior Recognition Using Accelerometer and Audio Sensors

This repository contains the source code and notebooks used for pig behavior recognition using wearable accelerometer and audio sensors.

The study evaluates accelerometer-based, audio-based, and multimodal late-fusion approaches for classifying pig behaviors under real production conditions.

## Dataset

The processed dataset is deposited on Zenodo.

Zenodo DOI:

TO_BE_ADDED_AFTER_ZENODO_PUBLICATION

The dataset includes:

- 7,892 processed 5-second accelerometer windows;
- 6,285 synchronized audio-accelerometer samples;
- 6,285 corresponding 5-second WAV audio files;
- 6,285 log-Mel spectrogram files;
- metadata linking accelerometer windows, audio files, and log-Mel files;
- class dictionary and file manifest.

The four behavioral classes are:

| Class | Description |
|---|---|
| lying | Combination of deitadoac and dormindo |
| eating | Feeding behavior |
| walking | Locomotion behavior |
| drinking | Water intake behavior |

## Repository structure

github_repository_v1/
├── configs/
│   └── paths_example.yaml
├── notebooks/
│   ├── 01_multimodal_fusion_accelerometer_audio.ipynb
│   └── 02_dataset_setup_and_data_analysis.ipynb
├── src/
│   ├── data/
│   ├── features/
│   ├── models/
│   ├── fusion/
│   ├── evaluation/
│   └── utils/
├── results/
│   ├── figures/
│   ├── metrics/
│   └── predictions/
└── docs/

## Notebooks

### 01_multimodal_fusion_accelerometer_audio.ipynb

Notebook for multimodal fusion experiments combining accelerometer and audio predictions.

Suggested title: Multimodal Fusion (Accelerometer and Audio).

### 02_dataset_setup_and_data_analysis.ipynb

Notebook for dataset setup, data inspection, preprocessing, and exploratory analysis.

Suggested title: Dataset Setup and Data Analysis.

## Installation

Create a Conda environment:

conda env create -f environment.yml
conda activate pig-multimodal

Or install dependencies using pip:

pip install -r requirements.txt

## Dataset setup

After downloading the dataset from Zenodo, extract it and update:

configs/paths_example.yaml

The dataset uses the column janela as the key for pairing modalities.

This identifier appears in:

1. the accelerometer dataset column janela;
2. WAV filenames using the pattern -jXXXX.wav;
3. log-Mel filenames using the pattern -jXXXX.npy.

## Citation

If you use this code or dataset, please cite the associated manuscript and the Zenodo dataset DOI.

## License

Code license: MIT License.

Dataset license: Creative Commons Attribution 4.0 International (CC BY 4.0), unless otherwise specified in the Zenodo record.
