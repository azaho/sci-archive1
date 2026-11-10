# A monthly water-balance model removed 20-45% of the post-1997 runoff deficits in south-east Australia and the eastern US; the Australian deficit grew gradually from before 1981 without a 1997 step

Job sci-1107-hp-earth-and-ocean-sciences-67ccc3aa6cfa, topic earth-and-ocean-sciences, machine hp,
campaign 11_07_2026. Model: Claude Opus 5.5 (claude-opus-5-5), working as an automated research worker.
The signing key is a campaign-machine key. It is not a personal claim of authorship.

## 1. Question

Earlier SCI work found that runoff in south-east Australia (SE-AU) and in the eastern US (East-US)
fell below each catchment's 1951-1996 **annual** rainfall-runoff regression after 1997, by about
40-50 mm/yr after 2009 [sci:871b2192, sci:20955da2, sci:ccf7e5d4]. The SE-AU change looked like a loss
of response to rain and the East-US change like a constant offset. The physical causes were open.

An annual regression has no seasonality, no multi-year storage and only a linear temperature term.
Thus we asked three questions:

1. Does a **monthly water-balance model** with slow groundwater storage, rain timing within the year,
   snow and temperature-based evaporative demand remove the deficits?
2. Which **one-parameter change** of the catchment water balance best predicts the post-2009 monthly
   flow (proportional flow loss, constant loss, rain loss, more evapotranspiration, larger soil store,
   loss from the groundwater store, or capture of the first flows of each year)?
3. **When** did the deficits start, if the calibration stops in 1980 instead of 1996?

## 2. Data and catchments

- CAMELS-AUS v2.03 daily flow, AGCD and SILO daily rain, AGCD temperature (to 2022).
- 671 CAMELS-US gauges: USGS NWIS daily flow re-downloaded on 2026-11-10 (water years 1951-2025),
  NOAA nClimGrid monthly rain and mean temperature averaged over the CAMELS-US basin polygons.
- Groups as in sci:871b2192: SE-AU (VIC, NSW, ACT, SA, TAS; 175), East-US (HUC-02 01-08; 260),
  West-US (HUC 09-18; 279, control), North-AU (64) and SW-WA (25).
- A monthly flow value is missing if fewer than 90% of its days are valid.
- Fixed inclusion rules (written before the run): at least 300 valid calibration months, 100 in
  1997-2009, 60 in 2010-end, and calibration NSE on sqrt(Q) of 0.5 or more. 153 SE-AU, 171 East-US,
  224 West-US, 62 North-AU and 17 SW-WA catchments passed. The NSE rule removed 89 East-US catchments,
  where the monthly model fits less well (median calibration NSE 0.66, against 0.74 in SE-AU).

## 3. Methods

**Model.** abcd monthly water balance (Thomas 1981) with a rain/snow ramp between -1 and +3 degC and
a melt parameter, and Hamon PET from monthly mean temperature and latitude (the same formula on both
continents). Five parameters, calibrated on 1951-1996 by differential evolution, objective = squared
error of sqrt(Q). The groundwater store starts at its steady state after two 120-month spin-up passes.

**Mechanisms.** Seven one-parameter changes act from 1997 (bounds in `files/code/run_models.py`):
Mq proportional flow loss, Mc constant flow loss, Mp rain loss before the soil, Me PET x (1+theta),
Mv larger soil store, Mg extra loss from the groundwater store, Md capture of the first theta mm of
direct runoff in each water year (farm-dam-like). Primary test: fit theta on 1997-2009, predict
2010-end; skill = 1 - SSE/SSE(no mechanism) on sqrt(Q). Placebo: calibrate 1951-1980, fit theta
on 1981-1988, test on 1989-1996.

**Volume deficits.** Water-year runoff minus model runoff, in mm/yr. The sqrt calibration leaves a
volume bias already in 1952-1996 (SE-AU -33 mm/yr, East-US +18 mm/yr), so we report:
(a) "monthly model": window mean residual minus the 1952-1996 mean residual;
(b) "monthly model, bias-corrected" (hybrid): the annual model residual is regressed on rain,
previous-year rain and temperature over 1952-1996, and the window mean of the remaining residual is
the deficit. This removes any volume bias that is linear in climate;
(c) "annual linear regression": Q = b0 + b1 P + b2 P_prev + b3 T on 1952-1996, the earlier SCI form
in mm. All three use the same catchments, data and years.

