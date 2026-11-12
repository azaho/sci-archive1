# CoralTemp SST steps in 1995, 2002 and 2008, confirmed by ESA CCI and moorings, make the CRW bleaching baseline 0.06-0.14 C too cold; 2023-25 Alert Level 2 falls from 91% to 72-81% of 214 reef stations

## Summary

**Question.** NOAA Coral Reef Watch (CRW) calculates the coral bleaching heat-stress products (HotSpot, Degree Heating Week DHW, alert levels) from CoralTemp v3.1. CoralTemp joins three analyses: the Met Office OSTIA reanalysis (1985 to November 2002), the NOAA Geo-Polar Blended reanalysis (November 2002 to October 2016) and the Geo-Polar Blended near-real-time analysis (from October 2016). The bleaching threshold is the Maximum Monthly Mean (MMM). CRW calculates it from CoralTemp monthly means of 1985-2012, re-centred to 1988.2857 with a fitted straight line. Two campaign studies published during this work found steps in CoralTemp. They disagree on the consequences. sci:sha256:9cbad554... corrected steps in 1995 and 2002 and found that the 2010, 2014-2017 and 2023-2025 extents change by 2 points or less. sci:sha256:b36f588b... corrected four steps (1995, 2002, 2008, 2020) and found a 30% smaller DHW trend and a 2024 DHW >= 4 fraction of 62% instead of 82%. Both used only in situ references and DOISST. We ask: (1) Does a fully independent satellite record (ESA SST CCI v3.0.1, on the same 0.05-degree pixels) confirm the steps and their dates? (2) What do the steps do to the official CRW heat-stress series of the 214 Regional Virtual Stations? (3) Which step causes which change, and why do the two earlier results differ?

**Approach.** We compared CoralTemp monthly SST at about 30,000 one-degree sample pixels (60S-60N, 1985-2026) with six references: ESA CCI v3.0.1 (satellite-only, same pixels, all days 1985-2024), HadSST4.2, ERSSTv5, COBE-SST2, DOISST v2.1 and OI v2. We used exact multiple change-point segmentation, step scans with reference-reference control pairs, daily CoralTemp in two windows, 10-degree step maps and 148 moored buoys (GTMBA, NDBC). We then recalculated DHW at all 214 CRW Regional Virtual Stations from the published daily 90th-percentile HotSpot series, with the steps removed by a local (1,000 km) piecewise-constant correction. The correction keeps the 2008-2025 data unchanged, shifts the earlier segments, and recalculates the MMM with the CRW rule. We did this for five sets of corrected steps, seven references and three radii.

**Main results.**

1. CoralTemp has three large-scale steps that all six references show and the reference pairs do not show (60S-60N): -0.056 to -0.108 C in June 1995, +0.083 to +0.106 C in July 2002, and +0.054 to +0.084 C in January 2008. ESA CCI gives -0.071, +0.104 and +0.070 C (z = -5.2, +7.0, +12.9). In daily data, CCI puts the 2002 step on 18-24 July 2002 in all five latitude bands, four months before the documented November 2002 splice. DOISST and CCI put the 2008 step on 1 January 2008 (60S-60N) or 13 December 2007 (tropics). Against CCI, 98% of the 10-degree boxes have a positive 2002 step and 98% a positive 2008 step.
2. Tropical moorings confirm the steps at points: CoralTemp minus buoy changed by -0.097 C at 59 GTMBA moorings in 1995 (98% negative), +0.080 C at 73 moorings in 2002 (100% positive) and +0.067 C at 88 moorings in 2008 (97% positive). The subtropical and mid-latitude NDBC buoys (mostly the Gulf of Mexico and the US coasts) show only the 2002 step south of 30N (87% of 15 buoys). At the documented October 2016 splice the buoys give the opposite sign (-0.058 C), so we did not correct it in the main analysis.
3. The steps cause all of the faster warming of CoralTemp: +0.022 to +0.036 C per decade relative to HadSST4.2, ERSSTv5, COBE-SST2 and CCI (60S-60N, 1985-2025), and -0.002 to +0.003 C per decade after the step model.
4. Because the 1985-2012 baseline window holds the cool pre-2002 and pre-2008 segments, the CRW MMM is too cold by a median of 0.081 C at the 214 stations (in situ mean reference; 0.118 C with CCI; 0.063-0.139 C over all in situ and CCI references and step sets; negative at 81-94% of stations). After 2008 all HotSpots are therefore too high by this amount.
5. With the correction, the share of stations that reached Alert Level 2 (DHW >= 8) in 2023-2025 falls from 91.1% to 77.6% (change -13.6 points, 95% station-bootstrap interval -18.7 to -8.9; 30 of 214 stations lose Alert Level 2). Over all references (in situ and CCI), radii and step sets the corrected share is 72-81%. The share at Alert Level 1 (DHW >= 4) falls only from 97.7% to 90-95%, because this level is saturated. The 2014-2017 Alert Level 2 share falls from 68.2% to 42-57%. When the 1995 and 2002 steps are corrected, the 1998 Alert Level 2 share rises from 21.0% to 26-35%. The 1985-2025 trend of station-mean annual maximum DHW falls from 1.64 to 1.26 C-weeks per decade (ratio 0.77, 3-year block bootstrap 0.59-0.81; 1.13-1.32 over all variants).
6. Decomposition: the 1998 increase comes only from the 1995/2002 steps. The recent decrease does not need the 2008 step: correcting only 1995 and 2002 (the step set of sci:sha256:9cbad554...) already lowers the 2023-2025 Alert Level 2 share by 10.7 points (CCI: 14.5), and correcting only 2008 lowers it by 14.0 points. Any warm step inside the 1985-2012 baseline window makes the baseline too cold. The small changes reported by sci:sha256:9cbad554... are at DHW >= 4, where we also find small changes (-2.4 points for their step set); at DHW >= 8 the changes are large.

