# In 16 homogenised DOISST v2.1 versions (60S-60N, 1982-2025), heatwave-day, frequency and record-year results survive; the flat peak-intensity trend and cold-spell lengthening do not

## Summary

NOAA Daily OISST v2.1 (DOISST) is the main daily sea surface temperature (SST) record for marine heatwave (MHW) and marine cold-spell (MCS) results. Campaign work found two kinds of artifacts in DOISST: steps in fast (sub-monthly) variance at satellite input changes, and steps in the mean (1985, 2005, 7 July 2020) plus a ship adjustment that is too large early in the record. Each earlier study corrected one kind of artifact with one set of choices. Thus it was not known which published results stay true for all reasonable corrections, and which results depend on the correction choice.

We built a homogenisation ensemble with 16 members. Each member is DOISST with one mean correction and one noise correction. The four mean corrections are: step fields fitted on HadSST4.2, step fields fitted on ERSSTv5, the mean of both without the ship term, and half of the combined correction (this member agrees with the drift of DOISST against moored buoys and Argo). The four noise targets give all input segments the fast-variance spectrum of 1985-2006 (noise added), 2007-2015, 2016-2020 or 2021-2025. We computed 17 standard statistics (Hobday et al. 2016 and 2018 definitions, 1983-2012 baseline) for 29,129 ice-free one-degree cells (60S-60N, 1982-2025), and the daily 60S-60N mean SST. We then tested 29 published global results and 8 trends in 22 regions. A result "survives" if all 16 members agree with it and the published value is inside the ensemble range.

Main results:

1. **The mean correction overshoots at moored buoys.** Published DOISST drifts by +0.034 C per decade against 142 moored buoys (95% interval 0.024 to 0.040). The full mean corrections drift by -0.017 to -0.021 C per decade. The half correction drifts by +0.007 (0.002 to 0.013). At the buoys the correction is too large at the 2016-01-01 and 2020-07-07 dates. DOISST is locally tied to buoy data, so a smooth regional correction is too large at buoy cells. Thus we kept the half correction as a member, and we treat the true mean correction as uncertain by a factor of about two.
2. **These results survive (all members agree, published value inside the range):** the rise of MHW days (published +21.2, ensemble +13.5 to +22.2 days per decade), of MHW frequency (+0.66; +0.54 to +0.86 events per decade), of category II+ MHW days (+2.66; +2.61 to +3.89), and of days above a fixed 99th percentile. The decrease of MCS days (-8.3; -10.1 to -6.0 days per decade, 1982-2020) survives. The 2023 record year for MHW days, category II+ days and cumulative intensity survives, and 2024 has more MHW days than 2023 in every member. The Frolicher et al. (2018) doubling of 99th-percentile days from 1982 to 2016 survives: 5-year means increase 2.3 to 4.3 times.
3. **These signs survive, but the published size is outside the ensemble range:** MHW duration trend (published +4.45; ensemble +1.53 to +4.21 days per decade; the members with the buoy-like 2016-2020 noise give +2.34 to +2.71), the annual maximum anomaly trend (published +0.108, ensemble +0.140 to +0.187 C per decade), the annual minimum anomaly trend (published +0.291, ensemble +0.137 to +0.192), the mean warming (published 0.190, ensemble 0.143 to 0.170), the size of the 2023 MHW-day excess (3.5 against 2.8 to 3.1 times the 1982-2022 mean) and of the 2023 duration excess (3.2 against 1.7 to 2.6 times).
4. **These published results do not survive.**
   - *MHW peak intensity:* published DOISST has almost no trend (+0.006 C per decade, interval includes zero). All members give +0.046 to +0.054 C per decade. In the tropics (20S-20N) the published trend is negative (-0.044), and all members give a positive trend (+0.011 to +0.025).
   - *2023 peak intensity:* in published DOISST, 2023 ranks 7th for MHW peak intensity. In all 16 members 2023 is the record year.
   - *MCS duration:* published DOISST gives a rise (+0.75 days per decade). Fifteen of 16 members give a decrease (-0.24 to +0.03). The published sign fails in 10 of 22 regions.
   - *Weaker cold spells (Wang et al. 2022):* no member gives weaker cold-spell peaks in 2011-2020 than in 1982-1991. The ensemble gives peaks 3 to 6% stronger. Our run of published DOISST gives no change (ratio 1.01), so we also could not reproduce the published 15% decrease with our definitions.
   - *Regional heatwave trends in the equatorial Pacific (Nino 3.4) and Humboldt boxes:* the published MHW-day and duration increases become unresolved (members disagree in sign).
