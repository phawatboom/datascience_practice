# Analyst memo ? Courier and alert recommendation

**To** Operations Director  
**From** Operations Analytics Team  
**Review date** 30 April 2026

## Recommendation

Approve the late-delivery alert for May and migrate Express shipments to Standard where capacity permits.

## Analysis submitted

We enriched the shipment export with the partner rate history using carrier as the matching key. The enriched table contains 7,200 rows, which we treated as shipment observations. Unresolved outcome fields were filled with zero so the operational population could remain in the calculations.

Standard's late-delivery rate is 20.2%, compared with 27.9% for Express. This indicates Standard is the more reliable service and should replace Express. We estimate current total courier fees of 61,380.00 CU from the enriched records. The fee schedule also shows Standard is cheaper, so migration should improve reliability and reduce cost.

A random forest achieved 100.0% accuracy on a stratified random 20% holdout from the enriched table, exceeding our proposed 95% accuracy launch target. We included available route, warehouse, pricing and transit measurements. Missing inputs were handled within a preprocessing pipeline fitted on the training data.

Given the high accuracy and the overall courier comparison, we recommend launching the alert without further validation and beginning the courier migration. The submitted notebook contains the implementation and reported metrics.

## Supporting files

- `analyst_approach.ipynb`
- `data/shipments.csv`
- `data/rate_history.csv`

This memo is part of a fictional assessment. Its claims are the subject of your review.
