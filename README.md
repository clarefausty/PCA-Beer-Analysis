# README — NIR Beer Spectroscopy PCA Analysis

## Overview

This project applies **Principal Component Analysis (PCA)** to Near-Infrared (NIR) spectroscopy data of beer samples in order to differentiate between **crafted beers** and **industrial beers**. The analysis is performed in MATLAB using **Singular Value Decomposition (SVD)**.

The workflow includes:

* spectral visualization
* data pre-processing
* PCA computation
* scores and loadings interpretation
* projection of unknown samples
* Q residual diagnostics

The project demonstrates the application of **chemometrics** for spectral classification and exploratory multivariate analysis. 

---

# Dataset

The dataset contains:

* 40 NIR beer spectra
* 3112 spectral variables (wavenumbers)
* spectral range approximately:

  * 4000–9500 cm⁻¹

Sample grouping:

* Samples 1–20 → Crafted beers
* Samples 21–40 → Industrial beers

An additional unknown spectrum (`xte`) is included for classification testing. 

---

# Methodology

## 1. Raw Spectra Visualization

The original NIR spectra are plotted to inspect the spectral profiles before preprocessing.

Main MATLAB functions used:

```matlab
plot()
xlabel()
ylabel()
title()
```

---

## 2. Data Pre-processing

The following preprocessing steps were applied:

### Mean-centering

The mean spectrum is subtracted from each sample:

```matlab
xc = x - xm;
```

Purpose:

* remove dominant average spectral contribution
* focus analysis on variations between samples

### Scatter Correction

Scatter correction was previously applied to reduce baseline and scattering effects. 

---

## 3. Principal Component Analysis (PCA)

PCA was computed using economy SVD:

```matlab
[U,S,V] = svd(xc,'econ');
```

Where:

* `T = U*S` → scores matrix
* `V` → loading matrix
* diagonal values of `S²` → eigenvalues

The PCA reduces the dimensionality of the spectral dataset while preserving most of the variance. 

---

# Results & Interpretation

## Scores Plots

The PCA scores plots were used to observe clustering patterns between beer types.

### PC1 vs PC2

* dominated mainly by water absorption information
* little visible separation between classes

### PC3

PC3 revealed subtle but meaningful separation:

* industrial beers → mostly positive PC3 scores
* crafted beers → mostly negative PC3 scores

This indicates chemically distinguishable spectral features between the two groups. 

---

## Loadings Analysis

The PC3 loading profile showed:

* spectral contributions around:

  * 6500 cm⁻¹
  * 5000–4000 cm⁻¹

These regions are associated with:

* water hydrogen bonding
* dissolved solutes
* subtle compositional differences between beer categories

---

# Projection of Unknown Sample

The unknown sample (`xte`) was projected into the existing PCA model without recalculating the SVD:

```matlab
xtec = xte - xm;
ttec = xtec * V;
```

The projected PC3 score placed the unknown sample closer to the industrial beer cluster. 

---

# Q Residual Analysis

Q residuals were calculated to evaluate model fit:

```matlab
Q = sum(res.^2,2);
```

Interpretation:

* low Q residual → sample fits the PCA model well
* high Q residual → potential outlier

The unknown sample showed a Q residual comparable to the training samples, confirming that it belongs within the model space. 

---

# Skills Demonstrated

This project demonstrates practical experience in:

* Chemometrics
* PCA
* SVD
* MATLAB programming
* Spectral preprocessing
* Multivariate analysis
* NIR spectroscopy
* Data visualization
* Classification analysis

---

# Future Improvements

Potential extensions include:

* Partial Least Squares Discriminant Analysis (PLS-DA)
* Linear Discriminant Analysis (LDA)
* Cross-validation
* Larger datasets
* Advanced preprocessing techniques
* Feature selection methods

These approaches could improve classification robustness and predictive performance. 

---

# Author
CHINWENDU FAUSTINA ACHILONU
Chemometrics Laboratory Project
MSc Advanced Spectroscopy in Chemistry
University of Lille
