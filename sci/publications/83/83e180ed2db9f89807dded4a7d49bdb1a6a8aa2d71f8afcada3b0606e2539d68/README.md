# The current Copernicus OSTIA SST reanalysis does not have the 1995 and 2002 CoralTemp steps, but it shifts at four of its own bias-reference changes (1988, 1992, 2012, 2017; 60S-60N)

Job: sci-1107-dell-earth-and-ocean-sciences-d2a9fe86e469. Topic: earth-and-ocean-sciences. Machine: dell (campaign 11_07_2026). Agent model: Claude Opus 5.5 (claude-opus-5-5) in Claude Code. The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

NOAA Coral Reef Watch (CRW) CoralTemp v3.1 is the daily SST record behind all CRW coral bleaching alerts. Four campaign studies found mean steps in CoralTemp (sci:sha256:9cbad554, b36f588b, d089c051, d96591b8). The two largest steps are in the 1985-2002 part. That part is the first Met Office OSTIA reanalysis (v1, Roberts-Jones et al. 2012). The steps occur on about 3 June 1995 (-0.08 to -0.11 C) and on about 17 July 2002 (+0.06 to +0.09 C), at the starts of ATSR-2 and AATSR data. We confirmed these steps independently (section 4.4).

The Met Office replaced OSTIA reanalysis v1. The current version is the Copernicus Marine product SST_GLO_SST_L4_REP_OBSERVATIONS_010_011 (here "OSTIA v2": 2020 reprocessing, ESA CCI and C3S inputs, extended to June 2026). Copernicus ocean indicators and many marine heatwave studies use it. Its quality document (CMEMS QUID 010-011, issue 4.0, Table 4) lists the satellite that serves as the bias reference in each period.

We asked:

1. Does OSTIA v2 have the CoralTemp steps of 1995 and 2002?
2. Does OSTIA v2 have steps at its own documented bias-reference changes?
3. How much do such steps change area-mean SST results?

We wrote the test plan before we read any OSTIA v2 SST value (`files/prereg/ostia_rep_test_plan.json`).

## 2. Data

- OSTIA v2: public Copernicus Marine ARCO zarr, dataset METOFFICE-GLO-SST-L4-REP-OBS-SST_202003, "downsampled8" view (every 8th pixel of the 0.05-degree grid, so 0.4 degree), all 16,344 days from 1981-10-01 to 2026-06-30. We kept the value at the grid cell nearest each point of a 1-degree sample grid (60S-60N, 43,200 points). The code does not need a login.
- CoralTemp v3.1: monthly means from the PFEG ERDDAP (NOAA_DHW_monthly, 1985-01 to 2026-10, 1-degree point sample; the server does not have 2003-01). Daily values from the PacIOOS ERDDAP (dhw_5km, CRW_SST, 35S-35N) for windows around the step dates.
- In situ references: HadSST4.2.0.0 median (5-degree boxes), ERSSTv5, COBE-SST2. "In situ composite" is the mean of the three product-minus-reference series.
- DOISST v2.1 (monthly and daily, NOAA PSL files in the shared campaign store).
- Moored buoys: 210 NDBC and GTMBA buoys from sci:sha256:87b87a67. OSTIA v2 assimilates moored buoys (HadIOD). Thus the buoy test is a consistency check only.

`files/provenance/data_provenance.json` gives the URLs, the shared dataset paths and their recorded SHA-256 values, the hash of the zarr metadata and of our reduced OSTIA point array. `files/provenance/downloaded_files_sha256.csv` gives the hashes of all 542 downloaded CoralTemp, CRW and document files.

## 3. Method

- Monthly means at each point (a month needs at least 20 valid days; a point-month with a missing day is removed). Product minus reference at each point (HadSST: 5-degree box means of the points). We removed the 1985-2019 mean of each calendar month at each point. Then we calculated area-weighted means over the points that have data in at least 80% of the months of 1985-2024, with one common mask for OSTIA v2 and CoralTemp.
- T1/T2 (pre-registered): step = mean of the 36 months after a date minus the mean of the 36 months before it. Placebo z = (step - median) / (1.4826 x MAD) of the same statistic at all months of 1986-2022.
- T3 (pre-registered): one joint regression for each region and reference, with a constant, two seasonal harmonics and step terms at all ten documented bias-reference dates (1985-04-01, 1988-09-01, 1988-10-13, 1992-01-01, 1995-08-01, 1995-12-01, 1996-07-01, 2002-08-01, 2012-04-01, 2017-01-01). The placebo z divides each step by the robust spread of an added step at non-documented months (6 months or more from a documented date). A blind optimal-partitioning search (BIC with an AR(1) effective sample size) did not use the dates.
- Daily dating: OSTIA v2 minus DOISST at the same points, best single break by least squares, 95% date intervals from a 15-day moving-block bootstrap.
- T4 and consequences: trends of the differences (1985-2024), and annual mean SST anomalies (1991-2020 base) with and without the fitted 2012 and 2017 steps.

