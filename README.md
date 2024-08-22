# EEG Data Processing
This project involves the processing and analysis of EEG data acquired during DBS experiments

## Data Processing Overview
All data processing functions were implemented using Python, leveraging the following packages:
- **NumPy**, **SciPy**, **FINN**

### Filtering and Downsampling
1. **Lowpass Filtering**: The data was first low-pass filtered below 300Hz to remove high-frequency noise.
2. **Downsampling**: Following lowpass filtering, the data was downsampled to 600Hz for efficient processing.

### Noise Reduction
- **Noisy Channel Identification**: The `cleansing.bad_channel_identification` module from FINN was used to detect and reject noisy channels.
- **Bandpass Filtering**: The data was band-pass filtered between 0.53Hz and 50Hz. 
  - The lower limit of 0.53Hz was chosen to reduce movement artifacts such as blinking or head movement.
  - The 50Hz cutoff was used to eliminate high-frequency noise.
- **Notch Filtering**: A notch filter was applied at 50Hz to suppress power line noise.

### Signal Re-referencing and Epoching
- **Re-referencing**: Electrode magnitudes were re-referenced using the common average re-referencing function in FINN.
- **Epoching**: The signal was segmented into 2-second epochs during specific periods:
  - **Rest Period**: 4-26 seconds
  - **Movement Period**: 54-76 seconds

### Beta Power Extraction and Normalization
- **Beta Power Extraction**: Beta power (13-32Hz) was extracted per channel per epoch using Welch's method for spectral density estimation.
- **Normalization**: The extracted beta power was normalized per epoch by dividing it by the total power between 0-300Hz.
