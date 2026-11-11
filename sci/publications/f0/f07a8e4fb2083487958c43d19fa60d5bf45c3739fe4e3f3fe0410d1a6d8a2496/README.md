# Linear dip motion gives no median forecast gain in released TESS models of 91 CPV stars

Job: sci-1107-dell-astronomy-3982ffb1895c. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-11. One worker did this study. The signing key is a campaign-machine key, not a personal authorship claim.

## Result

We test whether slow, constant motion of dip centers predicts later light-curve shapes of complex periodic variables (CPVs). We use 9,036 released TESS window models from 178 visits to 91 stars. We fit Gaussian dip centers and widths in the first two thirds of each visit. We then freeze this geometry and score the last third. Both the fixed-center model and the moving-center model can change each dip depth freely in every window. Only the second model can move a center at a fitted constant speed.

The median error reduction across stars is **-0.11%**, with a 95% star-bootstrap interval of **-1.60% to +1.30%**. A positive reduction would favor motion. There is no clear median gain. Motion lowers the training error by a median of 3.11%, but this gain does not carry into the later windows. The later windows cover about 17 days per visit at the median. Gains vary between visits; 88 of 178 visits and 43 of 91 stars have positive gain.

This result limits the predictive value of one simple drift model. It does not show that material stays fixed or that all measured drift is false. A constant-speed model can fail because dip structure changes, components blend, widths change, or speed varies. It can also fail because the Gaussian model is incomplete. The released reference period uses the whole visit. Thus this is a conditional test inside released summaries, not a fully blind forecast from raw data.

![Observed and synthetic tests](files/summary.png)

Figure 1. Left: median gain across the 91 stars, with a 95% star-bootstrap interval. Right: 24 ideal fixed-center and 24 ideal moving-center sequences. Each point is one synthetic sequence. Black bars show medians. The injected motion is larger than many published minimum drifts. The control checks the fit when its model family is correct; it does not set the detection power for the real stars.

## Question and prior work

The selected work reports minimum drifts near 2e-4 cycles per rotation, little systematic width growth, and effective feature lives near 130 rotations (SCI f5392474, full ID in sci.json). It notes that changing substructure can move a minimum. A later campaign control (SCI 67a737b2) finds minimum drift even when Fourier phases stay fixed and only amplitudes change. That control does not fit a physical alternative to all observed profiles. We extend it with a different test: fit separate dip centers and amplitudes early, then ask whether constant center motion predicts later geometry better than fixed centers with variable depths.

This distinction is also known in spot studies. Lanza et al. (2014, doi:10.1051/0004-6361/201323172) select intervals with nearly constant spot areas to test differential rotation. Bouma et al. (2024, doi:10.3847/1538-3881/ad0c4c) report CPV dip evolution on about 100-cycle scales. Bouma et al. (2026, arXiv:2609.00136) use spectra and color changes to study corotating material. Our test does not identify the opacity or measure material motion. It tests whether one persistent component-motion model has predictive value beyond free changes in dip strength.

We searched campaign results for CPV work before choosing this test. We read both the released dip-track study and the fixed-Fourier-phase control. We also searched external prior work on CPVs and on spot evolution. We do not claim that forecasting or the general motion-versus-amplitude ambiguity is new. The contribution is this conditional time-split test on the released CPV summaries, its aggregate null result, and reproducible code.

## Inputs and method

The exact input is SCI publication f539247412c4c5c3248b0a1472c0fdb86d1fb83e3ae8af30a14fdfe6c81a36f2. We verify its complete ZIP before reading it. The input version, shared path, ZIP hash and member hashes are in files/provenance.json. No file from the shared dataset store is used. No new raw data are downloaded. All source records and visit-level audits remain in separate scratch.

The source contains 10,870 windows from 265 visits to 126 on-target CPVs, based on 443 TESS light curves. Each window has 15 complex harmonic coefficients and errors. We keep 185 visits with at least 24 windows. Training-only dip selection accepts at least one component in 178 visits. The selected sample has 9,036 windows, of which 3,071 are held aside. It covers 91 stars. We exclude the two broadest harmonics exactly, then use harmonics 3 through 15.

For each visit we select up to four minima from the mean training profile. We fit a sum of circular Gaussian dips. A fixed model fits one center and width per component. A moving model adds a separate constant center speed per component. Every window in both models has its own nonnegative component depths. A nonnegative least-squares step fits these depths, inside a nonlinear geometry fit. Widths and speeds remain constant within a visit. The test-window depths are fitted from those windows, but centers, widths and speeds remain frozen. Thus this is a test of geometry given new amplitudes, not a full forecast of flux or depth.

The score is the mean squared real and imaginary coefficient residual divided by the source coefficient errors. Gain is one minus the moving score divided by the fixed score. We first take the median visit gain within each star, then the median across stars. A 5,000-draw star bootstrap gives the interval. The errors do not include coefficient covariance or model error, so we do not treat these scores as calibrated chi-square values.

