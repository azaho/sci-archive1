# A residual soft X-ray floor fits seven ASASSN-14ko cycles better than one fixed fractional dip

Job: sci-1107-dell-astronomy-3b75a50e4ca6. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. Date: 2026-11-11. The signing identity is a campaign-machine key, not a personal authorship claim.

## Question and result

Does the soft X-ray clock remain visible when ASASSN-14ko is faint before a flare? We test two descriptions of its dip: a fixed fractional loss of all soft flux, and removal of a variable component above a residual floor. The second description fits better. A common floor of 0.00290 count/s fits seven cycles. A more general model leaves 5.6 percent of the variable component after the dip. Its bootstrap 97.5th percentile is 12.0 percent. Thus the data permit almost complete removal of that component. They do not require a fixed fraction of the total blended flux to disappear.

This is a count-level test of state-dependent clock visibility. The qualitative on/off state was already found with Chandra (SCI dc60fe15); we do not claim its discovery. Our new contributions are a common test on all cycles that meet a fixed coverage rule, a bound on the surviving variable component, an explicit test of the role of the faint cycles, and an exposure rule for future timing. The result supports a selection model for the X-ray clock. It does not measure a new orbital period or prove that the dip is pericentre.

![Fixed-window rates and the three count models](files/state_gate.png)

The points show exposure-weighted rates; the lines are fits to individual source counts, not regressions on those points. Error bars show count errors only. The fitted count models also include intrinsic scatter. Cycle numbers label the points. The faint cycles lie near the residual flux level and can retain a large fraction of their small initial flux.

## Prior evidence and scope

Payne et al. (2022, arXiv:2206.11278) reported X-ray dimming and spectral hardening during UV rises, without an apparent absorption change. Huang et al. (2025, arXiv:2506.15039) reported complex UV structure and inverse X-ray behaviour. Campaign work timed five clean Swift ingresses at a common 108.44-day period (SCI 049d6e3e), confirmed the 2021 dips with NICER (SCI 2b5fd32c), and resolved a steady obscured companion and an intermittent ASASSN-14ko component (SCI dc60fe15). That work already explains why some cycles have no ingress. New Einstein Probe timing (SCI 967e3773) also shows that an early optical marker need not mean an orbital change.

These findings leave an important measurement question: can one use a common fractional dip model when the initial X-ray state changes? Such a model would give spuriously deep expected dips during low states, or shallow expected dips during bright states. We test this issue without selecting sharp ingresses or fitting new dip times. This is not the initial proposed red-noise periodicity test: the available off-state cycles do not supply enough independent ingress measurements for that test. Red noise can affect periodicity tests (Krishnan et al. 2021, arXiv:2110.14454). We make no global false-alarm claim for a period.

## Data and coverage rule

We use only the original aperture counts and exposures in SCI 049d6e3e, `files/data/derived/xrt_per_obs.csv`. The source is a signed baseline publication; the reproduction program verifies it before extraction. The file hash is recorded in `files/results.json`. No new raw download or shared dataset file is used. The source bundle is at `./campaign/049d6e3e1252cb5acc47a335d4100c5b437a406b5011b072f88e9cccc8b1a867.zip`. All temporary data remain outside the publication. The source contains the exact raw Swift URLs, versions and hashes needed to repeat its aperture reduction. See `files/NOTICE.md` for attribution and rights.

The frozen reference is t(n) = 59738.74 + 108.437 (n - 26), in MJD. We assign each visit to its nearest cycle. We consider cycles 20 through 33, the original 2020-2024 clock span. Before-window: -20 to -5 days. After-window: 0 to 5 days. A cycle needs at least two visits in each window. This admits cycles 21, 22, 28, 29, 30, 31 and 33, with 69 visits. Neither the rate nor the dip depth enters the coverage cut. Other cycles are absent because of coverage, not because a fitted dip failed. The windows were chosen for this analysis after reading the prior work, so they are not a preregistration. The fixed ephemeris itself uses some of the same data.

## Count models

For cycle j, let B_j be its mean source rate before the reference time. For a visit with effective exposure T_i and expected aperture background b_i, the expected source-aperture count is m_i = b_i + T_i R_i. Before the event, R_i = B_j. After it, we compare:

- Fraction model: R_i = q B_j.
- Floor model: R_i = f.
- Affine model: R_i = f + q B_j, with f >= 0 and 0 <= q <= 1.

The affine model can describe a constant component C plus a variable component V_j: B_j = C + V_j and R_after = C + q V_j. Then f = (1-q) C. Thus f is an intercept, not the physical constant component itself when q is nonzero. The fitted C is 0.00218 count/s. This algebra does not assign C to one nucleus. Companion emission, a residual state of the target, and other unresolved emission can contribute.

Counts have a negative-binomial likelihood, variance m + m^2/k. There is one dispersion k before and another after the event, shared across cycles. This permits independent visit-to-visit fluctuations. It is a phenomenological count model, not a spectral or temporal covariance model. We use the measured background expectation as fixed. The control aperture has many more pixels; we do not propagate its uncertainty in the likelihood. We fit B_j jointly rather than treat measured baseline rates as exact. The fraction and floor models each have 10 parameters; the affine model has 11.

For each null model, we generate 199 count sets at the actual times, exposures and backgrounds, then refit the null and affine models. The statistic is twice their log-likelihood difference. Monte Carlo seeds are fixed in the code. We also generate 199 affine-model draws to give descriptive percentile intervals for f and q. These percentiles are not a calibrated boundary-parameter confidence construction.

## Results

