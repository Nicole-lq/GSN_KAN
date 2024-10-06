<div align="center">

# Kicking the KAN with Photometric Redshifts (Photo-zs)

<p>
  <img src="images/KAN.png" width="300">
</p>

</div>

## Motivation

Kolmogorov-Arnold Networks (KANs) introduce a novel neural network architecture by replacing fixed activation functions on nodes with **learnable activation functions** on the edges between nodes. This approach offers:

- **Enhanced performance** relative to traditional neural networks (NNs).
- **Interpretability**: KAN models can be converted into analytic expressions, similar to symbolic regression (SR).

This project explores KANs for **photometric redshift extraction**, a critical challenge in astronomy, where the goal is to infer the redshift of astronomical objects using only broad-band photometry. The complex and non-linear mapping between observed photometric data and redshift may benefit from the flexibility and interpretability that KANs offer.


## Problem Overview: Photometric Redshift Extraction

In astronomy, **photometric redshift extraction** involves predicting the redshift of objects using only broad-band photometric data. The mapping from photometric data to redshift is highly complex and non-linear. Traditional approaches such as Multi-Layer Perceptrons (MLPs) can struggle with this complexity, so we propose KANs as a potential improvement.

The key question: **Are KANs more efficient, interpretable, and accurate than traditional MLPs?**


## Main Goal

The main objective of this project is to evaluate the practicality and utility of KANs for **photometric redshift prediction** and compare their performance against:

- **Multi-Layer Perceptron (MLP)**
- **Symbolic Regression (SR)**
- **Kolmogorov-Arnold Networks (KAN)**

Performance is measured using two key metrics: **R² (coefficient of determination)** and **Mean Squared Error (MSE)**.


## Data Source

The data used for this project comes from **Sloan Digital Sky Server V (SDSS DR18)**.

### Key Data Insights:

- A high frequency of data is observed for **small redshifts (0 ≤ z ≤ 0.2)**, indicating an unbalanced sample.
- The total observation count from **SDSS-18**: 19,909.


## Model Frameworks

### 1. **MLP Model**

- **Input**: 4 features (u, g, r, i)
- **Hidden Layers**: 
  - 1st layer: 64 neurons
  - 2nd layer: 32 neurons
- **Output**: 1 neuron (prediction)
- **Activation Function**: ReLU (hidden layers)
- **Training**:
  - Loss function: Mean Squared Error (MSE)
  - Optimizer: Adam (learning rate: 0.001)
  - Hardware: GPU (if available)

- **Results**:
  - R²: 0.439
  - Best MSE: 0.0024

<p align="left">
  <img src="images/MLP_r.png" width="1000">
</p>
  

### 2. **Symbolic Regression (SR)**

- **Goal**: Convert a neural network into an interpretable analytic equation.
- **Tool**: PySR (symbolic regression for Python/Julia)
  
- Data Handling:
  - Redshift binning to mitigate unbalanced data
  - Uniform normalization of features to [-1, 1]

- **Results**:
  - Non-Uniform Data:
    - R²: 0.410
    - MSE Best: 0.0022
  - Uniform Data:
    - R²: 0.576
    - MSE Best: 0.0130

<p align="left">
  <img src="images/SR_r.png" width="1000">
</p>
  
### 3. **KAN Model**

- **Structure**:
  - Width: [4, 2, 1] (input, hidden, output layers)
  - Grid size: 3, k-value: 3
  - Trainable parameters: 120
- **Training**:
  - Loss function: Mean Squared Error (MSE)
  - Optimizer: AdamW (learning rate: 0.001)
  - Hardware: GPU (if available)

- **Results**:
  - R²: 0.333
  - Best MSE: 0.0025

<p align="left">
  <img src="images/KAN_r.png" width="1000">
</p>


## Summary Statistics

| Model  | R²   | Best MSE  |
|--------|------|-----------|
| MLP    | 0.439| 0.0024    |
| SR     | 0.410| 0.0022    |
| KAN    | 0.333| 0.0025    |

KAN, SR, and MLP models achieve **comparable performance** on average. All models reach test MSE values smaller than 10⁻².


## Future Directions

This work opens up multiple avenues for future exploration:

- Investigate deeper and wider KAN architectures.
- Optimize hyperparameters.
- Address the challenges posed by unbalanced data.
- Explore **multi-KAN models** to improve generalization.
- Incorporate higher-quality data from SDSS DR18 and beyond.
