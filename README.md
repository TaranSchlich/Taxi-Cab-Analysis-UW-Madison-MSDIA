[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](
https://colab.research.google.com/github/TaranSchlich/Taxi-Cab-Analysis-UW-Madison-MSDIA/blob/main/GB881_Assignment_4_Schlichtmann_T.ipynb
)

# NYC Taxi Tip Analysis: Yellow vs. Green Cabs
**By: Taran Schlichtmann**
**Date: 09/30/2025**

A data analysis project using **Python**, **Pandas**, **Seaborn**, and **SciPy** to determine whether the **average tip** differs between **yellow** and **green** New York City taxis via a **two-sample t-test**.

> **Business context**: As a data analyst at a taxi company, you are tasked with assessing whether cab color (yellow vs. green) is associated with differences in tipping behavior. This repository replicates the analysis, visualizations, and statistical tests to support a data-driven conclusion.

---

## Repository Contents

- `gb881_assignment_4_schlichtmann_t.py` — Colab-exported Python script containing the analysis, visualizations, and inferential tests.  
- `README.md` — Project documentation (this file).

---

## Tech Stack

- Python 3.x
- Pandas — data loading/manipulation
- Seaborn — visualization
- SciPy — statistical tests

---

## Dataset

- **Source**: `https://bit.ly/taxi-samples` — sample NYC taxi trips with columns including `color` and `tip`.
- Loaded directly in the script as a pandas DataFrame:

```python
Taxi_Samples_df = pd.read_csv('https://bit.ly/taxi-samples')
```

---

## Objective & Hypotheses

**Goal**: Test if the mean tip differs between yellow and green cabs.

- **Null (H₀)**: μ_yellow = μ_green (no difference in mean tips)
- **Alternative (H₁)**: μ_yellow ≠ μ_green (difference in mean tips)

**Test**: Two-sample t-test (independent samples)

---

## 🛠️ Methodology

1. **Load & Inspect Data**  
   - Check shape, schema, preview rows (`.shape`, `.info()`, `.head()`).
2. **Segment by Cab Color**  
   - Create `Yellow_Cab_df` and `Green_Cab_df` from `Taxi_Samples_df[color]`.
3. **Explore Tip Distributions**  
   - Seaborn histograms via `sns.displot(..., x='tip')` for both groups.
4. **Assess Normality**  
   - D’Agostino–Pearson test: `stats.normaltest(series)`.
5. **Assess Equal Variances**  
   - Bartlett’s test: `stats.bartlett(yellow_tips, green_tips)`.
6. **Inferential Test**  
   - Independent two-sample t-test: `stats.ttest_ind(yellow_tips, green_tips)`.

---

## ✅ Results (from the provided script)

- **Normality**: Yellow cab tips are approximately normal (**p = 0.162**); green cab tips are **not normal (p < 0.05)**.  
- **Equal variances**: Bartlett’s test indicates **no significant difference in variances (p = 0.38)**.  
- **Two-sample t-test**: **p = 0.96** → fail to reject H₀; **no evidence** of a difference in mean tips by cab color.

> **Conclusion**: Cab color (yellow vs. green) **does not significantly affect** tip amounts in this sample.

---

## Visualizations

- Histograms (`sns.displot`) for yellow and green tips to gauge distribution shape and potential outliers.

---

## How to Run

### 1) Google Colab (recommended)
- Open the original notebook link: https://colab.research.google.com/drive/1VNQA_5DHc4m6EBpihovEnSdPMT80T3S6
- Run cells top-to-bottom.

### 2) Local Python environment
```bash
# Create & activate a virtual environment
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\\Scripts\\activate

# Install dependencies
pip install pandas seaborn scipy matplotlib

# Run the analysis script
python gb881_assignment_4_schlichtmann_t.py
```

> The script uses an external CSV via HTTPS; ensure your environment has internet access.

---

## Statistical Notes

- **Normality**: D’Agostino–Pearson test checks skewness & kurtosis jointly. When normality is violated (as in green tips), consider robust alternatives (e.g., Mann–Whitney U) or t-tests with caution—especially with large samples (where t-test is fairly robust).
- **Equal variances**: Bartlett’s test is sensitive to non-normality; Levene’s test is a more robust alternative. If variances differ, use `ttest_ind(..., equal_var=False)` (Welch’s t-test).
- **Effect size**: You can add Cohen’s _d_ to quantify magnitude even when p is non-significant.

---

## Project Structure

```
.
├── gb881_assignment_4_schlichtmann_t.py   # Core analysis
└── README.md                               # Documentation
```

---

## Reproducibility Checklist

- Seed setting not required (no random processes used).  
- External data URL (`bit.ly/taxi-samples`) must be reachable.  
- Python packages: `pandas`, `seaborn`, `scipy`, `matplotlib`.

---

## 📄 License

This project is for educational purposes.


