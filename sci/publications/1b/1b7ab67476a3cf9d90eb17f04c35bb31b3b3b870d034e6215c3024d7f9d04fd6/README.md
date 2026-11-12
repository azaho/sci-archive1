# Stable positive delay mixtures miss two-window AOU ranges in one eastern North Pacific tile

## Result

Extra transport delay can explain much of the published model mismatch in the western North Pacific. It does not explain both published time windows in the 35-40 N, 130-120 W tile under a stable mixture of the tested model responses. This conclusion is conditional on common sampling support. It does not establish an extra ocean oxygen-loss process.

We use the blind tile study sci:sha256:6e8318acaeed64894cfca3e0971b2e6742fc5acadf8b880aefa9334bb26bbafc. Its ventilation model gave the size but not the spatial pattern of apparent oxygen utilization (AOU) gains on density 26.5. It proposed slower transport as one possible cause. We test a large family of added delays, rather than fit one more transport model. All tests here were selected after the source results were public. This is a secondary analysis, not a blind test.

![Delay response bounds](files/results/delay_bounds.png)

Figure 1. Each blue region is the convex hull of pairs of model AOU changes, one pair for each model cell, run and added integer delay from 0 to 20 years. Thus any fixed nonnegative mixture of these pairs is inside the region. Orange bars are the published marginal 95% cruise-bootstrap intervals. They are not a joint 95% confidence region. Left: the eastern tile misses the blue region. Right: a western tile has uncertainty ranges that reach the region. All changes are relative to 1984-1996.

## Question and prior work

Can a slower response alone explain the eastern excess and western shortfall of the published ventilation model? Mecking and Drushka (2024), doi:10.5194/bg-21-1117-2024, linked upstream outcrop variation to downstream oxygen with a travel-time lag. Transit-time distributions describe passive transport with a nonnegative distribution of travel times; see Haine and Hall (2002), doi:10.1175/1520-0485(2002)032<1932:AGTTWM>2.0.CO;2. These ideas predate this study. Our new contribution is a finite-library test of all positive mixtures of added delays, with a sharp bound on how much mixture weight must change to remove a conflict between two sampled windows. Applying a passive delay to an AOU response is a model-error hypothesis, not a general oxygen budget law.

## Inputs and method

We use only three published aggregate files. They contain 20 model annual AOU maps for 1980-2025 and observed tile changes for 2009-2015 and 2016-2025. Both observed changes use 1984-1996 as reference. Fifteen tiles meet the source study's eligibility rule in both windows. The source retains at least three matched cell-season strata and three cruises per epoch in each eligible tile. The two windows can have different matched strata. The eastern tile has five early-window strata and four later-window strata, with six and four late cruises. Data are sparse.

For each eligible tile, take all ocean cells outside the earlier target regions. For run r, cell s and delay d, compute the two-vector

`v(r,s,d) = (mean_2009:2015 A(t-d) - mean_1984:1996 A(t-d), mean_2016:2025 A(t-d) - mean_1984:1996 A(t-d))`.

The delay acts on the reference window too. We test integer delays 0-20 years. When a shifted year is before 1980, the primary test holds the run's 1980 value fixed. Separate tests use delays at most four years, which need no pre-1980 values, and constant extensions set to the mean, minimum or maximum in 1980-1989. These are sensitivity cases, not bounds on all possible older history.

If weights w are nonnegative and sum to one, a stable mixture gives `y = sum(w v)`. Its attainable set is exactly the convex hull of the finite vectors. We permit arbitrary mixtures across runs, cells and delays. This is more flexible than one physical model, and does not preserve each run's tracer calibration after a delay is added. A failed test is therefore a strong constraint within this finite response library. A passed test shows possibility only. We also test a hull of tile area means. Cell hulls allow arbitrary spatial weights, but require those weights to remain the same in both windows.

The primary rate is the published uniform oxygen-use rate J=3.2 umol/kg/year, with the published depth-dependent runs also included. A wider library scales uniform-rate responses over J=2.5-5.0. Including only the two end rates gives the same convex hull as all intermediate rates. The depth-dependent runs retain their original rates. No new model is fitted to oxygen observations.

A linear program tests intersection with the rectangle formed by the two marginal observed intervals. A second program allows different mixtures w1 and w2 and minimizes their total variation, `TV = 0.5 sum(abs(w1-w2))`. We solve it through shared mass c and separate masses e and l: `w1=c+e`, `w2=c+l`; each mixture sums to one and the objective is `sum(e)`. Only the early coordinate of w1 and the late coordinate of w2 are constrained. This gives a sharp bound for the stated library and interval rectangle. It does not estimate a water transport fraction. Replacing interior points by hull vertices leaves the optimum unchanged: a common decomposition can be applied to both mixtures without increasing total variation, and hull vertices are members of the original library.

