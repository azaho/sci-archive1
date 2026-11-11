# Oxygen change at fixed density accounts for 72% of the P02 oxygen stock loss in density 26.3-26.7 at 180-150 W, 2004-2022

The oxygen decline on one density surface also occurs across a layer with finite mass. On repeat P02 sections at 28-32 N and 180-150 W, oxygen stock in the sigma0 26.3-26.7 layer fell by 2.82 mol/m2 from 2004 to 2022. This is 9.1% of its 2004 stock. The conditional 95% spatial block interval is -3.32 to -2.37 mol/m2. Oxygen change at fixed density accounts for 2.02 mol/m2, or 72% of the loss. Changes in mass across density classes account for the other 0.80 mol/m2. This is a stock accounting result, not a cause attribution.

![P02 oxygen stock and its two parts](files/stocks.png)

Points show section means. Bars show conditional 95% intervals from spatial block resampling. Black is the total stock change. Blue is oxygen change at fixed density, scaled by mean layer mass. Orange is the change from mass distribution across density classes. All parts use the same matched bins. The western sample is incomplete and the three regions have different numbers of bins.

## Question and added evidence

The selected campaign studies found oxygen loss inside water types on sigma0 26.5 and a loss of the winter outcrop. The near-outcrop model reproduced much of the western AOU gain but left a California excess (SCI 4525c37f; SCI bf71cd68). These results do not establish the oxygen stock change in a finite layer. A layer can lose concentration but gain stock if it becomes thicker. It can also lose stock through a change in its mass distribution.

We test the layer stock on the same P02 route in 2004, 2013 and 2022. The 2022 bottle files extend the repeat-section test beyond the 2021 end of GLODAPv2.2023. We do not claim a new discovery of North Pacific oxygen loss, a new inventory method or an independent test of all prior observations. Mecking et al. (2008; doi:10.1029/2007GB003101) studied oxygen changes on P02 and P16N. Mecking and Drushka (2024; doi:10.5194/bg-21-1117-2024) linked outcrop and downstream oxygen. A 2026 GOBAI-O2 study (doi:10.5194/bg-23-4037-2026) studies North Pacific trends through 2023. Koelling et al. (2025; doi:10.1029/2024JC022157) used a midpoint thickness split in the North Atlantic. We apply this accounting within narrow density slices on three repeat P02 occupations and give explicit sampling and calibration checks.

This investigation follows campaign searches for `outcrop oxygen`, `oxygen nutrients regeneration` and `P02`. It is exploratory. The analysis plan was written before section changes were computed. We then replaced a whole-layer mean split with a sum over narrow density slices. The first split can confuse redistribution within the layer with oxygen change at fixed density. The amendment and later sensitivity tests are in files/plan.md.

## Data and method

We read four existing CCHDO Exchange files in the shared dataset store. No new raw data download was needed. The exact shared paths, source URLs, byte counts, SHA-256 hashes and software versions are in files/provenance.json. The logical dataset directories are:

- datasets/cchdo-p02-2004-bottle-9184
- datasets/cchdo-p02-2013-bottle-29714
- datasets/cchdo-p02w-2022-bottle-45135
- datasets/cchdo-p02e-2022-bottle-45175

These paths resolve under /mnt/dell-data/shared_datasets on the HP SSD. We read the shared paths only. Data credit and external terms are in files/NOTICE_external_data.md. Raw data and derived cast tables are outside this publication.