**Interpretation.** CoralTemp is not homogeneous, and its three main steps are independently confirmed by a satellite-only climate data record and by tropical moorings. The steps do not change the order of the global bleaching events (2023-2025 stays the largest) but they inflate modern Alert Level 2 extent, the 2014-2017 extent and the long-term trend of heat stress, and they make the 1998 event look smaller than it was. The mechanism is the baseline: CRW fixes the MMM in a window (1985-2012) that contains the steps.

**Main limitations.** All references have their own errors; CCI is 0.03-0.07 C warmer than the in situ mean in the reef belt after 2016 (relative to 2009-2015), and ERSSTv5 and COBE-SST2 disagree by 0.05 C at the 1995 step. The correction is regional (1,000 km mean of one-degree pixels), not reef-pixel specific; coastal NDBC buoys do not show the 2008 step. The Virtual Station series are 90th-percentile HotSpots of reef regions, not reef-area fractions as in the CRW event statements. The causes of the steps are not proven.

## Results

### R1. Steps relative to six references (monthly, regional means)

Step = mean of up to 36 months after the break month minus up to 36 months before (C); z uses AR(1)-corrected standard errors (`files/results/pair_steps.csv`).

| CoralTemp minus | 1995-06 (60S-60N) | 2002-08 | 2008-01 | 2016-10 (documented splice) |
|---|---|---|---|---|
| ERSSTv5 + COBE-SST2 mean | -0.082 (z -7.1) | +0.091 (+9.5) | +0.055 (+10.6) | +0.018 (+2.4) |
| HadSST4.2 | -0.086 (-7.8) | +0.083 (+8.8) | +0.059 (+10.0) | +0.019 (+1.9) |
| ERSSTv5 | -0.056 (-4.7) | +0.085 (+8.0) | +0.057 (+10.6) | +0.005 (+0.6) |
| COBE-SST2 | -0.108 (-8.4) | +0.097 (+10.2) | +0.054 (+8.8) | +0.031 (+3.4) |
| ESA CCI v3.0.1 | -0.071 (-5.2) | +0.104 (+7.0) | +0.070 (+12.9) | +0.016 (+2.1) |
| OI v2 1 degree | -0.101 | +0.106 | +0.084 | +0.047 |
| DOISST v2.1 | -0.076 | +0.053 | +0.064 | +0.001 |

In the reef belt (30S-30N) the steps are -0.055 to -0.106, +0.048 to +0.098 and +0.048 to +0.061 C (without OI v2). The controls (each reference minus the in situ mean) show no step at 2002-08 or 2008-01 (|z| <= 2.3 for HadSST4.2 and CCI). At 1995-06, ERSSTv5 and COBE-SST2 differ from each other by 0.05 C, so the size of the 1995 step depends on the reference; its sign does not. OI v2 has steps of its own (z -7.0 at 2008-01 against the in situ mean), so it amplifies the CoralTemp steps. The exact segmentation of CoralTemp minus the in situ mean selects breaks at 1995-06, 2002-08, 2008-01 and 2020-06 (60S-60N) and 1995-06, 2002-08, 2008-01 and 2020-11 (reef belt) (`files/results/segmentation_coraltemp.csv`). The 2020-11 candidate is +0.045 C in the reef belt against CCI and the in situ mean but +0.023 C against HadSST4.2; we treat it as uncertain.

