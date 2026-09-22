# Analytical Report Structures

Apply these structures together with the analytical report rules in [SKILL.md](../SKILL.md). Choose a structure that fits the question and reader before drafting. The examples below are adapted from public guidance; they are not mandatory templates or findings from a specific dataset.

## 1. Decision Brief

Use when the reader needs to choose an action. Example question: "Should we expand the rollout of the new feature to all users?"

1. **Executive summary.** Recommended decision, strongest evidence, expected benefit, and material risk.
2. **Question and decision criteria.** What needs to be decided, for whom, and under what conditions an option is acceptable.
3. **Evidence and options.** Comparable results, costs, and limitations; maintaining the current state may also be an option.
4. **Recommendation.** What to start, stop, or change, and what observation would justify revisiting the decision. If evidence is insufficient, specify the next check.
5. **How to reproduce the calculations.** Data, queries, and parameters; keep limitations that affect the decision next to the conclusions.

Based on World Bank guidance: problem, analysis of evidence and options, and recommendations, with an executive summary at the beginning. This structure adapts that logic to product and business decisions. [Policy brief guidance, slides 17–21 and 31–32](https://thedocs.worldbank.org/en/doc/e325f4a236440853757892321dc84413-0320012024/original/D2S4-DevelopingPolicyBriefs.pdf#page=18).

## 2. Review of Meaningful Changes and Anomalies

Use for exploratory analysis without a predetermined explanation. A question is still required, for example: "Which changes in conversion over the month require investigation or a change in action?"

1. **Executive summary.** Most important signals, their practical implications, and investigation priorities.
2. **Comparison scope.** Period, groups, metric definitions, and baseline. Include only the context needed to understand the findings.
3. **Findings in order of importance.** For each: observation → supporting data → business implication → possible action or check. Show group sizes and uncertainty that affects the conclusion.
4. **Outliers and anomalous groups.** Where the deviation occurs, its magnitude, how it was detected, and whether it changes the overall conclusion. This discussion may sit within the relevant finding to avoid repetition.
5. **How to reproduce the review.** Sources, selection rules, queries, and calculations.

The UK Office for National Statistics (ONS) recommends identifying the main messages first, then expanding them in the same order through analysis and charts. Its guidance includes examples from published reviews. [ONS guidance and examples](https://service-manual.ons.gov.uk/content/writing-for-users/writing-main-points-and-analysis).

The absence of meaningful change may also answer the question and justify maintaining current actions. Do not equate usefulness with a requirement to find something sensational.

## 3. Hypothesis Testing or Effect Estimation

Use when the reader needs to know whether a claim is supported and how reliable the result is. Example question: "Does the new registration screen increase the proportion of completed registrations?"

1. **Executive summary.** Answer, effect size, uncertainty, and practical implication.
2. **Question and definitions.** Claim being tested, metric, and conditions under which the answer applies.
3. **Data and method.** Study design, groups, period, observation selection, and calculation. Explain whether the design supports conclusions about the cause of changes.
4. **Results.** Main effect, important differences between groups, outliers, and any checks performed to assess the robustness of the conclusion.
5. **Interpretation and action.** What is supported, what remains a hypothesis, which limitations change the decision, and what to do next.
6. **How to repeat the analysis.** Accessible data, exact queries or code, parameters, and expected results.

Based on the full report structure of the US Centers for Disease Control and Prevention (CDC): introduction, methods, results, and discussion. Its separate summary box addresses what is known, what the study adds, and what this changes in practice. This structure adapts that logic to analytical tasks without importing medical publication requirements. [CDC structure, sections 2.1 and 4.7](https://www.cdc.gov/mmwr/author_guide.html).

## How to Present an Anomaly

An outlier is an observation that differs markedly from comparable observations. A group anomaly is an unusual group metric relative to the selected baseline. State the detection criterion: a visual signal, a domain rule, or a statistical method. Do not present a visual impression as a test result.

Hypothetical example: mobile users have lower conversion than a comparable group. Show both conversion rates, numerators and denominators, the period, and the comparison method. Separately state the hypothesis of a failure and the check for errors at a specific step. The difference alone is insufficient to establish a bug as the cause.

Do not remove outliers merely because they complicate the main conclusion. Investigate possible data errors. If observations are excluded or corrected, state the reason, the number affected, and the impact on the result. This follows the US National Institute of Standards and Technology (NIST) guidance to distinguish erroneous data, random variation, and substantively interesting observations. [NIST explanation of outlier detection](https://itl.nist.gov/div898/handbook/eda/section3/eda35h.htm).

## What to Include for Reproduction

The reader must be able to go from source data to the published number or chart without access to the author's machine. For each main result, provide:

- **Data:** a link or source identifier accessible to the reader, version or preserved snapshot, period and time zone, meaning of a row, and required fields. For a mutable source, an extraction timestamp alone is insufficient: provide a preserved snapshot or a way to retrieve the historical state.
- **Selection and transformations:** filters, joins, deduplication, missing data handling, exclusions, and formulas that affect the result.
- **Code:** a complete runnable SQL query or sufficient code in the report; for a long calculation, an accessible link to a fixed version with its entry point. Illustrative pseudocode and a local path do not replace the calculation.
- **Execution:** parameters, execution order, SQL engine or runtime environment, and relevant dependency versions. For randomized calculations, include random number generator settings where applicable.
- **Comparison:** which query or step produces each table, chart, or metric, and which published result to compare with the repeated calculation. State acceptable numerical differences when they are expected.
- **Access and limitations:** permissions the reader needs and anything unavailable. If source data or code are accessible only to the author, reproducibility is not established. An anonymized example may explain the method but does not by itself reproduce the original results.

The principle of providing data, code, and environment descriptions together is explained in [The Turing Way: Research Compendia](https://book.the-turing-way.org/reproducible-research/compendia/). The impact of software versions is covered in its [Reproducible Environments chapter](https://book.the-turing-way.org/reproducible-research/renv/).

Place short queries next to their results. Put long queries in the methods section or an appendix, with a precise reference from the main text. Use existing accessible sources and appendices within the report. This reference does not require additional files or publication beyond the scope agreed with the user.