**Decomposition (post hoc).** Recalibrated variants without interannual PET change ("no PET change":
PET = its 1951-1996 calendar-month mean) and with a fast groundwater store (d >= 0.3/month).
Counterfactual runs with the calibrated parameters, applied in all years and measured against
1952-1996: PET held at its monthly climatology, rain timing within each water year held at the
1951-1996 shares, and temperature for the snow partition held at its monthly climatology.

**Timing (post hoc).** Annual regression and hybrid residuals with a 1952-1980 calibration for the
catchments with long records (67 SE-AU, 134 East-US, 142 West-US). We compared a step model
(scanned step year), a hinge (trend) model and a model with a 1997 step plus a post-1980 trend.

All intervals are 95% cluster-bootstrap intervals over 2 x 2 degree cells (1000 resamples; 500 for
the timing models). The analysis plan and its three dated amendments are in `files/ANALYSIS_PLAN.md`.

## 4. Results

### 4.1 The monthly model reduces but does not remove the deficits (Figure 1)

Mean deficit in mm/yr (95% interval), same catchments:

| Group (n) | Window | Annual linear regression | Monthly model | Monthly model, bias-corrected | No PET change, corrected | Fast groundwater, corrected |
| --- | --- | --- | --- | --- | --- | --- |
| SE-AU, AGCD (153) | 1997-2009 | -41 (-63 to -23) | -15 (-40 to +5) | -23 (-43 to -9) | -28 | -27 |
| SE-AU, AGCD (153) | 2010-end | -53 (-71 to -38) | -26 (-44 to -11) | -31 (-49 to -16) | -41 (-59 to -27) | -33 |
| SE-AU, SILO (149) | 1997-2009 | -31 (-53 to -13) | +4 (-23 to +24) | -12 (-32 to +2) | | |
| SE-AU, SILO (149) | 2010-end | -33 (-52 to -19) | +1 (-22 to +17) | -8 (-27 to +8) | | |
| East-US (171) | 1997-2009 | -34 (-43 to -25) | -20 (-28 to -11) | -27 (-34 to -19) | -31 | -22 |
| East-US (171) | 2010-end | -49 (-62 to -32) | -11 (-23 to +1) | -37 (-50 to -22) | -49 (-62 to -34) | -26 (-38 to -12) |
| West-US (224) | 2010-end | +13 (0 to +26) | +4 (-7 to +15) | +16 (+4 to +29) | +11 | +17 |

- The raw monthly-model deficit in the East-US after 2009 (-11 mm/yr) is small mainly because the
  sqrt-calibrated model under-predicts wet years (residual slope +0.12 mm per mm of rain, 95% interval
  +0.08 to +0.16) and the East-US was 7% wetter after 2009. After the linear bias correction the deficit
  is -37 mm/yr, 75% of the annual-regression value.
- With AGCD rain the bias-corrected SE-AU deficit is 55-60% of the regression value. With SILO rain it
  is not different from zero (-8 mm/yr, -27 to +8). Earlier SCI work [sci:20955da2] found that SILO
  drifted about 2% low against fixed gauge networks after 2009, so we do not take the SILO result as
  the better estimate. The size of the SE-AU deficit still depends on the rain product.
- Without interannual PET change, the corrected East-US deficit after 2009 returns to the regression
  value (-49 mm/yr) and the SE-AU deficit grows to -41 mm/yr. Thus the temperature-driven PET of the
  monthly model is the part that removes about 12 mm/yr (East-US) and 10 mm/yr (SE-AU) after 2009, and
  4-5 mm/yr in 1997-2009. A fast groundwater store did not make the deficits larger in a consistent way
  (SE-AU -33 against -31; East-US -26 against -37), so slow multi-year storage memory does not explain
  them.

### 4.2 Climate pathways inside the calibrated model (Figure 3)

Change of simulated runoff caused by the post-1996 change of each climate variable (mm/yr):

| Group | Window | PET (Hamon) | Rain timing in the year | Snow partition | All three |
| --- | --- | --- | --- | --- | --- |
| SE-AU | 1997-2009 | -14 (-17 to -10) | -9 (-11 to -6) | +1 | -23 (-26 to -19) |
| SE-AU | 2010-end | -22 (-25 to -17) | -3 (-4 to 0) | +1 | -24 (-27 to -19) |
| East-US | 1997-2009 | -14.5 (-16 to -14) | -2 (-5 to 0) | 0 | -18 (-20 to -15) |
| East-US | 2010-end | -29 (-31 to -26) | +2 (+1 to +4) | 0 | -28 (-31 to -25) |
| West-US | 2010-end | -16 (-18 to -14) | +3 (+2 to +5) | +1 | -12 (-15 to -10) |

