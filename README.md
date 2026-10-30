# Human Activity Recognition using an HMM

Formative 2 · Larissa Iriza

A bespoke Hidden Markov Model created using NumPy to infer human activity (standing, walking, jumping and static) from smartphone accelerometer and gyroscope data. This can help the elderly live independently at low cost using their existing smartphone.

## Folder Structure:
```

data/
train/
52 CSV files of cleaned labelled data (13 files per activity, approx. 10s of data)
test/
2 test files containing all 4 activities (approx. 10s of data)
figures/
Figures and results table obtained from the notebook
HMM_Activity_Recognition.ipynb
Full pipeline from data to feature extraction to HMM to evaluation
report.pdf
4-5 page report
```

## Data

iPhone 13 (iOS 18.5). Sensor Logger App.
Sampling Frequency: 100Hz. All sensors sampled onto precise 100Hz grid.
Sensors: Accelerometer (x, y, z), Gyroscope (x, y, z), Un-calibrated Accelerometer (gravity).
Each CSV contains timestamp_ns, seconds, sensor data and label.

Test File | Activities (~10s per activity)
--- | ---
test1 | Walk -> Jump -> Stand -> Static
test2 | Static -> Stand -> Jump -> Walk

## Method

2 Second sliding window (200 samples). 50% overlap.
Extracted 6 features. 3 from the time domain (standard deviation of acceleration magnitude, mean and standard deviation of gyroscope). 3 from the frequency domain (FFT dominant frequency, acceleration and gyroscope spectral energy).
Log transformation and Z-score normalisation applied. Only training data used for normalisation.
4 state HMM with diagonal Gaussian emission probabilities. Training was done using Baum-Welch algorithm. Algorithm converged once increase in likelihood < 1e-4. Decoding was done using Viterbi.

## Results (Unseen Data)

Activity | Samples | Sensitivity | Specificity
--- | --- | --- | ---
Stand | 20 | 0.80 | 0.85
Walk | 19 | 1.00 | 0.85
Jump | 20 | 1.00 | 1.00
Static | 20 | 0.30 | 1.00

Overall accuracy of 77.2%. See report for full discussion.

## To Run

1. Open HMM_Activity_Recognition.ipynb in Google Colab.
2. Run all cells. Upload recordings.zip (raw data from Sensor Logger).

## Data Collection Videos

Stand: https://drive.google.com/file/d/1UKD52YU7C0L3poasf7u_e04lLHbmcW3m/view?usp=sharing
Walk: https://drive.google.com/file/d/1ZHkZcLfCg2Lf940V_0hk3iIpSlcFqOZX/view?usp=sharing
Jump: https://drive.google.com/file/d/1FdOV-0T179y4UlS8zeaEBTlB2ccJeBir/view?usp=sharing
still: https://drive.google.com/file/d/16zcTTNA5F_wVan2hEIKBkJTVpaWfMe8r/view?usp=sharing