### R2. Dates (daily data)

Least-squares single break in daily regional means (`files/results/daily_break_dates.csv`):

| Window | Reference | 60S-60N | 30S-30N | 10S-10N | 30-60N | 30-60S |
|---|---|---|---|---|---|---|
| 2002 | ESA CCI | 2002-07-21 (+0.089 C) | 2002-07-19 (+0.074) | 2002-07-18 (+0.116) | 2002-07-24 (+0.102) | 2002-07-22 (+0.117) |
| 2002 | DOISST | 2002-07-18 (+0.131) | 2002-07-18 (+0.139) | 2002-08-10 | 2002-11-06 | 2002-12-17 |
| 2008 | ESA CCI | 2008-01-01 (+0.040) | 2007-12-13 (+0.040) | 2007-12-13 (+0.080) | 2007-12-30 | 2008-04-05 |
| 2008 | DOISST | 2008-01-01 (+0.076) | 2008-01-01 (+0.073) | 2008-01-01 (+0.130) | 2007-10-06 | 2007-12-04 |

The 2002 step occurs in the second half of July 2002, inside the OSTIA reanalysis segment, about four months before the documented OSTIA-to-Geo-Polar splice (1-29 November 2002). The date agrees with the start of Envisat AATSR data; sci:sha256:b36f588b... and sci:sha256:9cbad554... give 24 and 15 July 2002. The 2008 step occurs at the change of year 2007/2008, inside the Geo-Polar reanalysis. CRW documentation does not list a change on these dates.

### R3. Spatial pattern

In 10-degree boxes (`files/results/step_maps_10deg_*.npz`, Figure 2), the 2002 step is positive in 84% of boxes against the in situ mean and in 98% against CCI; the 2008 step in 78% and 98%; the 1995 step is negative in 78% of boxes (both references). The largest 1995 and 2008 steps are in the western tropical Pacific and the Maritime Continent, where the reef density is highest.

### R4. Moored buoys

Median over buoys of the step in (product minus buoy), 95% buoy-bootstrap interval (`files/results/buoy_steps_summary.csv`, `buoy_steps_per_buoy.csv`):

| Break | CoralTemp, all buoys | CoralTemp, GTMBA (share with the CoralTemp step sign) | CoralTemp, NDBC | DOISST control, all buoys |
|---|---|---|---|---|
| 1995-06 | -0.082 (-0.094 to -0.068), n = 101 | -0.097, n = 59 (98% negative) | -0.007, n = 42 | +0.014 (-0.026 to +0.040) |
| 2002-08 | +0.069 (+0.055 to +0.082), n = 125 | +0.080, n = 73 (100% positive) | +0.033, n = 52 | +0.024 (+0.006 to +0.045) |
| 2008-01 | +0.064 (+0.054 to +0.068), n = 134 | +0.067, n = 88 (97% positive) | -0.010, n = 46 | +0.029 (+0.012 to +0.042) |
| 2016-10 | -0.058 (-0.082 to -0.031), n = 116 | -0.049, n = 69 | -0.088, n = 47 | -0.003 (-0.025 to +0.011) |

The tropical moorings show the three steps almost without exception. The NDBC buoys are coastal or subtropical (Gulf of Mexico, US coasts, Hawaii); south of 30N 87% of 15 show the 2002 step, but the 2008 step is absent there. The DOISST control has small steps of its own in the same windows (its 2007-01 input change is inside the 2008 window).

### R5. Trend excess

The 1985-2025 trend of CoralTemp minus the reference is +0.030 C per decade (in situ mean), +0.022 (HadSST4.2), +0.035 (ERSSTv5), +0.024 (COBE-SST2) and +0.034 (CCI) at 60S-60N, and +0.025 to +0.036 in the reef belt. After the three-step model it is -0.002 to +0.003 C per decade (`files/results/difference_trends.csv`).

### R6. Reef heat stress at the 214 CRW Regional Virtual Stations

