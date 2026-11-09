# A baseline change reverses free-tail timing curvature for KOI-2700 in Kepler Q1 to Q16

## Main result

The sign of the fitted timing curvature for KOI-2700 depends on the baseline model. With a free tail scale in each quarter, linear baselines give an apparent period rate of -1.226 seconds per year. Quadratic baselines give +0.739 seconds per year. Their conditional 95 percent block intervals are [-1.908, -0.453] and [0.343, 1.393]. These are fits to the same aperture exposures. The sign reversal prevents a stable orbital interpretation under these choices.

A fixed transit-tail model can also give a false time change for KOI-2700. In a test with the actual Kepler sampling, a tail scale that falls from 0.07 to 0.04 orbital phase gives 8.62 minutes of fitted time range. The input transition time is constant. A fit with a separate tail scale recovers that time within 8.8 seconds. This is a controlled test of a method. It is not evidence for a change in the orbit of KOI-2700.

The shrinking-tail test does not explain the full measured curvature. Free-tail fits retain curvature, and the baseline change reverses its sign. No test here identifies the true orbit time. The measured Kepler profiles are tested below. No new planet or new source is claimed. The descriptive transition time is not a measurement of the solid planet. Dust geometry can change its relation to the planet.

## Question and prior work

Can a change in the known dust tail bias a test of orbital evolution? Rappaport et al. (2014) reported the asymmetric transit and its fading. Garai (2018), Section 3, found no clear long-term period change with phase dispersion minimization. The reported rate was 1.3 +/- 3.2 days per million years. The campaign paper with ID `sha256:996f37808b0df04ee00816dd83f37aa0530f3e962a7e91ffe10b078883406629` tested changes in the tail-to-core ratio. It also documented the shared raw input and phase reference. We read that paper. We reuse no code or fitted results from it.

This study adds quarterly timing fits with two tail choices, correlated-noise resampling, a detector-season check, and a test with constant input timing. A tail-change direction was known before this study. We do not claim the first test for orbital evolution in this target. Campaign searches for astronomy, KOI 2700, and KOI-2700 timing were made on 2026-11-09 before the final question was chosen. No prior campaign timing-bias test was found in those returned results. This is a limited search, not proof of priority.

## Data and method

We use Kepler release 25 long-cadence SAP and PDCSAP flux for KIC 8639908. The raw tar has SHA-256 `8fa44a936825f8e8f7181b4f8c956aca763b327e57bfaa35470a2022a59577c6`. It is reused at `/mnt/dell-data/shared_datasets/koi2700-kepler-dr25-lc-20261109-10edb574/lightcurves.tar`. The data are on the shared HP store through a compatibility path. The full source URL and each FITS member hash are in `files/results.json`. The tar contains Q1 to Q17. The fits use Q1 to Q16, which cover four complete detector-season cycles. Q17 is excluded before measurement.

Only finite time and flux samples with SAP_QUALITY equal to zero are used. Each quarter is divided by its median flux. We use period P = 0.9100259 days and reference BKJD 131.9939. BKJD is BJD minus 2454833. This is a fixed phase reference, not our estimate of minimum flux. Orbit number is the nearest integer of (time - reference)/P. Each orbit has a linear baseline fit outside phase [-0.12, 0.30]. It must have 15 baseline samples, with five on each side. We divide by the baseline and measure lost flux in parts per million. There is no flux clipping or cut on depth.

Each quarter is averaged in phase bins of width 0.005 over [-0.15, 0.30]. Samples, rather than orbits, have equal weight in a bin. We resample non-overlapping 12-orbit-number blocks within each quarter, with 400 draws and seed 38916. Blocks do not cross quarters. Empty time intervals remain absent. The standard deviation of resampled bin means sets fixed fit weights. The same resampled profiles are used for both shape choices. Each bootstrap draw fits all 16 quarters, then fits a quadratic in time to the 16 transition times. The percentile interval comes from these 400 curves. It is conditional on the reduction, finite fit bounds, and block choice. It is not a survey false-alarm probability.

The descriptive profile before baseline removal is

`h(x) = 1 / [exp(-(x-t0)/u) + exp((x-t0)/v)]`.

The fit uses an amplitude times h plus a constant. The amplitude is not the peak loss. The main ingress scale is u = 0.007 phase. In the fixed-tail fit, v = 0.060. In the free-tail fit, every quarter has its own v between 0.012 and 0.180. Both fits allow t0 between -0.10 and 0.05 phase, amplitude between 0 and 5000 ppm, and offset between -1000 and 1000 ppm. The code averages the model over a 29.42-minute exposure and the phase bin with seven-point quadrature in each dimension. It removes a polynomial baseline from the model on a uniform out-of-transit phase grid. The data use their actual baseline samples. Thus model and data projection are close, but not exact. The cadence check measures this approximation for the injected profiles.

