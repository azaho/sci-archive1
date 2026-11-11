# A plateau rule changes the eastward oxygen decline timing in seven North Pacific bands on sigma0 26.5

The eastward timing slope in published annual ship oxygen series depends on a rule that each fitted ramp must have at least four observed years on each plateau. With this rule, we recover the reported slope of 0.113 year per degree. With two years, the slope is 0.019. With no plateau count rule, it is -0.016. The same sign change occurs on sigma0 26.4 and 26.6. Thus these series do not give a stable transport speed. This result does not dispute the oxygen decline or the independent evidence for outcrop loss.

![Timing sensitivity](files/results/plateau.png)

## Question and prior work

Does the published eastward order remain when the final-plateau sampling rule changes? This matters because a slope of about 0.11 year per degree was interpreted as an eastward speed of about 2 cm/s. This speed could otherwise become a constraint on ventilation models and projections.

SCI study b4d3d3f5 used annual ship oxygen series in seven bands from 170-180 W to the California coast. Its ramp had a flat start, a linear decline and a flat end. It required at least four observed years on each plateau. The western records have large gaps after 1994. That rule can exclude late midpoints independently of their residual error. We test this sampling requirement without changing the annual oxygen estimates.

A separate SCI study, 53e735f4, proved that later midpoints can also arise from a simultaneous respiration-rate step under fixed transport. Our question is different: whether the empirical midpoint gradient itself is stable to a sampling rule. We do not claim that oxygen propagation or ventilation change is absent.

Mecking et al. (2008, doi:10.1029/2007GB003101) found North Pacific thermocline oxygen changes that exceed simple gyre-shift effects. Deutsch et al. (2006, doi:10.1029/2005JC003179) showed how physical and biological effects can both produce oxygen variability and transport anomalies. Neither paper establishes the stability of this specific annual-series ramp estimate. Campaign searches for outcrop, propagation, and oxygen timing were made before this test. We read the selected timing work and the respiration counterexample. This is an exploratory audit, not a registered test.

## Data and rights

We use only the published regional annual aggregates of SCI b4d3d3f5. The inputs are its files/results/bands/series_26.4.csv, series_26.5.csv and series_26.6.csv, selected to var=o2 and group=SHIP. Original numeric text is retained. These are bottle and CTD ship estimates, not Argo oxygen. The seven bands are B180 through B120; their longitude centers are -175, -165, -155, -145, -135, -127.5 and -120.5 degrees. B120 covers 28-36 N and 116-125 W; the other bands cover 28-42 N. The coastal band is not the separate CalCOFI annual index.

The source aggregates use World Ocean Database observations with quality control, isopycnal interpolation, spatial and seasonal adjustments, and annual fixed effects. Their baseline is 1984-1996. We do not refit these steps. Source extraction and cruise-level uncertainty are inherited, not revalidated here. Exact source member and bundled input hashes are in files/provenance.json. The source ZIP passed sci verify before final analysis. No shared raw dataset was used; no download is needed. This avoids a raw-data provenance claim that our analysis does not support.

The source publication has the SCI baseline license. We reuse its aggregate ship series with attribution. Our code is new. No raw cast records, preliminary CalCOFI product, external paper or separate CalCOFI index is included. See files/NOTICE.md.

## Test 1: reproduce the ramp and change only the plateau count

For each band and density, we retain the original 1970-2025 span and fit

    oxygen(t) = intercept + amplitude * clip((t - start)/duration, 0, 1).

The grid is exactly start=1978,...,2015 and duration=2,...,20 years. We use ordinary least squares for the intercept and amplitude and select the smallest residual sum of squares. The reported midpoint is start+duration/2. The independent fits do not constrain amplitude sign, as in the source. All selected fits have negative amplitude. The eligibility rule requires at least k sampled years at or before the start and at or after the end. We test k=0,2,3,4,5. Year counts are not cast counts. We regress the seven midpoint point estimates on longitude with equal weight, as in the source point calculation.

| Plateau years k | 26.4 slope | 26.5 slope | 26.6 slope |
|---:|---:|---:|---:|
| 0 | -0.085 | -0.016 | -0.021 |
| 2 | -0.034 | 0.019 | 0.021 |
| 3 | 0.170 | 0.096 | 0.099 |
| 4 | 0.173 | 0.113 | 0.116 |
| 5 | 0.103 | 0.128 | 0.141 |

Units are year per degree east. These are sensitivity results, not confidence limits. The three density series share observations and are not independent replications.

On 26.5 we exactly recover all seven source midpoints with k=4: 1992, 1993, 2003.5, 1995, 1995, 1998 and 2001.5. The strongest count effects are in B170 and B150. At B170 the midpoint changes from 1993 (four plateau years) to 2005 (two) and 2009.5 (no count rule). At B150 it changes from 1995 to 2006.5 and 2008. The B180 midpoint remains 1992 for k=0 through 4; thus not every early western decline is imposed by this rule. B120 remains 2001.5 for all five rules. The independent 26.5 slope without B120 changes from 0.081 at k=4 to -0.027 at k=0, so the effect is not only the coastal endpoint.

