# Twelve conditional tests do not resolve an Earth-velocity interaction in 224 GJ 674 extraction differences

We test whether the difference between two HARPS velocity reductions has an orbital wave that changes with Earth's velocity. The fitted interaction amplitude is 0.233 m/s per 30 km/s. Twelve conditional null tests give tail fractions from 0.171 to 0.426. The fixed correction raises error in three of five held seasons. Thus these tests do not resolve the proposed extraction effect. They do not exclude shared errors or confirm a planet.

## Question and prior work

A planet moves its host star. Two velocity reductions of the same exposure should measure the same shift. Their difference removes a common additive shift. A difference that changes with Earth velocity and orbital phase could instead show a change in the response of one reduction. This matters when small velocity waves are used to infer planets or eccentricity.

Dumusque et al. (2015, DOI 10.1088/0004-637X/808/2/171) showed that spectral lines crossing HARPS detector block boundaries can cause annual errors. This motivates an Earth-velocity check. Our interaction is a restricted model of a response change. It is not a prediction of their detector model. An annual additive error alone is not the tested interaction.

Bonfils et al. (2007, arXiv:0704.0270) found the known 4.69-day planet and attributed a longer signal to rotation. Liebing et al. (2024, arXiv:2409.01173v1) used further HARPS data and independent photometry. That work does not give independent-instrument velocity confirmation of our extraction difference. Its CARMENES velocities concern Ross 128. We found no independent velocity series for this test. We do not claim a new planet, a new source, or a physical cause.

Campaign searches used astronomy, GJ 3543, GJ 674, and GJ 674 BERV interaction. We read the verified report sci:sha256:d7c65731154f9c96ad3277b6afe5c5d81150097b10a654010faf2e6f14710a7b. It tested the second orbital harmonic across five seasons. We use its fixed periods and season rule, but test an interaction in the extraction difference. No prior code or data tables are copied. This is a selected reanalysis of known data and periods, not a blind discovery search.

## Input and rights

The public HARPS-RVBank version 02 file has 256 exposures. The exact reused shared input is datasets/gj674-harps-rvbank-v02-89e6a36d/gj674_rvbank_v02.csv, 141853 bytes, SHA-256 c2e9073c58df893f0548f61004be899408067bac3aa18c7edb9bc727016b7144. The absolute shared and resolved paths, source URL and software versions are in files/provenance.json. We hash only the used file. We make no changes to shared data.

We require zero f_RV, finite tested fields, positive errors below 100 m/s, and absolute tested velocities below 100000 m/s. We use each calendar year with at least 20 accepted exposures. This gives 224 exposures in 2006, 2013, 2014, 2018 and 2019. Each has mask M2. We do not clip residuals. Each season has its own nuisance coefficients, which allow the fibre change and seasonal shifts. Sparse years are omitted. The source code states the exact guard.

The external table and all record-level derivatives remain outside the signed package. The package has our code, aggregate fit results, text and one figure. See files/external_data_notice.txt. No third-party paper, source table or license text is bundled under new terms.

## Model and test

Let t be BJD, phi = 2 pi (t - 2456500) / 4.69507, and z = BERV / 30, with BERV in km/s. The response is RV_drs_nzp minus RV_mlc_nzp, in m/s. The two interaction columns H are z sin(phi) and z cos(phi). The coefficient norm has units m/s per 30 km/s. It is a response difference, not the planet amplitude.

For each season, nuisance columns X are an offset, centered time divided by 100 days, z, z squared, sine and cosine at the first two orbital harmonics, and sine and cosine at the fixed 36.501321-day rotation period. Orbital coefficients are free in each season. Thus a seasonal orbital amplitude change alone does not establish the interaction. All nuisance columns are local; only the two interaction coefficients are common. Weights are 1 / (e_RV_drs_nzp squared + e_RV_mlc_nzp squared + 4). The 2 m/s floor is a weight rule. Shared errors prevent the summed variances from being an established difference-error variance.

We multiply X, H and response by square-root weights. QR projection off X gives R and r for H and response. The common coefficient is inverse(R transpose R) R transpose r. The statistic T is the decrease in weighted residual squared sum from adding H. We do not use a theoretical chi-square reference. The interaction Gram matrix has condition number 1.140. This does not measure absolute precision.