5. **The noise target, not the mean correction, sets most of the uncertainty of event statistics.** For the MHW-day trend, 72% of the ensemble variance comes from the noise target and 28% from the mean correction. For MHW duration, the share of the noise target is 96%; for MHW peak intensity 80%. The mean correction sets most of the spread only for MCS frequency (87%), MCS duration (76%), cumulative intensity (58%) and the mean warming (100%). A record with less fast variance gives a larger MHW-day trend for the same warming (smooth target: +18.8 to +22.2; noisy target: +13.5 to +16.1 days per decade), because the number of threshold exceedances per degree of warming increases as the anomaly variance decreases. Thus the MHW-day trend depends on the effective resolution of the product, even after homogenisation.
6. **The 2023-2024 daily SST record streak survives.** In published DOISST, the 60S-60N mean set a calendar-day record on every day from 13 March 2023 to 13 July 2024 (489 days). In the mean-corrected versions the streak is 479-483 days and starts 6-10 days later. The mean margin over the earlier record (June 2023 to May 2024) falls from 0.208 to 0.175-0.195 C.
7. **No production splice at the 2020 step.** The NCEI daily files around 7 July 2020 were each made 15 days after their data day in the same production line (`date_created` 2020-07-18 to 2020-07-24 for 3-9 July), with the same platform list. Thus the undocumented 2020 step is not a change from a retrospective run to near-real-time production. Its cause is still unknown.

## Context in the campaign

This work combines the noise-step studies (sci:sha256:f50dc28f, 87b87a67, 69a00227, cfeb640f, 819eea65, 0d84af9c, 5d9b238d, ef9c2a57) and the mean-step studies (sci:sha256:b93b5f64, 645d0681). Those studies used one correction each. Study 645d0681 also gave a combined mean-plus-noise version with one choice (MN in our tables; we reproduce its global values within 1%). Studies 825d6796, 77b0a90c, b4e19931 and 6b5e961c gave worst-case bounds for arbitrary SST changes. Our ensemble is between these two approaches: it uses physically fitted corrections, and it measures how much the results change between reasonable correction choices. The buoy test of the mean correction (result 1) is new.

## Data

- DOISST v2.1 AVHRR-only daily mean files 1982-2025 (NOAA PSL copies in the shared campaign store, `datasets/noaa-psl-oisst-v21-highres-sst-day-mean-YYYY-20261109`; all 44 SHA-256 values agree with the store records; list in `provenance/data_provenance.json`). We used the native 0.25-degree pixel at every fourth row and column (one point per one-degree cell; the sample of sci:sha256:87b87a67 and 819eea65): 29,129 cells that are ice-free on all 16,071 days.
- Mean-step fields (15 dates, fitted on HadSST4.2 and ERSSTv5, 1000 km and 2000 km smoothing) from sci:sha256:645d0681 and the implied ship-bias field (iQuam-based) from sci:sha256:b93b5f64.
- Daily moored-buoy SST (90 GTMBA and 52 NDBC buoys with enough data) and DOISST at the buoy cells from sci:sha256:87b87a67.
- Global attributes of nine NCEI DOISST v2.1 daily files (2020-06-20, 2020-07-03 to 2020-07-09, 2020-07-20).

## Methods

**Mean corrections.** corrected = raw - C(t, x), with C the sum of the fitted step sizes at the 15 step dates (zero after 2023-04-01) plus the ship term (`code/hom.py`, unchanged from sci:sha256:645d0681). Members: `had` (HadSST4.2 fields + ship term), `ers` (ERSSTv5 fields + ship term), `s0` (mean of both fields, no ship term), `h50` (0.5 times the mean of both fields with the ship term).

