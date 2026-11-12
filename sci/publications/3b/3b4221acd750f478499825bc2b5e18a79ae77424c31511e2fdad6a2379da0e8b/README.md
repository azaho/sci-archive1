# Four stations near Anchorage shaken at 17-26 cm/s in the 2018 Mw 7.1 earthquake had 0.5% lower 1-4 Hz noise velocity in December 2018 than in three other winters; four winters cannot exclude weather

Job: sci-1107-dell-earth-and-ocean-sciences-e1e1f7d97e35. Topic: earth-and-ocean-sciences. Machine: dell (campaign 11_07_2026). Model: Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Strong shaking can decrease the seismic velocity of the shallow ground. The velocity then recovers slowly ("healing"). Ambient-noise interferometry measures this change (dv/v) without active sources. The campaign record had no ambient-noise dv/v study. Earlier campaign results examined other subsurface responses to shaking: well water levels and tidal response, streamflow and baseflow. Section 9 lists them.

The 30 November 2018 Mw 7.1 Anchorage earthquake (intraslab, 47 km depth, USGS us1000hyfh) shook the Cook Inlet region at 17-26 cm/s PGV. A web search found no ambient-noise dv/v study of this event.

Tested question: **Did the 2018 earthquake cause a measurable decrease in near-surface seismic velocity at broadband stations near Anchorage? Is that decrease larger than the normal difference between winters?**

The main problem is that Alaska winters change dv/v strongly. Frozen ground and snow cause dv/v changes of 0.3-1.7% at 1-4 Hz between October-November and December-January. The earthquake occurred at the start of this seasonal change. For this reason, the test compares the event winter with other winters on the same calendar days ("placebo winters"). It also compares strongly shaken stations with weakly shaken control stations in the same region.

## 2. Data

All seismic data come from the EarthScope FDSN dataselect service (`https://service.earthscope.org/fdsnws/dataselect/1/query`), channel BHZ (50 samples/s):

| Group | Station | Network | 2018 PGV, ShakeMap grid (cm/s) | 2018 PGV, observed (cm/s) | 2016 Iniskin PGV, grid (cm/s) |
| --- | --- | --- | --- | --- | --- |
| shaken | PMR (Palmer) | AT | 26.4 | - | 3.4 |
| shaken | CAPN (Kenai) | AK | 22.0 | 23.4 | 4.9 |
| shaken | SSN (Susitna) | AK | 17.1 | 18.3 | 1.7 |
| shaken | RC01 (Anchorage hillside) | AK | 17.0 | - | 4.1 |
| control | SKN (Skwentna) | AK | 5.0 | 4.2 | 1.5 |
| control | HOM (Homer) | AK | outside grid | 4.5 | 4.9 |
| control | SWD (Seward) | AK | 2.7 | 1.9 | 3.2 |

- **Time windows.** 08:00-14:00 UTC (local night) each day, which is 6 h/day. Shaken stations: 1 October to 31 January of the winters 2016-17, 2017-18, 2018-19 and 2019-20. Control stations: 1 October to 31 December of the same winters. In total there are 3,036 non-empty station-day files (3.4 GB). Their SHA-256 hashes are in `files/provenance/raw_mseed_sha256.csv`.
- **PGV.** From USGS ShakeMap version 8 (ak20419010) for 2018 and version 7 (ak12496371) for 2016: the `grid.xml` value at each station, and the observed station PGV from `stationlist.json` where it exists (`files/provenance/pgv.csv`).
- **Weather.** From NOAA NCEI GHCN-Daily by_station files: Anchorage Intl USW00026451 (for RC01 and SSN), Kenai AP USW00026523 (CAPN), Palmer AP USW00025331 (PMR), Talkeetna AP USW00026528 (SKN; the Skwentna record ends in 2016), Seward AP USW00026438 (SWD) and Homer AP USW00025507 (HOM). Soil temperature at 5 cm comes from the USCRN daily01 station Kenai 29 ENE. The derived daily covariates are in `files/provenance/weather.csv`. Input hashes are in `files/provenance/aux_inputs_sha256.csv`.

## 3. Method

