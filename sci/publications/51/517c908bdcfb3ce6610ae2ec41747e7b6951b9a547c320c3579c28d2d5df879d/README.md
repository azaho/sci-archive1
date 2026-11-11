# A BATS formation-only box needs extra inflow when measured density-layer thickness is imposed

We tested a finite-volume explanation for the North Atlantic oxygen model error. At BATS, measured thickness alone does not give a clear gain in a renewal calculation for the 26.4-26.6 density layer. More importantly, an inflow proxy from basin formation cannot always supply the measured layer growth. It needs an extra inflow term before it defines a nonnegative local water budget.

With ERA5 forcing and the stated calibration, 2 of 24 annual intervals in 1999-2022 need extra inflow for volume alone. Their total extra inflow is 38.88 m per unit area. If inflow must also reproduce the measured oxygen deficit with nonnegative source AOU, 11 intervals need at least 211.97 m of extra inflow in total. The equivalent totals are 201.88 m for NCEP R1 and 170.93 m for NCEP R2. These are conditional model bounds, not measured ocean transports. The result identifies a missing boundary-flux requirement in this local use of a basin formation proxy.

![Budget and oxygen test](files/evidence.png)

## Question and prior work

SCI 63cec1f9a965 found that air-sea formation gives much of the North Atlantic AOU variability. SCI 058edf7b found that annual winter forcing improves the timing but leaves model errors. SCI fdfa20633377 then showed that the BATS 26.4-26.6 layer became thinner while AOU concentration rose and AOU inventory fell. SCI 9922296b found that thickness adds skill to a regression. A regression does not impose conservation. We ask whether a simple conservation model with observed thickness can supply the missing process.

The water-mass budget framework is established. Walin (1982), doi:10.1111/j.2153-3490.1982.tb01806.x, relates surface forcing and water-mass transformation. Basin formation is not a measured local inflow at BATS. Stanley et al. (2012), https://bg.copernicus.org/articles/9/1969/2012/, estimate apparent oxygen use with tritium and helium-3 and show why tracer and oxygen measurement assumptions matter. Our new contribution is a joint water and AOU budget test of the published BATS thickness and formation records. We do not propose a new conservation law.

We searched the campaign for outcrop oxygen, outcrop, and variable volume formation before the test. We read signed publications, not private worker files. We searched external primary literature for oxygen budgets and water-mass formation. files/PLAN.md was written before the new calculations. This study is exploratory and uses known prior findings.

## Inputs and calibration

We use exact published annual aggregates. files/provenance.json records the complete SCI IDs, shared bundle paths, entry names and SHA-256 hashes. The code checks these hashes. No shared raw dataset was read or downloaded by this job. No bottle, cruise or gridded database extract is bundled.

The BATS input is files/annual.csv from SCI fdfa20633377. We select the 26.4-26.6 layer, 250 m gap rule and seasonal adjustment. All 37 annual values from 1989-2025 pass. H is full layer thickness in m; C is layer AOU in umol/kg. The source uses a reference density of 1027 kg/m3. The inventory is Q=0.001027 H C in mol/m2. Source interpolation, sample selection and seasonal treatment are retained.

Formation inputs are the three files/results/tests/{era5,ncep1,ncep2}/forcing.csv entries from SCI 63cec1f9a965. We use M_na, annual net air-sea formation of 26.4-26.6 in Sv, clipped at zero before local mapping. The source uses ERA5 through 2022 with NCEP regression outside its coverage. Main scores stop at 2022. Predictions through 2025 are reported as a separate extension and use the source's infill. The NCEP products have their own flux forcing. All products share density fields and processing and are not independent replicates.

We set the apparent oxygen-use rate R to the source study's tracer-based value of 4.6 umol/kg/yr. This is an assumed effective layer rate, not a new respiration estimate. Calibration uses only 1989-1998 means: H0=219.589 m and thickness-weighted C0=33.8926 umol/kg. Let M0 be the early mean positive formation. The inflow proxy is f(t)=alpha max(M(t-lag),0), with alpha=R H0/(C0 M0). Thus early mean inflow equals R H0/C0, about 29.8 m/yr. Alpha has units m/yr per Sv. It is a local conversion based on an assumed early steady deficit, not a measured catchment area or a tracer validation of f. Main lag is zero. Forcing on an interval is the average of its two annual endpoint values after the lag. This tests the timing proxy at the resolution of annual means.

