# LoanDefault

A logistic-regression exercise that estimates a borrower's probability of default and converts it into an expected credit loss.

> 09/2024<br>
> J.P. Morgan Chase Forage Quantitative Research Job Simulation

# Loan Default and Expected Loss

## Project overview

The supplied dataset contains 10,000 borrower records. The target records whether a borrower defaulted, while the explanatory variables describe their credit exposure, debt, income, employment history and FICO score.

The notebook trains a logistic regression classifier, visualises its test-set confusion matrix and defines an expected-loss function using the model's predicted probability of default.

## Business problem

The exercise is framed around a retail loan portfolio experiencing higher-than-expected defaults. The modelling task is to estimate each borrower's probability of default (PD) and translate that probability into a monetary expected loss for the outstanding exposure.

Logistic regression is used because it produces class probabilities directly and provides a simple, interpretable baseline for a binary credit-risk problem.

## Data

The model uses the following predictors:

| Variable | Meaning in the exercise |
| --- | --- |
| `credit_lines_outstanding` | Number of outstanding credit lines |
| `loan_amt_outstanding` | Current outstanding amount of the loan |
| `total_debt_outstanding` | Borrower's total outstanding debt |
| `income` | Borrower's income |
| `years_employed` | Recorded years in employment |
| `fico_score` | Borrower's FICO credit score |

`customer_id` is excluded from the feature matrix and `default` is used as the binary target. The dataset contains 1,851 defaults, giving an observed default rate of 18.51%.

## Method

1. Remove the identifier and target columns from the feature matrix.
2. Standardise the six numerical predictors.
3. Split the data into 80% training and 20% test sets using `random_state=42`.
4. Fit a scikit-learn logistic regression model.
5. Plot a confusion matrix for the held-out observations.
6. Use the predicted probability of default in the expected-loss calculation.

The standardisation step places variables measured on very different scales—such as income, debt and credit lines—on a comparable numerical scale before fitting the model.

## Model output

`LogisticRegression.predict()` is used to assign test-set classes for the confusion matrix. `predict_proba()` is used separately inside the loss function because expected loss requires the estimated probability of default rather than only a `default` or `non-default` label.

The confusion matrix provides a count of correct and incorrect predictions across the two classes. The notebook uses it as a visual diagnostic; it does not calculate or report a full set of performance and calibration statistics.

## Expected-loss function

`expected_loss(model, scaler, features)`:

1. standardises one new borrower's six input features;
2. obtains the predicted probability of default;
3. uses the outstanding loan amount as exposure at default;
4. assumes a recovery rate of 10%, giving loss-given-default of 90%; and
5. returns the probability-weighted loss.

For a fixed recovery rate of 10%, the notebook calculates:

$$
\text{Expected Loss}
= \text{PD} \times \text{Exposure} \times (1 - \text{Recovery Rate}).
$$

The worked borrower example in the saved notebook produces an expected loss of `$96.61`.

## Tools used

- pandas and NumPy for data handling and calculations;
- scikit-learn for preprocessing, splitting and logistic regression; and
- Matplotlib and Seaborn for the confusion-matrix visualisation.

## Repository contents

```text
.
├── Loan Data.csv    # Borrower data supplied with the simulation
├── task3.ipynb      # Model fitting, evaluation plot and loss function
└── README.md
```

## Scope and limitations

The notebook is an introductory credit-risk prototype. The scaler is fitted before the train-test split in the preserved exercise, which introduces information leakage into the evaluation. The model is not calibrated, compared with alternative classifiers or tested across time, and the 10% recovery rate is a fixed assumption. Its outputs should not be interpreted as production credit decisions or audited expected-credit-loss estimates.
