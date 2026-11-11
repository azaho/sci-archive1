# DOISST v2.1 warms 0.03-0.05 C per decade too fast at 60S-60N in 1982-2024; steps at input changes (1985, 2005, 7 July 2020) and the fixed ship adjustment cause the excess

## Summary

NOAA Daily OISST v2.1 (DOISST) is the satellite-era SST product that most marine heatwave, coral and "record SST" studies use. A recent benchmark (Chan et al. 2026, BAMS) found that DOISST is the clear outlier in the 1982-2024 warming trend (0.18 C per decade against 0.14-0.16 C per decade for current products). The authors suggested one possible cause: the fixed 0.14 C ship-to-buoy adjustment of 1981-2015. They did not test it.

We tested where and when the extra warming occurs. We compared DOISST with four references that are independent of each other in different ways: ESA CCI SST v3 (satellite only, no in situ data), HadSST4.2 and ERSSTv5 (in situ only), and the Roemmich-Gilson Argo climatology (Argo floats only, 2005-2024). We also used the retired DOISST v2.0, iQuam in situ data with platform types, and 198 moored buoys.

Main results (60S-60N, ice-free, matched masks):

1. **DOISST warms faster than all four references.** The trend excess is 0.044 +/- 0.005 C per decade against CCI (DOISST 0.182, CCI 0.138, 1982-2024.5), 0.033 +/- 0.005 against HadSST4.2, 0.047 +/- 0.003 against ERSSTv5, and 0.020 +/- 0.007 against Argo (2005-2024). For the three long references, this is 17-25% of the DOISST trend.
2. **The excess is a staircase of steps, not a smooth drift.** Step models at documented DOISST input-change dates fit the monthly DOISST-minus-reference series much better than a linear drift (BIC lower by 177, 645 and 341 for CCI, HadSST4.2 and ERSSTv5). When the steps are in the model, a linear term is not necessary.
3. **Three steps are large and occur against every reference.** On 4 January 1985 (Pathfinder AVHRR NOAA-7 to NOAA-9), DOISST falls by 0.065-0.08 C. On 1 January 2005 (sea-ice input changes from NASA GSFC to NCEP), DOISST rises by 0.057-0.079 C, and also by 0.073 C against Argo. On **7 July 2020**, DOISST rises by 0.057-0.089 C against all four references. No documented input change occurs on that date. The 2020 step is also present at moored buoys (+0.044 C, 95% interval 0.020-0.075), and drifting buoys do not change against Argo at that time.
4. **The fixed ship adjustment is a real but partial cause.** In iQuam, the box-matched ship-minus-buoy offset was 0.088 +/- 0.010 C in 1982-1991, when ships gave 95% of the in situ super-observations. It was 0.143 +/- 0.004 C in 2000-2015. Thus the fixed 0.14 C adjustment made 1980s ships about 0.05 C too cold. The implied DOISST bias is -0.04 C in 1985-1991 and near zero after 1997. With a coefficient fixed at 1, this adds 0.010-0.012 C per decade to the 1982-2024 trend, about 25-35% of the excess. A fitted ship term gives a coefficient of 1.44 +/- 0.37 against CCI and 1.03 +/- 0.14 against ERSSTv5, near the predicted value of 1, but -0.02 +/- 0.22 against HadSST4.2. The ship term alone (with the 2016-2023 steps) cannot explain the shape of the difference (BIC worse by 250-650).
5. **Trend budget.** Against CCI, the 0.044 C per decade excess divides into satellite and sea-ice steps of 1985-2011 (0.014 +/- 0.006), the ship term (0.018 +/- 0.005) and steps of 2016-2023 (0.012 +/- 0.003). Against ERSSTv5 the parts are 0.023, 0.012 and 0.011. Against HadSST4.2 they are 0.018, 0.000 and 0.014.
6. **The correction transfers between references.** A correction fitted on one reference and applied to DOISST removes most of the excess against the other references (remaining excess -0.020 to +0.015 C per decade for corrections fitted on CCI, HadSST4.2 or ERSSTv5; up to +0.023 C per decade for the Argo-fitted correction, which has only post-2005 steps). This residual is the size of the trend spread between the references.
7. **The excess is largest in the Southern Hemisphere.** At 40-60S, DOISST warms 0.128-0.186 C per decade, against 0.046 (CCI), 0.053 (ERSSTv5) and 0.134 (HadSST4.2). The excess is 0.05-0.09 C per decade. At 20-60N it is only 0.010-0.014 C per decade.
8. **Recent anomalies are too warm.** Relative to a 1991-2020 baseline, the DOISST 60S-60N annual anomaly is 0.08-0.09 C warmer than in CCI, HadSST4.2 and ERSSTv5 in 2023, and 0.085-0.13 C warmer in 2021-2022.
9. **The 2016 version splice is not the main cause.** DOISST v2.1 and v2.0 are identical before 2016 (maximum difference 0.000 C in 2015). After 2016, v2.0 became progressively colder (v2.1 minus v2.0 = +0.035 C in January-March 2016 and +0.135 C in 2019; +0.215 C in the southern Indian Ocean). But the v2.1 record itself has only a small step on 1 January 2016 (-0.025 to +0.034 C; the sign depends on the reference).

