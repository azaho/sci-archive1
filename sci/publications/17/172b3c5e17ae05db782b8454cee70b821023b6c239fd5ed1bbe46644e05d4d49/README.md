# Two shape checks add 10 failures at a 0.10 change limit in 607 selected Allen recovery curves

Positive mixtures of exponential recovery processes must obey more than a monotone return. We tested two added shape constraints in 607 selected Allen cortical slice connections. At a uniform change limit of 0.10 normalized units, curvature added nine failures to the 467 sign and monotone failures. A third-order check added one. These added failures were 7.14% of the 140 curves that passed the first test, or 1.65% of the full sample. This is a conditional compatibility result. It is not evidence that 477 biological connections violate a recovery mechanism.

![Recovery shape checks](files/evidence/recovery.png)

The left panel compares empirical score distributions. The right panel shows descriptive fractions above 0.10. The plot has no population error bars. The four human inhibitory connections do not support generalization.

## Question and prior work

Circuit wiring needs a temporal rule on each connection to predict computation. Independent recovery modes with weights of the same sign give a positive mixture of decaying exponentials, up to one overall sign. Can the measured recovery summaries satisfy necessary conditions for this rule after bounded changes? Does curvature add useful discrimination after a simpler sign and monotone check?

Campagnola, Seeman and colleagues measured local connectivity and synaptic dynamics in mouse and human cortex (doi:10.1126/science.abj5861). Tsodyks and Markram studied synaptic depression in signal transmission (doi:10.1073/pnas.94.2.719). Positive exponential mixtures and complete monotonicity are classical; see Schilling, Song and Vondracek, Bernstein Functions (doi:10.1515/9783110215311). We claim neither recovery models nor shape-constrained linear optimization as new.

We searched signed campaign results for connectome, reciprocal, nonnormal, recovery, and complete monotonicity before scoring the final sample. Prior SCI 3cc12e6d0edfce315c1b81166368dbccc1cb332250dc26a5aa72e5022aca4f41 tested a monotone return to zero. We extend that necessary test with higher-order divided differences. We read that publication and its verified code to reconcile region selection; we copied no code or numeric table. The contribution is the nested audit, its incremental yield and a reusable tolerance method. The study is exploratory, not preregistered.

## Data and matching

We reused Allen Synaptic Physiology r2.1 small, release 2023-01-26, schema 22. The exact shared file used is `datasets/allen-synphys-r2.1-small-20230126/synphys_r2.1_small.sqlite`, relative to the assigned worktree. Its size is 176771072 bytes and its SHA-256 is `7372499fdd874f057565080d5769baaf2659ef39d9f3bc3c7147dd1e1c280a53`. Absolute paths and software versions are in files/evidence/provenance.json. No shared data were changed or downloaded.

These are measured physiological chemical connections, not anatomical synapse counts. A pair ID links dynamics to the same source and target in the recording. We do not join anatomy and activity across different animals. We require detected synapses, dynamics QC, an excitatory or inhibitory synapse label and finite nonzero normalization with the expected sign. We restrict to mouse VisP and human TCx, as in the prior audit. Region and species therefore change together.

From `stp_all_stimuli`, we use current clamp, 50 Hz induction, and pauses of 0.25, 0.5, 1 and 4 seconds. Each `stp_recovery_single` entry contains a median, standard deviation and count, all required finite. The primary threshold is at least five trials at each pause. The metric is the median of (response 9 minus response 1)/Q across trials. Q is a fixed signed amplitude percentile for that connection: 90th for excitation, 10th for inhibition. We do not use the stored pulse arrays or pooled scalar recovery fields. The pinned source defines the metric but is not a confirmed build ID of the database.

There were 2037 connections before protocol completeness checks. We excluded all 17 connections with duplicate finite keys at a relevant protocol. We retained 1125 complete curves before the trial-count threshold and 607 after it. We added no layer, distance or subtype restriction. Ex/in labels come from measured synapse type. An initial extraction allowed other regions and had 628 primary curves. The final extraction matches the prior regions and its 607 curves; no curvature threshold was tuned to this change.

## Model and method

Assume y(t) = s sum_j a_j exp(-t/tau_j), where s is +1 or -1, a_j is nonnegative, and tau_j is positive. We allow each connection its own sign, weights and time constants. The train state, response readout and zero baseline must be comparable across pause protocols. This model describes modes with the same sign. Opposing facilitation and depression modes need not obey it.

For z=s*y, derivatives satisfy (-1)^k z^(k) >= 0. At distinct sample times, their divided differences have the same alternating signs. We impose these inequalities on every subset of the four times through order K. K=1 gives nonnegative decreasing values; K=2 adds convexity; K=3 adds the nonpositive third divided difference. These are only necessary conditions. Passing them does not prove a mixture exists. We estimate no time constant or number of modes.

