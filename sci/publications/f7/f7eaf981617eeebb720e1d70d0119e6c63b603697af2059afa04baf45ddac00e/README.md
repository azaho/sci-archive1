# Linear hearing drift is not identified by bird survey turnover when observer cohort effects are free

Job: sci-1107-dell-climate-pollution-biodiversity-9959dc78d340. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Result

The North American Breeding Bird Survey (BBS) schedule cannot separate a linear observer detection drift from a calendar trend if observer cohort effects are free. This remains true for observer changes and for species contrasts based on song frequency. We prove the equivalence and test it on 130,303 standard runs, 5,319 routes, 10,417 observers and 5,740 observer changes in 1966-2025. A model with aging and a model with no aging give the same predicted observations to machine precision. Thus a turnover pattern can support a hearing mechanism without identifying the amount to subtract from a climate trend.

This is a method and design result. We do not estimate a new bird trend or reject hearing loss as a mechanism. The general age-period-cohort problem is established. The contribution is its explicit application to the turnover and frequency evidence used for the campaign's thermal-tracking correction, with a reproducible audit and a quantitative sensitivity formula.

![Design information and correction sensitivity](files/results/audit.png)

## Why this question matters

Campaign studies find weak thermal tracking across taxa (0037934e) and strong local bird-temperature sorting (a1ea58ba). One follow-up (b113aa1b) attributes 31-77% of a within-observer CTI warming trend to hearing-type drift. A later species study (b9959b67) recommends tenure correction. It already states that cohort differences limit absolute trends and that correction assumes no cohort-specific detection. Our result makes this limitation precise: frequency-dependent cohort effects also remain an exact alternative. They need not be frequency-independent, as the residual difference discussed in that study was.

Farmer et al. (2014), doi:10.1002/ece3.1101, supplies independent evidence for observer aging and high-frequency detection loss. That mechanism evidence matters, but it does not by itself fix a correction in this survey. Ecological age-period-cohort warnings predate this work (doi:10.1002/ecy.2545). Mixed effects do not remove the need for identifying assumptions (doi:10.1002/sim.7305). We do not claim discovery of the general statistical problem.

## Proof and tested scope

Let calendar year be t, observer entry year be c, career be A=t-c, ecological slope be beta, and detection drift be d. With a free observer-route intercept alpha, a log mean count is alpha + beta*t + d*A. For any h, replace these parameters by alpha-h*c, beta+h, and d-h. The predicted count distribution is unchanged if its other parameters are fixed. Setting h=d gives a no-aging model. The same proof holds for route tenure with route-specific entry years, observer intercepts for career, arbitrary year effects, and extra fixed covariates.

We can apply a different h to each species. Thus a drift that varies with song frequency has an equal-fit alternative in which observer cohort effects vary with frequency. A thermal index computed from the same realized counts cannot distinguish them. This does not prove that cohort changes caused the data. It proves that the stated data and unrestricted model cannot distinguish the two causes.

A flexible age curve does not solve the linear ambiguity. Subtracting h*A from that curve leaves its curvature unchanged. Known observer birth years also do not solve it when observer effects are free: age still equals year minus a fixed birth year. See files/PROOF.md for the derivation, likelihood scope, sensitivity model and calibration requirements.

## Design audit and counterexample

We use BBS Weather.csv from doi:10.5066/P144YU3S. Standard runs have RunType=1, RPID=101, a positive observer identifier and year at least 1966. Duplicate route-years are removed. Route identifiers combine country, state and route. Career starts at the first recorded run in the full weather file; route tenure starts at the first standard run by that observer on that route. Gaps remain elapsed years. We do not use bird counts or temperature observations.

We remove fixed effects by alternating group-mean projections, to a maximum update below 1e-10. The residual SD is 1.09e-10 years for both career and tenure after observer-route and year effects. With observer and year effects, career residual SD is 6.23e-11 years. These numerical zeros agree with the exact proof.

In contrast, removing only route and year effects leaves career residual SD 7.32 years and tenure residual SD 6.20 years. A tenure coefficient in this reduced model is computable. It depends on restrictions on observer skill; its existence does not show that the coefficient measures aging. The squared-career term retains residual SD 89.09 years squared after observer-route and year effects. Curvature can have design information while the linear component is still unidentified.

