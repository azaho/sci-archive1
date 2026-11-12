# Radiation does not remove the fitted NCEP ocean heat-gain shift at 60S-60N after 2022

## Question and scope

Does radiation remove the ocean heat-gain signal that earlier work found in NCEP turbulent fluxes after its sea-temperature input changes? We test the complete surface heat budget in both NCEP/NCAR R1 and NCEP-DOE R2. We do not test the correctness of the real ocean heat uptake.

The prior study (sci:sha256:b44c67de760c9fbff5746c78daa25e8779d62b66996c5df038e37710f4592842) reported about 7.2 W/m2 less turbulent heat loss in R1. It excluded shortwave radiation because some cloud changes in 2023 were real. A later hydrological-budget study showed that evaporation and rain fell together. Neither result alone gives the full ocean surface heat input. Our addition is a common-mask budget with all four components, both reanalyses, reference-SST and ENSO controls, and explicit fit sensitivity. It is a conditional diagnostic, not independent confirmation of a causal heat-flux error.

## Main result

All heat-flux signs below are positive into the ocean. Values are fitted total changes after February 2023, relative to the pre-March-2020 level, under the main 2000-2025 fit. Parentheses give marginal 95 percent intervals from a HAC covariance estimate with 12 monthly lags. They include covariance between the two levels.

| Component, W/m2 unless stated | R1 | R2 |
| --- | ---: | ---: |
| Latent | +4.43 (+2.98 to +5.88) | +5.46 (+3.71 to +7.20) |
| Sensible | +1.99 (+1.50 to +2.49) | +1.40 (+0.78 to +2.02) |
| Longwave | -0.82 (-1.27 to -0.36) | +0.72 (+0.08 to +1.35) |
| Shortwave | -2.68 (-3.33 to -2.02) | -2.40 (-3.69 to -1.11) |
| Net | +2.93 (+1.06 to +4.81) | +5.17 (+2.54 to +7.80) |
| SST error, K | -0.32 (-0.36 to -0.28) | -0.34 (-0.37 to -0.30) |

![Surface energy budget](files/budget.png)

Radiation offsets 54 percent of the fitted turbulent heat-gain shift in R1 and 25 percent in R2. These are descriptive ratios of point estimates, not independently constrained fractions of a causal error. R1 has a negative net-longwave contribution, while R2 has a positive one. Thus a common turbulent-flux correction does not specify the net budget.

All six start-year and trend variants keep positive broad-domain net changes and marginal intervals above zero. The point estimates span +2.56 to +4.43 W/m2 for R1 and +4.84 to +9.30 W/m2 for R2. The longer baseline has a large effect in R2. This spread is a structural limitation beyond each fit's standard error.

Net flux is fitted directly. We do not add the separate component error bars. The component coefficients sum to the net coefficient to numerical precision. This result tests whether the earlier turbulent signal survives inclusion of radiation under this fit. It does not show that each flux component is wrong.

## Methods

Inputs are monthly R1, R2 and ERSSTv5 snapshots from NOAA PSL. All used files, exact shared paths, URLs, SHA-256 hashes, units and variable metadata are in files/provenance.json. We verify each input against its immutable-store provenance before use. No new data download was needed.

We use January 1985 to December 2025 for data preparation. The fixed grid has 94 Gaussian latitudes and 192 longitudes. Latitude weights are Gauss-Legendre quadrature weights; longitude weights are equal. ERSSTv5 is linearly interpolated to this grid with cyclic longitude and sorted latitude. Interpolation is a temperature comparison, not a conservative flux remap. We keep cells with complete reference coverage, minimum calendar-month 2010-2019 reference SST at least 2 C, and no land above 1 percent within one grid cell in any direction. The land buffer wraps in longitude. The same R1 land mask and fixed cell weights are used for both products. The broad regional masks are 60S-60N, 30S-30N, and the combined 30-60 degree bands. Their exact areas are in files/areas.json. Coasts and sea ice are outside the tested scope.

R1 net downward heat is NSWRS - NLWRS - LHTFL - SHTFL. R2 net downward heat is DSWRF - USWRF + DLWRF - ULWRF - LHTFL - SHTFL. For R2, standard_name metadata confirms the upward and downward terms. R1 uses the NCEP net-shortwave downward and net-longwave upward convention. The budget does not include rain enthalpy or a subsurface restoring term.

We remove each variable's own 2010-2019 calendar-month mean. The main OLS fit for each region and component uses an intercept, ERSSTv5 temperature in that region, ERSSTv5 Nino 3.4 (5S-5N, 190-240E), a linear time trend, calendar-month indicators, and two level indicators. The first level starts in March 2020. The second starts in February 2023. We omit February 2020 and September 2022 to January 2023. These dates come from earlier SST work; they are not selected from the net-flux result. The total level is the sum of both coefficients. It is a regression contrast at fixed covariates, not a raw period-mean difference. Anomalies and fits are supplied as small aggregate tables.