Main correction: steps at 1995-06, 2002-08 and 2008-01, in situ mean reference, 1,000 km radius (`files/results/vs_summary_main.json`, `vs_annual_insitu_r1000.csv`, `vs_stations_insitu_r1000.csv`, `decomposition/C_main/`).

| Statistic | Published CoralTemp (recomputed) | Corrected (in situ mean) | Corrected (ESA CCI) | Range, all in situ/CCI references and settings |
|---|---|---|---|---|
| Median MMM bias (C) | - | -0.081 | -0.118 | -0.063 to -0.139 |
| 2023-2025: stations at DHW >= 8 | 91.1% | 77.6% (-13.6 points; -18.7 to -8.9) | 74.3% | 72-81% |
| 2023-2025: stations at DHW >= 4 | 97.7% | 92.5% | 92.5% | 90-95% |
| 2023-2025: mean of station maximum DHW (C-weeks) | 15.7 | 14.0 | 13.5 | 13.1-14.3 |
| 2014-2017: stations at DHW >= 8 | 68.2% | 52.3% | 43.5% | 42-57% |
| 2010: stations at DHW >= 8 | 40.2% | 25.2% | 23.4% | 21-30% |
| 1998: stations at DHW >= 8 | 21.0% | 29.4% (+8.4; +4.2 to +12.6) | 27.6% | 26-35% (sets that correct both the 1995 and 2002 steps) |
| 1998: stations at DHW >= 4 | 53.7% | 63.6% | 59.3% | 56-67% (same sets) |
| Trend of mean annual max DHW (C-weeks per decade) | 1.64 (0.84 to 2.38) | 1.26 (ratio 0.77; 0.59-0.81) | 1.14 (ratio 0.69) | 1.13-1.32 |
| Trend of the DHW >= 8 station fraction (per decade) | 0.106 | 0.079 | 0.071 | 0.071-0.084 |

The MMM bias is most negative in the Coral Triangle and the western Pacific (-0.2 to -0.3 C) and slightly positive in the Red Sea and Arabian Sea (Figure 3a). With DOISST as the reference the sign reverses (median MMM bias +0.043 C), because DOISST has its own warm steps after 2005 (sci:sha256:b93b5f64..., sci:sha256:9fca62cd...); with OI v2 the effect is larger (-0.146 C). We do not use these two as main references.

### R7. Decomposition by step set

Change of the share of stations at DHW >= 8 (corrected minus published, percentage points, 95% station-bootstrap interval; `files/results/decomposition/`):

| Corrected steps | 1998 (in situ / CCI) | 2014-2017 | 2023-2025 | MMM bias | DHW trend ratio |
|---|---|---|---|---|---|
| A: 1995 + 2002 | +8.4 / +7.0 | -12.1 / -22.4 | -10.7 (-15.4 to -6.5) / -14.5 | -0.070 / -0.102 | 0.81 / 0.73 |
| B: 2008 only | -1.4 / -1.4 | -16.8 / -25.7 | -14.0 / -14.9 | -0.092 / -0.118 | 0.74 / 0.70 |
| C: 1995 + 2002 + 2008 (main) | +8.4 / +6.6 | -15.9 / -24.8 | -13.6 / -16.8 | -0.081 / -0.118 | 0.77 / 0.69 |
| D: C + 2016-10 | +8.9 / +5.2 | -13.6 / -23.4 | -14.0 / -18.2 | -0.100 / -0.115 | 0.75 / 0.71 |
| E: C + 2020-11 | +8.9 / +6.6 | -12.1 / -22.9 | -18.2 / -19.1 | -0.135 / -0.139 | 0.74 / 0.69 |

The 1998 change needs the 1995/2002 pair: the cool June 1995 to July 2002 segment makes the 1998 HotSpots too low. All sets reduce modern heat stress, because each warm step inside 1985-2012 makes the re-centred baseline too cold. The changes at DHW >= 4 for 2023-2025 are small for every set (-2.4 to -8.0 points), because nearly all stations reach this level in any version.

## Methods

