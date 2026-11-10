# Hidden low-runoff states in US reference basins: a test of the Victorian non-recovery result

Job: sci-1107-dell-earth-and-ocean-sciences-5b7d01fabc41 (campaign 11_07_2026), topic
earth-and-ocean-sciences, machine dell, account claude-andrii, model Claude Opus 5.5
(claude-opus-5-5). The signing key is a campaign-machine key, not a personal authorship claim.

## Question

Peterson et al. (2021, Science 372:745) found that many catchments in Victoria, Australia,
changed to a persistent low-runoff state during the Millennium Drought. In this state, the same
annual rainfall gave less streamflow. A prior campaign publication (SCI bundle 36d145c1) found
that most of these catchments stayed low through 2025. Both studies use a two-state hidden Markov
model (the "hydroState" model form) and select it by AIC.

We asked three questions for the contiguous United States:

1. Do the 671 CAMELS-US reference basins show the same hidden low-runoff states?
2. Are these states real changes, or does the method also find them in stationary data?
3. Did basins that were in the low state at the end of WY2016 (after the 2012-2016 drought in
   California and the West) stay low in water years (WY) 2017-2025?

## Data

- USGS NWIS daily mean discharge for the 671 CAMELS gauges, WY1951-WY2026, retrieved 2026-11-09.
- NOAA nClimGrid monthly precipitation and mean temperature, averaged over each CAMELS basin
  polygon with sub-cell coverage weights.
- CAMELS-US v1.2 basin boundaries (Zenodo 15529996).

A water year (October-September) is valid if at least 90% of its days have a flow value. The
sample has 554 basins with at least 40 valid years in WY1951-2016 and at least 7 valid years in
WY2017-2025. WY2026 flow is mostly provisional (40% of days), so we use WY2026 only as a
sensitivity check. See files/DATA_NOTICE.md for sources, versions, terms and hashes.

## Methods

We wrote the analysis plan (files/ANALYSIS_PLAN.md) before we computed model output. We added
four addenda during the work. Each addendum gives its time and the reason for it. Addenda 2 and
4 came after we saw interim results; we identify their tests as post hoc below.

Model. BoxCox(Q_t) = a0[s_t] + a1 P_t (+ phi y_{t-1}) + e, with two hidden states s_t that change
the intercept and the error sd, a two-state Markov chain, and 1-state alternatives. The model
is selected by AIC. We reused the Python port of this model from bundle 36d145c1 (files/code/hmm.py).
The port is not the official hydroState package.

Step A (fit WY1951-2016). A basin is "shifted" when a 2-state model has the lowest AIC, the low
state holds at most 50% of the years, and at least one run of 3 or more low years occurs. For
each low-state onset, we computed the precipitation z-score of the 3 preceding water years. We
compared the mean with a null that circularly shifts each basin's state series.

Step N (detection calibration). For each basin, we simulated 3 synthetic WY1951-2016 series from
each of two stationary 1-state models with the basin's real precipitation and missing years:
N1 = the AIC-best 1-state hydroState model; N2 = the same model with previous-year precipitation
P_{t-1} (storage memory). We applied the same fits and rules to these series.

Step B (out of sample). Parameters stay fixed at the WY1951-2016 fit. For basins that were low
in WY2016, we computed the forward-filtered probability of the normal state in WY2017-2025 and
the one-step predictive log score under "stay low" and "return to normal". For all basins, we
compared the predictive log score of the AIC-chosen model with that of the best 1-state model.

Addenda. (2) Same-likelihood 1-state competitors with P_{t-1} and a linear trend, and 2-state
models with P_{t-1}. (3) Regional mean of standardized residuals from a stationary relation
BoxCox(Q) = a + b P_t + c P_{t-1}, fitted on WY1951-2016. (4) "Mean-shift" 2-state models in
which the states change only the intercept and share one error sd, applied to the real data and
to all stored synthetic series.

## Results

All numbers are in files/results/summary.json (keys in brackets). Intervals are 95% basin-bootstrap
intervals unless we state otherwise. Log scores are natural-log predictive densities of annual Q,
per basin and year.

### 1. The hydroState-form model finds low states in many US basins (planned, Step A)

- With data to WY2016, a 2-state model has the lowest AIC in 405 of 554 basins (73%) [model_counts_fitA].
- 129 basins (23.3%, 19.9-26.7%) meet the shift rule [A1_shifted]. This is near the Victorian rate
  of 32% in bundle 36d145c1. No-AR models: 147; smoothed probabilities: 129.
- The low years of shifted basins form recurrent runs in 73 basins, one interior block in 20, one
  block at the end of the record in 28, and one block at the start in 8 [A3_pattern].
- Shifted basins occur in all regions (Figure 1a). California (USGS part 11) has 8 of 31.

### 2. Stationary simulations give almost the same result (planned Step N, Addendum 4)

- In synthetic series from stationary 1-state models, a 2-state model has the lowest AIC in
  72.4-73.8% (N1) and 73.5-75.6% (N2, with storage memory) of basins (range of 3 replicates), the
  same as the 73% in real data (Figure 2a) [N_detection].
