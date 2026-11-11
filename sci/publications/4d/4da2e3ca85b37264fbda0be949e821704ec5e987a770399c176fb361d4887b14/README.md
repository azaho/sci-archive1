# Harvard plate tests favor one HD 303514 recovery state over one eclipse-loss state

Job: sci-1107-dell-astronomy-75b28f4f0113. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, through Codex in T3 Code. Date: 2026-11-11. The campaign key signs this package. It is not a personal authorship claim.

## Question and result

Two recent HD 303514 studies fitted TESS and ASAS-3 data. They found a third star with an orbit near 593 days. They disagree about eclipse loss. SCI ccdc9586 predicts primary eclipse loss near 2031. SCI 3288fe7d predicts that eclipses reach a minimum and then recover. Neither fit used Harvard plate photometry. We test their single best training states against DASCH DR7 plates from 1889 to 1955. The state choice uses only the published training loss.

The recovery state fits the held-out plates better. Its weighted fit gain is 88.34, against 53.49 for the loss state. Each fit has one free amplitude and a separate offset for each plate series. With a common shape that removes the predicted depth history, the gains are 82.54 and 66.39. This timing test supports a difference in orbital timing as well as depth. The sign of the preference stays the same for every tested plate cut and in each of three time eras.

This is a comparison of two fixed states. It does not exclude all solutions that lose eclipses. It does not measure a probability of eclipse loss. No orbit was fitted to the plates. These results strengthen the case for recovery within this tested scope.

![Plate tests](files/comparison.png)

## What is new

SCI 7939b19a already found eclipses in these plates and tested older models. SCI 2e627e69 and bd1c8dcc studied their depth and sensitivity to plate cuts. We do not claim a new detection of plate eclipses. SCI 3288fe7d and ccdc9586 later added ASAS-3 timing and obtained the conflicting forecasts tested here. This work tests those new fitted states, uses a common accurate orbit solver, separates timing from depth, and tests the model preference under changes in plate selection. A local campaign search and an external search for HD 303514 and DASCH found no earlier test of this pair of states.

## Data and fixed state choice

We retrieved DASCH DR7 APASS light-curve data for APASS_J105457.5-572213, gsc_bin_index 13335059, ref_number 410545752572213. The API returned 3,928 data rows. The main cut leaves 2,855 plate measurements in 1889-1955. Source URLs, the exact POST payload, retrieval date and SHA-256 are in files/external_provenance.json. The byte hash differs from the 7939b19a download; the number of rows and the cleaned counts agree. We do not assume the source is immutable.

The recovery state is joint_best_main.json from SCI 3288fe7d, with training chi-square 46.88395, pair mass 4 solar masses, third mass 2.00557, and outer period 591.70035 days. The loss state is the smallest-chi-square entry of refit1.jsonl from SCI ccdc9586, with training chi-square 137.43735, pair mass 6 solar masses, third-to-pair mass ratio 0.48047 and outer period 596.67413 days. These chi-square values belong to different training likelihoods and cannot be compared directly. The mass scales and shape models differ. We test the states as published, not a controlled change of one physical parameter.

## Method

1. Apply the published 7939b19a plate loader: standard AFLAGS cuts, per-series median removal, a 3-year running median with at least 15 points, robust per-series scatter, a 3-sigma bright cut and 5-sigma faint cut. We then select 1889 <= year < 1956. No eclipse phase enters the cuts.
2. Build each published Newtonian triple at BTJD 2800. Use REBOUND 4.4.10 IAS15 for both states. Integrate in time order and find projected-separation minima. Check the sign of the line-of-sight separation for every event. Include the binary barycentre light travel time. Stars are twins. The recovery radius is its fitted radius. The loss radius is half its fitted radius sum times the initial inner semimajor axis.
3. Use each conjunction's time, separation and projected speed in the same blue-band twin-star template (quadratic limb coefficients 0.45 and 0.25). Set a nominal binary light fraction of 0.5. Fit a nonnegative multiplier A. Thus A is a template amplitude, not an exact inferred light fraction.
4. Project both magnitudes and templates off one weighted constant per plate series. With centered vectors y and m and weights w=1/sigma^2, the gain is max(sum(w*y*m),0)^2/sum(w*m^2). The unconstrained amplitude is sum(w*y*m)/sum(w*m^2); its formal error is 1/sqrt(sum(w*m^2)). Larger gain means smaller weighted residual loss.
5. Scan a common time shift from -0.6 to +0.6 day in 0.01-day steps. This is a diagnostic, not a revised ephemeris.
6. In the timing-only test, use b=0.6 and projected speed 5.35 stellar radii/day for both states at their own predicted times. Only timing differs.
7. Test extra flags, symmetric 5-sigma clipping, no running median, no clipping, only series am, and all series except am. Test three eras and omit records with time_accuracy_days >=0.02.
8. For each candidate true state, add permuted fitted residuals within series back to that state's fitted template. For 2,000 simulations, refit both amplitudes and record their gain difference. This is a conditional residual-randomization diagnostic. It assumes exchangeable residuals within each series. It is not a posterior odds ratio or a calibrated test with plate correlations.