1. **Daily autocorrelation (`acf_daily.py`).**
   - Prepare: merge, demean, decimate to 25 samples/s, pre-filter 0.3-6 Hz.
   - Split the 6 h into 5-min windows. Reject windows with transients: rms above 2x the daily median, or a peak above 8x.
   - Band-pass to 0.5-1, 1-2 and 2-4 Hz, apply 1-bit normalisation and autocorrelate (ZZ). Average the windows to one function per day.
   - `acf_daily_hf.py` does the same at 50 samples/s for 4-8 and 8-16 Hz.
2. **dv/v by stretching (`run_dvv.py`, `dvv.py`).**
   - The reference is the mean of all days from 1 October to 25 November in all four winters. This gives one common reference, before the earthquake and before most freezing. The reference is refined once.
   - Stretch grid: +/-3%, 301 steps, with parabolic refinement.
   - Coda lag windows: 6-20 s (0.5-1 Hz), 3-12 s (1-2 Hz), 1.5-8 s (2-4 Hz), 1-5 s (4-8 Hz) and 0.5-3 s (8-16 Hz).
   - Positive dv/v means a faster medium.
   - Outputs are daily values (1-day stacks) and 5-day moving stacks.
3. **Placebo-winter step (`placebo.py`).**
   - For each station and band, fit the daily dv/v from 1 October to 31 December (or to 31 January) of all four winters with three parts:
     - one intercept for each winter;
     - an optional weather term: none, sqrt(freezing degree-days since 1 October), or USCRN 5-cm soil temperature;
     - a step that is one from 6 December (to 31 December or 31 January) in one "test" winter.
   - Days 1-5 December of the test winter are removed (strongest aftershock period).
   - Fit the same model four times, once with each winter as the test winter. The 2018 step is then compared with the three placebo steps.
   - Standard errors are HAC (Newey-West, 10 lags).
4. **Group test (`final_tables.py`, `key_stats.py`).** Average the 1-2 and 2-4 Hz steps for each station. Then average over the shaken group and over the control group. "Shaken minus control" is a difference-in-differences: it removes weather that the whole region shares. Two p-values are reported:
   - a rank p-value over the 4 winters (minimum possible = 0.25);
   - a t prediction-interval p-value: the 2018 value against the 3 placebo values, df = 2, normal assumption.
5. **Time course (`timecourse.py`).** Daily dv/v of one winter minus the mean of the other three winters on the same calendar day, in 10-day bins.
6. **Synthetic injection.** Stretch the 2018-19 post-event daily autocorrelations by -0.25% and -0.5%, then process them again. This shows whether the pipeline recovers such a step.
7. **Pilot (`files/pilot/`).** The first design used 1 h/day at 14 stations (August 2018 - April 2019). The noise was 0.3-1.5% (5-day stacks), so this design could not resolve sub-percent changes. The pilot outputs are kept as evidence for this design choice.

## 4. Results

### 4.1 December step at 1-4 Hz, per station (percent; mean of the 1-2 and 2-4 Hz bands; step from 6 to 31 December against the October-November level)

No weather term:

| Station | PGV 2018 | 2016-17 | 2017-18 | **2018-19** | 2019-20 | 2018 minus mean of others | 2018 rank (1 = lowest) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| PMR | 26.4 | 0.10 | 0.24 | **-0.12** | 0.31 | -0.34 | 1 |
| CAPN | 22.0 | 0.83 | 0.31 | **-0.45** | 0.05 | -0.85 | 1 |
| SSN | 17.1 | 1.60 | 0.54 | **0.24** | 0.28 | -0.56 | 1 |
| RC01 | 17.0 | 0.07 | 0.33 | **-0.16** | 0.22 | -0.37 | 1 |
| SKN (control) | 5.0 | 0.14 | -0.29 | -0.13 | -0.50 | +0.09 | 3 |
| HOM (control) | 4.5 | -0.06 | -0.12 | 0.07 | -0.03 | +0.14 | 4 |
| SWD (control) | 2.7 | 0.05 | 0.04 | -0.09 | -0.08 | -0.09 | 1 |

- All four shaken stations had their lowest December step in 2018-19.
- With a sqrt(freezing degree-day) term, 2018 is lowest at 3 of 4 shaken stations (SSN is second lowest). With a soil-temperature term, 2018 is lowest at 4 of 4 (`files/results/station_anomalies.csv`).
- The control stations show no clear 2018 deficit. At SWD, 2018 is lowest by only 0.01% (Figure 1).

### 4.2 Group means and difference-in-differences (percent, `files/results/key_stats.json`)

