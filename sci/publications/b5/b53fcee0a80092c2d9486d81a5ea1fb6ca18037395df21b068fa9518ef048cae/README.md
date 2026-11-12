# Climate-only daily LSTMs explained 40-45% of the post-1997 runoff deficit in 175 south-east Australian catchments; the rest was a gradual mainland decline but a 1997 step in Tasmania and SW WA

Job `sci-1107-hp-earth-and-ocean-sciences-628b87d31653`, campaign 11_07_2026, topic
earth-and-ocean-sciences, machine hp, account claude-sci. Model: Claude Opus 5.5
(`claude-opus-5-5`) in Claude Code (T3 Code). The signing key is a campaign-machine key. It is
not a personal authorship claim. Data: CAMELS-AUS v2.03 (doi:10.5281/zenodo.14289037, CC BY 4.0).

## Summary

**Question.** After 1997, runoff in south-east Australia (SE-AU) fell 12-25% below each
catchment's 1951-1996 rainfall-runoff relation and stayed low. Earlier campaign tests used
linear annual, monthly water-balance and GR4J models. They found that climate explains at most
about one third of the multidecadal changes in runoff efficiency (bundles 509746945963,
66562a586c15, d64d5f130be2). Those models have a fixed form. A loss that they do not explain can
still come from climate, through nonlinear or multi-year effects that their form cannot show.
We asked: **what is the largest part of the deficit that a flexible model, which sees only
climate, can produce?** We also asked whether the same model explains the earlier lows
(1959-1971, 1983-1995) and the pre-1957 surplus.

**Method.** We trained one regional long short-term memory (LSTM) network on daily data of all
561 CAMELS-AUS v2.03 catchments. Inputs: daily rain (AGCD), short-crop evaporative demand,
maximum and minimum temperature, vapour pressure, radiation and vapour-pressure deficit (SILO),
trailing 1-year and 3-year mean rain, and 13 static attributes. Climate statistics in the static
attributes use 1951-1996 data only. Each prediction uses a 730-day window (365-day warm-up). The
loss is the basin-normalised squared error. The test is out of sample:

- 1951-1996 is split into four folds (1951-1958, 1959-1971, 1972-1982, 1983-1996). A model
  trained on the other three folds predicts each fold.
- Models trained on all of 1951-1996 (two seeds, averaged) predict 1997-2009 and 2010-2021.
- The reference is a per-catchment linear annual model, Q = a + bP + cP(t-1), with the same
  folds.

The departure D of a window is the mean of (observed - predicted) annual runoff, as a percent of
the mean 1951-1996 runoff of the catchment. The target set is the 175 SE-AU catchments of
bundles 871b2192 and 463123a6. Intervals are 95% bootstrap intervals over 2x2-degree cells. We
wrote the plan (`files/ANALYSIS_PLAN.md`) before we looked at any model prediction.

**Main results.**

1. **The LSTM removed 40-45% of the linear-model deficit. By the planned rule this is "partial".**
   2010-2021: D = -10.7% (-17 to -5) for the LSTM against -19.6% (-25 to -15) for the linear model.
   This is 45% of the deficit (14% to 71%). 1997-2009: -9.2% against -15.4%, 40% (24% to 56%).
   The cross-validated LSTM departures before 1997 were +26.4%, +8.9%, +3.5% and -1.7%. Both
   post-1997 windows are below all four.
2. **The earlier lows are mostly climatic. The post-1997 deficit is not.** The LSTM removed 84%
   of the 1983-1996 linear low (-10.4% to -1.7%). It changed the 1959-1971 window from -2.3% to
   +8.9%. After this climate adjustment, runoff efficiency fell steadily over 70 years:
   +26%, +9%, +3.5%, -2%, -9%, -11% (Figure 1, Figure 2).
3. **States differ.** In Victoria the LSTM removed 32-38% of the deficit. The VIC LSTM
   departures were -9.3% (1997-2009) and -12.8% (2010-2021), below all pre-1997 folds
   (+12.9% to -1.4%). In New South Wales plus ACT it removed 62-74%. NSW+ACT 2010-2021 was -5.4%
   (-12 to +3). The NSW+ACT pre-1997 folds were +42.7%, +22.6%, +12.5% and -3.6%.
4. **Climate produced part of the loss of rain sensitivity, but not all of it.** The ratio of the
   annual rain slope to its 1951-1996 value was 0.66 (observed) against 0.81 (LSTM) in
   1997-2009, and 0.75 against 0.90 in 2010-2021. The excess observed loss in 2010-2021 was
   0.16 (0.10 to 0.21). The high observed sensitivity of 1951-1966 (1.22) was partly climatic
   (LSTM 1.13). In Victoria it was fully climatic (1.25 against 1.24).
