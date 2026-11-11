# CoralTemp v3.1 has mean steps at the 1995 ATSR-2 and 2002 AATSR starts, in 2008 and in 2020; removing them cuts 2024 reef pixels at DHW 4 or more from 83% to 63% (35S-35N, six references)

## Summary

NOAA Coral Reef Watch (CRW) calculates coral bleaching heat stress (HotSpots, Degree Heating Weeks, Bleaching Alert Areas) from CoralTemp v3.1, a daily 5-km SST record from 1985. CoralTemp joins three analyses: the Met Office OSTIA reanalysis (1985 to November 2002), the NOAA Geo-Polar Blended (GPB) reanalysis (November 2002 to October 2016) and the GPB near-real-time analysis (from October 2016). CRW calculates the bleaching threshold (the maximum monthly mean, MMM) from 1985-2012 CoralTemp and compares every new day with it. Thus, a change in the mean of CoralTemp between the climatology years and today changes all heat-stress values. Earlier campaign work found steps in NOAA DOISST (sci:sha256:b93b5f64, 645d0681) and examined DHW from DOISST (sci:sha256:ef9c2a57), but did not test CoralTemp itself.

We compared CoralTemp with six references of different types at 35S-35N for 1985-2025: ERSSTv5 and HadSST4.2 (in situ), mean-homogenised DOISST (sci:sha256:645d0681), ESA SST CCI v3 (satellite only, no in situ data), 72 GTMBA and 25 NDBC moored buoys (in situ points), and 1,662 reef pixels.

Main results:

1. **CoralTemp is not homogeneous. Its difference from every reference is a staircase with four large steps.** A break search with ENSO terms finds the same months in all independent references: June 1995 (CoralTemp becomes colder by 0.04-0.16 C), August 2002 (warmer by 0.06-0.12 C), January 2008 (warmer by 0.04-0.07 C) and about October 2020 (warmer by 0.04-0.06 C). The documented reanalysis-to-near-real-time splice of October 2016 gives only a small step (-0.05 to +0.03 C). Against random dates, the four steps are significant for all in situ fields (p <= 0.009) and for the buoys (p = 0.009-0.09).
2. **The two early steps are not at the documented splice.** With daily data (every eighth day), the 1995 step occurs between 21 May and 30 June 1995 and the 2002 step between 19 July and 4 August 2002, three to four months before the November 2002 OSTIA-to-GPB merge. A separate term for the merge is small (-0.021 to +0.031 C, sign changes between references). Both dates agree with the first ATSR-2 data of the ARC record (31 May 1995, CEDA catalogue) and the start of AATSR operations (23 July 2002, ESA). OSTIA uses (A)ATSR data with drifting buoys as its bias-correction reference (Donlon et al. 2012). We did not confirm the cause in the OSTIA reanalysis input logs. We found no documented cause for the 2008 and 2020 steps.
3. **The steps make CoralTemp warm too fast.** The 1985-2025 trend of CoralTemp minus reference is +0.034 (ERSSTv5), +0.031 (HadSST4.2) and +0.033 C per decade (homogenised DOISST) at 35S-35N, +0.036-0.039 at 20S-20N (including ESA CCI), and +0.049 at the reef pixels. In every series the step terms explain all of this excess (residual trend -0.001 to 0.000 C per decade). The GTMBA buoys give a smaller excess (+0.012) because their 1995 step is larger. The CoralTemp trend falls from 0.179 to 0.147 C per decade at 35S-35N and from 0.216 to 0.181 C per decade at the reef pixels after homogenisation.
4. **The bleaching threshold is too low for today's CoralTemp.** We fitted spatial step fields (in situ references, 1000 km smoothing), removed them (present level kept, past adjusted) and recalculated the MMM with the CRW method. Our recalculation of the official MMM agrees within +-0.004 C. The homogenised MMM is higher by 0.14 C on average (10-90%: +0.05 to +0.21 C; 0.135-0.141 C for the four reference fields; 0.128 C for the satellite-only CCI variant). Thus, relative to its own climatology, published CoralTemp shows today's reefs about 0.14 C warmer than a homogeneous record would.
5. **Heat-stress trends are about 20-30% too large.** For the monthly heat-stress index (annual maximum Degree Heating Months, 3-month window), the 1985-2025 reef-mean trend falls from 0.45 to 0.36 C-months per decade (ratio 0.78-0.82 for all reference fields). The trend of months with a HotSpot of 1 C or more falls by 28-34%.
6. **The 2023-2025 bleaching-event footprint is about one fifth smaller.** Because DHW depends only on SST minus MMM, the higher homogenised MMM lowers every HotSpot after October 2020 by about 0.14 C. With complete daily CoralTemp for October 2022 to December 2025, our recalculation of the official composites agrees (2024: 82.8% against 83.1% of reef pixels at DHW >= 4; per-pixel mean difference -0.04 C-weeks). After homogenisation, the reef pixels with an annual maximum DHW of 4 C-weeks or more fall from 83.1% to 62.9% in 2024 (61-67% for six correction variants), from 43.9% to 37.1% in 2023 and from 54.9% to 40.8% in 2025. At 8 C-weeks or more, 2024 falls from 51.2% to 36.9% (36-39%). Over 2023-2025, the pixels that reached DHW >= 4 in at least one year fall from 90.6% to 73.4% (71-78%), and those at DHW >= 8 from 63.2% to 48.9% (47-50%). The mean annual maximum DHW falls by 20-26% (2024: 9.7 to 7.6 C-weeks). The event is still the largest in the record, but its reported extent depends on the steps.