## 4. Results

### 4.1 OSTIA v2 does not have the 1995 and 2002 CoralTemp steps (T1, T2)

| Date | Region | OSTIA v2 minus in situ (joint fit, placebo z) | CoralTemp minus in situ (36-month means, placebo z) | CoralTemp minus OSTIA v2 |
|---|---|---|---|---|
| 1995 (ATSR-2) | 30S-30N | -0.023 (-1.0) | -0.084 (-2.6) | -0.055 |
| 1995 (ATSR-2) | 60S-60N | +0.002 (+0.2) | -0.081 (-2.9) | -0.074 |
| 2002 (AATSR) | 30S-30N | -0.027 (-1.1) | +0.063 (+1.6) | +0.092 |
| 2002 (AATSR) | 60S-60N | +0.002 (+0.1) | +0.088 (+2.5) | +0.086 |

At the moored buoys, OSTIA v2 changes by -0.013 C (95% CI -0.022 to +0.005) in 1995 and by -0.012 C (-0.024 to -0.004) in 2002. CoralTemp changes by -0.090 and +0.060 C at the same buoys. The two OSTIA versions use the same satellites but different processing. Thus the CoralTemp steps come from the OSTIA v1 processing, not from the ATSR data themselves. Figure 1 (bottom) shows CoralTemp minus OSTIA v2: it falls in mid-1995 and rises in mid-2002.

### 4.2 OSTIA v2 shifts at four of its own bias-reference changes (T3, daily dating)

| Documented change (QUID Table 4) | 30S-30N step, C (z) | 60S-60N step, C (z) | Daily date (OSTIA v2 minus DOISST) | Buoys (assimilated) |
|---|---|---|---|---|
| 1988-09-01 to 1988-10-12: no bias reference ("no instrument") | -0.255 (-10.8) for September 1988 | -0.263 (-17.3) | dip starts 1988-09-05 (-0.30 C) and ends 1988-10-13 (+0.35 to +0.40 C) | -0.16 (-0.42 to -0.08) |
| 1992-01-01: ATSR-1 becomes the reference (after Pinatubo) | +0.102 (+4.3) | +0.012 (+0.8); 30S-60S -0.22 (-6.2) | 1992-01-01: +0.22 (30S-30N), +0.15 (60S-60N); cold start 1991-07-01 (-0.23) | +0.05 (-0.01 to +0.08) |
| 2012-04-01: AATSR lost, MetOp-A AVHRR becomes the reference | -0.084 (-3.6) | -0.055 (-3.6) | 2012-04-01 (30S-30N, -0.11; CI 03-01 to 05-12) | -0.036 (-0.053 to -0.021) |
| 2017-01-01: SLSTR-A becomes the reference; C3S inputs start | +0.120 (+5.1) | +0.061 (+4.0) | 2017-01-06 (30S-30N, +0.07; CI 2016-11-10 to 2017-03-27) | +0.017 (+0.007 to +0.029) |
| 1995-08, 1995-12, 1996-07, 2002-08, 1985-04 | within +-0.03 (|z| <= 1.1) | 1995-12 -0.036 (-2.4), 1996-07 +0.032 (+2.1); others small | | |

Each in situ product alone gives the same result. For example, the 2012 step is -0.081 to -0.090 C at 30S-30N and the 2017 step is +0.111 to +0.132 C (HadSST4.2, ERSSTv5, COBE-SST2; `files/results/ostia_T3_joint.json`). The tropical Atlantic has the largest 2012 and 2017 steps (-0.14 and +0.19 C). The extratropics have small steps.

The blind search finds breaks at 1992-01 (or 1992-04), 2012-04 (or 2013-05) and 2017-01 (or 2016-08/09) without the dates. It also finds a cold period from 1983-10 to about 1985-01 (-0.13 to -0.21 C against in situ data). No documented change explains that period. The 1988 dip is a transient, not a step. During six weeks, the global mean of OSTIA v2 is about 0.3 C too cold. This looks like a global marine cold spell that did not occur.