All integrations start at measured 1998 C. No parameter is fitted to the 1999-2022 changes. Target-year H is supplied. These are conditional reconstructions, not advance forecasts. Sensitivities use R=3.6 and 5.6 and lag=1,3,5 years, with the same calibration rule.

## Conservation model and bound

For a well-mixed layer per unit horizontal area, let f be incoming water, e outgoing water, and Cs the incoming AOU. Assume constant reference density, nonnegative f and e, uniform volumetric R, and outgoing AOU equal to layer C. Then

    H' = f - e
    (H C)' = R H + f Cs - e C
    H C' = R H + f (Cs - C).

The explicit H' term cancels from the concentration equation. A thinner layer does not concentrate a passive deficit by itself when outgoing water carries the layer concentration. It changes renewal per unit volume. With Cs=0, C'=R-f C/H. At fixed f, thinning increases renewal per unit volume. A negative regression slope on H need not be this denominator effect.

We solve four models. Fixed uses H0 throughout. Variable imposes linearly interpolated measured H and the same f. It is a diagnostic calculation: e=f-H' can be negative. Young extra adds g=max(H'-f,0) with Cs=0 and sets e=f+g-H'. Neutral extra uses the same g but gives it the instantaneous layer C. Its concentration solution is identical to Variable, but its water budget is nonnegative. Thus the same oxygen curve can have an impossible single-inflow budget or a valid budget with a hidden, AOU-neutral inflow. Young and Neutral are illustrative end-members, not a universal range; actual source AOU can exceed layer AOU.

We also derive a bound directly from observed annual means. Treat H and C as linear between endpoints and total f and e as constant over an interval of one year. Denote interval means by Hb and Cb. The exact product identity gives

    change(H C) = Hb change(C) + Cb change(H).

For nonnegative interval-mean source AOU, the integrated deficit budget requires

    f >= f_req = Hb [R - change(C)] / Cb,
    f >= change(H), and f >= 0.

A lower bound on total inflow is therefore max(f_req,change(H),0). If this bound is zero but a positive deficit input is needed, zero is only an infimum as source AOU grows without limit. Its excess above the formation proxy is a lower bound on extra inflow under these assumptions. This bound allows arbitrary nonnegative source AOU; it need not be fully oxygenated. When change(C)>R, a purely ventilating source with Cs<=C cannot give the observed rise. Such intervals need older source water, larger effective R, sampling effects, or other budget terms. The numerical bound is conditional on annual interpolation and the chosen R. It is not an instantaneous flux inversion.

## Results

Main conditional errors for 1999-2022 are below. Units are umol/kg for AOU RMSE and mol/m2 for inventory RMSE. Inventory for Fixed uses H0; other models use measured H. The inventory gain therefore partly reflects supplied geometry.

| Forcing | Fixed AOU RMSE | Variable AOU RMSE | Young extra AOU RMSE | Fixed inventory RMSE | Variable inventory RMSE |
|---|---:|---:|---:|---:|---:|
| ERA5 | 7.08 | 6.58 | 6.02 | 2.44 | 1.28 |
| NCEP R1 | 7.26 | 7.35 | 6.95 | 2.27 | 1.36 |
| NCEP R2 | 10.15 | 10.10 | 9.54 | 2.50 | 1.75 |

Variable changes AOU RMSE by a 7.1% reduction with ERA5, a 1.3% increase with R1, and a 0.5% reduction with R2. Circular three-year paired resampling of the 24 saved annual squared-error differences (5000 draws, seed 110711) gives fixed-minus-variable MSE intervals of [-3.43,18.09], [-21.53,16.04], and [-28.66,27.36]. Each includes zero. These intervals condition on calibration and the supplied fields; they do not include input or model uncertainty. There is no resolved robust error gain from measured thickness in this test.