Consequence: CoralTemp-based statements about how fast reef heat stress increases, and how much of the reef area reached bleaching-level stress in recent years, include an artifact of the record. The direction is the same in all six references. The size depends on the reference by a factor of about two for single steps, but the trend excess (0.031-0.039 C per decade) and the MMM change (+0.128 to +0.141 C) agree closely, including a satellite-only variant.

## Context in the campaign

This work extends the campaign series on daily SST records. Studies sci:sha256:f50dc28f, 87b87a67, 69a00227, cfeb640f, 819eea65, 0d84af9c, 5d9b238d, 4e3a13fa, 5003de8e and 5d8902f2 found noise and spatial-detail steps in DOISST, CCI and ERA5. Study b93b5f64 found mean steps in DOISST and 645d0681 made a mean-homogenised DOISST, which is one of our references here. Study ef9c2a57 found that DOISST noise steps make reef DHW trends too low and that mean-warming differences between products are a larger uncertainty; its limitation was that it did not test the operational CRW product. This study tests that product. Study d9bdf1f8 homogenised seven monthly and daily SST products jointly but did not include CoralTemp. A related published study (Margaritis, Kent and Foster 2025, PLOS Climate, doi:10.1371/journal.pclm.0000480) found that CoralTemp warms faster than CCI and reef loggers at Caribbean sites by up to 0.20 C per decade; it did not identify the dates or the effect on the CRW threshold.

## Data

- CoralTemp v3.1 daily SST, NOAA CRW (STAR file server, MD5 checked; some days through the CoastWatch ERDDAP `noaacrwsstDaily`, identical values checked to 4e-15 C). We kept a 0.25-degree sample (every fifth 5-km pixel, at DOISST cell centres) at 34.875S-34.875N. Days used: every eighth day of 1985-01-01 to February 2008 (1054 days, for break dating; the rest of the every-eighth-day sample could not be downloaded in time) and all days from 9 October 2022 to 31 December 2025 (1,180 days, for the 2023-2025 DHW); 2,314 days in total (1,122 from STAR files, 1,192 through ERDDAP).
- CRW official monthly mean SST (all 492 months 1985-2025, MD5 checked), annual maximum DHW composites (1986-2025), annual mean SST, and the MMM climatology `ct5km_climatology_v3.1.nc`.
- DOISST v2.1 daily (shared campaign copies 1982-2025), ERSSTv5, HadSST4.2, CPC Nino 3.4 (shared copies).
- From earlier campaign bundles: the 1,763 reef pixels (ef9c2a57; 1,662 inside 35S-35N with complete data), DOISST mean-step fields and correction code (645d0681), moored-buoy daily SST (87b87a67), the daily DOISST-minus-CCI regional series and CCI point mask (b93b5f64).