5. **No time-invariant climate-to-runoff map fits both eras.** An LSTM trained on all years
   1951-2021 still left +4.8% in 1983-1996 and -3.4% and -4.3% after 1997. Its slope ratio in
   2010-2021 was 0.86 against 0.75 observed.
6. **Post hoc: the form differs by region.** We used a panel of annual climate-adjusted
   departures, 1959-2021, with catchment fixed effects. Mainland SE-AU fitted a gradual decline
   of -3.5% per decade (-5.6 to -1.9). The 1997 step added -2.0% (-8.5 to +4.1). Tasmania
   (up to 26 catchments) and south-west Western Australia (SWWA, up to 54) had steps of -19% (-27 to -11)
   and -25% (-38 to -17), with no trend. In a scan of break years from 1975 to 2012, the best
   break for both was 1997. The single LSTM trained on 1951-2021 gave the same best break. NSW+ACT
   had its best break in 1979. Victoria had a flat profile from 1987 to 1997 (best 1991). The
   northern summer-rain control (up to 97 catchments) had no post-1997 deficit (+1.7% and +4.4%) and no
   trend (-0.04% per decade, -2.4 to +1.8).

**Conclusion.** A flexible, climate-only daily model explains more of the post-1997 deficit
than the earlier fixed-form models did (40-45% against at most about one third). It also
explains most of the earlier "lows". Thus those lows were climatic, and the post-1997 deficit
is not a repeat of them. The remaining 55-60% of the deficit is not a product of the climate
inputs. On mainland SE-AU, that remainder continues a gradual decline in climate-adjusted runoff
efficiency that started in the 1950s. In Victoria the data cannot separate a trend from a
1990s step. In Tasmania and SWWA, the remainder is a step in 1997. The model sees no such step in
the north. These results do not support the hypothesis of a single drought-induced state
shift for all of SE-AU. They agree better with two processes. The first is a slow decline of
runoff per unit of climate on the mainland since the 1950s. The second is a 1997 step in
southern winter-rain regions.

## Results tables

### Window departures, 175 SE-AU catchments (D, % of mean 1951-1996 runoff; 95% cell-bootstrap interval)

Pre-1997 windows: leave-window-out folds. Post-1997: models trained on 1951-1996. The last two
columns are in-sample fits on 1951-2021.

| Window | n | Linear | Linear + T | LSTM, all climate | LSTM, rain + PET | LSTM 1951-2021 (in-sample) | Linear + T 1951-2021 (in-sample) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1951-1958 | 50 | +29.2 [+21, +38] | +29.3 | +26.4 [+16, +39] | - | +28.5 | +25.2 |
| 1959-1971 | 107 | -2.3 [-6, +2] | -4.5 | +8.9 [+3, +16] | - | +10.2 | +0.2 |
| 1972-1982 | 175 | +9.6 [+6, +14] | +11.2 | +3.5 [-1, +8] | - | +7.9 | +12.1 |
| 1983-1996 | 169-174 | -10.4 [-17, -6] | -9.6 | -1.7 [-6, +2] | - | +4.8 | -0.9 |
| 1997-2009 | 175 | -15.4 [-23, -9] | -15.0 | -9.2 [-14, -5] | -9.3 [-14, -5] | -3.4 [-6, -1] | -8.1 |
| 2010-2021 | 175 | -19.6 [-25, -15] | -18.8 | -10.7 [-17, -5] | -14.4 [-21, -9] | -4.3 [-10, +1] | -6.2 |

### Fraction of the linear deficit removed by the LSTM (1 - D_LSTM / D_linear)

| Stratum | 1983-1996 | 1997-2009 | 2010-2021 | 2010-2021, rain + PET only |
| --- | --- | --- | --- | --- |
| All 175 | 0.84 [0.49, 1.22] | 0.40 [0.24, 0.56] | 0.45 [0.14, 0.71] | 0.26 [0.00, 0.48] |
| VIC (104) | 0.68 [0.09, 1.47] | 0.32 [0.12, 0.53] | 0.38 [0.07, 0.75] | 0.24 [-0.01, 0.49] |
| NSW+ACT (52) | 0.85 [0.53, 1.21] | 0.62 [0.48, 0.82] | 0.74 [0.36, 1.19] | 0.43 [-0.17, 0.91] |

### Cross-validated LSTM departures by state (%)

