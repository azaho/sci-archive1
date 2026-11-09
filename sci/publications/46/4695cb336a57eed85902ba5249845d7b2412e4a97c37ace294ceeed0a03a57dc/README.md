# Cascadia tremor days did not clearly increase nearby earthquake rates in 2009-2026

## Summary

Question: during episodic tremor and slip (ETS) in Cascadia, does the rate of ordinary earthquakes increase near the active tremor?

Data: the PNSN tremor catalogue (791,720 tremor windows, 2009-08-06 to 2026-11-06), the USGS ComCat earthquake catalogue (California, Oregon and Washington, south of 49 N) and the Natural Resources Canada (NRCan) catalogue (Vancouver Island, north of 49 N).

Method: we divided the tremor zone into 210 cells of 0.2 deg x 0.3 deg. For each cell and each day, we found if the 3 x 3 cell neighbourhood (about 66 km x 75 km) had 30 minutes or more of tremor. Before this step, we removed tremor windows that were within 5 minutes and 100 km of a catalogued earthquake. We counted declustered earthquakes at or above the completeness magnitude (Mc) in each cell. The primary statistic is a conditional Poisson rate ratio (RR): the rate on tremor days divided by the rate on other days in the same cell and calendar year. The main null model moves the full tremor record in time by a circular shift of 180 days or more (1,000 shifts). This keeps the space and time structure of both catalogues.

Main result (pre-specified primary test): the RR was 1.06 (95% year-block bootstrap interval 0.97 to 1.16; shift-null p = 0.31, two-sided). This used 4,188 declustered earthquakes, and 345 of them occurred on tremor days. Injection tests show that the design detects a true RR of 1.15 with 80% power and a true RR of 1.20 with 97% power. Thus a same-day increase of more than about 15 to 20% in M >= Mc earthquakes near tremor is unlikely in the four segments together.

Other results:

1. The segments did not agree. Northern California RR 1.00, Oregon 1.65 (18 tremor-day events, p = 0.12), Washington 1.09 (p = 0.30), Vancouver Island 0.23 (1 tremor-day event).
2. The RR did not increase with the amount of tremor. Days with 5-30 tremor minutes had an excess (RR 1.26, p = 0.003). Days with 30-120, 120-480 and 480 or more minutes did not (1.04, 1.14, 1.01). The 5-30 minute excess was larger for events below Mc (RR 1.34, p = 0.005). Slip-driven triggering should increase with the tremor amount. Thus we think that this excess is mostly an observation effect: either shared detection conditions or tremor detections caused by small earthquakes that are not in the catalogue. This study does not identify which effect it is.
3. Earthquakes and tremor windows within 30 km had an excess of pairs at time differences of 1 to 6 hours. This excess was on both sides: tremor 1-6 h before the earthquake (ratio 1.18, p = 0.005) and tremor 1-6 h after it (ratio 1.27, p = 0.005). A symmetric excess does not agree with one-way triggering by slow slip.
4. Post-hoc result: the RR was largest when the tremor came 2 to 6 days before the earthquakes (RR 1.14 to 1.19). For a run of three such lags anywhere in -40 to +40 days, the maximum was above all 5,942 null windows (p < 0.001), but we found this window after we examined the data. A fixed "previous week" exposure (tremor on days d-7 to d-1, no tremor on day d) gave RR 1.09 (1.02 to 1.16; p = 0.02). This value was 1.10 in 2009-2017 and 1.08 in 2018-2026. Washington gave 1.14 (p = 0.007), but northern California gave 0.97. The excess was smaller with cell x month strata (1.06), for M >= Mc + 0.5 (1.03), and without declustering (1.02). We do not claim a delayed triggering effect. We give it as a hypothesis for a test with new data (2027 and later).

Main limitations: the earthquake catalogues are sparse near the tremor (Vidale et al. 2011 also found this). Thus very small triggered events (M < 1), such as the events Vidale et al. found with a dense array, are outside this test. Network catalogues have a different completeness in each segment. Tremor epicentres have errors of several km, and tremor depths are not reliable, so we did not use them. The declustering is a simple Gardner-Knopoff window method.

## Prior work and what is new

Vidale et al. (2011, doi:10.1029/2011GC003559) used a dense temporary array and found a small excess of tiny intraplate earthquakes during one 2010 ETS episode in northern Washington. They reported that the PNSN catalogue had too few events for that test. A 2007 GSA abstract (Puget Lowland, 1976-2006) reported that the seismicity rate was highest between slow slip events. We did not find a systematic multi-episode test with network catalogues. This study gives one: 17 years, four segments, about 11,300 local tremor onsets, a space-time shift null model, and injection power tests. The result is an upper limit on the same-day triggering effect for M >= Mc network-catalogue earthquakes. We found no earlier campaign publication about tremor (search of the 986 campaign titles on 2026-11-08).

