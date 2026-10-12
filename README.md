# Multimodal Pig Behavior Recognition Using Accelerometer and Audio Sensors

This repository provides a Jupyter notebook documenting experiments for pig behavior recognition using wearable triaxial accelerometer and audio sensors under commercial production conditions.

The notebook evaluates accelerometer-based, audio-based, and multimodal late-fusion approaches for four behavioral classes: lying, eating, walking, and drinking.

## Dataset

The processed dataset is available on Zenodo:

**DOI:** [10.5281/zenodo.22900705](https://doi.org/10.5281/zenodo.22900705)

The dataset includes:

- 7,892 processed 5-second accelerometer windows;
- 6,285 synchronized audio–accelerometer samples;
- 6,285 corresponding 5-second WAV audio files;
- 6,285 log-Mel spectrogram files;
- metadata linking accelerometer windows, audio files, and spectrograms;
- a class dictionary and file manifest.

| Class | Description |
|---|---|
| lying | Awake lying and sleeping, combining the original labels `deitadoac` and `dormindo` |
| eating | Feeding behavior |
| walking | Walking behavior |
| drinking | Water intake behavior |

Dataset files are downloaded separately and are not included in this repository.

## Notebook

**`multimodal_fusion_accelerometer_audio.ipynb`**

The notebook contains the experimental code, explanatory Markdown cells, and saved outputs. It covers:

- Dataset inspection and class distributions.
- Accelerometer feature extraction and MDRF-CS evaluation.
- An AD-BL-SMOTE plus MLP reference baseline.
- An embedded-oriented Random Forest comparison.
- LMAAN training and an audio CNN baseline without SE blocks.
- AST, EfficientAT MN40, and PANNs CNN14 experiments.
- Nested out-of-fold predictions for fusion-weight estimation.
- Late-fusion strategies and statistical comparisons.

The notebook retains both fully nested fusion experiments and experiments using shortcut audio-weight estimation. These configurations are identified in the accompanying explanations.

## Requirements

A Python environment with Jupyter Notebook or JupyterLab is required. Dependencies used across the experiments include:

- NumPy, pandas, and SciPy;
- scikit-learn and joblib;
- Matplotlib and seaborn;
- PyTorch;
- Transformers;
- librosa, soundfile, and torchlibrosa.

The EfficientAT and PANNs experiments also use external model repositories and pretrained checkpoints, as specified in their respective cells. Downloading these resources requires an internet connection.

A CUDA-capable GPU is recommended for neural-network training.

## Dataset Setup

1. Download and extract the dataset from Zenodo.
2. Open the notebook.
3. Update the local paths in the cells you intend to run, including `BASE`, `CSV`, `LOGMEL`, and `WAVDIR`, where applicable.
4. Run the preparation cells required by the selected experiment.

The notebook retains paths from the original Windows machines. It does not use a centralized configuration file, so paths must be checked in each relevant cell.

The main accelerometer file is:

`dataset_treinamento_suinos.csv`

The `janela` column identifies each window and is used to pair modalities.

Several experimental cells expect audio and spectrogram filenames to contain only the numeric window identifier, for example:

- `6006.wav`
- `6006.npy`

If the downloaded files include prefixes, consult the dataset metadata and file manifest to establish the correspondence and adapt the filenames or loading code before running those cells.

## Evaluation Protocol

Experiments use leave-one-animal-out (LOAO) validation, holding out one animal for testing in each outer fold.

Accelerometer-only experiments may use all 7,892 accelerometer windows. Audio and paired multimodal experiments use the corresponding synchronized subset of 6,285 windows.

Two forms of performance reporting are distinguished:

- **Pooled metrics:** calculated after combining held-out predictions across animals.
- **Per-animal metrics:** calculated separately for each animal and summarized as mean ± standard deviation.

These summaries are not interchangeable. Paired statistical comparisons use animal-level scores.

## Saved Outputs and Execution

Saved outputs document previous experimental runs and can be inspected without rerunning the notebook.

Training cells can be computationally expensive, especially those generating nested out-of-fold predictions. Run the relevant experiment sections and their prerequisites rather than executing the entire notebook indiscriminately.

Local datasets, dependency versions, hardware, and random seeds may affect reproduced results. Some cells save files with fixed names, which may overwrite outputs from earlier runs.

## Citation

If you use this code or dataset, please cite the associated manuscript and the Zenodo dataset:

[https://doi.org/10.5281/zenodo.22900705](https://doi.org/10.5281/zenodo.22900705)

## License

The code is released under the MIT License.

The dataset is distributed under Creative Commons Attribution 4.0 International (CC BY 4.0), subject to the terms specified in the Zenodo record.

External libraries, model repositories, and pretrained checkpoints remain subject to their respective licenses.