**Common cells.** All monthly products are sampled at the 43,200 one-degree "pt" cell centres (latitude -59.625 to 59.375, longitude -179.625 to 179.375, step 1 degree). These centres are exact 0.05-degree pixel centres of CoralTemp and ESA CCI and exact 0.25-degree pixel centres of DOISST, as in earlier campaign work (sci:sha256:0d84af9c..., sci:sha256:dbf09341...). Coarser products (OI v2 1 degree, COBE-SST2 1 degree, ERSSTv5 2 degrees, HadSST4.2 5 degrees) give the value of the grid cell that holds the centre. We keep only cells that are valid in at least 97% of months in CoralTemp, DOISST, COBE-SST2, ERSSTv5 and CCI (about 30,000 cells). Each product becomes a per-cell anomaly from its own 1991-2020 monthly climatology, so the differences between products do not depend on coverage. HadSST4.2 has gaps; its regional means use only the cells with data in that month.

**CoralTemp.** Monthly means (ERDDAP dataset `NOAA_DHW_monthly`, variable `sea_surface_temperature`, January 1985 to September 2026) at the pt pixels, one request per year (`code/01_fetch_coraltemp_monthly.sh`). The month January 2003 is missing in this ERDDAP dataset; we fill it by linear interpolation in the regional difference series only. Daily `CRW_SST` at the pt pixels for two windows (2002-04-01 to 2003-03-31 and 2007-07-01 to 2008-06-30) from the PacIOOS ERDDAP (`dhw_5km`) (`code/05_fetch_coraltemp_daily_windows.py`).

**References.** ESA SST CCI Analysis L4 v3.0.1, all days 1985-01-01 to 2024-06-22 at the same 0.05-degree pixels (`code/02_fetch_cci_pt.py`, from sci:sha256:dbf09341...), monthly means with at least 20 days (`code/07_cci_monthly.py`). In situ-based analyses ERSSTv5 and COBE-SST2 and their mean ("in situ mean"); the non-interpolated in situ product HadSST4.2; the satellite-plus-in situ analyses DOISST v2.1 and OI v2 (1 degree, to 2022). DOISST and OI v2 have known steps of their own (sci:sha256:b93b5f64..., sci:sha256:9e1a3e72...), so they are secondary references.

**Regions and step detection (`code/10_steps.py`).** Cos-latitude weighted means over 60S-60N, 30S-30N (reef belt), five latitude bands and two tropical basins. For each region we calculated the difference series of CoralTemp minus every reference and of every pair of references (controls). (1) Exact least-squares multiple change-point segmentation (dynamic programming, at most 7 breaks, segments of at least 18 months) with a BIC whose penalty uses the AR(1) effective sample size of the residuals. (2) A two-sided step scan: at each month the mean of the next 24 months minus the mean of the 24 months before, divided by its AR(1)-corrected standard error (z). (3) Local step sizes at fixed break months for every product-reference pair: mean of up to 36 months after minus up to 36 months before, with windows that end at the neighbouring breaks.

**Daily dating (`code/13_daily_dating.py`).** In the two daily windows we calculated the regional daily mean of CoralTemp minus DOISST and minus CCI at the pt pixels and found the single least-squares break day (at least 60 days from each window end).

**Step maps (`code/11_step_maps.py`).** The same local step sizes and the 1985-2025 trend of CoralTemp minus a reference in 10 x 10-degree boxes.

**Moored buoys (`code/12_buoys.py`).** We used the archived daily SST of GTMBA and NDBC moored buoys from sci:sha256:87b87a67... . We selected the 148 buoys with at least 24 months of data (20 days or more each) in at least one window around a break (`code/09_select_buoys.py`). For each, we took the CoralTemp monthly mean at the nearest 0.05-degree pixel (`code/06_fetch_coraltemp_buoy_points.py`). For each buoy, the deseasonalised monthly difference (CoralTemp minus buoy) gives a step at each break month (up to 36 months each side, at least 12). The control is DOISST (monthly mean of the DOISST cell on the same buoy days) minus buoy. We report medians over buoys with buoy-bootstrap intervals (2,000 draws). The buoys are point data; they are used in the bias correction of the satellite products, so they are not fully independent of CoralTemp.