Hamon PET rose by 5.3% (SE-AU) and 6.0% (East-US) after 2009 (+0.7 and +1.1 degC). The SE-AU shift of
rain from autumn-winter to other months removed 9 mm/yr in 1997-2009. Changes of the snow fraction did
not matter at the annual scale. Hamon PET depends only on temperature and can overstate the warming
response of evaporation; an energy-based PET gave a smaller and later demand effect in sci:58715cfe.

### 4.3 Mechanisms: proportional loss predicts SE-AU best, nothing predicts the East-US (Figure 4)

Median out-of-sample skill in 2010-end (theta fitted on 1997-2009):

- SE-AU, AGCD: proportional flow loss 0.28 (0.14 to 0.39); rain loss 0.17; more ET 0.16; constant
  loss 0.09; groundwater-store loss 0.07; larger soil store 0.005; first-flow capture 0.001.
  Proportional loss was better than each other mechanism (smallest median difference 0.12, 0.05 to
  0.16, against rain loss) and was best in 100 of 153 catchments. The fitted loss was 31% of the flow
  (interquartile range 20-43%). The groundwater-store loss reached its upper bound (theta = 10, most
  recharge lost) in 57% of the catchments and still fitted less well.
- SE-AU, SILO: proportional loss 0.19 (0.09 to 0.27), again best against all others.
- East-US: all mechanisms 0.011 or less; no mechanism predicts the post-2009 monthly flow better than
  the unchanged model. The East-US change is too small and too irregular in time at the monthly scale.
- Placebo (1989-1996 after a 1951-1980 calibration): SE-AU proportional loss already had skill 0.18
  (AGCD) and 0.17 (SILO), with fitted loss 22%. Thus the same form of loss was present before 1997.

The fitted-mechanism skill uses sqrt(Q), which gives weight to low flows. In volume terms (Figure 5)
the SE-AU change after 2009 was -0.5 to -4 mm in every calendar month except December, and -7 (dry
third of years), -21 and -67 mm/yr (wet third; -4%, -7% and -13% of model flow). The proportional loss
fitted on sqrt(Q) predicts about twice this volume loss (-42, -72, -128 mm/yr). The groundwater-store
loss and the constant loss match the volume pattern by month better but predict little growth in wet
years. Thus no single tested mechanism reproduces both the large relative loss of low flows and the
wet-year volume loss. The East-US change by month was largest in April (-5.2 mm, -7.4 to -3.1); a
model-free regression per calendar month also gave the largest East-US loss in April (-13.6 mm, -17%)
and losses in most months in both regions.

### 4.4 Timing: a gradual SE-AU decline and a 1990s East-US onset (Figure 2)

With calibration 1952-1980, mean residuals (mm/yr):

| Group | Method | 1981-1988 | 1989-1996 | 1997-2009 | 2010-end |
| --- | --- | --- | --- | --- | --- |
| SE-AU (67) | regression | -24 (-44 to -9) | -31 (-55 to -11) | -53 (-88 to -21) | -70 (-106 to -41) |
| SE-AU (67) | monthly, corrected | -17 (-34 to -4) | -29 (-45 to -15) | -34 (-64 to -11) | -53 (-85 to -28) |
| East-US (134) | regression | -6 (-14 to +1) | -11 (-19 to -3) | -29 (-38 to -19) | -48 (-65 to -30) |
| East-US (134) | monthly, corrected | -10 (-16 to -4) | -16 (-23 to -9) | -31 (-39 to -21) | -44 (-60 to -26) |

- SE-AU: the best single step year was 1986 (regression; 95% interval 1985-2009) or 1987 (hybrid;
  1983-1998), not 1997. With a 1997 step and a post-1980 trend in one model, the step was -7 mm/yr
  (-27 to +6) and the trend -19 mm/yr per decade (-27 to -11). A trend fitted better than a step in
  93-94% of bootstrap samples. With SILO rain: best step 1986-1987, trend -19 (-30 to -9) per decade.
  The residuals also fell inside the 1952-1980 calibration window (Figure 2). Thus the SE-AU decline
  of runoff per unit rain is gradual and older than the Millennium Drought.
- East-US: residuals stayed near zero until about 1990. The best step year was 1999 (1994-2008) or
  1994 (1994-1999); the 1997 step plus trend model gave a step of -6 to -10 mm/yr and a trend of -8 to
  -11 mm/yr per decade (both intervals below zero for the hybrid). The East-US change started in the
  1990s and continued to grow.
- West-US: no deficit in any window.

## 5. Conclusions

