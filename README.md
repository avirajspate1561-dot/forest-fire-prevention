# Forest Fire Prevention & Probability Modeling (Montesinho Natural Park)

A statistical data analytics capstone project examining wildfire behavior, spatial frequencies, feature distributions, and probability models for 517 recorded fires in Montesinho Natural Park (2000–2003).

---

## Executive Summary

Building on prior spatial and meteorological analysis, this project provides advanced modeling capabilities for local park agencies. By converting burn area into discrete size classifications and testing continuous features against known probability distributions, this analysis equips park authorities with empirical probabilities to optimize early fire detection and resource allocation.

### Key Performance Indicators & Statistics
* **Total Wildfires Analyzed**: 517 records
* **Small Area Fire Rate ($< 0.5\text{ ha}$)**: **49.71%** (257 out of 517 fires)
* **High-Risk Grid Location ($X = 2$)**: **14.12%** of total fires occur in this spatial coordinate
* **Average Temperature at Fire Outbreak**: **18.89°C** ($\bar{x} = 18.89$, $s = 5.81$)

---

## Key Probabilities & Insights

### 1. Spatial Probability Analysis ($X = 2$ Grid Coordinate)
* **$P(X = 2)$**: 0.1412 ($14.12\%$) — 73 total fires occurred in coordinate $X=2$.
* **$P(\text{area} < 0.5\text{ ha})$**: 0.4971 ($49.71\%$) — Nearly half of all fires were contained early as small fires.
* **$P(\text{area} < 0.5 \text{ and } X = 2)$**: 0.0619 ($6.19\%$) — 32 fires were both small and occurred in grid coordinate $X=2$.
* **$P(\text{area} < 0.5 \mid X = 2)$**: 0.4384 ($43.84\%$) — Given a fire occurs at $X=2$, there is a 43.84% conditional probability that it remains small.

> **Independence Test Result**: Since $P(\text{area} < 0.5) \times P(X = 2) = 0.0702 \neq 0.0619$, spatial location $X=2$ and fire size class are **statistically dependent**.

### 2. Feature Distributions & Statistical Modeling
* **Temperature (`temp`)**: Follows an approximate **Normal Distribution** centered around $18.89^\circ\text{C}$.
  * **Empirical Rule Validation**:
    * $\bar{x} \pm 1s$ ($13.08^\circ\text{C}$ to $24.70^\circ\text{C}$): **70.99%** of data (Expected: ~68%)
    * $\bar{x} \pm 2s$ ($7.28^\circ\text{C}$ to $30.70^\circ\text{C}$): **93.81%** of data (Expected: ~95%)
    * $\bar{x} \pm 3s$ ($1.47^\circ\text{C}$ to $36.31^\circ\text{C}$): **100.00%** of data (Expected: ~99.7%)
* **Small Area Indicator (`is_small`)**: Feature engineered in Column `N` (`=IF(M2<0.5, 1, 0)`), forming a **Bernoulli Distribution** with parameter $p \approx 0.4971$.
* **Initial Spread Index (`ISI`)**: Positively skewed distribution (Log-Normal / Gamma behavior).
* **Drought Code (`DC`)**: Strongly left-skewed, bimodal distribution peaking during late dry seasons.

---

## Visualizations

| Distribution Breakdown |
| :---: |
| ![Feature Distributions](visuals/forest_fire_distributions.png) |

---

## Recommendations for Local Agencies

1. **Targeted Spatial Patrols**: Concentrate automated surveillance units on grid $X=2$, which accounts for over 14% of overall ignition events.
2. **Temperature-Triggered Alerts**: Deploy heightened response levels when ambient temperatures cross $24.7^\circ\text{C}$ ($\bar{x} + 1s$), as fire severity risk significantly increases past this threshold.
3. **Feature-Based Risk Scoring**: Integrate binary size classification (`is_small`) into operational dashboards to evaluate early containment efficiency.

---

## Repository Structure

```text
forest-fire-prevention/
├── README.md                                           <- Executive summary & project documentation
├── LICENSE                                             <- Project license (MIT)
├── data/
│   └── C2M2_GradedLab_Forest_fire_prevention_follow_up.xlsx  <- Dataset
├── notebooks/
│   └── forest_fire_analysis.ipynb                      <- Execution notebook
└── visuals/
    └── forest_fire_distributions.png                   <- Generated visual export

Tools & Libraries Used
Python 3.10+: Core analysis language

Pandas & NumPy: Data processing and statistical aggregation

Matplotlib & Seaborn: Charting and visualization generation

SciPy (scipy.stats): Normal distribution modeling

VS Code / Jupyter Notebook: Interactive workspace environment

Git / GitHub: Version control and documentation hosting
