## Causal Inference  
## Author: Qingyu Chen

### Overview
This analysis estimates the causal impact of Grade 1 class‑size reduction on reading achievement using the Early Childhood Longitudinal Study — Kindergarten Cohort (ECLS‑K) 1998 public dataset (NCES) using causal inference methods. The author assess five methods and assess their performance in solving the research question.

---

## Research Question
This study evaluates the impact of **reducing Grade 1 class size** on students' **reading achievement scores** using propensity score-based methods. We dichotomize the treatment variable **A4CLSIZE**:
- **Small class**: ≤ 19 students
- **Regular class**: ≥ 20 students

The outcome variable is **C4RRSCAL** (Grade 1 reading achievement score). Any student with missing treatment or outcome data is excluded from the analysis.

### Covariates Considered
We adjust for the following **pre-treatment covariates**:
- **Student demographics**:
  - Gender (transformed into a three-category variable "gender3")
  - Race (transformed into a six-category variable "race6")
- **Kindergarten academic performance**:
  - Reading scores: Fall (**C1RRSCAL**), Spring (**C2RRSCAL**)
  - Math scores: Fall (**C1R2MSCL**), Spring (**C2R2MSCL**)
- **Grade 1 teacher's experience**: Years of teaching (**B4YRSTC**)

Missing values (-1, -9) are handled using **mean imputation with missing indicators**.

---

## Methodology & Implementation

### 1. Descriptive Analysis
- Compute mean difference in reading scores between treatment and control groups
- Report standard errors, hypothesis test results, and effect size (scaled using control group SD)

### 2. Exploring Potential Confounders
- Compare pre-treatment covariates between treatment and control groups
- Create a balance table using `CreateTableOne()` in R
- Determine which group is relatively advantaged in expected reading achievement

### 3. Propensity Score Estimation & Common Support
- Estimate propensity scores via **logistic regression**
- Decide whether to include **quadratic terms or interactions** for balance adjustment
- Save **logit propensity scores** and report model coefficients
- Visualize distribution of propensity scores using:
  - **Histograms** (e.g., `histbackback()` in R)
  - **Mean and variance comparison** between groups
- Identify **common support region** and remove extreme cases

### 4. Propensity Score Matching (PSM)
- Choose between **ATT (treatment on the treated) vs. ATE (average treatment effect)**
- Apply **1:1 nearest-neighbor matching with replacement** using:
  - `teffects psmatch` in Stata
  - `MatchIt` and `cobalt` in R
- Check **covariate balance** after matching
- Estimate treatment effect and report results (SE, hypothesis test, effect size)

### 5. Propensity Score Stratification
- Divide data into **quintiles** based on logit propensity scores
- Compare within-stratum standardized differences and variance ratios
- Decide if further stratification is needed
- Compute **within-stratum treatment effects** and analyze pattern of effects
- Estimate ATE by **regressing outcome on treatment and strata indicators**

### 6. Inverse Probability of Treatment Weighting (IPTW)
- Estimate ATE using:
  - `teffects ipw` in Stata
  - `PSweight` in R
- Check **covariate balance after weighting**
- Estimate treatment effect and compare with previous methods

### 7. Marginal Mean Weighting through Stratification (MMWS)
- Apply **mmws.exe** for ATE estimation
- Stratify data based on logit propensity scores
- Compare balance pre/post-weighting and estimate treatment effect

### 8. Identification Assumptions & Sensitivity Analysis
- Define the **key identification assumption** for causal inference
- Identify a **potential unmeasured confounder** and assess its impact on results
- Discuss **sensitivity analysis** and conditions for detecting bias due to unmeasured confounders

---

## Software & Tools
- **Stata**: `teffects`, `ivregress`, `tabstat`, `tebalance`
- **R**: `MatchIt`, `cobalt`, `Hmisc`, `dplyr`, `PSweight`
- **mmws.exe**: For stratified marginal mean weighting

---

## File Structure
```
📂 causal-inference-psm
│── 📄 README.md        # This document
│── 📄 assignment2.R    # R script for data preprocessing & analysis
│── 📄 assignment2.do   # Stata script for data preprocessing & analysis
│── 📊 results/         # Output tables & plots
│── 📂 data/            # Data files (ECLS-K public-use data)
│── 📂 figures/         # Graphical visualizations of results
```
---

## Key Findings
- Initial descriptive analysis suggests **a significant difference** in reading achievement between small and regular classes.
- After applying **propensity score methods**, the estimated treatment effect remains significant but varies across methods.
- **Balance diagnostics** indicate that PSM and IPTW methods effectively reduce pre-treatment covariate differences.
- **Sensitivity analysis** highlights the potential influence of unmeasured confounders.

---

## Conclusion
This study employs **propensity score-based methods** to estimate the **causal effect** of class size reduction on Grade 1 reading achievement. The findings suggest that **smaller class sizes** positively impact student performance, though results depend on the estimation method used. Future work should explore **sensitivity analyses** to assess the robustness of these conclusions.

---

## References
- Hong, G. (2015). *Causality in a Social World: Moderation, Mediation and Spill-over*. Wiley.
- Rosenbaum, P. R., & Rubin, D. B. (1983). The central role of the propensity score in observational studies. *Biometrika*, 70(1), 41-55.

---

## Contact
For any questions or collaboration inquiries, please reach out via **GitHub Issues** or email me at **qingyuchen@uchicago.edu**.

---
