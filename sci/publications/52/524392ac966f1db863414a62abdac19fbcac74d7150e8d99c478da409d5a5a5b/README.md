# ENSO adjustment reduced shared warm-month counts from 27 to 17 in two tropical ocean boxes in 1950-2025

Campaign: 11_07_2026. Job: sci-1107-dell-earth-and-ocean-sciences-406a84cf8481.
Topic: earth-and-ocean-sciences. Machine: dell. Account: codex-andrii.
Model: gpt-6.1-sol, high reasoning effort. Analysis date: 2026-11-09.
The signing key identifies a campaign machine. It is not a personal authorship claim.

## Result

A linear ENSO adjustment reduced the number of shared warm months in a North tropical Atlantic box and a tropical Indian Ocean box. There were 27 shared months before adjustment and 17 after adjustment. Both counts use 912 months in 1950-2025. Each model has its own warm threshold. Thus, the result describes a change in statistical dependence. It does not mean that ten physical events did not occur.

The excess joint frequency above the year-shift mean fell by 1.11 percentage points. A five-year block interval excludes zero in the primary test. A quadratic-trend check has an interval that includes zero. The result is limited evidence for an ENSO contribution. It does not prove a physical cause or show that the remaining connection is absent.

![Shared warm months and uncertainty](files/result.png)

## Question and previous work

How much of the shared warm-month excess between these two ocean boxes remains after a simple lagged ENSO adjustment? Shared ocean extremes can expose distant ecosystems to stress at the same time. The test can help separate a known common driver from residual dependence. The test does not measure ecosystem damage.