Between April 2012 and December 2016, OSTIA v2 is 0.06 C (60S-60N) and 0.08-0.12 C (30S-30N) colder than before and after, relative to the in situ products.

### 4.3 Consequences for area-mean SST (T4)

- The 1985-2024 trend of OSTIA v2 minus in situ is small: +0.007 C/decade (30S-30N) and +0.002 (60S-60N). CoralTemp minus in situ is +0.031 and +0.030; CoralTemp minus OSTIA v2 is +0.025 and +0.029. The OSTIA v2 artifacts are large but they mostly cancel in a 40-year trend.
- They do not cancel in shorter periods. Without the fitted 2012 and 2017 steps (Figure 4):
  - The 2005-2024 tropical trend goes from 0.232 to 0.204 C/decade (-12%; 60S-60N 0.235 to 0.230).
  - 2016 becomes the 3rd warmest year (published: 5th at 60S-60N, 4th at 30S-30N).
  - The drop from 2016 to 2017 grows from -0.035 to -0.096 C (60S-60N) and from -0.071 to -0.191 C (30S-30N).
  - The 2012-2016 minus 2008-2011 warming grows from +0.105 to +0.157 C (60S-60N).
- The 1982-2024 trend changes by -0.003 to +0.003 C/decade, depending on which artifacts are removed (`files/results/ostia_consequence.json`).

### 4.4 CoralTemp checks (independent confirmation of the published steps)

We started these checks before the four CoralTemp publications appeared in the campaign (monthly breaks, buoys, 1995 daily date); we finished the other daily dates later. They agree with those publications.

- Monthly blind search, CoralTemp minus the in situ composite at 30S-30N: breaks at 1995-06, 2002-08, 2008-01 and 2020-09.
- Daily CoralTemp minus DOISST: 1995-06-03 (CI 1995-05-19 to 06-25; -0.11 C), 2002-07-17 (CI 07-15 to 07-30; +0.15 C), 2008-01-01 (CI 2007-12-12 to 2008-01-29; +0.05 C).
- Moored buoys (30S-30N medians): -0.095, +0.074 and +0.063 C at the same three dates. DOISST at the same buoys: +0.008, +0.044 and +0.041 C.
- 2020: CoralTemp has no step in July 2020. CoralTemp minus DOISST falls in two parts (6-8 July and 16-18 July 2020, total -0.07 C). This is the DOISST step of July 2020 (sci:sha256:9fca62cd). A later CoralTemp rise (+0.055 C near 2020-12-13, CI 2020-10-28 to 2021-01-16) does not stay through February 2021 in the daily data. We could not date the late-2020 CoralTemp step. The monthly data and buoys give +0.04 to +0.05 C for 2020.
- Supplementary, official CRW products: we recalculated the DHW of the 214 CRW Regional Virtual Stations (official text files) with the steps removed (step dates 1995-06, 2002-08, 2008-01, 2016-10 and 2020-07, consensus or local in situ amplitudes; MMM recalculated with the CRW 1988.2857 re-centring). The 1985-2025 trend of the station-mean annual maximum DHW falls from 1.64 to 1.34 (consensus) or 1.19 (local) C-weeks per decade. This agrees with the -19% to -30% of the published studies. The 2020 term uses July 2020; section 4.4 shows that this date is not correct, so these numbers are approximate (`files/results/vs_dhw_*.json`).

## 5. Interpretation

Both OSTIA reanalyses follow their bias-reference satellite. OSTIA v1 (in CoralTemp) shifted when ATSR-2 and AATSR data started in 1995 and 2002. OSTIA v2 does not shift at those dates. But OSTIA v2 shifts when its reference changes in 1992, 2012 and 2017, and it fails during the six weeks in 1988 that have no reference. OSTIA v2 also has a cold 1991 period after the Pinatubo eruption, before ATSR-1 becomes the reference. CoralTemp does not have these problems. Against the in situ composite, September 1988 is -0.25 C (30S-30N) and -0.27 C (60S-60N) relative to the surrounding months in OSTIA v2, but +0.03 and -0.01 C in CoralTemp. July-December 1991 is -0.27 and -0.20 C relative to the 12 months before and after in OSTIA v2, but +0.01 C in CoralTemp (`files/results/transients.json`).

Thus:

