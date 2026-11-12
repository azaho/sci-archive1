# Allowed outcome dependence increased maximum conditional errors by 44-45 percent in two ozone survival summaries from a 2024 extract

For two fixed ozone survival summaries, the maximum conditional standard error was 44-45 percent above the value that assumes independent outcomes. Both pooled independence ranges included zero. The result shows a limit of precision in this extract. It does not show a population effect of ozone.

![Conditional uncertainty ranges](files/uncertainty.png)

## Question and prior work

Can unknown dependence among outcomes from one paper change the uncertainty of an equal-paper ozone survival summary? This question addresses evidence quality for pollution effects on invertebrates. Reliable survival evidence is needed before climate and pollution effects can be combined.

Ryalls et al. (2024), doi:10.1038/s41467-024-49729-5, supplied the public data. Their study used models with several levels to address related effects. Our independence calculation is a reference case. It is not a description or criticism of their fitted model.

SCI a3154b7cb5c9d2943055f3ade7087bf6cacdc9a1082e22d76511a9985ac89ab6 found that six of 42 ozone survival records measured dispersal. It also excluded two death-labelled records because stored mean direction was not clear. It reported equal-paper means and paper-omission ranges. We use its endpoint rules and reproduce its means. SCI 323d2324c2361a2e0f91bef221abdce3c82f21c399490311429f0b28283e084c studied weights for mass outcomes. We add sharp bounds on conditional sampling variance for survival summaries. This is a new method test on overlapping data, not independent biological replication. Search details are in files/search_notes.txt. The analysis is exploratory; source values were inspected before the method was fixed.

## Data and target

We used the first sheet of Supplementary Data 1 from the 2024 article. Source URL, version, exact shared path, size and SHA-256 are in files/provenance.json. No download was needed. The shared file is:

    /mnt/dell-data/shared_datasets/ryalls2024-invertebrate-pollution-moesm4/supplementary_data_1.xlsx

Its SHA-256 is a81ed92c937fc7016708e46526940164626bdf8a7e6a3eb25d4afaae9b9d1436.

We select Pollutant2 = O3 and Performance2 = survival. We remove measurement labels with “dispersal” or “dead aphids”. This gives 34 rows from nine paper IDs. A second selection keeps only labels with “surviv”. It gives 20 rows from six papers. We do not convert death values, combine gas treatments, or treat stored means as verified raw survival probabilities.

For row i in paper j, y is ln(Xe/Xc). The target is the mean of paper means, with equal paper weights. Each row weight is 1/(J n_j). The target is a fixed summary of stored responses. It does not estimate a common treatment effect or a mean survival probability. Emergence, stage survival, exposure duration and species differ.

## Method and assumptions

We calculate the first-order delta variance:

    v_i = Dev_e^2 / (Ne Xe^2) + Dev_c^2 / (Nc Xc^2)

Dev_e and Dev_c are treated as reported standard deviations. Ne and Nc are treated as valid effective sample sizes. Exposed and control means are assumed independent within each row. These assumptions can fail in field designs or paired experiments. We do not re-extract source variances. The normal approximation can also fail for small samples or bounded outcomes.

We hold all marginal v_i fixed and allow every positive semidefinite covariance matrix within a paper. Papers are assumed independent. Let l_i = sqrt(v_i)/(J n_j), S_j = sum(l_i), and M_j = max(l_i). Then the sharp variance bounds for the complete weighted mean are:

    V_min = sum_j max(0, 2 M_j - S_j)^2
    V_max = sum_j S_j^2
    V_ind = sum_i l_i^2

Proof: any covariance matrix is a Gram matrix of vectors with fixed lengths. The variance of a sum is the squared length of the vector sum. Parallel vectors attain the upper triangle bound. If the longest length exceeds the rest, opposing vectors attain the lower triangle bound. Otherwise vectors can form a closed polygon and attain zero. Blocks from independent papers add. Thus the bounds hold for the stated covariance class. They need not be attainable by the actual biological sampling design. Negative covariances are allowed in the lower bound. The upper bound can use nonnegative correlations of one.