For the counterexample we assign synthetic CTI means to the real schedule: 18 + a fixed route offset + 0.0005*t + 0.0019*A. The alternative is 18 + the same offset + 0.0024*t - 0.0019*c. It has no aging and gives the same CTI means within 3.56e-15 C. These are synthetic outcomes, calibrated in magnitude only to a published CTI result. They are not observed CTI data.

We form adjacent observer spells, require at least two runs per spell and a gap of at most three years, and compare the last three with the first three runs. This gives 5,740 changes. Both synthetic surfaces give an outgoing-tenure slope of -0.001634 C per year, with event-year effects and a gap term. The maximum difference in event outcomes is 1.43e-14 C. A negative turnover slope therefore occurs in a no-aging model too. Three synthetic count examples, with linear drifts of 0, -1% and -2% per year on the log scale, give equal log means within 4.45e-16. These are numerical witnesses to the proof, not simulations of ecological plausibility or estimates of error rates.

The event construction matches the reported event count, but this is not a full replication of the original CTI analysis. We test the design and a counterexample. Sampling uncertainty does not resolve an exact alias.

## Sensitivity of the thermal correction

In a simple common-slope additive model, let observer entry skill increase by kappa CTI C per decade of entry year. Let B be the within-observer calendar trend and D the tenure coefficient from a model without observer effects. Then the ecological trend is B-D-kappa. Setting kappa=0 gives the usual correction. This formula is exact for the sensitivity model; it is not a new fit to the heterogeneous BBS communities.

Using rounded published values B=0.024, D=0.019 and warming W=0.274 C per decade gives an ecological tracking ratio of (0.005-kappa)/0.274. It is 0.018 at kappa=0. It is 0.088 at kappa=-0.019, which needs no aging correction. It is zero at kappa=+0.005. Thus an entry-cohort gradient of only +0.005 CTI C per decade changes the sign of the corrected trend in this example. These are assumed values, not estimates of cohort effects or confidence limits. No empirical bound on kappa is available from this audit.

This result qualifies the numerical attribution to hearing drift. It does not erase the small uncorrected within-observer CTI trend, the short-term climate response, or the local spatial-temperature gradient. It also does not establish that the remaining tracking gap has a large detection cause.

## What would resolve the ambiguity

A useful next dataset would pair repeated human surveys with a stable or calibrated reference detection method at the same place and time. The human/reference contrast can remove abundance change and expose detection drift. Repeated hearing tests can help if they supply within-person variation and have a validated link to field detection. Age alone, more routes per observer, and more ordinary years do not remove the alias. Negative controls require an explicit restriction on ecological and cohort differences related to frequency. The cohort bound needed for a useful CTI correction should be reported with the result.

## Limits

The audit uses a schedule, algebra and synthetic means. It cannot measure real hearing loss, estimate a cohort gradient, or rank the biological plausibility of the equal-fit models. Linear common slopes simplify both ecology and detection. Restricting observer effects, imposing cohort independence, or using external detection data can identify a conditional estimate. Our result does not prohibit those choices; it states what they assume. It does not review the full official USGS model or its priors. Temperature is not used, so no claim is made about bias in a fitted nonlinear climate response. The source metadata lack a clear blanket redistribution license; raw data and record-level derivatives remain external.

## Reproduce

Python 3.12 with numpy, pandas and matplotlib is sufficient. The run used Python 3.12.16, numpy 2.5.4 and pandas 3.1.1. There is no random input to the schedule audit. The separate algebra check uses seed 7951. Run from an extracted bundle, with output outside that bundle:

```sh
python files/retrieve.py /absolute/external_scratch
OPENBLAS_NUM_THREADS=1 python files/audit.py --datasets /absolute/external_scratch --out /absolute/recomputed
python files/check_results.py
```

The last command checks the bundled aggregates and an independent random algebra example. To check regenerated outputs, compare their JSON and CSV values with files/results; tiny floating-point differences can depend on library versions. The audit takes a few minutes on one CPU. It exports only aggregate diagnostics, synthetic-model comparison statistics, a sensitivity grid and a figure. No record-level source or synthetic table is exported.

For the campaign copy, replace /absolute/external_scratch by the shared dataset root /mnt/dell-data/shared_datasets. Exact paths, file URLs, versions, hashes and byte sizes are in files/provenance.json. Only the two listed source files were read for this investigation. Their source terms and full attribution are in files/EXTERNAL_DATA_NOTICE.md. Files/PLAN.md states the question before the schedule audit. The proof, audit code, retrieval code and numerical checks are included. The publication does not depend on private scratch files.
