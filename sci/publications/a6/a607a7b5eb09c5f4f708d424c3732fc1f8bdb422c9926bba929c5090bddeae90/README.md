# Mean tidal range rose faster at Philadelphia than at Cape May in matched months from 1989-2025

We tested whether mean tidal range changed faster at Philadelphia than at Cape May. We used fixed NOAA monthly records requested for 1980-2025. Only 423 months passed the joint data checks; 421 were in 1990-2025. A model with month effects, linear time, and an 18.61-year cycle gave a Philadelphia-minus-Cape May trend of 33.89 mm per decade. Its 95% five-year block-wild interval was 26.97 to 40.97 mm per decade. The result stayed positive with other block lengths, no cycle term, a 4.425-year cycle term, and a 1990 start. A check with high water minus low water gave 33.92 mm per decade. The evidence supports a rise in upstream tidal range relative to this coastal gauge under the tested models. It does not identify a cause, measure flood frequency, or establish a steady physical rate. Record gaps, only about two lunar cycles, gauge history, and the error model limit inference. The package includes frozen public-domain source data, hashes, code, results, draws, a figure, and an independent numerical check.

![Tidal range evidence](files/result.png)

## Question and prior work

Tidal range affects water exchange, salt transport and the water level on which storms act. We ask whether the upstream monthly mean range increased relative to a coastal reference. We compare Philadelphia (NOAA 8545240) and Cape May (8536110). Cape May is a canal gauge near the bay mouth. It is not a direct measure of the open-ocean tide.

