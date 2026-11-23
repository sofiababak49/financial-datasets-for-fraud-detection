# Financial Transaction Risk & Fraud Pattern Analysis
## Objective
This project analyses a labelled financial transaction dataset with Python to understand which transaction types, amounts and account balances are more common in fraudulent transactions. I also create several simple rules to identify potentially fraudulent transactions and compare their results with a Random Forest model.
## Dataset
The project uses the PaySim dataset [Synthetic Financial Datasets For Fraud Detection](https://www.kaggle.com/datasets/ealaxi/paysim1) from Kaggle. The data is synthetic and was generated using a simulator based on real mobile money transactions. This means that the results show patterns in simulated data and can not fully represent real banking activity. The analysed file has 859,186 transactions and 11 columns (type, amount, origin and destination balances and a fraud label). One row without a fraud label was excluded from the model. The dataset is not included in this repository because of its size. To run the notebook, download the CSV file from Kaggle and place it in the same folder as the notebook.
## Tools
Python, Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, Jupyter Notebook
## Analysis
Data check, normal amounts and activity per account, accounts with unusually high activity, time patterns and bursts, channels and transaction types, variables useful for detecting unusual behaviour and 3 simple rules that flag suspicious transactions.
## Key Findings
1. Fraud is rare (484 transactions, 0.056%) and appears only in TRANSFER (0.329%) and CASH_OUT (0.081%); the other three transaction types contain no fraud.
2. Fraudulent transactions have higher amounts than normal ones (median 235,375.43 vs 80,679.50). The top 1% of amounts (above 1,341,777.27) has fraud rate of 1.059% compared to 0.056% overall, but holds only 18.8% of all fraud.
3. In 95.2% of fraud cases (461 out of 484) the origin account was left empty. However, 199,138 transactions show the same pattern, so this rule also catches a large number of normal transactions.
4. At least 2 of the 3 rules detect 96.1% of fraud cases (465 out of 484). However, they also flag 164,143 transactions, around 19% of the total. Only 0.28% of these alerts are real fraud.
5. On a test set of 100,000 transactions with 56 fraud cases, the rule-based approach finds 54 (recall 0.96), but also produces 18,765 false alarms. Random Forest performs worse, detecting only 9 fraud cases (recall 0.16). Its precision is 0.08 and PR-AUC is 0.029. The model only used transaction type and amount.
## Limitations
- The data is synthetic, so patterns such as emptied accounts may reflect how it was generated rather than real-world fraud.
- The balance columns may not be reliable for fraud detectionaccording to the dataset description. For this reason, they were not included in the Random Forest model.
- Rule thresholds were chosen on the same data  on which they were tested, so the rule results may be too optimistic. 
- The test set has only 56 fraud cases, so the model results are unstable.