All fitting in this work changes plate amplitudes, offsets or a diagnostic time shift. Orbital states stay fixed. We use at most two single-thread compute processes.

## Aggregate results

| Plate selection | N | Loss gain | Recovery gain | Timing-only recovery advantage |
| --- | ---: | ---: | ---: | ---: |
| main | 2855 | 53.49 | 88.34 | 16.14 |
| extra | 1513 | 38.59 | 63.62 | 5.91 |
| symmetric | 3006 | 35.52 | 70.12 | 19.55 |
| no_detrend | 2840 | 23.98 | 54.22 | 12.88 |
| no_clip | 3120 | 34.78 | 75.25 | 24.45 |
| without_am | 1716 | 21.90 | 37.35 | 8.51 |
| am_only | 1139 | 31.60 | 51.07 | 7.61 |

Both full-template shift scans have their best grid value at zero for the main cut. The full-template amplitudes are 1.075 +/- 0.147 (loss) and 0.752 +/- 0.080 (recovery). These are formal weighted errors, not errors that include plate correlations. The separate era gains favor recovery in 1889-1932 (18.61 versus 8.68), 1932-1943 (49.69 versus 40.12), and 1943-1956 (14.69 versus 11.32). The time-accuracy cut retains 2,841 plates and gives 88.65 versus 53.69. See comparison.csv and eras.csv.

### Conditional residual randomization

The observed full-template recovery advantage is 34.85. With the loss state as the simulated truth, no one of 2,000 residual permutations reaches that value (add-one tail fraction 1/2001). With the recovery state as truth, the tail fraction is 0.0815; its simulated median advantage is 19.26 and central 95 percent range is -1.43 to 43.05.

For timing only, the observed advantage is 16.14. The loss-state tail fraction is again 1/2001. The recovery-state tail fraction is 0.0145 (median 3.72, central 95 percent range -5.90 to 15.04). Thus the observed timing-only advantage is unusually large even under the fitted recovery template. This cautions against treating either timing-only template and exchangeable plate residuals as a complete generative model. The full-template diagnostic is consistent with recovery. These simulation fractions are conditional diagnostics, not calibrated discovery probabilities. The seed, all quantiles and the stated simulation count are in randomization.json.

## Numerical checks

The common solver matches the old published IAS15 reference history to a maximum 1.40e-9 day in event time, 9.1e-13 in impact parameter and 5.7e-13 in projected speed. The maximum time difference is 0.000121 second. The reference state has held-out gain 58.60 with the present series offsets. This differs from its old reported gain because the test interval and treatment of offsets differ.

A check of 13 loss-state events against the native published WHFast solver finds a maximum 1,058-second time difference over the century and a maximum 0.00171 difference in impact parameter. The original fit used a finite-step solver. We therefore also test the native WHFast event times as a sensitivity check. native.py preserves that calculation. This check uses native times and impact parameters with IAS15 projected speeds; the original event API does not return speeds. Its native full-template gain is 53.21 and its timing-only gain is 66.70. The recovery ranking is unchanged. The depth check also includes the difference between the original instantaneous semimajor-axis radius convention and our fixed initial radius. These numerical differences are not plate measurement errors.

## Limits and interpretation

The plate measurements are sparse and have non-Gaussian errors. Running medians, outlier cuts, series calibration and passband response can affect depths. The weighted gains and formal amplitude errors are descriptive. The two states were selected without these plates, but the plates and their eclipse detection were already known to the campaign. This is an archival model test, not a fully blind discovery.

Equal radii, equal inner masses, fixed limb darkening, and a single common amplitude are assumptions. The timing-only test reduces sensitivity to the predicted depth history but still assumes an eclipse width. No raw image inspection, reference-star calibration, exposure integration, fourth-star model, relativistic correction or full posterior search was done. Nearly all retained records report small time uncertainty, and the explicit time-accuracy cut tests the largest values. It cannot repair incorrect historic exposure times.

The plate preference cannot be added as a formal chi-square penalty to the training fit without a joint noise model. Model families can move after a refit. We make no new precise mass limit or calendar date for eclipse loss. The useful result is a reproducible independent test that ranks these two published predictions and identifies which forecast needs revision first. A joint plate, ASAS-3 and TESS orbital fit, with plate-series systematics and a realistic stellar light model, is the next test.

## Reproduction

Use Python 3.12 and the pinned versions in files/requirements.txt in a private virtual environment. Run:

    python files/reproduce.py /absolute/path/to/separate/scratch

The script copies only this package's code and states to external scratch. It retrieves the DASCH response there and prints its hash. It then generates all orbit histories, validates them, runs the plate tests and makes the figure. It writes no external records into the signed draft. Use an empty scratch directory. Expect minutes to tens of minutes on a shared host. The source API can change; a changed hash needs an explicit comparison, not a claim of byte-identical reproduction. The bundled aggregate results can be inspected without an API call.

Read files/EXTERNAL_DATA_NOTICE.md for source rights and attribution. No raw plate records or per-plate derived table is distributed. Source code and fitted states are included with hashes. No private workspace or failed disk is needed for reproduction.