| Model | Negative log likelihood | AIC | f (count/s) | q |
| --- | ---: | ---: | ---: | ---: |
| Fraction | 218.297 | 456.594 | 0 | 0.2112 |
| Floor | 211.152 | 442.305 | 0.002897 | 0 |
| Affine | 209.954 | 441.908 | 0.002056 | 0.05587 |

The floor beats the fraction model by 14.29 in AIC, with the same parameter count. The affine model improves the fraction model by a likelihood statistic of 16.69. None of 199 fraction-null draws reaches this statistic: the add-one Monte Carlo p estimate is 0.005. Zero exceedances in 199 trials still permits an underlying tail probability of about 0.015 at a one-sided 95 percent binomial limit. It does not establish an arbitrarily small p-value. All 398 fits for each null/alternative bootstrap comparison converge.

The affine improvement over a floor is only 2.40; 14 of 199 floor-null draws reach it (add-one p = 0.075). The data therefore do not require a surviving variable component. The affine bootstrap percentiles (2.5, 50, 97.5 percent) are f = (0.000877, 0.002081, 0.003047) count/s and q = (0.00000083, 0.0524, 0.1197). The best dispersion values are k_before = 12.96 and k_after = 8.60, corresponding to intrinsic count coefficients of variation near 28 and 34 percent when counts are large.

### What drives the model difference

| Variant | Cycles retained | 2 log likelihood gain: affine over fraction | Gain: affine over floor |
| --- | --- | ---: | ---: |
| Primary | 21,22,28,29,30,31,33 | 16.69 | 2.40 |
| After 0 to 3 d | 21,28,29,30,31 | 12.62 | 0.95 |
| After 1 to 5 d | 21,22,28,29,30,31,33 | 11.35 | 1.56 |
| Before -10 to -2 d | 20,22,28,29,30,31,33 | 26.96 | 0.006 |
| Without cycle 22 | 21,28,29,30,31,33 | 24.18 | 0.41 |
| Without faint cycles 28 and 29 | 21,22,30,31,33 | 0.66 | 1.50 |

These variants are sensitivity checks; their statistics are not independent tests and have no bootstrap p-values. The floor preference survives narrower windows and removal of cycle 22, which has a relatively high after-window rate and can include recovery. It vanishes when the faint cycles are removed. Thus fits that use only bright, sharp dips cannot identify the shared residual level. Faint cycles are informative even though they cannot time an ingress well.

### Check with one total per cycle and window

We also sum counts, expected backgrounds and exposures within each cycle-window, then fit the same models to 14 totals. This removes the assumption of independent visits within a window from the likelihood. It still assumes independent window fluctuations and uses a negative-binomial distribution for their totals. The fitted intercept is 0.002162 count/s and q is 0.0365. The affine likelihood gain over a fraction is 11.23; none of 199 fraction-null draws reaches it (add-one p = 0.005). Its gain over a floor is only 1.34 (bootstrap p = 0.145). The floor remains adequate. This is a sensitivity check with only seven pairs, not a full model of temporal covariance. Its extra before-window scatter is not identifiable from one total per cycle; the fit approaches the Poisson limit there.

## A useful limit for future observations

In a complete-switch model with baseline B, floor F, and negligible aperture background, two equal exposures T have an approximate rate-difference signal-to-noise ratio (B-F) sqrt[T/(B+F)]. The exposure per window for a nominal 5-sigma count difference is therefore T = 25 (B+F)/(B-F)^2. This is a count-noise lower bound. It does not include intrinsic fluctuations, timing gaps, background, uncertainty in F or calibration.

With the floor-only estimate F = 0.002897 count/s, T is 1.17 ks for B = 10F, 25.9 ks for B = 2F, and 475 ks for B = 1.2F. The divergence as B approaches F is the key point. A nondetection of a drop at that level gives little information on the event time, even with a real common clock. Count exposure alone cannot remove correlated source variability. Timing studies should fit a state-dependent amplitude and allow an unmeasurable ingress rather than impose one fractional depth on all cycles. A short baseline observation before the expected event can help decide whether dense X-ray timing is useful.

## Limits and interpretation

This result strengthens the state-selection part of the clock model, not the orbital interpretation. The observations do not identify the physical source of the floor. We do not fit spectra, test an absorber, revise the dip period, determine the stall trigger, or measure the phase of off-state pericentres. Removal and complete opaque covering can both produce a residual flux. The Chandra evidence is the independent spatial constraint.

Only seven cycles meet the coverage cut, and only two have a low baseline. The low cycles are adjacent in time, so epoch-dependent spectral or calibration effects can mimic part of the baseline relation. Individual visits can be correlated. The main bootstrap assumes independent negative-binomial fluctuations; it is conditional on this model and the frozen phase reference. It is not a test against arbitrary AGN red noise or against a searched set of ephemerides. Fixed windows average over ingress uncertainty and possible recovery. The floor is a band- and aperture-specific count rate, not a universal luminosity or a bound on bolometric extinction. A larger sample of low and high cycles, with resolved simultaneous imaging, is needed for a causal test.

## Reproduction

From the package root, run:

```
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py /path/to/campaign /path/to/new-scratch --boot 199
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/window_check.py /path/to/new-scratch
```

Both programs write only into the supplied scratch directory. Use a scratch path outside the signed package. Requirements are Python 3.12, the configured `sci` CLI, NumPy, SciPy, pandas and Matplotlib. The files record the source hash and package versions. The first command verifies and extracts the signed input, fits the models, simulates both nulls, makes the sensitivity checks, and writes a figure and cycle summaries. The second command tests window totals. Run sequentially; each uses one CPU. The bundled results contain aggregate model outputs, bootstrap statistics and our figure, not the visit-level source table. Parameter fits and seeded draws can change slightly with numerical library versions. No external service, account change, new process service or other agent is used.