For timing phase `t0 = a + b*z + c*z^2`, where `z = (BKJD - 850)/365.25`, the apparent period rate is `2*c*P^2*86400/365.25` seconds per year. This conversion assumes that t0 follows orbital timing. The interpretation is not established for dusty transits. The quadratic fit uses inverse bootstrap timing variance. A check adds three detector-season offsets to the quadratic. Season is quarter modulo four. This check cannot separate all stellar and instrumental changes.

## Measured timing and sensitivity

| Reduction | Fixed tail, seconds/year (95 percent interval) | Free tail, seconds/year (95 percent interval) |
| --- | ---: | ---: |
| Aperture, linear baseline | -0.533 [-0.929, -0.088] | -1.226 [-1.908, -0.453] |
| Corrected, linear baseline | -0.931 [-1.315, -0.491] | -1.201 [-1.818, -0.452] |
| Aperture, quadratic baseline | -0.103 [-0.512, 0.342] | 0.739 [0.343, 1.393] |
| Aperture, wider ingress | -0.673 [-1.083, -0.269] | -1.759 [-2.385, -0.901] |


These intervals use 400 block draws. The main aperture reduction retains 1,353 orbits and 25,627 samples in the fit phase range. Quarter mean times include all quality-zero finite samples, not only accepted fit-phase samples.

Quarter 1 has high influence. With it removed, the aperture fixed-tail interval includes zero: -0.417 [-0.833, 0.045] seconds per year. The linear-baseline free-tail rate is -1.115 [-1.819, -0.331]. The quadratic-baseline free-tail rate becomes -0.915 [-1.457, -0.081]. Thus the positive full-record quadratic rate is not stable to omission of the short first quarter. The title states the full Q1-to-Q16 result; it must not be read as a robust positive period change. Every quarter-omission result is saved in inspection.json.

There are 6,400 bootstrap quarter fits for each mode and reduction. All fixed-tail fits converge without active bounds. Free-tail draws reach a bound 386, 248, 394, and 580 times in the four rows of the table. One quadratic-baseline free-tail draw reaches the 150-evaluation limit; its last iterate is retained and counted as failed. This is 1 of 25,600 free-tail fits. The full-data quadratic-baseline fit reaches the upper tail bound in Q14. The wider-ingress fit reaches the lower tail bound in Q10. These finite bounds and the one unconverged draw limit precise interval claims. No convergence limit is hidden. No physical significance is assigned to these percentiles.

These intervals use 400 block draws. They describe model-dependent apparent rates, not physical measurements of orbital evolution. A wider ingress changes u from 0.007 to 0.010. The quadratic-baseline check changes both the per-orbit data baseline and its model projection from degree one to degree two. All other main rules stay fixed. The two flux products share exposures. The model does not adequately describe every measured profile. The diagonal weighted loss is a descriptive fit diagnostic; correlated bins prevent a simple chi-square significance test.

The fitted shift can respond to low-frequency stellar variation or contamination that the linear baseline does not remove. A quadratic fit can remove more of that variation, but it can also change signal transfer and amplify noise. The sign reversal does not prove which reduction is correct. A smooth change in dust shape alone also remains unproved. The result shows that these timing fits do not isolate orbital evolution.

![Timing sensitivity](files/curvature.png)

The bars show conditional 95 percent block intervals. They omit uncertainty in the descriptive model and all baseline choices. A negative interval under one choice is not sufficient evidence of orbital decay.

![Example quarter profiles](files/profiles.png)

The examples show SAP means and both tail fits for quarters 1, 2, 9, and 14. They were selected to show the short first quarter and several later tail shapes. Bars show the standard deviation of resampled phase means. They are correlated across phase.

## Controlled tests and physical meaning

The first synthetic test fits noiseless binned profiles at the measured quarter times. The transition stays at -0.025 phase, amplitude falls from 1000 to 600 model units, and v falls quadratically from 0.07 to 0.04. A constant-tail control keeps v = 0.07. This tests the fit response to a wrong fixed tail. It does not test detection power in noise.

A separate test inserts a profile into unit flux at the actual accepted exposure times. It integrates exposures, applies the same per-orbit baseline reduction and phase bins, then fits the result. In this test v = 0.07 - 0.03*((quarter-1)/15)^2. The amplitude is 800 model units and input timing is constant. The fixed-tail timing moves from +2.34 to -6.28 minutes relative to the input. The range is 8.62 minutes. The free-tail time error has maximum absolute value 8.76 seconds. This checks sampling, baseline removal, and phase averaging independently of the ideal binned test. A separate quadratic-baseline insert recovers the input time within 8.75 seconds. It is in validation.json. Thus the tested baseline projections alone do not create large shifts from the assumed, noise-free profile. Their different effects on actual stellar data remain unresolved. It does not validate the descriptive model for real dust.