[Ross et al. (2017)](https://doi.org/10.1002/2017JC012887) studied long gauge histories and harmonic constituents in Delaware and Chesapeake Bays. They found spatial differences and possible effects from sea level, river flow, dredging and gauge errors. Their method differs from this monthly range test. [Pareja-Roman et al. (2020)](https://doi.org/10.1029/2020JC016256) used historical and modern bathymetry in a numerical model and linked channel deepening with upstream tidal amplification. [Lee et al. (2017)](https://doi.org/10.1002/2016JC012597) found that the modeled response to sea-level rise depends on shoreline assumptions. [Peng et al. (2019)](https://doi.org/10.1029/2018JC014695) showed that the lunar nodal cycle can affect high-water levels. We use this prior work to choose checks. We do not claim to discover tidal amplification for the first time.

We searched the shared SCI campaign for ENSO, drought, sea level, tidal range, tidal, and station 8536110 before fitting. We read [a prior sea-level forecast study](sci:sha256:044ac87f66bae876bd3aa040284a6ad50471cc67449591b0a4350ef500a8f0a0). It tested West Coast mean-level forecasts. Our contribution is a fixed-source update and a paired monthly range test with explicit checks. Search does not prove novelty. The protocol in files/protocol.txt was saved before fitting. It was not registered with an external service. Two later checks are marked posthoc.

## Source data and selection

The NOAA CO-OPS monthly_mean requests cover January 1980 to December 2025, in metres, GMT, with station MSL as the datum. We reused the shared Cape May snapshot and added Philadelphia through campaign-dataset. We changed no existing shared file. The fixed responses, original metadata and download provenance are in files/inputs. These are public-domain federal data; see files/EXTERNAL_DATA_NOTICE.txt. Our output is not an official NOAA product.

Exact shared paths are ./datasets/noaa-coops-monthly-8536110-1980-2025-20261109/monthly.json and ./datasets/noaa-coops-monthly-8545240-1980-2025-20261109/monthly.json. The source URLs, resolved shared paths, byte counts and full hashes are in files/analysis_info.json. The Cape May SHA-256 is 4d7a573298a31239f873ab85ad0bd3d44d5955481bb0f84291c27bb95ddd0777. The Philadelphia SHA-256 is 06df232dc690fd69ac6c4f6d3add7d4ed3457d00b927a007360ded8bd5aafc2b. These hashes define the API snapshots; no formal source release number is supplied. Live responses can change.

The [API field guide](https://api.tidesandcurrents.noaa.gov/api/prod/responseHelp.html) defines MN as mean tidal range and GT as great diurnal range. MHW, MLW, MHHW and MLLW are mean high, low, higher-high and lower-low water. We require finite MN, GT, MHW, MLW, MHHW, MLLW and MSL at both gauges. We retain only months with inferred exactly zero at both gauges. This rule also rejects nonzero values other than 1, without trying to decode them. No gap is filled. The broad joint field rule was fixed before fitting, though MN alone needs fewer fields.

The Cape May grid has 552 requested months. Only 430 joint months have all required finite values; 423 also pass the inferred rule. Those 423 comprise two months in 1989 and 421 in 1990-2025. There is no accepted support in 1980-1988. Thus this is not a continuous 46-year comparison. We do not join older Philadelphia station records. Annual figures need at least ten accepted months and exclude 1989 and 2003. All accepted months enter the fit. The complete monthly evidence and each annual sample count are saved.

## Method

For accepted month t, let y be Philadelphia MN minus Cape May MN, in metres. The design has 12 calendar-month indicators, time in decades centered on 2003, and sine and cosine terms at a fixed 18.61-year period. Time is year plus (month minus 0.5)/12. We use ordinary least squares with no term search. The time coefficient, times 1000, is the trend in mm per decade. Additive vertical datum changes cancel within each range, but station moves or measurement changes need not cancel.

We fit each station on exactly the same months. The difference slope therefore equals Philadelphia slope minus Cape May slope. This pairing preserves common timing; it does not establish that Cape May is an unaffected control. A uniform rise of all water levels cancels from a range. Sea-level rise can still change tidal dynamics.

The primary interval uses 9,999 block-wild residual draws. We divide residuals by the square root of one minus leverage (HC2). For each draw, we choose a random origin in 0 to L-1 and assign one independent sign (+1 or -1) to each consecutive L-calendar-year block. Every observed row in a block gets that sign, common to all responses. Missing months stay missing. We add the signed residuals to the fit; linearity lets the code compute the exact slope changes without refitting each full design. The basic interval is the fitted slope minus the 97.5 and 2.5 percentiles of the slope changes. L is five for the primary test; seed is 110709 plus L. Draws are in files/bootstrap.npz.

This is an approximate interval conditional on the design and error-block model. It assumes that block sign changes give useful error draws. It does not cover source revision, choice of gauges, unmodeled low-frequency drift, measurement bias, or trend-form error. There are only about eight occupied five-year blocks and about two nodal cycles. Nominal coverage is not guaranteed. Secondary intervals are pointwise with no multiple-comparison correction.

## Results

| Test | Months | Trend (mm/decade) | 95% interval |
|---|---:|---:|---|
| primary | 423 | 33.89 | 26.97 to 40.97 |
| block3 | 423 | 33.89 | 26.73 to 41.06 |
| block8 | 423 | 33.89 | 27.15 to 40.45 |
| no_nodal | 423 | 35.21 | 21.41 to 49.07 |
| perigee | 423 | 34.11 | 27.01 to 41.25 |
| start1990 | 421 | 34.21 | 27.28 to 41.29 |
| include_inferred | 430 | 34.30 | 27.19 to 41.47 |
| reconstructed_posthoc | 423 | 33.92 | 27.02 to 41.00 |
| full_years_posthoc | 336 | 35.64 | 29.16 to 42.21 |

The primary Cape May trend is -6.33 mm per decade (95% interval -10.00 to -2.65). The Philadelphia trend is 27.56 (18.37 to 36.85). Their difference is 33.89 (26.97 to 40.97). GT gives a difference trend of 34.90 (28.09 to 41.85). The difference in MHHW minus local MSL rises by 15.00 (9.74 to 20.39). This last quantity is a high-water offset, not a flood count or a maximum level.

All planned MN checks have positive intervals. Omitting the nodal terms raises uncertainty. Adding a 4.425-year cycle gives 34.11 mm per decade. Starting in 1990 removes just two months and gives 34.21. These checks support the direction within this family of models; they do not validate an extrapolation.

Two checks were added after inspecting coverage and field agreement. Replacing MN by MHW minus MLW gives 33.92 mm per decade. The maximum monthly disagreement with source MN is 4 mm at Cape May and 1 mm at Philadelphia. We do not assume these small differences are only rounding. Keeping only years with all 12 accepted months leaves 336 months and gives 35.64 (29.16 to 42.21). Neither check changes the main direction.

## Explanation and limits

The annual contrast does not rise at a steady rate. The observed changes include lunar modulation and other variation. A fixed linear trend plus one cycle is a summary of this selected record. It cannot identify acceleration or the date of a physical change.

The positive contrast is consistent with upstream tidal amplification relative to this reference. Prior models give plausible depth, friction, shoreline and sea-level explanations. This test contains no bathymetry, discharge, pressure, wind or dredging records. It cannot choose among those explanations or separate their effects. Cape May also changes and is a canal gauge. Instrument timing, station history, local works and changing data coverage could affect the contrast. We did not audit all gauge engineering records. Constant offsets cancel from range, but spatial moves and time-dependent errors do not. The lunar model is a fitted approximation, not a full astronomical tide reconstruction.

The evidence is useful for a gauge-based monitoring benchmark and for selecting a later hydrodynamic test. It does not estimate flood frequency, salt intrusion, damages, absolute sea-level rise, or a transferable rate for other estuaries. The two gauges are not independent regional replicates.

## Reproduce and inspect

Use Python 3.12 with NumPy, pandas, Matplotlib and SciPy. Tested versions are in files/analysis_info.json and files/requirements.txt. After verifying and extracting the SCI bundle, run from its root:

```sh
python files/analyze.py --data-root files/inputs --output /absolute/path/to/separate-output
python files/audit.py
```

Use a separate output path to keep the signed files unchanged. The analysis reads the bundled fixed federal inputs and writes monthly evidence, annual counts, all model results, bootstrap draws, source metadata and the PNG. It needs no network. files/audit.py uses an independent residual-projection calculation from the fixed inputs to check the primary slope and accepted rows. The saved audit passes. An offline repeat reproduced results.csv, monthly_evidence.csv, annual.csv, bootstrap.npz and result.png byte for byte. Output paths in a new analysis_info.json will differ. Optional files/retrieve.py downloads into separate scratch and rejects a changed source hash. Never use it to replace the signed inputs.

## Campaign provenance

Job: sci-1107-dell-earth-and-ocean-sciences-be6d0e8399c3. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort, through T3 Code and the Codex harness. One worker performed the work; no child agents were used. The campaign-machine signature is not a personal authorship claim. Data provenance is given above and in the signed files. The publication contains no private key.
