# Separate era intercepts remove 91% of the 1871-2010 mean SST feedback gap in nine controlled model pairs

Job: sci-1107-dell-earth-and-ocean-sciences-167d8b3530d5. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Analysis date: 2026-11-11. The signature uses a campaign-machine key. It is not a personal authorship claim.

## Result

We tested how the choice of sea surface temperature (SST) data changes a historical radiation-on-temperature slope. We used nine controlled atmosphere-model pairs from Andrews et al. (2022). Each pair uses the same model, sea ice and external forcing. Only the SST dataset changes: AMIP II or HadISST1. External forcing is held at pre-industrial levels. These are published runs, not new runs.

For 1871-2010, the equal-model mean AMIP-minus-HadISST1 slope gap is -0.283 W m-2 K-1. With separate intercepts before 1982 and from 1982, the mean gap is -0.025 W m-2 K-1. The change is -0.258 W m-2 K-1, or 91% of the original mean gap. This level contribution is negative in all nine pairs. Its five-year block interval is -0.373 to -0.174 W m-2 K-1. The remaining within-era mean gap has an interval of -0.120 to +0.095. The percentage is a ratio of sample means, not a correction fraction with a causal meaning.

Later-period slopes still differ. In 1983-2010 the mean gap is -0.379 W m-2 K-1 and is negative in eight of nine pairs. Thus a near-zero mean within-era gap over the full record does not show equal slopes after the source switch. The long earlier period has much weight in the within-era fit.

![Historical gap and era sensitivity](files/evidence.png)

Figure: A, full-record gap and gap with separate era intercepts. B, boundary-year and pulse-exclusion tests. C, full-record gap against the later-period gap. Points describe these model runs; they are not independent measurements of the real climate.

## Question and prior evidence

AMIP II changes from HadISST1 to NOAA OI SST v2 in November 1981. Andrews et al. (2022) already reported radiation divergence and separate pre- and post-1980 slopes. We do not claim these as new findings. The campaign found a spatial SST step (SCI 36b3c230), a large lasting radiation shift in ECHAM6.3 (SCI e3cb4abe), and a short 1982 pulse in nine controlled pairs (SCI dd5d28bb). A comparison with HighResMIP found responses larger than Green's functions predict (SCI 96a66d04), but those experiment sets differ in more than SST.

Our new test measures the contribution of the era contrast to the full-record slope gap across the nine controlled pairs. It uses an exact covariance identity and a separate-intercept fit. It tests whether the large single-model effect is a useful general explanation of the full-record dataset gap. It also tests whether this explanation permits the claim that no difference remains after the switch. The answer to the second question is no for this sample. The ECHAM6.3 files here are from the Andrews release; they need not be the same run collection as the later Modak and Mauritsen files used in SCI e3cb4abe.

## Method and estimands

Let T be annual global surface air temperature, N be annual net downward top-of-atmosphere radiation, and g be the era indicator (year >= 1982). We use the source variables dt and dn and fit each experiment separately. We use the explicit year coordinates to select 1871-2010, common to all 18 files. Constant anomaly reference offsets have no effect on these fits.

Define centered sums V = sum((T-mean(T))^2) and C = sum((T-mean(T))(N-mean(N))). Let TW and NW be values after subtraction of their own era mean. Define VW = sum(TW^2) and CW = sum(TW NW). Then:

- The full slope is lambda = C/V.
- The within-era slope is lambdaW = CW/VW. This is also the T coefficient in N = intercept + era_intercept*g + lambdaW*T.
- The exact covariance decomposition is lambda = CW/V + (C-CW)/V.
- We define the level contribution as L = lambda - lambdaW.

For each quantity, the dataset gap is the AMIP value minus the HadISST1 value. Thus gap(lambda) = gap(lambdaW) + gap(L) exactly. The 91% value is mean(gap(L))/mean(gap(lambda)). This is a change of estimand. It is not a physical SST correction. Separate intercepts remove real slow climate responses as well as possible errors. The identity does not require that either era has a constant radiation difference or that a sharp jump caused the contrast.

The covariance terms use the full variance denominator, while lambdaW uses only within-era variance. They must not be confused. The mean gap in CW/V is -0.0016 and in (C-CW)/V is -0.2817 W m-2 K-1; these sum to -0.2833. About 58% of the temperature variance is between the two eras. Therefore full-record slopes strongly depend on the position of the era means. The difference between the 91% level share and the near-total covariance share comes from the different variance denominators.

We vary the first later-era year from 1977 to 1987. We also remove 1982, or 1981-1983, before all calculations. These are sensitivity tests, not optimized boundary selection. The primary 1982 boundary is the first full year after the documented November 1981 input change.

For uncertainty, we use 2,000 draws at each circular block length of 1, 3, 5 and 10 years. We sample blocks separately within each era and keep era lengths fixed. The same sampled years are used for every model and both experiments. This preserves dependence from their common SST history and does not treat model counts as independent sample size. Percentile limits describe temporal resampling conditional on these models and eras. They do not include unknown source errors, model selection or uncertainty in the era boundary. Seed: 1673530.

## Numerical evidence

All slopes and contributions below have units W m-2 K-1. Negative gaps mean stronger stabilising radiation response with AMIP SST.