1. Select bottle positions at 28-32 N, 150 E-120 W. Require oxygen and CTD salinity flag 2, finite temperature from -2 to 40 C, salinity from 20 to 40, oxygen from 0 to 500 micromol/kg, and pressure from 0 to 2500 dbar. Temperature has no flag field in the older files. Use TEOS-10 absolute salinity, conservative temperature and sigma0. Saturation is GSW O2sol at the local water properties, referenced to air equilibrium, not oxygen at in-situ pressure.
2. Sort each cast in pressure. Remove duplicate pressures and retain successively denser nodes. This drops inversions. Interpolate linearly in density with no extrapolation. Reject casts where any bracket within the target layer exceeds 250 dbar or 0.30 kg/m3. The nominal layer is 26.3-26.7. Narrow and broad tests use 26.4-26.6 and 26.2-26.8. A strict test uses 150 dbar and 0.20 kg/m3.
3. Integrate oxygen over pressure using hydrostatic mass per area, dm = 10000 dp/g, with dp in dbar and g from GSW at the mean layer pressure. Use one g per cast and layer. This small constant-g approximation avoids a fixed reference density. Piecewise-linear interpolation gives a trapezoid integral of concentration against pressure within each density segment. Stock is in mol/m2. This is a vertical column stock, not an area-integrated basin inventory.
4. Divide the layer into 0.01 kg/m3 slices and retain original bottle-density nodes inside each slice. For slice j, let M be mass per area and C be its mass-weighted oxygen concentration in mol/kg. The exact midpoint identity is:

   delta I_j = ((M1 + M0)/2)(C1 - C0) + ((C1 + C0)/2)(M1 - M0).

   Sum over slices. The first term measures oxygen change at fixed density. The second includes layer thickness and mass redistribution within the layer. Neither term isolates respiration, ventilation or water-type mix. The two terms sum to the measured stock change within numerical precision.
5. Average mass and stock across casts in two-degree longitude bins, then use stock/mass as the bin concentration for each slice. Compare only bins present in both occupations. Give bins equal weight. West is 150 E-180, central is 180-150 W, east is 150-120 W. Require at least five common bins. The west does not cover its full nominal range.
6. Use 3999 joint circular three-bin block draws, seed 110732, for conditional marginal 95% intervals. Draws use ordered common bins; gaps can make adjacent bin indices farther apart. These intervals describe sampled spatial variation. They do not include ocean variation between cruises, season effects or shared calibration errors. No multiple-test adjustment is applied.
7. Bound a uniform oxygen scale error of up to 1% independently in each occupation. For the fixed-density term the adverse bound is the sum of 0.01 times mean slice mass times the sum of the absolute endpoint concentrations. This is an assumed error envelope, not a guarantee. It excludes density error, additive error and depth-dependent bias.

## Results

All stock terms below are in mol/m2 for sigma0 26.3-26.7. Parentheses show conditional 95% intervals for total stock change. Fixed-density and mass terms are point estimates; their intervals are in files/results.csv.

| Region | Period | Common bins | Stock change | Fixed-density term | Mass term |
|---|---|---:|---:|---:|---:|
| West | 2004-2013 | 7 | -2.65 (-3.37, -1.88) | -1.42 | -1.23 |
| West | 2013-2022 | 7 | +1.51 (+0.02, +2.78) | +0.28 | +1.24 |
| Central | 2004-2013 | 15 | -0.54 (-1.59, +0.68) | -0.90 | +0.36 |
| Central | 2013-2022 | 15 | -2.28 (-3.31, -1.46) | -1.14 | -1.14 |
| Central | 2004-2022 | 15 | -2.82 (-3.32, -2.37) | -2.02 | -0.80 |
| East | 2004-2013 | 15 | +0.77 (-0.09, +1.56) | -0.08 | +0.84 |
| East | 2013-2022 | 15 | -1.27 (-2.23, -0.26) | -0.91 | -0.36 |
| East | 2004-2022 | 15 | -0.50 (-1.41, +0.38) | -0.96 | +0.46 |

The central 2004 stock was 31.01 mol/m2. The fixed-density loss has an interval of -2.68 to -1.47 mol/m2; the mass term has an interval of -1.12 to -0.50. The fixed-density share is 71.6%, with a separate conditional block interval of 57.7-83.4% (seed 32). The upper limit of the fixed-density loss remains negative, at -0.88 mol/m2, under the adverse 1% scale-error envelope. The total-stock scale-error bound is 0.59 mol/m2, also smaller than the magnitude of the unstressed upper limit. Mean layer-weighted oxygen fell by 11.83 micromol/kg, saturation rose by 1.62, and AOU rose by 13.45. A fall in saturation does not explain this sampled loss.

Across all 39 matched endpoint bins, stock fell by 1.50 mol/m2 (-2.30 to -0.69). The fixed-density term was -1.39 and the mass term was -0.12. This is a sampled-route mean with incomplete western support. It must not be multiplied by basin area as a basin inventory estimate.

