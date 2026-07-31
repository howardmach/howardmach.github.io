---
layout: default
title: Penguin Regression Analysis
---

# 🐧 Analysis of Palmer Archipelago Penguins: Prediction Model on Flipper Length

**Authors:** Howard Mach, Andy Chandler, Thompson Pham  
**Tools & Technologies:** R, Multiple Linear Regression, Residual Analysis, Diagnostics, ANOVA  
**Data Source:** Palmer Station Antarctica LTER / Kaggle (Gorman et al., 2014)[cite: 3]

---

## 📌 Executive Summary

This study constructs a predictive model to estimate penguin flipper length ($\text{mm}$) based on morphological features and stable isotope signatures ($^{13}\text{C}$ and $^{15}\text{N}$) collected at Palmer Station, Antarctica[cite: 3]. Through backward selection, residual diagnostics, and Box-Cox transformation testing, a reduced 4-predictor multiple linear regression model was built, achieving an **Adjusted $R^2$ of 0.8527**[cite: 3].

---

## 📊 Dataset & Variable Overview

The dataset covers **344 observations** across 3 species (*Adélie*, *Chinstrap*, and *Gentoo*) from three islands in the Palmer Archipelago[cite: 3].

* **Response Variable ($Y$):** Flipper Length ($\text{mm}$)[cite: 3]
* **Predictor Variables ($X$):**
  * `body_mass_g`: Body mass in grams[cite: 3]
  * `culmen_length_mm`: Length of the upper ridge of the bill ($\text{mm}$)[cite: 3]
  * `culmen_depth_mm`: Depth of the upper ridge of the bill ($\text{mm}$)[cite: 3]
  * `Delta 13 C (o/oo)`: Carbon isotope ratio ($^{13}\text{C}$), reflective of foraging habits and diet[cite: 3]
  * `Delta 15 N (o/oo)`: Nitrogen isotope ratio ($^{15}\text{N}$)[cite: 3]
  * `sex`, `species`, `island`, `clutch_completion`[cite: 3]

---

## 🛠️ Methodology & Modeling Steps

### 1. Model Selection & Fitting
Starting with a full model incorporating physical traits and isotopic markers, backward variable selection was conducted[cite: 3]:

* **Full Model:** Included $^{15}\text{N}$, $^{13}\text{C}$, culmen depth, culmen length, and body mass ($R^2_{\text{adj}} = 0.8448$)[cite: 3]. Isotope $^{15}\text{N}$ was statistically insignificant ($p = 0.513$) and subsequently removed[cite: 3].
* **Reduced Model:** Dropping $^{15}\text{N}$ improved model parsimony and boosted accuracy ($R^2_{\text{adj}} = 0.8527$, $F = 467$, $p < 2.2 \times 10^{-16}$)[cite: 3].
* **Model Comparison (ANOVA):** An ANOVA test between full and reduced models yielded $p = 0.645$, confirming the reduced model as the superior fit[cite: 3].
* **Multicollinearity Check:** All Variance Inflation Factor (VIF) values remained well below the critical threshold of 10 (highest VIF was 2.60 for `body_mass_g`), confirming no severe collinearity[cite: 3].

### 2. Residual Diagnostics & Outlier Removal
* Standardized, Studentized, and R-Student residual plots revealed an extreme outlier at **Observation 157** (falling beyond the $\pm 3$ threshold)[cite: 3].
* Removing Observation 157 brought all remaining residuals within the $[-3, 3]$ bounds, satisfying key regression assumptions[cite: 3].

### 3. Normality & Transformation Verification
* Residual Q-Q plots and density histograms showed strong alignment with normal error distributions[cite: 3].
* A **Box-Cox transformation test** returned an optimal $\lambda = 1.51$[cite: 3]. Because $\lambda = 1.0$ falls comfortably within the $95\%$ confidence interval, **no non-linear transformation was necessary**[cite: 3].

---

## 📐 Final Fitted Regression Equation

$$Y_{\text{flipper}} = 74.9158 - 2.8069(\Delta^{13}\text{C}) - 1.2943(\text{Culmen Depth}) + 0.8637(\text{Culmen Length}) + 0.0091(\text{Body Mass})$$[cite: 3]

---

## 📈 Key Findings & Insights

1. **Body Mass & Bill Dimensions:** Body mass ($p < 2 \times 10^{-16}$) and culmen length ($p < 2 \times 10^{-16}$) exhibit strong positive associations with flipper length[cite: 3].
2. **Isotopic Signatures:** Carbon isotope ratios ($\Delta^{13}\text{C}$) showed significant negative predictive value ($p = 7.29 \times 10^{-8}$), linking foraging zones/dietary compositions directly to physical penguin morphology[cite: 3].
3. **Species Clustering:** Exploratory analysis confirmed distinct physical clustering—*Gentoo* penguins consistently exhibited higher body mass and longer flipper lengths compared to *Adélie* and *Chinstrap* species[cite: 3].

---

## 📄 Full Project Report & Appendix

<iframe src="../assets/pdfs/penguins_regression.pdf" width="100%" height="700px" style="border: none;">
    This browser does not support inline PDFs. Please download the file below.
</iframe>

<p align="center">
  <a href="../assets/pdfs/penguins_regression.pdf" target="_blank" style="padding: 10px 20px; background-color: #0366d6; color: white; border-radius: 6px; text-decoration: none; font-weight: bold;">
    📥 Download Full PDF Report
  </a>
</p>
