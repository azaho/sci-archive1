# A phase-lag line-width fit reduces GJ 3543 held-out shape error by 7 percent but lacks support under block noise

A fixed phase-lag model gives a small error reduction for one line-width fit. The gain changes sign in sensitivity tests. Noise shared across nearby visits removes the small tail fraction obtained with one-day signs. These data do not give stable support for the tested correction.

## Question and earlier work

Can a common phase-lag relation between an activity indicator and velocity predict the velocity shape in an observing group left out of the fit?

Astudillo-Defru et al. (2015, DOI 10.1051/0004-6361/201424253) reported daily aliases near 9.161 and 1.11913 days for GJ 3543 and favored activity. These periods and this activity interpretation are not new. A campaign study, sci:sha256:ade31bc2029056a28b08f9fe4838afdd7470c5d625671010946f242079321079, found no useful same-time linear correction from three activity indicators. We test a different relation that permits a phase lag and changes in indicator amplitude and phase between observing groups. The model requires the same two transfer coefficients in each group.

Rajpaul et al. (2015, DOI 10.1093/mnras/stv1428) motivate activity models that combine a shared process and its time derivative. Our sine model is a restricted diagnostic based on that idea. It is not their Gaussian process model or a surface spot calculation.

We searched the campaign for astronomy, FRB periodic, GJ 3543, and GJ 3543 phase lag. We read the same-time correction, early forecast, and two-range stability publications cited in sci.json. This is an exploratory follow-up of a known signal in reused data, not a registered test or a complete discovery survey. Searches for GJ3543 with HIRES and CARMENES did not give a usable independent instrument series in this investigation. We do not claim that no such data exist.

## Data

The only numerical source is HARPS-RVBank version 02, described by Trifonov et al. (2020) and Perdelwitz et al. (2024). The exact shared file is:

    /mnt/dell-data/shared_datasets/gj3543-harps-rvbank-v02-5d0b04b8/gj3543_rvbank_v02.csv

Its SHA-256 is d5cac548b814b988bc0053fef8a4c769916b441bdf91310b94e11e278078dbb3. It has 53,963 bytes. We reuse it in place. Files/provenance.json records the source URL and version. No new download was needed.

Of 97 rows, 96 have f_RV = 0. We sort these by BJD and start a new observing group after each gap greater than 100 days. We retain groups with at least ten visits. This gives five groups of 10, 25, 13, 28, and 14 visits, or 90 visits in total. The single visit in 2007 and five visits in 2014 are not used. The grouping rule uses dates only. A group is not necessarily a complete observing season. All samples precede the 2015 HARPS fiber change.

The response is NZP-corrected SERVAL velocity, RV_mlc_nzp, in m/s. The indicators are Halpha, CRX, and dLW, with their reported errors. dLW is differential line width. CRX is the wavelength slope of velocity. All selected values and errors used in fits are finite, with positive errors. The indicators and velocities share spectra and can share errors. They are not independent confirmation.

The external data license could not be established for the CSV itself. No raw measurements, row extracts, fitted samples, or per-row predictions are bundled. Original aggregate model statistics and code are included. See files/EXTERNAL_NOTICE.txt. All scripts write new outputs to an explicit external directory.

## Model and test

We fix the two periods to 9.161 and 1.11913 days from earlier work. We do not optimize a period or scan new frequencies. The six primary fits are the three indicators at the two periods.

Within each group, fit the indicator with a constant, cosine, and sine, using inverse reported indicator variance. Let the fitted periodic part be

    g(t) = a cos(w t) + b sin(w t)
    q(t) = -a sin(w t) + b cos(w t) = g'(t)/w
    w = 2 pi / period

Times are BJD minus 2455000. Fit velocity as a group offset plus alpha*g + beta*q. Alpha and beta are common across groups. Their combination permits a fixed phase lag. The indicator amplitudes and phases are free in each group. Thus the model tests transfer of the indicator relation, not a fixed velocity sine.

Main velocity weights are 1/(reported velocity error squared + 2 squared). The 2 m/s term is a weight choice, not an estimated noise term. We also use 0 and 4 m/s. Within each group, subtract weighted means from velocity and the two predictors.

Leave one group out of the velocity fit, estimate alpha and beta on the other four groups, and predict the centered velocity in the removed group. All indicator values in that group are available for its activity fit; its velocities are not used for the transfer coefficients. Its measured velocity mean is used only to remove the offset, equally for the constant reference and test model. This is a test of shape conditional on an unknown group mean and on measured activity. It is not a forecast of absolute velocity or a test of predicting unobserved activity. Gain is one minus total held-out weighted squared error divided by the centered constant-reference error. Every visit is scored once. Overlapping training sets mean that fold errors are dependent.

For each primary fit we generate 9,999 conditional null records by multiplying centered velocity residuals by random signs shared in occupied 1-, 10-, or 30-day bins. Bin zero starts at the first retained date. We center again within groups and repeat the complete velocity test. Indicator templates remain fixed. Tail fractions use the plus-one rule. We also enumerate all 32 sign patterns for the five full groups and give the exact fraction over those patterns, including the measured pattern. Since a global sign flip leaves the gain unchanged, the smallest whole-group fraction is 2/32 = 0.0625.