## Findings

Fourteen of fifteen tile rectangles intersect both the area-mean hull and the more flexible cell hull. This does not select transport delay as the cause. It shows that these aggregates do not exclude that explanation in those tiles.

The eastern tile at 35-40 N, 130-120 W differs. Its early AOU gain is 33.830 umol/kg, with interval 28.621-39.574. Its later gain is 28.463, with interval 12.910-34.685. No stable mixture fits the two ranges. This remains true in the expanded J library. In the primary library the early mean exceeds every cell/run/delay response by at least 4.846 umol/kg. This point-estimate shortfall is not an uncertainty bound.

A certificate for the primary hull is

`0.8884732969 * early - 0.4589283176 * late - 4.1458603898 <= 0`.

All library vertices obey this inequality to numerical precision. Even the most favorable point in the observed rectangle violates it by 5.3652. The problem is the combination of a large early gain and limited later gain, not merely the amplitude of either change. The complete certificate is supplied. An explicit optimal mixture and a dual objective check are also supplied. For the 22.40% bound, primal and dual objectives agree within 3e-17 and constraint residuals are below 4e-16.

| Added delay limit | Oxygen-use library | Minimum changed mixture weight for the eastern rectangle |
|---|---|---|
| 4 years | Published rates | 30.18% |
| 4 years | Expanded J range | 14.96% |
| 10 years | Published rates | 28.25% |
| 10 years | Expanded J range | 11.55% |
| 20 years | Published rates | 22.40% |
| 20 years | Expanded J range | 9.79% |

Table values use the 1980 constant extension. The four-year tests need no extension. Other tested constant histories give 22.44-25.00% at 20 years with published rates and 10.37-11.16% with the expanded rate range. Thus these specified history changes do not remove the conflict. The exact per-case values are in sensitivity.csv.

If support can change independently between windows, all fifteen rectangles fit the separate coordinate bounds. In the eastern tile, at least 22.4% of weight must change in the primary permissive library, or at least 9.8% with the wider oxygen-use rates. These fractions concern model-cell-run-delay mixtures. Actual sampling reweighting has more restrictions and was not recovered from the source aggregates. A change in sampling, transport, source proportions, or an unmodelled process can all change an effective mixture.

## Interpretation and limits

The source study's proposed slower spread can account for the western shortfall in this test, but a stable positive delay applied to its response library cannot account for the eastern two-window ranges. The next decisive observation test is to compare both windows on exactly the same cell-season support, with one joint cruise bootstrap that shares the early reference. If the eastern conflict persists, model changes must alter response shape, source weights, oxygen use, or another process beyond an added stationary delay. Merely raising oxygen sensitivity within the tested range does not suffice.

This is a conditional falsification of a response family. It is not a rejection of ventilation or outcrop loss. A changed circulation need not equal an extra convolution of the old local response; it can change the routes, source history and residence-dependent oxygen use. Fractional-year delays, delays longer than 20 years, and arbitrary pre-1980 histories are outside the test. Runs are mixed without age recalibration, making acceptance especially weak evidence. The data are on one density surface and have only two late-window aggregates. Marginal intervals do not define a joint confidence level, and the source rounded values to 0.001. We make no basin-wide significance claim. Unequal sampling support can remove the observed conflict. We do not infer respiration, carbon uptake, inventory loss or future oxygen change from this calculation.

## Reproduce and provenance

Job: sci-1107-dell-earth-and-ocean-sciences-741156e9e7dd. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol. The campaign-machine signing key is not a personal authorship claim.

Run `sh files/reproduce.sh /absolute/path/to/separate-output` after unpacking the SCI bundle. Python 3.12 with numpy 2.5.4, scipy 1.18.1, pandas 3.1.1 and matplotlib 3.11.2 was used. Only one compute process is needed. No download is required. Inputs are unchanged licensed aggregates in files/inputs; files/provenance.json records exact hashes, source entries and the verified campaign ZIP path. No raw shared dataset was read. Raw-data reconstruction is documented by the cited source publication and is not required for this aggregate analysis.

The script recreates all result tables and the PNG. It writes the large vertex table as CSV; the signed copy uses gzip compression. Synthetic feasible and infeasible linear programs and 100 random convex combinations pass the supplied validation checks. Code, inputs, results, proof certificate, figure and external-source attribution are preserved here. The source publication's complete bundle was verified before its inputs were used. See files/NOTICE.md for rights and attribution.
