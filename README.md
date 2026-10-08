

## TeachEdge-ECL: Egret Swarm-Optimized Conv-LSTM for Teaching Effectiveness Prediction and Edge-Based Decision Support

TeachEdge-ECL is a reproducible machine-learning framework for **three-class teaching-effectiveness prediction** using an **Egret Swarm Optimization (ESO)-tuned Conv-LSTM network**.

The framework combines:

- leakage-controlled data preprocessing,
- Savitzky-Golay smoothing,
- Principal Component Analysis (PCA),
- Conv1D-based feature extraction,
- Long Short-Term Memory (LSTM) modelling,
- Egret Swarm Optimization for hyperparameter tuning,
- repeated stratified cross-validation,
- statistical significance testing,
- permutation-based feature importance,
- teacher-oriented decision support, and
- TensorFlow Lite deployment on a Raspberry Pi 5.

The predicted teaching-effectiveness levels are:

- **Low**
- **Medium**
- **High**

---

## Overview

TeachEdge-ECL contains two main phases:

### Offline phase

1. Load and clean the Teacher-Student Teaching Effectiveness dataset.
2. Remove non-predictive identifiers.
3. Encode categorical attributes.
4. Perform stratified train/validation/test splitting.
5. Apply min-max normalization.
6. Apply Savitzky-Golay smoothing to classroom indicators.
7. Reduce dimensionality using PCA.
8. Train the Conv-LSTM model.
9. Optimize model hyperparameters using ESO.
10. Evaluate the final model using:
   - held-out testing,
   - repeated 5-fold cross-validation,
   - ablation experiments,
   - optimizer comparisons,
   - baseline comparisons, and
   - corrected statistical tests.
11. Compute permutation importance and classroom-indicator thresholds.
12. Convert the trained model to TensorFlow Lite.

### Online edge phase

The deployed Raspberry Pi system:

1. receives a new classroom record,
2. applies the stored preprocessing pipeline,
3. predicts teaching effectiveness,
4. returns the predicted class,
5. returns the prediction probability, and
6. flags classroom indicators requiring teacher attention.

The system is intended as **decision support**. It does not automatically prescribe teaching interventions.

---

## Framework

```text
Teacher-Student Teaching Effectiveness Dataset
                    |
                    v
        Cleaning and Encoding
                    |
                    v
         Stratified Data Split
          60% / 20% / 20%
                    |
                    v
        Min-Max Normalization
                    |
                    v
       Savitzky-Golay Smoothing
                    |
                    v
        PCA Feature Extraction
          95% Variance Retained
                    |
                    v
        Conv-LSTM Prediction Model
                    |
              +-----+------+
              |            |
              v            |
       ESO Hyperparameter  |
          Optimization     |
              |            |
              +------------+
                    |
                    v
           Final Evaluation
                    |
          +---------+---------+
          |                   |
          v                   v
 Decision Support      TensorFlow Lite
                            Export
                               |
                               v
                       Raspberry Pi 5