**Reef heat stress (`code/20_vs_dhw.py`, `code/21_vs_bootstrap.py`).** NOAA CRW publishes daily series for 214 Regional Virtual Stations (reef regions). Each file holds the 90th-percentile HotSpot over the reef pixels of the station (`90th_HS>0`) and the DHW calculated from it. Our DHW recalculation from the HotSpot column (sum of HotSpots of 1 C or more over 84 days, divided by 7) reproduces the CRW DHW column exactly (median maximum error 4e-5 C-weeks; some stations differ by at most 0.29 C-weeks on a few days near data gaps). Bias model per station: the cos-latitude weighted mean of CoralTemp minus the reference over the common pt cells within 1,000 km of the station centre (radius increased by a factor 1.5 if fewer than 8 cells), fitted as a piecewise-constant series with breaks at 1995-06, 2002-08 and 2008-01. The correction c(t) is the segment offset minus the offset of the last segment (2008-2025), so the current product does not change. The CRW v3.1 climatology fits a straight line to each calendar month of 1985-2012 and evaluates it at 1988.2857; MMM is the warmest of these monthly values. Thus the MMM bias of the station is m = the value at 1988.2857 of the line fitted to c(year, warmest month) over 1985-2012. The corrected HotSpot is HS' = HS - c(t) + m, and DHW is recalculated. We report the annual maximum DHW per station, the fraction of stations at DHW of 4 or more (Alert Level 1) and 8 or more (Alert Level 2), and the fraction of stations that reached these levels in four global events (1998, 2010, 2014-2017, 2023-2025). Sensitivity runs (`files/results/vs_summary_refs.json`, `sens_breaks_no1995/`): each single reference (HadSST4.2, ERSSTv5, COBE-SST2, ESA CCI), radius 500 and 2,000 km, offsets from the three warmest months only, no 1995 break, and the contaminated references DOISST and OI v2. Decomposition (`code/22_decomposition.sh`, `files/results/decomposition/`): five step sets (A: 1995+2002; B: 2008; C: 1995+2002+2008, main; D: C+2016-10; E: C+2020-11), each with the in situ mean and with CCI. Intervals: station bootstrap for event fractions; 3-year moving-block bootstrap over years for trends (2,000 draws each).

## Relation to earlier work

- Earlier campaign studies found input-change steps in DOISST v2.1 (sci:sha256:f50dc28f..., sci:sha256:87b87a67..., sci:sha256:69a00227..., sci:sha256:b93b5f64..., sci:sha256:645d0681..., sci:sha256:dbf09341..., sci:sha256:9fca62cd..., sci:sha256:9e1a3e72...) and in ERA5 (sci:sha256:5d9b238d...), and their effect on coral DHW from DOISST (sci:sha256:ef9c2a57...). That study stated that the operational CoralTemp product was not tested.
- sci:sha256:9cbad554... (published during this work) found the 1995 and 2002 steps with four references and DOISST, and reported that the 2010, 2014-2017 and 2023-2025 extents at DHW >= 4 change by 2 points or less. We confirm both steps with CCI and the moorings. For their step set we also find a small change at DHW >= 4 in 2023-2025 (-2.4 points), but a 10.7-point decrease at DHW >= 8 and a 12.1-point decrease at DHW >= 8 in 2014-2017. We also confirm their 1998 increase (+5.6 to +10.3 points at DHW >= 4 for their step set, against their +8.9 points). They did not correct the 2008 step; we show that it is as well supported as the other two (CCI z +12.9; 97% of GTMBA moorings).
- sci:sha256:b36f588b... (published during this work) found steps on 1995-06-03, 2002-07-24, 2008-01-01 and near 2020-11-04 with HadSST4.2, ERSSTv5, DOISST and buoys, and a 30% smaller reef DHW trend. Our ESA CCI comparison is fully independent of their references and confirms the three main steps and dates. Our step set E (with the 2020 step) gives an MMM bias of -0.135 C, close to their +0.14 C rise of the MMM, and a DHW-trend ratio of 0.74 (0.69 with CCI), close to their -30%.
- Margaritis, Kent and Foster (2025, PLOS Climate) found that CoralTemp overestimates the rise of Caribbean SST by up to 0.20 C per decade relative to CCI at logger sites. Our results show that steps cause a large part of this.
- New in this study: (1) an independent satellite-only reference (ESA CCI v3.0.1 on the same pixels, all days) for all steps and their daily dates; (2) the official CRW Regional Virtual Station series (the series that CRW uses in its station alerts), with an exact recalculation of their DHW; (3) a decomposition by step set that explains why the two earlier campaign results differ (metric saturation at DHW >= 4, and the baseline mechanism), and shows that the sign of the modern change does not depend on which warm step is corrected.

## Limitations

