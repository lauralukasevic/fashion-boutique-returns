# Fashion Boutique Returns: What Drives Returns and Markdowns?

I used the **CRISP-DM** process to study product returns and markdowns in a fashion boutique dataset.

## Project question

**Topic:** Understanding which product and pricing factors are linked to returns, to support markdown and return-reduction decisions.

**Research questions**

1. Which **categories, brands, sizes or seasons** have the highest return rate?
2. Do **heavily discounted items** get returned more often?
3. Do **return reasons** differ by category?
4. Does **high stock** go with deeper markdowns?

## Key findings

I analysed **2,176 products**, of which **320 (14.7%) were returned** and **878 (40.3%) were marked down**.

| **Question** | **Result** | **Evidence** |
| --- | --- | --- |
| Product characteristics | Weak effects only. Summer items and Ann Taylor have higher return rates. Category and size have no effect. | Chi-square: category p = 0.798, brand p = 0.178, season p = 0.049, size p = 0.642. Logistic regression: pseudo R² = 0.011, AUC = 0.574. Summer odds ratio 1.54 (p = 0.013) vs Fall. |
| Markdown and returns | Heavy discounts (40+%) do not raise returns. Only the 21-40% band has higher odds of return. | Chi-square p = 0.050. 21-40% band odds ratio 1.47 (p = 0.022), about 1.54 (p = 0.013) after adjusting for category, brand and season. |
| Return reasons | No significant difference between categories. | Chi-square p = (your value), Cramér's V = (your value). |
| Stock and markdown | No relationship. | Spearman rho = 0.013, p = 0.540. |

**Recommendations for the boutique:** review Ann Taylor and Summer items first, do not assume deep discounts increase returns, look more closely at moderate (21-40%) discounts, and collect richer data (customer information, sales volume, markdown dates).

**Limitations:** the models explain very little (pseudo R² of at most 0.016), many tests were run, the data has no customer or sales information, and the dataset looks synthetic (75% of purchase dates are the same date). The results are associations, not causal effects.

## CRISP-DM steps in the notebook

1. **Business Understanding:** goal, research questions and the variables needed
2. **Data Understanding:** structure, missing values, duplicates, distributions, consistency checks and a first look at each question
3. **Data Preparation:** handling missing sizes and return reasons, converting the return flag, markdown bands, outlier check
4. **Modeling:** chi-square tests, logistic regression (odds ratios and AUC), Cramér's V, heatmap and Spearman correlation
5. **Evaluation:** answers to the research questions and limitations
6. **Deployment:** recommendations for the boutique

## Repository structure

```
├── (your notebook name).ipynb     # Main notebook (analysis with notes)
├── requirements.txt               # Python libraries needed
└── README.md                      # This file
```

## Data

The dataset is `fashion_boutique_dataset.csv` (2,176 products, 14 columns). Put it in the project's main folder (next to the notebook). It isn't included in this repository.

## How to run it

```bash
# 1. Create and activate a virtual environment
python3 -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate

# 2. Install the libraries
pip install -r requirements.txt

# 3. Add fashion_boutique_dataset.csv to the folder, then start Jupyter
jupyter notebook
```

Open the notebook and choose **Run → Run All Cells**.

## Tools

Python · pandas · NumPy · seaborn · Matplotlib · SciPy · statsmodels · scikit-learn · Jupyter

## Main references

- Chapman, P. et al. (2000). *CRISP-DM 1.0: Step-by-step data mining guide*. SPSS Inc.

## Author

**Laura Lukasevic**