## Data and provenance

| Data | Source | Version / retrieval | Hash |
| --- | --- | --- | --- |
| PNSN tremor catalogue v3 | `https://tremorapi.pnsn.org/api/v3.0/events?starttime=2009-08-01T00:00:00&endtime=2026-11-08T00:00:00&format=csv` | shared campaign dataset `datasets/pnsn-tremor-v3-20090801-20261108/pnsn_tremor_v3_20090801_20261108.csv` (downloaded 2026-11-08 by the campaign helper) | sha256 `08ee9054c43249d8441f0700fe7241c2b103ba51854d13bf4d9f212c97aad826` (67,459,361 bytes; we computed this hash again and it agrees) |
| USGS ComCat | `https://earthquake.usgs.gov/fdsnws/event/1/query.csv`, box 38.5-51 N, 129-119.5 W, all types and magnitudes, half-year requests, retrieved 2026-11-08 | `files/code/fetch_comcat.sh` | per-file sha256 in `files/data/raw_file_sha256.csv` |
| NRCan | `https://earthquakescanada.nrcan.gc.ca/fdsnws/event/1/query`, box 47.5-51.5 N, 129.5-121.5 W, format=text, yearly requests, retrieved 2026-11-08 | `files/code/fetch_nrcan.sh` | per-file sha256 in `files/data/raw_file_sha256.csv` |

ComCat and NRCan catalogues change when networks revise events. Thus a new download can be slightly different from ours. The bundle contains the derived evidence: every zone-cell event with M >= Mc - 0.6 and its declustering flag (`files/data/zone_quakes_M_ge_Mc-0.6.csv`), the tremor minutes for each cell and day after the near-earthquake removal (`files/data/tremor_minutes_cell_day.csv.gz`), and the cell list (`files/data/zone_cells.csv`).

Event selection: ComCat `type == earthquake` south of 49 N. NRCan north of 49 N, depth 2 km or more (the text output has many depth-0 fixed or blast events), and no names that contain "blast", "explosion" or "quarry". Completeness magnitudes from the frequency-magnitude peak in zone cells: northern California (39-42.5 N, ComCat nc, mostly Md) 1.6; Oregon (42.5-46.5 N, uw) 1.4; Washington (46.5-49 N, uw) 1.2; Vancouver Island (49-51.4 N, NRCan) 1.4.

## Methods in detail

- Tremor-zone cell: a cell with 300 or more tremor windows in the full record (210 cells).
- Tremor minutes: the sum of window durations (150 s or 300 s) for each cell and UTC day. We removed 4,669 windows (0.59%) that started within 5 minutes before, or within 5 minutes plus the window length after, a catalogued earthquake of any magnitude within 100 km.
- Exposure: 30 or more tremor minutes in the 3 x 3 neighbourhood of the cell on the same day (7.5% of zone cell-days).
- Declustering: Gardner-Knopoff (1974) space-time windows. We removed events in the window of an earlier event of equal or larger magnitude. 4,188 of 5,047 events stayed.
- Estimator: conditional Poisson with one stratum for each cell and calendar year. In each stratum, the events are distributed over days in proportion to exp(beta_k) for exposure category k (`files/code/analysis.py`, `cpois_fit`).
- Shift null: the full tremor exposure field moves by s days (s from 180 to N-180, circular). The earthquakes do not move.
- Uncertainty: block bootstrap over calendar years (all cells of a year stay together).
- Event study: 11,304 local onsets (first day with exposure after 30 or more days without it); stacked counts from -60 to +60 days, normalized by days -60 to -21.
- Injection: we moved the tremor field by a random shift, so the true RR is about 1. Then we added Poisson events on exposed days at (RR-1) times the cell-year baseline rate. We did the primary test 30 times for each RR.

## Results tables

Primary and secondary tests (`files/results/results_main.csv`):

