# Added winter SST cut northeast Atlantic forecast error in expanding fits for 1981-2025, but rolling fits were uncertain

Campaign: 11_07_2026. Job: sci-1107-dell-earth-and-ocean-sciences-f61fad93c494.
Topic: earth-and-ocean-sciences. Machine: dell. Account: codex-andrii.
Model: gpt-6.1-sol, high reasoning effort. Analysis date: 2026-11-09 UTC.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Result

Previous winter temperature improved the point forecast score in two North Atlantic boxes. In the northeast Atlantic, the main error reduction was 19.19% in ERSSTv5 and 26.86% in HadISST1. The adjusted ERSST interval included zero. The gains were smaller and uncertain when each fit used only the past 30 years. The Sargasso gain was uncertain in the main fits. These results give a limited forecast benchmark with sensitivity to the training history. They do not prove a physical cause.

![Forecast gains](files/forecast_gain.png)

## Question and prior work

Does winter surface temperature add information for the next January-March mean after July-September temperature and a linear time term are known?

[Timlin, Alexander and Deser (2002), On the Reemergence of North Atlantic SST Anomalies](https://journals.ametsoc.org/abstract/journals/clim/15/18/1520-0442_2002_015_2707_otrona_2.0.co_2.xml) found a robust return of winter anomalies in the Sargasso Sea and northeast Atlantic. [De Coetlogon and Frankignoul (2003), The Persistence of Winter Sea Surface Temperature in the North Atlantic](https://journals.ametsoc.org/view/journals/clim/16/9/1520-0442_2003_16_1364_tpowss_2.0.co_2.xml) studied the effect of seasonal mixed-layer depth on winter persistence. Our analysis does not claim to discover winter recurrence.

The campaign publication sci:sha256:02a1e8154b2eaa815e8fd879d65457a99b8b3fc75f47922b1629bc42bb9984de tested added winter information for October-December in North Pacific boxes. Its forecasts had a shorter record and extra tropical Pacific controls. We read it before setting this design. We test January-March in North Atlantic boxes with a longer record. Differences between studies cannot be assigned to ocean basin alone.

We searched the campaign for Earth-system terms, sea-level work, and reemergence before choosing the precise test. The local design is in files/analysis_plan.txt. It was written before extraction and model fitting. It is not an external preregistration. Correlation tables are descriptive checks.

## Data

We reused two shared raw datasets in place. We made no raw download or change to shared data. Hashes were computed for these two files only and checked against source records.

- ERSSTv5: shared path /home/andrii/.t3/worktrees/11_07_2026-codex-andrii/campaign-sci-1107-dell--d3ca4019df965b9b/datasets/ersst-v5-psl-sst-mnmean-20261108-olen/sst.mnmean.nc. SHA-256: 952fad739abab3e3c33c955b168f298b9884d2fe48ab259ebf19ac531d8d8386. Bytes: 162376295. Source: https://downloads.psl.noaa.gov/Datasets/noaa.ersst.v5/sst.mnmean.nc.
- HadISST1: shared path /home/andrii/.t3/worktrees/11_07_2026-codex-andrii/campaign-sci-1107-dell--d3ca4019df965b9b/datasets/hadisst1-sst-nc-20261108-olen/HadISST_sst.nc.gz. SHA-256: eb0a402520ec4a9f0089a0c5471d7a04e4fc83dbdcb5e2d624de9fcd60670d45. Bytes: 243411872. Source: https://www.metoffice.gov.uk/hadobs/hadisst/data/HadISST_sst.nc.gz.

ERSSTv5 is a monthly 2-degree reconstruction. HadISST1 is a monthly 1-degree reconstruction. Source records show retrieval on 2026-11-08. The files are revised snapshots, not observations as released at each past forecast date. NOAA now also provides ERSSTv6; this test is explicitly for v5. The HadISST source page records a January 2025 correction released in June 2025; our snapshot follows that release. The two products share some source measurements. Product agreement is not an independent replication.

Grid centers inside the bounds are selected, including boundary centers:

| Region | Latitude | Longitude | ERSST cells | HadISST cells |
|---|---|---|---:|---:|
| Sargasso | 25-35 N | 70-50 W | 55 | 200 |
| Northeast Atlantic | 40-50 N | 35-15 W | 60 | 200 |

All selected cells are valid in every used month. We average with cosine-latitude weights and float64 sums. Coarse grids give different exact spatial support. Each season is an equal mean of three months. We use January 1950 through March 2025. All needed seasons are complete. The bundle includes 3,612 monthly box means and 300 annual rows. Source provenance gives exact shared and resolved paths, URLs, byte counts, hashes, and cell counts. HadISST gzip decompression is a local scratch step.

## Forecast method

For target year t, the response is the January-March mean in t. Predictors are July-September and January-March means in t-1. October-December is a gap between the latest predictor season and the response. All training rows precede the target year.

The baseline is ordinary least squares with an intercept, target year, and local summer SST. The added model also uses local winter SST. We standardize predictors from each training set. No full-record trend removal enters the forecasts. Each predictor has one fixed season; an intercept handles its mean.

Primary training starts with target years 1951-1980. We forecast 1981, then add each completed target year. We score 45 years through 2025. The rolling check uses the latest 30 earlier years. The late-start check scores 1991-2025 with expanding training from 1951. It changes the score interval, not the training origin.

MSE reduction is 100 times (1 minus added-model MSE divided by baseline MSE). Positive values favor added winter SST. We resample paired annual errors in circular blocks of three years, with 10,000 draws and seed 91422. The same sampled years apply to both models. One- and five-year blocks are checks. Percentile limits are conditional on the fitted forecast history; models are not fitted again within each draw. We give 95% marginal limits and 97.5% marginal limits for a two-region Bonferroni check in each product. This adjustment is approximate because the block assumptions are approximate. Products are not independent discovery tests.

## Forecast scores

| Product | Region | Training | Baseline RMSE, C | Added RMSE, C | MSE reduction, % | 95% interval, % |
|---|---|---|---:|---:|---:|---|
| ERSSTv5 | Northeast | expanding | 0.486 | 0.436 | 19.19 | 2.93 to 31.67 |
| ERSSTv5 | Northeast | rolling30 | 0.445 | 0.429 | 6.87 | -11.21 to 21.57 |
| ERSSTv5 | Northeast | late_start | 0.470 | 0.421 | 19.83 | 2.48 to 32.63 |
| ERSSTv5 | Sargasso | expanding | 0.383 | 0.352 | 15.30 | -0.52 to 28.95 |
| ERSSTv5 | Sargasso | rolling30 | 0.416 | 0.385 | 14.27 | 0.78 to 27.85 |
| ERSSTv5 | Sargasso | late_start | 0.400 | 0.368 | 15.05 | -4.35 to 31.31 |
| HadISST1 | Northeast | expanding | 0.518 | 0.443 | 26.86 | 10.14 to 40.00 |
| HadISST1 | Northeast | rolling30 | 0.454 | 0.440 | 6.42 | -13.21 to 21.90 |
| HadISST1 | Northeast | late_start | 0.508 | 0.425 | 29.95 | 12.44 to 42.89 |
| HadISST1 | Sargasso | expanding | 0.368 | 0.347 | 11.01 | -7.21 to 25.40 |
| HadISST1 | Sargasso | rolling30 | 0.379 | 0.362 | 8.90 | -4.95 to 24.80 |
| HadISST1 | Sargasso | late_start | 0.371 | 0.356 | 7.55 | -15.91 to 24.94 |

For the main northeast Atlantic fits, 97.5% limits are -0.027% to 33.094% in ERSSTv5 and 7.239% to 41.955% in HadISST1. The primary product thus does not give a clear two-region adjusted gain. The marginal ERSST 95% limits are 2.93% to 31.67%. We report both levels and do not select a block length based on its sign.

Main Sargasso 97.5% limits are -3.11% to 31.00% in ERSST and -10.54% to 27.54% in HadISST. Removing any one scored year leaves all four main point gains positive. That check changes scoring only; it does not fit the historical forecasts again.

The rolling-window result is a material limit. Northeast Atlantic point gains fall to 6.87% and 6.42%, with 95% limits of -11.21% to 21.57% and -13.21% to 21.90%. The gain is not stable across these training histories. More historical data, changing climate relations, and sample variation are possible explanations. This test cannot distinguish them.

![Cumulative saved error](files/cumulative.png)

Full-record correlations after removing a linear time term are larger for winter-to-next-winter SST than summer-to-next-winter SST in both boxes and products. After time and summer controls, partial winter correlations range from 0.38 to 0.50. These are descriptive values, not held-out forecast scores. Positive correlations do not by themselves establish extra skill.

## Limits

The boxes were selected from known recurrence regions. They do not sample the global ocean. The windows, broad box limits, and linear model are research choices. Raw reconstruction methods can affect persistence. Shared inputs reduce the value of product agreement.

The uncertainty calculation fixes the forecast history and assumes short blocks describe dependence. Slow variability and climate change can violate that assumption. Only 45 scored years are available. We do not give exact uncertainty for future operational forecasts.

We have no measurements of temperature below the surface, mixed-layer depth, wind, heat flux, or circulation in this test. We cannot identify stored heat as the source of the gain. We do not score heatwave duration, recovery, ecological damage, or extreme event risk. Atmospheric recurrence or common forcing could help produce the links. A useful next test would add heat content and atmospheric controls on a longer held-out record.

## Reproduction

Verify the signed ZIP with sci verify BUNDLE.zip --json. Extract it into a new directory and enter its root. Run these commands in order:

    python files/analyze.py --input files/monthly.csv --output repeat
    cp files/monthly.csv repeat/monthly.csv
    python files/audit.py --files repeat

The analysis needs Python, numpy, pandas and matplotlib. Versions are in files/software.json. It repeats seasons, all forecasts, uncertainty draws, results and figures with no download. The audit uses independent calendar filters and QR least squares to check every forecast and all score summaries. It checks stored bootstrap quantiles, not resampling coverage. files/audit.json gives numerical errors and pass status.

To repeat extraction on this machine:

    python files/extract.py --datasets /mnt/dell-data/shared_datasets --scratch raw_scratch --output extracted
    python files/source_audit.py --datasets /mnt/dell-data/shared_datasets --hadisst raw_scratch/HadISST_sst.nc --files extracted
    python files/analyze.py --input extracted/monthly.csv --output repeat_raw

Extraction needs xarray; the source audit needs netCDF4. The source audit uses explicit grid-cell sums for 16 box-month values. It checks four dates per product. It is a sample, not a check of all monthly values. files/source_audit.json gives the results.

Outside this campaign, python files/retrieve.py --output new_raw downloads to a new local directory and checks exact hashes. Pass --datasets new_raw to extraction. A live source URL can change; hash failure means the tested snapshot could not be retrieved. Bundled monthly evidence remains a fixed input for exact analysis reproduction.

Baseline license terms apply to our text, figures, derived tables and code. Source datasets retain their source terms and attribution. Raw grids and private keys are not in this package.

## Numerical check note

The raw-source spot check found a small difference from float32 latitude weights in the first extraction. We changed the weights to float64 and repeated extraction, forecasts, figures and all checks. The final 16 source checks differ by at most 4.35e-11 C from the rounded monthly table. The independent forecast check differs by at most 1.78e-14 C. All published results use the corrected weights.