URLs, byte counts and hashes of all files are in `files/provenance/`. Licences and attribution are in `files/NOTICE_external_data.md`.

## Methods

**Difference series.** We averaged CoralTemp and DOISST over the same valid 0.25-degree cells in 1-degree boxes (monthly), and to 2-degree (ERSSTv5) and 5-degree (HadSST4.2) boxes. We removed the calendar-month mean of each box difference and took cos-latitude weighted means on fixed masks (boxes valid in at least 95% of months; 80% for HadSST4.2). For homogenised DOISST we subtracted the monthly mean of the 645d0681 correction (HOM; variants fitted on one reference). For buoys we used per-buoy monthly means (at least 15 days) minus CoralTemp at the buoy cell. For ESA CCI (20S-20N) we chained CoralTemp minus DOISST on the CCI point mask of b93b5f64 with the monthly mean of its daily DOISST-minus-CCI series.

**Breaks.** Binary segmentation of each monthly series with Nino 3.4 (lags 0-3 months) as regressors (`breakpoints.py`). We kept break months that occur within three months in at least three of the four independent reference types (ERSSTv5, HadSST4.2, homogenised DOISST, GTMBA buoys). The joint model is D(t) = a + sum h_k S_k(t) + sum g_l N34(t-l) with Newey-West (12-lag) errors; the merge months (2002-11, 2016-10) are left out. The p-value against random dates ranks the 12-month-after minus 12-month-before difference at the break among the same statistic at all months at least 13 months from a break. Because the dates were selected from the same data, these p-values are optimistic; the agreement of independent reference types is the main evidence. Daily dating uses every eighth day and the largest 300-day before/after jump within +-14 months.

**Correction.** In each reference box we fitted the joint model and smoothed the box step sizes on the sphere (Gaussian, L = 1000 km; 2000 km variant) with inverse-variance weights (AR(1)-inflated). The main field (INSITU) is the mean of the ERSSTv5 and HadSST4.2 fields; ERSSTv5-only, HadSST4.2-only and DOISST-HOM fields are variants. The homogenised SST is CoralTemp - C(t,x), C = sum_k h_k(x)(S_k(t) - 1), so values after October 2020 do not change.

**Heat stress.** MMM by the CRW v3.1 method (monthly means of 1985-2012 regressed on year, evaluated at 1988.2857, maximum of the 12 months), from the official monthly means. Degree Heating Months: sum over three months of the positive monthly HotSpot. DHW: CRW v3.1 (84-day sum of daily HotSpots of 1 C or more, divided by 7), from daily CoralTemp with the official MMM (check against the official annual composites) and from homogenised CoralTemp with the homogenised MMM. Trend intervals: moving-block bootstrap over years (blocks of 3).

**Satellite-only variant.** The same step sizes at all reef pixels, taken from the CoralTemp-minus-ESA-CCI model (20S-20N). This variant uses no in situ data.

**Test of the correction.** We applied the INSITU correction at the buoy cells (buoys not used in the fit) and at the reef pixels against homogenised DOISST.

## Results tables

Joint step model (C, 95% interval about +-2 SE; `results/breaks_model.csv`, `results/cci_trop_model.csv`):