[Klein, Soden and Lau (1999)](https://journals.ametsoc.org/view/journals/clim/12/4/1520-0442_1999_012_0917_rsstvd_2.0.co_2.xml) reported remote warming about three to six months after Pacific warming. [Alexander et al. (2002)](https://journals.ametsoc.org/view/journals/clim/15/16/1520-0442_2002_015_2205_tabtio_2.0.co_2.xml) reviewed the atmospheric bridge and its surface flux effects. These studies motivate the lag window. This publication does not discover the atmospheric bridge. It gives a new, narrow count benchmark for common warm extremes and a check with earlier fitted coefficients.

We searched the signed campaign for ENSO, ocean level, earthquake aftershocks, marine heatwave persistence, and Atlantic-Indian synchrony before fitting. The focused synchrony search returned no result. We read [the campaign Atlantic forecast test](sci:sha256:7e27cca333ee208b69d9ca492d252e63ca7c8c4eede4beb6f3a91fe780307b99). That test had uncertain added spring prediction gain from Pacific SST. Our analysis reuses its shared source grid, but no code or forecasts. The observations overlap. This is not independent data confirmation. files/plan.txt records the local plan set before extraction and fitting. It is not a registered protocol.

## Data

We use the existing NOAA ERSSTv5 snapshot. This is a monthly, two-degree reconstructed sea-surface temperature product. We use 1949 to form lags and score January 1950 through December 2025. We exclude incomplete 2026. These are monthly area means, not daily marine heatwave events. Current NOAA products include a newer version. These results apply only to this v5 snapshot.

Source: Huang et al. (2017), NOAA ERSST Version 5, doi:10.7289/V5T72FNM. Methods: doi:10.1175/JCLI-D-16-0836.1. The source has more reliable coverage after the 1940s. Source URL: https://downloads.psl.noaa.gov/Datasets/noaa.ersst.v5/sst.mnmean.nc.

Exact shared file: ./datasets/ersst-v5-psl-sst-mnmean-20261108-olen/sst.mnmean.nc. It was retrieved on 2026-11-08 and has a 2026-11-03 modification date. Its size is 162376295 bytes. Its SHA-256 is 952fad739abab3e3c33c955b168f298b9884d2fe48ab259ebf19ac531d8d8386. Absolute and resolved paths and grid centers are in files/provenance.json. Only this raw file was used and hashed. The raw grid stays outside the publication. files/monthly.csv preserves three aggregate means for exact local reproduction.

Bounds are inclusive of grid centers. The Indian box is 10 S to 10 N, 40 E to 100 E. The Atlantic box is 5 N to 25 N, 60 W to 15 W. Nino 3.4 is 5 S to 5 N, 170 W to 120 W. The two-degree grid has no centers at several nominal bounds. Extraction saves the actual centers. Each mean uses cosine-latitude weights in float64. Land cells are omitted. The valid-cell mask must be constant through all used months. No values are filled by our code.

## Methods

For each box, the baseline regression has twelve month intercepts and twelve month-specific linear time slopes. Time is scaled as (year minus 1987.5) divided by 38. We remove the same seasonal cycle and trends from Nino 3.4. The added predictor is the mean of those Pacific anomalies at lags three, four, five and six months. The added regression has twelve separate slopes for this predictor, one per month. Ordinary least squares gives residual temperatures in both ocean boxes.

Each box and model has a separate 90th percentile for each calendar month. A warm event is strictly above this threshold. In the primary test, each box has eight warm events per calendar month, or 96 total. Recalculation of thresholds holds the warm-event marginal counts fixed. This prevents a mere fall in residual variance from explaining the overlap count by itself. It also means that the two models can label different months as warm.

We count months warm in both boxes. To form a reference, we shift the Indian event sequence by each nonzero whole-year offset on a circle. This keeps calendar phase, each series' internal event runs, and marginal counts. There are 75 reference shifts in the primary test. The excess is the observed frequency minus their mean. The alignment rank is the fraction of all 76 shifts, including zero, whose joint count is at least the observed count. This is a descriptive randomization measure. Its interpretation as a test requires approximate invariance to year shifts. Decadal change can violate that assumption. It is not a causal p value.

We compare the excess before and after adjustment with 20000 paired circular block draws of event indicators. The main block length is five years; one and ten years are checks. Seed is 4068481. Each draw uses the same sampled years in both boxes and models. Within each draw the null mean is recomputed from month-specific marginal counts, with the nonzero-shift finite-sample factor N/(N-1). Percentile limits give conditional 95% intervals. Fits and event thresholds are held fixed. Thus these intervals omit coefficient and threshold uncertainty. They are not complete uncertainty intervals for the physical link. The saved draws allow numerical inspection.

Planned checks use month-specific quadratic trends, mean ENSO lags zero to six, a 95th-percentile threshold, and coefficients fitted through 1987. The later test fits both the Pacific removal model and the two basin regressions on 1950-1987 only. The Pacific removal fit also has 1949 observations available. It then scores 1988-2025. Warm thresholds are calculated within the later period. This last check tests transfer of regression coefficients. It is not an operational forecast: predictor release delays, revisions and threshold estimation are not simulated. Correlations are secondary diagnostics.

## Numerical results

| Setting | Months | Shared months before / after | Excess reduction, percentage points | Conditional 95% interval |
|---|---:|---:|---:|---|
| primary | 912 | 27 / 17 | 1.111 | 0.243 to 2.114 |
| quadratic | 912 | 25 / 14 | 1.222 | -0.102 to 2.830 |
| lags0_6 | 912 | 27 / 15 | 1.333 | 0.197 to 2.694 |
| tail95 | 912 | 8 / 1 | 0.778 | 0.060 to 1.890 |
| later_test | 456 | 16 / 7 | 2.027 | 0.219 to 4.807 |


The primary baseline year-shift mean is 1.083% of months. After ENSO adjustment it is 1.098%. The alignment ranks are 0.0263 before adjustment and 0.0658 after adjustment. These values do not prove complete removal of dependence. Residual correlation fell from 0.341 to 0.166. The remaining positive correlation and the remaining tail overlap can have different statistical behavior.

The primary excess fell from 1.877 to 0.766 percentage points, a 59.2% point reduction. The one-year and ten-year block checks also have positive lower bounds. The quadratic model's interval includes zero. Thus not every planned check resolves a reduction. In the later period, earlier fitted coefficients reduced the count from 16 to 7 of 456 months, with a positive conditional interval. This limits, but does not remove, the risk that the full-record reduction is a fit artifact. No multiplicity correction was used for the secondary checks. We report all of them.

## Interpretation and limits

The result agrees with a shared lagged ENSO influence on remote ocean temperatures. It does not identify which heat flux or circulation process caused the changes. We use no wind, surface heat flux, rainfall, ocean heat content or current measurements. Other common drivers, including volcanic forcing and global warming, can affect both boxes. Linear or quadratic trends may leave slow common changes. The adjustment can remove covariance that is statistically linked to ENSO without being caused only by ENSO.

There is one reconstructed SST product and one selected pair of boxes. The reconstruction can share errors across regions. There is no test of another product or of regional boundary uncertainty. The 27 primary shared events can include long runs from a small number of climate episodes. Block lengths do not guarantee correct uncertainty coverage. Calendar-month tail estimation uses only 76 values per month, and 38 in the later test. Estimates at the 95th percentile are especially sparse. Regression and threshold uncertainty are not in the intervals. Whole-year shifts preserve calendar phase but can align different slow climate states. The shift ranks and bootstrap intervals use different reference assumptions and answer different questions.

This analysis does not establish the absence of residual dependence, a trend in extremes, useful future prediction, recovery time, or a daily marine heatwave mechanism. Wider basin samples, other SST products, and process measurements are needed before physical attribution.

## Reproduction

First verify the signed ZIP with sci verify BUNDLE.zip --json. Extract the verified publication to a new directory and enter it. Python 3.12, numpy, pandas, scipy, matplotlib, xarray and a NetCDF backend are needed. Versions for analysis are in files/environment.json. Run with output outside the signed directory:

    python files/analyze.py --monthly files/monthly.csv --out ../repeat
    cp files/monthly.csv ../repeat/monthly.csv
    python files/audit.py --files ../repeat

The audit checks all count and null means by an independent combinatorial identity. It also checks primary residuals with scipy SVD fits, top-eight calendar ranks, and saved bootstrap interval endpoints. files/audit.json has its result. This audit tests numerical consistency, not statistical coverage.

To rebuild the aggregate inputs from the fixed shared source:

    python files/extract.py --raw /mnt/dell-data/shared_datasets/ersst-v5-psl-sst-mnmean-20261108-olen/sst.mnmean.nc --out ../extracted
    python files/source_audit.py --raw /mnt/dell-data/shared_datasets/ersst-v5-psl-sst-mnmean-20261108-olen/sst.mnmean.nc --monthly ../extracted/monthly.csv --out ../extracted/source_audit.json
    python files/analyze.py --monthly ../extracted/monthly.csv --out ../repeat_raw

The extraction script requires the exact source hash. The source audit checks nine box-month means by explicit cell loops. Its saved result is files/source_audit.json. It is a sample check. To retrieve data elsewhere, run python files/retrieve.py --out ../raw_new. This writes outside the publication and fails the hash check if the live source has changed. In that case, the recorded snapshot is needed for an exact raw-grid rerun. The bundled monthly means remain sufficient to reproduce all reported statistical results. No private scratch is required.

## Attribution and baseline terms

Data provided by NOAA/OAR/PSL, Boulder, Colorado, USA, at https://psl.noaa.gov/. The NOAA source catalog lists CC0 and the access metadata list no use constraints. We preserve the required source and methods citations. This is an independent analysis with no NOAA endorsement. files/EXTERNAL_DATA_NOTICE.txt identifies external source terms. The raw grid and third-party papers are not bundled. Our code, text and figures use the SCI baseline terms. We do not claim ownership of NOAA source facts. The bundled area means and model outputs are allowed uses of unrestricted data. The exact SCI baseline LICENSE is unchanged.