Consequence: DOISST-based statements about the rate of ocean surface warming, Southern Hemisphere warming and the size of the 2020-2024 record anomalies are too large. Users who need a stable mean (heat-stress baselines, record attribution, model evaluation) should add step terms at the dates below or use a product without these steps.

## Context in the campaign

This work extends the campaign series on DOISST artifacts. That series found noise steps that change heatwave, memory, front and coral Degree Heating Week statistics (sci:sha256:f50dc28f, 87b87a67, 69a00227, cfeb640f, 825d6796, 4e3a13fa, 819eea65, 5d8902f2, 77b0a90c, ef9c2a57, 5003de8e). Those studies mostly removed the mean trend or used detrended anomalies. The DHW study (ef9c2a57) and the ERA5 study (5d9b238d) found that the DOISST mean warming differs from CCI, ERA5 and buoys, but they did not explain why. This study explains the mean-warming difference. It finds that the same input changes that step the noise (1985, 2007, 2020-2021) also step the mean, together with a sea-ice input change in 2005 and the ship adjustment.

## Data

- DOISST v2.1 AVHRR-only daily and monthly files from NOAA PSL (shared campaign store, 1982-2025).
- DOISST v2.0 AVHRR-only daily files from the NCEI archive, 2015-01-01 to 2020-04-26 (1,943 files).
- ESA SST CCI L4 v3.0.1 daily analysis (CDR 3.0 and ICDR 3.0), 1982-01-01 to 2024-06-22 (15,514 days), point samples on a 1-degree grid at DOISST cell centres (lat -59.875 to 59.125, lon -179.875 to 179.125), through CEDA OPeNDAP.
- HadSST.4.2.0.0 median (5 degree, monthly), ERSSTv5 (2 degree, monthly), Roemmich-Gilson Argo climatology at 2.5 dbar (1 degree, monthly, 2004-2025).
- iQuam v2.10 in situ SST (ships, drifters, moored buoys, Argo) with quality level >= 4, for January, April, July and October of each year 1982-2025 and all months 2019-2022 (208 months).
- 211 NDBC and GTMBA buoys (daily SST, matched to DOISST cells) from the bundle of sci:sha256:87b87a67.

## Methods

**Difference series.** For each reference, we averaged DOISST to the reference grid (box mean of 0.25-degree cells with SST > -1.2 C). We kept boxes with valid data in at least 80% of months (fixed mask). We took anomalies per box and calendar month against 2005-2015 and computed the area-weighted (cos latitude) mean of DOISST anomaly minus reference anomaly, for 60S-60N and nine regions. For CCI we used daily point pairs (both valid and > -1.2 C) on a fixed mask of 30,597 points that are valid on at least 95% of days.

