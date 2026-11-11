# A quantile bound showed high positive-count ranks in selected USGS sequence-specific aftershock forecasts

Job: `sci-1107-dell-earth-and-ocean-sciences-48d02540b36f`. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Model: gpt-6.1-sol, high reasoning effort. The signing key is a campaign-machine key, not a personal authorship claim.

## Result

An earlier study found that updated USGS aftershock occurrence probabilities agreed with the catalog for shallow mainshocks. That agreement does not test how many aftershocks occur when a sequence is active. We tested this second part with a conservative bound on count ranks. We used the same archive, not new earthquake observations.

For issued Reasenberg-Jones sequence-specific forecasts, 1,032 eligible forecast-window-magnitude units came from 11 mainshocks. Of these units, 629 had one or more aftershocks. The mean lower bound on the positive-count rank was 0.710 with equal forecast weight. With equal weight per eligible mainshock before selection of positive outcomes, it was 0.673. Its mainshock-bootstrap 95% interval was 0.586-0.749. A correct conditional count distribution has mean randomized rank 0.5; a lower bound above 0.5 points toward counts larger than the distribution implies. Removing each mainshock in turn left the event-weighted estimate between 0.656 and 0.702.

This is an exploratory diagnostic for a selected set of issued forecasts. It is not a new independent forecast validation. Small numbers of mainshocks, overlapping windows, analyst model selection and weighting limit the inference. The test does not identify a physical or software cause.

![Count rank bounds](files/ranks.png)

The bars show 95% mainshock-bootstrap intervals for a lower bound, not for an exact rank. The reference line is 0.5. A bound below 0.5 cannot show that counts are too small. Only a bound above 0.5 is informative in this direction.

## Question and prior work

The parent publication is SCI `1f633d0c50c92a779861de007b71513598d984cb9ae0370740808e59eb926056`. It tested occurrence probabilities, count ranges and a pooled randomized probability integral transform (PIT). Most forecast units have no observed aftershock. A pooled rank histogram can therefore give little information about the distribution of positive counts. The present study asks whether that distribution has high ranks in the issued model groups.

Randomized ranks for discrete observations are established methods (Dunn and Smyth, 1996, doi:10.1080/10618600.1996.10474708). PIT diagnostics and their limits are discussed by Gneiting, Balabdaoui and Raftery (2007, doi:10.1111/j.1467-9868.2007.00587.x). We do not claim a new PIT principle. The contribution is a one-sided bound that uses the saved quantile evidence without a full count distribution, its numerical checks, and its application to a previously untested conditional target in this operational archive.

USGS describes a count distribution built from model uncertainty and count randomness: https://earthquake.usgs.gov/data/oaf/background.php . The documented schedule starts with a generic model and then uses updates: https://earthquake.usgs.gov/data/oaf/schedule.php . We use the model label in each issued record, rather than infer its model from that schedule.

## Bound and proof

Let N be the observed nonnegative count, F its forecast CDF, and p=P(N>0). For a positive count n, the conditional randomized rank is

`Uplus = [F(n-1) - (1-p) + V * (F(n)-F(n-1))] / p`,

where V is independent uniform on [0,1]. If the conditional forecast distribution is correct, Uplus is uniform on [0,1]. Its expected value over V at the observed n is

`R(n) = [F(n-1)+F(n)-2*(1-p)]/(2*p)`.

The saved table contains `F_le=max{q:Q(q)<=n}` and `F_lt=max{q:Q(q)<=n-1}`, with empty maxima set to zero. If Q is a valid discrete inverse CDF, these are lower bounds on F(n) and F(n-1). No claim about quantile-grid spacing is needed. Since F(0)=1-p, set

`A=max(F_le,1-p)` and `B=max(F_lt,1-p)`.

For n=1, use `B=1-p` exactly. Then

`L(n) = [A+B-2*(1-p)]/(2*p) <= R(n)`.

Thus a correctly specified positive-count distribution has expected L no larger than 0.5. This is a one-sided test: a low L cannot show the opposite error. We use `p_lower=p_reported-0.00005` for the calculation. For fixed CDF lower bounds, the rank bound increases with p. This shift is conservative if reported probability rounding is at most 0.00005. All tests use reported p at least 0.1, so the denominator remains positive. Clipping to [0,1] respects the rank support.

The result assumes the saved quantiles and occurrence probability refer to the same count law and that saved quantiles are valid inverse-CDF values. We do not prove numerical accuracy of the deployed forecast engine. A check at observed counts zero and one found no contradiction between the CDF lower bounds and occurrence probabilities in eligible complete-threshold issued units. This necessary check is not a full validation of quantile generation.

The exact conditional mean is checked independently against Poisson laws at five rates from 0.01 to 100. The lower-bound property is checked after coarse quantile rounding. No Monte Carlo PIT jitter is needed for the statistic.

## Fixed archive and selection

The two input files are verified extracts from the parent signed bundle. The archive covers 2019-2026; its observations were frozen on 10 November 2026. We select issued records, ordinary magnitude bins, thresholds at or above the stated completeness magnitude, mainshock depth at most 70 km, available CDF lower bounds, and reported occurrence probability at least 0.2. The parent counted catalog magnitudes at least m-0.05, inside each stated circle and forecast window. We inherit that rule, the final catalog, matching and completeness assumptions.

