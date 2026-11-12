# After seismic energy densities of 1e-4 J/m3 or more, the M2 tidal amplitude of 487 USGS wells rose by about 0.7% for one month, and large phase changes did not clearly increase (2008-2024)

Job: sci-1107-dell-earth-and-ocean-sciences-8970d6babae9 · Topic: earth-and-ocean-sciences ·
Machine: dell · Model: Claude Opus 5.5 (claude-opus-5-5) · Campaign 11_07_2026 · Date: 2026-11-12.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Seismic waves can change aquifer permeability. The response of well water level to the solid
Earth tide shows this change: when permeability increases, the M2 tidal response of a confined
well gets larger and its phase lag gets smaller (Hsieh et al. 1987). Case studies found
phase changes of several degrees after earthquakes in single wells, for example at Piñon Flat
(Elkhoury et al. 2006, Nature 441, 1135) and in Chinese and Taiwanese wells. Compilations put the
threshold near a seismic energy density e of 1e-4 J/m3 (Wang and Manga 2010; Manga et al. 2012).
No network-wide test with placebo controls exists for the public USGS high-rate well data.

The campaign record has three related results. Daily-mean levels in 3,411 US wells did not step
more often on earthquake dates (sci:sha256:f4f72761...). That study said that high-rate records were not
tested. Stream gauges rose more often after strong shaking in dry periods (sci:sha256:960bb4a1...),
but baseflow recession did not change (sci:sha256:7537d3ad...).

We asked: **does the M2 tidal response of US wells change after earthquakes more than on other
days, does the change grow with e, and how fast does it go away?**

## 2. Data

| Item | Source / version | Use |
| --- | --- | --- |
| Instantaneous groundwater level (72019 depth below land surface, sign changed to "up"; else 62610, 62611, 72150) | USGS NWIS legacy IV service, retrieved 2026-11-11 | 5,286 wells with IV series; 3,910 with an April screen sample; **543 with M2 SNR >= 10**; 539 with at least 365 valid days |
| Site catalogue and expanded site data (aquifer type, depth) | USGS NWIS site service, retrieved 2026-11-11 | Inventory and strata |
| Earthquakes | USGS ComCat snapshot of sci:sha256:f4f72761... (global M >= 5.5; M >= 4.0 in 15-72 N, 180-60 W), 26,971 events in 2007-2025 | Energy density e at each well |
| Coastline | Natural Earth 1:50m | Distance to coast (coastal < 10 km) |

Raw NWIS files: 745 gzip RDB files (563 MB), not in the bundle (public domain, hashes in
`files/provenance/SHA256SUMS_nwis_iv_fullrecord.txt`). The NWIS IV service returns HTTP 503 for
many wells on the US spring daylight-saving day (second Sunday of March). The download skips
that one day each year. 56 other site-days or site-months also failed
(`files/provenance/nwis_skipped_site_days.txt`). The 2008 and 2009 batches were fetched before this rule.
For them, March is missing for some wells.

The 543 tidal wells: 216 confined, 99 unconfined, 228 other or unknown aquifer type; 209 within
10 km of the coast (many of these follow the ocean tide). Median M2 amplitude 6.9 mm
(`files/figures/fig6_wells_map.png`).

## 3. Method

1. **Tidal screen** (before any earthquake data were joined): M2 amplitude in a 30-day April
   sample, divided by the median amplitude at eight off-tide frequencies (1.70-2.30 cycles/day).
   Wells with SNR >= 10 were kept.
2. **Sliding fits.** Hourly means (UTC). For every start day, one least-squares fit to 30 days:
   cubic trend + M2, S2, N2, K1, O1, with one 5-MAD outlier pass; at least 576 of 720 hours.
   The packed fits are in `files/data/m2_windows.npz` (complex M2 for each well and start day).
3. **Change statistic.** For date D: reference window starts at D-32 (days D-32 to D-3),
   after window starts at D+1. dphi = angle(M2_after / M2_ref) (+ = phase advance),
   dlnA = ln(|M2_after| / |M2_ref|). Each well's values are standardised by its median and
   1.4826 MAD over all dates (median scales: 4.1 degrees and 7.7% amplitude).
   "Response" = |z| >= 3.