- The hydroState-form shift rule flags 15.7-18.4% (N1) and 13.5-16.1% (N2) of synthetic series,
  against 23.3% of real basins. Thus about two thirds of the real detections are expected without
  any change in the rainfall-runoff relation.
- Cause: in 36% of real 2-state fits, the low-state error sd is less than 0.2 times the normal-state
  sd, often at the lower bound. A narrow or wide state absorbs a few outlier years.
- With the mean-shift form (one shared error sd; states change only the intercept; post hoc,
  Addendum 4), 62 real basins (11.2%, 8.7-13.9%) have a mean shift that beats every 1-state model
  (base, AR1, previous-year precipitation, trend) and meets the run rule [T_real]. The synthetic
  rates are 10.6-13.0% (N1) and 8.7-11.6% (N2) [T_sim_N1_shift_frac, T_sim_N2_shift_frac]. The
  expected count under N2 is 56; the probability of 62 or more is 0.17 [T_expected_N2]. The share of
  basins in which the mean-shift model beats all 1-state models is also the same: 223 real versus
  203-234 synthetic.

Thus annual runoff in these reference basins shows no clear excess of hidden mean shifts over
stationary series with storage memory.

### 3. Low-state onsets do not follow dry periods (planned A2)

- Mean z-score of precipitation in the 3 water years before 164 low-state onsets: +0.06; circular
  shift null 95% range -0.15 to +0.15; one-sided p (dry) = 0.80 (Figure 2b) [A2].
- Mean-shift form: 103 onsets, -0.05 (null -0.20 to +0.18), p = 0.35 [T_A2].
- In the synthetic series, the same statistic was -0.06 to -0.02 (N1) and +0.08 to +0.12 (N2)
  [N_onset_mean_z]. The Victorian mechanism (a low state that starts in a multi-year drought) does
  not appear in these data.

### 4. Most basins that were low in WY2016 returned in WY2017-2025 (planned Step B)

- 54 shifted basins were in the low state in WY2016. With parameters fixed at the WY1951-2016 fit,
  42 (78%) had a normal-state probability above 0.5 in at least one year of WY2017-2025 [B1].
- "Stay low" minus "return to normal": median -0.45 log units per year (-2.35 to +0.03); "stay low"
  scored better in 39% of these basins [B2]. A fit to WY2014 gave 43 of 53 returned and -2.12
  (-10.1 to -0.34) [B_sens_2014split].
- The 12 basins without a return have one long low block that started in 1985-2006 in 10 cases.
  Ten of the 12 are in the East (USGS parts 01-03). Most were not dry in WY2012-2016 (median precipitation z +0.42; 2 of 12 below 0). They had more
  rain in WY2017-2025 than the basins that returned (median maximum annual z 2.34 vs 1.73,
  Mann-Whitney p = 0.09) [B4]. These look like gradual changes, not drought effects.
- Memory form (2-state with previous-year precipitation, post hoc): 35 basins low in WY2016, 33
  returned; stay low minus return -2.62 (-4.13 to -1.06) [M_groupL]. Mean-shift form: 39 low, 36
  returned; -0.72 (-0.98 to +0.52) [T_groupL].

### 5. Hidden-state models predicted WY2017-2025 runoff worse than 1-state models

- In the 405 basins where AIC chose a 2-state model, its one-step log score was lower than that of
  the best 1-state model by a median 0.087 per year (0.068 to 0.106) [B3_2state_selected] (Figure 3b).
- The best memory model (P_{t-1}) also scored lower than the AIC-chosen hydroState model (median
  -0.050, -0.082 to -0.034), and adding P_{t-1} to the 1-state AR1 model lowered the score (median
  -0.036, -0.048 to -0.022), although the in-sample P_{t-1} coefficient is positive in 94% of basins
  [M_oos_mem_minus_hydrostate, M_oos_1mem_minus_1base].

### 6. Regional residuals: California recovered after 2016; the East stays low since about 2000 (Addendum 3)

Standardized residuals relative to BoxCox(Q) = a + b P_t + c P_{t-1}, fitted on WY1951-2016
(Figure 1b) [files/results/residuals/residual_summary.json]:

| Region (USGS parts) | Basins | WY2012-2016 | WY2017-2025 | WY2017-2025, wet years (P z > 0.5) |
| --- | --- | --- | --- | --- |
| California (11) | 31 | -0.34 (-0.52, -0.16) | +0.21 (-0.04, +0.46) | +0.35 (-0.05, +0.76) |
| West interior (09-10, 12-14) | 122 | -0.26 (-0.38, -0.15) | -0.05 (-0.14, +0.05) | +0.12 (-0.06, +0.31) |
| Central (05-08) | 161 | -0.32 (-0.41, -0.23) | +0.04 (-0.05, +0.13) | +0.12 (-0.01, +0.25) |
| East (01-04) | 240 | -0.34 (-0.40, -0.29) | -0.13 (-0.20, -0.07) | -0.12 (-0.22, -0.03) |

