# Fashion Boutique Returns: What Drives Returns and Markdowns?

I used the **CRISP-DM** process to study product returns and markdowns in a fashion boutique dataset.

## Project question

**Topic:** Understanding which product and pricing factors are linked to returns, to support markdown and return-reduction decisions.

**Research questions**

1. Which **categories, brands, sizes or seasons** have the highest return rate?
2. Do **heavily discounted items** get returned more often?
3. Does **high stock** go with deeper markdowns?

## Key findings

I analysed **2,176 products**, of which **320 (14.7%) were returned** and **878 (40.3%) were marked down**.

| **Question** | **Result** | **Evidence** |
| --- | --- | --- |
| Product characteristics | Weak effects only. Summer items and Ann Taylor have higher return rates. Category and size have no effect. | Chi-square: category p = 0.798, brand p = 0.178, season p = 0.049, size p = 0.642. Logistic regression: pseudo R² = 0.011, AUC = 0.574. Summer odds ratio 1.54 (p = 0.013) vs Fall. |
| Markdown and returns | Heavy discounts (40+%) do not raise returns. Only the 21-40% band has higher odds of return. | Chi-square p = 0.050. 21-40% band odds ratio 1.47 (p = 0.022), about 1.54 (p = 0.013) after adjusting for category, brand and season. |
| Stock and markdown | No relationship. | Spearman rho = 0.013, p = 0.540. |

**Recommendations for the boutique:** review Ann Taylor and Summer items first, do not assume deep discounts increase returns, look more closely at moderate (21-40%) discounts, and collect richer data (customer information, sales volume, markdown dates).

**Limitations:** the models explain very little (pseudo R² of at most 0.016), many tests were run, the data has no customer or sales information, and the dataset looks synthetic (75% of purchase dates are the same date). The results are associations, not causal effects.

## Key insight

Returns are hard to predict from the product information available. Brand, season, category, size and discount level together explain only about 1-2% of the differences in returns, and the best model is only slightly better than chance (AUC = 0.574). Two patterns stand out: Summer items and Ann Taylor products are returned more often, and items marked down by 21-40% are returned more often than full-price items. Heavy discounts (40+%) do not increase returns, and stock level does not explain how deep a markdown is.

In other words, most of what drives returns is not in this dataset. Customer behaviour, product quality and fit are likely to matter more than the characteristics recorded here.

## CRISP-DM steps in the notebook

1. **Business Understanding:** goal, research questions and the variables needed
2. **Data Understanding:** structure, missing values, duplicates, distributions, consistency checks and a first look at each question
3. **Data Preparation:** handling missing sizes, converting the return flag, markdown bands, outlier check
4. **Modeling:** chi-square tests, logistic regression (odds ratios and AUC) and Spearman correlation
5. **Evaluation:** answers to the research questions and limitations
6. **Deployment:** recommendations for the boutique

## Repository structure

```
├── boutique_crispdm.ipynb         # Main notebook (analysis with notes)
├── requirements.txt               # Python libraries needed
└── README.md                      # This file
```

## Data

The dataset is the **Retail Fashion Boutique Data & Sales Analytics 2025** dataset from Kaggle: [https://www.kaggle.com/datasets/pratyushpuri/retail-fashion-boutique-data-sales-analytics-2025](https://www.kaggle.com/datasets/pratyushpuri/retail-fashion-boutique-data-sales-analytics-2025)

It has 2,176 products (one row per product) and 14 columns:

- **Product:** category, brand, season, size, colour
- **Pricing:** original price, markdown percentage, current price
- **Inventory:** stock quantity
- **Customer outcome:** customer rating, returned (yes/no), return reason
- **Date:** purchase date

Download `fashion_boutique_dataset.csv` and put it in the project's main folder (next to the notebook). It isn't included in this repository.

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

Open `boutique_crispdm.ipynb` and choose **Run → Run All Cells**.

## Key learnings

- A weak or non-significant result is still a valid finding. Here it shows that the available product information explains very little about returns.
- Looking at one factor at a time and at all factors together can give different answers, so I used both chi-square tests and logistic regression.
- With a binary outcome, accuracy is misleading when only 14.7% of items are returned, so I used odds ratios, pseudo R² and AUC to judge the model.
- The choice of baseline group changes how a regression looks: Ann Taylor has the highest return rate, which makes the other brands appear lower.
- When many tests are run, a few p-values just under 0.05 can appear by chance, so I treated borderline results with caution.

## Future improvements

- Add customer-level data (for example customer ID, age group, previous returns) to see whether who buys matters more than what is bought.
- Add sales volume, so return rates can be compared with how often each product sells.
- Record the date a markdown was applied and the stock level at that time, to study whether stock really leads to discounts.
- Use real boutique data, because this dataset looks synthetic (75% of purchase dates are the same date, and stock and ratings are evenly spread).
- Try a tree-based model (for example a random forest) to check whether non-linear patterns predict returns better than logistic regression.

## Tools

Python · pandas · NumPy · seaborn · Matplotlib · SciPy · statsmodels · scikit-learn · Jupyter

## Main references

- Chapman, P. et al. (2000). *CRISP-DM 1.0: Step-by-step data mining guide*. SPSS Inc.
- Retail Fashion Boutique Data & Sales Analytics 2025 (Kaggle): https://www.kaggle.com/datasets/pratyushpuri/retail-fashion-boutique-data-sales-analytics-2025

## Author

**Laura Lukasevic**
