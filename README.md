# Causal Inference: The Effect of Class Size on Test Scores

**Author:** Qingyu Chen  
**Date:** 2025‑02‑28  

---

## Overview

This repository investigates how **Grade 1 class size** impacts **reading achievement**, using data from the [Early Childhood Longitudinal Study – Kindergarten Cohort (ECLS‑K) 1998](https://nces.ed.gov/ecls/Kindergarten.asp). Specifically, it compares **small classes (≤19 students)** with **regular classes (≥20 students)** to determine whether smaller class sizes lead to higher reading scores.

---

## Files

- **Causal Inference_ the Effect of Class Size on Test Scores.Rmd**  
  Main R Markdown file containing data cleaning, analysis code, and commentary on five causal inference methods.
- **Causal Inference_ the Effect of Class Size on Test Scores.pdf**  
  Rendered output (knitted PDF) from the R Markdown file.
- **ECLSK98_class_size.dta**  
  Public‑use dataset (a subset of ECLS‑K 1998).
- **README.md**  
  This file.

---

## Research Question

Does reducing Grade 1 class size significantly improve students’ reading achievement scores?  
- **Treatment Variable:** `A4CLSIZE` (class size; small vs. regular)  
- **Outcome Variable:** `C4RRSCAL` (reading score)  

Pre-treatment covariates include prior academic performance and demographic factors, helping to control for selection bias.

---

## Methods

We apply five causal inference techniques to estimate the treatment effect:

1. **Propensity Score Matching (PSM)**  
   - Matches treated and control students with similar observed covariates.
2. **Inverse Probability of Treatment Weighting (IPTW)**  
   - Weights observations by the inverse of their propensity to receive treatment.
3. **Marginal Mean Weighting through Stratification (MMWS)**  
   - Stratifies the sample by propensity score and applies weighting within each stratum.
4. **Instrumental Variables (IV)**  
   - Uses an external instrument to address potential unobserved confounding.
5. **Difference‑in‑Differences (DID)**  
   - Compares pre- and post-intervention outcomes assuming parallel trends.

Each method relies on different assumptions:
- **PSM, IPTW, MMWS:** Assume no unobserved confounding after controlling for observed covariates.
- **IV:** Requires a valid instrument that affects class size but not reading outcomes directly.
- **DID:** Assumes that, in the absence of the intervention, both groups would have followed parallel trends.

---

## How to Replicate

1. **Install Required Packages:**  
   Open R and run:
   ```r
   install.packages(c("haven", "dplyr", "Hmisc", "MatchIt", "ggplot2", 
                      "tableone", "cobalt", "twang", "PSweight", "knitr", 
                      "broom", "kableExtra", "AER", "plm", "systemfit", 
                      "tidyverse", "fixest"))

For questions or further discussion, please open an issue on GitHub or email me at:
qingyuchen@uchicago.edu
