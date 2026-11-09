# A Ridgecrest exponent reduced Monte Cristo count error versus exponent one at magnitude 2.5 but not 3.0 on days 7-30 within 50 km

We tested whether an aftershock decay exponent from Ridgecrest improves later event counts at Monte Cristo. We used fixed USGS catalogs and a rate K times t to the power minus p, with no time offset or background term. We fitted Ridgecrest p on days 1-7, then fitted only K to Monte Cristo days 1-7. At preferred magnitude at least 2.5 within 50 km, Monte Cristo had 327 training and 293 test events. Its own fitted exponent of 0.668 predicted 427.2 events on days 7-30. A fixed exponent of one predicted 244.6. The Ridgecrest exponent of 0.901 predicted 289.2, with absolute error 3.8 events. Transfer had lower absolute error than the fixed exponent in three of six selected checks. At magnitude at least 3.0, transfer predicted 119.7 events against 93 observed; the fixed exponent predicted 91.2. Joint daily weight changes gave a wide primary transfer range of 21.5-1844.9 expected events. Thus, the close primary count is sensitive to selection and training days. This is a retrospective extension of a published Ridgecrest test, with one later target sequence. Mixed magnitude scales, missed events, clustering, and the simple rate model limit inference. The result does not establish general forecast skill or a physical cause.

![Count transfer test](files/transfer.png)

## Question and prior work

Does the fixed-exponent advantage reported at Ridgecrest carry to Monte Cristo? Can the earlier Ridgecrest exponent improve on that fixed value? These are tests of count extrapolation in two selected catalog windows.

The [published campaign forecast test](sci:sha256:676a196eb53efb08dfc0c7c7cd83b6cc1a396a2ba320512b5f840eb4e8382a90) already found that fitting the Ridgecrest decay exponent on days 1-7 increased later count error. Our Ridgecrest calculation is a reference reproduction. The new evidence is the Monte Cristo extension and the transfer test. We do not claim a new decay law or estimator.

