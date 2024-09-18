# LoanDefault

09/2024<br>
JPMorgan Chase Forage Quantitative Research

# The Task

This task focuses on predicting loan defaults and calculating expected loss. The retail banking arm has been facing higher-than-expected loan defaults, and your role is to build a predictive model that estimates the probability of default (PD) for each loan. With this probability, you will calculate the expected loss on each loan using a predefined recovery rate.

### Data

The provided dataset contains customer details such as income, total loans outstanding, credit score, and loan history, along with whether or not the borrower has previously defaulted. Using this data, the task is to predict the likelihood of default for each customer and use it to estimate the expected loss on their loan.

### Project Goals

- **Predict Loan Defaults**: Build a model to predict whether a borrower is likely to default based on their loan characteristics.
- **Calculate Expected Loss**: Use the predicted probability of default (PD) and a recovery rate of 10% to calculate the expected loss for each borrower.
  
Expected loss is calculated as:

$\text{Expected Loss} = \text{PD} \times \text{Outstanding Loan Amount} \times (1 - \text{Recovery Rate})$

### Steps Involved

1. **Data Preprocessing**: Handle missing values and preprocess the features for model training.
2. **Model Training**: Train a classification model (logistic regression) to predict the probability of default.
3. **Expected Loss Calculation**: Define a function that takes a borrower’s details and returns the expected loss based on the model's prediction.

# The Code

Key components of the code include:

- `expected_loss(model, scaler, features)`: This function calculates the expected loss for a given borrower based on the predicted probability of default.


