# Mock practical assessment 02 ? Evaluate an existing approach

This is a deliberately challenging synthetic practice case. Its difficulty and format are our choices, rather than a verified description of QuantumBlack's assessment.

## The assignment

You are reviewing an analyst's recommendation before an operations director approves a courier change and a predictive late-delivery alert. At dispatch, the proposed alert should identify shipments that will miss their promised transit time. The intended first production scoring batch is May 2026, using information available at dispatch.

Read `ANALYST_MEMO.md`, inspect and run `analyst_approach.ipynb`, and use the supplied data to decide which conclusions management can rely on. Submit your own evidence and analysis in `review.ipynb`.

The files describe a fictional marketplace, observed as of the end of 30 April 2026. Missing outcomes mean the shipment's final delivery outcome is unresolved at that date. These records remain in the operational population. Monetary values are in one common practice currency, CU.

## Data dictionary

### data/shipments.csv

The intended grain is one dispatched shipment. IDs are unique in this export. Sellers can have many shipments.

| Field | Meaning and timing |
|---|---|
| shipment_id | Shipment identifier |
| seller_id | Merchant identifier, known at dispatch |
| dispatch_date | Dispatch date, January through April 2026 |
| carrier | Standard or Express service selected at dispatch |
| route_type | Urban or Rural, known at dispatch |
| promised_transit_days | Contractual maximum transit time in days, known at dispatch |
| distance_km | Estimated route distance available at dispatch, sometimes missing |
| warehouse_backlog | Warehouse workload at dispatch, sometimes missing |
| actual_transit_days | Final realised transit time, recorded upon delivery |
| exception_scans_after_dispatch | Count accumulated over the delivery journey, available in final form after delivery |
| delivered_date | Final delivery date when observed |
| late_delivery | 1 if final transit exceeds the promise, 0 otherwise, blank if final outcome remains unresolved |

### data/rate_history.csv

A historical price schedule. Each carrier and route type can have multiple effective dates. A row becomes effective on `effective_from` and remains effective until superseded for that same carrier and route type. Use the applicable schedule on the dispatch date to estimate a shipment's fee. There is no additional fee adjustment in this exercise.

| Field | Meaning |
|---|---|
| carrier | Courier service |
| route_type | Urban or Rural pricing segment |
| effective_from | First date on which this schedule applies |
| fee_cu | Fee per shipment in CU |

## Core review ? 60 minutes

1. **Reproduce and audit, approximately 15 minutes.** State the intended decision and prediction time. Find and prioritise the issues that materially affect the submitted metrics or recommendation. For at least four findings, give the affected code or claim, concrete evidence, consequence and correction. Quantify the impact of at least two findings. Distinguish confirmed errors from uncertainties.

2. **Reassess courier performance, approximately 15 minutes.** Produce a reliable comparison using the underlying shipments, with group sizes, known-outcome counts and unresolved-outcome counts. Investigate whether the overall courier comparison is sufficient to support switching services. Use one SQL query somewhere in your evidence. Explain which population each denominator describes.

3. **Rebuild the evaluation, approximately 20 minutes.** Choose and justify an evaluation design appropriate to the intended May deployment. Construct one baseline and one corrected model using eligible features and training-only preprocessing. Report a labelled confusion matrix and metrics relevant to the alert's operational purpose. Explain why your scores differ from the submitted result. Default thresholds are sufficient. Avoid tuning against your final evaluation period.

4. **Advise management, approximately 10 minutes.** Write a 150?250 word decision note saying what should proceed, what should be held, what evidence supports that position, and two concrete next actions. Separate prediction performance from evidence about whether changing courier service improves outcomes. Include at least three meaningful validation checks across your work.

## Optional extension ? 15 minutes

Reconstruct applicable fees using the historical schedule. Show total fees overall and by courier, validate that each shipment receives exactly one applicable fee, and quantify the difference from the analyst's fee estimate. State what additional evidence would be needed to forecast the cost and delivery effect of switching customers to another courier.

## Deliverables and practice rules

Use `.venv-py311`. Work in this folder so the CSV paths start with `data/`. Start a 60-minute timer when beginning the review. Official documentation and autocomplete are allowed for this practice. Attempt the work without AI assistance, and note any help used.

A well-evidenced partial review is preferable to unsupported claims. Prioritise problems by their effect on the decision. You do not need to discover every possible issue, use a particular estimator or memorise unfamiliar APIs. If the extension is unfinished, describe your intended method.

Save the completed review notebook with outputs, elapsed time and resource use. Preserve the original analyst submission so comparisons are reproducible.

The core scoring is 30 points for the audit, 20 for courier analysis, 30 for corrected evaluation and 20 for the management note and checks. The extension earns up to 10 additional practice points. This is a practice rubric, unrelated to company scoring. No answer key is included in these files.