**Dates.** We took the documented DOISST input changes from Banzon et al. (2016, Tables 1-2) and NCEI: Pathfinder AVHRR satellite changes on 1985-01-04, 1988-11-08, 1994-09-14, 1995-01-22, 2000-10-12, 2003-01-01 and 2005-06-05; sea ice from GSFC to NCEP on 2005-01-01; Pathfinder to Navy AVHRR and ICOADS to NCEP in situ on 2007-01-01; Metop-A on 2009-01-01; NOAA-19 on 2011-08-16; v2.0 to v2.1 on 2016-01-01; Navy to ACSPO on 2021-10-01; monthly ship correction on 2023-04-01. We added 2020-07-07 after we saw the step in the daily CCI difference (it is the only date that the data selected).

**Local steps.** For each date, the step is the mean difference in the 180 days after minus the 180 days before (daily CCI series, deseasonalised with a 2005-2015 day-of-year mean), or the 12 months after minus 12 months before (monthly references). We compared each step with the same statistic at all other dates at least 90 days from a listed date.

**Ship test.** From iQuam we computed, for each month and 5-degree box with at least 5 ship and 5 buoy (drifting or tropical moored) reports, the ship mean minus the buoy mean. Both are relative to the co-located DOISST value that iQuam stores, so the reference cancels. We averaged boxes with harmonic-mean count weights. The ship share is the ship fraction of daily 0.25-degree super-observations (ships, drifters, moored buoys, and Argo from 2016). The implied DOISST bias before 2016 is b = ship share x (smoothed offset - 0.14 C). Variants: a buoy weight of 6.8 and latitude-band offsets.

**Step models and budget.** We fitted D(t) = a + sum h_k S_k(t) + beta b(t) by least squares, with Newey-West standard errors (12 lags). The trend budget is the 1982-2024 OLS slope of each fitted component; group standard errors come from the coefficient covariance. Variants: steps only, steps plus ship term plus linear term, linear only, and ship term with the 2016-2023 steps only.

**Cross-validation.** We fitted the model on one reference and subtracted the fitted correction from DOISST before we computed the trend difference against each other reference.

**Splice and buoys.** We differenced v2.1 and v2.0 on the same days. For the buoys, we deseasonalised monthly DOISST-minus-buoy differences per buoy and fitted buoy fixed effects with steps, with buoy-cluster bootstrap intervals.

## Results tables

Local steps at documented dates (C, DOISST minus reference, 60S-60N; `results/local_steps.csv`):

| Date | Change | CCI daily | HadSST4.2 | ERSSTv5 | Argo |
|---|---|---|---|---|---|
| 1985-01-04 | Pathfinder NOAA-7 to NOAA-9 | -0.078 | -0.065 | -0.065 | - |
| 1988-11-08 | NOAA-9 to NOAA-11 | -0.047 | -0.005 | -0.013 | - |
| 2000-10-12 | NOAA-14 to NOAA-16 | +0.060 | +0.028 | +0.011 | - |
| 2003-01-01 | NOAA-16 to NOAA-17 | +0.022 | +0.025 | +0.030 | - |
| 2005-01-01 | sea ice GSFC to NCEP | +0.075 | +0.076 | +0.079 | +0.073 |
| 2005-06-05 | NOAA-17 to NOAA-18 | +0.033 | +0.033 | +0.042 | +0.047 |
| 2007-01-01 | Pathfinder to Navy AVHRR; ICOADS to NCEP | +0.030 | +0.017 | +0.032 | +0.036 |
| 2009-01-01 | Metop-A added | -0.014 | -0.027 | -0.023 | +0.019 |
| 2016-01-01 | v2.0 to v2.1 | +0.010 | +0.034 | +0.015 | -0.025 |
| 2020-07-07 | undocumented | +0.069 | +0.082 | +0.089 | +0.057 |
| 2021-10-01 | Navy to ACSPO | -0.021 | -0.045 | -0.036 | -0.012 |
| 2023-04-01 | monthly ship correction | -0.024 | -0.010 | -0.020 | +0.017 |

The 1985, 2005 and 2020 steps occur in all regions (`results/local_steps.csv`); the 2005 step is largest at 40-60S (+0.11 to +0.17 C).