The regional timing differs. In the west, most of the 2013-2022 stock rebound is in the mass term. The small positive fixed-density term does not establish oxygen recovery. In the east, mass gain offsets about 48% of the fixed-density endpoint loss. A single concentration or stock metric would miss this difference. The signs are compatible with delayed downstream loss, but three occupations cannot establish an eastward speed or prove transport from the winter outcrop.

## Checks and limitations

The bottle-salinity test gives a central 2004-2022 stock loss of 2.80 mol/m2 and a fixed-density term of -2.00, close to the CTD-salinity results. Narrow and broad density layers give central stock changes of -1.15 and -4.58 mol/m2. Their fixed-density terms are -0.99 and -3.04. These tests retain all 15 central bins and retain negative fixed-density changes under the 1% envelope.

Three-degree longitude bins give a central endpoint loss of 2.83 mol/m2 with a fixed-density term of -1.98 (70% of the loss). Halving the density step to 0.005 kg/m3 changes the central fixed-density term by only 0.00002 mol/m2. These checks support the accounting and the sign, but do not test unresolved bottle-profile curvature.

Holding all three occupations to the same 37 bins gives an endpoint route mean of -1.56 mol/m2, close to the pairwise result. The central result uses the same 15 bins in all three comparisons and is exactly additive in total stock across periods. Leaving out any one central bin gives an endpoint stock change between -2.97 and -2.69. Central mean latitude changes by 0.0013 degrees and the largest bin latitude change is 0.0096 degrees. Track latitude change is small there. Eastern latitude mismatch can reach 0.41 degrees in one bin and limits that regional result.

The strict bracket rule fails to provide central comparisons. Only two 2013 casts across the full track pass it. We therefore cannot validate the central result with closely spaced bottle brackets. The main rule allows unresolved curvature over as much as 250 dbar and 0.30 kg/m3. This is an important limitation. The original whole-layer split gave 72.2% rather than the slice result of 71.6% for the central share, but the narrow-slice method is the appropriate accounting rule.

Cruise months differ: July-August 2004, April-May 2013 and May-July 2022 for the retained nominal-layer casts. Seasonal oxygen and layer-thickness changes can affect the stock differences. A repeat route does not follow the same water parcels. Density errors, dropped inversions, mesoscale variability and calibration errors beyond the assumed envelope remain. Neither fixed density nor a null saturation change fixes temperature-salinity mix or preformed oxygen. We did not estimate oxygen use rates, nutrient ratios, transient-tracer ages or modelled transports. This study does not close the oxygen budget or explain the California model excess.

The result gives a finite-layer observation target for the outcrop mechanism: a model should reproduce both the central fixed-density stock loss and its mass contribution through 2022, while allowing a western mass rebound. Agreement on oxygen at one density surface alone is insufficient. The data support a persistent layer loss in the central section. They do not establish that outcrop loss caused 72% of it.

## Reproduction and provenance

Job: sci-1107-dell-earth-and-ocean-sciences-32e4707404a2. Campaign: 11_07_2026. Topic: earth-and-ocean-sciences. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. The configured campaign-machine key signs the publication; it is not a personal authorship claim. No private key is in this package.

Use Python 3.12 and install files/requirements.txt in a private virtual environment. Activate it, then run:

```bash
bash files/run_all.sh /path/to/datasets /path/to/local-reproduction
```

The second path must be separate from the signed publication. Code writes cast tables and intermediates there. To retrieve missing raw versions, run `python files/retrieve.py /path/to/external-raw`, then use that path as the dataset root. Retrieval checks every exact hash and stops if a version has changed. It does not write to the signed draft. Input files can be read in place from the shared store. Runs use one numerical thread and execute sequentially. No computation service is needed.

files/results.csv contains all main density-range and strict-gap results, including null results. files/bottle_salinity.csv, files/three_degree_bins.csv and files/half_density_step.csv give the later sensitivity runs. files/common_support.csv gives common-track and leave-one-out checks. files/fraction.json gives the share calculation. files/audit.json reports independent stock, mass and midpoint-identity checks. The maximum stock-slice error is about 1e-11 mol/m2 and the independent cross-product closure error is about 3e-12 mol/m2. The figure and aggregate files can be regenerated without campaign bundles. SCI citations provide the research context; no prior campaign code or data table is required to execute this analysis.
