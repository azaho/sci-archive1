# The fitted MPI–CNRM radiation-slope contrast lies in shortwave cloud radiative effect in 1980–2014

Job: sci-1107-dell-earth-and-ocean-sciences-b1a06623c7ba. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-11, America/Los_Angeles. The signing identity is a campaign-machine key. It is not a personal authorship claim.

## Question

Why do fitted radiation responses to SST dataset differences vary across atmosphere models? A prior study (SCI 96a66d04) compared AMIP and HighResMIP runs. It found annual radiation slopes of 1.2–3.9 relative to a five-model Green's-function prediction. This has consequences for estimates of the effect of SST input steps on radiation. Here we separate the fitted slopes into clear-sky radiation and cloud radiative effect (CRE). We then separate each term into shortwave (SW) and longwave (LW) radiation.

The new result is a component and uncertainty test of the **spread across models**, not a new estimate of the mean response or of an SST step. The largest fitted net contrast in the source study was MPI-ESM1-2-HR minus CNRM-CM6-1-HR. We test that contrast with a common predictor and common years. The fitted contrast lies in SW CRE. However, selection-adjusted limits and a shorter record do not establish a clear contrast. This identifies a useful diagnostic for controlled model tests. It does not establish a cloud feedback mechanism.

## Results

![Radiation slope components](files/decomposition.png)

All slopes below use annual means, 1980–2014, a cubic time control, and a fitted sea-ice term. The SST predictor is the equal-pair mean of the five-Green's-function net predictions. Each model has its own fitted coefficients. The units are dimensionless: radiation and its prediction both use W m-2.

| Pair | Net slope | Clear-sky slope | CRE slope | SW CRE slope |
|---|---:|---:|---:|---:|
| CNRM-CM6-1 | 1.450 | 0.759 | 0.692 | 0.481 |
| CNRM-CM6-1-HR | 1.175 | 1.206 | -0.031 | 0.102 |
| GFDL-AM4/CM4C192 | 1.689 | 1.034 | 0.655 | 0.439 |
| HadGEM3-GC31-LL/LM | 2.753 | 2.080 | 0.673 | -0.149 |
| HadGEM3-GC31-MM | 1.882 | 1.336 | 0.546 | 0.152 |
| IPSL-CM6A-LR | 2.597 | 1.174 | 1.422 | 1.230 |
| MPI-ESM1-2-HR | 3.753 | 1.199 | 2.554 | 2.684 |

The MPI-minus-CNRM-HR contrast is **2.578** in net radiation. Its clear-sky component is **-0.008**, its CRE component is **2.585**, and its SW CRE component is **2.582**. LW CRE contributes only **0.003**. Thus almost all of the fitted endpoint contrast is in SW CRE. This is an exact decomposition of fitted associations; it is not a partition of Green's-function error.

Conditional 95% residual-block intervals, with three-year blocks and 4,000 draws, are:

| Contrast component | Estimate | Lower limit | Upper limit |
|---|---:|---:|---:|
| Net | 2.578 | -0.431 | 5.916 |
| Clear sky | -0.008 | -3.438 | 3.778 |
| CRE | 2.585 | 0.683 | 4.358 |
| SW CRE | 2.582 | 0.531 | 4.529 |
| LW CRE | 0.003 | -0.971 | 0.994 |

The net contrast is less precise than the CRE contrast. Large clear-sky noise adds uncertainty. An unresolved clear-sky contrast does not prove that clear-sky responses are equal.

**Selection limits the evidence.** The endpoints were selected by their net slopes in the source study. Simultaneous 95% intervals over all 21 pair contrasts include zero: -0.169 to 5.340 for CRE and -0.344 to 5.507 for SW CRE. These adjust for pair selection within a component, not for all analysis choices. An equal-slope null test over all seven pairs gives a probability of 0.030 for SW CRE, 0.078 for net CRE, 0.303 for net radiation, and 0.836 for clear sky. The SW CRE probability is exploratory and is not corrected for the nine radiation components. It is not a confirmatory rejection.

Across all seven fitted net slopes, CRE supplies 82.5% of their covariance-based dispersion. The share is cov(net slope, CRE slope) / var(net slope), with pairs weighted equally. The complementary clear-sky share is 17.5%. Averaging the two CNRM and two HadGEM pairs before this calculation gives a CRE share of 91.2% across five families. But the three-year interval for the seven-pair share is -4.9% to 112.5%. The family interval is -5.1% to 162.1%. A covariance share can be below zero or above one. These wide limits do not establish how physical model spread is partitioned.

![Marginal and simultaneous contrast intervals](files/contrast.png)

## Sensitivity

One- and five-year blocks retain positive marginal MPI-minus-CNRM-HR CRE and SW CRE intervals. The simultaneous intervals still include zero. Constant, linear and cubic time controls, with or without volcanic years and with common or pair-specific predictors, give descriptive CRE dispersion shares of 66.6%–92.6%. These are sensitivity fits, not independent confirmations.

A control for the November 1981 SST splice uses an annual step with value 0 before 1981, 2/12 in 1981 and 1 thereafter. All coefficients are refitted. The net contrast falls to 1.382. The CRE contrast remains 2.478 (0.421–4.366), and SW CRE remains 2.431 (0.162–4.489). Thus, in this fit, a single early step does not account for all of the CRE slope contrast. The step control can remove real SST response as well as an input artifact. Only two early years constrain its pre-step level.

Excluding 1982–1984 and 1991–1993 gives a CRE contrast of 2.604 (0.812–4.272) and SW CRE of 2.552 (0.613–4.425). Starting instead in 1985 gives CRE 2.331 (-0.182 to 4.860) and SW CRE 2.657 (-0.176 to 5.275). The shorter record therefore retains the point contrast but does not resolve it. These intervals are marginal and conditional on fixed predictors. In the volcanic exclusion, block adjacency follows retained years and crosses calendar gaps.