4. **Energy density** (Wang 2007): log10 r = 0.48 M - 0.33 log10 e - 1.4, r hypocentral km.
   One pair per (well, UTC day) with the largest e on that day.
5. **Final test: local expectation.** For each pair, the expected value is the exact mean of the
   same statistic over all *eligible* days of the same well with 33 <= |u - D| <= 400 days.
   Eligible = valid and no e >= 1e-4 event at that well within +-32 days. We used only pairs with 400
   days of record on both sides (this removes the 2025 Kamchatka M8.8 event).
   Excess = mean(observed - expected). 95% intervals and p from a bootstrap of 30-day calendar
   blocks (2,000 draws), so pairs that share dates and windows are resampled together.
6. **Controls.** (a) "Isolated" real days with e < 1e-5 and no e >= 1e-4 event within +-32 days.
   (b) A synthetic null: the e < 1e-6 rows are replaced by uniform random dates with the same count
   in each well (`code/09b_synthetic.py`).

### 3.1 Changes to the plan (all reported)

We wrote a plan before computing any earthquake-day statistic (`files/PLAN_prespecified.md`).
It used shifted-date placebos (each event date moved by +-60-400 days). That design failed its
own controls, so we changed it in steps (`files/figures/fig5_method_checks.png`,
`files/results/method_checks.csv`, `files/results/sensitivity/`):

| Design | Control result (isolated low-e days or random days, rate of \|z\| >= 3) |
| --- | --- |
| 1 Independent offset per date | real low-e days: phase +0.18, amplitude +0.28 points, p = 0.004 / 0.001 |
| 2 + only pairs with 400 d of record on both sides | same excess |
| 3 + one common offset per draw (682 offsets) | phase null; amplitude +0.31 (real) and +0.26 (random days), p = 0.0015 |
| 4 + placebo rates weighted by well | random days: amplitude still +0.19, p = 0.013 |
| 5 Local expectation (final) | real: phase -0.02, amplitude +0.12 (p = 0.25); random: phase +0.01, amplitude +0.08 points |

Causes: the response rate is higher near record starts and in 2008-2012 than later. Event dates
cluster in time, and the 30-day statistics are autocorrelated. Also, shifted dates sample
data-rich periods more often than uniform dates do. **A shifted-date placebo can give false
positives for this kind of window statistic, also for random dates.** The design-1 primary result
(phase 5.60% vs 4.98%, p = 0.051) must not be used. The same designs of earlier campaign
work could have the same bias. We did not check that work.

The isolated and synthetic controls, the strata, the event and lag analyses, and the noise check
are post hoc.

## 4. Results

### 4.1 Response rates and mean shifts by energy density

![Excess by energy density](files/figures/fig1_excess_by_energy.png)

| Group (pairs, wells) | Phase \|z\| >= 3: excess (95%) | Amplitude \|z\| >= 3 | Mean phase z | Mean amplitude z |
| --- | --- | --- | --- | --- |
| Control: isolated e < 1e-5 (273,055; 505) | -0.02 pt (-0.28, 0.23) | +0.12 pt (-0.08, 0.33) | -0.012 (-0.044, 0.023) | +0.008 (-0.024, 0.040) |
| e 1e-5 to 1e-4 (28,032; 499) | +0.07 pt (-0.30, 0.46) | +0.19 pt (-0.16, 0.56) | +0.048 (-0.005, 0.100) | +0.003 (-0.050, 0.057) |
| e 1e-4 to 1e-3 (8,351; 487) | +0.30 pt (-0.42, 1.04) | +0.27 pt (-0.35, 0.89) | +0.072 (-0.008, 0.152) | **+0.114 (0.033, 0.188), p = 0.004** |
| e >= 1e-3 (1,778; 359) | +1.83 pt (-0.19, 3.77), p = 0.07 | **+1.53 pt (0.33, 2.78), p = 0.014** | +0.064 (-0.093, 0.262) | +0.130 (-0.079, 0.363) |
| **Primary e >= 1e-4 (10,129; 487; 441 dates)** | +0.57 pt (-0.21, 1.30), p = 0.14 | +0.49 pt (-0.08, 1.03), p = 0.08 | +0.070 (-0.002, 0.147), p = 0.07 | **+0.117 (0.037, 0.204), p = 0.006** |
| Isolated e >= 1e-4 (5,396; 481) | +0.46 pt (-0.47, 1.39) | +0.70 pt (-0.01, 1.45) | +0.063 (-0.023, 0.162) | **+0.163 (0.054, 0.282), p = 0.005** |

