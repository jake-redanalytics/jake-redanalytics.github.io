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
