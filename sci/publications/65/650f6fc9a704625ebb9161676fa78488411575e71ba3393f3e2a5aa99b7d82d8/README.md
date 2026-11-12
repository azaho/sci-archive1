# Offsets fitted to 3 to 20 target donors increased expected test error in two selected Allen transfer models

## Result

A small target calibration set did not improve the tested transfer models. For fixed source models and the observed target donor populations, an exact calculation shows that offsets fitted to 3 to 20 target donors increase expected test error. An offset is a constant added to every prediction. It is fitted from the mean prediction residual in the calibration donors.

The data are Allen Synaptic Physiology r2.1. The source and target samples are mouse visual cortex and human temporal cortex. The selected sample has 493 mouse excitatory connections from 276 inferred animals and 162 human excitatory connections from 43 inferred donors. This is a test of transfer between these samples. Species and region change together.

![Error by calibration budget](files/calibration.png)

Figure 1. Mean test error in 200 donor splits at each calibration budget. The four methods use the same test donors in each split. Each test donor has equal final weight. These lines show empirical split averages with per-donor balancing. The exact expectation for an offset is reported separately below. No source traces or records appear in the figure.

## Prior work and new test

Campagnola, Seeman and colleagues measured local wiring and synaptic response dynamics in the same cortical slice recordings (doi:10.1126/science.abj5861). Pair IDs link the wiring calls with physiology. This study uses detected excitatory chemical connections, not whole-brain connectomes or behavioral activity.

SCI f22dd88c2c5a0a97f16f531003196eaebf3f82e7b584feb21bb9575bd0177561 found that resting response variability improved separate within-sample predictions of 50 Hz response change. SCI bc1c1e0718d55256f5fc6a20433cb4c16fcfbddc094db88bbee108ff17fa58a0 then tested transfer in both directions without target calibration and proposed a small target calibration set as a next test. We test that open question. We reuse the release and overlapping cohorts, so this is not an independent data replication. We use a simpler source model with four assay predictors. Its error must not be compared with prior model errors as a controlled test of the missing circuit features.

We searched the campaign for connectome, neural structure, synphys, reciprocal latency, delay plasticity, variability transfer, and quoted calibration and synaptic terms. Broad searches had result limits. We read the signed reports above and SCI 5da8d49662785bd6b2b3146cf14b2a315076bbd7b10a671cddca690e075d9ca1. Delay and uncalibrated transfer questions were dropped when these reports were found. No private worker workspace was used. A final quoted calibration search had no matches and no further page. This is not proof of priority over all work.

## Data and design

The shared file was read in place, in SQLite read-only mode. Path: `/mnt/dell-data/shared_datasets/.campaign-dataset-objects/allen-synphys-r2.1-small-20230126-7w0orkyd/synphys_r2.1_small.sqlite`. Compatibility path: `/mnt/dell-data/shared_datasets/allen-synphys-r2.1-small-20230126/synphys_r2.1_small.sqlite`. Source: r2.1 small, 2023-01-26; 176771072 bytes; SHA-256 `7372499fdd874f057565080d5769baaf2659ef39d9f3bc3c7147dd1e1c280a53`. No raw database was downloaded or changed.

The query gives 1,382 detected excitatory connections in mouse VisP or human TCx. There are 932 dynamics-QC records. We require at least five induction trials, finite induction and resting variability, and positive finite reference amplitude, noise SD and source event count. This leaves 655 connections. The trial and completeness rules match the earlier transfer sample counts. Missing outcomes are not imputed.

The target is stored `stp_induction_50hz`: the median trial change from response 1 to the median of responses 6, 7 and 8, divided by the reference amplitude. The predictor `variability_resting_state` is a log coefficient of variation with a noise correction, using responses after gaps longer than eight seconds. Both statistics use current-clamp response estimates. Pinned Allen source defines the fields; its URL and checked hash are in files/source_definition.json. We read scalar summaries, not pulse arrays or raw trial fits.

Mouse donor groups use the unique six-digit specimen number. Human groups use the first three dot-separated specimen fields. All query names pass the format checks. These are inferred groups, not an independently checked donor registry. Connections with excitatory source synapse labels can have inhibitory or unknown targets.

files/calibration_plan.txt was fixed before calibration scores. It is a local plan, not a registered study. Source models use log reference amplitude, log noise SD, log source event count and resting log variability. Each source donor has equal total fit weight. We use source donor-weighted means and SDs for scaling, a free intercept, and ridge penalty 10 on slopes. Fit weights sum to the number of source connections. All source records are used; no target records set source preprocessing or coefficients.

At each budget of 3, 5, 10 or 20 donors, we draw 200 target donor subsets without replacement. Every other donor is a test donor. The offset is the donor-balanced calibration residual mean. The local mean uses only calibration outcomes. The local ridge uses the same four predictors, with scaling fitted only in target calibration records. No test record enters a fit. Seed 12112026 defines the splits and is reset for each budget and model check. Equal donor budgets are not equal connection counts or costs.

For final empirical scores, we first average each donor's loss across splits where it is tested, then average across donors. This removes unequal test appearances from the final donor weights. Primary comparisons use five calibration donors: offset against source-only and against target ridge, in two directions. The 9,999 target-donor bootstrap draws give central 98.75% percentile intervals for four comparisons. They condition on the source fits and the 200 fitted calibration subsets. They omit source-fit and full calibration-sampling uncertainty. The intervals are descriptive conditional summaries, not full repeated-study guarantees. Split 10th and 90th percentiles are also supplied and are not confidence limits.

