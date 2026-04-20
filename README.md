# A/B Test Analysis: Marketing Ad Campaign

**Author:** Ernesto Acosta Berg 

**Tools:** Python · Pandas · SciPy · Matplotlib · Seaborn  
**Dataset:** [Marketing A/B Testing — Kaggle](https://www.kaggle.com/datasets/faviovaz/marketing-ab-testing)

\---

## Overview

A company ran an A/B test on **588,101 users** to determine whether showing a paid advertisement increases conversions compared to a neutral public service announcement (PSA) control.

This project performs the full analysis: statistical hypothesis testing, effect sizing, confidence intervals, and segmentation to find the best-performing user segments.

\---

## Key Results

|Metric|PSA (Control)|Ad (Treatment)|
|-|-|-|
|Users|23,524|564,577|
|Conversions|420|14,423|
|Conversion Rate|1.785%|2.555%|
|95% CI|1.624% – 1.963%|2.514% – 2.596%|
|**Relative Lift**|—|**+43.1%**|

**Statistical test:** Chi-square (χ² = 54.0, p < 0.001) → **H₀ rejected. The ad significantly increases conversions.**

\---

## Segmentation Findings

|Dimension|Best Segment|Conversion Rate|
|-|-|-|
|Day of week|Monday|3.32%|
|Hour of day|16:00|3.09%|
|Ad exposure|120+ ads seen|16.9%|

* **Monday is the strongest day** — 56% higher than Saturday (worst day at 2.13%).
* **Peak hour is 16:00** — late afternoon outperforms early morning and late night.
* **Dose-response effect:** Users exposed to more ads convert at dramatically higher rates. Note: this is correlational — high-exposure users may already be higher-intent.

\---

## Visualizations

![Conversion Rate](outputs/01_conversion_rate.png)
![Conversion by Day](outputs/02_conversion_by_day.png)
![Conversion by Hour](outputs/03_conversion_by_hour.png)
![Conversion by Exposure](outputs/04_conversion_by_exposure.png)
![Heatmap Day x Hour](outputs/05_heatmap_day_hour.png)

\---

## Project Structure

```
ab-testing-marketing/
├── data/
│   └── marketing\_AB.csv
├── notebooks/
│   └── ab\_test\_analysis.ipynb
├── outputs/
│   ├── 01\_conversion\_rate.png
│   ├── 02\_conversion\_by\_day.png
│   ├── 03\_conversion\_by\_hour.png
│   ├── 04\_conversion\_by\_exposure.png
│   └── 05\_heatmap\_day\_hour.png
├── README.md
└── requirements.txt
```

\---

## How to Run

```bash
# 1. Clone the repo
git clone https://github.com/ebctrl/ab-testing-marketing.git
cd ab-testing-marketing

# 2. Install dependencies
pip install -r requirements.txt

# 3. Open the notebook
jupyter notebook notebooks/ab\_test\_analysis.ipynb
```

\---

## Methods

**Chi-Square Test of Independence** — tests whether group membership (ad vs PSA) and conversion (yes/no) are independent. Chosen because both variables are categorical and sample sizes are large.

**Wilson Score Confidence Intervals** — more accurate than normal approximation for proportions, especially when rates are low (< 5%).

**Segmentation** — conversion rates broken down by day, hour, and ad exposure bucket to identify actionable targeting patterns.

\---

## Caveats

* The PSA group is only 4% of the total dataset (imbalanced groups). The sample size is still sufficient for a valid test, but worth noting.
* Dose-response analysis is **correlational, not causal**. Users who see 120+ ads may be power users or repeat visitors who would have converted anyway.
* No user demographic data is available, which limits further segmentation.

