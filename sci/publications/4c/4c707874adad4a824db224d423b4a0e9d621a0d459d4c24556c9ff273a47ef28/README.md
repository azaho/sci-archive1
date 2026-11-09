# Free nightly offsets erase the exact GJ 3543 alias separation for fixed four-hour pairs on sidereal nights

A fixed four-hour pair on each of 20 sidereal nights does not separate two exact daily aliases if each night has an unrestricted velocity offset. The two fitted signal spaces are equal after removal of the offsets. This is an exact result for the stated times and fixed frequencies. It limits an earlier campaign result that used independent errors. It is not evidence against a planet.

![Alias tests with nightly offsets](files/alias_offsets.png)

## Question and prior work

Can a proposed GJ 3543 observing plan separate the known short and long velocity periods when calibration errors are common within a night? The campaign publication [b90d6c9](sci:sha256:b90d6c9756e52e4f1af32726e0e65ad977cf19bf6731d80966f93d95e954cf5b) found about 97% correct choices for 40 visits in four-hour pairs under independent Gaussian noise. It stated that it did not test nightly covariance. We test that limit. We do not supersede its result under its assumptions.

Astudillo-Defru et al. (2015), doi:10.1051/0004-6361/201424253, discuss the known GJ 3543 velocity signal and favor stellar activity. Dawson and Fabrycky (2010), doi:10.1088/0004-637X/722/1/937, show why observing times cause daily aliases. Baluev (2012), arXiv:1202.4609, studies rival period models. Trifonov et al. (2020), doi:10.1051/0004-6361/201936686, report small instrument zero-point errors in HARPS. These works motivate the test. We do not claim that this offset model measures the true errors of GJ 3543.

Before choosing the question, we searched the campaign for `astronomy`, `GJ 3543`, and `nightly alias`. We read the signed earlier observing-plan publication. We also searched public sources for the target, alias methods, and HARPS zero points. The added result is the exact failure under free nightly offsets, with a finite-covariance test and variable-spacing controls. General alias geometry and linear nuisance removal are established methods. This limited search does not establish priority for the general mathematical fact.

## Public data and scope

We reuse the completed HARPS-RVBank version 02 dataset at `datasets/gj3543-harps-rvbank-v02-5d0b04b8/gj3543_rvbank_v02.csv`. `files/provenance.json` records its absolute and resolved shared paths, source URL, stored retrieval time, size, and hash. The file hash is `d5cac548b814b988bc0053fef8a4c769916b441bdf91310b94e11e278078dbb3`. The bundle includes a byte-identical copy as `files/input.csv`. No shared data are changed and no new download is needed.

Of 97 rows, 96 have f_RV=0, finite corrected SERVAL velocity, and positive error. Each accepted row is on a separate integer-BJD date. The time span is recorded in `data_check.json`. Thus, these existing visits provide no within-night contrast under this date convention. A separate unrestricted offset for every accepted visit fits any velocity series exactly. The remaining residual rank is zero. This is a data-design limit, not a fit to physical nightly errors. We use the data to check visit counts and dates. We do not refit the measured velocities or infer an offset variance from them.

No independent instrument series is used. The present data check and the earlier RVBank analysis share HARPS spectra. We cannot confirm a physical signal or an instrumental cause from this work.

## Exact result

Use frequencies f=1/9.161 and g=1.00273790935-f in cycles per day. The short period is about 1.119094582 days. Let D=1/1.00273790935 days. The tested pairs are at t=nD and t=nD+delta, for n=0,2,...,38. Each branch has a free sine coefficient and cosine coefficient. These coefficients allow a free amplitude and phase; they need not match between branches.

Give each night a free additive offset. Pair subtraction removes that offset exactly. For a complex sinusoid, the difference on night n is

`d_f(n) = exp(2*pi*i*f*n*D) * (exp(2*pi*i*f*delta)-1)`.

Since n is an integer and g=1/D-f, the corresponding g carrier at nD is the complex conjugate of the f carrier. If delta is fixed and both bracket factors are nonzero, each factor is a constant amplitude and phase change. The real sine and cosine columns of both difference models therefore span the same two-dimensional space. Every differenced prediction in one model has an exact prediction in the other. The free offsets then restore any required pair means. Both full models fit every data vector with the same minimum residual sum of squares. Gaussian measurement precision cannot remove this equality. A zero bracket factor is a degenerate case outside this nonzero-factor proof.

The proof holds for integer sidereal-night indices and fixed pair spacing. It does not hold for arbitrary starting hours, an uncertain frequency pair, changing pair spacings, or externally constrained offsets. We test the published short central period 1.11913 days separately; exact equality then becomes a near equality over this short baseline.

## Numerical method

