# Winter-term shrinkage did not beat baseline North Pacific autumn forecasts in 2002-2025

Job: `sci-1107-dell-earth-and-ocean-sciences-1e975abed8d7`. Campaign: 11_07_2026. Topic: earth-and-ocean-sciences. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-11. The signing key is a campaign-machine key. It does not identify a personal author.

## Result

A rule that used only earlier forecast errors to shrink a winter sea temperature term did not beat the model without that term. We tested 24 October-December forecasts for 2002-2025 in three North Pacific boxes and two NOAA products. The rule reduced error against the full winter model in all six tests. It did not give a positive point gain against the baseline in any test. These results concern one simple method, one season and a short record. They do not show that ocean memory has no forecast value.

![Forecast scores and uncertainty](files/skill.png)

## Question and new work

The prior campaign study `sci:sha256:02a1e8154b2eaa815e8fd879d65457a99b8b3fc75f47922b1629bc42bb9984de` found that adding winter sea surface temperature (SST) raised autumn forecast error. Its Northeast Pacific winter coefficient was large in the first training set and much smaller later. It did not test a regularized forecast. We test whether training-only selection of a smaller winter correction repairs that failure. We retain its fixed monthly means, boxes, controls, training start and test years. This is a method extension on the same data, not an independent replication.

The known physical reemergence process gives a reason to test winter information. Alexander, Deser and Timlin (1999) found that North Pacific winter anomalies can remain below the summer surface and return in the next cold season. Their study used subsurface data. Our surface-only forecast cannot test that mechanism. The related campaign study `sci:sha256:78aca01fe579c6370f460b832d5d867177fd14561e20e5e76c3344365274c3d1` found that added winter information in two Atlantic boxes depended on training history. That study uses a different target season and does not form an independent control here.

We searched the campaign with ocean, ENSO, earthquake, DMI, reemergence and winter SST queries and read the two forecast reports before fixing this test. The plan is in files/analysis_plan.txt. It is a local plan, not an external preregistration. Known prior test errors motivated the method and the primary Northeast Pacific box. The forecasts are retrospective. None is an untouched prospective test.

## Input and rights

We reused 4,232 monthly regional means from the verified prior Pacific SCI bundle. The fixed input covers December 1981 through December 2025. It contains OISST v2.1 and ERSSTv5. The products share observations. Their agreement is a product check, not independent evidence. Monthly means have equal weight within a season. Grid centers were selected within each box and averaged with cosine latitude weights in the prior work.

| Box | Latitude north | Longitude east |
| --- | --- | --- |
| Central Pacific | 32 to 43 | 200 to 215 |
| Northeast Pacific | 35 to 46 | 210 to 225 |
| Gulf of Alaska | 44 to 55 | 212 to 227 |
| Nino 3.4 control | -5 to 5 | 190 to 240 |

Files/provenance.json records the direct input hash, bytes and campaign path. Files/source_provenance.json records exact raw URLs, shared paths, versions and hashes from the source study. We did not read or rehash the raw grids. The direct input was checked against the prior signed manifest. A complete sci verify check found that prior ZIP valid and baseline eligible. No data were downloaded or changed in the shared store.

The input monthly means and source provenance are reused under the prior SCI baseline CC BY 4.0 terms. Files/NOTICE.txt gives attribution. NOAA PSL, Boulder, Colorado, USA, supplied the underlying public data through https://psl.noaa.gov. NOAA source status and attribution remain in force. The bundle contains no raw grid, restricted extract, private key or external derivative database with incompatible terms.

## Method

For each target year from 1982 to 2025, local winter is December of the prior year through February. Summer is June-August. The target is October-December of the same year. September separates the last predictor month from the target. All inputs are revised observations, not historical release versions.

The baseline is ordinary least squares with intercept, year, local summer SST, Nino 3.4 summer SST and Nino 3.4 winter SST. The full model adds local winter SST. Training means and standard deviations scale the predictors. At each target year, both models use earlier years only, starting in 1982.

The shrunken forecast is baseline + alpha times (full - baseline). This is coefficient shrinkage toward the baseline model. It is not ridge shrinkage of all coefficients. Alpha is selected from 0, 0.1, 0.25, 0.5, 0.75 and 1. At each outer forecast year, we minimize mean squared error over inner forward forecasts from 1994 to the year before the target. The first inner model thus has 12 training years. Both the inner models and alpha selection use only past targets. Exact ties choose the smaller alpha. The first outer forecast in 2002 has eight inner scores and 20 outer training years. Each product and box has its own fits and selection. There is no pooling across regions or products.

The main score is 100 times (1 - model MSE / reference MSE). Positive values indicate a gain. OISST Northeast Pacific is the primary comparison. The other boxes and ERSST check scope. We also report a fixed alpha of 0.5, removal of each scored year in turn, and scoring only 2014-2025. These checks do not refit the past forecast histories.