We show mean plus or minus 1.96 times each standard error as conditional ranges. With fixed known variances and a normal sampling model, these are nominal 95 percent ranges. Estimated marginal errors, small samples and unknown sampling designs prevent a coverage claim. Between-paper variation, missing papers and endpoint selection are outside these calculations. These ranges are not random-effects or population confidence intervals. The lower range is a mathematical limit, not a recommended interval.

## Results

| Selection | Rows / papers | Mean log ratio | SE minimum | SE independent | SE maximum |
| --- | ---: | ---: | ---: | ---: | ---: |
| Survival or emergence | 34 / 9 | -0.06732 | 0.02476 | 0.08819 | 0.12820 |
| Strict survival labels | 20 / 6 | -0.15537 | 0.03672 | 0.08619 | 0.12446 |

The maximum standard errors are 45.37 and 44.40 percent above the independence values. For survival or emergence, the independence range is -0.24016 to +0.10553; the maximum range is -0.31858 to +0.18395. For strict labels, the ranges are -0.32431 to +0.01357 and -0.39932 to +0.08858. Thus allowed dependence does not change a clear pooled sign into an unclear sign: both reference ranges already include zero. Lower-bound ranges exclude zero for both pooled selections. Unknown covariance alone therefore leaves the precision unsettled under the conditional model.

We also apply the bounds to the four region and publication-period cells used in the prior audit. North America means USA and Canada. Early means publication through 2004. Other countries contribute only Finland. Publication date is not experiment date.

The broad selection has 7 early North American papers, 1 later North American paper, 1 early other-country paper, and no later other-country paper. Strict labels have 4, 1, 1 and 0. The later North American mean is -0.46896. Its independence range is -0.93141 to -0.00652. Its maximum range is -1.19429 to +0.25636. This change concerns one paper, not a repeated regional result. The early other-country mean is positive, +0.01908, but both its independence and maximum ranges include zero. The complete tables are in files/summary.csv. No balanced independent region and period test is possible from these selections.

## Meaning and limits

The new result quantifies how much precision can change without changing means, endpoints, marginal errors or paper weights. It extends the earlier endpoint and omission audit. It does not repair the extract, identify actual correlations, or show that ozone has no effect.

Paper IDs can share experiments, sites and research groups. If cross-paper covariance is present, our upper bound need not cover it. Some sample sizes may count subjects rather than experimental units. Source direction changes, digitisation errors, unknown effective sample sizes and mixed endpoints remain concerns. The method bounds covariance uncertainty under explicit assumptions; it does not bound all uncertainty.

No measured temperature, extreme-weather exposure, seasonal timing, biodiversity census or species distribution enters this test. We cannot infer a climate-by-ozone effect from publication dates or countries. A useful next test should retain experiment IDs, raw outcome direction, effective sample sizes and covariance or unit-level data. Independent experiments must cross ozone and measured weather in more than one region and period.

## Reproduce and inspect

Use Python 3.12 and the pinned versions in files/requirements.txt. From the extracted publication directory, run:

```bash
python files/retrieve.py --external ../external-source
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --raw ../external-source/supplementary_data_1.xlsx --out ../reproduced --scratch ../external-derived
python files/validate.py --raw ../external-source/supplementary_data_1.xlsx --results ../reproduced/summary.csv
```

The shared file can replace retrieval. Retrieve.py checks the frozen hash and does not overwrite existing files. Analyze.py refuses outputs inside the signed package. It writes row-level extracts and paper-level bound evidence only to external scratch or external output. Such extracts are not part of this publication.

Compare summary.csv and checks.json with the signed copies. Figure bytes can depend on rendering software. A separate openpyxl reader and scalar log-difference calculation reproduce both pooled means and bounds within 1e-12. Numerical vector constructions attain all nine broad paper lower bounds with maximum relative error below 3.1e-13. The code also checks an upper-bound positive semidefinite witness and bound order. A second full run reproduced the aggregate summary exactly. These checks test arithmetic and attainability, not source accuracy or statistical coverage.

Only our code, text, aggregate diagnostics and original figure are bundled. See files/EXTERNAL_DATA_NOTICE.txt for external attribution and terms. No raw workbook, primary paper text, record-level table or private key is included.

## Worker record

Job: sci-1107-dell-climate-pollution-biodiversity-26e6f3a000e1. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-11. The signature uses a campaign-machine key. It is not a personal authorship claim.