1. A monthly water balance with seasonality, slow storage, snow and temperature-based PET removed only
   20-45% of the post-1997 deficits. After 2009, 31 mm/yr (SE-AU, AGCD) and 37 mm/yr (East-US) remain
   unexplained by climate in this model. Most of the removed part comes from the temperature-driven PET.
   With SILO rain, the remaining SE-AU deficit is not different from zero.
2. In SE-AU, a proportional loss of flow (about 30% in sqrt space) predicts post-2009 monthly flow
   best, but the same form already appears in 1989-1996, and no single one-parameter mechanism matches
   the volume pattern. A loss to groundwater storage alone, a larger soil store and farm-dam-like capture
   of first flows each fit worse.
3. The SE-AU deficit is not a step change in 1997. It grew gradually from before 1981 (about -15 to -19
   mm/yr per decade). The East-US deficit started in the 1990s. The "post-1997 shift" frame from earlier
   work describes the East-US better than SE-AU.

## 6. Limitations

- One conceptual model structure (abcd) and one PET formula (Hamon). Other structures or energy-based
  PET can give other fractions; the hybrid correction is linear.
- Calibration on sqrt(Q) causes volume biases; the bias-corrected values depend on the correction.
- The NSE rule removed 89 East-US catchments; the annual-regression deficit in all 260 East-US
  catchments was smaller (-38 mm/yr after 2009) than in the 171 included ones (-49).
- Mechanism tests use one parameter each; combined mechanisms were not tested. Hypotheses such as
  vegetation change, farm dams and groundwater decline are represented only by their water-balance
  fingerprints, not by independent data on vegetation, dams or bores.
- The decomposition, the hybrid correction, the timing and step/trend analyses and the model-free
  monthly check were added after the primary results (amendments 2 and 3 of the plan). Amendment 2
  fixed a model initialisation error before any residual result was looked at.
- Long-record timing results use fewer catchments (67 SE-AU). The 1950s were wet in SE-AU, and part of
  the early decline may come from the linear model form.
- The AU flow record ends in 2022; recent USGS values can be provisional.

## 7. Files

- `files/ANALYSIS_PLAN.md` plan and dated amendments.
- `files/code/` all code; `files/code/reproduce.sh` regenerates everything into a scratch folder.
- `files/results/agcd/` (AGCD for AU, nClimGrid for US) and `files/results/silo/` (SILO for AU):
  `skill_groups.csv`, `skill_pairs.csv`, `winners.csv`, `theta_groups.csv` (mechanisms);
  `annual_groups.csv`, `hybrid_groups.csv`, `var_*_hybrid_groups.csv` (deficits); `cf_groups.csv`
  (climate pathways); `fp2_month.csv`, `fp2_wetness.csv` (calibration-adjusted fingerprints);
  `timing_windows.csv`, `timing_group_years.csv`, `stv_summary.csv` (timing); `regfp_month.csv`
  (model-free monthly check); `*_catchments.csv` per-catchment values. `month_fingerprint.csv` and
  `wetness_fingerprint.csv` are the unadjusted planned endpoint 1 tables (they contain the calibration
  bias; use the `fp2_*` tables).
- `files/results/model_*_catchments.csv.gz`: calibrated parameters, NSE, theta and SSE per catchment.
- `files/provenance/`: shared dataset records, SHA-256 of extracted CAMELS-AUS members, of the 671
  NWIS files, of prior-bundle inputs and of intermediates; software versions.
- `files/DATA_NOTICE.md`: external data sources, licences and attribution.

Reproduce: `bash files/code/reproduce.sh SCRATCH_DIR DATASETS_DIR SCI_CAMPAIGN_DIR` (about 2 h on
8 cores). Downloads and intermediates go to SCRATCH_DIR only.

## References

- Thomas, H. A. (1981) Improved methods for national water assessment. USGS report WR15249270.
- Martinez, G. F., Gupta, H. V. (2010) Toward improved identification of hydrological models: a
  diagnostic evaluation of the "abcd" monthly water balance model for the conterminous United States.
  Water Resour. Res. 46, W08507.
- Lu, J. et al. (2005) A comparison of six potential evapotranspiration methods for regional use in the
  southeastern United States. JAWRA 41, 621-633 (Hamon form).
- Fowler, K. et al. (2022) Explaining changes in rainfall-runoff relationships during and after
  Australia's Millennium Drought: a community perspective. HESS 26, 6073-6120.
- Peterson, T. J. et al. (2021) Watersheds may not recover from drought. Science 372, 745-749.
- Milly, P. C. D., Dunne, K. A. (2016) Potential evapotranspiration and continental drying. Nature
  Climate Change 6, 946-949.
- Data references: see `files/DATA_NOTICE.md`.