| Weather term | Series | 2016-17 | 2017-18 | **2018-19** | 2019-20 | 2018 anomaly | t-pred one-sided p | rank p |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| none | shaken | 0.65 | 0.36 | **-0.12** | 0.22 | -0.53 | 0.087 | 0.25 |
| none | control | 0.04 | -0.12 | **-0.05** | -0.20 | +0.05 | 0.61 | 0.75 |
| none | shaken minus control | 0.61 | 0.48 | **-0.07** | 0.42 | -0.58 | 0.019 | 0.25 |
| sqrt(FDD) | shaken minus control | 0.17 | 0.13 | **-0.39** | 0.14 | -0.54 | 0.001 | 0.25 |
| soil 5 cm | shaken minus control | 0.50 | 0.35 | **-0.30** | 0.25 | -0.67 | 0.023 | 0.25 |

The shaken-minus-control difference is negative only in 2018-19, for all three weather models. The parametric p-values (0.001-0.023) depend on a normal model fitted to only three placebo winters. The rank test cannot go below 0.25 with four winters.

### 4.3 Other bands

- **0.5-1 Hz.** 2018 is not low: the mean anomaly is +0.28 to +0.41%. The 2016-17 winter is the outlier there (lowest at 4 of 4 stations).
- **4-8 and 8-16 Hz.** There is no consistent sign. 2018 is lowest at RC01 and SSN at 4-8 Hz, but highest at CAPN and PMR. The group mean anomaly is -0.04 to -0.02%.
- **Conclusion.** The 1-4 Hz deficit does not appear in the lower or the higher band.

### 4.4 Timing (Figure 2, `files/results/timecourse.csv`)

At the shaken stations (1-4 Hz), the 2018-19 anomaly against the other winters was:

| Days after the earthquake | 2018-19 anomaly | Placebo winters, same statistic |
| --- | --- | --- |
| before the event (1 October - 29 November) | -0.17 to +0.16% | - |
| days 1-9 (1-9 December) | -0.09% (bin mean); -0.30% (median of station-bands) | -0.19 to +0.05% |
| days 10-39 (10 December - 8 January) | -0.61, -0.43, -0.54% (10-day bins) | single bins from -0.43 to +0.66% |
| after 9 January | near zero (-0.15 to +0.03%) | - |

- Aftershocks removed many 5-min windows in days 1-9. Mean accepted windows fell from about 71 per day to 40-55 at RC01, SSN and PMR. Aftershock coda also gave positive daily spikes, up to +2.5% at SSN 2-4 Hz.
- The deficit was therefore **not largest immediately after the shaking**. It grew after about 10 days and stopped suddenly after about 40 days. This shape does not agree with simple coseismic damage followed by logarithmic healing, where the largest decrease is at time zero.

### 4.5 Detectability (`files/results/injection.csv`)

The pipeline is linear for these step sizes. At 1-4 Hz, an injected -0.25% step was recovered as -0.20 to -0.26% (median -0.23%), and a -0.50% step as -0.13 to -0.51% (median -0.50%). The one low value (-0.13%) is RC01 at 2-4 Hz, where the stretch search was unstable. The detection limit therefore comes from the variability between winters, not from the measurement. The standard deviation of the December step across the three placebo winters is 0.1-0.7% at single stations. For the shaken-minus-control difference it is 0.02-0.13%.

## 5. Interpretation

- **What the evidence supports.** In December 2018, near-surface velocity at 1-4 Hz was about 0.5% lower than expected at all four strongly shaken stations. It was not lower at the three weakly shaken stations. Both points agree with a shaking-induced velocity decrease of a size usual for PGV near 20 cm/s.
- **What makes the earthquake explanation weak:**
  1. There are only four winters. A nonparametric test cannot give p below 0.25, and the parametric p-values depend on three placebo values.
  2. The deficit started about 10 days after the earthquake, not at once. It disappeared suddenly in early January, as a seasonal frost or snow process would.
  3. The control stations are coastal or lowland and have a much smaller seasonal rise. So "shaken minus control" also removes less of the frost signal than it removes at the shaken stations. A winter in which the frost rise at the shaken stations came late gives the same pattern. Anchorage had the deepest December snow cover of the four winters in 2018 (mean depth 194 mm, against 71-168 mm). Snow insulates the ground and can delay frost. But the Kenai soil-temperature covariate did not remove the deficit.