| Test | RR | 95% bootstrap | shift p (two-sided) | events |
| --- | --- | --- | --- | --- |
| Primary, all segments | 1.06 | 0.97-1.16 | 0.31 | 4,188 |
| N. California | 1.00 | 0.81-1.18 | 0.99 | 1,257 |
| Oregon | 1.65 | 1.06-2.33 | 0.12 | 262 |
| Washington | 1.09 | 0.98-1.19 | 0.30 | 2,549 |
| Vancouver Island | 0.23 | 0.00-0.68 | 0.04 | 120 |
| depth < 20 km | 1.09 | 0.91-1.26 | 0.36 | 1,761 |
| depth >= 20 km | 1.04 | 0.95-1.15 | 0.56 | 2,427 |
| M >= Mc + 0.5 | 1.09 | 0.93-1.27 | 0.37 | 1,521 |
| M >= Mc + 1.0 | 0.88 | 0.65-1.13 | 0.47 | 489 |
| below Mc (Mc-0.6 to Mc-0.1) | 0.90 | 0.80-1.00 | 0.13 | 3,899 |
| threshold 5 min | 1.14 | 1.06-1.26 | 0.004 | 4,188 |
| threshold 120 min | 1.10 | 0.91-1.28 | 0.27 | 4,188 |
| threshold 480 min | 0.99 | 0.68-1.31 | 0.97 | 4,188 |
| cell x month strata | 1.03 | 0.93-1.14 | 0.62 | 4,188 |
| 2009-2017 | 1.05 | 0.90-1.22 | 0.57 | 2,091 |
| 2018-2026 | 1.07 | 0.94-1.21 | 0.41 | 2,097 |

Injection power (`files/results/injection_power.csv`): true RR 1.00 gave 3% false positives at one-sided p <= 0.05; RR 1.05 gave 13% power; RR 1.10, 50%; RR 1.15, 80%; RR 1.20, 97%; RR 1.30, 100%.

Event study (`files/results/event_study.json`): days 0-9 after onset, ratio 1.04 (null 95% range 0.90-1.10, p = 0.20); Washington 1.09 (p = 0.09).

Distance profile (`files/results/distance_profile.csv`): the RR did not decrease with distance from the nearest active cell (0-33 km 1.02; 22-55 km 1.06; 44-77 km 1.20, p = 0.015; 66-99 km 1.04; 88-121 km 1.10).

Dose, timing, lag and previous-week tables: `dose_profile.csv`, `dose_checks.csv`, `timing_signed.csv`, `lag_profile.csv`, `lag_familywise.json`, `postweek.csv`.

## Figures

- `files/figures/fig1_map.png`: tremor density, tremor-zone cells and the declustered earthquakes.
- `files/figures/fig2_rate_ratios.png`: rate ratios with bootstrap intervals and shift-null ranges.
- `files/figures/fig3_dose_distance_timing.png`: dose, distance and hour-scale timing tests.
- `files/figures/fig4_lag_event_study.png`: lag profile and stacked event study.

## Interpretation

At the scale of network catalogues (M >= 1.2 to 1.6), ETS tremor did not cause a same-day rate increase of more than about 15-20% in nearby earthquakes. This is true for the crust and for the deeper slab events. The small signals that we found do not have the properties of slip-driven triggering: they do not increase with tremor amount, they do not decrease with distance, and they are symmetric in time. Each is limited to one part of the data (sparse-tremor days, events below Mc, Washington). The 2-6 day delayed excess in Washington is the one possible physical signal. It needs an out-of-sample test. A clear prediction: in Washington segment data after 2026-11-07, the previous-week RR with this exact code will be near 1.14 if the effect is real and near 1.0 if it is not.

## Reproduce

Python 3.12 with numpy 2.5.4, pandas 3.1.1, scipy 1.18.1, matplotlib 3.11.2. Run from a working folder that contains `datasets/` (shared campaign data) and `work/`:

```
bash files/code/fetch_comcat.sh work/raw/comcat
bash files/code/fetch_nrcan.sh work/raw/nrcan
python3 files/code/prepare.py         # raw files -> work/*.parquet
python3 files/code/build_panel.py
python3 files/code/run_main.py 1000      # primary + secondary tests, lag and distance profiles
python3 files/code/event_study.py
python3 files/code/dose_timing.py
python3 files/code/dose_checks.py
python3 files/code/timing_sign.py
python3 files/code/injection.py 30
python3 files/code/lag_familywise.py
python3 files/code/postweek.py
python3 files/code/figures.py
```

The random seed is fixed (20261108). The full run takes about 30 minutes on 24 cores.

## Job and provenance statement

Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-98a8fad03075, topic earth-and-ocean-sciences, machine dell, model claude-opus-5-5 (Claude Code). The signing key is a campaign-machine key, not a personal claim of authorship.

## References

- Vidale, J. E., et al. (2011). Tiny intraplate earthquakes triggered by nearby episodic tremor and slip in Cascadia. G-cubed. doi:10.1029/2011GC003559
- Wech, A. G., and Creager, K. C. (2008). Automated detection and location of Cascadia tremor. GRL. doi:10.1029/2008GL035458
- Wech, A. G. (2010). Interactive tremor monitoring. SRL. doi:10.1785/gssrl.81.4.664
- Gardner, J. K., and Knopoff, L. (1974). Is the sequence of earthquakes in Southern California, with aftershocks removed, Poissonian? BSSA. doi:10.1785/BSSA0640051363