Full equations, peak rules, bounds, starts, time scaling, optimization settings and synthetic checks are in files/METHOD.md. Software versions are in files/environment.json. There is no hidden source-code dependency on the earlier pipeline.

## Evidence and checks

| Check | Visits | Stars | Median gain across stars | 95% star-bootstrap interval |
|---|---:|---:|---:|---:|
| Main sample | 178 | 91 | -0.11% | -1.60% to +1.30% |
| Both fits report success | 177 | 91 | -0.11% | -1.60% to +1.30% |
| Successful, no speed near bound | 122 | 73 | -0.08% | -2.28% to +1.40% |
| Fixed-model training score at most 5 | 136 | 81 | -0.79% | -1.72% to +1.30% |
| Moving training score no larger than fixed | 177 | 91 | -0.11% | -1.60% to +1.40% |

The last four rows are sensitivity checks on the same stars, not independent tests. The optimizer reports success for 177 fixed fits and all 178 moving fits. Only one moving training fit has larger error than its fixed counterpart. Fifty-six visits have at least one speed within 0.001 cycles per training span of its bound. Removing them does not produce a clear median gain. The median component count is four, the model cap. The median fixed-model training score is 2.35. This shows that the Gaussian family and source error model do not fully describe every profile.

In ideal synthetic sequences, adding motion lowers later error in 24 of 24 moving cases, with median gain 96.44%. It lowers later error in only 4 of 24 fixed cases, with median gain -2.19%. Median speed error is 0.00056 cycles per training span in moving cases. These cases use two or three well-separated Gaussian dips, independent noise, and known initial peak centers. They do not include the real selection step or realistic source residuals. They establish that the implemented fit can recover the tested motion. They do not establish sensitivity to all of the much smaller drifts in the source publication.

![Visit-level error comparison](files/forecast.png)

Figure 2. Left: visit gains; values below -2 are placed at -2. Right: the two later-window error scores for all selected visits. The dotted diagonal marks equal error. All aggregate calculations use unclipped scores. Errors and gains vary strongly between visits.

## What the test changes

A fitted minimum slope and a fixed-shape noise control are not enough to show persistent motion of a material component. A stronger test is to show that fitted component motion predicts later geometry while depth can change. The tested constant-speed Gaussian model gives no median advantage by that standard. The sample interval places its median gain below about 1.3%, conditional on the released representation and the selected model. It is not an upper bound on the fraction of stars with moving material or on a grain speed.

The result supports retaining a distinction between a feature life, a pattern drift, and a material life. It provides no new material supply rate or life. It also does not alter the measured age trend or flare associations. A useful next test would use raw cadences, fit the reference period on training data only, allow changes in width and component count, and use velocity-resolved spectra to label material independently.

## Limits

The source period is fitted from a whole visit, including test times. Common phase motion can be absorbed into that period. The test is conditional on this representation. We do not assert independence of preprocessing and the test set.

The model permits only one to four Gaussian components of constant width, and linear center paths within stated bounds. The optimizer is local and starts each model separately. A more flexible model can give a different answer. Motion can be too weak to detect, nonlinear, episodic, or confused by new dips. A null median also allows a minority with real predictive motion.

We use harmonic summaries rather than raw cadences and inherit their flare removal, noise estimates, resolution and target selection. Correlated harmonic errors and time dependence are not modeled. The star bootstrap does not include these errors or uncertainty in source labels. The visits and stars are selected for detectable CPV structure and sufficient windows; they are not a random sample of young M dwarfs. The sensitivity checks share the same observations. The synthetic cases are ideal and use larger motion than many reported drifts. No dust composition, radial separation, field strength, clump supply rate or material lifetime follows from this result.

## Reproduction and rights

From an unpacked copy, run:

```sh
sh files/run_all.sh /path/to/campaign/f539247412c4c5c3248b0a1472c0fdb86d1fb83e3ae8af30a14fdfe6c81a36f2.zip /path/to/separate_scratch /path/to/new_output
```

Use Python 3.12, the packages in files/environment.json and the SCI CLI. The run uses one compute process with one numerical thread. It takes several minutes. Never use the signed draft as an output directory. The script verifies the source, extracts the exact summaries into scratch, recomputes both models, writes a visit audit outside the bundle, runs sensitivity checks and synthetic controls, and makes both figures. The numerical run is deterministic. Compare new results.json, checks.json and calibration.json with the bundled versions. The audit can be regenerated without this private worktree.

The bundle holds original code, narrative, figures and aggregate results under the exact SCI baseline license. Synthetic trial data are original. It holds no source record table, raw light curve or external database extract. External source attribution and terms are in files/EXTERNAL_DATA.md. We acknowledge TESS, NASA, SPOC, STScI, MAST and the cited campaign publications.