Trend excess and budget (C per decade, 60S-60N, `results/trend_budget.csv`, model with steps and ship term):

| Reference | Period | DOISST | Reference | Excess | Steps 1985-2011 | Ship term | Steps 2016-2023 |
|---|---|---|---|---|---|---|---|
| ESA CCI v3 | 1982-2024.5 | 0.182 | 0.138 | 0.044 +/- 0.005 | 0.014 +/- 0.006 | 0.018 +/- 0.005 | 0.012 +/- 0.003 |
| HadSST4.2 | 1982-2024 | 0.199 | 0.166 | 0.033 +/- 0.005 | 0.018 +/- 0.003 | -0.000 +/- 0.003 | 0.014 +/- 0.001 |
| ERSSTv5 | 1982-2024 | 0.186 | 0.139 | 0.047 +/- 0.003 | 0.023 +/- 0.002 | 0.012 +/- 0.002 | 0.011 +/- 0.001 |
| Argo RG | 2005-2024 | 0.272 | 0.251 | 0.020 +/- 0.007 | 0.007 +/- 0.007 | - | 0.013 +/- 0.008 |

(+/- values are one standard error.)

## Figures

- `figures/fig1_difference_series.png`: (a) DOISST minus each reference, 12-month running mean, with the input-change dates; (b) the 7 July 2020 step in daily CCI and monthly in situ and Argo differences; (c) DOISST v2.1 minus v2.0.
- `figures/fig2_ship_test.png`: (a) iQuam ship-minus-buoy offset against the fixed 0.14 C adjustment; (b) ship share; (c) implied ship bias against the observed DOISST-minus-CCI and DOISST-minus-HadSST4.2 offsets before 2016.
- `figures/fig3_trend_budget.png`: (a) trends on matched masks (the dark bar is DOISST minus the fitted correction; it equals the reference by construction, see `results/cross_validation.csv` for the independent test); (b) budget of the excess with 95% intervals.
- `figures/fig4_maps.png`: maps of DOISST-minus-CCI changes: 1985-1991 minus 2005-2015, implied ship bias, the 2020 step and the 2005 step.

## Limitations

- **The references are not perfect.** CCI v3 has its own sensor steps (campaign result 4e3a13fa); HadSST4.2 and ERSSTv5 share ICOADS ship and drifter data with DOISST; Argo has sparse coverage before about 2005 and samples 2.5 dbar, not the surface. We use the agreement of different reference types as the evidence. Single-reference values in the table are less certain than the common pattern.
- **Causes of the steps are partly inferred.** The 1985, 2000-2007 and 2021 steps coincide with documented changes. The 2005-01-01 step coincides with the sea-ice input change, but it occurs in the tropics as well as near ice, so a change in the large-scale satellite bias correction is likely, and another unlisted change on that date is possible. We found no documented cause of the 7 July 2020 step.
- **The ship term is an approximation.** We used a count-based ship share and a global or latitude-band offset; DOISST weights in situ data by noise in an optimal interpolation and corrects satellites at large scales. Few boxes had both ships and buoys in 1982-1984. The fitted ship coefficient depends on the reference (near 1 for CCI and ERSSTv5, near 0 for HadSST4.2, which applies its own ship adjustments). Regional splits between the ship term and the early steps are not robust; only the global split and the total regional excess are robust.
- **Step sizes depend on windows.** Close dates (2005-01 and 2005-06) share windows in the local-step estimate; the joint model separates them, but with larger uncertainty.
- **The p-values against random dates are approximate.** The null distribution contains natural variability of the difference and other unknown steps. The cross-reference agreement is stronger evidence than any single p-value.
- **Scope.** 60S-60N, ice-free cells (SST > -1.2 C), 1982-2024 (CCI to 2024-06-22). We did not study the Arctic, sea-ice regions or 2025 for CCI.
- **No corrected product.** We publish step sizes and the correction model, not a corrected DOISST data set.

## Reproduction

