# Multivariate Analysis with MaxDiff

## Canonical Record

This document provides a canonical record of the 2019 conference presentation *Multivariate Analysis with MaxDiff: A Curious Look at the Properties of MaxDiff Utilities*, by Jake Lee and Jeff D. Brazell.

This is not a subsequently written paper. It is a structured record of the presentation’s background, claims, tests, evidence, and practical implications.
 
### Conference Record

- **Conference:** 2019 Advanced Research Techniques (ART) Forum, American Marketing Association
- **Presentation date:** June 14, 2019
- **Session:** New Data II
- **Location:** Brigham Young University, Provo, Utah
- **Conference listing:** [2019 Advanced Research Techniques (ART) Forum](https://www.ama.org/events/conference/2019-advanced-research-techniques-art-forum/)

The AMA conference program described the presentation as an examination of whether MaxDiff is appropriate as an input to downstream multivariate techniques, using a study in which respondents were split between a MaxDiff exercise and a Select-any-of-J question.

## Background

MaxDiff is widely used to measure relative preference or importance across a set of items. The presentation asked a narrower question: whether respondent-level utilities estimated from a MaxDiff exercise can also be treated as ordinary multivariate data for downstream analyses such as factor analysis, regression, segmentation, or other methods that depend on the covariance or correlation structure among items.

The motivating concern was that MaxDiff utilities are constrained by the comparative task and resulting utility structure. That creates technical problems for some multivariate procedures and raises a more substantive question: whether the correlations among estimated utilities reflect the underlying relationships among respondents' preferences or are partly artifacts of the MaxDiff exercise itself.

## Core Claims

### 1. MaxDiff can recover aggregate item ordering well

The presentation did not argue that MaxDiff is ineffective for measuring relative preference or importance. In the simulations, MaxDiff recovered the aggregate ordering of items well even when random choice error was present.

### 2. Respondent-level MaxDiff utilities do not reliably recover the underlying correlation structure

The central claim was that the relationships among estimated respondent-level MaxDiff utilities should not be assumed to represent the underlying relationships among the attributes themselves. The comparative structure of the MaxDiff task imposes a distribution and covariance structure on the resulting utilities.

### 3. Increasing the number of MaxDiff tasks does not solve the correlation problem

In simulations where the true utility means and covariance matrix were known, increasing the number of tasks from 12 to as many as 120 improved measurement of aggregate item ordering but did not recover the true correlations among attributes.

### 4. Multivariate analyses that depend on those correlations can therefore be misleading

Factor analysis, regression, segmentation, TURF, and related procedures depend in different ways on relationships among variables. If the covariance or correlation structure in the MaxDiff utilities is an artifact of the measurement exercise rather than a faithful representation of the underlying data-generating process, results from those downstream analyses can be difficult to interpret substantively.

## Evidence and Tests

The presentation used both empirical comparisons and simulation to test whether the observed correlation problem could be explained by features other than the MaxDiff task itself.

### Empirical comparison

In the primary study, respondents were randomly assigned to either a MaxDiff exercise or a Select-any-of-J exercise using the same underlying set of statements. Aggregate item means aligned reasonably well across the two approaches, but the correlation structures differed substantially.

A second dataset using a different set of gaming-related statements produced the same general pattern, reducing the likelihood that the original result was specific to one dataset.

### Simulation with known means and covariance

Synthetic respondent utilities were generated from a known multivariate distribution with specified means and covariance structure. MaxDiff tasks were then simulated using random Gumbel error.

The number of tasks was increased from 12 to 18, 24, 30, 60, and 120. Aggregate item ordering was recovered well, but even at 120 tasks the estimated respondent-level utilities did not recover the true correlation structure.

### Alternative coding

The MaxDiff model was estimated using alternative coding schemes. Mean utilities and bivariate correlations were highly consistent across coding approaches, indicating that the problem was not an artifact of the particular coding convention used.

### Alternative covariance prior

The hierarchical model was re-estimated in Stan using a more flexible covariance specification rather than an inverse-Wishart prior. Separating the estimation of variances and correlations did not restore the true correlation structure.

### Anchored MaxDiff

An indirect anchoring procedure was tested in simulation. Anchoring slightly improved aggregate ordering but did not solve the correlation problem.

### Probability transformation

Transforming MaxDiff utilities into probability-like scores did not solve the issue. The resulting correlations were perturbed rather than restored to the underlying correlation structure.

### Zero-signal simulation

In an additional simulation, all true utilities were set to zero and respondents' MaxDiff choices were generated only by random Gumbel error. The resulting estimated utilities still produced apparent correlations as large as approximately ±0.4.
