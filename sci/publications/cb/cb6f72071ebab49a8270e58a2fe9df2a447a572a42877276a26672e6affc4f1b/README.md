# Canadian river ice-flag seasons shortened less than air-temperature sensitivity predicts

**Job:** sci-1107-dell-earth-and-ocean-sciences-bbabe49ae83f · **Topic:** earth-and-ocean-sciences · **Campaign:** 11_07_2026 · **Machine:** dell · **Model:** Claude Opus 5.5 (claude-opus-5-5), account claude-andrii · **Date:** 2026-11-09.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Water Survey of Canada hydrometric stations mark each day of daily discharge that ice affects with the symbol "B" (ice conditions) in the national HYDAT archive. The first and last B day of a winter are standard proxies for river freeze-up and break-up (de Rham et al. 2020). We asked one question:

> Does the year-to-year sensitivity of these dates to local air temperature, fitted in 1966-1995, predict how much the dates moved in 1996-2025, when the air was warmer?

If river ice follows air temperature only, the observed mean shift must agree with the predicted shift. If the observed shift is smaller or has the opposite sign, a factor other than the local air temperature in the season windows (river hydraulics, snow, data practice, or temperature outside the windows) also changed.

Main results (568 stations, 30 + 30 winters, GHCN-CAMS temperature, 95% intervals from a bootstrap over HYDAT sub-drainage areas):

| Quantity (1996-2025 minus 1966-1995) | Observed | Temperature-predicted | Observed minus predicted |
|---|---|---|---|
| First B day (freeze-up proxy) | +0.1 d [-0.8, +0.9] | +2.5 d [+2.2, +2.8] | **-2.4 d [-3.1, -1.7]** |
| Last B day (break-up proxy) | -0.5 d [-1.9, +1.0] | -1.3 d [-1.9, -0.6] | +0.8 d [-0.2, +1.9] |
| B season length | -0.6 d [-2.5, +1.6] | -3.3 d [-3.7, -2.9] | **+2.8 d [+1.0, +4.7]** |

1. The local cold-season air warmed by 0.8-1.0 °C. The fitted sensitivities (+3.0 d/°C for freeze-up, -3.2 d/°C for break-up, -3.4 d/°C for season length) predict a 3.3-day shorter ice-flag season. The observed mean season became only 0.6 days shorter (17% of the prediction). The deficit is in the first B day: it did not become later.
2. The deficit is regional (Figure 3, Figure 6). In Ontario (191 stations), the Maritimes (49) and the Prairie provinces SK and MB (50), the mean season shortened as predicted (observed minus predicted -0.7, -1.4 and +0.5 d; intervals include 0). The Prairie mean hides a split: Saskatchewan stations (Regina office) +4.2 d [0.4, 9.6], Manitoba stations (Winnipeg office) -1.7 d [-7.4, +3.2]. In British Columbia and Alberta (205 stations), the flagged season became **longer** by 4.4 d [2.3, 6.4] against a predicted 2.2 d shortening (difference +6.6 d [4.6, 8.5]). The North (YT, NT, NU; 40 stations; +4.1 d [2.8, 5.6]) and Newfoundland and Labrador (24; +9.6 d [1.9, 15.0]) also have positive differences.
3. Part of the national deficit comes from more sporadic, short B flags at the edges of the season (Figure 5). The mean number of separate B runs per winter increased from about 1.8-2.3 in the late 1960s to about 2.3-3.6 after 2000. When we use the first and last run of 14 or more consecutive B days ("continuous ice") on the same 449 stations, the season-length difference falls from +2.2 d [0.4, 4.1] to +0.9 d [-1.2, +3.1], and the freeze-up difference falls from -1.9 d to -0.9 d [-2.1, +0.1].
4. The regional contrast stays with the continuous-ice dates: West +2.8 d [1.1, 5.0], North +4.9 d [3.4, 6.8], Newfoundland and Labrador +8.1 d [5.0, 15.4], while Ontario (-3.0 d [-6.7, +4.4]) and the Maritimes (-2.1 d [-4.8, +0.9]) shortened at least as much as predicted.
5. The deficit is largest in the most recent period. For a 1981-2002 training period and a 2003-2025 test period, the season length did not change (flag dates +1.5 d [-0.6, +3.7]; continuous-ice dates 0.0 d [-1.6, +1.6]) against a predicted -2.7 to -2.8 d. The differences are +4.2 d [2.1, 6.1] and +2.8 d [1.2, 4.4]. Break-up moved 1.3 d later although the spring windows did not warm.
6. Pre-freeze-up discharge does not explain the freeze-up deficit. Log discharge in the open-water month before the freeze-up window has a small coefficient (+0.7 d per log unit [0.04, 1.5]) and its mean did not change (+0.007 log units), so the freeze-up difference stays at -2.4 d [-3.2, -1.5].
7. The temperature model has real year-to-year skill: in the test period it reduces the mean squared error of individual station-winter dates by 10-19% relative to the training mean. Extrapolation of the training-period linear trend is much worse (error 1.7-2.0 times the training mean error), because the 1966-1995 trends did not continue.