## Data and method

The only numerical input is the verified aggregate table `files/data/pair_series_monthly.csv.gz` in SCI publication `sha256:96a66d04c75df7c97e71eb3d97a5d79e109a0c0d3eed2d9aa855cd062c8ca119`. It has 3,024 monthly rows and 21 columns. We retain accepted months, restrict to 1980–2014, and form equal-month annual means. Every retained pair-year has 12 months. No new model fields or observations are used. No raw dataset under `./datasets` is used.

Let N be the source net downward radiation difference, and C its clear-sky difference. Define CRE = N - C. Define LW clear sky = C - SW clear sky; define SW CRE and LW CRE by subtraction from their all-sky components. The source uses negative outgoing SW plus LW for N. It assumes the incoming solar term cancels between experiments. We retain that assumption and do not independently check incoming solar radiation. In CRE the incoming term cancels within each experiment.

For each pair and component y, fit by least squares:

    y = c0 + c1 t + c2 t^2 + c3 t^3 + b_ice I + a g + error.

Here t spans -1 to 1 in 1980–2014. I is the mean sea-ice predictor across pairs. g is the mean five-function net SST prediction across pairs. The functions are CAM5, CanESM5, ECHAM6, GFDL-AM4 and HadAM3. They cover ice-free SST at 60 S–60 N. Common g and I make the component and pair comparisons use the same design. A pair-specific predictor check changes individual component slopes by at most 0.225. Net = clear + CRE slope identities hold within 1.3e-15. An independent partial-regression formula agrees with joint least squares within 2.9e-14. Source net and SW+LW values agree within 5e-6 W m-2, from saved rounding.

For uncertainty, keep the design fixed. Resample the fitted multivariate annual residuals in circular blocks of one, three or five years. Use the same indices for all pairs and components. Multiply residuals by sqrt(n/(n-p)) for a residual degrees-of-freedom adjustment. Add them to the fitted series and refit. Use 4,000 draws per block, seed 1107. Report marginal percentile intervals. This retains cross-pair and cross-component residual dependence. It assumes that residual blocks can move in time. It does not include SST predictor error, uncertainty in the source reduction, uncertainty in model selection, or full climate uncertainty.

The equal-slope test compares sum of squared centered fitted slopes with the distribution from centered bootstrap slope errors. This is the fixed-design equal-slope null: pair-specific time and ice terms remain free. The simultaneous contrast interval uses the 95th percentile of the maximum absolute standardized bootstrap error over 21 pair contrasts. It controls pair selection within each channel under the resampling model. It does not make the selected analysis confirmatory.

## Prior work and meaning

The GFMIP protocol (doi:10.1029/2023MS003700) describes the linear spatial response method. HighResMIP (doi:10.5194/gmd-9-4185-2016) uses a distinct experiment protocol. SCI 96a66d04 established the model-pair comparison. SCI 27de4f26 tested temporal transfer and found uncertain calibration. SCI 7c2b5a42 found a past, cloud-linked radiation signal. SCI e3cb4abe found an early SW cloud step in a different, controlled ECHAM6.3 experiment. We do not repeat those timing, transfer or step estimates. We test the across-model component spread and its uncertainty. Campaign searches for SST, Green functions, and cloud/clear-sky terms preceded this final scope. The analysis is exploratory, and the splice sensitivity was added after reading the later step study.

CRE is not cloud feedback. It includes cloud masking of temperature, water vapor, albedo and forcing effects (Soden et al., 2008, doi:10.1175/2007JCLI2110.1). There is no clear-sky Green's-function prediction in the input table. We therefore cannot assign the Green's-function error to clouds. Nor can these regressions show which SST dataset is correct. The source experiments differ in daily versus monthly SST, sea ice, external forcing, initial state and, for some pairs, model version or resolution. These differences can affect CRE as well as clear sky. Some pairs are related, and single HighResMIP runs carry internal variability. The apparent component spread can contain noise.

The practical result is a narrower model-test target: compare SW CRE under identical atmospheric forcing and configuration, with raw and corrected SST and multiple members, especially in MPI and CNRM-HR. The point evidence places their fitted difference there. The present data do not justify a universal multiplier for an SST artifact, a climate-sensitivity estimate, or a causal claim about cloud change.

## Reproduce

Use Python 3.12, NumPy, pandas and Matplotlib. Set numerical library threads to one. First obtain and verify the source ZIP with SCI. The exact shared archive used is `/mnt/dell-data/campaigns/11_07_2026/96a66d04c75df7c97e71eb3d97a5d79e109a0c0d3eed2d9aa855cd062c8ca119.zip`, accessed through `./campaign`. Its file hash and the entry hash are in `files/audit.json`. The input entry SHA-256 is `94ba20761c0ff3ea514a739063984188233401bb496a2630e26b2a78f8d90e6e`. Source store versions, original URLs, reduction code and rights notices remain in the cited signed publication. This package does not rely on a private workspace.

Run from a separate working directory:

```sh
sci verify /path/to/96a66d04c75df7c97e71eb3d97a5d79e109a0c0d3eed2d9aa855cd062c8ca119.zip --json
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python /path/to/publication/files/analyze.py --source /path/to/96a66d04c75df7c97e71eb3d97a5d79e109a0c0d3eed2d9aa855cd062c8ca119.zip --out ./regenerated
```

Compare the regenerated CSVs, NPZ draws and audit values with the package. Plot bytes can depend on plotting-library versions. The script checks the exact input entry hash and writes only to the output directory. Keep outputs outside the signed publication. Bundled files include our code, aggregate statistics, coefficient draws, figure, environment, source verification and notices. External monthly records are not bundled.