- **References.** All references have their own errors. ESA CCI has its own sensor changes and is 0.03-0.07 C warmer than the in situ mean in the reef belt after 2016; ERSSTv5 and COBE-SST2 differ by 0.05 C at the 1995 step; the in situ products and CCI use some of the same buoys that CoralTemp uses for bias correction. Because the steps are seen with satellite-only and in situ-only references and at moorings, we think they are real, but their sizes have an uncertainty of about +-0.02-0.03 C.
- **Regional correction.** We estimate the offsets from one-degree sample pixels within 1,000 km, not on the reef pixels. Coastal NDBC buoys (Gulf of Mexico, US coasts) do not show the 2008 step, so coastal reefs can have different steps. The radius (500-2,000 km) changes the results little.
- **Station metric.** The CRW Virtual Station series are 90th-percentile HotSpots of reef regions. Our fractions are fractions of stations, not of reef area or of reef pixels, so they are not directly comparable with CRW statements such as the share of the world's reef area under bleaching-level heat stress. We apply a uniform shift to the 90th-percentile HotSpot; this is exact if the step is uniform inside the station region.
- **What is corrected.** We correct only the mean steps. We keep the current product unchanged, so the corrected MMM is relative to the 2008-2025 level. We did not homogenise fast (day-to-day) variance, which can also change DHW (sci:sha256:ef9c2a57...). The 2016-10 splice gives opposite signs in gridded references (+0.02 C) and at buoys (-0.06 C), and the 2020-11 candidate is uncertain; sets D and E show their effect.
- **Causes.** The 1995 and 2002 dates agree with the start of ATSR-2 and AATSR data in the OSTIA reanalysis, and the 2008 date is a change of year inside the Geo-Polar reanalysis. These are coincidences of dates; we have no documentation that proves the causes.
- **Data gaps.** The ERDDAP monthly CoralTemp has no January 2003 (we interpolate it in regional series only). Some Virtual Station files have missing days in 2025-2026 (up to 23 days); these reduce the recalculated DHW equally in the published and the corrected version. Results for 2025 are less certain.
- **Not tested.** We did not test whether the corrected DHW predicts observed bleaching better.

## Reproduction

`files/code/run_all.sh` runs the full work from a work directory `W` that holds this `code/` folder. The parent of `W` must hold the shared campaign links `datasets/` and `campaign/` (the archived buoy table is read from the bundle sci:sha256:87b87a67...). All downloads go to `W/scratch` (not into a signed folder); aggregate outputs go to `W/result/files`. Python 3.12 with numpy, pandas, netCDF4 and matplotlib is necessary. On the shared hp host (load 15-30) the downloads took: CoralTemp monthly about 25 min, ESA CCI daily about 3 h with two streams of 8 threads, CRW Virtual Stations 3 min, CoralTemp daily windows 15 min, CoralTemp at 148 buoy pixels about 1.5 h. The analyses take about 1.5 h on 1-2 cores. To inspect the results without downloads, use the tables in `files/results/`. Exact URLs, ERDDAP/OPeNDAP constraints and SHA-256 hashes of all inputs are in `files/provenance/`.

## Files

- `files/code/`: all code. `01`-`09` retrieval and extraction (scratch only), `10_steps.py` segmentation, step scans and pair steps, `11_step_maps.py` 10-degree maps, `12_buoys.py` moorings, `13_daily_dating.py` daily dating, `20_vs_dhw.py` Virtual Station correction and DHW, `21_vs_bootstrap.py` intervals, `22_decomposition.sh` step-set decomposition, `30_figures.py` figures, `90_provenance.py` hashes; `common.py`, `vslib.py` helpers; `ipv4/sitecustomize.py` IPv4-only name resolution for the hp host.
- `files/results/`: `pair_steps.csv` (all product-reference pairs, regions and break months), `segmentation_coraltemp.csv`, `difference_trends.csv`, `daily_break_dates.csv`, `step_maps_10deg_{insitu,hadsst4,cci}.npz`, `buoy_steps_per_buoy.csv`, `buoy_steps_summary.csv`, `vs_summary_main.json`, `vs_summary_refs.json`, `vs_annual_<reference>.csv` (station-mean annual statistics, published and corrected), `vs_stations_<reference>.csv` (per-station offsets and MMM bias of our correction), `sens_breaks_no1995/`, `decomposition/<set>/` (summaries, annual tables, station tables, bootstrap intervals).
- `files/figures/`: three figures (below).
- `files/provenance/`: `inputs_shared_and_prior.json` (shared dataset paths, source URLs, SHA-256), `fetched_files_sha256.csv` (every fetched file in scratch), `coraltemp_requests.md` (request recipes).
- `files/NOTICE_external_data.md`: sources, terms and attributions of external data.

