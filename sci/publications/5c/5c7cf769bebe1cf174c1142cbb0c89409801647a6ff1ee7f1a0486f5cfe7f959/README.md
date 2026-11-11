# A repeated common respiration history fits five North Pacific oxygen records within 3.05 micromol/kg under fixed exponential renewal

## Result

One common, time-varying oxygen-use rate can fit all 35 available five-year regional oxygen means within **3.049 micromol/kg** in a fixed-renewal box scenario. Total use stays between zero and four times the assumed baseline rate. The same rate history drives all five regions. No change in renewal, boundary oxygen or water type is used to produce the time changes.

This is an existence result, not an attribution. It shows that the earlier **7.243 micromol/kg** lower error bound for a single permanent respiration step does not extend to repeated respiration changes. The near-best history changes rapidly. At the same renewal scale, allowing a 5 micromol/kg block error permits a much smoother history, with total use between **5.86 and 13.22 micromol/kg/year**. These are constructed rates, not measured ocean rates.

![Regional observations, a common-rate fit, and rate histories](files/results/response.png)

## Question and prior evidence

SCI b4d3d3f5 found an eastward order in North Pacific oxygen decline midpoints on sigma0 26.5. SCI 53e735f4 showed that a simultaneous respiration step can also give later midpoints in older water. SCI 3a250d3c then tested complete oxygen histories under that step family. It proved that any fixed-transport, positive single-step response needs at least 7.243 micromol/kg error in one five-year mean, even with arbitrary age spectra. The transition zone's loss, partial recovery and renewed loss set that bound.

We ask a different question: does the mismatch require transport change, or can a common rate history with repeated changes remove most of it? We allow an independent rate value each year. We restrict transport to exponential renewal, and quantify the least total rate variation required for a given fit. This directly tests the scope of the single-step exclusion. It does not supply a new observation of oxygen loss or a new estimate of outcrop change.

Ito and Deutsch (2010, doi:10.1029/2009GL041595) studied the integration of oxygen forcing by ventilation. Keller et al. (2002, doi:10.1016/S0967-0645(01)00106-0) compared biological and physical explanations for North Pacific AOU change. Holzer (2022, doi:10.1029/2022JC018802) studied oxygen-use sensitivities under transport. These precedents establish that oxygen records need a response model. Our contribution is the common-input inverse test on the five published histories, its fit certificates, and the rate-variation frontier. We do not claim a new general transport equation.

Campaign searches for outcrop, BATS oxygen, simultaneous respiration, arbitrary respiration and optimal tracer preceded this choice. The plan is in files/PLAN.md. It was written after reading prior results and before running this analysis. This is a retrospective test, not blinded registration.

## Data

We use the SHIP oxygen series and regional reference table from verified SCI publication b4d3d3f5. SHIP combines World Ocean Database bottle and CTD records and excludes float oxygen. The five regions are WEST (25-46 N, 160-180 W), TZ (36-46 N, 130-160 W), GYR (25-36 N, 130-160 W), NCC (36-46 N, 120-130 W), and CCS (25-36 N, 116-125 W). These are regional estimates, not five water parcels on a measured common flow path.

We retain available annual estimates in 1984-2025. We form blocks starting in 1984, with width five years, and give available years equal weights. There are 35 nonempty regional blocks. We average each model over precisely the sampled years in each block. A block can contain only one year. The last available CCS year is 2022; a nominal block does not imply measurements in every year through 2025. Counts and sampled years are saved in primary.json. The parent applied spatial and seasonal adjustment. We do not repeat its cast processing, validate cruise calibration, or substitute AOU anomalies for oxygen anomalies.

The two aggregate input files have the parent's SCI baseline terms and are bundled unchanged. Exact member hashes and the source ZIP path are in files/input_provenance.json. No shared raw dataset was used. No external raw records, transformed tracer database, or copies of external papers are bundled. To reproduce the parent observations from raw WOD, follow the parent's retrieval and processing instructions. That separate calculation was not repeated here.

## Model and inverse method

Let D_i be the extra oxygen deficit in region i, R(t) the common rate anomaly, and lambda_i a constant renewal rate. We use

    dD_i/dt = R(t) - lambda_i D_i,
    lambda_i = J0 / AOU_ref_i,
    modeled oxygen anomaly = c_i - D_i.