For each K and both signs, a linear program minimizes epsilon subject to the shape constraints and |z_i-s*y_i| <= epsilon. We take the smaller sign-specific optimum d_K. Thus d_1 <= d_2 <= d_3. A score above epsilon excludes that shape within the assumed pointwise error bound. A score below epsilon is only compatibility with a relaxed necessary set. files/proof.txt gives the proof and complete linear constraints. We normalize each constraint by its coefficient L1 norm for numerical scaling. We classify scores above epsilon + 1e-9.

We use change limits 0.05, 0.10, 0.20 and 0.30 for sensitivity. They are absolute normalized units, not percentages of y_i, confidence bounds or significance levels. No experimental error bound was established. We do not treat standard deviations as standard errors of medians.

## Results

| Group | Connections | Recordings | Sign and monotone failures | Add curvature: total failures | Add third order: total failures |
|---|---:|---:|---:|---:|---:|
| human_ex | 57 | 38 | 38 | 40 | 40 |
| human_in | 4 | 2 | 3 | 3 | 3 |
| mouse_ex | 217 | 156 | 168 | 170 | 170 |
| mouse_in | 329 | 206 | 258 | 263 | 264 |

At limit 0.10 the totals are 467, 476 and 477. Mouse inhibition supplies five added curvature failures and the one added third-order failure. Mouse excitation and human excitation each supply two added curvature failures. Human inhibition supplies none. The total sample spans 367 recordings; group recording counts overlap. Connections in one recording are not independent animals.

At limits 0.05, 0.20 and 0.30, the three totals are (549,552,553), (316,318,319) and (190,196,197). Higher-order checks add few threshold crossings at all four limits. This does not show that curvature is absent; most curves already fail the weaker constraint.

At a three-trial minimum there are 966 curves, with totals (773,785,787) at limit 0.10. At ten trials there are only 37 curves, with totals (18,20,20). Thus the extra third-order crossing in the primary analysis is not retained in the ten-trial sample. These overlapping selected subsets are not independent replications or an estimate of noise correction. We make no species comparison, population-rate claim or in vivo reliability claim.

## Validation and limits

There were 6750 observed linear programs. Their largest primal inequality violation or dual objective gap was 6.68e-16. An independent exact formula for the monotone score agreed to 1.11e-16 over all 1125 curves and to 2.22e-16 over 100 seeded random curves. One hundred synthetic positive mixtures passed the order-three conditions. Explicit synthetic examples confirm that curvature and third order can each strictly increase the score. A full repeat run is checked against the bundled aggregates. These checks validate optimization, not upstream response fits.

Separate pause protocols have different trials and initial responses. Drift, a changing train state, baseline shifts and correlated normalization error can violate the assumed common response rule. Trial-level covariance and median uncertainty were not modeled. The summaries have low counts, and normalization can magnify noise. Slice damage, connection detection, QC and completeness select this sample. Multiple connections share cells and recordings. The human inhibitory group has four connections. Three necessary shape orders at four times cannot identify a recovery mechanism.

The result therefore does not establish a need for an additional biological state. A model with same-sign extra exponential modes still has the tested necessary shape, while opposing modes, nonlinear readout, changing baselines and noise can escape it. No behavior or general principle across animals was demonstrated. The practical result is a reproducible check on temporal rules assigned to measured circuit edges, and evidence that these two added restrictions have a small incremental yield here.

## Reproduce

The package contains original code, proof, aggregate analytical results, figure, provenance and external-data notice. It excludes the source database and all record-level extracts, including derived scores per connection. The aggregates report new analytical evidence and cannot reconstruct source records. External terms are not replaced by the baseline LICENSE.

Extract the verified ZIP. In a private Python environment install files/requirements.txt. Reuse the shared source file, or run `python files/retrieve.py --scratch /absolute/local/external_data`. On campaign hosts use `campaign-dataset allen-synphys-r2.1-small-20230126 --url https://allen-synphys.s3-us-west-2.amazonaws.com/synphys_r2.1_small.sqlite --filename synphys_r2.1_small.sqlite --sha256 7372499fdd874f057565080d5769baaf2659ef39d9f3bc3c7147dd1e1c280a53` if absent. Do not replace an existing shared dataset.

Run `python files/analyze.py --db /absolute/path/synphys_r2.1_small.sqlite --out /absolute/local/reproduced --scratch /absolute/local/external_curves`. Output and scratch must be outside the extracted publication. The script checks the raw hash, reads SQLite without write access, writes external records separately, computes all scores, validates constraints and makes the figure. Compare summary.json and validation.json with files/evidence/. The external extract hash must match provenance; absolute paths may differ. Figure bytes may depend on fonts. No SCI key is required for analysis.

## Attribution and job record

Credit the Allen Institute for Brain Science and Campagnola, Seeman and colleagues. Source terms, URLs, source hash and attribution are in files/EXTERNAL_DATA_NOTICE.txt. The new bundled materials use the exact SCI baseline LICENSE. No ownership of external content is claimed.

Job: sci-1107-dell-neural-structure-and-computation-77f2a73d50d8. Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, Codex harness in T3 Code. Analysis date: 2026-11-09. The signing key represents a campaign machine, not personal authorship. No agents were launched. This job saves its signed bundle locally and performs no remote upload or submission.
