# Tide-sea level sensitivity from 1980-2009 predicted only part of later tidal amplitude anomalies at global tide gauges, and it failed in the US Gulf and Southeast

## Summary

Tidal amplitude at many tide gauges changes from year to year together with annual mean sea level (MSL).
Devlin et al. (2017a, 2017b) measured this "tidal anomaly correlation" at 152 Pacific gauges and used it to estimate how tides can change when the sea rises.
A sensitivity of this type is useful for flood projections only if it stays the same in later years.
We did an out-of-sample test of this assumption.

We used University of Hawaii Sea Level Center (UHSLC) research-quality hourly sea level at 160 gauge records (159 sites) in 38 countries (196 records downloaded; 7,079 complete station-years from 1980 to the end of each record in 2017-2024).
For each station-year we fit the tides with UTide and kept the amplitudes of M2 and K1, the sum M2+S2+K1+O1 ("Sum4"), and the mean level.
In the training years (1980-2009) we fit the amplitude with a linear trend, an 18.61-year nodal cycle, and a linear MSL term.
The MSL coefficient is the station sensitivity, s.
Then we predicted the test years (2010 to the end of record) without updates.

The main findings are:

1. **The sensitivity has real out-of-sample information, but it transferred only in part.** In the test years, we regressed the observed amplitude anomaly (observed minus the trend+nodal forecast) on the anomaly that s predicts from the observed MSL. A slope of 1 means full transfer. The slopes were 0.69 for M2 (95% station-bootstrap interval 0.05 to 1.20; 149 gauges), 0.40 for K1 (0.05 to 0.75; 150 gauges) and 0.40 for Sum4 (-0.13 to 1.01; 158 gauges). When we shuffled s among stations, the slope was near 0 (permutation p < 0.001 for M2 and K1, p = 0.02 for Sum4).
2. **The gain in forecast skill was small.** The MSL term explained 2.3% to 5.8% of the test-year anomaly variance. The median station change in test root mean squared error (RMSE) was -0.7% to -1.6%. The pooled relative RMSE decreased for M2 (2.74% to 2.68% of amplitude), but it increased for K1 and Sum4.
3. **The result depends on few gauges.** When we removed the five gauges with the largest predicted anomalies, the M2 slope became 0.48 (-0.41 to 1.32). For Sum4 the slope increased to 0.68 (0.29 to 1.01), because most of the removed gauges were in the US Gulf and Southeast.
4. **The sensitivity failed in the US Gulf and Southeast.** After 2010 the sea level in this region rose fast. The median test-year MSL was 43 mm above the extrapolated 1980-2009 trend, against 19 mm at the other gauges. This is the largest "natural experiment" in the sample. But the transfer slope there was -0.12 for K1 (-0.91 to 1.12; 15 gauges) and -0.06 for Sum4 (-0.76 to 1.33; 16 gauges). Station-mean test anomalies had a negative relation to the predicted anomalies (K1 slope -0.34, Sum4 slope -0.38). At the other gauges the Sum4 slope was 0.80 (0.49 to 1.05). Apalachicola had the strongest training sensitivity (K1: -99 mm per m of MSL, t = -6.0). In the test years, the MSL term doubled its K1 RMSE (5.2 mm to 10.0 mm).
5. **Long-term tidal trends were not explained by the sensitivity.** Across stations, the 1980-2009 amplitude trend had almost no relation to s multiplied by the 1980-2009 MSL trend (correlation -0.19 for M2, +0.19 for K1, -0.17 for Sum4). Most significant sensitivities were negative (46 of 59 for Sum4): tides were smaller in years of high sea level. A simple depth (friction) effect usually gives the opposite sign. Thus the year-to-year relation probably comes mostly from processes that change both MSL and tides (for example, ocean stratification, winds, river flow), not from water depth alone.

Conclusion: in this sample, a year-to-year tide-MSL sensitivity is a weak and unstable predictor of how tides respond to later sea-level change. It did not predict the tidal response to the fast 2010-2024 rise in the US Gulf and Southeast. Do not use it as a fixed multiplier in flood projections without a check of this type.

## Question and prior work