| Reference | 1995-06 | 2002-08 | 2008-01 | 2016-11 (splice) | 2020-10 | Trend of difference (C/decade) |
|---|---|---|---|---|---|---|
| ERSSTv5, 35S-35N | -0.037 (0.010) | +0.058 (0.010) | +0.057 (0.009) | -0.016 (0.009) | +0.040 (0.010) | +0.034 |
| HadSST4.2, 35S-35N | -0.093 (0.009) | +0.098 (0.009) | +0.055 (0.010) | -0.015 (0.009) | +0.041 (0.012) | +0.031 |
| Homogenised DOISST, 35S-35N | -0.067 (0.007) | +0.079 (0.010) | +0.057 (0.012) | -0.018 (0.009) | +0.044 (0.007) | +0.033 |
| ESA CCI v3, 20S-20N | -0.099 (0.010) | +0.118 (0.008) | +0.065 (0.006) | -0.040 (0.010) | +0.046 (0.010) | +0.036 |
| GTMBA buoys (72) | -0.159 (0.013) | +0.104 (0.008) | +0.070 (0.005) | -0.047 (0.010) | +0.039 (0.011) | +0.012 |
| Reef pixels, homogenised DOISST | -0.088 (0.010) | +0.118 (0.016) | +0.043 (0.017) | +0.032 (0.013) | +0.050 (0.011) | +0.049 |
| Published DOISST, 35S-35N (for comparison) | -0.090 | +0.018 | +0.043 | -0.053 | +0.012 | -0.016 |

(The published-DOISST row differs because DOISST has its own steps at 2005, 2016 and July 2020.)

Smoothed step fields at the reef pixels (mean; `results/ct_step_fields_summary.csv`): 1995-06 -0.074, 2002-08 +0.102, 2008-01 +0.036, 2016-11 -0.014, 2020-10 +0.063 C (INSITU, L = 1000 km). The net change, present level minus the 1985-1995 level, is +0.11 C at the reefs.

SST trends 1985-2025 (C per decade, `results/trends_abs.csv`): CoralTemp 0.179 -> 0.147 (35S-35N), 0.166 -> 0.131 (20S-20N), 0.216 -> 0.181 (reef pixels); homogenised DOISST 0.146, 0.132 and 0.167.

MMM change after homogenisation (`results/mmm_shift_summary.csv`): +0.140 C (INSITU), +0.141 (ERSSTv5), +0.140 (HadSST4.2), +0.135 (DOISST HOM), +0.131 (L = 2000 km).

Monthly heat stress at the reef pixels, 1985-2025 trend per decade (`results/monthly_heat_trends.csv`):

| Metric | Published | Homogenised (INSITU) | Ratio (all fields) |
|---|---|---|---|
| Annual maximum DHM (C-months) | 0.45 (0.30-0.58) | 0.36 (0.22-0.46) | 0.78-0.82 |
| Reef pixels with DHM >= 1 C-month (%) | 20.2 (15.6-24.4) | 16.2 (11.3-20.0) | 0.80-0.82 |
| Months with HotSpot >= 1 C | 0.18 (0.07-0.28) | 0.12 (0.04-0.20) | 0.66-0.72 |

Reef pixels at bleaching-level heat stress (`results/dhw_annual.csv`, `results/dhw_event.csv`; range = six correction variants: INSITU L1000 and L2000, ERSSTv5, HadSST4.2, homogenised DOISST, uniform ESA CCI steps):

| Statistic | Official CRW composite | Recomputed (published CoralTemp) | Homogenised (INSITU) | Range of variants |
|---|---|---|---|---|
| 2023, annual max DHW >= 4 (%) | 43.9 | 43.6 | 37.1 | 37.1-37.7 |
| 2024, annual max DHW >= 4 (%) | 83.1 | 82.8 | 62.9 | 61.3-67.2 |
| 2025, annual max DHW >= 4 (%) | 54.9 | 54.5 | 40.8 | 40.7-43.9 |
| 2024, annual max DHW >= 8 (%) | 51.2 | 50.7 | 36.9 | 36.1-38.5 |
| 2023-2025, DHW >= 4 in any year (%) | 90.6 | 90.4 | 73.4 | 71.0-78.4 |
| 2023-2025, DHW >= 8 in any year (%) | 63.2 | 62.9 | 48.9 | 47.1-50.2 |
| 2024, reef-mean annual max DHW (C-weeks) | 9.71 | 9.67 | 7.61 | 7.59-7.78 |

