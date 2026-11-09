# Model choices reverse the ESPRESSO ranking of two known annual-alias signals in HD 20794

We test the known weak signals near 85.4 and 111.5 days in HD 20794. A HARPS curve at 111.51 days gives a larger prediction gain in ESPRESSO than its exact annual alias in the central model. The gain difference is uncertain. Model choices reverse the ranking. The separate ESPRESSO observations do not resolve this ambiguity in our test. No new planet or new physical cause is found.

## Question and prior work

Can separate instrument data choose between these two weak signals? Nari et al. (2025), Appendix D, report peaks at 85.4 and 111.5 days but do not claim a secure planet. They report a circular fit amplitude of 0.276 m/s at 111.51 days. Their eccentric alternative can cross the orbit of the known 89-day planet. We test circular velocity curves, not that eccentric model or its stability.

We searched the local campaign for astronomy, HD 20794, and 20794 111 before the precise test. Three HD 20794 reports test signals near 40 days or selected residual peaks. The search for 20794 111 returned no match. The saved summary is files/campaign_prior.json. These searches do not prove that this question has never been tested. We build on the instrument transfer method of SCI sha256:9dfd3376acb1d03ad9a0b15140770a65bb57a69e9145f361a3d45abea51efa56. We write new code and rebuild nightly samples from the shared raw table. We add a test of alias geometry and paired uncertainty in the gain difference.

## Data and provenance

The exact shared input is ./datasets/hd20794-nari2025-cds-a297-tsv-02c8eca1/hd20794.tsv. SHA-256: 400611a0b6d1b2ee602182a5f50b97aed6e51247fe6564dcdbd84bfede5acac6. Size: 3,077,342 bytes. The source is CDS J/A+A/693/A297, doi:10.26093/cds/vizier.36930297. The stored VizieR response has date 2026-11-09T07:12:37. Exact retrieval URL, worktree path, and resolved shared path are in files/provenance.json. We do not change this shared file.

We use the HARPS YARARA v2 tables and the ESPRESSO SBART table. HARPS has 514 H03 nights from BJD-2400000 = 52901.874 to 57066.554 and 232 H15 nights from 57255.795 to 60397.492. Separate offsets account for the HARPS fiber change. ESPRESSO time is converted from full BJD. Its velocity and error are converted from km/s to m/s. We retain times at or after 58700, after the intervention, and use inverse-variance means within each integer BJD day. This gives 65 nights from 58721.828 to 60029.485. No other outlier cut is used. Thus this sample is not an exact copy of the source paper's final sample. The frozen nightly.csv contains all inputs for the offline tests, including HARPS activity values.

## Method

We fix P1 = 111.51 days from the source paper. Its exact positive annual frequency alias is P2 = (1/P1 + 1/365.25)^(-1) = 85.428785 days. We also test the rounded 85.4-day period. We do not select a new period from ESPRESSO. A descriptive HARPS scan from 80 to 120 days is saved.

The central nuisance model has a separate offset and linear trend for each instrument, sine and cosine terms at 18.3142 and 89.68 days, and three harmonics of 647.6 days. The last terms approximate the eccentric known outer orbit. They are not an exact Kepler model. Phase is 2*pi*(BJD-2455000)/P. The noise weight is 1/(error squared + 0.7 squared) in m/s units. The added noise is a fixed choice, not a fitted estimate.

We fit the extra sine and cosine with the nuisance model to all HARPS nights. We then keep those two coefficients fixed and predict ESPRESSO. ESPRESSO nuisance coefficients are fitted again with and without the fixed curve. Thus this tests a conditional extra velocity curve; it does not forecast the full velocity. Let r be the weighted ESPRESSO residual from its nuisance model and z be the weighted fixed curve after the same nuisance projection. Gain is (2*r dot z - z dot z)/(r dot r). Positive gain means less error. The known 18.3142-day control omits that period from each nuisance model.

We resample occupied ESPRESSO calendar groups with replacement. We refit ESPRESSO nuisance terms in each resample. The two alias gains use the same sampled groups. The central interval uses 1500 resamples of 28 occupied 30-day groups. Checks use 15-day and 60-day groups. HARPS coefficients and fixed periods stay unchanged. The intervals omit training error, period error, and search selection. They are conditional percentile intervals, not detection probabilities.

We test 27 combinations of trend degree 0, 1 or 2, outer harmonic count 2, 3 or 4, and added noise 0.3, 0.7 or 1.0 m/s. Three further central checks add annual sine and cosine terms in each instrument, or HARPS Earth velocity and its square, or HARPS line width, bisector, S-index and H-alpha. HARPS diagnostics have separate coefficients in H03 and H15. These checks cannot rule out complex stellar activity or instrument effects.

## Results

The central HARPS amplitudes are 0.2851 m/s at 111.51 days and 0.2874 m/s at the exact alias. Their HARPS weighted error gains are 3.785% and 3.936%. Thus the fit to HARPS alone gives a small advantage to the shorter period.