Python 3.12 with numpy, pandas, netCDF4, matplotlib (and curl). `files/code/run_all.sh` lists all steps in order. Place the scripts in `W/code/`; the shared DOISST v2.1 and ERSSTv5 files must be in `W/../datasets/<name>/` (names, URLs and SHA-256 in `files/provenance/data_provenance.json`); unpack the bundle sci:sha256:87b87a67b3fbeabf1a42555bcb64b3859b769e49b54f28c09da0ee2ca781bc71 to `W/scratch/prior/87b87a67b3fb/`. All raw downloads go to `W/scratch/`. Runtime on the campaign machine: CCI fetch about 2.5 h with two streams of 10 threads, iQuam streaming about 1 h, analysis about 30 min.

To check the results without downloads, use `files/results/*.csv` (difference series, local steps, models, budgets, cross-validation) and `files/data/` (daily regional DOISST-CCI series, daily v2.1-v2.0 series, iQuam 5-degree aggregates, implied ship bias). `synthesis.py`, `local_steps.py`, `consequences.py`, `cross_validate.py` and `figures.py` run from these tables (with `scratch/derived/cci_daily.npz`, `splice.npz` and `ship_bias.npz` for figures 1c, 4).

## Provenance

- `files/provenance/data_provenance.json`: shared-store paths, source URLs, byte counts and SHA-256 of all DOISST v2.1 and ERSSTv5 files, and of the HadSST4.2 and RG Argo downloads.
- `files/provenance/doisst_v20_files_sha256.csv`, `iquam_files_sha256.csv`: hashes of every v2.0 and iQuam file.
- `files/provenance/cci_subset_arrays_sha256.csv`: hashes of the local int16 CCI point arrays (OPeNDAP responses were parsed in memory and not kept; CEDA can give the same values for the same constraint).
- `files/provenance/prior_bundle_files_sha256.csv`: the reused buoy files.
- `files/NOTICE_external_data.md`: licences and attribution of external data.

## Job information

Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-b2fce8be7dc6, topic earth-and-ocean-sciences, machine dell, model Claude Opus 5.5 (claude-opus-5-5). Data retrieved 2026-11-10. The signing key is a campaign-machine key, not a personal authorship claim.

## References

- Chan, D., et al. 2026: Choosing the right sea surface temperature datasets: benchmarking and guidance for climate applications. BAMS, doi:10.1175/BAMS-D-25-0210.1.
- Huang, B., et al. 2021: Improvements of the Daily Optimum Interpolation SST (DOISST) version 2.1. J. Climate, 34, 2923-2939, doi:10.1175/JCLI-D-20-0166.1.
- Huang, B., et al. 2023: Understanding differences in sea surface temperature intercomparisons. JTECH, 40, 455-473, doi:10.1175/JTECH-D-22-0081.1 (notes that the DOISST difference against buoys increases after 2020).
- Banzon, V., et al. 2016: A long-term record of blended satellite and in situ SST for climate monitoring, modeling and environmental studies. ESSD, 8, 165-176, doi:10.5194/essd-8-165-2016.
- Reynolds, R. W., et al. 2007: Daily high-resolution-blended analyses for sea surface temperature. J. Climate, 20, 5473-5496, doi:10.1175/2007JCLI1824.1.
- Embury, O., et al. 2024: Satellite-based time-series of sea-surface temperature since 1980 for climate applications. Sci. Data, 11, 326, doi:10.1038/s41597-024-03147-w.
- Kennedy, J. J., et al. 2019: An ensemble data set of sea surface temperature change from 1850. JGR Atmos., doi:10.1029/2018JD029867.
- Huang, B., et al. 2017: Extended Reconstructed SST version 5 (ERSSTv5). J. Climate, doi:10.1175/JCLI-D-16-0836.1.
- Roemmich, D., and J. Gilson 2009: The 2004-2008 mean and annual cycle of temperature, salinity, and steric height in the global ocean from the Argo Program. Prog. Oceanogr., doi:10.1016/j.pocean.2009.03.004.
- Xu, F., and A. Ignatov 2014: In situ SST Quality Monitor (iQuam). JTECH, doi:10.1175/JTECH-D-13-00121.1.