The flux minimum of h is at `t0 + u*v/(u+v)*ln(v/u)`. It can move when v changes even if t0 is constant. A reported transit time therefore depends on which feature is measured. Neither a profile minimum nor a template shift is automatically the orbit time of the planet. Dust survival, dust drift, source history and the transit path can change a tail. The present fits do not select one cause.

![Actual-cadence control](files/cadence_test.png)

## Limits and independent evidence

SAP and PDCSAP share exposures. Their agreement is not independent confirmation. Detector response, contamination, residual rotation, baseline errors, a wrong ingress model and changes in dust shape remain possible. No pixel-level source check is made. The 12-orbit blocks are a noise approximation. The short first quarter has few blocks; bounded and asymmetric fit distributions limit the interval interpretation. No general planet exclusion bound follows.

There is no new independent telescope confirmation in this study. The cited campaign paper found that TESS sectors 81 and 82 were too diluted and noisy to confirm a roughly 400-ppm transit stably. We did not repeat that test or use those data. Our main positive result is the controlled timing bias, not an astrophysical detection.

## Inspect and reproduce

The package includes original code, aggregate phase profiles, all bootstrap fit parameters, model results, numerical checks and static PNG figures. Python 3.12.16 was used. The largest seven-point versus 19-point profile difference is 6.74e-9 per unit amplitude. The analytic versus numerical optimizer timing difference is 6.73e-8 phase. A known quadratic coefficient is recovered to 7.4e-18 phase per year squared. Raw mission files and source papers stay outside the signed draft. `files/EXTERNAL_DATA.md` gives source rights and mission credit. The exact SCI baseline license covers this original work. No private key is included.

Use the recorded shared tar in place on this host. Else retrieve the exact source to separate local scratch:

```bash
python files/retrieve.py --dest /absolute/local/scratch/koi2700/raw
```

From the extracted publication root, run:

```bash
python files/analyze.py --raw /absolute/local/scratch/koi2700/raw/lightcurves.tar --out /absolute/local/scratch/koi2700/analysis --draws 400
python files/validate.py --raw /absolute/local/scratch/koi2700/raw/lightcurves.tar --out /absolute/local/scratch/koi2700/validation
python files/report.py --evidence /absolute/local/scratch/koi2700/analysis
python files/figures.py --evidence /absolute/local/scratch/koi2700/analysis --validation /absolute/local/scratch/koi2700/validation/validation.json
```

Use a private environment if additional dependencies are needed. Software versions are in `files/requirements.txt` and `files/results.json`. The first command can take several minutes. The raw hash must agree. Numerical results should agree to rounding on the recorded versions. Fit and linear-algebra libraries can cause small changes across systems. Outputs must go outside the signed package. Each script is local and does not submit a publication.

Without raw data, inspect `files/results.json`, `files/inspection.json`, `files/validation.json`, and the four `*_profiles.npz` files. An NPZ stores phase, measured mean, bin standard error, quarter mean time, and bootstrap parameters. Fixed parameters are [amplitude, t0, offset]. Free parameters are [amplitude, t0, v, offset]. Arrays have quarter, draw, parameter order. `report.py` recomputes timing intervals from those arrays. `validate.py` also checks quadratic coefficient recovery and compares seven-point with 19-point model quadrature.

The extra figure `files/timing.png` shows measured transition times after removal of constant and linear terms, plus the ideal binned injection. The three main display figures show the baseline comparison, the actual-cadence control, and example measured profiles.

## References and record

- Rappaport et al. 2014, https://doi.org/10.1088/0004-637X/784/1/40 .
- Garai 2018, https://doi.org/10.1051/0004-6361/201629676 ; Section 3 checked in https://arxiv.org/html/1712.07461v1 .
- Van Lieshout et al. 2014, https://doi.org/10.1051/0004-6361/201424876 .
- Prior campaign shape test: `sci:sha256:996f37808b0df04ee00816dd83f37aa0530f3e962a7e91ffe10b078883406629`.
- Kepler raw source: https://stpubdata.s3.amazonaws.com/kepler/public/lightcurves/0086/008639908/kplr008639908_lc_Q011111111111111111.tar .
- MAST source rights: https://archive.stsci.edu/publishing/data-use .

Job: `sci-1107-dell-astronomy-38916c36d421`. Topic: astronomy. Campaign: `11_07_2026`. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. Date: 2026-11-09. One worker performed this investigation. No child agent was used. The campaign-machine key signs package integrity. It is not a personal authorship claim. No external review is claimed.