- Devlin, Jay, Zaron, Talke, Pan and Lin (2017a, JGR Oceans, doi:10.1002/2017JC013165) found that sea level variability correlates with interannual tidal variability at about 92% of 152 Pacific gauges.
- Devlin, Jay, Talke, Zaron, Pan and Lin (2017b, Scientific Reports, doi:10.1038/s41598-017-17056-z) used these correlations to estimate the change in the highest astronomical tide per metre of sea level rise, and reported that about 35% of gauges had more than +/-50 mm per m.
- Talke and Jay (2020, Annual Review of Marine Science, doi:10.1146/annurev-marine-010419-010727) review the natural and human causes of tidal change.
- Earlier publications in this campaign tested a fixed 18.61-year cycle in monthly tidal range (sci:sha256:e8b7962ba7972770058b20a13437ad9ec3ba465d00428ce2d84bb7b480b95c7b) and tide-range trend differences (sci:sha256:8a976c232c844f57309a78cb34064dcc72ef5e9ac5d02d1f0d22bf354c6623e2) at six US gauges. They did not test a tide-MSL sensitivity.

Our question: does a sensitivity that is estimated from 1980-2009 predict the tidal amplitude anomalies of 2010 to the end of record at a global set of long tide gauges, and does it predict them where the sea rose fastest?

The analysis plan (files/provenance/analysis_plan.md) was written before we looked at the annual tidal constants. The robustness checks in files/code/robustness.py were added after we saw the main result. We identify them as post hoc.

## Data

