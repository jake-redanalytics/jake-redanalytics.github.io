# Respondent Covariates Can Lie

**Evidence from Hierarchical Choice Models**

This research examines a failure mode in hierarchical choice models: respondent covariates can receive strong in-sample support while producing systematic preference structure that fails to generalize to new respondents.

The central question is not simply whether respondent covariates should be included, but how much preference heterogeneity a model should be allowed to attribute to them.

## Paper

**Respondent Covariates Can Lie: Evidence from Hierarchical Choice Models**  
Jake Lee, Red Analytics, Inc.  
September 2026

[Download the paper](respondent-covariates-can-lie.pdf)

### Main result

The primary stress test deliberately broke the relationship between a respondent characteristic and preference, then entered twenty shuffled versions of that characteristic as upper-level covariates.

The conventional, more permissive specification looked extraordinarily successful in sample. But when evaluated on respondents held completely outside estimation, the result reversed:

- **Base:** mean new-respondent log PPL = -23.311
- **Permissive, 20 placebo covariates:** -32.809
- **Regularized ("Justified"), 20 placebo covariates:** -23.264

The permissive model therefore fell **9.498 log predictive-likelihood units per respondent below Base**, despite its very strong in-sample performance.

The paper follows this failure through:

- new-person predictive validation
- fitted heterogeneity and its attribution
- willingness-to-pay differentiation
- price-response and revenue consequences

The broader principle is **earned heterogeneity**: systematic preference differentiation should not receive evidentiary credit simply because a model can estimate it. It should be supported by evidence appropriate to the claim being made.

## Replication / Extension

A separate public analysis examines the same general problem using another dataset and implementation.

**Medium article:** link forthcoming

Replication materials will be added to the [`replication`](replication/) folder.

## Related Articles

Three shorter LinkedIn articles discuss related issues in model validation, respondent covariates, and evidence standards.

1. Link forthcoming
2. Link forthcoming
3. Link forthcoming

## Scope

The paper demonstrates a failure mode; it does **not** estimate how frequently that failure occurs across hierarchical choice applications.

The regularization approach examined in the paper is one possible response, not a claim that it is uniquely correct. Other regularization structures may control the same problem as well or better.