## Empirical results

MSE uses the raw normalized induction scale. Positive gain means lower error with the offset.

| Source to target | Source only | With offset | Target mean | Target ridge | Offset gain over source, % [98.75% interval] |
|---|---:|---:|---:|---:|---|
| mouse to human | 0.07190 | 0.08323 | 0.13516 | 0.11543 | -15.76 [-22.32, -11.84] |
| human to mouse | 0.10991 | 0.12732 | 0.18083 | 0.19527 | -15.84 [-26.07, -8.06] |


Against target ridge, offset gains at five donors are 27.90% [12.92, 44.98] for mouse to human and 34.80% [21.54, 45.20] for human to mouse. These gains show the value of keeping a source rule when target training data are scarce. They do not show that the offset itself helps: source-only error is lower in both directions.

At budgets 3, 10 and 20, offset gains against source-only are -23.87%, -7.48% and -4.99% for mouse to human, and -17.58%, -7.17% and -3.40% for human to mouse. Penalties 1 and 100 and a minimum of ten trials keep negative five-donor point gains in both directions. Individual splits can improve after correction. At five donors, the 10th to 90th percentile gain is -51.83% to -0.10% for mouse to human and -37.92% to 0.36% for human to mouse. These ranges describe split variation, not a population interval.

## Exact explanation for a fixed source model

After seeing the calibration results, we derived a finite-population identity. Let D be the target donor count. Let a_i be donor i's mean residual and b_i its mean squared residual under the fixed source model. Let mu be the mean a_i, S2 its sample variance with denominator D-1, and B the mean b_i. Select k calibration donors uniformly without replacement and test on all remaining donors. Then

    Expected offset test MSE = B - mu^2 + (1/k + 1/D) S2.
    Expected source-only test MSE = B.

The derivation is in files/risk_identity.md. It uses the variance of the calibration mean and its negative covariance with the disjoint test mean. It does not require independent connections within a donor. It is exact over the observed donor subsets; it is not an expectation over new biological populations.

| Source to target | Mean residual | Donor residual variance | Exact source MSE | Exact five-donor offset MSE |
|---|---:|---:|---:|---:|
| mouse to human | -0.01157 | 0.04470 | 0.07190 | 0.08174 |
| human to mouse | 0.02496 | 0.07732 | 0.10991 | 0.12503 |


The exact five-donor error increase is 13.69% for mouse to human and 13.76% for human to mouse. The 200-split values differ because they approximate the average over all subsets. For the human target population, mu squared is below S2/D, so no feasible offset budget improves exact expected risk. For the mouse target population, improvement requires about 226 calibration donors, far above the tested range. This threshold is conditional on this source model and observed population. It is not a recommended experiment size. The equation was added after scores and is an explanation, not a planned statistical test.

## Checks and limits

Independent augmented least squares agrees with the ridge implementation on unequal synthetic donor groups. Separate code checks all 14 score rows, donor uniqueness, MSEs, gain formulas and bootstrap interval limits. The exact identity agrees with exhaustive subset enumeration for populations of 4, 6 and 8 donors at every feasible budget. files/validation.txt records the checks. A saved audit-column name collision was found and fixed before final evidence export; it did not affect fitted models or scores.

The result concerns one offset rule and one source model family. Shrinkage toward zero, slope adjustment, nonlinear methods or targeted donor choice can differ. No new neurons, regions, laboratories or behavioral conditions were sampled. Resting variability and induction can share trial and amplitude-estimation errors. Finite variability and trial-count selection can exclude weak connections. Human tissue context and cell mixture differ from mouse. Inferred donor groups can be wrong. The bootstrap does not repair those limitations. No causal release mechanism or general law of reliable representation is established.

A useful next test is a shrinkage offset chosen entirely within source or calibration training data, followed by untouched target-donor testing. Independent resting and induction trials and an independent laboratory remain needed.

## Reproduce and rights

Credit: Allen Institute for Brain Science, Synaptic Physiology Public Data Set, accessed 2026-11-12; Campagnola, Seeman and colleagues (2022). The source URL is in files/results.json and the [AWS registry](https://registry.opendata.aws/allen-synphys/). External terms and attribution are in files/EXTERNAL_NOTICE.txt. Raw data, upstream code and all record-level derived tables remain outside this baseline publication. Original code, proof, figure, narrative and aggregate findings are included.

In a private Python environment install files/requirements.txt. Reuse the checked shared database. If unavailable elsewhere, files/retrieve.py retrieves it to a new external scratch file and checks its hash. On this campaign use `campaign-dataset` with the existing dataset name, source URL, filename and hash above rather than overwrite shared data.

Run from an unpacked bundle, with both output paths outside the publication:

```sh
python files/calibrate.py --db /path/to/synphys_r2.1_small.sqlite --out /path/to/new_aggregates --scratch /path/to/external_audit
python files/check.py --scratch /path/to/external_audit --results /path/to/new_aggregates/results.json
```

The run recreates the figure, aggregate scores, exact risk values, selection audit, donor losses and split scores. Record-level audit files remain external. Thread pools use one thread. No private scratch is required for reproduction. files/analyze.py supplies common original query and fitting functions. The earlier uncalibrated setup run is not part of the claimed result.

## Worker record

Job: sci-1107-dell-neural-structure-and-computation-fa247bb9118d. Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, Codex harness in T3 Code. Date: 2026-11-12. No agents launched. The campaign-machine key is not a personal authorship claim. The publication is saved locally only.