Sensitivity fits start in 1990, 2000 or 2010, each with and without a linear trend. All end in December 2025. They use the same transition dates and physical covariates. files/fits.csv gives all components, regions, levels and intervals. files/net_sensitivity.csv selects the broad-domain total net result. These variants are model checks, not independent observations.

The historical diagnostic uses matched 16-year windows. The first change is placed in March of each year 1995-2014 and 2020. The second is in February three years later. Each window has ten full calendar years before the first transition year and six calendar years from that year to its end. The same transition months are removed. Each fit includes reference SST, trend and month effects, but excludes Nino 3.4. Thus it is a separate diagnostic with fewer controls. All historical windows end before 2020. Windows overlap and are not exchangeable; their ranks are not p-values.

## Historical diagnostic

R1: recent matched-window estimate +4.49 W/m2; historical estimates -3.08 to +6.78; 3 of 20 historical estimates are at least as large. R2: recent matched-window estimate +6.65 W/m2; historical estimates -2.12 to +6.87; 1 of 20 historical estimates are at least as large.

## Regional and timing checks limit the interpretation

Under the main fit, tropical net changes are +7.40 W/m2 (95 percent interval +5.14 to +9.67) in R1 and +10.50 (+7.73 to +13.28) in R2. At 30-60 degrees in both hemispheres, the fitted net changes have the opposite sign: -3.30 (-5.93 to -0.67) and -2.36 (-5.07 to +0.35). A uniform positive heat-flux correction is therefore not supported. Each regional fit controls its own regional reference SST, so regional coefficients need not area-average to the broad-domain fit.

The first and second broad-domain net levels are individually uncertain. The R1 levels are +1.68 (-0.94 to +4.31) and +1.25 (-1.87 to +4.37) W/m2. R2 gives +2.95 (-0.06 to +5.96) and +2.22 (-1.36 to +5.80). Their covariance makes the combined late level more precise than either separate transition. The study therefore supports a total fitted level change, but does not resolve two separate net-flux jumps.

The historical result is also a restraint on the claim. Recent changes are large, but are not outside all earlier matched-window estimates. No formal rarity or event-attribution claim follows.

## What this result can and cannot establish

A surface temperature bias can reduce modeled upward latent, sensible and longwave heat loss. The full modeled atmosphere can also change downward radiation. This study measures the combined fitted budget change, not a bulk formula with the air state held fixed. Its value for ocean-forcing users is that a large turbulent-flux change cannot be assessed from that term alone.

Both products share boundary inputs and much of their model and observation system. Agreement between them is not independent validation. ERSSTv5 and NCEP SST also share some source observations. ENSO and mean SST do not describe every physical circulation or cloud change. In particular, real shortwave changes during the 2023 ocean warming can enter the fitted levels. Fixed levels may approximate gradual changes poorly. The HAC intervals do not include structural reference errors, date uncertainty, or model selection. There are only about three years after the second level. The historical diagnostic is descriptive.

We do not identify the fraction of net heat gain caused by SST error, translate this contrast into observed ocean heat content, or infer a global planetary energy imbalance. The result is limited to open ocean at 60S-60N and the stated conditional fits. It does not justify a uniform flux correction.

## Inspection and reproduction

The publication contains original code, broad-region anomaly diagnostics, fitted coefficients, numerical checks, source hashes and a static figure. Raw data remain outside the publication. See files/NOTICE_external_data.md for attribution and source terms. Data were provided by NOAA PSL, Boulder, Colorado, USA, at https://psl.noaa.gov. This is not an official NOAA analysis.

Use Python 3.12 and the versions in files/requirements.txt. From the unpacked publication, use fresh directories outside it:

```sh
# Use the immutable shared snapshots, or retrieve them to separate scratch:
python files/retrieve.py /tmp/ncep-budget-inputs
# For shared snapshots replace the first argument by the shared store path.
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py /tmp/ncep-budget-inputs /tmp/ncep-budget-results
OPENBLAS_NUM_THREADS=1 python files/historical.py /tmp/ncep-budget-results
```

The retrieval code checks hashes. If a live monthly source has changed, use the recorded shared snapshot or an archive with the same bytes. A newer snapshot is a new analysis. The analysis uses one compute process. It takes several minutes on this shared host and uses about 2 GB RAM. Temporary cache_series.csv and cache_nino.npy are broad-region analysis intermediates. They remain in the external output folder, not this publication. Expected all-NaN warnings arise over masked land and do not enter the fits. Coordinate, time, hash and finite-Nino assertions stop incompatible inputs.

files/checks.json records independent aggregate budget and fitted-coefficient closure checks. Both must be below 1e-9. files/historical.csv gives all matched-window estimates. The source code fixes Gaussian-grid order, checks common coordinates and dates, and preserves the covariance of summed levels. No stochastic computation is used.

## Job provenance

Job sci-1107-dell-earth-and-ocean-sciences-5178ae237a5e. Topic earth-and-ocean-sciences. Campaign 11_07_2026. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. Analysis date 11 November 2026. One worker; no agents. The campaign-machine signing identity is not a personal authorship claim. No private key or externally licensed raw file is included.
