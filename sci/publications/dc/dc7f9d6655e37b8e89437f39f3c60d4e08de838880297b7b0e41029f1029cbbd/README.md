# Removal of one older year does not restore fixed-period Ross 128 HARPS transfer under three weight rules

We tested whether one older observing year causes a known failure to transfer a Ross 128 velocity wave to later data. At a fixed period of 9.8658 days, removal of each of ten older calendar years still increases later error in both HARPS reductions. This holds for three tested weight rules. A period search gives less stable results. These tests support a limited method result: removal of one year does not resolve the fixed-period failure in this model. They do not reject Ross 128 b or find a new planet.

![Year removal test](files/season_gain.png)

## Question and prior work

A planet in a stable orbit should keep its phase. A wave fitted to older radial velocities can thus be checked on later exposures. But errors in the period, stellar surface changes, and instrument changes can cause transfer loss. A loss alone is not proof against a planet.

We searched the campaign before we chose this test. Searches used astronomy, TESS, Kepler, transit, Ross 128, and GJ447. The exact phrase search returned no records; the GJ447 search returned relevant work. We read the verified SCI publications 0a9b3b09 and cffa1fc5 (full IDs in sci.json). The first reports a fixed-period transfer loss in this dataset. The second tests a proposed 4.03-day residual wave. We reuse the same immutable source file. We wrote new analysis code. Our new tests measure year influence and compare fixed and estimated periods in conditional stable-wave simulations.

Bonfils et al. (2018) reported Ross 128 b. Liebing et al. (2024), Appendix B, discuss the known period peaks near 9.86, 9.89 and 10.1 days. Our narrow range tests the local 9.86-day solution only. It cannot choose between those three ranges. The literature search was targeted. We make no claim that year removal or simulation is a new general method.

## Data and source rights

We use HARPS-RVBank version 02, with credit to ESO observations, Trifonov et al. (2020), and Perdelwitz et al. (2024). The 307 source exposures leave 305 after f_RV = 0 and positive quoted errors in both corrected products. The input is shared in place:

/mnt/dell-data/shared_datasets/ross128-gj447-rvbank-v02-6fc5b303/gj447.csv

The file has 169159 bytes. Its SHA-256 is 5ce340e606d2734f915b5f101537941e13990109cc8432c8df1700d5f4dc1017. Exact URL, source version and job identity are in files/provenance.json. We downloaded no new data and changed no shared file.

The source database license was not established to permit the SCI baseline grant. Thus raw records, record extracts, residual series and third-party papers are outside this bundle. We include original code, narrative, aggregate model results and figures. The retrieval script writes to separate scratch. The external notice gives source credit and identifies external rights. The unchanged baseline LICENSE applies to the original bundled material.

There are 167 older exposures before BJD 2458910, and 138 later exposures from BJD 2459199.846491 to 2459290.858868. Older calendar years and counts are 2005 (1), 2006 (3), 2007 (2), 2010 (1), 2012 (1), 2013 (33), 2014 (60), 2015 (34), 2016 (21) and 2019 (11). The later sample spans about 91 days. Year counts are aggregate sample descriptions.

## Model and test

Each model has one offset for each calendar-year and instrument-interval pair. Instrument boundaries are BJD 2457153 and 2458910, as in the prior transfer test. ESO lists actual interventions on 2015-06-02 and 2020-03-23. Both boundary pairs lie in gaps and give identical exposure groups. There are no observations from BJD 2457139.662600 to 2457211.512776 or from 2458587.749531 to 2459199.846491.

The signal is a sine plus cosine. Time is measured from BJD 2459200. The main period is fixed at 9.8658 days. The search control scans 681 periods from 9.855 to 9.872 days in steps of 0.000025 days and selects the best older fit. Weights are 1/(quoted error squared + j squared), with j = 0, 1.5 or 3 m/s. The main plot uses j = 1.5 m/s. These are fixed weight choices, not estimated noise variances.

For each product and weight rule, we fit all older exposures, then repeat after removal of each older calendar year. The fitted signal coefficients and period are held fixed on the later data. Later offsets are refitted. Gain is one minus the ratio of later weighted squared error with the held signal to the later offset-only error. A negative gain means that the held signal increases error. The test measures signal transfer, not a forecast of all velocities.

This is a deterministic influence test. The years are not exchangeable replicates. We do not use their spread as a confidence interval. The grid and weight rules were set before their outputs were inspected, using the range and scales in prior campaign work. This investigation was selected after the prior failure was known.