The satellite-only variant (uniform ESA CCI steps, no in situ data) gives an MMM change of +0.128 C, a DHM trend ratio of 0.79 and 67.2% of reef pixels at DHW >= 4 in 2024.

Test of the correction (`results/validation.csv`): at the 72 GTMBA buoys, the standard deviation of the 12-month mean CoralTemp-minus-buoy difference falls from 0.064 to 0.031 C, and the step sizes fall to -0.05, +0.01, +0.02, -0.02 and 0.00 C. The buoy trend difference changes from +0.012 to -0.012 C per decade, so at the buoys the correction is slightly too large. At the reef pixels the trend difference against homogenised DOISST falls from +0.049 to +0.013 C per decade.

## Figures

- `figures/fig1_steps_series.png`: (a) CoralTemp minus ERSSTv5, HadSST4.2 and homogenised DOISST (35S-35N, 12-month running means) with the break dates; (b) reef pixels, GTMBA buoys and ESA CCI (20S-20N); (c) joint-model step sizes for all references.
- `figures/fig2_step_maps.png`: smoothed in situ step fields for the five dates and the net change, with the reef pixels.
- `figures/fig3_heat_stress.png`: (a) MMM change at the reef pixels; (b) annual maximum DHM, published and homogenised; (c, d) reef pixels with annual maximum DHW >= 4 and >= 8 C-weeks in 2023-2025 (official, recomputed, homogenised with the range of six variants).
- `figures/fig4_daily_dating.png`: the 1995 and 2002 steps at daily resolution (every eighth day) against ESA CCI, homogenised DOISST and moored buoys, with the ATSR-2 and AATSR start dates and the November 2002 merge.

## Limitations

- **The references have their own errors.** ERSSTv5 and HadSST4.2 share ICOADS ships and drifters; homogenised DOISST is fitted on them; CCI has its own sensor changes (sci:sha256:4e3a13fa) and the chained CCI series is approximate (CCI daily gaps); GTMBA buoys are equatorial open-ocean points. Step sizes for a single date differ by up to a factor of three between references (1995: -0.04 to -0.16 C). The dates, signs and the total trend excess agree.
- **Break dates were selected from the data**, so the random-date p-values are optimistic. The two dates without documentation (2008, 2020) are dated only to about one to three months.
- **Causes are not confirmed.** The 1995 and 2002 dates agree with the ATSR-2 (31 May 1995) and AATSR (23 July 2002) data starts in the OSTIA period; we did not inspect the OSTIA or GPB input logs.
- **The correction is smooth.** Fields are smoothed over 1000 km, so coastal and reef-scale step patterns are not resolved; the 10-90% range of the MMM change (+0.05 to +0.21 C) shows spatial structure that the smoothing may blur. The correction keeps the present level and changes the past. HotSpots and DHW do not depend on this choice, because a constant added to the whole homogenised record changes SST and MMM equally.
- **We did not correct noise.** CoralTemp sources differ in smoothing; ef9c2a57 shows that noise changes can bias DHW in the opposite direction. We did not have enough consecutive daily data (download limits on a shared link) to measure CoralTemp fast-variance changes.
- **Daily DHW only for 2023-2025.** The 1985-2025 trend results use the monthly DHM index; DHW trends over the full record need the full daily record (about 150 GB), which we could not download on the shared, congested link in this job. The 2008 and 2020 breaks are dated only to about one to three months (monthly data).
- **Reef pixels** are the 1,662 DOISST cells (0.25 degree) with coral survey sites from ef9c2a57, sampled at one 5-km CoralTemp pixel each; they are not the CRW 5-km reef mask, so the fractions are not the official CRW reef-area fractions.

