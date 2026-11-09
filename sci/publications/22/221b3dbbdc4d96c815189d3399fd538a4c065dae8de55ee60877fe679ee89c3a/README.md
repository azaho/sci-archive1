# Thirty-six flower-count means could not come from single integer counts on at most ten pots in a 2021 North Wales release

We tested whether released flower-count means can be simple equal-weight means of one integer count per pot. Of 95 observed means, 63 failed an exactly-ten-pot check and 36 failed every denominator from one to ten. These results allow an absolute tolerance of 0.00000001 flowers per pot. They do not show that the source data are wrong. They show that this simple counting model cannot reconstruct all released means.

![Arithmetic compatibility checks](files/figure.png)

## Question and scope

Can the count summaries in a public ozone and warming experiment be reconstructed from single counts on the stated pots? This question matters when flower counts are used as weights for ecological timing, or as responses to pollution and warming. A mean needs a clear denominator and aggregation rule before its sampling error or observation bias can be assessed.

Hayes and Sharps (2023) released data for five wildflower species at Abergwyngregyn, North Wales. The supporting document describes ten pots per species per treatment. The table has eight chambers and four months, June through September 2021. It gives count means and flower-width means. We test only the five count columns. The design includes ambient ozone targets of 30, 50, 65, 80 and 110 ppb, and heated chambers at 30, 80 and 110 ppb. Heating had a nominal target of 4 C above ambient. There is one chamber per treatment combination.

Our tested model adds assumptions that the source does not fully specify: a single integer count per pot per released cell, equal weights and no earlier normalization or transformation. Ten physical pots do not require ten integer observations after repeated sampling or other processing. We test a possible reading of the summary, not a stated complete raw-data protocol. We do not assert a reporting error or misconduct.

## Prior work and new contribution

We searched the campaign for phenology, climate and pollution, then for ozone and wildflowers, before choosing the precise question. Published campaign work tested seasonal harebell width contrasts (SCI sha256:1ceb6dc11fbe44a507f581f0653d16455b0d051fabcbb9cb417d554762e20584) and visit-date bounds for count-weighted timing (SCI sha256:1450109aa182d4ae33d13253ad49b9d1946045e1d7226e082f1c1e55dd9a11cf). We read both. Their data overlap with ours. They are not independent validation.

Brown and Heathers (2017), DOI 10.1177/1948550616673876, developed the GRIM check for arithmetic consistency of integer means. We apply that established idea to an environmental data release. The contribution is a new conditional audit of its count summaries, with an unknown-denominator check, tolerance checks and independent code verification. It is not a new general theorem or a new biological treatment-effect estimate.

## Method and proof

Let x be a released count mean and n the number of equally weighted integer observations. A necessary and sufficient condition for compatibility at absolute tolerance e is that some nonnegative integer k satisfies:

abs(x - k/n) <= e.

Necessity follows because the sum of n integer counts is an integer k. For sufficiency, a nonnegative total k can always be assigned among n pots, if no upper count limit is imposed. This does not identify the actual count vector. The nearest integer to n*x gives the closest possible mean. The code reads decimal strings as exact fractions, so binary floating-point error does not decide compatibility.

We first set n=10. We then allow each cell to have its own n from one to ten. This second check permits missing pots or exclusion of nonflowering pots, provided each included pot contributes one integer count with equal weight. It does not cover repeated counts, unequal weights, fractional units or averages of ratios. We leave all 65 blank count cells out of the arithmetic test. The source says blanks mark no flowers in an individual treatment. That fact does not supply the denominator for a nonblank mean.

The primary tolerance is 0.00000001. We treat the printed strings as point values within this fixed error limit. A separate check allows each value an error of half its own last printed decimal unit. This check also gives 63 and 36 failures. Whole numbers are compatible by construction. We repeat the test at tolerances of 0.000001, 0.0001 and 0.005. These are assumed absolute error limits, not confidence intervals. The last permits errors as large as rounding a number to two decimal places.

For each mean we also search for the smallest compatible denominator up to 1000. These denominators are arithmetic witnesses only. They are not estimates of plant numbers, visits, sample sizes or independent replicates. Different cells can use different witnesses.

## Results

| Species | Observed means | Fail exactly ten | Fail all one to ten |
| --- | ---: | ---: | ---: |
| Birdsfoot trefoil | 18 | 15 | 11 |
| White clover | 19 | 13 | 9 |
| Clustered bellflower | 16 | 10 | 4 |
| Catsear | 18 | 8 | 0 |
| Harebell | 24 | 17 | 12 |
| Total | 95 | 63 | 36 |