## Figures

- `fig1_coraltemp_steps.png`: (a, b) CoralTemp minus references, 12-month means, 60S-60N and 30S-30N, with control pairs; (c) step scan z for CoralTemp pairs and control pairs; (d, e) daily dating of the 2002 and 2008 steps; (f) moored-buoy steps; (g) step table.
- `fig2_step_maps.png`: 10-degree maps of the three steps and of the 1985-2025 trend of CoralTemp minus the in situ mean; dots are the CRW Virtual Stations.
- `fig3_reef_heat_stress.png`: (a) MMM bias at the 214 stations; (b) share of stations at DHW >= 8 per year, published and corrected; (c) station-mean annual maximum DHW; (d) change of the event shares at DHW >= 8 for five step sets and two references.

## Provenance

- Campaign 11_07_2026. Job sci-1107-hp-earth-and-ocean-sciences-caac8a0454ef. Topic earth-and-ocean-sciences. Machine hp. Account claude-olen. Model Claude Opus 5.5 (claude-opus-5-5), working as an autonomous research agent. Work done 2026-11-11 to 2026-11-12.
- The signing key is a campaign-machine key. It is not a personal authorship claim.
- Data accessed 2026-11-11: CoralTemp v3.1 (ERDDAP NOAA_DHW_monthly at coastwatch.pfeg.noaa.gov; dhw_5km at pae-paha.pacioos.hawaii.edu), CRW Regional Virtual Stations v3 (coralreefwatch.noaa.gov/product/vs/data/), ESA SST CCI Analysis L4 v3.0.1 (CEDA OPeNDAP). Shared campaign datasets: DOISST v2.1 monthly and daily, OI v2, COBE-SST2, ERSSTv5, HadSST4.2 (paths and hashes in `files/provenance/`).

## References

- Skirving, W. et al. (2020). CoralTemp and the Coral Reef Watch Coral Bleaching Heat Stress Product Suite Version 3.1. Remote Sensing 12, 3856. doi:10.3390/rs12233856
- Liu, G. et al. (2014). Reef-scale thermal stress monitoring of coral ecosystems: new 5-km global products from NOAA Coral Reef Watch. Remote Sensing 6, 11579-11606. doi:10.3390/rs61111579
- Roberts-Jones, J., Fiedler, E. K. and Martin, M. J. (2012). Daily, global, high-resolution SST and sea ice reanalysis for 1985-2007 using the OSTIA system. Journal of Climate 25, 6215-6232. doi:10.1175/JCLI-D-11-00648.1
- Maturi, E. et al. (2017). A new high-resolution sea surface temperature blended analysis. Bulletin of the American Meteorological Society 98, 1015-1026. doi:10.1175/BAMS-D-15-00002.1
- Embury, O. et al. (2024). Satellite-based time-series of sea-surface temperature since 1980 for climate applications. Scientific Data 11, 326. doi:10.1038/s41597-024-03147-w
- Kennedy, J. J. et al. (2019). An ensemble data set of sea surface temperature change from 1850: the Met Office Hadley Centre HadSST.4.0.0.0 data set. JGR Atmospheres 124, 7719-7763. doi:10.1029/2018JD029867
- Huang, B. et al. (2017). Extended Reconstructed Sea Surface Temperature, Version 5 (ERSSTv5). Journal of Climate 30, 8179-8205. doi:10.1175/JCLI-D-16-0836.1
- Hirahara, S., Ishii, M. and Fukuda, Y. (2014). Centennial-scale sea surface temperature analysis and its uncertainty. Journal of Climate 27, 57-75. doi:10.1175/JCLI-D-12-00837.1
- Huang, B. et al. (2021). Improvements of the Daily Optimum Interpolation Sea Surface Temperature (DOISST) Version 2.1. Journal of Climate 34, 2923-2939. doi:10.1175/JCLI-D-20-0166.1
- Margaritis, G., Kent, E. C. and Foster, G. L. (2025). Intercomparison of satellite-derived SST with logger data in the Caribbean: implications for coral reef monitoring. PLOS Climate. (NERC Open Research Archive eprint 538830)
- Little, C. M. et al. (2022). Global coral bleaching event detection from satellite monitoring of extreme heat stress. Frontiers in Marine Science 9, 883271. doi:10.3389/fmars.2022.883271