The result is robust to the temperature product (Berkeley Earth instead of GHCN-CAMS: season difference +3.0 d [1.2, 5.0]) and to the split year (1971-1997 vs 1998-2025: +1.9 d [0.4, 3.7]). In the earliest comparison (1966-1980 vs 1981-1995, 190 stations) the flag-date season difference was +2.3 d [-0.1, +4.4] and the continuous-ice difference was -1.1 d [-3.3, +1.5].

**Interpretation, with limits.** Air temperature in the season windows explains the year-to-year timing of river-ice flags well and explains the long-term change in eastern and central Canada. It does not explain the long-term change in western, northern and Newfoundland rivers, where the ice-flag season stopped shortening or became longer. Two classes of explanation remain and this study cannot separate them: (a) a change in hydrometric practice (how and when hydrographers apply the B flag; offices, instruments and estimation methods changed during the record), and (b) physical changes that make river ice in these regions less sensitive to air temperature (for example snow cover, winter flow regime, frazil-ice formation in cold snaps, or temperature extremes that a two-month mean does not show). Grouped by Water Survey of Canada regional office, the flag-date season difference is positive at all four western offices (Vancouver +5.4 d [3.8, 6.7], Calgary +8.8 d [4.2, 12.2], Regina +4.2 d [0.4, 9.6], Yellowknife +3.4 d [1.8, 5.5]), near zero at Burlington (-0.3 d [-2.3, +3.8]) and Winnipeg (-1.7 d [-7.4, +3.2]), and negative at Quebec City (-10.1 d, 11 stations). Office boundaries follow geography, so this grouping cannot separate practice from climate. In the Dartmouth office, Newfoundland and Labrador (+9.6 d) differs from New Brunswick and Nova Scotia (-1.4 d), so the office alone does not explain the pattern. Users of HYDAT B dates as a climate indicator in western and northern Canada should not assume that the dates follow air temperature over decades.

## Prior work

- de Rham et al. (2020, ESSD) built the Canadian River Ice Database from the same national archive and documented that the first B date can precede a full ice cover by weeks (backwater from frazil or anchor ice), that ice-affected discharge has no single standard estimation method, and that data entry error for B dates is about 7.5%.
- Zhang et al. (2001, WRR) used Reference Hydrometric Basin Network data and reported evidence of earlier freeze-up, mainly in eastern Canada, which is opposite to the expected effect of warming. Our result is the same in sign for the first B date (it moved earlier relative to temperature) but we find the strongest deficit in the west and north.
- Dibike et al. (2025, Water) analysed ice-influenced annual maximum water levels at selected stations for 1966-1990 and 1991-2015; freeze-over water levels occurred later at most stations in 1991-2015, and break-up timing trends were mixed.
- A previous campaign publication (sci:sha256:d945072e...) found that northern-hemisphere lake ice-on dates in 1991-2020 were 3.8 days **later** than air-temperature models predicted. The river first-B dates here moved **earlier** than predicted. Lakes and rivers therefore depart from the air-temperature expectation in opposite directions at freeze-up.

## Data

| Source | Version and bytes used | Licence | Use |
|---|---|---|---|
| ECCC National Water Data Archive HYDAT, SQLite | Release 2026-10-19, `Hydat_sqlite3_20261019.zip` sha256 `644d0b26...602ed4`, unzipped `Hydat.sqlite3` sha256 `a2c84de2...7ec315a`. Shared campaign copy: `/mnt/dell-data/shared_datasets/eccc-hydat-sqlite3-20261019/` | Open Government Licence - Canada 2.0 | Daily discharge values and the B (ice conditions) symbol; station metadata; regulation flag; RHBN flag; monthly mean discharge |
| NOAA PSL GHCN-CAMS monthly air temperature 0.5° | `air.mon.mean.nc` 1948-01 to 2026-10, sha256 `8dbe8e8c...0802b`. Shared copy: `/mnt/dell-data/shared_datasets/psl-ghcncams-air-mon-mean-20261105/` | NOAA public data | Main temperature input |
| Berkeley Earth gridded TAVG 1° (Complete_TAVG_LatLong1.nc) | to 2024-12, sha256 `4b78118b...40664`. Shared copy: `/mnt/dell-data/shared_datasets/berkeley-earth-complete-tavg-latlong1-20261109/` | CC BY-NC 4.0 | Robustness check only; only national aggregate results are in this package |
| Natural Earth 10 m land v5 | `ne_10m_land.zip` sha256 `e547d749...a922dc` | Public domain | Map background |

No raw third-party data are in this package. `files/code/00_get_data.sh` downloads the inputs into a separate scratch folder and checks the hashes. See `files/NOTICE.md` for attribution and licence notes.

## Methods

**Ice-flag dates.** A winter W runs from 1 September of year W-1 to 31 July of year W. We kept a station-winter only if every day in this window has a published daily discharge (this removes seasonal stations). For each such winter: first B day (freeze-up proxy), last B day (break-up proxy), and season length (last minus first plus 1). We removed winters with a B flag on 1 September or 31 July. Robustness definition: start of the first run and end of the last run of 14 or more consecutive B days.

