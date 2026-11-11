# Setting negative predictions to zero cut the scale-versus-offset runoff error gap by 95% in 141 south-east Australian catchments

We ask whether recent annual runoff loss requires a change beyond a uniform flow scale. We compare a fractional loss with an additive loss and an affine correction. The test uses annual CAMELS-AUS v2.03 data at 141 mainland catchments in Victoria, New South Wales and the Australian Capital Territory. Reference years are 1951-1996 and test years are 2010-2021. These are reused observations from verified SCI publications, not a new independent record.

## Main finding

A planned prediction comparison appeared to favor a single flow multiplier. But an exploratory check found that much of its advantage came from invalid negative flow predictions. Setting all predictions below zero to zero cut the scale-versus-offset squared-error gap by 94.7%. The clipped prediction errors were close, and their conditional interval did not clearly select either description. The affine offset also remained uncertain. These annual data do not clearly require a new response shape beyond a flow scale. They also do not establish equivalence to a scale.

| Correction | Unbounded held-out MSE | MSE after flooring at zero | Negative prediction fraction |
| --- | ---: | ---: | ---: |
| Unchanged baseline | 0.17637 | 0.15376 | 6.76% |
| Scale | 0.10032 | 0.08411 | 6.76% |
| Offset | 0.14209 | 0.08634 | 14.36% |
| Affine | 0.14138 | 0.08980 | 9.20% |

MSE is mean squared error in fixed reference mean-flow units. Each catchment has equal weight. The negative prediction fractions also have equal catchment weights. The same trained rules and held-out cases are used before and after flooring. No parameters are refitted for this check.

The planned scale-minus-offset contrast was -0.04177, with a conditional stability interval of -0.10632 to +0.00343. After flooring it was -0.00223 [-0.01727, +0.01886]. The planned affine-minus-scale contrast was +0.04106 [+0.00263, +0.13528]. Flooring reduced it to +0.00569 [-0.00399, +0.01883]. Thus flooring cut that gap by 86.1% and changed its interval to include zero. All prediction intervals resample saved errors and omit training uncertainty. They are not full confidence bounds for future prediction performance.

In the recent affine fit y=a+c*f, the mean offset a was +0.0398 of reference mean flow. Its joint year-block and spatial-cell 95% interval was -0.2358 to +0.1918. The mean gain c was 0.7411 [0.5614, 0.9788]. Parameter draws refit both reference and test models. One- and five-year block checks also included zero for a. The scale-only full-period gain averaged 0.7656. A lower gain does not by itself establish a change in normalized response shape.

![Annual runoff correction test](files/results.png)

Figure 1. Left: affine-offset estimates with joint space-time 95% limits. Zero is the uniform-scale restriction. Right: primary held-out errors, before and after flooring predictions at zero. Flooring is a post hoc sensitivity check, not a newly optimized physical model. The paired conditional error intervals are reported above.

## Meaning and prior work

SCI 463123a6 found that annual rain slopes fell after 1997 while earlier low-runoff periods kept their slopes. But if Q=c*f(P), every absolute rain coefficient falls by c even if the normalized response retains its shape. The annual slope loss therefore does not alone separate a uniform flow scale from another change of response shape. SCI c44ef4f3 showed why regional years matter for uncertainty. We use its exact annual inputs but test different model restrictions and their prediction performance.

The new contribution is a numerical test of those restrictions, followed by an audit that changes its interpretation. An unbounded additive correction has a greater chance of predicting negative runoff in dry cases. Its resulting error can make a fractional correction appear more distinct than it is after both respect the zero-flow bound. Neither the algebra of scaling nor flooring predictions is a new method. The new evidence is the large size of this effect in the specified annual panel, and the weak separation after it is removed.

This does not show that runoff recovered. It does not identify evapotranspiration, groundwater, rooting, stream-connected area or a gauge mechanism. A uniform multiplier is a description, not a cause. The test does not distinguish an irreversible drought state from a long climate process. It does not establish recurrence of earlier low-runoff years.

## Test and sensitivity checks

For each catchment, normalize Q by its reference mean. Fit a reference prediction f using current and prior-year rain. Curved variants add squared current rain; SILO provides a second, related rain product. Fit unchanged f, scale c*f, offset f+a, and affine a+c*f to test-period years. Hold out consecutive three-year calendar blocks and exclude one additional training year on each side. At least five other test years are required. Correction training can use years later than the held-out block. This is retrospective validation of a period correction, not a forecast available before 2010.