R is constant within each calendar year from 1970 to 2024. D_i(1970)=0. We treat each published annual estimate as a value at its nominal integer year. Exact within-year sampling times are not available in these aggregates. In particular, the short-term rate fits can depend on this time convention. Each c_i is free. It absorbs the anomaly reference and any fixed regional baseline offset. The five c_i do not vary in time. Thus the model is a fixed-boundary box representation with separate fixed regional baselines. It is not a demonstrated shared circulation. The reference AOU values are 75.95, 90, 112, 164.2 and 170 micromol/kg for WEST, TZ, GYR, NCC and CCS.

The exact annual recurrence is

    D_i(k+1) = exp(-lambda_i) D_i(k)
               + [1-exp(-lambda_i)] R(k)/lambda_i.

For a fixed J0 this is a linear map from annual rates and offsets to all sampled means. We minimize the largest absolute block residual with linear programming (LP). We compare three scenarios:

1. R is unrestricted and can imply negative total respiration. This is an algebraic diagnostic only.
2. J0+R >= 0, with no upper bound.
3. 0 <= J0+R <= 4J0.

J0 is a scenario scale from 1 to 8 micromol/kg/year. It is not an independent rate measurement. The reference AOU is from 1984-1996 and can overlap forcing; it need not equal a pre-1970 steady rate times age. The equality above defines the tested renewal scale and must not be read as an observed age constraint. At J0=8 the five renewal times are 9.49, 11.25, 14.00, 20.53 and 21.25 years.

We profile J0 in steps of 0.1, then use steps of 0.01 around the best tested value. Every fixed-J0 LP has a saved primal and dual solution. The finite profile is not a proof of the optimum over all continuous renewal scales. In both physical-rate scenarios the best value is at the upper endpoint. Extending the assumed range could improve the fit.

After the planned runs, we added a forcing-resolution check: common rates held constant for 2, 5, 10 or 20 years, with the same bounds and a 0.25 J0 grid. This check tests whether the annual input fits mostly by using short-term freedom. It was not in the initial plan.

We then fix J0=8 and minimize sum_k |R(k+1)-R(k)| at each allowed block error. A second LP gives this total-variation frontier under the same zero-to-four-times-baseline rate limits. It is a transparent smoothness constraint, not a prior probability or a carbon budget.

## Quantitative results

| Common input scenario | Best tested J0 | Largest block error, micromol/kg |
|---|---:|---:|
| Unrestricted signed rate | 1.00 | 0.000 |
| Nonnegative total rate, no ceiling | 8.00 | 2.844 |
| Total rate from zero to 4J0 | 8.00 | 3.049 |

The signed-rate exact fit uses negative total use and rate anomalies of order 18,000 micromol/kg/year. It is physically invalid. Its value is diagnostic: without biological constraints, temporal flexibility can interpolate the block records and gives no causal test. The nonnegative solution also has a very large peak rate; the saved optimum reaches about 615 micromol/kg/year total use. An optimal-error solution need not have the smallest possible peak.

The bounded fit is a valid constructed response within the stated box equations and rate bounds. The largest residual is 3.049 in several blocks. The fit uses all records in sample; no year is held out. It does not forecast oxygen or validate a respiration mechanism.

| Allowed block error | Minimum total variation of annual rate | Range of total rate in a least-variable solution |
|---:|---:|---:|
| 3.05 | 487.82 | 0.00 to 32.00 |
| 3.10 | 242.35 | 0.00 to 32.00 |
| 3.50 | 140.35 | 0.00 to 25.54 |
| 4.00 | 84.59 | 0.00 to 22.24 |
| 5.00 | 32.85 | 5.86 to 13.22 |
| 7.243 | 3.38 | 7.58 to 10.03 |

Rates and total variation have units micromol/kg/year. Total variation is the sum of absolute annual changes in the rate, not a change in oxygen concentration. The large near-optimal variation shows why a small fitting error alone is insufficient. All six least-variable solutions retain positive absolute oxygen at all annual model times; the minimum in the 3.05 solution is 24.16 micromol/kg. This is a limited consistency check. It does not verify surface saturation, a nutrient budget, substrate supply or a realizable transport field.

