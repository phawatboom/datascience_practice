# Mock practical assessment 01

This is a synthetic practice assessment, not an official QuantumBlack or McKinsey assessment. The 60-minute time limit is our practice format. Your invitation gives a 60-minute interview and does not establish how long its practical component lasts.

## Business brief

A subscription company wants to prioritise customers for a retention campaign at the end of 30 June 2026. Investigate its customer base and build a baseline model predicting churn over the following 90 days. The company wants to catch churners while controlling unnecessary contacts.

The files are retrospective exports. Decide which fields would actually be available when a prediction is made.

## Files and meaning

`data/customer_snapshots.csv` contains customer records. The intended grain is one customer at the snapshot date. Exports may contain quality issues. All monetary fields use the same arbitrary practice currency, CU.

| Column | Meaning |
|---|---|
| customer_id | Customer identifier |
| snapshot_date | Date when input measurements were taken |
| country | Country recorded at the snapshot |
| plan_id | Subscription plan at the snapshot |
| contract | Monthly or annual billing at the snapshot |
| tenure_months | Months as a customer, positive whole numbers |
| monthly_charge | Actual recurring monthly charge in CU, strictly positive for this population |
| usage_hours_last_30d | Usage in the 30 days ending at the snapshot, nonnegative |
| support_tickets_last_30d | Tickets in the 30 days ending at the snapshot, nonnegative |
| churn_next_90d | Outcome over the next 90 days, 1 for churn and 0 for stayed. Blank means unknown outcome |
| cancellation_date | Actual cancellation date observed during the following 90 days, blank otherwise |

`data/plans.csv` is a plan lookup with `plan_id`, `plan_name` and `list_price` in CU. List price can differ from actual monthly charge. The intended lookup grain is one row per plan. Some customer plan IDs may have no match.

## Working conditions

Start a 60-minute timer when you begin task 1. Use the supplied `assessment.ipynb` and the `.venv-py311` kernel. It opens in this folder, so the CSV paths start with `data/`. Save your work regularly.

Attempt the mock without AI help. Python/SQL autocomplete and official library documentation are allowed for this practice. If you get stuck, document the issue and continue. These are practice rules rather than confirmed interview rules.

No extra packages are needed. Pandas, NumPy, scikit-learn, Matplotlib and Python's sqlite3 module are available.

## Task 1 ? Inspect and clean (15 minutes, 25 points)

Load both files. Explain the grain, inspect types, missing values, duplicates and invalid values. Produce an analytical customer table and a cleaned plan lookup. State and implement justified decisions for missing IDs/features/targets, malformed charges, invalid charges and category inconsistencies.

Join plan information to customers while keeping every cleaned customer. Validate lookup cardinality and show how many customer records do not match a plan. Report before/after row counts and demonstrate that the join preserves the intended customer grain. Document assumptions.

## Task 2 ? Analysis and SQL (10 minutes, 15 points)

Using one row per customer, return country-level customer count, sum of known valid monthly charges, count of known outcomes and churn rate among known outcomes. Preserve customers with missing country in an explicit Unknown group. Missing charges must not become invented revenue. Give the charge coverage count so the sum can be interpreted.

Write one SQL query reproducing that summary. You may load your cleaned analytical table into an in-memory SQLite database with Pandas `to_sql`. Use the cleaned table before modelling imputation.

Explain the denominator of churn rate. Identify one pattern with sample sizes and one data-quality limitation.

## Task 3 ? Classification (20 minutes, 30 points)

Define the prediction target and justified features. Reserve a stratified 20% test set with random_state=42. Explain exclusions. Build a majority-class baseline and a logistic regression model using a Pipeline and ColumnTransformer. Handle missing numeric and categorical inputs, scale as appropriate and handle unseen categories. Fit learned preprocessing using training data only.

Report baseline and model accuracy, model churn precision and recall, and a labelled confusion matrix. Explain why accuracy alone is insufficient. Use the default classification threshold for this mock.

## Task 4 ? Validate and communicate (10 minutes, 30 points)

Include at least three meaningful checks relevant to your decisions, beyond code running successfully. Write 4?6 sentences answering what you found, whether the model improves on the baseline, what limits the results and what you would investigate before launching a campaign. Propose two concrete next actions, distinguishing predictive results from evidence about whether an intervention works.

Use the remaining 5 minutes for a top-to-bottom run and save. A working partial solution with sound reasoning earns credit. Explain any unfinished work.

## Submission and review

Submit this notebook with outputs and written conclusions. No answer key is included. Tell the assistant when you are finished, your elapsed time, and where you got stuck. Review will cover correctness, cleaning decisions, SQL, leakage, metrics, validation, communication and independence. The scoring above is a practice rubric, not company scoring.