**Noise corrections.** For each cell we estimated the anomaly spectrum in six input segments (1982-84, 1985-2006, 2007-15, 2016-20 to 6 July, 7 July 2020-Sept 2021, Oct 2021-2025) and changed only periods shorter than about 32 days (taper to 64 days) (`code/degrade.py`, from sci:sha256:819eea65 and 645d0681). Targets: `d85` adds noise so that every segment has at least the 1985-2006 power; `m07`, `m16`, `m21` match every segment to the 2007-2015, 2016-2020 or 2021-2025 power (filter where the segment is noisier, added noise where it is smoother). sci:sha256:819eea65 found that the 2016-2020 segment is closest to the buoys, so we also report the four `m16` members as a "best" subset. A second noise seed for one member changed the global trends by at most 0.007 days per decade (MHW days).

**Statistics** (`code/20_ensemble.py`, `code/mhwlib.py`; Hobday et al. 2016 reference rules: 1983-2012 baseline, 11-day window, 31-day smoothing, events of at least 5 days, gaps of at most 2 days joined, events counted in their start year): MHW and MCS days, number of events, mean duration and mean peak intensity of events that start in the year, cumulative intensity; category II+ and III+ days (Hobday et al. 2018: (SST - climatology) / (threshold - climatology) at least 2 or 3 on MHW days); days above a day-of-year 99th percentile of 1982-2016 SST and days with anomaly above one all-season 99th percentile of 1982-2016 anomalies (two readings of the Frolicher et al. 2018 definition, no minimum duration); annual maximum, minimum and mean anomaly. Each version uses its own climatology and thresholds. We also kept the published (raw), mean-only (M = mean of the HadSST4.2 and ERSSTv5 fields), noise-only (N, `m16`) and combined (MN) versions of sci:sha256:645d0681.

**Aggregation** (`code/50_aggregate.py`). Area weights cos(latitude). Event means (duration, peak intensity) use only cell-years with events. OLS trends per decade; 95% moving-block bootstrap intervals (3-year blocks) for the reference versions. Two-factor variance split of the 16 member trends: variance of the four mean-correction means, variance of the four noise-target means, remainder.

**Claims** (`code/60_claims.py`). For each published result we computed the same statistic in published DOISST and in all members. Classes: *survives* (all members agree with the published statement and the published value is inside the member range), *sign only* (all members agree, the published value is outside the range), *unresolved* (members disagree), *fails* (no member agrees). For regional trends "agree" means "same sign as published DOISST". Published values in the literature used other DOISST versions, periods, baselines and sample grids; we compare our own run of published DOISST with the ensemble, so the test measures the effect of the artifacts, not the exact reproduction of each paper.

**Buoy test** (`code/40_buoy_mean.py`, `code/41_buoy_steps.py`). Matched days with |DOISST - buoy| < 5 C; monthly means with at least 10 days; per-buoy OLS trend (at least 120 months over at least 15 years); local steps at each correction date (up to two years each side, cut at the neighbouring dates). Medians over buoys with bootstrap intervals over buoys.

**Daily records** (`code/30_daily_global.py`, `code/31_records.py`). Area-weighted mean over all valid cells of the one-degree sample at 60S-60N (sea-ice cells, SST at or below -1.2 C, are not corrected). A calendar-day record is a value above the same day of year in all earlier years.

## Results tables

Global 1982-2025 trends per decade (1-degree sample, 29,129 cells; `results/ensemble_summary.csv`):