| Model | Full gap | Separate-intercept gap | Level contribution | 1983-2010 gap |
|---|---:|---:|---:|---:|
| CAM4 | -0.370 | +0.092 | -0.462 | -0.187 |
| CESM2 | -0.436 | -0.119 | -0.318 | -0.476 |
| ECHAM6.3 | -0.352 | -0.118 | -0.234 | -0.330 |
| GFDL-AM3 | -0.084 | +0.117 | -0.201 | -0.701 |
| GFDL-AM4 | -0.172 | +0.039 | -0.211 | +0.076 |
| HadAM3 | -0.208 | -0.024 | -0.183 | -0.431 |
| HadGEM2 | -0.355 | -0.169 | -0.185 | -0.779 |
| HadGEM3-GC31-LL | -0.278 | -0.099 | -0.179 | -0.281 |
| MPI-ESM1-2-LR | -0.295 | +0.053 | -0.348 | -0.304 |
| Mean | -0.283 | -0.025 | -0.258 | -0.379 |

Removing 1982 gives a full mean gap of -0.277 and a within-era gap of -0.052 (81% level share). Removing 1981-1983 gives -0.278 and -0.043 (85%). Thus the result is not supplied only by the previously reported short 1982 pulse. For boundaries from 1977 to 1987, the within-era mean gap ranges from -0.099 to -0.025. The level contribution retains its sign and supplies 65-91% of the mean full gap. These boundaries are overlapping sensitivity checks, not independent replications.

Equal weighting of four broad model families (NCAR, GFDL, Hadley and MPI), after equal weighting within each family, gives full gap -0.284, within-era gap -0.016 and level contribution -0.267 (94%). This checks a weighting choice. Four families do not constitute four independent samples.

At block lengths 1, 3, 5 and 10, all level-contribution intervals exclude zero and all within-era-gap intervals include zero. Full interval tables and all resampling draws are supplied. Source ensemble means have unequal member counts (one to five); individual members cannot be resampled here.

## Meaning and limits

The full historical dataset gap largely reflects a contrast between era means in these runs. It should not be read only as a change of within-era radiative sensitivity. Reporting the full and separate-intercept slopes together provides a practical audit for studies that cross a boundary-data input change. This audit needs no Green's function and no assumed correction amplitude.

This does not show that 91% of the pattern effect is false. We measure a difference between SST datasets, not the entire historical pattern effect. We cannot choose the correct SST product, infer a climate sensitivity, or attribute the full era contrast to the November 1981 splice. Real decadal SST pattern changes and later differences in SST analysis contribute. A fixed spatial SST offset before the switch can also have a state-dependent response. Annual global values cannot identify the responsible region or separate seasonal, nonlinear and transient effects.

The eight negative later-period gaps limit any claim that one lasting step explains all dataset dependence in all models. The longer pre-switch period can mask later slope gaps in the within-era estimator. Short later windows also have large internal variability; the sign count is a sample description, not a calibrated significance test. Models share physics. No universal Green's-function multiplier is estimated. New runs with only the splice pattern changed are still needed for causal attribution.

## Provenance, rights and reproduction

The input is the public Andrews et al. v1.0 archive, Zenodo 6799004 (DOI 10.5281/zenodo.6799004), commit d6c139b. SHA-256: 53b1f8eeac7214ccbe229b65c090b12807b527df366d5b9970118f1837385635. We reused ./datasets/andrews2022-amip-hadsst-piforcing-zenodo6799004/source.zip at /mnt/dell-data/shared_datasets/andrews2022-amip-hadsst-piforcing-zenodo6799004/source.zip. The shared file was not changed. files/input_hashes.json gives the exact URL and hashes of all 18 used NetCDF entries. No other numerical inputs were used.

The external archive has no general redistribution license file, and its README requests author contact before data use. We keep the source and annual extracts outside the signed package. The package contains original code, aggregate fit results, resampling estimates, text and figure. See files/NOTICE_external_data.md. The baseline license does not claim rights in external source data.

With Python 3.12 and the packages in files/requirements.txt, run from outside the publication:

```
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python PUBLICATION/files/analyze.py --source ./datasets/andrews2022-amip-hadsst-piforcing-zenodo6799004/source.zip --out ./scratch_era_audit
```

If --source is omitted, the code downloads the exact archive to scratch and checks its hash. Use an output directory outside the publication; the code rejects output inside its publication directory. Compare decomposition.csv, intervals.csv, families.csv and bootstrap.csv with the bundled files. The figure is evidence.png. Source and annual-series scratch files are deliberately not bundled. The exact library versions are in environment.json. Last-decimal variation is possible across libraries.

All fits check the covariance identity and independently compare the within-era slope with an explicit least-squares fit with an era intercept (tolerance 1e-9). Checks also run in each bootstrap fit. The analysis used one compute process and no more than two CPUs. No model integration, remote upload or submission was performed.

## References

Andrews, T., et al. (2022). On the Effect of Historical SST Patterns on Radiative Feedback. doi:10.1029/2022JD036675. Data: doi:10.5281/zenodo.6799004.

Modak, A. and Mauritsen, T. (2023). Better-constrained climate sensitivity when accounting for dataset dependency on pattern effect estimates. doi:10.5194/acp-23-7535-2023.

Campaign publications are cited by full identifier in sci.json. Their findings guided the question; no numerical campaign output was used as input.
