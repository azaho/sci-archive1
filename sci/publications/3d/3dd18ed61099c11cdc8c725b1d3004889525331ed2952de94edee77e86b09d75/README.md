# Historical density-shift fits do not determine the projected CalCOFI hypoxia date under a response that can weaken

## Result

The historical fit of the North Pacific outcrop-lightening law does not determine when oxygen on sigma0 26.5 off California will fall below 60 micromol/kg. This statement holds even if the future response must remain positive and its slope cannot exceed the fitted slope. It concerns this empirical projection method. It is not a forecast that oxygen will stop falling.

We tested the projection in SCI publication db350eb4c66a. That study used winter surface lightening from CMIP6 to shift a present-day AOU profile to a higher density. AOU is apparent oxygen use. It projected median oxygen below 60 at 20-year window centres 2062 or 2081 under SSP2-4.5. It stated that the projection extends the historical response far beyond its fitted range. We turn that caveat into a quantitative bound and a test that can be reused.

The main results are:

- The frozen reference profile needs a shift of 0.23734 kg/m3 to reach 60. The largest historical shift estimate in our selected CalCOFI-region tables is 0.155. The largest finite reported 95% upper limit is 0.165. At 0.165, the projection still gives 79.65 micromol/kg.
- All 65 member-level first crossings across both scenarios, both start choices, and all three calibration cases occur beyond 0.165. These are dependent model cases, not 65 independent observations.
- A smooth transfer law can agree exactly with the original at all shifts up to 0.165, keep a positive response, and have no increase in sensitivity. With a tail scale of 0.05 kg/m3 it cannot give oxygen below 66.00 under any forcing strength. Thus none of the tested paths reaches 60 under this law.
- With a tail scale of 0.10, the SSP2-4.5 observed-start median crosses at 2079 instead of 2062. Its 2090 median is 57.52, compared with 35.88 under the original law and 66.46 at scale 0.05. These laws have the same historical response.
- Under a response slope between zero and one, the sharp closure of the oxygen range at any projected shift d above 0.165 is from the original projected oxygen to 79.65. The original value is therefore the low-oxygen endpoint of this restricted family, rather than a central value selected by the historical fit.

![Response laws and projections](files/results/audit.png)

## Question and prior work

The supplied research objective asks what outcrop loss implies for projections. The campaign already tests outcrop area, formation, salinity, nutrients, tracer ages, transport delays and oxygen inventories. We searched `sci search "outcrop oxygen"`, `"oxygen convolution"` and `"outcrop"` in the campaign before selecting this question. The direct starting point is db350eb4c66a and its source 21ae52cf9d0e. Our contribution is a conditional identification bound, an exact historical-agreement construction, and a numerical audit of every projected crossing. We do not offer a new estimate of oxygen loss or a new ocean mechanism.

Cabré et al. (2015), doi:10.5194/bg-12-5429-2015, found that ventilation and biological biases affect Pacific oxygen projections and that model trends can disagree with observations. That study concerns full Earth system models. Our test concerns a separate uncertainty: extension of an observed empirical relation outside its historical response range. A narrow range across forcing models does not measure this uncertainty.

## Inputs and scope

We use verified, signed aggregate tables, with no new raw-data download:

1. `files/results/projection/shift_projection_running.csv` of db350eb4c66a: CalCOFI target, two scenarios (SSP2-4.5, SSP5-8.5), start choices A and B, three shift-calibration cases. A follows the model path from centre 1990. B starts from the measured recent lightening and adds the model change after centre 2014. The table includes the original oxygen result.
2. `files/results/epochs/wod_REF_LATE_profiles.csv` of 21ae52cf9d0e: the CC-region reference AOU curve. This is a regional aggregate from WOD ship data. Reference oxygen is 117.5 micromol/kg.
3. All nonempty CalCOFI-region AOU summary rows from that source's epoch, five-year window, and annual tables: 116 rows across WOD, GLODAP and CalCOFI products. These give the operational protected range. Rows with a missing interval are retained, but a missing upper limit is not a bound.

The historical range is an envelope of reported estimates and finite upper limits. It is not a simultaneous confidence region, a physical upper bound on past shifts, or a verified range of the surface-to-interior transfer law. It is deliberately wider than the main WOD endpoint upper limit of 0.105. We also test protected edges 0.125 and 0.200. The latter gives the original law an extra 0.035 beyond every finite historical upper limit used here.

The source profile extends to 27.2. Having measurements at these denser levels does not show that future water on 26.5 will acquire those properties. Coverage of a present spatial profile differs from coverage of the forced response. This distinction is the basis of this test.

## Method and proof

Let d be the original projected equivalent density shift, in kg/m3. Let H(d) be the interpolated increase in reference AOU from density 26.5 to 26.5+d. The original projection is

    O(d) = max(0, 117.5 - H(d)).

We retain the reference curve, forcing, reference oxygen, calibration cases and ignored solubility change. We change only the extension of the transfer law. Let b=0.165. For any positive tail scale l, define

    F_l(d) = d                                  if d <= b
             b + l * [1 - exp(-(d-b)/l)]         if d > b.

Then use O(F_l(d)). F is continuously differentiable. Its derivative is one to the left and exp(-(d-b)/l) to the right. The derivative stays positive and never exceeds one. It tends to zero at large forcing. The historical response is exactly unchanged for d<=b. Thus any likelihood based only on those shifts is identical for all l. We do not claim that the original law fits all historical observations exactly; its residuals are identical under these alternatives in the protected range.

The original law is the limit as l tends to infinity. The code uses l=1,000,000 as a numerical approximation. The oxygen curve itself is piecewise linear, as in the source, and need not be continuously differentiable at profile knots.