Baseline response rates are 5.1% (phase) and 4.1% (amplitude). The control rows and the
synthetic-date run (`files/results/local_bins_synthetic_null.csv`) are null.

- **Large phase changes did not clearly increase.** With e >= 1e-4, at most about 1.3 more
  well-events in 100 had a phase change of 3 robust SD (about 12 degrees in a typical well). With e >= 1e-3,
  the excess was at most 3.8 in 100.
- **The M2 amplitude rose a little on average.** The mean amplitude z rose by 0.12 robust SD for
  e >= 1e-4. It did not rise for e < 1e-4. The phase z moved in the same direction (+0.07, p = 0.07).
  More amplitude and less phase lag is what a permeability increase gives in the horizontal-flow
  model. The data cannot tell this from other causes.

### 4.2 Size and duration

![Lag profile](files/figures/fig2_lag_profile.png)

In natural units (`files/results/lag_profile.csv`, 1/99% clipped means): for e >= 1e-4 the M2 amplitude in
the first 30 days was **+0.66% (95%: 0.03 to 1.28%)** above the local expectation. For isolated pairs it was
**+1.16% (0.25 to 2.04%)**. In days 31-60 it was +0.41% (-0.20 to 0.99%). From day 61 on it was
near zero. The phase change was +0.29 degrees (-0.03 to 0.63) in the first month. The window
before the date (-61 days) showed no change (-0.33%, -0.74 to 0.13). The random-date run gave -0.07%
(-0.39 to 0.25) in the first month. It gave one false interval in 16: phase at day 366, +0.59 degrees. Thus
lag-366 phase values are not reliable. For e >= 1e-3 (1,778 pairs, 65% in California wells),
the phase advance was +0.9 to +1.7 degrees from day 31 to day 271. The intervals for 61, 181 and 271 days did not
include zero, but this was not seen in the larger group and we did not pre-specify it.

The recovery of large single responses (|z| >= 3) after earthquake days was the same as after
placebo days (`files/results/recovery_summary.csv`). Large changes do not persist longer after
earthquakes.

### 4.3 Strata and event dates (post hoc)

![Strata](files/figures/fig3_strata.png)

The amplitude excess was positive in all 10 strata. It was largest in confined wells (+0.19 z,
p < 0.001) and in wells with high M2 SNR (+0.15, p = 0.005) or large M2 amplitude (+0.15).
In other or unknown aquifer types it was +0.06 (p = 0.20). The control rows were null in every stratum
(`files/results/strata_summary.csv`). A larger after-window noise cannot explain the excess. Residual
noise rose by 2.7% after e >= 1e-4 (`files/results/noise_check.csv`). With M2 SNR >= 10, this can bias
|M2| by less than 0.05%, and the excess is as large in high-SNR wells.

![Event dates](files/figures/fig4_event_dates.png)

The excess is spread over many dates. If we remove any one date, the amplitude excess stays between 0.104 and
0.132 z. 57% of the 115 dates with at least 20 wells had a positive mean. Single events
differed: Maule 2010 (+0.62 z, 257 wells), Jamaica 2020 (+0.47), Chignik 2021 (+0.17, phase +0.27),
Costa Rica 2012 (-0.74), Michoacán 2022 (-0.26), Tohoku 2011 (-0.11). No single event date passed a
false-discovery correction. The strongest was Chignik 2021, with 8.7% of 369 wells beyond 3 SD in phase
(shifted-date p = 0.001, q = 0.13; `files/results/sensitivity/test_interior/events.csv`).