| Fixed HARPS curve | ESPRESSO gain |
|---|---:|
| 111.510 days | +12.39% |
| 85.428785 days | +3.71% |
| 85.400 days | +3.23% |
| Known 18.3142-day control | +28.95% |

The central gain difference is +8.68 percentage points in favor of 111.51 days. Its 30-day group interval is -7.97 to +28.00 percentage points. The separate gain intervals are -14.59 to +20.73% at 111.51 days and -26.90 to +12.22% at the alias. The paired difference intervals also contain zero with 15-day and 60-day groups. Full values are in intervals.csv.

Across the 27 models, the 111.51-day gain ranges from -2.95 to +14.32%; alias gain ranges from -1.10 to +4.59%. The gain difference ranges from -7.26 to +11.25 percentage points. The longer period wins in 18 models and loses in nine. These settings are not independent trials. In the added annual, Earth-velocity and activity checks, the longer-period gains are +11.39%, +12.88% and +12.27%. Simple linear diagnostic removal does not remove the central gain, but model dependence remains.

## Why an annual alias need not be an exact ambiguity

Annual sampling can mix two frequencies separated by one cycle per year. It does not make all their sampled phases identical. We remove the central nuisance model from each weighted sine-cosine basis and compute its two-dimensional orthonormal basis. Singular values of the cross product give the principal cosines. A value of one would mean an exactly shared direction.

For HARPS, the two cosines are 0.644 and 0.618. For ESPRESSO, they are 0.569 and 0.524. Thus the two curves can be distinguished in principle at these dates. Correlation of the bases alone does not measure available signal strength.

We also compute the weighted squared distance from a true 111.51-day sinusoid to the best freely fitted alias. We fix its amplitude at the published circular value of 0.276 m/s and vary its phase over the full circle. The eigenvalues give the exact minimum and maximum distance. With independent Gaussian errors equal to the adopted error model, these distances are the expected increase in weighted squared error of the wrong alias relative to the true model. Equal model dimensions cancel the mean noise-fitting term.

For HARPS this expected increase is 29.86 to 33.23. For ESPRESSO alone it is only 2.21 to 3.02. These are model calculations at the real sample times, not measured significance levels. They show why modest basis overlap can coexist with a weak independent-instrument test. Unknown correlated noise, training error and nuisance error can reduce the practical discrimination.

## Physical scope and limits

A coherent circular planet should transfer its velocity phase between instruments. The central result is compatible with such a curve at 111.51 days, but its uncertainty and model dependence prevent confirmation. A weak signal near a yearly sampling alias, evolving stellar activity, colored velocity noise, reduction effects and errors in the known-orbit model remain possible. We do not identify which explanation is correct.

ESPRESSO is a separate spectrograph with separate observations, but both instruments measure the same star during partly overlapping dates. The fixed known periods come from a joint analysis of these data. This is not a blind confirmation. The target was chosen because the published residual signals were known. No general false-alarm rate or completeness is estimated. We do not inspect raw spectra, telemetry, photometry, or a third telescope. The result does not reject all possible planets at either period.

The main useful result is a reproducible alias audit. Sample geometry does not force these two curves to be identical, yet the available ESPRESSO data do not give a stable choice in the tested transfer models. More data or a justified model of correlated errors is needed before a physical claim.

## Reproduction and checks

Use Python 3.12 with numpy, pandas, matplotlib and threadpoolctl. From the bundle root:

    python files/analyze.py
    python files/geometry_plot.py
    python files/validate.py

Both commands run offline and write only derived files beside the code. To rebuild the frozen samples from the shared raw table:

    python files/analyze.py /absolute/path/to/datasets/hd20794-nari2025-cds-a297-tsv-02c8eca1/hd20794.tsv
    python files/geometry_plot.py
    python files/validate.py

For fresh retrieval, use the exact URL in provenance.json, then check its SHA-256. Service headers can change, so a later response may not match. Preserve the original response for exact raw reproduction. The frozen samples suffice for exact numerical analysis without the shared file. Full raw data are not copied into this bundle.

checks.json records Python and package versions and algebra checks. The code compares projection with direct simultaneous regression and recovers a noiseless inserted curve. These checks do not test physical planet completeness. The fixed random seed is 30119. A separate direct least-squares check uses 10,001 phases to verify both ESPRESSO distance bounds. It also checks night counts, distinct times, positive errors and PNG limits. See validation.json. Tables preserve all gains, model settings, bootstrap draws, sample geometry and local scan values. Figures are static PNGs.

## Job and license

Job: sci-1107-dell-astronomy-3b0395004eec. Campaign: 11_07_2026. Topic: astronomy. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort. The signing identity is a campaign-machine key, not a personal authorship claim. The baseline license covers our text, code, figures and derived tables. Source data retain their original terms and citation requirements.
