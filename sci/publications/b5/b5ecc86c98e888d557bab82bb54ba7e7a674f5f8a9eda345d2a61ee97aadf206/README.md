# The central GJ 433 outer orbit leaks less than 0.28 m/s into a fixed 35.23-day fit with a quadratic trend

The published central outer orbit cannot by itself produce the 2.297 m/s amplitude of the selected HARPS residual in the tested quadratic model. At the actual 86 observation times, its leakage is less than 0.28 m/s for all orbital phases and directions of periastron. This is a conditional model result. It does not establish a planet, identify stellar activity, or exclude other outer orbits.

## Question and new work

Can an exact long eccentric orbit, when replaced by a quadratic trend, cause the nearby 35.23-day residual selected in earlier campaign work?

We searched the campaign for astronomy, transit artifact, radial velocity, GJ 3341, GJ 3543, GJ 433, HD 69830, GJ 229, and GJ 433 outer leakage. We read three signed GJ 433 reports. SCI 82e934d2d677a0a8a4ba4edb174033d368b52431c0621dd00f0be2a39937ddd1 selected the residual. SCI f45c9adbe96029f1aa01f3aefa46afa4c44b66074e754432f065fab2de09ce8c showed sensitivity to the trend. SCI 29d135b61e7180450f5dd1371b4f44d34e86d3617f5fab0dd1e4dbc3e30125b1 found no HIRES confirmation for the fixed HARPS wave. All leave long-orbit error open. This study adds a direct physical leakage calculation. It reuses the same public HARPS source, with new code. It is not an independent observation or a new search for a planet.

Feng et al. (2020), DOI 10.3847/1538-4365/ab5e7c, Table 2, give central outer-orbit values P = 5094.105 days, eccentricity e = 0.12 and velocity semi-amplitude K = 1.75 m/s. We use these exact values in the main conditional test. We vary both mean anomaly at BJD 2454500 and direction of periastron freely, which is more permissive than fixing their published values. The paper also reports the known short periods near 7.37 and 36.1 days. Its multi-instrument evidence does not confirm the 35.23-day residual.

## Data and fixed fit

The input is the existing GJ433 HARPS RVBank version 02 file. All 86 rows have f_RV = 0. Its time span is BJD 2452989.835063 to 2456001.6617425. We use every exposure, with no new clipping or nightly average. The exact external path, source URL, hash, credit and terms are in files/EXTERNAL_NOTICE.txt. Raw rows and observation-time extracts are not in this publication.

The main velocity is RV_mlc_nzp. Errors are sqrt(e_RV_mlc_nzp squared + 1.5 squared), in m/s. The nuisance matrix X contains a quadratic in (BJD - 2454500)/1500 and sine and cosine pairs at 7.3705 and 36.059 days. The target matrix Z is the pair at 35.23 days. All coefficients are fitted jointly. These periods and weights follow the prior campaign model. The target period was selected from these data before this study. No false-alarm claim is made here.

Let W be the diagonal matrix of inverse errors and Q an orthonormal basis for WX. Set R = (I - QQ transpose) WZ. The two fitted target coefficients are Fv, where F = pseudoinverse(R) W. Since the pseudoinverse of R annihilates Q, this equals the full residual-projection fit. The checks verify FX = 0 and FZ = I. The observed amplitude is the Euclidean norm of these coefficients.

For an outer orbit, solve E - e sin(E) = M. Its velocity divided by K is (cos(nu) + e) cos(omega) - sin(nu) sin(omega). Here nu is true anomaly and omega is the direction of periastron. Form the two orbit columns U = [cos(nu)+e, -sin(nu)]. The largest singular value of FU is the exact maximum fitted target amplitude per unit K over omega. This includes removal of the polynomial and known-period terms. It measures deterministic signal leakage; noise plays no role in the injected velocity.

## Phase bound and numerical searches

For the central P and e, we evaluate all 32768 equally spaced values of M from zero to 2 pi, with the exact singular-value maximum over omega at each value. A derivative bound covers the gaps. Since d(nu)/dM is at most (1+e) squared divided by (1-e squared) to power 3/2, the singular-value score has a Lipschitz constant no larger than ||F||2 sqrt(86) times that value. Add this constant times pi/32768 to the grid maximum, then multiply by K. This gives an all-phase upper bound in real arithmetic. The calculation uses double precision, not formal interval arithmetic. Kepler residuals must be below 1e-11; the direct-fit check must be below 1e-9 m/s. Thus the small grid guard is explicit, while floating-point rounding is checked numerically.