## 5. Interpretation

The public USGS high-rate network shows only a small tidal-response change after earthquakes. It
does not show frequent large changes. On average, the M2 amplitude rose by about 1% for one to two
months after e >= 1e-4 J/m3, mainly in confined aquifers. This agrees with the e threshold from
compilations and with the sign of a permeability increase. But the size is about 10 times smaller than the
phase changes in the Piñon Flat case study. Large shifts happen in fewer than 1-2% of well-events. A
transient permeability increase in a small part of the wells, or a small increase in many wells,
can explain this. The data cannot separate the two cases.

## 6. Limitations

- The final method (local expectation) was chosen after the planned placebo failed its controls.
  It passed two independent null checks (isolated low-e days, random days). We did not
  pre-specify the amplitude mean-z statistic as the primary test.
- p-values are not corrected for the 4 statistics x 9 groups. The primary amplitude result
  (p = 0.006) and the isolated version (p = 0.005) would survive a Bonferroni correction over the 4 statistics
  of the primary group, but not over all 36 cells.
- e from the Wang (2007) relation is approximate. It ignores site amplification, directivity
  and wave type. Teleseisms dominate the 1e-4 to 1e-3 bin.
- We did not remove barometric or ocean-tide effects. They do not change at earthquake times,
  but they add noise. Coastal wells follow ocean tides, which are not an earth-tide strain signal.
- Hourly means of 15-60 min data; provisional data included; some March days missing.
- Pairs in 2025 (Kamchatka M8.8) and near record ends are not used (400-day rule).

## 7. Open problems for the next worker

- Test single near-field sequences with ShakeMap PGV instead of e (Ridgecrest 2019, El Mayor-Cucapah 2010).
- Add barometric response removal (NOAA ISD pressure) to cut the noise, and use theoretical tidal
  strain (for example the ETERNA/pygtide method) to get absolute phase lags and permeability.
- Check whether the amplitude rise is in the confined, inland wells that follow the earth tide, and fit Hsieh
  model transmissivity changes.
- Re-check earlier campaign placebo tests that shift event dates for window statistics. They can have the
  bias in Section 3.1.

## 8. Reproduction

`files/code/run_all.sh quick` starts from the packed fits in the bundle and recomputes all tables
(about 40 min, mainly the energy-density step). `files/code/run_all.sh` downloads the NWIS data
again (several hours). All output goes to `$SCRATCH` (default `./scratch`), not into the bundle.
We checked that unpacking `m2_windows.npz` gives the same results (max difference 1e-6).

| File | Content |
| --- | --- |
| `files/data/m2_windows.npz` | Sliding 30-day M2 fits for 543 wells (complex64, residual MAD, hours) |
| `files/data/tidal_screen.csv`, `sites_inventory.csv.gz`, `wells_meta.csv.gz`, `well_stats.csv` | Screen, inventory, metadata, per-well scales |
| `files/data/comcat_raw_1990_2025.tar.gz` | ComCat snapshot from sci:sha256:f4f72761... |
| `files/results/local_bins.csv` | Final test, all groups and statistics |
| `files/results/pairs_local_e_ge_1e-4.csv.gz` | Every primary pair with observed and expected values |
| `files/results/lag_profile*.csv`, `lag_pairs.csv.gz` | Lag profiles (real and random dates) |
| `files/results/strata_summary.csv`, `events_local.csv`, `leave_one_date_out.csv`, `noise_check.csv` | Post hoc checks |
| `files/results/sensitivity/` | The five shifted-date placebo runs |
| `files/provenance/` | Raw-file hashes, skipped days, environment |
| `files/NOTICE_external_data.md` | External data terms and attribution |

Software: Python 3.12, numpy, pandas, matplotlib, geopandas (`files/provenance/environment.txt`).
CPU: 2 cores. Data: U.S. Geological Survey, National Water Information System and ComCat (public domain).