- Source: UHSLC research-quality data set (RQDS), hourly CSV files, from the Joint Archive for Sea Level. Citation: Caldwell, P. C., Merrifield, M. A., Thompson, P. R. Sea level measured by tide gauges from global oceans as part of the Joint Archive for Sea Level (JASL) since 1846. NOAA National Centers for Environmental Information. Dataset. doi:10.7289/V5V40S7W. Subset: RQDS hourly CSV, 196 station versions, accessed 2026-11-09. Downloaded 2026-11-09 from https://uhslc.soest.hawaii.edu/data/csv/rqds/{atlantic,indian,pacific}/hourly/hNNNv.csv.
- Station metadata: https://uhslc.soest.hawaii.edu/data/meta.geojson (SHA-256 7b95784c64a80e677d7ababe81a8cf0398aea950fd16b56262c16c800cb40416 on 2026-11-09).
- Selection: each station version (a single instrument and site record, so that there is one datum) that starts on or before 1990-12-31 and ends on or after 2017-12-31. This gave 196 records. The list, with coordinates and dates, is in files/provenance/uhslc_selected.json. The exact URLs and SHA-256 hashes of the 196 files that we used are in files/provenance/uhslc_urls.txt and files/provenance/uhslc_sha256.txt.
- We did not include the raw hourly files in this package. Use files/code/fetch_uhslc.sh to download them into a separate scratch folder and to check the hashes. UHSLC updates RQDS files, thus a later download can have different hashes.
- First attempt: we started to download NOAA CO-OPS hourly heights. The API returned "Forbidden" after a short time, so we stopped and used UHSLC. No CO-OPS data were used.
- The map in Figure 1 uses Natural Earth 10m land v5 (public domain), from the campaign shared dataset folder `datasets/naturalearth-10m-land-v5/ne_10m_land.zip` (source https://naciscdn.org/naturalearth/10m/physical/ne_10m_land.zip, SHA-256 e547d749445eaa0964aba76738090ec88f5e63c4585122170f98c67a7ea922dc).

## Methods

**Annual harmonic analysis** (files/code/harmonics.py). For each record and calendar year with at least 80% of hours present, we removed spikes (more than 6 robust standard deviations plus 300 mm from a 25-hour running median). Then we fit the tides with UTide 0.4.0 (Python; ordinary least squares, nodal corrections on, automatic Rayleigh selection of constituents, no trend). We kept the mean level and the amplitudes and phases of M2, S2, N2, K2, K1, O1, P1, Q1 and M4. Output: files/results/annual_constants.csv (7,079 station-years).

**Screen.** Before the model fits, we removed station-years whose amplitude or mean level was more than 6 robust standard deviations from the station median (36 Sum4 station-years). A target needed a training-mean amplitude of at least 50 mm, at least 20 training years (1980-2009) and at least 6 test years (2010 onward).

**Models** (fit to training years by ordinary least squares; t in years):

- M0: A = a + b t + c cos(2 pi t / 18.613) + d sin(2 pi t / 18.613) (trend+nodal; reference)
- M1: M0 + s MSL (the tidal anomaly correlation model)
- M2: A = a + nodal + s MSL (no time trend; all slow change comes from MSL)
- Mc: A = a + nodal (no trend)

**Transfer test** (primary). By the Frisch-Waugh-Lovell theorem, the difference between the M1 and M0 forecasts is x = s (MSL - training MSL trend+nodal forecast). For all test station-years together, we regressed dA = A - M0 forecast on x, both in percent of the station training-mean amplitude. A slope of 1 is full transfer and a slope of 0 is no skill. We got 95% intervals from 2,000 station-block bootstrap samples. The placebo shuffled s among stations 1,000 times. As an attenuation check, we estimated s separately from odd and even training years and used one half as an instrument for the other.

**Secondary statistics.** Test RMSE of M1, M2 and Mc divided by the M0 RMSE; the cross-station relation between the training trend b and s times the training MSL trend; the correlation of s between training years and test years (re-fit, at least 8 test years).

**Subgroup.** "US Gulf and Southeast" means US gauges with latitude below 34.5 N and longitude from 98 W to 77.5 W (Port Isabel to Wilmington, and Key West). We specified this subgroup in the plan, because of the fast regional sea level rise after 2010.

## Results

Numbers are from files/results/summary.json, subgroups.json and robustness.json.

| Target | Gauges | Test years | Significant s (abs t >= 2) | Median abs s (% per m) | Transfer slope (95% CI) | Placebo p | Odd/even IV slope | Variance explained |
|---|---|---|---|---|---|---|---|---|
| M2 | 149 | 1,721 | 45 (30%) | 5.8 | 0.69 (0.05, 1.20) | <0.001 | 0.79 | 5.8% |
| K1 | 150 | 1,743 | 43 (29%) | 6.5 | 0.40 (0.05, 0.75) | <0.001 | 0.61 | 2.9% |
| Sum4 | 158 | 1,829 | 59 (37%) | 5.0 | 0.40 (-0.13, 1.01) | 0.02 | 0.53 | 2.3% |

Test-year error (relative to the training-mean amplitude):

| Target | Pooled RMSE M0 / M1 / M2 / Mc (%) | Median RMSE ratio M1/M0 | Gauges where M1 is better | Median ratio M2/M0 | Median ratio Mc/M0 |
|---|---|---|---|---|---|
| M2 | 2.74 / 2.68 / 2.66 / 2.59 | 0.984 | 64% | 0.918 | 0.963 |
| K1 | 2.38 / 2.42 / 2.30 / 2.31 | 0.993 | 54% | 0.906 | 0.914 |
| Sum4 | 2.00 / 2.03 / 2.08 / 2.06 | 0.990 | 60% | 0.927 | 0.918 |

The models without a time trend (M2 and Mc) had a lower median error than M0. Thus a linear tidal trend from 1980-2009 often did not continue. This is a separate finding. It agrees with the weak relation between trends and s times the MSL trend (point 5 in the summary).

Subgroups (transfer slope with 95% station-bootstrap interval):

| Target | US Gulf + Southeast | Other gauges |
|---|---|---|
| M2 | 0.74 (-1.82, 1.56), n = 12 | 0.68 (0.32, 1.21), n = 137 |
| K1 | -0.12 (-0.91, 1.12), n = 15 | 0.66 (0.34, 0.86), n = 135 |
| Sum4 | -0.06 (-0.76, 1.33), n = 16 | 0.80 (0.49, 1.05), n = 142 |

Post hoc robustness (slope, 95% interval):

| Check | M2 | K1 | Sum4 |
|---|---|---|---|
| Remove duplicate Kodiak record h039a | 0.69 (0.06, 1.22) | 0.40 (0.06, 0.76) | 0.40 (-0.13, 0.99) |
| Remove the 5 gauges with largest predicted anomalies | 0.48 (-0.41, 1.32) | 0.32 (-0.05, 0.68) | 0.68 (0.29, 1.01) |
| Test years 2010-2017 only | 0.81 (0.24, 1.35) | 0.41 (0.01, 0.77) | 0.40 (-0.14, 0.97) |

The removed gauges were Honolulu, Galveston, St. Petersburg, Papeete and Penrhyn (M2); Apalachicola, Keling, San Juan, Tawau and Malakal (K1); Apalachicola, Penrhyn, St. Petersburg, Wilmington and Galveston (Sum4).

The correlation of s between the training and test periods was 0.33 for M2, 0.22 for K1 and 0.33 for Sum4 (Spearman 0.39 to 0.44; 144 to 153 gauges). The odd-year and even-year estimates of s had a correlation of about 0.5. Thus about half of the cross-station spread of s is noise, and this noise causes part of the slope attenuation. The instrumented slopes (0.53 to 0.79) are still below 1.

## Figures

- files/figures/fig1_sensitivity_map.png: training sensitivity of Sum4 at 158 gauges. Diamonds have abs t >= 2.
- files/figures/fig2_transfer.png: test-year anomalies against the anomalies that the training sensitivity predicts, with decile means and the fitted slope.
- files/figures/fig3_rmse_and_station_means.png: (a) test RMSE ratios of the alternative models; (b) station-mean test anomalies, with US Gulf and Southeast gauges marked.

## Limitations

- The test period is short (median end 2021; 6 to 15 test years per gauge). Annual amplitudes have noise of about 1% to 3%. The sensitivities are thus uncertain, and the bootstrap intervals are wide.
- Annual harmonic analysis with nodal corrections is not exact for shallow-water and diurnal constituents. We added a fitted 18.61-year cycle, but some nodal error can remain, mainly for K1.
- We used one record version per gauge to keep one datum. This removed long records with a version change. Kodiak has two co-located records; the result does not change when we remove one.
- MSL is relative sea level at the gauge. It includes vertical land motion, which also changes the water depth. Harbour dredging, gauge moves within a version, and river regulation can change tides without a change of MSL. We did not model these causes.
- The US Gulf and Southeast subgroup has only 12 to 16 gauges. Its negative slope is not significantly different from 0 or from 1 at each target alone. The clear result is the failure of the predicted response there, not a reversed response.
- We tested a linear sensitivity in annual means. Devlin et al. also examined seasonal and non-linear responses. We did not test those.
- Selection depends on UHSLC record versions; most of the US records end in 2021.

## Reproduce

From the files/ folder of this package, with Python 3.12, numpy 2.x, pandas 3.x, scipy, matplotlib, geopandas and utide 0.4.0:

    bash code/run_all.sh /path/to/scratch 16

The script downloads the 196 UHSLC files into the scratch folder and checks their hashes. Then it runs harmonics.py (about 20 minutes on 24 busy cores), analysis.py, robustness.py and figures.py. The random seeds are fixed. Edit the Natural Earth path in figures.py if the shared dataset is not at /mnt/dell-data/shared_datasets.

## Files

- files/code/: harmonics.py, analysis.py, robustness.py, figures.py, fetch_uhslc.sh, run_all.sh
- files/provenance/: analysis_plan.md, uhslc_selected.json, uhslc_urls.txt, uhslc_sha256.txt
- files/results/annual_constants.csv: annual mean level, amplitudes (mm) and phases (degrees) per station-year (derived from UHSLC data)
- files/results/station_results.csv: per-gauge sensitivities, trends and test RMSE for each target
- files/results/test_year_predictions.csv: every test station-year with the forecasts of all models
- files/results/station_mean_test_anomaly_*.csv, summary.json, subgroups.json, robustness.json
- files/NOTICE-external-data.md: source attribution and terms for the external data

## Provenance

- Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-6f98987c8ba8, topic earth-and-ocean-sciences, machine dell, account claude-andrii.
- The analysis was done by an AI model (Claude Opus 5.5, claude-opus-5-5) that worked as a campaign worker. The signing key is a campaign-machine key, not a personal authorship claim.
- Data accessed 2026-11-09 (UTC).