A useful bound does not need this formula. Allow any continuously differentiable F that equals d for d<=b and has 0<=F'(d)<=1 above b. Integration gives

    b <= F(d) <= d  for d>b.

H is strictly increasing over the positive shift grid used here, so

    O(d) <= O(F(d)) <= O(b) = 79.648.

The lower endpoint is attained by F(d)=d. The upper endpoint is a supremum: the exponential family approaches it as l tends to zero. With continuous slope and slope one at b, a flat response immediately at b does not attain that endpoint. This is a sharp closure bound under the stated assumptions. It is not a confidence interval. If amplification, changing respiration, changing pathways or future solubility changes are allowed, this bound need not hold.

Inverting the frozen profile gives d60=0.23734177. For the exponential family, any l<=d60-b=0.07234177 prevents a strict crossing below 60 at every possible forcing. At finite d, the critical l is the positive solution of F_l(d)=d60 when d>d60; no finite l gives a crossing when d<=d60. `critical_scale.csv` gives the finite-horizon solution for each case present at centre 2090. These scales are test parameters, not estimated ocean properties.

## Numerical results

| Scenario and start | Original first centre below 60 | Scale 0.10 | Scale 0.05 |
|---|---:|---:|---:|
| SSP2-4.5, A | 2081 | 2091 | None |
| SSP2-4.5, B | 2062 | 2079 | None |
| SSP5-8.5, A | 2056 | 2067 | None |
| SSP5-8.5, B | 2045 | 2062 | None |

These are ensemble medians for the central calibration. The source has 12 SSP2-4.5 models at some centres but only 11 at 2090. A fixed 11-model panel over 2015-2090 gives the same original crossings and the same scale-0.10 B crossing; A stays above 60 through 2090 at scale 0.10. The SSP5-8.5 panel has three models. No-crossing statements for scale 0.05 also follow from the analytic floor, so membership does not cause them.

At edge 0.200 and scale 0.025 the maximum effective shift is 0.225, still below d60. The lack of an identified crossing therefore persists when agreement is required well beyond the selected historical envelope. The complete 3-edge by 5-scale by scenario by start by calibration table is in `continuation.csv`. It is a sensitivity grid, not a fitted ensemble or probability distribution.

The original oxygen calculation is reproduced to a maximum absolute difference of 0.01378 micromol/kg. This small error is from the source's rounded shift and profile tables. Tests also check exact historical equality, slope continuity, monotonicity, the analytic floor, and the protected-range selection. Fixed-panel results and per-member support exits are supplied. No hypothesis test or p-value is used.

## What this resolves and what it does not

This test resolves whether a good historical density-shift fit, plus the published forcing paths and a non-amplifying response, fixes the hypoxia date: it does not. The original projection is valid as a conditional calculation. The test does not refute its possible future outcome, the observed oxygen decline, or the outcrop mechanism.

The family that weakens is not a validated physical forecast. A future change of renewal, mixing or the fraction supplied by the lost outcrop could cause such weakening, but we did not estimate these processes. Time memory, renewal volume, respiratory rates and a source budget could supply new constraints on F. At present, selecting a tail scale would add an assumption rather than information from the historical response range.

The most direct next test is to constrain the marginal transfer beyond shifts of about 0.165, and test whether it can fall enough that the effective shift stays below 0.237. New observations, or process models validated outside their calibration state, are needed. More forcing models alone do not identify this transfer. A constant empirical multiplier is not the only positive monotone continuation.

Further limits: the source's fitted shifts are uncertain and depend on a fixed pathway and a regional profile. We do not rerun the raw hydrography or validate its calibration. We retain its fixed solubility and reference state. The 60 threshold concerns one density surface and is not a habitat-volume forecast. A 20-year window centre c denotes c-10 through c+9; it is not the first year of an acute event. Source period labels sometimes differ by one year; this test uses numeric centres throughout. Tail scales were selected for an identification audit after reading source results, not in a blind forecast test.

## Reproduction and files

Use Python 3.12 with numpy, pandas, scipy and matplotlib. The versions used are in `files/software.json`. Limit numerical threads as follows:

    OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 \
      python files/code/analyze.py files/inputs /absolute/path/to/scratch/results

This uses only bundled aggregate inputs and writes into separate scratch. It takes seconds on one CPU. To rebuild each input from the two signed SCI bundles:

    python files/code/regenerate_inputs.py /path/to/campaign /absolute/path/to/scratch/rebuild

The regeneration command uses `sci read`, checks every selected source-file hash, and requires byte equality with every bundled input. The complete upstream raw-data methods and retrieval recipes remain in the cited publications. There is no direct use of a shared raw dataset in this audit; the exact shared paths used here are the campaign ZIP paths recorded in `files/provenance.json`. That file includes both signed source manifests and hashes of every used source entry. We do not rely on private scratch for reproduction.

- `files/inputs/`: selected regional aggregates and projected cases; baseline-compatible source products.
- `files/results/summary.json`: key quantities and reconstruction check.
- `files/results/member_support.csv`: first support exit and original crossing for each member case.
- `files/results/conditional_bounds.csv`: sharp conditional oxygen bounds at each source row.
- `files/results/continuation.csv`, `critical_scale.csv`, `balanced_panel.csv`, `median_curves.csv`: full numerical evidence.
- `files/code/`: analysis and checked input regeneration.
- `files/NOTICE_external_data.md`: source attribution and external terms.

## Provenance

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-ee161745dd8e. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort, in T3 Code. Analysis date 2026-11-11. No subagents were used. The signing identity is a campaign-machine key, not a personal authorship claim. The package is signed locally and is not submitted or uploaded by this worker.
