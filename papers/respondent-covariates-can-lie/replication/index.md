---
title: "Improving Choice Model Accuracy Using Covariates Depends on What You Hold Out"
description: "Same-respondent task holdouts and new-respondent holdouts test different claims in hierarchical discrete choice models."
---

# Improving Choice Model Accuracy Using Covariates Depends on What You Hold Out

*Same-respondent task holdouts and new-respondent holdouts test different claims in hierarchical discrete choice models*

> **Publication note:** The canonical public version of this article is published on Medium. This GitHub version is maintained as a machine-readable mirror for indexing, retrieval, citation, and methodological reference.
>
> [Read the canonical version on Medium](MEDIUM-URL-HERE)
Related paper: [Respondent Covariates Can Lie: Evidence from Hierarchical Choice Models](../respondent_covariates_can_lie.pdf)

Improved prediction is not a complete claim until we know what was held
out.

That distinction matters because many applied choice models are used to
predict people whose choice histories were unused during estimation.
Their respondent characteristics may be observed, but their individual
preference parameters cannot be informed by choices the model has
already seen. Predicting another choice from a respondent already used
in estimation is a different problem.

Those are different prediction problems. In this case, they lead to very
different conclusions about the value of respondent covariates.

## A practical example

DisplayR's article [How to Improve Choice Model Accuracy Using
Covariates](https://www.displayr.com/improve-choice-model-accuracy-with-covariates/)
uses the public cruise data from Sawtooth Software's [2016 CBC
Prediction
Competition](https://www.quirks.com/storage/attachments/57d78590d82f1c0a1824d8b8/57d7859bd82f1c0a1824d8c0/original/201606_quirks.pdf).
The study includes 600 respondents completing 15 choice tasks, with four
cruise alternatives per task. The alternatives vary in destination,
cruise line, trip length, room type, amenities, and price. We directly
extend that analysis: we start with the same dataset, the same
favorite-cruise-line covariate, and the same held-out-task logic, then
add new-respondent validation.

In that example, favorite cruise line is added through the software’s
Respondent-specific covariates input to a hierarchical Bayes choice
model, yielding a minor gain in prediction of a held-out choice task.

We started in the same place.

The first 14 choice tasks were used to estimate the model, and task 15
was held out. The Base model used no respondent covariates. The second
model added favorite cruise line, represented by five encoded covariate
columns, relying on the standard upper-level treatment.

| **Respondent information**               | **Covariate treatment** | **Mean probability assigned to chosen held-out alternative** |
|------------------------------------------|-------------------------|--------------------------------------------------------------|
| None                                     | Base                    | .540                                                         |
| Favorite cruise line (5 encoded columns) | Permissive              | .548                                                         |

Using the same task-holdout logic and a comparable empirical metric, we
obtained the same qualitative finding: favorite cruise line slightly
improved prediction of another choice from respondents whose other
choices had already been observed.

So far, so good.

## More respondent covariates look even better

DisplayR also observes that a more complete analysis could include the
other covariates of interest.

We took the suggestion literally.

The respondent file contains 12 core survey items covering cruise
experience, future cruise likelihood, available travel resources,
motivations, preferred itinerary, preferred cruise line, trip length,
employment, marital status, and education. After categorical coding,
those questions produced 49 respondent-covariate columns.

That is a lot of upper-level flexibility.

In the conventional hierarchical specification, the encoded
respondent-covariate effects receive the model's standard baseline
upper-level prior scale. Individual coefficients can still be pulled
toward zero by that prior and by the posterior evidence, but there is no
additional learned scale that can attenuate the effects associated with
one respondent-covariate column as a group. We refer to this treatment
of respondent covariates as Permissive.

The model using the full questionnaire set under Permissive treatment
appeared highly effective.

| **Evidence**                        | **Base model, no covariates** | **Full questionnaire set (49 columns), Permissive treatment** | **Change** |
|-------------------------------------|-------------------------------|---------------------------------------------------------------|------------|
| Mean log likelihood                 | -2770                         | -1271                                                         | +1499      |
| Newton-Raftery log marginal density | -2885                         | -1381                                                         | +1504      |
| Mean probability on held-out task   | .540                          | .587                                                          | +.047      |

Likelihood measures how well the model accounts for the choices used to
estimate it. Added flexibility can improve likelihood, so a better
likelihood alone is entirely expected.

Raw likelihood invites immediate scrutiny because the larger model has
many more upper-level coefficients. We therefore also examined the
Newton-Raftery approximation to log marginal density, a familiar
Bayesian model-evidence calculation that integrates over the specified
prior. It strongly favored the model using the full respondent-covariate
set under Permissive treatment as well.

Then the held-out task seemingly validated the result. The average
probability assigned to the alternative respondents actually chose
increased from .540 to .587.

One respondent covariate helped a little. Forty-nine encoded covariate
columns seemingly helped even more.

## Held-out tasks vs. held-out respondents in choice-model validation

Now we need to ask precisely what was held out.

In the first validation test, the model had already seen 14 choices from
each respondent. Only task 15 was hidden. The model therefore possessed
substantial information about the preferences of the person it was
trying to predict.

We call this a same-respondent task holdout.

A new-respondent holdout asks a different question. None of that
person's choice data are used during estimation. The model must transfer
what it learned from other respondents to someone whose choices it has
never seen.

The distinction is especially important when respondent covariates are
being evaluated. In a same-respondent task holdout, the person's other
choices can do much of the work of identifying that person's
preferences. In a new-respondent holdout, the learned population and
covariate structure has to shoulder far more of that burden.

The phrase out-of-sample is often used for both kinds of validation.
That language is not precise enough on its own.

A held-out task and a held-out respondent are not interchangeable
evaluation frameworks. When respondent covariates are being evaluated,
ask what was actually held out.

## New-respondent validation gives a different answer

Let’s revisit the favorite cruise line covariate.

In this fixed 300/300 respondent split, the Permissive treatment
improved the familiar same-respondent task-holdout statistic slightly.
When predictive performance was instead evaluated on respondents whose
choices were completely excluded from estimation, that advantage
disappeared. The earlier task-holdout result remains intact. Favorite
cruise line helped predict another choice from respondents the model
already knew. It did not establish better prediction for respondents
whose choice histories were unavailable.

The difference becomes much more pronounced with the full questionnaire
set.

| **Respondent information**                  | **Covariate treatment** | **New-respondent performance vs. Base** | **Held-out respondents improved vs. Base** |
|---------------------------------------------|-------------------------|-----------------------------------------|--------------------------------------------|
| Favorite cruise line (5 encoded columns)    | Permissive              | Slightly worse                          | 52%                                        |
| Full questionnaire set (49 encoded columns) | Permissive              | Much worse                              | 14%                                        |

The 49-column Permissive treatment also shows the textbook signature of
overfitting. It fits the estimation data dramatically better, yet
predictive performance deteriorates sharply on respondents whose choices
played no role in fitting the model.

The same-respondent task-holdout result explains why that overfit could
be overlooked in practice. A familiar validation summary still looked
better even while the much broader respondent-level structure failed to
transfer to new people.

## Even the held-out-task score can change the conclusion

The task-holdout result contains its own caveat.

The arithmetic mean probability assigned to the chosen held-out
alternative improved under the 49-column Permissive treatment. But the
mean log predictive probability for that same held-out task degraded.

Those statements can both be true. The Permissive treatment produced
modestly better predictions for many respondents, but it also produced
some very poor predictions. The arithmetic mean chosen probability
rewards the gains, while the log score penalizes confident mistakes far
more heavily. The arithmetic chosen probability closely matches the
practical validation approach in the motivating example.

So there are two questions underlying an assertion such as “holdout
prediction improved”: what was held out, and how was predictive success
scored?

The main subject here is the first question. But this case also shows
why the second demands a clear statement.

## "Use fewer covariates" is sensible advice. It is not a stopping rule.

Practitioner guidance has long flagged this hazard.

Sawtooth Software's [published
guidance](https://content.sawtoothsoftware.com/assets/8457c054-5abf-40b2-a833-7c67902f23dd)
has long urged moderation. Analysts are advised to avoid using too many
covariates, focus on a relatively small number that are likely to be
useful, watch for multicollinearity, and favor respondent information
with genuine predictive value.

That is sensible advice. It also moves the ultimate burden onto the
analyst.

Which covariates should be included? How many? Should an ordinal
variable be treated continuously or categorically? Which categories
should be combined? Which subsets should be tested? How much model
selection suffices?

A real questionnaire can contain dozens of plausible respondent
variables. A rigorous pruning strategy can require many additional model
fits, with validation required at each stage. Repeated selection against
the same validation evidence can itself become another opportunity to
overfit.

There has also been a more optimistic intuition around hierarchical
Bayes: useful respondent information should matter, while irrelevant
information may largely wash out. Earlier Sawtooth examples help explain
why that intuition can feel reasonable. Models containing several poorly
chosen covariates could still appear remarkably resilient when evaluated
on held-out tasks from respondents already used in estimation.

Together, those ideas leave practitioners with an uncomfortable
compromise: be selective about respondent covariates, but expect HB to
tolerate at least some poor choices. That position is easier to
understand when much of the reassuring validation evidence comes from
predicting additional tasks for respondents the model already knows.

The new-respondent test asks a different question.

## Regularizing respondent covariates with learned shrinkage

There is another possible response to the selection problem.

Instead of giving every encoded respondent-covariate column only the
ordinary fixed upper-level prior scale, each encoded column can
incorporate a separate learned nonnegative scale under a shrinkage
prior.

The regularization operates at the encoded respondent-covariate level
rather than coefficient by coefficient. One learned scale regulates that
encoded covariate’s upper-level influence across the preference means it
can shift.

We call this a [Justified treatment of respondent
covariates](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=7457138).
The architecture and broader evidence are developed in *Respondent
Covariates Can Lie*.

| **Respondent information** | **Encoded covariate columns** | **Covariate treatment** |
|----------------------------|-------------------------------|-------------------------|
| None                       | 0                             | Base                    |
| Favorite cruise line       | 5                             | Permissive              |
| Favorite cruise line       | 5                             | Justified               |
| Full questionnaire set     | 49                            | Permissive              |
| Full questionnaire set     | 49                            | Justified               |

In this case, with the same 49 encoded covariate columns, the Justified
treatment went beyond merely avoiding the severe new-respondent loss
produced by the Permissive treatment. It improved prediction relative to
the Base model.

For new respondents, predictive success is evaluated via
respondent-level log PPL, the joint posterior predictive likelihood of
all 15 choices for a respondent whose choices were completely excluded
from estimation. The integration treats each new respondent as having
one latent preference vector shared across that respondent’s 15 choices.

| **Respondent information**          | **Covariate treatment** | **New-respondent performance vs. Base** | **Held-out respondents improved vs. Base** |
|-------------------------------------|-------------------------|-----------------------------------------|--------------------------------------------|
| Full questionnaire set (49 columns) | Permissive              | -10.7 mean log PPL/respondent           | 14%                                        |
| Full questionnaire set (49 columns) | Justified               | +0.40 mean log PPL/respondent           | 65%                                        |

The same large respondent-information set produced divergent outcomes
depending on how the covariates were treated. The Justified treatment
also outperformed the Permissive treatment for about 90% of the new
respondents.

Under the Justified treatment, each encoded column receives an
additional learned local scale that can attenuate the systematic
differentiation associated with it.

The practical objective is to reduce the consequences of giving
respondent information more systematic influence than the evidence
supports. In this example, that treatment transformed a drastic
new-respondent loss into an improvement over Base.

## What this result does and does not show

This cruise analysis is a single public-data case study. The earlier
*Respondent Covariates Can Lie* paper provides separate evidence using a
different dataset and purposely constructed stress tests of
new-respondent generalization. The earlier paper follows the failure
through fitted heterogeneity and downstream economic consequences. Here,
the narrower purpose is to connect the same predictive failure pattern
to a familiar practitioner benchmark dataset.

Same-respondent task holdouts remain defensible. They answer a useful
question when the objective is to predict another choice from someone
whose preferences have already been partially observed. New-respondent
holdouts answer a different question and become important when the model
is supposed to predict people whose choice histories were unavailable
during estimation.

The results also do not suggest that every Permissive treatment of
respondent covariates will overfit, or that every Justified treatment
will improve prediction. Broader claims require replication across
additional datasets.

But the distinction between the validation targets stands firm.

A model can look better under a familiar same-respondent task-holdout
summary while becoming worse at predicting people it has never seen. For
many applications, the model ultimately needs to predict people whose
choice histories were not available during estimation.

**Improved prediction is not a complete claim until we know what was
held out.**

Before accepting a claim of improved out-of-sample prediction, ask
whether the model was predicting a new task or a new person.

## Replication details

The public cruise data contain 600 respondents and 15 stated-preference
tasks per respondent. We randomly assigned 300 respondents to estimation
and 300 to new-respondent validation. For estimation respondents, tasks
1 through 14 were used to fit the models and task 15 was reserved for
same-respondent validation. All 15 choices from the 300 validation
respondents were excluded from estimation.

We estimated five specifications:

| **Respondent information** | **Encoded covariate columns** | **Treatment** | **Role**                                              |
|----------------------------|-------------------------------|---------------|-------------------------------------------------------|
| None                       | 0                             | Base          | Benchmark                                             |
| Favorite cruise line       | 5                             | Permissive    | Reproduce motivating task-holdout result              |
| Favorite cruise line       | 5                             | Justified     | Compare treatments with the same information          |
| Full questionnaire set     | 49                            | Permissive    | Test the expanded covariate set                       |
| Full questionnaire set     | 49                            | Justified     | Compare treatments with the same expanded information |

The upper-level model follows the notation in *Respondent Covariates Can Lie*. For respondent *i*,

**β<sub>i</sub> = z<sub>i</sub>Γ + ξ<sub>i</sub>, ξ<sub>i</sub> ∼ N(0, Σ).**

For encoded respondent-covariate column *j*, let γ<sub>j</sub> represent the vector of upper-level effects. Under the Justified treatment,

**γ<sub>j</sub> ∣ s<sub>j</sub> ∼ N(0, (s<sub>j</sub>σ<sub>γ</sub>)<sup>2</sup>I), s<sub>j</sub> ∼ HalfNormal(0, 0.5).**

The learned s<sub>j</sub> therefore scales the entire row of upper-level effects tied to the individual covariate column *j*. Under the Permissive treatment, the corresponding scale is fixed at s<sub>j</sub> = 1.

For the same-respondent task holdout,

**PPP<sub>i</sub> = p(y<sub>i,15</sub> ∣ z<sub>i</sub>, D<sub>est</sub>) = ∫ p(y<sub>i,15</sub> ∣ β<sub>i</sub>) p(β<sub>i</sub> ∣ z<sub>i</sub>, D<sub>est</sub>), dβ<sub>i</sub>.**

Here D<sub>est</sub> includes that respondent's first 14 choices. The task-holdout comparison reports the arithmetic mean of PPP<sub>i</sub> across respondents; we also utilized log(PPP<sub>i</sub>) to examine the proper log predictive score.

For a new respondent whose choices were entirely omitted during estimation,

**PPL<sub>i</sub> = p(y<sub>i</sub> ∣ z<sub>i</sub>, D<sub>est</sub>) = ∬ p(y<sub>i</sub> ∣ β<sub>i</sub>), p(β<sub>i</sub> ∣ z<sub>i</sub>, Γ, Σ), p(Γ, Σ ∣ D<sub>est</sub>), dβ<sub>i</sub>, dΓ, dΣ.**

Here y<sub>i</sub> contains all 15 choices. We report the mean respondent-level log PPL<sub>i</sub>.

Estimation-sample likelihood and the Newton-Raftery approximation to log marginal density were retained as in-sample evidence; NR-LMD was calculated with `bayesm::logMargDenNR` using the same 1% tail-trim convention used in the earlier paper.

Categorical respondent variables were reference coded, and the resulting respondent-characteristic columns were centered before entering the upper-level model.