**Stations.** Stations need at least 15 usable ice winters in the training period and 15 in the test period, and B flags in at least 90% of complete training winters (persistent ice). This gives 568 stations for the main analysis (165 with a regulation flag, 158 in the Reference Hydrometric Basin Network) and 449 stations for the 14-day-run definition.

**Temperature windows.** For each station and date variable, the window is the calendar month that contains the training-period median date and the month before it. For season length, the window is all months from the median freeze-up month to the median break-up month. Temperature comes from the nearest grid cell with data.

**Model and test.** Within-station regression of date on window temperature in the training period gives a pooled slope b (days per °C; bootstrap interval over sub-drainage areas). The predicted shift for a station is b × (test mean temperature - training mean temperature). We report the station-mean observed shift, predicted shift and their difference, with 95% intervals from 2,000 bootstrap draws of the 3-character HYDAT sub-drainage areas (for example 05A) to allow for spatial correlation. We also report station-specific and empirical-Bayes-shrunk slopes (`k_eb` is the slope of observed on predicted shifts across stations), mean-squared-error skill of station-winter predictions relative to the training mean, and a linear-trend extrapolation as a comparison forecast. The flow test adds the log monthly mean discharge of the open-water month before the freeze-up window (or the September-October mean) to the regression.

## Limitations

- The B flag records an ice effect on the discharge record, not a direct observation of ice cover. Its use changes with hydrographer practice, instruments and estimation methods, and the archive does not document these changes station by station. We cannot separate a practice change from a physical change.
- Window temperature is a two-month mean of a 0.5° grid cell. It does not resolve cold-snap timing, snow cover, or local water temperature. Errors in the temperature data make the fitted slope smaller, which makes the predicted shift smaller; so this error cannot produce the observed deficit, but other omitted variables that co-vary with temperature year to year can bias the slope in either direction.
- Station selection requires long, complete winter records. It favours long-running stations and southern Canada (305 of 568 stations are south of 50° N). Quebec has only 3 stations in the sample, because few Quebec records pass the completeness and persistent-ice criteria (de Rham et al. 2020 note that Quebec provincial data use a different ice symbol).
- The bootstrap allows correlation within sub-drainage areas but not between neighbouring areas; regional intervals with few sub-drainage areas (Maritimes 6, Newfoundland and Labrador 5) are approximate.
- The 2025 winter has fewer complete station records (371 in the main set) possibly because some 2025 records are not yet final in the October 2026 release.
- We did not test snow depth, winter precipitation, temperature extremes, or changes in station equipment.

## Figures

- `files/figures/fig1_national_series.png`: national mean station anomalies of the three date variables and their temperature-predicted values, 1966-2025.
- `files/figures/fig2_shift_obs_vs_pred.png`: observed and predicted mean shifts by station group.
- `files/figures/fig3_map_duration_residual.png`: station map of observed minus predicted change in season length.
- `files/figures/fig4_regional_residuals.png`: regional residuals by 5-winter block.
- `files/figures/fig5_intermittency_and_runs.png`: B-run counts per winter, sporadic edge flags, and flag- vs run-based results on the same stations.
- `files/figures/fig6_regional_season_length.png`: regional observed and predicted change in season length for both definitions.

## Files

- `files/code/`: all code. `00_get_data.sh` (download and hash check), `run_all.sh` (full pipeline), `01_extract_ice.py`, `01b_extract_runs.py`, `02_station_temps.py`, `03_analysis.py`, `04_flow_covariate.py`, `05_figures.py`, `06_fig_runs.py`, `07_collect.py`, `08_regional_ci.py`, `09_fig_regions.py`.
- `files/results/results_summary.csv`: one row per analysis, variable and station group (observed, predicted and difference with intervals; slopes; skill).
- `files/results/<analysis>/summary.json`, `national_year_signal.csv` (national mean anomalies by winter), `station_shift_<variable>.csv` (per-station slope, temperature change, observed and predicted shift; station number only). The Berkeley Earth run has only `summary.json`.
- `files/results/regional_shift_main.csv`, `regional_shift_runs14.csv`, `office_shift_main.csv`, `office_shift_runs14.csv` (by regional office), `regional_residual_by_period.csv`, `flow_covariate.json`, `intermittency_by_winter.csv`, `flag_vs_run_same_stations.csv`.

## Reproduce

```bash
bash files/code/00_get_data.sh /tmp/riverice_inputs          # about 1.2 GB
bash files/code/run_all.sh /tmp/riverice_inputs /tmp/riverice_work /tmp/riverice_files
```

Python 3.12 with numpy 2.5.4, pandas 3.1.1, xarray 2026.9.0 (netCDF4 backend), matplotlib 3.11.2, geopandas 1.2.0. The full run takes about 20 minutes on one core. Bootstrap seeds are fixed in the scripts.