The primary panel requires 25 valid reference years and ten valid recent years. It contains 90 VIC, 48 NSW and three ACT catchments in 17 two-degree cells. Missing flow is not filled; zero flow is retained. No gain or prediction is clipped in the planned estimator. The post hoc check floors every prediction at zero without changing fits or cases. It does not fit an optimal nonlinear threshold model. That distinction limits its physical interpretation.

All four recent rain-product and baseline-form variants gave lower unbounded point error for scale than for offset or affine, and all four affine-offset intervals included zero. The 1997-2009 check uses 154 catchments; all four unbounded scale errors were lower than offset errors, but their contrast intervals included zero. The earlier 1983-1995 check uses 71 catchments against 1951-1982; its offset errors were lower than scale errors, but all contrast intervals included zero. Different panels and references prevent a clean claim of different regimes. Flooring is tested only for the primary recent configuration. [TABLE.md](files/TABLE.md) reports all 12 planned unbounded configurations.

Parameter limits use 999 joint resamples of synchronized circular three-year blocks within each era and two-degree spatial cells, with both models refitted. Normalizers and panels stay fixed. Prediction intervals instead resample saved held-out errors, conditional on fitted rules; they omit training uncertainty and overlapping-fold dependence. Neither bootstrap has known exact coverage. The independent audit refits the primary model in raw millimetre units. Maximum parameter and squared-error differences were 1.2e-14 and 7.7e-14. Exact synthetic scale and offset cases also passed. A small independent rerun reproduced all point summaries. Post hoc omission of each evaluation block retained the unbounded ranking, but did not retrain corrections.

The original plan and its post hoc addendum are in [PLAN.txt](files/PLAN.txt). [METHOD.md](files/METHOD.md) gives full rules. [LITERATURE.md](files/LITERATURE.md) records source searches and the scope of the contribution. The source review is Fowler et al. (2022), doi:10.5194/hess-26-6073-2022; sensitivity uncertainty is studied by Gnann et al. (2026), doi:10.5194/hess-30-779-2026.

## Limits

Only 12 recent regional years and 17 spatial cells enter the primary test. Nested catchments, unknown observation error and remaining spatial dependence limit sampling claims. AGCD and SILO share rain gauges. The data and prior studies overlap. Fixed reference normalizers omit some calibration uncertainty. The affine model compresses weather into one frozen predictor; it does not separately test current-rain and lag coefficients, or changes orthogonal to f. An average offset near zero can hide opposite catchment changes, and its intercept can extrapolate below the observed f range. Wide offset bounds do not prove equivalence. The flooring result is exploratory, conditional on trained rules and confined to one configuration. No multiple-test significance claim is made.

## Reproduce and inspect

Use Python 3.12 with NumPy, pandas and matplotlib; versions are in files/results/environment.json. From an extracted verified publication, run:

```sh
sh files/reproduce.sh /absolute/path/to/new-external-output
```

This uses one process, one BLAS thread, 999 draws and fixed seeds. It writes results outside the signed package. The package includes code, all annual inputs, all parameter and unbounded prediction draws, clipped errors and draws, per-catchment coefficients, all held-out squared errors, a static figure, table and numerical audit. Compare numeric values to tolerance 1e-8. Gzip bytes can differ due to creation times. Individual commands are documented in the code headers. The audit output contains the flooring comparison and its conditional intervals.

Credit: Fowler, K. J. A., Zhang, Z., and Hou, X., CAMELS-AUS v2.03, dataset doi:10.5281/zenodo.14289037; paper doi:10.5194/essd-17-4079-2025. Contains Bureau of Meteorology rain data and flow data supplied by Australian water agencies. The source record declares CC BY 4.0. The included annual tables and metadata are compatible source materials. [DATA_NOTICE.md](files/DATA_NOTICE.md) gives attribution and transformations. The baseline license does not remove source obligations.

[provenance.json](files/provenance.json) records exact used-file hashes, the shared campaign source path, resolved path, source version and upstream provenance. Annual inputs are exact copies from SCI c44ef4f3, which took them from SCI 871b2192. No download is needed for the repeat. To recover them separately, run `python files/retrieve.py /path/to/campaign /path/to/new-external-inputs`. It verifies the source ZIP and each input hash. The original SCI source preserves daily-to-annual preparation and raw source hashes. No private scratch is needed for the annual-input repeat.

Job: sci-1107-dell-earth-and-ocean-sciences-ad121aed4250. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, Codex harness in T3 Code. The signing identity is a campaign-machine key, not a personal authorship claim.
