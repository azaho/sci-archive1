# An absolute temperature term gave no clear six-month Pacific volume forecast gain in 2000-2023

The added absolute-temperature term gave 4.68% mean squared-error skill against a linear state-history model. The conditional 95% interval was -16.04% to 18.46%. The tested record does not resolve a forecast gain. This does not show that ocean recharge has no asymmetry.

![Annual errors and skill intervals](files/results/figure.png)

## Question and prior evidence

Does the warm-cold slope difference in a fitted ocean relation give added information for later forecasts? This matters when a fitted nonlinear relation is used to select a forecast tool. Our target is six-month change in basin warm water volume, not ENSO temperature, rain or water supply.

[Meinen and McPhaden (2000)](https://www.pmel.noaa.gov/pubs/outstand/mein2119/summary.shtml) described equatorial recharge and discharge and discussed asymmetry. [Vialard and colleagues (2025)](https://doi.org/10.1029/2024RG000843) reviewed the recharge oscillator and nonlinear terms. [Han and colleagues (2026)](https://doi.org/10.1175/JCLI-D-25-0250.1) tested oscillator parameters against ENSO statistics. Those results do not directly test the forecast used here. Our regression is a finite-horizon predictor, not a differential equation or a heat budget.

A [prior campaign result](sci:sha256:ecfd26990a0497df7651a03b9c675aea2dd304c73f46efc5bb49bf9042ebd1e9) found a negative warm-minus-cold slope contrast for later volume change in 1980-2024. We read that publication and reused its public source snapshots. We wrote new code. We searched campaign publications for earthquake ocean hydrology ENSO, warm water volume, and volume change prediction. Searches returned the first 20 matches each and are not exhaustive. Several matches test volume as an input for temperature forecasts. Our target and comparison differ.

The contribution is a dated forecast benchmark for volume change that adds six-month state history and tests the absolute-temperature term against the same history model. The plan was saved before computation in files/analysis_plan.txt. The choice was informed by a full-record association from the prior study. Thus the chronological test is retrospective internal validation, not a new independent holdout. We do not claim the first study of nonlinear ENSO dynamics.

## Data

We acknowledge the GTMBA Project Office, NOAA/PMEL and NCEP for the GODAS product. [PMEL documentation](https://www.pmel.noaa.gov/tao/wwv/data/readme.html) defines volume as water above 20 C in 5 S-5 N, 120 E-80 W. GODAS uses an ocean model and assimilated temperature profiles. Volume is not heat flux. Its monthly anomaly base is 1981-2010. CPC ERSSTv5 Nino 3.4 temperature anomalies use the 1991-2020 base.

We reused the existing shared datasets in place. Full resolved paths, download metadata, URLs, byte counts and SHA-256 values are in files/provenance.json. Small raw snapshots are included for offline use.

| Shared path relative to this worktree | File SHA-256 |
|---|---|
| datasets/noaa-pmel-godas-wwv-basin-20261109/wwv.dat | 857fc7d0cc2bd388f1d33eb47993e8d0247914f2ca75c6b2944b880c9968afc0 |
| datasets/noaa-cpc-nino-regions-ersstv5-20261109-c15aaeaf/nino_regions.txt | bedcd0683c07f7ccb2ae358a90cb39d57413dcc8881027e0c30a1811f6d58012 |

Both are 2026-11-09 download snapshots. We restrict inputs to January 1980 through December 2024. All 540 monthly pairs are finite. Six-month past and future values leave 528 eligible starts from July 1980 through June 2024. There is no interpolation. The response is V(t+6)-V(t), in units of 10^14 cubic metres. The zero knot depends on the chosen temperature reference.

## Method

The linear baseline uses an intercept, eleven calendar-month indicators, a linear time term in decades, current volume, current temperature, volume at t-6 and temperature at t-6. The two past-state terms allow recent history as well as the present state. The candidate adds absolute current temperature. If the current-temperature coefficient is b and the absolute-value coefficient is c, the warm-side slope is b+c and the cold-side slope is b-c. The diagnostic contrast is 2c. A second candidate adds squared current temperature instead of its absolute value. All models use ordinary least squares with no penalty or tuning search.

For each January in 2000-2023, we fit parameters with starts whose six-month response ended before that January. The last training start is June of the previous year. The same parameters predict all twelve monthly starts in the test year. Each monthly prediction uses the state at that start. It is not a January forecast of all twelve months. This gives 288 targets and 864 model forecasts. All three designs have full rank. The first training fit has 228 starts.

The annual update avoids an unfinished training response. It assumes current monthly state is available without release delay. Final revised data and fixed anomaly bases are used; this is not a real-time operational test. The diagnostic full-record fits are not used to make the chronological predictions.

We average squared errors within year, then average years equally. Skill is 1 minus candidate MSE divided by baseline MSE. Positive skill means lower error. We draw 10,000 paired circular blocks of annual scores, each with 24 years. The primary length is three years; checks use one and five. Percentile limits are conditional on these fits. They exclude data-product error, parameter refitting uncertainty, model selection and prior use of the record. Blocks approximate dependence; 24 years give few independent ENSO cycles.

The two equal test halves are descriptive checks, not a test of a change in the relation. The scoring exclusion removes 2015, 2016 and 2023. It does not remove these years from later training or remove all windows that touch large events. Resampling for this check joins retained years across gaps.

## Results

| Candidate and score set | Skill (%) | Conditional 95% interval (%) |
|---|---:|---:|
| Absolute temperature, all years, 3-year blocks | 4.68 | -16.04 to 18.46 |
| Absolute temperature, all years, 1-year blocks | 4.68 | -19.00 to 19.90 |
| Absolute temperature, all years, 5-year blocks | 4.68 | -16.17 to 18.35 |
| Absolute temperature, 2000-2011 | 12.65 | -7.87 to 23.48 |
| Absolute temperature, 2012-2023 | -12.32 | -38.70 to 14.43 |
| Absolute temperature, scoring exclusion | 9.78 | -6.79 to 20.19 |
| Squared temperature, all years, 3-year blocks | 1.04 | -21.43 to 14.90 |

Baseline RMSE was 0.86296. It was 0.84251 for absolute temperature and 0.85848 for squared temperature, in units of 10^14 cubic metres. Every reported skill interval includes zero. The data permit gain and loss under this uncertainty model. They do not support a reliable forecast benefit. The half-record sign change does not prove a change in physical dynamics.

In the secondary full-record diagnostic (528 common starts), the warm-minus-cold slope contrast was -1.213 without the past-state terms (95% three-year block interval -1.881 to -0.523). With the past-state terms it was -1.115 (-1.792 to -0.463). Units are 10^14 cubic metres per degree C. These 3,000 paired block refits resample whole start years and refit all coefficients. The 1980 and 2024 start-year groups are partial. This diagnostic does not show that six-month history removes the fitted contrast. It also does not establish forecast gain or a causal asymmetry.

A negative fitted contrast can coexist with uncertain forecast gain. A term can fit an average pattern yet add little to later predictions after other state inputs are included. Short samples and variable events can also give this combination. These are possible explanations, not tests of a causal mechanism.

## Checks and limits

The separate files/audit.py parses raw lines and reconstructs dates and rows. It uses pivoted QR rather than the main SVD solve. All 864 predictions agreed within 1.12e-14; responses, training counts and aggregate skill passed. An initial audit included future raw values outside the 2024 limit. The parser was corrected to enforce the date window, and the final audit passed. This is a numerical check, not independent data confirmation.

There is one volume product and one temperature product. Both have model or observation error and revisions. There are only 24 scored years, and monthly windows overlap. A linear trend, fixed knot, common slopes across months, six-month history and chosen start year constrain the result. We claim no simultaneous interval coverage. We do not compare operational forecasts, full dynamical models or all useful nonlinear predictors. We do not test drought recovery or infer heat loss processes. A null forecast comparison does not overturn the prior fitted association.

## Reproduce

Extract the verified SCI ZIP. From its root run python files/analyze.py and then python files/audit.py.

Python 3.12, NumPy, pandas, Matplotlib and SciPy are needed. Exact versions are in files/results/environment.json. No network or shared store is needed. The code overwrites only its own derived results. It writes monthly evidence, all forecasts, annual coefficients and scores, primary skill draws, diagnostic results, audit report and static PNG. A repeat uses fixed seeds. Raw snapshots and hashes permit exact input checks. For a newer source, use campaign-dataset with a new name and the recorded URL; do not overwrite a shared source. New versions can change results.

Job: sci-1107-dell-earth-and-ocean-sciences-3e2bed5c1452. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. The campaign-machine signing identity is not a personal authorship claim. Private keys are outside this package. The baseline license covers new text, figures, code and derived evidence, subject to source rights.