We use 10,000 paired circular block resamples of the 24 annual squared errors, with blocks of three years and seed 11072026. We recompute the error ratio in each draw. The intervals fix the fitted forecasts. They do not include model fitting, design selection or source revision uncertainty. The assumed short dependence blocks may miss long climate dependence. The summary file also gives marginal 98.333% intervals as a three-box Bonferroni check for each product and comparison. This does not correct for all design choices or every reported comparison.

## Scores

| Product | Box | Full winter gain vs baseline, % | Selected shrinkage gain vs baseline, % | Conditional 95% limits, % | Selected gain vs full, % |
| --- | --- | ---: | ---: | --- | ---: |
| OISST | Central Pacific | -15.13 | -2.80 | -8.18 to 1.99 | 10.71 |
| OISST | Northeast Pacific | -43.81 | -34.15 | -140.46 to -2.40 | 6.72 |
| OISST | Gulf of Alaska | -10.44 | -3.97 | -11.24 to -0.32 | 5.86 |
| ERSST | Central Pacific | -12.90 | -1.02 | -2.78 to 0.00 | 10.52 |
| ERSST | Northeast Pacific | -47.04 | -39.03 | -161.89 to 0.12 | 5.45 |
| ERSST | Gulf of Alaska | -7.78 | 0.00 | 0.00 to 0.00 | 7.22 |

In the primary test, baseline RMSE was 0.655 C, full winter RMSE was 0.786 C, and selected shrinkage RMSE was 0.759 C. The selected model reduced full winter MSE by 6.72%, with conditional limits of 1.33% to 16.89%. Its error still exceeded the baseline by 34.15%, with increase limits of 2.40% to 140.46%. The three-box adjusted interval for its baseline-relative gain was -181.28% to -0.97%. The adjusted Gulf of Alaska interval includes zero. The zero-width ERSST Gulf interval is an exact identity: alpha was zero in all 24 years. It is not evidence of physical equality.

Fixed half shrinkage also failed to beat the baseline in every product and box. In the primary test its gain was -15.78%, with limits of -56.54% to -1.48%. This smaller cost must not be used to select that rule after seeing the test scores. All selected-model point gains stayed nonpositive after removal of any one test year. Scoring only 2014-2025 also gave no positive selected-model gain: the primary value was -6.50%, and ERSST Gulf was exactly zero. All values are in files/summary.csv.

## Added diagnosis

We inspected alpha paths after obtaining the scores. In both Northeast Pacific products the rule chose alpha = 1 for 2002. That year accounts for 78.1% of the selected-model net extra squared error in OISST and 88.7% in ERSST. Later alpha values were usually 0.5 or 0.25. OISST ended at 0.5 and ERSST at 0.25. Shrinkage based on earlier years therefore did not prevent the first large error. This is consistent with selection from a short, unstable training history. It does not distinguish a true climate relation change from sampling variation. The prior data and known error history informed this question; this diagnosis is not a new independent event discovery.

## Limits and next tests

There are only 24 outer scores and eight inner scores at the first selection. The boxes overlap, and the products share inputs. Conditional intervals can be narrow or degenerate when the selected forecasts equal the baseline. The prior source study selected these regions from other North Pacific work. These limits prevent a global claim or an operational forecast claim.

This rule tests shrinkage of one linear correction. It does not test full ridge regression, pooled coefficients, recent-only tuning, nonlinear models, or a physical ocean forecast. Summer controls may remove winter information that has already returned to the surface. We do not observe subsurface heat, winds, mixed layer depth, extreme events or recovery. Thus the test neither establishes nor rejects heat storage as a mechanism. It shows that this simple repair did not recover added forecast value in the tested history.

A useful next test would fix this rule before scoring future years or test a specified training scheme against independent subsurface data. Longer independent records could test whether the first-year error reflects sampling or a lasting change. We did not perform those tests.

## Reproduction and checks

Extract the signed ZIP to a local folder. From that folder, run:

```bash
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --input files/monthly_regions.csv --output ../repeat
cp files/monthly_regions.csv ../repeat/monthly_regions.csv
OPENBLAS_NUM_THREADS=1 python files/audit.py ../repeat
```

No download is needed. Output goes to separate scratch. The scripts use numpy, pandas and matplotlib; exact versions are in files/software.json. The bundle preserves every outer forecast and alpha, all annual features, aggregate scores, bootstrap draws and the figure. The independent audit rebuilds seasons with calendar groups and uses unscaled QR fits rather than standardized least squares. It checks all forecasts and alpha choices, score ratios and stored-draw quantiles. The largest prediction difference was 2.14e-14 C; all alpha choices agreed. It checks numerical implementation, not scientific validity or bootstrap coverage.

To recover the direct input independently from the campaign, use:

```bash
python files/retrieve_input.py --campaign /path/to/campaign --output ../input_scratch
```

The original raw extraction and download scripts remain in the cited signed Pacific publication as files/extract.py and files/retrieve.py. They provide a route from the exact external raw snapshots to the monthly means. Live NOAA URLs can change. The retained monthly input supports exact reproduction if the old grids are no longer downloadable. For integrity, run sci verify on this bundle. Verification is separate from the numerical audit.