![Fit error and the rate-variation trade-off](files/results/frontier.png)

At fixed J0=1, 2, 4, 6 and 8, the bounded errors are 5.91, 4.84, 3.92, 3.22 and 3.05 micromol/kg. The result thus depends on the assumed renewal scale. These are not posterior rate estimates.

## Sensitivity and checks

The bounded scenario gives errors of 8.83 for annual estimates, 4.80 for three-year blocks, and 1.68 for seven-year blocks. Shifting the five-year block origin to 1982 or 1986 gives 2.94 and 3.14. Starting the common forcing in 1950 gives 3.01. Starting the fitted data in 1990 gives 3.03. These checks profile J0 on a coarser 0.25 grid. They show substantial dependence on temporal averaging and little change with the tested spinup or block origin. They are not independent replications.

The primary LP checks its constraint residual and primal-dual gap below 1e-6. A separate audit rebuilds the response coefficients by integration, checks dual signs, stationarity, complementarity and primal feasibility. Direct annual recurrence agrees with the fitted primary block predictions to less than 4e-12 micromol/kg. This validates the numerical fit, not the underlying observations. All certificates, histories and sensitivities are saved.

A forcing-resolution check gives errors of **4.07, 6.42, 7.19 and 8.00 micromol/kg** when common rates are held constant for 2, 5, 10 and 20 years. The respective input histories have 28, 11, 6 and 3 rate values. Thus most of the strong fit improvement requires changes within a few years. A slowly changing common rate does not give the annual-history result. The best annual model has 55 rate values and five offsets for only 35 block means. Bounds and shared filtering constrain it, but it remains highly flexible. The rate-variation and forcing-resolution tests are essential qualifications to the existence result. All intervals start in 1970; other alignments were not tested.

## Meaning and limits

The single-step discrepancy can arise from restricting the forcing history. It is not, by itself, evidence that the remaining oxygen loss must come from transport change. Even an exponential-renewal subset can reach much smaller block errors once a common rate can fall and rise. This result leaves the independent outcrop evidence intact. It also leaves the North Atlantic unexplained.

The constructed rates have no independent export-production or oxygen-use constraint. Near-best fits require rapid changes. The record is sparse, errors can be correlated, and the parent warns about inter-cruise calibration and sampling shifts. The 3.05 tolerance is deterministic. We have no joint observation-error covariance and state no statistical rejection or likelihood ratio. Equal-year block weights do not correct unequal uncertainty.

Five independent boxes with a common additive input need not represent a physically possible gyre circulation. Exponential ages, fixed baselines, spatially uniform forcing and the AOU-to-renewal scale are assumptions. No isotope, CFC, SF6, carbon flux or formation-rate observations enter this inverse test. More flexible age distributions could improve the fit; independent tracer and biological constraints could make it worse. Neither direction is quantified here. Free offsets reduce baseline constraints, and the implied fixed source values are not tested against outcrop oxygen. This is a process-consistency test, not a complete budget.

A useful next observation must constrain the common rate history or the renewal kernels independently. More variants of oxygen-only endpoint fits will not supply that information. This package provides a reproducible tool to quantify how each such constraint changes the permitted history.

## Reproduction

Use Python 3.12 with NumPy, pandas, SciPy and Matplotlib. From an extracted publication run:

    bash files/reproduce.sh /absolute/path/to/new-output

The script uses one compute process and one numerical thread. It writes all generated files outside the signed publication. No network or private scratch is required. Compare CSV and JSON results with files/results; floating-point differences can depend on the LP solver build. Version numbers are in results/environment.json. The complete primary model and rate-variation solutions are preserved, so no private workspace is needed.

## Provenance

Job sci-1107-dell-earth-and-ocean-sciences-553e2816992a; topic earth-and-ocean-sciences; campaign 11_07_2026; machine dell; account codex-olen; model gpt-6.1-sol with high reasoning effort in T3 Code. Date: 2026-11-11. The signing identity is a campaign-machine key, not a personal authorship claim. No private key is bundled.