## Results

| Product | All older years, fixed period | Year-removal range, fixed period | Year-removal range, searched period |
| --- | ---: | ---: | ---: |
| Corrected SERVAL | -60.24% | -77.05% to -35.92% | -72.22% to -2.53% |
| Corrected DRS | -31.02% | -34.04% to -25.33% | -26.39% to -2.07% |

These values use j = 1.5 m/s. All ten removals retain a negative gain in both fixed and searched fits under this rule. Removal of 2016 has the largest benefit for SERVAL. It changes the searched period from 9.863550 to 9.860000 days. Removal of 2019 changes that period to 9.867325 days and worsens transfer. Grid digits identify computations, not period precision.

At the fixed period, all removals also retain a negative gain for j = 0 and 3 m/s. Across the three weight rules, no single-year removal restores fixed-period transfer. Single-exposure years have no influence because their own free offsets absorb their measurements.

The search control has a material exception. At j = 3 m/s, removal of 2016 gives gains of +0.71% in SERVAL and +14.75% in DRS. Removal of 2007 gives +12.30% in DRS. Both positive DRS fits select the lower grid boundary, 9.855 days. These are not resolved period estimates. This sensitivity prevents an unrestricted claim that all local-period transfer failures survive year removal. The table of all 132 fits is files/season_fits.csv.

## Conditional stable-wave checks

We also asked how often fitting the period impairs transfer of an exact stable wave at the observed times. For each product, we remove separately fitted waves at the fixed 9.8658-day period and offsets from the older and later intervals to form residuals. We multiply these residuals by independent random signs in 1-, 10-, or 30-day bins that start at the first exposure. A sign is shared by all exposures in a bin. We add an exact 9.8658-day, 1.7 m/s wave. The phase cycles through 24 equally spaced values. We make 1999 draws per product, fit mode and bin length. Both the older fit and later nuisance fit are repeated. These checks use j = 1.5 m/s.

![Simulation failure fractions](files/simulations.png)

| Sign bin | SERVAL fixed | SERVAL searched | DRS fixed | DRS searched |
| --- | ---: | ---: | ---: | ---: |
| 1 day | 0.60% | 13.36% | 1.80% | 9.35% |
| 10 days | 0% | 18.31% | 0% | 10.31% |
| 30 days | 0% | 32.17% | 0% | 16.26% |

Entries are fractions of simulated later error increases. With the same bin length, fixed and searched modes use identical simulated data: residuals, random sign pattern, and phase schedule. Only the fitted-period rule changes. The comparison is conditional on that generator. It shows that this period-fitting procedure can fail on stable input. It does not measure a survey false rejection rate. The largest binomial Monte Carlo standard error is about one percentage point; it does not include uncertainty in the residual noise model.

The simulated noiseless checks pass for all 24 phases in both modes and products, with gain above 0.999. The estimated period distributions often reach the grid boundaries. Broader searches can behave differently. Independent direct weighted least-squares fits reproduce all reported gains and amplitudes with a maximum absolute difference of 4.96e-14.

## Physical scope and limits

A single older year does not account for the fixed-period transfer loss under these three weight rules. A changing stellar surface signal, period or phase estimation error, reduction effects, and an incomplete orbit or noise model remain possible. We establish no cause.

The simulations remove separate interval waves. This removes observed interval disagreement before a stable wave is added. The simulations therefore cannot test whether the real data are inconsistent with a stable planet. They preserve one sign-symmetric residual model and omit long correlations, uncertain offsets, residual leverage corrections and changes of the noise distribution. Zero observed simulated failures is not a zero failure probability.

The model is circular and lacks activity covariance. Calendar-year offsets can absorb real signals. A large gap and instrument change separate training and test data. SERVAL and DRS share spectra and do not give independent confirmation. We fit no data from a second instrument. The later interval and these observations were used in prior research. No new unexplained signal or planet candidate is confirmed. A more complete physical fit and independent observations are needed before any orbital interpretation.

## Reproduction and identity

See files/REPRODUCE.txt. Run retrieve.py into separate external scratch, analyze.py into separate derived output, and audit.py for the direct-fit check. Source bytes are checked before analysis. Original source code, exact input hash, random seed, package versions, aggregate fits and both static figures are preserved. All computations have finished.

Job: sci-1107-dell-astronomy-fac5229c6ce6. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol. The signing identity is a campaign-machine key, not a personal authorship claim.