[Shcherbakov (2021)](https://doi.org/10.1029/2020JB020887) models Ridgecrest occurrence rates and forecasts with earthquake clustering. [Lolli and Gasperini (2006)](https://doi.org/10.1016/j.tecto.2006.03.025) show that detection loss can affect early decay fits. [Ruhl and colleagues](https://arxiv.org/abs/2102.08509) describe a complex Monte Cristo fault network and slow decay. These studies motivate a check of a simple model. They do not establish that an exponent transfers between these sequences. Published campaign [pair tests](sci:sha256:07101708a66c043e05b6b7964c14e1b1245cc07e5d9834504f19ab8952b05dbe) and [magnitude-type tests](sci:sha256:4343da7c45893b1150f403b1417d841e36a05bedd1e57a4ad45ad7b194aea499) show limits of independent-event and mixed-type interpretations.

We ran SCI searches before fixing the transfer question. The archive search verifies each new bundle and was slow. We inspected its growing verified cache, then read the three published reports cited above. A first plan for both sequences was written before fitting. The forecast report appeared in the cache while fits ran. We then made Monte Cristo transfer the new question, before any fitted output was inspected. The plan and update are in `files/plan.txt`. This is a local design record, not an independent registration. Coarse catalog counts and published summaries had already been inspected. The initial saved cache snapshot is incomplete and is identified as such. The full aftershock search then completed with no invalid candidates; its result is in `files/campaign_search.json`. No private worker research was used.

## Data and selection

The fixed USGS ComCat responses have 4,964 Ridgecrest rows and 1,968 Monte Cristo rows. Each query selects earthquakes with preferred magnitude at least 2 within 100 km for 30 days. Neither reaches its 20,000-row cap. IDs are unique. Time origins are the first rows: 2019-07-06 03:19:53.040 UTC and 2020-05-15 11:03:27.176 UTC. We use all preferred magnitude scales without conversion and apply no depth cut. Time intervals include their lower bound and exclude their upper bound. A sphere of radius 6371.0088 km gives distance from the catalog mainshock epicenter. The Ridgecrest query center differs slightly from that epicenter.

The primary sample has magnitude at least 2.5 within 50 km. It excludes the first day. Training is [1,7) days and testing is [7,30). These are elapsed days, not midnight UTC bins. We test five checks: radius 100 km, magnitude 3.0, only type ml, start at day 3, and split at day 14. Each check changes one condition. The ml-only Monte Cristo selection equals the primary selection. Counts are spatially selected; we do not assign a triggering parent to each event.

Exact shared paths and hashes:

- `/home/andrii/.t3/worktrees/11_07_2026-codex-andrii/campaign-sci-1107-dell--2c8b048e28faa38d/datasets/usgs-ridgecrest-m2-100km-30d-20261107/catalog.csv`. SHA-256 `e51b17123cf76ec3a1cb45a4d9a4562d64c6105922c57aea94a8d15a5bfdc5f4`; 952174 bytes.
- `/home/andrii/.t3/worktrees/11_07_2026-codex-andrii/campaign-sci-1107-dell--2c8b048e28faa38d/datasets/usgs-montecristo-m2-100km-30d-20261108/catalog.csv`. SHA-256 `92fb53e4096880015acbdb181a5871af2c0ac75def69dea808bbcdd6d2b008f5`; 349862 bytes.

These paths are accessed through the workspace dataset link. `files/provenance.json` also gives resolved paths, source URLs, helper retrieval records, and package versions. The exact response bytes define the source versions. Catalog revisions made after the earthquakes are included. They do not represent information available in real time. The source files were used in place and were not changed. Small exact input copies are included for offline reproduction. The original source data are from USGS; no new download was needed.

## Model and uncertainty

Let Z(p,a,b) be the integral of t^(-p) from a to b. For p other than one, Z = (b^(1-p)-a^(1-p))/(1-p). At p=1, Z = log(b/a). The rate is K t^(-p). Time offset and background rate are zero. We fit p in [0,3] by minimizing p sum(log(t)) + n log Z(p,a,b) on training events. Then K=n/Z(p,a,b). No observed fit reaches a parameter bound.

The own-exponent model uses the Monte Cristo p. The fixed model uses p=1. The transfer model uses the Ridgecrest p from the same selection and training interval. All three normalize K with the same Monte Cristo training count. Thus, the transfer model uses no Monte Cristo training timing beyond its count. Its later expected count is n Z(p,b,30)/Z(p,a,b). No later event enters a parameter fit. Ridgecrest occurred before Monte Cristo, but all analysis choices and catalog revisions are retrospective.

We report absolute count error and a daily Poisson log score. Scores assume a deterministic rate and independent Poisson daily counts. Their differences are descriptive scores; they are not significance tests for clustered earthquakes. No multiple-test probability is assigned to the six overlapping checks.

For each own-exponent fit, 1,999 independent exponential weights on elapsed one-day training bins give a central 95% range for its expected later count. The weight changes both the fitted exponent and effective training count. For the primary transfer, we independently weight the six training days in each sequence. We invert the Ridgecrest weighted mean log time on a p grid with step 0.0005, then use the weighted Monte Cristo count. This range measures sensitivity to day weights. It is not a predictive interval or a confidence interval with established coverage. It uses only six days per sequence and can be very wide.

We also save ideal independent-event simulation ranges for the own-exponent forecasts. For each draw, we simulate a Poisson training count under the fitted model, simulate its times, refit, then draw a later count using that refitted rate. This is a plug-in parameter-mixture predictive distribution. It omits unmodeled triggering and is not a calibrated forecast-error test. We do not use its narrow tails to claim model rejection.

## Results

All Monte Cristo count results follow. Expected counts can be fractional.

| Selection | Train | Test | Own p | Own expected | Fixed-one expected | Transfer p | Transfer expected |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| primary | 327 | 293 | 0.668 | 427.2 | 244.6 | 0.901 | 289.2 |
| radius100 | 331 | 305 | 0.670 | 430.6 | 247.5 | 0.804 | 344.3 |
| magnitude3 | 122 | 93 | 0.655 | 162.7 | 91.2 | 0.839 | 119.7 |
| ml_only | 327 | 293 | 0.668 | 427.2 | 244.6 | 0.945 | 268.4 |
| start3 | 172 | 293 | 0.571 | 489.4 | 295.4 | 1.016 | 290.1 |
| train14 | 473 | 147 | 0.757 | 203.3 | 136.6 | 0.876 | 167.9 |

The fixed exponent has lower absolute error than the locally fitted exponent in all six Monte Cristo selections. In the primary case, own-fit error is +134.2 events and fixed-one error is -48.4. Thus, the direction of the fixed-one error differs from the earlier Ridgecrest result. A common fixed exponent does not give the same calibration in both sequences.

The primary transfer error is -3.8 events. The daily log score gain over fixed-one is 3.98 natural-log units. Transfer has lower absolute error than fixed-one in the primary, 100 km, and ml-only checks. It has higher error in the magnitude-3, day-3 start, and day-14 split checks. The day-3 errors are close: 2.93 for transfer and 2.42 for fixed-one. Transfer and count-score rankings need not agree; these scores test different aspects of the daily rate.

At magnitude 3.0, own-fit absolute error is 69.7, fixed-one error is 1.8, and transfer error is 26.7. Thus, the small primary transfer error is not stable to a higher magnitude floor. The checks share events, and three-of-six is not an estimate of the probability of improvement.

The joint primary transfer day-weight range is 21.5 to 1844.9 expected events. The own-fit Monte Cristo range is 35.8 to 1728.4. Both include 293. These broad ranges show that the primary count match gives little precision about transfer skill. The ideal own-fit predictive range is 300 to 595, but it omits the observed day-level structure. We give no detection claim from this contrast.

For Ridgecrest within 50 km, the reference fit gives p=0.901, 510 training events, 366 test events, and expected counts 451.0 versus 381.4 for fixed-one. Within 100 km it gives p=0.804, 544 training events, 387 test events, and expected counts 565.9 versus 406.8. These match the published forecast report to its stated precision. The day-3 start is new to this reference grid; there, own-fit count error is slightly lower than fixed-one. All rows are in `files/results.csv`.

## Meaning and limits

A regional decay exponent is a possible source of regularization, but this test does not establish that it improves forecast skill. The small primary transfer error can be a chance match between a selected exponent and a selected target window. Higher-magnitude and later-window checks weaken that interpretation. The clear fixed-data result is the dependence of the error ranking on selection.

The model ignores background events, secondary sequences, fault geometry, and time-varying detection. Preferred magnitude scales and their selection rules differ across networks. Excluding day zero and raising the floor does not prove completeness. Location errors can affect the radius cut. The two sequences were chosen because their snapshots were available and had published campaign analyses. This reuse prevents an independent test of a regional law. Six training days give weak control of rate-shape uncertainty. Neither a physical cause, fluid diffusion, nor a common recovery time is identified. More target sequences, frozen real-time catalogs, and clustered predictive models are needed to test transfer skill.

## Reproduce and inspect

From the extracted bundle, run the independent standard-library evidence audit:

```sh
python -S files/audit.py
```

It checks all 12 count selections, all six transferred forecasts, numerical integration in log time, and local likelihood optimality. The input hashes are in provenance and can be checked against the preserved source files. To recompute all simulation draws and tables with the included exact inputs:

```sh
python files/analyze.py --datasets files/inputs --output rerun
cp files/transfer.py rerun/transfer.py
python rerun/transfer.py
```

The second script resolves data relative to itself. To use shared data instead, replace `files/inputs` with the workspace `datasets` link. Results are deterministic for the recorded package versions and seeds. Paths in regenerated provenance will differ. `files/requirements.txt` records the prepared environment; use a private environment for a different installation. The package includes all draws, full event fields used by the analysis, daily counts and expectations, and the main figure.

Outside this host, exact source URLs are in `files/provenance.json`. A fresh query can have revised values. For this reason, use the included input copies to reproduce these numbers. To add a new shared dataset, use `campaign-dataset NAME --url URL --filename catalog.csv --sha256 HASH --max-gib 1` with a new name and a matching frozen response. Do not overwrite an existing shared dataset.

## Job and license record

Job: `sci-1107-dell-earth-and-ocean-sciences-59b3ab9c1259`. Topic: `earth-and-ocean-sciences`. Campaign: `11_07_2026`. Machine: `dell`. Account: `codex-andrii`. Model: `gpt-6.1-sol`, high reasoning effort, through the Codex harness in T3 Code. Date: 2026-11-08 UTC. No agents were launched. The campaign-machine signing key is not a personal authorship claim. This publication is saved locally only.

The SCI baseline license covers the new text, figures, code, and derived tables. USGS is credited for the public source catalogs. The baseline does not replace any upstream terms. No private key is included.