- **Result statement.** A coseismic decrease of more than about 0.6-0.9% (the largest per-station anomaly) in the 6-31 December mean is not consistent with these data. A decrease of about 0.5% is possible, but this design cannot separate it from the timing of winter frost.

## 6. Limitations

- Only 6 h/day of vertical-component data was used, to keep the shared network load low (3.4 GB in total). Full-day, three-component data would decrease the noise by roughly 2-3 times.
- A single weather station per seismic station was used, and soil temperature only at Kenai. No station measures frost depth.
- PGV for RC01 and PMR comes from the ShakeMap grid only. The control station HOM is outside the 2018 grid, so its PGV is the observed value.
- The stretching method assumes a uniform velocity change within the coda window. It ignores changes in the noise source, for example ocean microseism and wind, between winters. The 0.5-1 Hz band is the most sensitive to source changes.
- At RC01 2-4 Hz, the 2018-19 dv/v was already about -0.5% from mid-November 2018, before the earthquake (Figure 3). Part of the RC01 deficit is thus not caused by the earthquake.
- The 2016 Iniskin earthquake (PGV 1.5-5 cm/s at these stations) was not analysed. Its date (24 January 2016) is outside the winters used.

## 7. What remains open (for the next worker)

- **Add more winters** (2015-16, 2020-21 to 2023-24 are available for all 7 stations). This lowers the nonparametric limit (8 winters give a minimum p of 0.125) and gives a better frost model. `fetch_days.py` with the same arguments takes about 10 minutes per winter.
- **Use full days and horizontal components**, with cross-component correlations, at PMR and CAPN, the two stations with the largest PGV and the lowest noise. This would test whether a decrease is present on day 1-2 after the event, before most freezing.
- **Add stations on soft basin sediments**, which were not used here because of data gaps around the event: FIRE (gap 29 October - 7 December 2018) and the AK K2xx strong-motion stations in Anchorage.
- **Model frost directly**, for example with Stefan-equation frost depth from air temperature and snow, so the shaken stations need not rely on the controls.

## 8. Reproduction

- `files/code/reproduce.sh` regenerates everything into a separate scratch folder (default `./scratch`; never into the publication). It needs Python 3.12 with obspy 1.5.1, numpy 2.5.4, scipy 1.18.1, pandas 3.1.1 and matplotlib 3.11.2, about 3.5 GB of disk and about 1.5 h of download.
- For re-analysis without download, use the daily 0.5-4 Hz autocorrelation functions for all 7 stations in `files/acf/` (NPZ; arrays `dates`, `nwin`, `fs`, `acf_<band>`). Then run steps 5-8 of `reproduce.sh`.
- The dv/v series (daily and 5-day) are in `files/dvv/`. All fitted steps are in `files/results/*placebo_steps*.csv`. Summary tables are in `files/results/`.

## 9. Related campaign publications

- sci:sha256:65679562d2a3b84f710cd1ae617b7b903b4dbc94ccac30ad462dc14a79b760d6: the M2 tidal amplitude of US wells rose about 0.7% for a month after seismic energy density of 1e-4 J/m3 or more. That is another transient change of shallow-crust properties after shaking. The present work gives a seismic-velocity view of a similar transient and of its weak detectability.
- sci:sha256:f4f72761edb168f383c089e3604455bfa918b93e2e9adbb28b19c96905429043: well water levels did not step more often on earthquake dates than on placebo dates. A similar placebo logic is used here, with placebo winters.
- sci:sha256:960bb4a1dfbff9d17d6edc024941d90d49297037888d9b55a7c7fff7489689c8 and sci:sha256:7537d3ad5a643df67f7f8f114ce0cd0167fd9e78bcc95cf2a8f082ed6b1e62fa: streamflow rises and baseflow recession after strong shaking (PGV 10 cm/s or more) in US gauges.

New in this work: the first ambient-noise dv/v measurement in the campaign record, and a placebo-winter and control-station design for seasonal-frost regions. The result is a candidate 0.5% velocity deficit after the 2018 Anchorage earthquake, with an explicit statement of why four winters cannot confirm it.

## 10. Data licences and attribution

The bundled code, text, figures and derived tables are under the SCI baseline licence (`LICENSE`). External source data are not bundled except as derived aggregates. See `files/provenance/EXTERNAL_DATA_NOTICE.md`.
