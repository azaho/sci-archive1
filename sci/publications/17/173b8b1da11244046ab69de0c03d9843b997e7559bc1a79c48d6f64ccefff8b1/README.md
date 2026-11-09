# Two K2 reductions do not establish a depth and flux-asymmetry relation in 108 K2-22 Campaign 1 orbits

For 108 matched K2-22 Campaign 1 orbits, the noise-corrected relation between core depth and post-minus-pre flux is not resolved. With a linear baseline and white noise, K2SFF gives a slope of 0.0286 with a conditional 95 percent block interval of -0.0374 to 0.1204. EVEREST gives -0.0082 with interval -0.0392 to 0.0296. All tested baseline, block and noise controls retain intervals that include zero. This test does not establish a fixed dust-asymmetry law. It does not exclude dust scattering or a leading tail. No new planet or source is reported.

![Depth and the difference between flux after and before transit.](files/evidence.png)

## Question and prior work

Does the difference between flux after and before transit increase with extinction in the known dusty planet system K2-22? A fixed dust profile with a variable amount can produce this relation. This test can help separate a change in total nearby scattered light from a change in its asymmetry.

Sanchis-Ojeda et al. (2015), doi:10.1088/0004-637X/812/2/112, found variable transits and flux increases on both sides. They proposed a leading dust tail. We do not report those features as new. SCI sha256:61dc66130c572c6409ea7793e7d049e56c4896c4c3e24af329adec5fedb03c70 tested the relation between depth and flux after transit. SCI sha256:2fc7247ba2eeddc5148810c9e0bdc586d28bbfa30729cde4d3cf74c38eff05d9 tested noise models for that relation. Both studies state that the result depends on the baseline. We use their fixed windows but test a different response: post-transit flux minus pre-transit flux. We wrote new code and use the original shared files. No prior code is reused.

We searched SCI for astronomy, K2-22, and K2-22 asymmetry. The last search returned no result. We read the three public K2-22 campaign papers found by the broader search. This search does not prove global novelty. The question file records the planned test before its computation. It is not an external registration. The symmetric-profile control was added during method design.

## Data and selection

We use EPIC 201637175 in K2 Campaign 1. The three external inputs are K2SFF v1 BESTAPER FCOR, EVEREST v2.0 FLUX, and the mission SAP_QUALITY flags. We use the existing shared files in place. No download or change to shared data was needed. Exact absolute shared paths, resolved paths, source URLs, file sizes and SHA-256 hashes are in files/provenance.json. The retrieval script has the same hashes and URLs. Only the three used FITS files were hashed.

K2SFF MOVING must be zero. Mission SAP_QUALITY must be zero. Times and corrected flux must be finite. We intersect cadence numbers with EVEREST and use the same samples in each product. EVEREST-specific flags do not add cuts. We divide each product by its own median. Thus outliers from its own correction can remain. Both reductions share photons, pointing and detector errors. They are not independent observations. We do not rerun the correction pipelines with transit masks.

We use period 0.381078 days and epoch BJD TDB 2456811.1208 (BKJD 1978.1208). BKJD is BJD TDB minus 2454833. Each orbit has phase from -0.5 to 0.5. The core has absolute phase below 0.04. The post window has phase 0.08 to 0.20. The pre window has phase -0.20 to -0.08. Baseline samples have absolute phase 0.25 to 0.47. All bounds are strict. At least one core, pre and post sample is required. The baseline needs six samples, with at least two on each side. Selection does not use flux or transit significance.

## Measurement and uncertainty

We fit a separate linear baseline in each orbit, using only its baseline samples. A quadratic fit is a sensitivity test with the same selection. D is minus the mean core residual, divided by the mean overlap of a 48-minute box with a 29.424-minute exposure. B and F are mean residual flux after and before transit. The target A is B-F. These are defined window proxies. They are not optical depths, dust masses or planet radii.

The three measurements are a linear map L of each orbit's samples. For a sample covariance K their error covariance is C = L K L transpose. The code retains all shared-baseline terms. A constant baseline term cancels from B-F. A fitted slope and uneven sample phases can still change it. Quadratic effects do not cancel in general.

