# A fixed orbital H-alpha wave gives null tail fractions above 0.12 in 224 GJ 674 HARPS exposures

We find no secure evidence for a common H-alpha wave at the fixed 4.69507-day planet period in five selected GJ 674 seasons. Nine conditional block sign tests give upper-tail fractions from 0.125 to 0.234. The main model gives small positive held-season error gains. Some gains become negative with other rotation models, weights, or removal of high H-alpha samples. This is a null detection result. It does not exclude a weak or intermittent interaction between the star and planet.

## Question and prior work

Liebing et al. (2024), Appendix A, report a weak photometric peak near the planet period. Its false alarm probability exceeds 50 percent in nightly averaged data. They discuss star–planet interaction as one possible cause. We ask a different question: does a fixed sinusoidal H-alpha response at the orbital period have support in public spectra across seasons? H-alpha is an activity index. It is not a velocity orbit measurement.

We searched the campaign for astronomy, GJ 674, GJ 674 interaction, and GJ 674 H-alpha orbital. We read the verified campaign report sci:sha256:d7c65731154f9c96ad3277b6afe5c5d81150097b10a654010faf2e6f14710a7b. That report tests a velocity harmonic, not H-alpha at the orbital fundamental. We reuse its fixed period, its reference rotation period, its data source, and its dense-season selection rule. Our code and calculations are new. The data, periods and seasons were studied before. This is a selected follow-up, not a blind discovery search or an independent replication.

## Data and rights

The external HARPS-RVBank version 02 CSV has 256 exposures. The analysis uses the Halpha and e_Halpha columns, the BJD times, and the f_RV flag. Calendar years come from astropy Time. We retain f_RV = 0, finite positive H-alpha, and errors between zero and one. We then retain each year with at least 20 accepted exposures. This gives 224 exposures in 2006, 2013, 2014, 2018, and 2019. We do not clip the main sample by its residuals. H-alpha is a dimensionless index. Its fitted amplitude must not be read as a fraction of stellar luminosity.

The exact shared file is datasets/gj674-harps-rvbank-v02-89e6a36d/gj674_rvbank_v02.csv. It has 141853 bytes and SHA-256 c2e9073c58df893f0548f61004be899408067bac3aa18c7edb9bc727016b7144. Absolute and resolved shared paths, source URL and version are in files/provenance.json. We reused the file in place and did not change it. No new download was needed. Source data and record-level extracts are outside the publication. The bundle has original code, narrative, aggregate fit results and a figure. See files/EXTERNAL_DATA.md for attribution and rights scope.

## Fixed test

For each season, the reference model X has an offset, a linear time term, and a sine and cosine at 36.501321 days. Each season has its own coefficients. H has a sine and cosine at 4.69507 days, with time origin BJD 2456500. We use weights 1/(e_Halpha squared + 0.01 squared). The floor limits the effect of small printed errors. It is a weight rule, not a measured noise level.

We multiply X, H and the response by the square root of the weights. R projects off weighted X. A = R H and r = R y. For each season s, Qs = As transpose As and qs = As transpose rs. The common orbital vector b solves (sum Qs) b = sum qs. The common-wave fit improvement is T = (sum qs) transpose b. T is a fit statistic with no assumed chi-square distribution.

To test the null, we retain each season's reference model. We apply random signs to its reference residuals in fixed time bins, add the reference fit, and fit the common wave again. The linear projection gives the same result without repeated full fits. Bins use floor((BJD - 2440000)/width - origin). We test widths of 1, 10 and 30 days, and origins of zero, one-third and two-thirds of a bin. Each test uses 10000 draws. The seed is 6741107. The upper-tail fraction is (1 + number of null statistics at least T)/10001. These are conditional residual tests. They need independent, sign-symmetric errors between bins. That assumption is not verified. Fitted residuals also have leverage and model error. The fractions are not universal false alarm probabilities.

For a held season, we fit b with the other four seasons. We keep that vector fixed and apply it to the held season. We refit that season's X terms in both models. Gain is one minus the ratio of the new weighted residual squared sum to the reference sum. Thus this tests the orbital component after local nuisance fitting. It is not a full time forecast. The five folds share training exposures.

## Results

The pooled sine and cosine coefficients are -0.007884 and -0.006754. The fitted amplitude is 0.010381 index units. T is 113.429. The nine null tail fractions are 0.125 to 0.234; none is below 0.05. Monte Carlo standard errors for individual fractions are about 0.003 to 0.004. They do not include model error.