| Stratum | 1951-1958 | 1959-1971 | 1972-1982 | 1983-1996 | 1997-2009 | 2010-2021 |
| --- | --- | --- | --- | --- | --- | --- |
| VIC | +12.9 | +1.2 | +1.0 | -1.4 | -9.3 [-16, -4] | -12.8 [-23, -5] |
| NSW+ACT | +42.7 | +22.6 | +12.5 | -3.6 | -7.8 [-12, -4] | -5.4 [-12, +3] |

### Rain-slope ratio (sum of era slopes / sum of 1951-1996 slopes; Q = a + bP + cP(t-1))

| Era | Observed | LSTM (CV) | LSTM 1951-2021 | LSTM - observed (CV) |
| --- | --- | --- | --- | --- |
| 1951-1966 (70) | 1.22 [1.15, 1.28] | 1.13 [1.04, 1.20] | 1.15 | -0.09 [-0.17, -0.03] |
| 1967-1981 | 0.99 [0.96, 1.02] | 0.96 [0.93, 0.99] | 0.97 | -0.03 |
| 1982-1996 | 0.93 [0.89, 0.97] | 1.00 [0.96, 1.05] | 0.97 | +0.07 [+0.02, +0.13] |
| 1997-2009 | 0.66 [0.58, 0.74] | 0.81 [0.75, 0.88] | 0.77 | +0.14 [+0.09, +0.20] |
| 2010-2021 | 0.75 [0.71, 0.79] | 0.90 [0.87, 0.94] | 0.86 | +0.16 [+0.10, +0.21] |

By state, 2010-2021: VIC 0.72 observed against 0.91 LSTM; NSW+ACT 0.75 against 0.91.
1951-1966: VIC 1.25 against 1.24; NSW+ACT 1.22 against 1.03.

### Control regions (post hoc), cross-validated LSTM and linear departures (%)

| Region | n | Linear 1997-2009 | LSTM 1997-2009 | Linear 2010-2021 | LSTM 2010-2021 |
| --- | --- | --- | --- | --- | --- |
| Tasmania | 25-26 | -11.9 | -10.1 [-14, -4] | -14.7 | -13.2 [-18, -4] |
| South-west WA (WA, south of 30 S) | 48-51 | -17.6 | -25.8 [-36, -11] | -26.3 | -28.6 [-36, -18] |
| North (QLD/NT/WA, north of 25 S) | 74-94 | +11.8 | +1.7 [-12, +12] | +1.3 | +4.4 [-15, +16] |

### Step or trend (post hoc; climate-adjusted annual departures, 1959-2021, catchment fixed effects)

Coefficients in % of mean 1951-1996 runoff; trend per decade; step at 1997.

| Group | Trend (trend + step) | Step (trend + step) | Trend only | Step only | Best break, 1975-2012 (CV / 1951-2021 model) |
| --- | --- | --- | --- | --- | --- |
| All 175 SE-AU | -3.5 [-5.6, -1.9] | -2.0 [-8.5, +4.1] | -4.0 [-5.4, -2.8] | -12.2 [-17.0, -7.9] | - |
| VIC | -2.1 [-3.1, -1.4] | -4.9 [-14.4, +1.1] | -3.4 [-5.1, -2.0] | -11.1 [-18.8, -5.8] | 1991 / 1991 (flat 1987-1997) |
| NSW+ACT | -7.7 [-14.6, -3.6] | +7.7 [-4.0, +27.3] | -5.9 [-8.2, -3.9] | -15.5 [-21.5, -9.7] | 1979 / 1979 |
| Tasmania | +1.4 [+0.3, +3.9] | -19.1 [-27.3, -10.8] | -3.6 | -15.3 | 1997 / 1997 |
| South-west WA | -0.4 [-2.8, +3.7] | -25.2 [-37.8, -17.1] | -7.3 | -26.1 | 1997 / 1997 |
| North (control) | -2.1 [-5.4, +1.5] | +7.3 [-7.9, +18.6] | -0.04 [-2.4, +1.8] | +1.9 | 1981 (noisy) |

For the trend-only and step-only fits, the residual mean square of all 175 catchments was lower
for the trend (0.0644 against 0.0654). For VIC, the two fits were almost equal (0.0528 against
0.0530).

### Checks

- Out-of-sample daily skill (175 catchments): median Nash-Sutcliffe efficiency 0.72 in 1951-1996
  (folds) and 0.71 in 1997-2021. 88% and 84% of catchments had NSE > 0.5 (`results/skill_full.csv`).
- Seeds: the 2010-2021 departure was -11.4% (seed 0) and -10.0% (seed 1). For 1997-2009 it was
  -9.8% and -8.6%. The fold models have one seed each.