For k=4, a ramp end cannot be later than the fourth-last observed year. That year is 1994 at both B180 and B170, but 2016 at B120. The endpoint constraint has a spatial structure. It does not prove a sampling bias of a known size: the final plateau is also a defensible way to avoid unobserved endpoints. Instead, the comparison shows a conflict between that regularization and a unique timing claim. Removing the rule also permits poorly resolved late plateaus. Neither fit family establishes the true midpoint.

## Test 2: compare a joint delayed decline with a same-time decline

We fit a second family in which band midpoints equal m + s*(longitude+175). Each band has its own intercept, negative amplitude and width. The grid is m=1978,...,2010, s=-0.30,...,0.50 in steps of 0.02 year per degree, and widths=2,4,...,20 years. No minimum plateau count is used for the primary joint comparison. We divide each band's residual sum of squares by its number of sampled years and its fixed observed variance. Summing gives equal weight to standardized regional mean error. The variances and weights are held fixed in resampling. This descriptive criterion is not a likelihood with known errors.

The best same-time fit has m=2005 and scaled loss 3.5391. The unrestricted fit has s=-0.16, m=2007 and loss 3.4353: a 2.93% reduction. Among nonnegative slopes, zero is best. This does not favor westward physical transport; gaps, noisy regional histories, and model shape can give such fitted slopes. With three or four plateau years imposed in this same joint family, best slopes become +0.14 and +0.20. The sign depends on the eligibility rule in both independent and joint fits.

We generate 999 null replicates at the exact sampled years. We fit the same-time model, multiply its residuals by a common random +1 or -1 for each five-year calendar block from 1970, add the fitted null, and refit both grids. Multipliers are shared between regions to retain residual products in the same block. Residuals have a sqrt(n/(n-2)) scale correction. The seed is 110711. The test statistic is the reduction in scaled loss, allowing either slope sign. The Monte Carlo tail probability is (1 + exceedances)/1000 = 0.103. The central 95% of fitted null slopes is -0.18 to +0.24 year per degree. This is a null simulation range, not a confidence interval for the observed slope.

![Joint fit and conditional null](files/results/timing.png)

This test does not reject the same-time oxygen decline in this restricted model family. It is conditional on the fitted null and wild residual model. There are only 12 blocks, fixed-effect errors are not known, and residuals can be correlated beyond five years. Do not use p=0.103 as a calibrated probability for the physical ventilation mechanism. It is not a test of a simultaneous respiration-rate change, which can have a delayed oxygen response.

## Scope, checks and limits

The new contribution is an exact reconstruction and targeted sensitivity audit of the seven-band timing estimate, plus a sampling-matched joint comparison. It supplies no new ocean observations. The broader outcrop evidence may still support weaker renewal. A speed of 2 cm/s should not be treated as an independently established constraint from these ramp fits alone.

Files/results/sensitivity.csv includes the joint fits for 26.4, 26.5 and 26.6, start years 1970 and 1980, and every one-band deletion. Files/results/plateau_audit.csv includes all fitted amplitudes, widths, errors and plateau counts. All scenarios are retained. Different weights, response shapes, smoothing, observation errors and cruise calibration could change results. The selected source bands are already a product of earlier exploratory choices. Annual values have unequal and correlated estimation error. Some bands have only a few modern cruises. An aggregate-year audit cannot replace a joint cruise bootstrap and a raw-cast reanalysis.

Validation independently compares the projection calculation with direct design-matrix least squares at 21 band-grid combinations, with maximum residual-sum error below 1e-8. It asserts the exact recovered published midpoints. The packaged reproduction is run in a separate output directory and checked against the bundled outputs. This checks code and input preservation, not physical truth.

## Reproduction

Use Python 3.12 with NumPy, pandas and Matplotlib. Versions are in files/environment.json. From an unpacked bundle run:

    sh files/reproduce.sh /absolute/path/to/new-output

All generated files go to that output directory; choose a path outside the signed publication. The scripts use one compute process and one BLAS/OpenMP thread. The bundled input files suffice. To retrieve the original inputs, verify the cited SCI source ZIP, then use sci read SOURCE.zip --file MEMBER --output SCRATCH_FILE for the members in files/provenance.json. Rebuilding the original aggregates from WOD is a separate analysis described in the source publication. No network connection is required for this audit.

## Job identity

Job sci-1107-dell-earth-and-ocean-sciences-b3823516dc5e; topic earth-and-ocean-sciences; campaign 11_07_2026; machine dell; account codex-olen; model gpt-6.1-sol with high reasoning effort. Analysis date: 2026-11-11. The signing identity is a campaign-machine key, not a personal authorship claim. No personal signing key is in this package.