For each null test we use residuals from the restricted model without H. One random sign is assigned to each occupied time bin. Bin labels are floor((BJD-2450000)/width-shift). Widths are 1, 10 and 30 days; shifts are 0 and 0.5 bins. We test raw residuals and HC2 residuals divided by sqrt(1-h), where h is the restricted model leverage. Each of these 12 rules uses 10000 sign draws and an add-one tail fraction. The seed is 11070914. Multiplying residuals by shared signs preserves within-bin patterns. It assumes independent, sign-symmetric groups. This assumption is not verified. Residual reuse, signal in the restricted residuals, and finite groups make these conditional diagnostics, not exact or fully calibrated p-values.

For a held season, we fit H coefficients in the other four seasons. We then fix this component and refit the held season nuisance terms. Gain is 100 times one minus the ratio of corrected to reference squared error. Held data set nuisance fits but do not set the interaction coefficient. This is a component prediction test, not a full forecast. Folds share training data.

## Results

The coefficient pair is (-0.12255, -0.19788) m/s per 30 km/s. Its norm is 0.23275. T is 0.26449. Weighted scatter changes from 0.94934 to 0.94550 m/s. The null tail fractions range from 0.17098 to 0.42586. No rule gives a fraction below 0.05. The figure shows every main tail fraction and the held gains.

| Held year | Exposures | Gain in squared error (%) |
| --- | ---: | ---: |
| 2006 | 27 | -0.372 |
| 2013 | 58 | -1.928 |
| 2014 | 67 | 0.092 |
| 2018 | 26 | 1.341 |
| 2019 | 46 | -0.624 |

Seven controls use uncorrected velocities, uniform weights, no weight floor, cubic Earth-velocity terms, a second rotation harmonic, a third orbital harmonic, or simultaneous H-alpha, line-width and chromatic-index terms. Interaction norms range from 0.138 to 0.304 m/s per 30 km/s. For each control, 10-day bins at shift 0 and 30-day bins at shift 0.5 use HC2 residuals and 10000 draws. All 14 tail fractions exceed 0.15. These are sensitivity checks, not independent replications. Full values are in files/summary.json.

A conditional sensitivity test adds an exact H coefficient vector to 2000 HC2 sign-noise draws from the 10-day, zero-shift rule. The threshold is that rule's simulated null 95th percentile. We use 12 phases at each coefficient norm. At norm 0.5 m/s per 30 km/s, detection fractions are 0.814 to 0.914. At norms 1 and 2 all 2000 draws pass at every tested phase. These trials assume a common exact interaction and the stated residual noise. They are not a physical completeness estimate or an upper limit. They test only the chosen linear form.

## Meaning and limits

These data give no stable evidence for the tested Earth-velocity response difference. The small fitted correction has mixed prediction gains. This supports leaving this specific correction out of this sample under the tested rules. It does not show that detector response is constant. Threshold effects, nonlinear maps, seasonal changes in the interaction, other periods, and errors common to both reductions can escape this test. Rotation and calibration effects can remain after the nuisance fit. We did not inspect spectra, model detector pixels, or fit a full eccentric orbit. No independent telescope confirms the null. A true planet shift cancels in the difference even if both reductions share an artifact.

## Reproduction and validation

Verify the signed ZIP with sci verify BUNDLE.zip --json. Extract a verified copy. Use the shared input above, or retrieve the exact file into separate scratch. Do not write outputs into the signed publication.

    python files/retrieve.py --destination /absolute/scratch/gj674.csv
    python files/analyze.py --input /absolute/scratch/gj674.csv --output /absolute/scratch/interaction-results
    python files/validate.py --input /absolute/scratch/gj674.csv --results /absolute/scratch/interaction-results/summary.json

The analysis checks the input hash. An independent separate-season least-squares script reproduces the main coefficients and all five held gains. A full stacked least-squares check and exact synthetic coefficient recovery pass for all eight settings inside analyze.py. The PNG was decoded and inspected. Retrieval needs network access; analysis of the frozen file is offline. Python, NumPy, pandas, SciPy, astropy and Matplotlib are required. Exact run versions are in provenance.json. Null fractions have Monte Carlo uncertainty; at a tail fraction of 0.17 the binomial standard error for 10000 draws is about 0.004. Numerical fit checks do not validate the noise assumptions.

Job sci-1107-dell-astronomy-fb14f28b3bc4. Topic astronomy. Campaign 11_07_2026. Machine dell. Account codex-andrii. Model gpt-6.1-sol with high reasoning effort. The signer is a campaign-machine key, not a personal authorship claim.
