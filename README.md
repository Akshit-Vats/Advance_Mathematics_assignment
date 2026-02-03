# Advance_Mathematics_assignment

# Non-Linear Air Quality Data Transformation & PDF Estimation

This repository contains a data science pipeline designed to perform non-linear transformations on air quality data ($NO_2$ concentrations) and estimate the optimal parameters of a Probability Density Function (PDF) using Machine Learning techniques.

---

## 📖 Project Overview
The objective is to analyze Nitrogen Dioxide ($NO_2$) levels from the India Air Quality dataset, apply a deterministic non-linear shift based on a unique identifier (University Roll Number), and model the resulting distribution using **Non-Linear Least Squares (NLLS)** estimation.

## 🛠 Methodology

### Phase 1: Data Pre-processing
* **Dataset:** Historical India Air Quality Data (1990–2015).
* **Feature Selection:** Focused on $NO_2$ levels as the primary variable ($x$).
* **Cleaning:** * Resolved character encoding issues (UTF-8/ISO-8859-1).
    * Handled missing values (NaN) via **mean imputation** to maintain statistical consistency.

### Phase 2: Non-Linear Transformation
The raw feature $x$ is mapped to a transformed variable $z$ via a sine-based function. This introduces periodic "noise" or distortion to the data distribution.

$$z = T_r(x) = x + a_r \sin(b_r x)$$

**Parameters derived from Roll Number ($r$):**
* $a_r = 0.05 \times (r \pmod 7)$: Adjusts the **amplitude** of the non-linear shift.
* $b_r = 0.3 \times (r \pmod 5 + 1)$: Adjusts the **frequency** of the oscillation.

### Phase 3: Learning the PDF Model
We model the transformed data's density using a Gaussian-style function. The goal is to "learn" the distribution parameters that best fit the observed histogram.

**Model Equation:**
$$\hat{p}(z) = c \cdot e^{-\lambda(z-\mu)^2}$$



**Optimization Parameters:**
* **$\mu$ (Mu):** Represents the central tendency (mean) of the transformed data.
* **$\lambda$ (Lambda):** Represents the precision (inverse of the variance).
* **$c$:** A scaling factor used to align the curve peak with the data's density scale.

**Technique:** The project utilizes **Non-Linear Least Squares (NLLS)** to iteratively minimize the residual sum of squares between the model $\hat{p}(z)$ and the empirical histogram density.

**result:** c = 0.02610997949865131

lambda = 0.0018764106667276252

mu = 19.423434512082626

---

## 🚀 Getting Started

### Prerequisites
* Python 3.x
* NumPy
* Pandas
* Scipy (for `curve_fit` implementation)
* Matplotlib / Seaborn (for visualization)

### Execution
1. **Load Data:** Ensure the `data.csv` is in the root directory.
2. **Set Roll Number:** Update the variable `r` in the script to your specific University Roll Number.
3. **Run Analysis:** Execute the main script to perform the transformation and curve fitting.