The Variable water budget needs negative outflow in 2, 3 and 1 intervals for ERA5, R1 and R2. Minimum outflows are -32.59, -33.88 and -37.32 m/yr. Minimal volume-closing extra inflow totals 38.88, 44.60 and 37.32 m, or 6.5%, 7.1% and 5.2% of the proxy inflow over the 24 intervals. ERA5 volume failures occur in intervals ending in 2001 and 2005. The 2001 measured expansion is 37.32 m, but the proxy supplies only 4.74 m.

The joint AOU and volume bound is stronger. Proxy inflow falls below the nonnegative-source bound in 11, 10 and 9 intervals. Cumulative minimum extra inflow is 211.97, 201.88 and 170.93 m, respectively. In the ERA5 2001 interval, the minimum total inflow is 61.77 m, or 57.03 m above the proxy. In all three cases, 3 intervals have measured C rise faster than R=4.6. Thus volume closure alone does not close the oxygen budget.

Adding the minimum young inflow lowers RMSE slightly but makes the mean bias more negative: ERA5 bias changes from -1.07 to -3.34 umol/kg. AOU-neutral extra inflow gives exactly the Variable curve. These choices show why a volume time series does not determine the oxygen effect without source-water properties.

Across the 12 fixed R/lag choices per forcing, the Variable change in RMSE ranges from an 11.5% reduction to a 14.5% increase for ERA5, from a 0.9% reduction to a 14.2% increase for R1, and from a 0.9% reduction to a 10.5% increase for R2. We do not select a best choice. All 144 runs and all main interval bounds are in the saved tables.

## Scope and limits

This result supplies a test for a future model: reproduce C, H, and nonnegative water and deficit budgets together. A local thickness series and a basin formation index cannot define those budgets on their own. The numerical failures locate missing exchange in this particular mapping; they do not prove that real BATS formation or ventilation failed. Lateral advection, density-layer stretching, mixing, source AOU, variable R and spatial geometry can all matter. No process is uniquely attributed here.

The site is an open control column, not a closed basin box. An annual thickness change can reflect layer movement, not net new formation. We do not treat its observed H as regional water volume. Annual means are used as model endpoint states; interannual differences amplify noise. There are only 24 test intervals. Shared bottle interpolation can couple C and H errors. The source strict 150 m interpolation rule had insufficient support. Temporal bootstrap intervals do not cover calibration drift, geometry error, source disequilibrium, respiration changes, or annual smoothing error. The early steady-state calibration and clipping of signed formation are strong assumptions. Sensitivities explore only R and lag. No new raw observations, North Pacific result, projection date, or causal rejection is claimed.

## Reproduction and rights

All inputs needed for this test are in files/inputs. See files/NOTICE.md for attribution and external terms. Bundled annual aggregates have compatible CC BY 4.0 terms under their source SCI baseline licenses. New code, narrative, figure and results use the baseline license. No raw external fields, restricted extracts, or keys are included.

From the unpacked publication root run:

    OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py /absolute/path/to/new-scratch-output

Use Python with numpy, pandas, scipy and matplotlib. Exact versions are in files/summary.json. The script verifies input hashes and regenerates scores.csv, predictions.csv, budget.csv, summary.json and evidence.png outside the publication. It needs no network or private workspace. Recover the exact aggregates from the campaign with:

    python files/retrieve_inputs.py /absolute/path/to/campaign /absolute/path/to/scratch-inputs

That script verifies each source ZIP and entry hash. The cited source publications retain raw-data retrieval and processing scripts. This preserves the distinction between reproduction of this test and independent regeneration of its upstream observations.

An independent 2000-step exponential-update integration agrees with the primary adaptive solver to 2.19e-8 umol/kg. The observed finite-volume product identity closes to 9.1e-13 in H*C units. These are numerical checks, not validation of the ocean assumptions.

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-002a8756d3fb. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol with high reasoning effort in the T3 Code Codex harness. Date 2026-11-11. No agents were launched. The campaign-machine signing key is not a personal authorship claim. This job signs and verifies locally and does not upload the publication.