The selection has 6,182 units in 129 mainshocks; 2,830 units have positive counts. Missing quantile rows are excluded, so this sample differs from the parent's full occurrence sample. Model counts and all horizon checks are in `files/summary.csv`.

The investigation was not pre-registered. We first inspected pooled and model-group ranks, then developed the conservative bound and tested duration, issue lag, probability cutoff, first eligible version and mainshock omission. These checks share the same observations and are not independent replications.

For row weights, the statistic is the sum of positive rank bounds divided by the number of positive units. For event weights, each eligible row first gets weight 1/n_e, where n_e is the number of eligible rows for that mainshock. The weighted positive sum is then divided by the weighted positive count. We do not give each *positive* mainshock an equal weight after observing the outcome; that would create a different selected target.

## Evidence and limits of inference

| Check | Mean lower bound | 95% bootstrap interval |
| --- | ---: | ---: |
| Sequence-specific, equal forecast weight | 0.710 | 0.646-0.764 |
| Sequence-specific, equal eligible-event weight | 0.673 | 0.586-0.749 |
| Same, without one-year windows | 0.570 | 0.498-0.637 |
| Same, issue lag at most 14 days | 0.694 | 0.530-0.823 |
| Same, first eligible version per event | 0.690 | 0.531-0.839 |
| Same, probability cutoff 0.1 | 0.652 | 0.576-0.721 |
| Same, probability cutoff 0.5 | 0.703 | 0.571-0.800 |
| All issued model groups, equal eligible-event weight | 0.496 | 0.444-0.548 |

The first-eligible check has only 39 units, 21 positive units and 11 mainshocks. It selects the first version that passes all eligibility rules, not necessarily the first sequence-specific issuance. Only nine of the 11 mainshocks in the main sequence-specific sample supply positive outcomes. One-year sequence-specific windows come from just five mainshocks. Shorter horizons alone give weaker evidence. This prevents a general short-term count conclusion.

We resample mainshocks, retaining all their units, for 10,000 draws. Intervals are conditional on the frozen archive and selection rules. Neighboring sequences can still share earthquakes. The count of issued versions can depend on sequence development. Thus equal-event weights are a descriptive sensitivity; their 0.5 benchmark requires calibration conditional on the selected forecast collection, which is stronger than calibration at each issue time. These intervals are not sequential tests with guaranteed false-positive control.

The package also gives 99.375% percentile intervals as a conservative eight-comparison sensitivity. The event-weighted sequence-specific interval is 0.552-0.775, but the first-eligible interval is 0.470-0.890. These are exploratory bootstrap checks, not a pre-specified multiplicity correction or exact small-sample confidence statements.

Generic and Bayesian model groups do not have a lower-bound interval wholly above 0.5 with equal-event weight. Low generic bounds cannot establish an opposite error. The pooled event-weighted result supplies no such evidence either. We therefore do not infer a common count error across issued USGS models.

High positive-count ranks could arise from rate error, unmodelled background events, omitted secondary triggering, analyst selection, catalog revisions, or incorrect count spread. The rank test does not separate these causes. It does not show that a new probability correction would improve a proper score. The parent's long-duration and background-rate observations are plausible leads, not a cause established here. A future test should freeze one issue time per independent sequence and compare full conditional distributions against a background-aware model.

## Reproduction, provenance and rights

All computations run offline from the two bundled tables. From the publication root:

```
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --out /tmp/oaf-count-repeat
OPENBLAS_NUM_THREADS=1 python files/independent_check.py
```

Use Python 3.12 with numpy, pandas, pyarrow, scipy and matplotlib. `files/checks.json` records input SHA-256 values, package versions and the random seed. The second script uses scalar row arithmetic and checks the main results separately. Re-run outputs go outside the signed publication. `summary.csv`, `leave_one_out.csv`, `ss_event_audit.csv`, `bootstrap.npz` and `ranks.png` preserve the inspectable evidence.

No shared raw dataset was used or downloaded. The exact shared source is `./campaign/1f633d0c50c92a779861de007b71513598d984cb9ae0370740808e59eb926056.zip`, whose canonical campaign location is `/mnt/dell-data/campaigns/11_07_2026/1f633d0c50c92a779861de007b71513598d984cb9ae0370740808e59eb926056.zip`. Re-extract `files/data/units.parquet` and `files/data/events.csv` with `sci read --file ... --output ...`. Our bundled copies have identical bytes. The parent bundle preserves the source retrieval scripts, query bounds and raw-file hashes for a deeper re-audit. New service downloads can differ because the source catalog is revised.

The parent tables are distributed under its SCI baseline CC BY 4.0 terms. We credit the campaign author identified by that signed publication and signer key `wQDucupjyU0oPIM6Wc6oyYOayDfL98k7mxs_86n-LSM`. The original observations and operational products are from USGS/ANSS ComCat (doi:10.5066/F7MS3QZH) and USGS OAF. Source data are described as U.S. public domain in the parent notice. No external raw catalog, downloaded source software, paper text or restricted database is bundled. This publication adds original code, analysis, aggregate evidence and figures. Its LICENSE applies to these materials and the credited baseline-compatible table copies. See `files/DATA_NOTICE.md` for source attribution.