## Reproduction

Python 3.12 with numpy, scipy, pandas, netCDF4, matplotlib and curl (`files/provenance/environment.txt`). Put `files/code/*.py` in `WORK/code/`, the shared datasets in `WORK/../datasets/<name>/`, and unpack the four cited campaign bundles to `WORK/scratch/prior/<first 12 hex digits>/`. Order (`files/code/run_all.sh`): `fetch_crw_official.sh`, `fetch_crw_monthly.sh`, `fetch_coraltemp_erddap.py` and `fetch_coraltemp.py` (daily; write only a 0.25-degree int16 sample to `scratch/ct_chunks/`), `oi_year.py`, `buoy_matrix.py`, `official_annual.py`, `build_monthly.py`, `analysis_monthly.py`, `breakpoints.py`, `fit_breaks_model.py`, `cci_monthly.py`, `step_fields_ct.py`, `mmm_shift.py`, `trends_abs.py`, `validate_correction.py`, `monthly_heat.py`, `daily_diffs.py`, `date_breaks.py`, `reef_daily.py`, `analysis_dhw.py`, figure scripts. All downloads go to local scratch folders, not into the bundle. Run time on the shared campaign host: monthly part about 1 h; daily downloads are limited by the network (about 10 MB per day of data).

To inspect the results without downloads, use `files/results/` (all tables; `ct_step_fields.npz` holds the smoothed step fields on the 1-degree grid, which are our correction and contain no CoralTemp values).

## Job information

Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-10e825eb44ad, topic earth-and-ocean-sciences, machine dell, model Claude Opus 5.5 (claude-opus-5-5). Data retrieved 2026-11-10 and 2026-11-11. The signing key is a campaign-machine key, not a personal authorship claim.

## References

- Skirving, W., et al., 2020: CoralTemp and the Coral Reef Watch Coral Bleaching Heat Stress Product Suite Version 3.1. Remote Sensing, 12, 3856, doi:10.3390/rs12233856.
- Roberts-Jones, J., E. K. Fiedler and M. J. Martin, 2012: Daily, global, high-resolution SST and sea ice reanalysis for 1985-2007 using the OSTIA system. J. Climate, 25, 6215-6232, doi:10.1175/JCLI-D-11-00648.1.
- Donlon, C. J., et al., 2012: The Operational Sea Surface Temperature and Sea Ice Analysis (OSTIA) system. Remote Sens. Environ., 116, 140-158, doi:10.1016/j.rse.2010.10.017.
- Maturi, E., et al., 2017: A new high-resolution sea surface temperature blended analysis. BAMS, 98, 1015-1026, doi:10.1175/BAMS-D-15-00002.1.
- Margaritis, G., E. C. Kent and G. L. Foster, 2025: Intercomparison of satellite-derived SST with logger data in the Caribbean - Implications for coral reef monitoring. PLOS Climate, 4, e0000480, doi:10.1371/journal.pclm.0000480.
- Liu, G., A. E. Strong and W. Skirving, 2003: Remote sensing of sea surface temperatures during 2002 Barrier Reef coral bleaching. Eos, 84, 137-141, doi:10.1029/2003EO150001.
- Huang, B., et al., 2017: ERSSTv5. J. Climate, doi:10.1175/JCLI-D-16-0836.1. Kennedy, J. J., et al., 2019: HadSST4. JGR Atmos., doi:10.1029/2018JD029867. Huang, B., et al., 2021: DOISST v2.1. J. Climate, doi:10.1175/JCLI-D-20-0166.1. Embury, O., et al., 2024: ESA SST CCI v3. Sci. Data, doi:10.1038/s41597-024-03147-w.