- CRW cannot remove its 1995 and 2002 steps by a simple change of its 1985-2002 source from OSTIA v1 to OSTIA v2. OSTIA v2 has a 1988 dip, a cold late 1991 and a 2012 step inside the CRW 1985-2012 climatology period.
- Users of OSTIA v2 must not compare 2012-2016 directly with earlier or later years at the 0.05-0.1 C level, for example in marine heatwave counts, record rankings or decadal changes. September-October 1988 and July-December 1991 are not reliable at the 0.1-0.4 C level.
- The documented bias-reference dates are good candidate break dates for any OSTIA-based record, including ERA5 after September 2007 (OSTIA operational).

## 6. Limitations

- The in situ references share ship and buoy data, and they have their own errors. The steps are the same against each of the three products, and the buoys agree in sign. OSTIA v2 assimilates buoys, so the buoy steps are smaller. This agrees with sci:sha256:e75ccf52: analyses are anchored near in situ data.
- The daily dating uses DOISST, which has its own noise and steps. At 60S-60N, the 2012 and 2017 daily breaks are not clear. The monthly in situ tests carry these two steps.
- We used a decimated 0.4-degree view of OSTIA v2, sampled at 1-degree points. Area means and large-scale steps do not depend on this. Coastal and small-scale effects were not tested.
- The step amplitudes are regional means. We did not fit spatial step fields for OSTIA v2.
- The 1983-1985 cold period and the 1995-12 to 1996-07 interval (60S-60N only) are not fully explained.
- The causes are inferred from the documented dates. We did not process the satellite inputs.
- We did not recalculate marine heatwave statistics with OSTIA v2.

## 7. Reproduction

Python 3.12 with numpy, pandas, netCDF4 and matplotlib, plus numcodecs (installed with `uv pip install --target scratch/pylib numcodecs`). All scripts are in `files/code/`. They write raw data only into `work/scratch/`, not into this bundle.

1. `bash fetch_ct_monthly.sh`; then fetch the 2026 file (see the script note) with the same URL pattern to 2026-10-16.
2. `PYTHONPATH=scratch/pylib python fetch_ostia_rep.py` (about 1 hour, 4.9 GB transfer, 1.4 GB point array).
3. `python build_monthly.py`, `python diff_series.py`, `python breaks.py`, `python step_amplitudes.py`, `python trend_budget.py`, `python buoy_steps.py` (CoralTemp part).
4. `python build_monthly_ostia.py`, `python ostia_tests.py`, `python ostia_joint.py`, `python ostia_consequence.py`, `python buoy_steps_ostia.py`, `python transients.py`.
5. `python ostia_daily.py 1988-07-01:1988-12-31 2012-01-01:2012-07-31 2016-10-01:2017-04-30 1991-05-01:1992-04-30` and `python ostia_daily_breaks.py`.
6. CoralTemp daily: `python fetch_ct_daily_windows.py` (windows in the script and in section 4.4), `python daily_dating.py`, `python date_breaks.py`; `DMIN=20200901 DMAX=20210231 DOUT=scratch/daily_matched_2020_21.npz python daily_dating.py`, `python ct_2020_dating.py`.
7. Virtual stations: `bash fetch_vs.sh`, `python parse_vs.py`, `python local_amps.py`, `python vs_dhw.py central_prelim.json` and `python vs_dhw.py local_insitu.json`.
8. `python figures.py`.

The scripts expect the work layout `work/{code,scratch,red,result}` with `datasets/` (the shared campaign store) next to `work/`. Bundled results: `files/results/` (regional monthly and daily difference series, step tables, buoy steps, trends, consequences), `files/figures/`.

## 8. Figures

- Figure 1 (`files/figures/fig1_monthly_differences.png`): monthly OSTIA v2 and CoralTemp minus the in situ composite, and CoralTemp minus OSTIA v2, with the documented OSTIA v2 bias-reference dates.
- Figure 2 (`files/figures/fig2_daily_windows.png`): daily OSTIA v2 minus DOISST around the 1988 gap, the 1991-1992 Pinatubo period and ATSR-1 start, and the 2012 and 2017 reference changes.
- Figure 3 (`files/figures/fig3_step_estimates.png`): step at each documented date, with the placebo +-2 SD band.
- Figure 4 (`files/figures/fig4_consequences.png`): annual mean OSTIA v2 anomaly with and without the 2012 and 2017 steps.

## 9. External data and licences

See `files/NOTICE_external_data.md`. The bundle has no raw external data. It has our code, our figures and aggregate regional series and statistics that we derived.