| Statistic | Published (95% CI) | M | N | MN | Ensemble min - median - max | m16 members | Variance share: mean / noise |
|---|---|---|---|---|---|---|---|
| MHW days | 21.17 (15.8 to 26.9) | 15.70 | 21.98 | 16.35 | 13.54 - 16.28 - 22.15 | 16.10 - 19.11 | 0.28 / 0.72 |
| MHW events | 0.656 (0.54 to 0.77) | 0.472 | 0.851 | 0.662 | 0.540 - 0.698 - 0.856 | 0.641 - 0.760 | 0.30 / 0.70 |
| MHW duration (days) | 4.45 (2.88 to 6.13) | 3.62 | 3.12 | 2.34 | 1.53 - 2.34 - 4.21 | 2.34 - 2.71 | 0.04 / 0.96 |
| MHW peak intensity (C) | 0.006 (-0.010 to 0.022) | 0.002 | 0.053 | 0.049 | 0.046 - 0.049 - 0.054 | 0.049 - 0.051 | 0.19 / 0.80 |
| MHW cumulative intensity (C day) | 30.3 | 22.7 | 31.4 | 23.6 | 21.5 - 23.9 - 29.7 | 23.2 - 27.4 | 0.58 / 0.41 |
| Category II+ days | 2.66 | 1.82 | 4.16 | 2.97 | 2.61 - 2.98 - 3.89 | 2.96 - 3.54 | 0.51 / 0.49 |
| Category III+ days | 0.108 | 0.062 | 0.250 | 0.163 | 0.133 - 0.165 - 0.232 | 0.161 - 0.204 | 0.44 / 0.55 |
| Days > 99th pct (day-of-year) | 4.00 | 2.76 | 5.86 | 4.36 | 3.73 - 4.36 - 5.64 | - | 0.37 / 0.63 |
| MCS days | -7.70 (-9.2 to -6.2) | -6.33 | -8.78 | -7.26 | -9.50 - -7.52 - -5.80 | - | 0.29 / 0.70 |
| MCS events | -0.725 | -0.633 | -0.640 | -0.540 | -0.624 - -0.568 - -0.509 | - | 0.87 / 0.13 |
| MCS duration (days) | 0.752 (0.24 to 1.24) | 0.935 | -0.277 | -0.095 | -0.240 - -0.130 - +0.027 | -0.191 - -0.022 | 0.76 / 0.17 |
| MCS peak intensity (C; negative = stronger) | +0.004 (-0.022 to 0.028) | +0.015 | -0.046 | -0.034 | -0.040 - -0.029 - -0.020 | - | 0.19 / 0.80 |
| Annual max anomaly (C) | 0.108 | 0.067 | 0.207 | 0.166 | 0.140 - 0.166 - 0.187 | - | 0.57 / 0.43 |
| Annual min anomaly (C) | 0.291 | 0.251 | 0.184 | 0.143 | 0.137 - 0.152 - 0.192 | - | 0.41 / 0.59 |
| Mean anomaly (C) | 0.190 | 0.150 | 0.190 | 0.150 | 0.143 - 0.153 - 0.170 | - | 1.00 / 0.00 |

Survival of published results (`results/claims.csv`; all 29 rows are in the file):

| Published result | Source | Published DOISST (our run) | Ensemble range | Class |
|---|---|---|---|---|
| MHW days increased (1982-2025) | Oliver et al. 2018; campaign | +21.2 d/decade | +13.5 to +22.2 | survives |
| MHW frequency increased | Oliver et al. 2018 | +0.66 /decade | +0.54 to +0.86 | survives |
| MHW duration increased | Oliver et al. 2018 | +4.45 d/decade | +1.53 to +4.21 | sign only (too large) |
| MHW peak intensity increased | Frolicher et al. 2018 | +0.006 C/decade (not significant) | +0.046 to +0.054 | sign only (8 times too small) |
| Category II+ MHW days increased | Hobday et al. 2018 categories | +2.66 d/decade | +2.61 to +3.89 | survives |
| Category III+ MHW days increased | Hobday et al. 2018 categories | +0.108 d/decade | +0.133 to +0.232 | sign only (too small) |
| 99th-percentile days doubled 1982-2016 | Frolicher et al. 2018 | x2.34 (day-of-year) / x2.45 (anomaly) | x2.37 to x4.27 / x2.34 to x4.25 | sign only / survives |
| MCS days decreased (1982-2020) | Wang et al. 2022; Schlegel et al. 2021 | -8.3 d/decade | -10.1 to -6.0 | survives |
| MCS days fell to about 25% of the 1980s | Wang et al. 2022 | 2011-2020 / 1982-1991 = 0.34 | 0.38 to 0.48 | sign only (fall too large) |
| MCS about 15% less intense | Wang et al. 2022 | ratio 1.01 | 1.03 to 1.06 (stronger) | fails |
| MCS duration increased | published DOISST trend | +0.75 d/decade | -0.24 to +0.03 (1 of 16 positive) | unresolved |
| 2023 record year: MHW days, category II+ days, cumulative intensity | Dong et al. 2025 | rank 1 | rank 1 in all members | survives |
| 2023 record year: MHW duration | Dong et al. 2025 | rank 1 | rank 1 in 9 members, rank 2 in 7 | unresolved |
| 2023 MHW days / 1982-2022 mean | Dong et al. 2025 | 3.51 | 2.83 to 3.10 | sign only |
| 2023 not a record for MHW peak intensity | published DOISST, sci:0d84af9c | rank 7 | rank 1 in all members | fails |
| 2024 more MHW days than 2023 | sci:645d0681 | +16.0 days | +11.1 to +17.0 | survives |
| Daily 60S-60N record streak 2023-2024 | Climate Reanalyzer (DOISST) | 489 days, margin 0.208 C | 479-483 days, margin 0.175-0.195 C | survives (smaller margin) |

