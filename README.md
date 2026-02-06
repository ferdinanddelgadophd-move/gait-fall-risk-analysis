# Gait Deterioration & Fall Risk Classification

**Can fatigue-related changes in gait during the 6-minute walk test discriminate fallers from non-fallers in older adults?**

![Python](https://img.shields.io/badge/Python-3.10+-3776ab?style=flat&logo=python&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=flat)
![Status](https://img.shields.io/badge/Status-Active-gold?style=flat)

---

## Overview

Most gait-based fall risk assessments rely on **overall averages** — mean gait speed, mean stride length, etc. But what if the important signal isn't in the average, but in **how gait changes over time** as fatigue accumulates?

This project introduces a **quarters-based segmentation** approach to the 6-minute walk test (6MWT). Instead of summarizing each participant's gait with a single number, we divide their gait cycles into four temporal quarters (Q1–Q4) and extract features that capture:

- **Fatigue magnitude** — How much does performance drop from Q1 to Q4?
- **Deterioration rate** — How linear and steep is the decline?
- **Variability changes** — Does gait become more erratic under fatigue?
- **Asymmetry shifts** — Do balance deficits emerge or worsen?

These fatigue-derived features are then tested for their ability to discriminate between older adults who have fallen in the past year and those who have not.

## Dataset

- **N = 60** community-dwelling older adults (23 fallers, 37 non-fallers)
- **6-minute walk test** with wearable IMU sensors (APDM Mobility Lab)
- **Cycle-by-cycle gait data**: 34 metrics × 100–170 cycles per participant
- **Demographics**: age, sex, fall history, medical conditions

## Methods

| Step | Approach |
|------|----------|
| Data parsing | Custom CSV parser for APDM Mobility Lab walk trial exports |
| Segmentation | Divide each participant's gait cycles into 4 equal quarters |
| Feature engineering | Quarter means, SDs, CVs, Q4−Q1 differences, linear slopes |
| Statistical testing | Shapiro-Wilk → Levene's → Student's t / Welch's t / Mann-Whitney U |
| Effect sizes | Hedge's g (parametric) or rank-biserial r (non-parametric) |
| Multiple comparisons | Benjamini-Hochberg FDR correction (α = 0.05) |
| Classification | Logistic regression with Leave-One-Out cross-validation |

## Key Visualizations

The notebook produces:
- **Quarter trajectory plots** showing how fallers vs. non-fallers diverge across the walk
- **Effect size forest plot** ranking the most discriminating features
- **ROC curve** and **confusion matrix** from LOO cross-validated classification

## Repository Structure

```
├── gait_quarters_analysis.ipynb   # Main analysis notebook
├── data/
│   ├── demographics.csv           # Participant demographics & fall status
│   └── walk_trials/               # Raw cycle-by-cycle walk trial CSVs
├── figures/                       # Generated visualizations
├── requirements.txt               # Python dependencies
└── README.md
```

## Quick Start

```bash
git clone https://github.com/ferdinanddelgadophd-move/gait-fall-risk-analysis.git
cd gait-fall-risk-analysis
pip install -r requirements.txt
jupyter notebook gait_quarters_analysis.ipynb
```

## Requirements

```
pandas>=1.5
numpy>=1.23
scipy>=1.10
scikit-learn>=1.2
matplotlib>=3.6
seaborn>=0.12
jupyter>=1.0
```

## Author

**Ferdinand Delgado, PhD**  
Data Scientist & Applied Statistician  
[ferdinanddelgadophd@gmail.com](mailto:ferdinanddelgadophd@gmail.com) · [LinkedIn](https://www.linkedin.com/in/ferdinanddelgado/) · [Portfolio](https://ferdinanddelgadophd-move.github.io)

## License

MIT License — see [LICENSE](LICENSE) for details.