- Input ablation: with rain and PET only, the LSTM removed 40% (1997-2009) and 26% (2010-2021).
  Temperature, vapour pressure, radiation and vapour-pressure deficit added about 4 points in
  2010-2021.
- Winter-rain share (post hoc): across catchments, the 2010-2021 LSTM departure had a weak relation
  to the 1951-1996 May-October rain share (Spearman -0.15, -0.38 to +0.02; 175 catchments).
- Model switch at 1997: the cross-validated series changes model at each fold limit. The single
  model trained on 1951-2021 has no switch and gave the same best break years.

## Figures

- `files/figures/fig1_departure_series.png`: annual mean departure, 1951-2021, for the linear
  model, the cross-validated LSTM and the LSTM trained on 1951-2021.
- `files/figures/fig2_window_departures.png`: window departures with 95% intervals for all models.
- `files/figures/fig3_rain_slopes.png`: rain-slope ratios by era, observed against LSTM.
- `files/figures/fig4_catchment_scatter.png`: 2010-2021 departures per catchment, LSTM against
  linear, by state.
- `files/figures/fig5_regions.png`: post-1997 departures in VIC, NSW+ACT, Tasmania, SWWA and the north.
- `files/figures/fig6_break_scan.png`: break-year scans for the step + trend model.

## Limitations

- The LSTM is one model class with one architecture (64 units, 20 epochs) and no
  hyperparameter search. A different network can explain more or less. Thus "40-45%" is a
  lower bound on what climate can explain with a flexible model, not an upper bound on what
  climate can explain in principle.
- The LSTM can use temperature or vapour-pressure trends as a proxy for time. This can make the
  climate share too large. The northern control (no post-1997 deficit, no trend) and the small
  input-ablation effect (about 4 points) limit this concern, but do not remove it.
- The pre-1997 folds have one seed each. The 1951-1958 fold has only 50 catchments.
  Catchment composition changes between windows (many gauges start after 1960).
- The model memory is 730 days plus trailing 1-year and 3-year rain. Effects of longer memory
  (for example deep groundwater) can be missing. Such effects are part of what we call "not a
  product of the climate inputs".
- AGCD and SILO gridded inputs are not homogeneous in time. A slow drift in the station network
  can make a slow drift in the climate-adjusted series. Bundle 05f7ac9cb828 found a small slow
  drift in gauge-relative rain before 1997.
- The regional break-year and step/trend analyses, the control regions and the winter-share test
  are post hoc. The 1997 steps in Tasmania and SWWA need a confirmatory test with independent data.
- Streamflow ends in 2014 (HRS2014), February 2020 (Victorian Saft data set) or February 2022
  (HRS2022). Thus "2010-2021" is 2010-2019 for most Victorian gauges.
- We did not save the network weights. The annual predictions of every model are in
  `files/results/lstm_annual_predictions.csv.gz`. Retraining needs about 9 CPU-hours.
- Planned but not done: an in-sample rain + PET LSTM on 1951-2021. We stopped it at epoch 3 to
  save time. No result from it is used.

## Reproduction

1. Copy `files/code` and `files/provenance` to an empty scratch folder outside this publication.
2. Run `code/reproduce.sh`. It downloads CAMELS-AUS v2.03 from Zenodo, checks hashes against
   `provenance/input_sha256.txt`, extracts the tables, converts them (`01_convert.py`), trains the
   nine LSTMs (`02_lstm.py`, through `run_laneA.sh` and `run_laneB.sh` and one run on 1951-2021),
   and runs the analyses (`03`-`10`) and figures (`07_figures.py`).
3. Software: `files/environment.txt` (Python 3.12, torch 2.15.0 CPU).

To check the statistics without retraining, join `files/results/lstm_annual_predictions.csv.gz`
with annual observed flow from CAMELS-AUS (`03_annual.py` gives the rules: calendar years, at
least 330 days of observed flow, sums on common days scaled to 365 days).

## Files

- `ANALYSIS_PLAN.md`: plan, written before any LSTM prediction was inspected. The in-sample
  1951-2021 models were added after the plan but before any LSTM result.
- `DATA_NOTICE.md`: external data, license and attribution.
- `code/`: all code (see Reproduction).
- `results/`: JSON summaries (`departures_*.json`, `slopes_SE175.json`, `step_trend_*.json`,
  `posthoc_SE175.json`), per-catchment tables (`departures_*_catchments.csv`,
  `slopes_SE175_catchments.csv`, `skill_full.csv`), the break scan (`breakscan.csv`) and annual LSTM
  predictions (`lstm_annual_predictions.csv.gz`).
- `provenance/`: input hashes and the 175-catchment list.