Regional 1982-2025 trends (`results/regional_survival.csv`; 22 regions x 8 statistics = 176 tests): 84 survive, 69 keep their sign with a biased size, 9 are unresolved and 14 fail. By statistic: MHW frequency survives in 21 of 22 regions; MHW days in 12 (sign kept in 20); category II+ days in 18; MCS days in 18. MHW duration keeps its sign but is too large in 15 regions. MHW peak intensity is too small in 15 regions and has the wrong sign in 4 (tropics, Bay of Bengal, South China Sea, Gulf of Mexico/Caribbean). The MCS-duration sign fails in 10 regions. In the Nino 3.4 box the published MHW-day trend (+4.2 days per decade) becomes -1.4 to +1.6.

Moored buoys (`results/buoy_mean_offset.csv`, `results/buoy_steps_by_date.csv`): DOISST minus buoy trend (median, 95% CI, C per decade): published +0.034 (0.024 to 0.040), h50 +0.007 (0.002 to 0.013), HOM -0.020 (-0.026 to -0.013), HadSST fit -0.021, ERSSTv5 fit -0.018, no ship term -0.021, L = 2000 km -0.017. Local steps (published / HOM, C): 2007-01-01 +0.070 / +0.033; 2016-01-01 -0.008 / -0.046; 2020-07-07 +0.043 / -0.028; 2021-10-01 -0.050 / -0.002.

## Figures

- `figures/fig1_buoy_validation.png`: (a) DOISST minus buoy trend for published and mean-corrected versions, all buoys, GTMBA and NDBC; (b) local steps at each correction date, published and HOM, with the HOM correction step at the buoys.
- `figures/fig2_global_series.png`: global annual series of nine statistics; published DOISST (blue) and the 16-member range and median (orange).
- `figures/fig3_trend_survival.png`: (a) global 1982-2025 trends of 17 statistics, scaled by the absolute ensemble median: published value against the ensemble range; (b) share of the ensemble variance from the mean-correction choice, the noise-target choice and their interaction.
- `figures/fig4_regional_survival.png`: 22 regions x 8 trends: log2 of published / ensemble median and the survival class.
- `figures/fig5_daily_records.png`: daily 60S-60N mean SST in 2023-2024 and its margin over the 1982-2022 record for each day (the corrections are zero after April 2023, so the 2023-2024 curves agree and the margins change through the earlier records).

## Limitations

- **The ensemble is not a probability distribution.** The members are four plausible mean corrections times four plausible noise targets, with equal weight. The true record can lie outside the range, for example if all step fields share an error. The range shows how much the correction choice matters, not a confidence interval.
- **The mean correction is uncertain by about a factor of two.** In situ fits (HadSST4.2, ERSSTv5) and CCI agree on a DOISST excess of about 0.04 C per decade, but moored buoys (and Argo in sci:sha256:b93b5f64) give 0.02-0.03. Buoys are DOISST inputs, so DOISST is tied to them at buoy cells; this can make buoy steps smaller than open-ocean steps. Buoys sample mainly the tropical Pacific and US coasts.
- **The noise target is a choice.** No target is true everywhere: the 2016-2020 segment is closest to buoys, but buoys are point values and a gridded field should have less fast variance. The MHW-day, duration and intensity trends depend on this choice (result 5).
- **Published values in papers used other inputs.** Oliver et al. (2018) and Frolicher et al. (2018) used DOISST v2.0 for 1982-2016; Wang et al. (2022) used DOISST to 2020 with their own definitions. We test the effect of the artifacts on our run of the same statistic, not each paper's exact numbers. We could not reproduce the published 15% weaker cold spells with our definitions.
- **Sample and region.** One 0.25-degree pixel per one-degree cell, 60S-60N, cells ice-free on all days (polar splices are in sci:sha256:7102a214). A 2-degree subsample (7,288 cells; `results_2deg_check/`) gives the same global values within about 1%. Small regions (about 120-200 cells) are less certain.
- **Daily record series.** Our 60S-60N mean uses the one-degree point sample, not the full grid, so absolute values can differ slightly from Climate Reanalyzer.
- **The 2020 step cause is still unknown.** We only excluded a production splice.

