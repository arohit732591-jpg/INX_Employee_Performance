# Employee Performance Analysis

A data science project that analyses the employee data of a fictional company, INX Future Inc, to find why performance has declined, which factors matter most, and whether performance can be predicted.

This was completed as a course project. The business case and data come from the course material.

## Business Problem

INX Future Inc has seen its employee performance indexes fall, and client satisfaction has dropped by 8 percentage points. The CEO wants to understand the causes without penalising employees in a way that harms morale. The project delivers:

1. Department-wise performance
2. The top 3 factors affecting employee performance
3. A trained model that predicts the performance rating
4. Recommendations to improve performance

## Data

- 1,200 employees and 28 columns, with no missing values and no duplicate rows
- Target: `PerformanceRating`, with 1 (Low), 2 (Good), 3 (Excellent) and 4 (Outstanding)
- No employee is rated Low. In the data, 16% are rated Good, 73% Excellent and 11% Outstanding
- The data dictionary is in `references/data_dictionary.csv`

## Key Findings

**Department-wise performance**
- Development performs best, with only about 4% of employees rated Good (the lowest rating in the data).
- Finance has the highest share rated Good (about 31%), followed by Sales (23%) and Research and Development (20%).
- Sales and Research and Development hold about 80% of all employees rated Good (155 of 194).

**Top 3 factors affecting performance** (confirmed by both correlation and Random Forest feature importance)
1. Last salary hike percentage
2. Environment satisfaction
3. Years since last promotion

These are strong links, not proven causes. For example, top performers may receive bigger salary hikes, so part of the effect may run in the opposite direction.

**Prediction model**

| Model | Test accuracy |
|---|---|
| Random Forest | 93.8% |
| Support Vector Machine | 83.3% |
| Logistic Regression | 82.5% |

- Random Forest is the final model. Five-fold cross-validation gave an average accuracy of 92.8%.
- It identified 85% of employees rated Good and 73% of employees rated Outstanding.
- Because 73% of employees are rated Excellent, accuracy alone can mislead, so the confusion matrix and classification report were used as well.

**Limitation for hiring**

A second model using only information known before joining (age, education, experience, job role and similar) reached about 70% accuracy, which is no better than always predicting Excellent (about 73%). A candidate's background does not reliably predict later performance in this data, so this model should not be used alone for hiring decisions.

## Recommendations (summary)

- Start improvement efforts in Sales and Research and Development
- Improve the work environment for employees with Low or Medium satisfaction
- Review promotion timelines for employees who have waited more than two years
- Make salary hike decisions transparent and linked to performance
- Use the model to find employees who need support, not to penalise them
- Do not rely on candidate background for hiring
- Test changes with one team before applying them company-wide

The full reasoning is in `project_summary.ipynb`.

## Project Structure

```
INX_Employee_Performance/
├── project_summary.ipynb          Requirement, analysis, results and recommendations
├── data/
│   ├── external/
│   ├── processed/                 cleaned_data.csv, encoded_data.csv
│   └── raw/                       original Excel file
├── src/
│   ├── data_processing/
│   │   ├── data_processing.ipynb
│   │   └── data_exploratory_analysis.ipynb
│   ├── models/
│   │   ├── train_model.ipynb
│   │   ├── predict_model.ipynb
│   │   └── *.pkl                  saved models, encoders and column lists
│   └── visualization/
│       └── visualize.ipynb
└── references/
    └── data_dictionary.csv
```

## How to Run

1. Install the requirements:
   ```bash
   pip install pandas numpy scikit-learn matplotlib seaborn joblib xlrd jupyter
   ```
2. Run the notebooks in this order, because each one uses files saved by the previous one:
   1. `src/data_processing/data_processing.ipynb`
   2. `src/data_processing/data_exploratory_analysis.ipynb`
   3. `src/models/train_model.ipynb`
   4. `src/models/predict_model.ipynb`
   5. `src/visualization/visualize.ipynb`
3. Read `project_summary.ipynb` for the findings and recommendations.

The saved models are included, so `predict_model.ipynb` can also be run on its own.

## Tools Used

Python, pandas, NumPy, scikit-learn (Random Forest, Logistic Regression, Support Vector Machine), matplotlib, seaborn, joblib, Jupyter