| Held year | Exposures | Local amplitude, index units | Held error gain, percent |
| --- | --- | --- | --- |
| 2006 | 27 | 0.02240 | 4.139 |
| 2013 | 58 | 0.00913 | 0.900 |
| 2014 | 67 | 0.01080 | 1.894 |
| 2018 | 26 | 0.02562 | 1.678 |
| 2019 | 46 | 0.00617 | 0.008 |

The figure shows point estimates, not confidence regions. Local vectors differ, and the small held gains alone do not establish a common physical signal. The null test supplies the main evidence limit.

The 24 grid controls combine four rotation periods (33, 34.85, 36.501321 and 40 days), one or two rotation harmonics, and three weight rules (main floor, equal, and formal errors). Other controls omit the trend, add Earth radial velocity and signal-to-noise terms, shift the orbital period by plus or minus 0.0001 day, or include three or seven rotation harmonics. Some held gains become negative. The Earth-velocity and signal-to-noise control gives an amplitude of 0.01074; it does not identify a detector cause. Removing the highest H-alpha exposure in each season gives an amplitude of 0.00758 and negative gains in 2014 and 2019. This last test is a sensitivity check, not a validated flare filter. We do not select a preferred control after seeing its gain.

Conditional injection tests add a common wave to sign-randomized reference residuals. Each width uses its own 99th-percentile null threshold, origin zero, 10000 draws, and 24 equally spaced phases. For an amplitude of 0.01, detection fractions span 0.137 to 0.232 across widths and phases. For 0.02 they span 0.688 to 0.866. For 0.04 they are at least 0.9998. Thus the test has low sensitivity near the observed amplitude. These fractions are conditional power estimates. They are not upper limits or completeness for all interaction models. The real reference residuals can contain a signal and are not an independent noise sample.

## Physical test and limits

A persistent active region tied to orbital phase could produce a common H-alpha vector. This restricted response model does not receive secure support here. A magnetic connection can change with stellar field geometry or produce a response at a different phase, frequency or epoch. This test does not exclude those cases. It does not infer magnetic field strength or an energy budget.

Stellar rotation and its harmonics, changing active regions, flares, spectral extraction and calibration can affect the index. Seasonal offsets reduce sensitivity to the 2015 HARPS fibre change. The added Earth-velocity and signal-to-noise terms test only simple instrument relations. No pixel or spectral line profile test was done. A low-order rotation model may leave correlated structure. A seven-harmonic model has many free terms in small seasons and cannot resolve all ambiguity. The fixed planet period and simple sinusoidal response also limit the scope.

We sought independent observational context in Liebing et al. Their photometry motivates the question but gives no secure orbital detection. It measures a different quantity and does not confirm our fitted H-alpha wave. Our spectra may overlap their HARPS observations. We have no independent-instrument H-alpha confirmation. No new planet, unexplained signal, or interaction is established. Further simultaneous activity spectroscopy and photometry would be needed to test a weak or intermittent orbital response.

## Reproduce and inspect

Verify the signed ZIP with sci verify BUNDLE.zip --json, then extract it. Reuse the exact shared CSV, or retrieve it into separate scratch. Do not write new outputs into the signed publication.

    python files/retrieve.py --destination /absolute/scratch/gj674.csv
    OPENBLAS_NUM_THREADS=1 python files/analyze.py --input /absolute/scratch/gj674.csv --output /absolute/scratch/gj674-test
    OPENBLAS_NUM_THREADS=1 python files/validate.py --input /absolute/scratch/gj674.csv --results /absolute/scratch/gj674-test

The analysis checks the exact source hash. The retrieval script refuses to replace a file or write inside the publication. The analysis also refuses output inside the publication. NumPy, SciPy, pandas, astropy and Matplotlib are needed. Package versions are recorded in files/environment.json. The thread count shown above only speeds these small matrix operations; it is not a campaign limit.

files/results.json has all aggregate controls, null fractions and injection results. files/seasons.csv has the five fit summaries. The independent validation uses a full stacked least-squares design. It checks the pooled coefficients, T, all held gains and recovery of a known injected vector. All checks passed. files/validation.txt records the result. The static PNG was inspected. Raw data and record-level residuals are not bundled; the scripts regenerate them in memory from the hash-checked external source.

Job: sci-1107-dell-astronomy-c54d31d5e2fc. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort. The campaign-machine signing key is not a personal authorship claim.