## Reproduction

`files/code/run_all.sh` lists all steps. Python 3.12 with numpy, scipy, pandas, netCDF4 and matplotlib (`provenance/environment.json`). Put the scripts in `WORK/code/`; the shared DOISST files are read from `WORK/../datasets/<name>/` (or set `OISST_DIR`; names, URLs and SHA-256 in `provenance/data_provenance.json`); set `CAMPAIGN` to a folder with the ZIPs of sci:sha256:645d0681..., b93b5f64... and 87b87a67.... All intermediates go to `WORK/derived`, `WORK/scratch` and `WORK/results`. On the campaign host (2-CPU slice, shared load) extraction took 25 min, the one-degree ensemble 4 h with 2 processes (about 3 min per 400 cells for 21 versions), the daily series 45 min.

To inspect the results without downloads: `results/annual_regional.csv.gz` (annual means of 17 statistics for 21 versions and 22 regions), `results/trends.csv`, `results/ensemble_summary.csv`, `results/claims.csv`, `results/regional_survival.csv`, the buoy tables, `results/daily_records.csv`, `data/daily_global_60S60N.csv.gz` (daily 60S-60N mean SST, published and five mean-corrected versions) and `data/ncei_2020_file_attributes.json`. Region boxes are in `code/regions.py`.

## Provenance

- `provenance/data_provenance.json`: shared-store paths, source URLs, byte counts and SHA-256 of the 44 DOISST files; SHA-256 of the files reused from prior bundles.
- `provenance/environment.json`: software versions.
- `NOTICE_external_data.md`: licences and attribution of the external data. No raw external data are in this bundle.

## Job information

Campaign 11_07_2026, job sci-1107-hp-earth-and-ocean-sciences-318613a1eff5, topic earth-and-ocean-sciences, machine hp, model Claude Opus 5.5 (claude-opus-5-5). Data read 2026-11-10 and 2026-11-11. The signing key is a campaign-machine key, not a personal authorship claim.

## References

- Hobday, A. J., et al., 2016: A hierarchical approach to defining marine heatwaves. Prog. Oceanogr., 141, 227-238, doi:10.1016/j.pocean.2015.12.014.
- Hobday, A. J., et al., 2018: Categorizing and naming marine heatwaves. Oceanography, 31(2), 162-173, doi:10.5670/oceanog.2018.205.
- Oliver, E. C. J., et al., 2018: Longer and more frequent marine heatwaves over the past century. Nat. Commun., 9, 1324, doi:10.1038/s41467-018-03732-9.
- Frolicher, T. L., E. M. Fischer and N. Gruber, 2018: Marine heatwaves under global warming. Nature, 560, 360-364, doi:10.1038/s41586-018-0383-9.
- Wang, Y., J. B. Kajtar, L. V. Alexander, G. S. Pilo and N. J. Holbrook, 2022: Understanding the changing nature of marine cold-spells. Geophys. Res. Lett., 49 (author copy: https://figshare.utas.edu.au/articles/journal_contribution/Understanding_the_changing_nature_of_marine_cold-spells/23005310).
- Dong, T., et al., 2025: Record-breaking 2023 marine heatwaves. Science, doi:10.1126/science.adr0910.
- Huang, B., et al., 2021: Improvements of the Daily Optimum Interpolation Sea Surface Temperature (DOISST) version 2.1. J. Climate, 34, 2923-2939, doi:10.1175/JCLI-D-20-0166.1.