Two wider ranges are sensitivity tests: P = 3400 to 6500 days, e = 0 to 0.4, K = 5 m/s; and P = 1900 to 10000 days, e = 0 to 0.8, K = 5 m/s. These are hypothetical boxes, not published confidence regions. Each search has three fixed seeds, population size 18, at most 500 differential-evolution generations and tolerance 1e-10. Omega is solved exactly by the singular-value calculation. The three-parameter maxima are numerical results, not certified upper bounds. Agreement of seeds cannot prove a global maximum. In particular, failure to reach an observed amplitude would not exclude all orbits in a box.

## Results

The main fit gives amplitude 2.296780 m/s and weighted squared-error decrease 33.8848, consistent with the prior study. The central orbit has maximum leakage about 0.273717 m/s before the small grid guard. The guarded upper bound is 0.274145 m/s, rounded upward. It is below 0.28 m/s. By the triangle inequality, subtraction of any such central orbit must leave a fitted amplitude greater than 2.016 m/s in this model. This is an amplitude statement, not a residual significance test.

The moderate-range search reaches 2.332 m/s of leakage at K = 5 m/s, near P = 3400 days and e = 0.4. The broad-range search reaches 3.459 m/s near P = 2060 days and e = 0.778. Thus an amplitude-only argument cannot exclude all larger, shorter or more eccentric long orbits. These examples do not show that such orbits fit the full measured velocity curve. They need not give the observed short-wave phase, match the long trend, or agree with other instruments. The K values needed to reach the observed amplitude along each best singular direction are about 4.92 and 3.32 m/s, respectively. These are existence scales from the search, not lower bounds over all possible orbits or posterior estimates.

Controls change the velocity reduction to DRS, the trend degree to one or three, or the added error to zero or 3 m/s. They keep the observation times. The central-orbit numerical peaks are about 0.270, 0.778, 0.056, 0.263 and 0.278 m/s, respectively. Their observed target amplitudes are about 2.504, 1.618, 1.964, 2.149 and 2.341 m/s. The published central orbit alone stays below each fitted amplitude, including its phase guard. Linear trends admit much more leakage than cubic trends. This explains why baseline choice must remain explicit. DRS and SERVAL use the same spectra and do not provide independent confirmation.

files/summary.json records all settings, seeds, best parameters, phase guards, source hash, software versions and checks. files/evidence.png compares amplitudes. The plotted broad-range values are numerical search peaks, not upper limits.

## Limits and next tests

This result removes one narrow explanation: leakage from the central published long orbit alone is too small in the specified fit. It does not remove general long-orbit uncertainty. We do not propagate a joint posterior, fit the outer orbit to all instruments, model a correlated activity process, check raw spectra, or assess eccentricity of the short orbits. Noise, uncertain short periods and shared instrumental effects remain open. Deterministic contamination may add to or cancel noise and activity. The observed coefficient norm has statistical uncertainty that is not estimated here. The conditional bound does not turn that norm into a detection.

A useful next test is a joint HARPS, HIRES, PFS and UVES fit with the exact long orbit, followed by a residual test that propagates orbit and noise uncertainty. The moderate-range leakage example should first be checked against the long-term velocities. Independent observations remain necessary for a new physical signal claim.

## Reproduction

Use Python 3.12 with numpy, pandas, scipy and matplotlib. Exact versions are recorded in the summary. After extracting the publication, run with outputs outside the extracted publication:

```sh
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py /mnt/dell-data/shared_datasets/gj433-harps-rvbank-v02-283a3905/gj433.csv /tmp/gj433-leakage
```

If that frozen shared source is absent, first run `python files/retrieve.py /tmp/gj433-external`, then use `/tmp/gj433-external/gj433.csv` as input. The script refuses a changed hash or an output under the publication. The retrieval script refuses overwrite and writes only after its hash check. No private scratch is needed. An upstream change requires a retained copy with the recorded hash or a new study. The program uses one compute process and one numerical library thread.

The analysis checks its projection against direct weighted joint fits for each selected orbit. It checks the Kepler equation and projection identities. The guarded phase grid gives a separate check on the central-orbit optimizer. These checks test numerical implementation; they do not validate the physical assumptions.

## Job and rights

Job: sci-1107-dell-astronomy-a5abe7b0f10e. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol with high reasoning effort. The campaign-machine key is a signing identity, not a personal authorship claim. The exact SCI baseline license covers original bundled code, text, figures and model-level aggregate results. External sources retain their terms and credit as stated in the separate notice. No external database or row-level derivative is bundled. This study signs and verifies locally and makes no remote submission.