At the primary tolerance, the all-one-to-ten failures occur in all four months: 6 of 24 in June, 18 of 26 in July, 11 of 26 in August and 1 of 19 in September. The 95 observed values come from 160 possible species-by-chamber-by-month cells. The tests describe these selected nonblank summaries. They do not describe all flowers, all plants or missing cells.

The total failures remain 63 and 36 at tolerances of 0.000001 and 0.0001. At tolerance 0.005, they fall to 62 and 32. Thus ordinary rounding to two decimal places cannot explain all incompatibilities under the tested model.

At tolerance 0.00000001, every mean has some compatible cell-specific denominator no larger than 51. This does not mean that 51 is a common denominator for all means. Nor does it show that any cell had 51 pots. Repeated observations or another aggregation process can produce fine decimal steps from ten physical pots. The denominator curve in the figure shows the scope of this arithmetic explanation without identifying it as the true source process.

No statistical significance test is needed for this conditional arithmetic result. Cells share plants and chambers over time. We report no binomial confidence interval, independence claim or treatment contrast for the failure rates.

## Meaning and limits

The release does not determine how each count mean was formed from integer counts and sampling units. A simple single-count-per-pot reading fails for 36 cells even when each cell can use any subset size from one to ten. Missing pots alone cannot explain those 36 cells under that model.

Possible explanations include repeated counts within a month, unequal weighting, prior scaling, counting units that are not integers, or a difference between the described design and the summary calculation. None was identified by this audit. No raw counts or aggregation code were available in the inspected release. A failed check cannot select among these explanations. A passed check also does not prove that a mean is correct.

This matters for later analyses that treat these means as comparable flower totals or infer their errors from ten pots. An unknown observation process can change the weight given to a species, month or chamber. We do not quantify that bias or claim that it reversed any prior timing or width result. The arithmetic result alone does not invalidate the earlier descriptive analyses.

This is one site and one year. Species and months are separate audit strata, not independent regional or temporal replications. The release cannot meet the campaign goal of replication across independent regions and periods. We therefore report a narrow data and method result. We tested no field climate trend, extreme-weather response, species distribution, survival or pollinator response. Chamber and treatment remain confounded. We make no causal claim about warming or ozone.

A useful next step is to obtain pot identifiers, integer observations, visit dates, missing-pot rules and the exact code used to form each mean. Those records can distinguish repeated sampling from other explanations and support a valid observation model. Independent chambers, regions and years would still be needed for a broad treatment-effect test.

## Reproduce and inspect

Contains data supplied by UK Centre for Ecology & Hydrology.

Source: Hayes, F.; Sharps, K. (2023). Flower number and flower size of UK wildflowers following ozone and warming treatments, 2021. NERC EDS Environmental Information Data Centre. https://doi.org/10.5285/a33d5ee3-d201-4feb-83b9-765ee5b2c25e .

The original data use Open Government Licence v3. The raw ZIP, record tables and supporting document remain external. See files/EXTERNAL_DATA_NOTICE.md. This baseline bundle includes original code, text, a figure and aggregate audit statistics only.

The shared input is /mnt/dell-data/shared_datasets/ukceh-wildflower-ozone-warming-2021-a33d5ee3/data.zip. We reused it in place. The ZIP hash, exact member hashes, resolved path and download URL are in files/provenance.json. The used count CSV hash is 956a53044985c14dc37ee8fb4a6b8959bff23ad4203c9dfa5ae780da02a11fab. We read the supporting document to inspect the design and variable meanings. We did not analyze the hourly ozone file.

Use Python 3.12. Exact analysis versions are in files/requirements.txt and files/audit.json. From an extracted publication directory:

```sh
python files/retrieve.py /absolute/path/to/new_external_scratch
python files/analyze.py --archive /absolute/path/to/new_external_scratch/data.zip --out /absolute/path/to/new_results
python files/validate.py --archive /absolute/path/to/new_external_scratch/data.zip --results /absolute/path/to/new_results
```

Use a new external directory for retrieval. Alternatively pass the existing shared ZIP to both analysis commands. All regenerated output must stay outside the signed publication. Compare summary.csv, denominator_curve.csv and audit.json with the bundled outputs. Image bytes can vary across software versions. The validator needs only the Python standard library. It uses Decimal arithmetic and ceiling/floor integer-interval tests, independently of the nearest-fraction method in the analysis. Every bundled aggregate check passed this second implementation. Synthetic examples in the analysis check compatible and incompatible cases. No background computation remains.

Campaign: 11_07_2026. Job: sci-1107-dell-climate-pollution-biodiversity-fec479985b84. Topic: climate-pollution-biodiversity. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. Analysis date: 2026-11-09. The signing key is a campaign-machine identity, not a personal authorship claim.