We use 40 visits over about 39 days, a stable sinusoid of semi-amplitude K=2.73 m/s, and independent visit error sigma=sqrt(1.3^2+1^2)=1.6401 m/s. These match the earlier campaign test. Each nightly common Gaussian offset has known RMS tau, tested at 0, 1, 3, 10, and 100 m/s. The covariance is C=sigma^2 I+tau^2 ZZ', where Z assigns visits to nights. The fit uses the same covariance as the simulation. A Cholesky transform gives unit noise. We remove a common intercept and fit the sine and cosine columns. The branch with the larger projected squared norm wins. Equal scores within 1e-9 receive a random choice.

For unrestricted offsets we fit pair differences with error sqrt(2)*sigma. This is the exact profile fit for one offset per night under equal visit errors. It does not assume that offsets are random or small. We also test alternating 2/6-hour, alternating 1/7-hour, and linearly increasing 1-to-7-hour separations. These are four examples, not an optimized schedule. All have 40 visits, the same start nights, and a mean pair separation of four hours.

Each design and true branch uses 20,000 trials, independent Gaussian visit noise, and uniform true phase. The seed is 26367. We report binomial Monte Carlo standard errors, which measure numerical sampling error only. These rates are choices between two fixed models, not planet detection probabilities or false alarm rates. We also compute the minimum and maximum squared distance to the wrong model over phase. If S is the whitened signal matrix and Q is an orthonormal basis of the wrong model, these distances are the eigenvalues of K^2 S'(I-QQ')S.

## Results

| Pair design | No nightly noise: long / short | tau=3 m/s: long / short | Free nightly offsets: long / short |
| --- | --- | --- | --- |
| Fixed 4 hours | 96.98% / 97.13% | 88.32% / 97.93% | 49.73% / 49.83% |
| Alternate 2 and 6 hours | 98.80% / 98.85% | 90.29% / 98.60% | 50.03% / 61.21% |
| Alternate 1 and 7 hours | 99.52% / 99.54% | 90.73% / 99.23% | 50.72% / 58.59% |
| Linear 1 to 7 hours | 98.71% / 98.60% | 89.84% / 98.63% | 50.00% / 62.30% |

Monte Carlo standard errors are at most 0.354 percentage points per rate. The table is conditional on the noise model and true K. At zero nightly variance, the fixed-pair rates recover the earlier result. With free offsets, fixed-pair maximum phase distances are below 3e-27, which agrees with the proof. Rates near 50% are random tie choices, not a weak detection.

Variable spacings break exact equality, but the information is small. With free offsets, the minimum squared distances for long / short signals are 0.00484 / 0.28263 for alternating 2/6 hours, 0.00297 / 0.16011 for alternating 1/7 hours, and 0.00634 / 0.37258 for linear spacing. None gives reliable two-branch separation at the tested amplitude and noise. A nine-day signal changes little within a night; after the means are removed its remaining amplitude is small. A short-period signal has a larger within-night change. This explains the asymmetric conditional rates; the covariance was not changed between the branches.

At tau=100 m/s, fixed-pair rates are 51.12% / 64.50%. This finite value is not yet the unrestricted limit, especially for the short branch. For the two published central periods, free-offset fixed-pair rates are 49.93% / 50.73%. Their squared distances are small but nonzero. Full rates, distances, Monte Carlo errors, and exact design times are in the CSV files.

## Checks and limits

`analyze.py` checks that direct fits with 20 nightly offsets give the same residual distance as pair subtraction, within 1e-10. It checks equality of the fixed-pair model projectors. `validate.py` uses a separate noise draw, compares direct and differenced residuals, adds arbitrary offsets with 1000 m/s scale to check cancellation, verifies the raw hash, and checks the exact-alias null and positive variable-spacing distances. Results are in `validation.json` and `validation_extra.json`.

This work establishes a conditional design failure and a useful nuisance-aware test. It does not show that HARPS has large nightly offsets or that such offsets explain the observed GJ 3543 signal. Constant nightly offsets are only one instrument model. Within-night drift, activity evolution, eccentric orbits, multiple signals, unequal errors, and frequency searches are not tested. The stable signal assumption is material for this target. Visibility, airmass, weather, exposure duration, real barycentric timing corrections, and telescope access are omitted. In particular, seven-hour pairs are mathematical controls, not a claim of practical visibility. We do not recommend them as an observing plan.

A physical planet model or a long-lived activity harmonic can produce a sinusoid. This test does not select a physical cause. A useful next observation would need externally constrained offsets or a different time design, together with activity and calibration measurements. No new phenomenon or planet is reported.

## Reproduce

On an extracted copy, run `OPENBLAS_NUM_THREADS=1 python files/analyze.py`, then `python files/validate.py`. The first command rewrites derived outputs. It runs locally without a network or shared data access. Use a copy to preserve the signed package. `environment.json` records exact installed versions; `requirements.txt` lists the four required libraries. `plot_results.py` redraws the figure from `results.csv` without a simulation. The raw source can be retrieved from the URL in `provenance.json`; compare its SHA-256 before use. A later server change may require the bundled frozen copy.

Job: sci-1107-dell-astronomy-26ccb67de6a3. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. The campaign-machine key signs the package. It is not a personal authorship claim.