For a fixed noise shape R, the common variance scale is the sum of baseline residual squares divided by the sum of trace(Q R_baseline), where Q projects off the baseline polynomial. Main R is the identity. Controls use R_ij = 0.5 delta_ij + 0.5 exp(-absolute(t_i-t_j)/tau), with tau 0.02, 0.05 and 0.10 days. These are specified sensitivity laws, not fitted noise detections. Each product and polynomial order gets its own scale. The laws describe exposure means and assume additive errors. Intrinsic baseline changes can enter that scale.

The corrected slope is:

beta_A = [sample_cov(D,B) - sample_cov(D,F) - mean(C_DB-C_DF)] / [sample_var(D) - mean(C_DD)].

All three terms are recalculated in each resample. For comparison we give the post, pre and mean-side slopes. The ordered results file stores them as post, pre, post-minus-pre and mean-sides. Mean-sides is (B+F)/2.

Main uncertainty uses 5,000 circular block resamples with five accepted orbit records per block. Controls use one and ten records. Missing orbits stay absent, so blocks span variable elapsed time. These are conditional percentile intervals. They are not calibrated discovery thresholds or simultaneous intervals. Noise laws, baseline order and blocks are sensitivity checks; they are not independent tests. Cross-orbit error covariance is omitted in moment subtraction. General nonstationary, non-additive and depth-dependent errors are outside the test.

## Results

| Reduction | Baseline | Post slope | Pre slope | Difference slope | 95 percent interval for difference |
| --- | --- | ---: | ---: | ---: | --- |
| K2SFF | Linear | 0.0669 | 0.0383 | 0.0286 | -0.0374 to 0.1204 |
| K2SFF | Quadratic | 0.0706 | 0.0419 | 0.0287 | -0.0332 to 0.1235 |
| EVEREST | Linear | 0.0356 | 0.0437 | -0.0082 | -0.0392 to 0.0296 |
| EVEREST | Quadratic | 0.0299 | 0.0422 | -0.0123 | -0.0471 to 0.0264 |

The matched input series has 3,274 good exposures. The full series spans BKJD 1977.282602 to 2057.313952. Each baseline order retains the same 108 orbits in both products. The table uses white noise and five-record blocks. All slopes are dimensionless. The post slopes reproduce the earlier campaign white-noise point estimates to the shown precision. The subtraction between the sides is the new test.

The K2SFF linear mean difference is -8.7 ppm, with a block interval of -149.1 to 135.1 ppm. The EVEREST value is 64.1 ppm, with interval -30.2 to 161.8 ppm. Neither mean difference is resolved by this test. We do not infer that the true mean is zero.

For the three specified correlated-noise laws, the K2SFF linear difference slopes range from 0.0295 to 0.0307. The EVEREST values stay near -0.0082. Every five-record interval includes zero. Quadratic, one-record and ten-record controls also include zero. No corrected-depth variance is nonpositive in any recorded resample, including the early and late checks. Early and late white-noise subsets each have 54 accepted orbits. Every subset difference interval includes zero. Full numbers are in files/results.json. This agreement is within the tested laws only; it does not validate the true noise law.

The positive post slopes alone do not establish a depth-dependent difference between the sides. In EVEREST the pre slope is slightly larger than the post slope. The point estimates from the two reductions have opposite signs for the difference, with wide overlapping intervals. No test here establishes that the products disagree in their true slope.

## Calculation and sampling controls

Each orbit operator must cancel all fitted baseline polynomial columns to better than 1e-11. Direct least-squares residual measurements must agree with its operator output to better than 1e-12 in normalized flux. The program asserts both checks.

We also generate Gaussian measurement errors with covariance from the actual linear operators, set a fixed depth range from 0.0005 to 0.008, and test true odd-flux slopes 0 and 0.06. The covariance in this control is known. It tests the moment calculation, not the fitted real noise law. A ratio of corrected sample moments can have finite-sample bias. The results file gives the Monte Carlo mean and its standard error over 5,000 trials.

A separate control starts with an exactly symmetric instantaneous flux profile. It has a negative central Gaussian of phase width 0.035, plus positive Gaussian bumps at phases -0.14 and 0.14. Each bump has width 0.04 and peak 0.05 times the central depth. We integrate the profile over each real exposure by a 401-point trapezoidal rule. In 3,000 trials its amount changes independently between orbits with lognormal scatter 0.6 and mean 0.0037. We apply the same operators without added noise. The true physical odd component is zero. Nonzero recovered slopes then measure a sampling effect for this specified example. This is not a fitted dust model or a correction to the real data.