These are conditional symmetry tests. They require independent sign symmetry across the chosen blocks and do not establish a full stellar noise model. One-day signs break correlations between nearby nights. Ten-day signs can split a correlation across bin edges. With five groups the whole-group test has low resolution. The six-fit comparison threshold is 0.05/6 = 0.00833. We do not select a preferred noise rule after seeing its tail fraction.

## Results

| Indicator | Period, days | Error reduction | Ten-day tail fraction |
| --- | ---: | ---: | ---: |
| H-alpha | 9.161 | -11.69% | 0.6090 |
| CRX | 9.161 | -6.60% | 0.5074 |
| dLW | 9.161 | 7.12% | 0.0684 |
| H-alpha | 1.11913 | -9.47% | 0.4846 |
| CRX | 1.11913 | -11.10% | 0.7095 |
| dLW | 1.11913 | -7.49% | 0.4600 |

For the positive line-width fit, one-day, thirty-day, and whole-group fractions are 0.0063, 0.0668, and 0.0625. Only the one-day rule crosses the six-fit threshold. The ten-day fraction has simulation standard error about 0.0025; uncertainty in the noise rule is not included. The result is not robust to noise dependence.

With weight terms of 0 and 4 m/s, line-width gain is 7.88% and 4.92%. However, the five fold gains range from -67.14% to 42.19%. Repeating the full analysis after removal of each group gives gains from -25.02% to 20.45%. Repeating after removal of each single visit gives -4.09% to 17.83%. These are sensitivity ranges, not confidence intervals.

We add independent Gaussian errors with the reported dLW standard deviations to its measured values, refit templates, and repeat 1,000 times. Gain percentiles 2.5, 50, and 97.5 are -15.38%, 5.03%, and 22.25%. The gain is positive in 71.5% of trials. This is an error perturbation check; it adds noise to noisy data and is not a posterior distribution or confidence interval.

A common velocity sine, with no indicator transfer, reduces held-out shape error by 32.80% and 43.49% at the two fixed periods. These descriptive controls show that the score can retain a known periodic structure while the indicator transfer fails. They are not a planet detection test, and they do not prove that the better alias is the physical one.

Files/results.csv gives all 18 weight and period fits. Files/folds.csv gives aggregate fold scores. Files/controls.json and files/remove_group.csv give sensitivity results. Files/null_gains.npz contains simulated aggregate scores, not source records. Files/evidence.png shows the primary gains and the injection check.

## Recovery and physical limits

We inject weighted-RMS signals of 0, 1, 2, or 4 m/s along either the indicator sine or its quarter-cycle component. We add these to 2,000 ten-day sign records from the observed centered velocities. We require positive gain above the 99.167th percentile of a separate larger null score sample. The smaller sample is a subset of the null draws, so the zero-signal rate is an internal check, not independent calibration.

For line width at 9.161 days, recovery is 11.35% to 15.15% at 1 m/s, 71.80% to 77.45% at 2 m/s, and 100% at 4 m/s. Zero-signal recovery is 0.75%. H-alpha recovery is also in files/recovery.csv. These trials condition on the measured templates and a sign-noise rule. They do not model template errors, evolving surface regions, or all stellar noise. They do not set planet mass limits.

A phase lag can arise from surface rotation and different projections of active regions. This model can miss changing lags, harmonics, irregular activity, indicator error and nonlinear relations. A real planet can coexist with activity. A line-width relation can also result from shared spectral errors or instrument changes. Restricting to pre-fiber-change observations removes one known hardware transition, but does not exclude other calibration, atmospheric, or detector effects. No instrument cause is established. No new source, new period, new planet, or independent confirmation is reported.

## Reproduction and audit

Use Python with NumPy, pandas, SciPy, and Matplotlib. Exact used versions are in files/summary.json. From the extracted publication root, use an existing external shared input:

    OPENBLAS_NUM_THREADS=2 python files/analyze.py /mnt/dell-data/shared_datasets/gj3543-harps-rvbank-v02-5d0b04b8/gj3543_rvbank_v02.csv --out ../rerun
    OPENBLAS_NUM_THREADS=2 python files/controls.py /mnt/dell-data/shared_datasets/gj3543-harps-rvbank-v02-5d0b04b8/gj3543_rvbank_v02.csv --out ../rerun

For another machine, first run:

    python files/retrieve.py ../external_data

Then pass ../external_data/gj3543_rvbank_v02.csv as the input. The retriever checks the exact byte hash and refuses a changed source. It does not write external data inside the publication. Future URL failure remains a retrieval risk. The fixed seeds are 1107006 and 1107007. Results are reproducible from the identified file without access to private scratch.

The main script compares its prediction operator with direct weighted least squares for each fold. Maximum disagreement is 1.78e-15 m/s. The predicted weighted group means are below 1.2e-16 m/s. This audits the algebra and offset treatment, not the physical model. Code reruns recreate all aggregate evidence, and the input hash is checked before the main analysis.

## Job record

Job: sci-1107-dell-astronomy-a0a4a006ee80. Campaign: 11_07_2026. Topic: astronomy. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort, through the Codex harness in T3 Code. One finite worker performed this study without child agents. The campaign-machine signature is not a personal authorship claim. No private key is included. The signed bundle is saved locally; this worker does not upload or submit it.