California runoff was below the relation during the 2012-2016 drought and returned to or above it
after 2016. No region shows a California-type persistent deficit. Eastern runoff has been below the
relation since about 2000 (5-year means -0.14 to -0.38), which agrees with the eastern "no return"
basins in result 4. WY2026 residuals are -0.44 to -0.97 in all regions; WY2026 uses mostly
provisional flow and preliminary nClimGrid values, so we do not interpret them.

### 7. Sensitivity and exploratory results

- 97% valid-day threshold: 128 shifted basins, 42 of 54 returned, 2-state minus 1-state score -0.089
  (files/results/sensitivity_valid97/summary.json).
- Including WY2026 in the stay-low test: median -0.56 (-1.99 to +0.02) [B2.low_minus_normal_with2026].
- Exploratory (Step C): the shift flag had a weak relation to snow share (+0.27 per SD, p = 0.02) and
  basin area (-0.23 per SD, p = 0.03), and no clear relation to aridity or baseflow index
  [C_logit_shifted]. Because most flags are expected under the null, we do not interpret these.

## Interpretation

The Victorian result does not transfer to US reference basins at the annual scale. The
hydroState-form AIC rule finds low states in about a quarter of basins, but stationary series give
most of these detections. Mean shifts occur at the null rate. Low-state onsets do not follow dry
years. Most basins that were low in WY2016 returned, and hidden-state models made worse
out-of-sample forecasts. California runoff fell below its rainfall relation in 2012-2016 and then
recovered. We did not find "watersheds that do not recover from drought" in these basins. A
method note also follows: an AIC preference for a 2-state annual runoff model is not evidence of a
state change unless it exceeds the rate in matched stationary simulations.

## Limitations

- We use annual totals and one model family. Seasonal or daily models can detect changes that
  annual models do not resolve.
- The hydroState-form results apply to our Python port with its parameter bounds (state sd at
  least 0.05 times the 1-state residual sd). The official hydroState package can behave
  differently. The bound affects how easily a narrow state absorbs outlier years.
- CAMELS basins are reference basins, but some have local human effects (diversions, land use,
  gauge and rating changes). The single-block "terminal" low states in the East can come from such
  effects or from changes in the nClimGrid station network; we cannot separate these causes.
- nClimGrid is an interpolated grid; its station density changes with time. The most recent
  months are preliminary. Together with provisional USGS flow, this can explain the large negative
  WY2026 residuals in all regions. We do not interpret WY2026.
- The synthetic nulls use Gaussian errors in Box-Cox space. Real errors can have heavier tails, so
  the null rates can be too low or too high. Three replicates per null give only a rough range.
- The 2012-2016 drought was severe mainly in California and the Southwest. Many basins in the
  "low in WY2016" groups were not in drought, so this is not a test of the response to one
  drought event in every basin.
- Addenda 2 and 4 are post hoc tests. We report the planned results unchanged.

## Reproduction

files/code/reproduce.sh SCRATCH_DIR downloads all inputs into SCRATCH_DIR and runs the full
pipeline: basin_climate.py, build_annual.py, run_us.py (fits), run_ext.py (memory models),
sim_null.py (synthetic nulls), run_tied.py (mean-shift models), residuals.py, analyze.py and
figures.py. Runtime is about 3 hours on 12-18 cores. The per-basin fit outputs that we used are in
files/fits/*.tar.gz, so analyze.py and figures.py can run without a refit (see files/code/README_code.md).
Exact USGS bytes are not bundled; their SHA-256 are in files/provenance/usgs_rdb_sha256.txt. USGS
can revise data, so a new download can differ.

## Files

- files/ANALYSIS_PLAN.md: plan and four dated addenda.
- files/DATA_NOTICE.md: external data sources, terms and attribution.
- files/data/annual_wy.csv: water-year Q, P, T, PET and data completeness for 671 basins (derived).
- files/data/basin_attributes.csv: area, centroid, aridity, baseflow index, snow share.
- files/results/: summary.json (all planned and added statistics), per-basin tables, null
  detection tables, residual tables, 97% sensitivity summary.
- files/fits/: per-basin model outputs (JSON in tar.gz).
- files/figures/: three figures.
- files/code/: all code.
- files/provenance/: hashes of all inputs.

## References

- Peterson, T. J., Saft, M., Peel, M. C., John, A. (2021). Watersheds may not recover from drought.
  Science 372, 745-749. doi:10.1126/science.abd5085
- Addor, N., Newman, A. J., Mizukami, N., Clark, M. P. (2017). The CAMELS data set. HESS 21, 5293-5313.
- Newman, A. J., et al. (2015). Development of a large-sample watershed-scale hydrometeorological
  data set for the contiguous USA. HESS 19, 209-223.
- Vose, R. S., et al. (2014). NOAA Monthly U.S. Climate Gridded Dataset (NClimGrid), v1.
  doi:10.7289/V5SX6B56
- Prior campaign bundle sha256:36d145c14c6ec974218c8e931718ed72d3cce8b76d5aec730e2ff5932212ff61
  (Victorian catchments after the Millennium Drought, 2018-2025).