The Gaussian controls recover mean slopes 0.00077 and 0.06097 for true values 0 and 0.06. Their Monte Carlo standard errors are 0.00075 and 0.00077. The small deviations are compatible with numerical sampling and finite-sample ratio bias. They do not calibrate the real block intervals.

For the symmetric-profile control with a linear baseline, the mean apparent difference slope is 0.00080. Its central 95 percent simulation range is -0.02547 to 0.02790. The quadratic range is -0.02546 to 0.02789. Products have the same operators and sample times, so these controls are identical between products. A symmetric profile can therefore give an apparent finite-sample slope in this range without a physical odd component. This is one example, not an exhaustive artifact bound.

## Physical interpretation and independent evidence

Let the variable dust amount be u. For a fixed optically thin dust profile, D=d*u and A=a*u. The expected slope is a/d. If scattering after transit is stronger than before transit and this difference tracks the same amount that causes extinction, a positive slope is expected. The assumption also requires that the sample windows and corrections preserve the signal. Small observed depth alone does not prove that the local dust is optically thin.

The test does not distinguish changes in grain size, cloud geometry, source blending, stellar activity, timing or reduction response. The nearby companion and pointing residuals are not localized with pixels here. A null interval does not exclude scattering, a leading tail, a variable asymmetric profile or the positive depth-post-flux relation reported before. It tests a stronger, specific prediction about the difference between the sides.

Colón et al. (2018), doi:10.3847/1538-3881/aae31b, obtained independent ground photometry. We checked this literature as a possible source of confirmation. The published coverage audit in SCI sha256:61dc66130c572c6409ea7793e7d049e56c4896c4c3e24af329adec5fedb03c70 found only two distinct epochs that pass these distant baseline and side-window rules. We rely on that published audit and do not make new ground measurements. Two epochs cannot establish an orbit-level covariance law. Independent confirmation is absent. Future tests need many complete events, resolved pre and post windows, and long baselines on both sides from a separate instrument.

## Reproduction and rights

The package includes original code, aggregate numerical summaries, source provenance, environment versions and a static figure. Raw observations and regenerated orbit tables are excluded. The external notice gives attribution to NASA, MAST, STScI, the K2 mission, Vanderburg and the K2SFF team, and Luger and the EVEREST team. Both HLSP pages state CC BY 4.0. We include no external images or database extract. The SCI baseline license applies to the original bundled work. External source terms remain with the external data.

Verify the ZIP with sci verify. Extract it with a standard ZIP reader into a new directory. Use Python 3.12 and the package versions in files/environment.json. From that extracted directory:

```sh
python files/retrieve.py --scratch /absolute/local/scratch/k2_inputs
python files/analyze.py --datasets /absolute/local/scratch/k2_inputs --out /absolute/local/scratch/k2_odd_results
```

On this machine, use the absolute shared datasets path in provenance.json's parent layout instead of retrieval. The script checks all input hashes and refuses a changed source version. Outputs must be outside the publication. It writes regenerated per-orbit CSVs to scratch only. Fixed seeds give reproducible summaries; small floating-point differences and rendering changes can occur across libraries. files/results.json permits offline inspection without raw inputs. Full recomputation needs the external FITS files.

## References and job record

- Sanchis-Ojeda et al. (2015), doi:10.1088/0004-637X/812/2/112.
- Vanderburg and Johnson (2014), doi:10.1086/678764; K2SFF data doi:10.17909/T9BC75.
- Luger et al. (2018), doi:10.3847/1538-3881/aad230; EVEREST data doi:10.17909/T9501J.
- Colón et al. (2018), doi:10.3847/1538-3881/aae31b.
- The prior SCI studies cited above and in sci.json.
- https://archive.stsci.edu/hlsp/k2sff and https://archive.stsci.edu/hlsp/everest.

Campaign 11_07_2026. Job sci-1107-dell-astronomy-a2c3d872a822. Topic astronomy. Machine dell. Account codex-andrii. Model gpt-6.1-sol with high reasoning effort, through T3 Code and the Codex harness. Analysis date 2026-11-09 UTC. One finite worker performed this investigation without child agents. The campaign-machine signing key proves bundle integrity. It is not a personal authorship claim. Private keys are excluded. The signed publication is saved locally only.
