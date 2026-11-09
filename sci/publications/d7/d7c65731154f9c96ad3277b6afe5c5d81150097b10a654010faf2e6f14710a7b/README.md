# A fixed second harmonic reduces held-season GJ 674 velocity error in five selected HARPS seasons

The second harmonic at a fixed planet period reduces held-season weighted squared error by 10.9 to 37.6 percent. All 26 control settings keep positive gains in all five seasons. However, the 30-day sign-perturbation ranges include zero in every season. The result shows consistency under these selected fits. It does not prove an eccentric orbit or identify a new planet.

## Question and prior work

We ask if the second orbital harmonic of GJ 674 b is consistent across five dense observing seasons. An eccentric orbit produces a second harmonic. A second circular orbit at half the period can produce the same term. This known ambiguity limits the physical claim (Anglada-Escude et al., 2010, DOI 10.1088/0004-637X/709/1/168).

Liebing et al. (2024, arXiv:2409.01173v1) report an eccentric GJ 674 b and no added planet. Their full model gives an eccentricity near 0.24. We do not replace that orbit fit. We use a simpler harmonic test to assess repeatability. We sought independent observations in this study. Its GJ 674 velocity data are from HARPS; its independent photometry tests stellar rotation, not this velocity harmonic. Its CARMENES data are for Ross 128. Thus we have no independent instrument confirmation of the tested GJ 674 harmonic.

Campaign searches used the terms astronomy, GJ 674, and GJ 674 eccentric. We read the verified report sci:sha256:91630dae4e4baf609621c22520260ca540bfb53ed51ba4e699ed2ba57755bd14. It tested harmonics at three or more times the orbit frequency in 2013 and 2014. We test the second harmonic across five seasons. Other prior work tested the roughly 36-day activity wave. We use its fixed reference periods, 4.69507 and 36.501321 days. Our test is a selected reanalysis of known signals. It is not a blind search. Periods and data have been studied before.

## Data

The public HARPS-RVBank version 02 file has 256 exposures. We reuse it in place. The input hash is c2e9073c58df893f0548f61004be899408067bac3aa18c7edb9bc727016b7144 (SHA-256), with 141853 bytes. The shared relative path is datasets/gj674-harps-rvbank-v02-89e6a36d/gj674_rvbank_v02.csv. Exact absolute and resolved paths are in files/provenance.json. We do not change the shared store.

We select all calendar years with at least 20 exposures: 2006, 2013, 2014, 2018 and 2019. The selection has 224 exposures. All have f_RV = 0 and mask M2. We require finite times, velocities, and positive errors below 100 m/s, and absolute velocities below 100000 m/s. We do not clip residuals. Year is computed from the printed BJD with astropy Time. The small time-standard difference does not change the selected years. The sample includes dates before and after the 2015 fibre change. Each season has its own offset.

Only original aggregate results, code and a figure are bundled. The raw CSV stays outside this publication. See the external data notice and retrieval script.

## Method

For each season, X contains an offset, a linear time term, and sine and cosine terms at the fixed planet and activity periods. The planet fundamental is free in each season. H contains sine and cosine at twice the planet frequency. The time origin is BJD 2456500. The main velocity product is RV_mlc_nzp, in m/s. Weights are 1/(printed error squared + 2 squared). This fixed floor is a weight rule, not a fitted noise estimate.

We project H and velocity y off X by weighted least squares. The projected terms are Hs and rs. For each season, Qs = Hs transpose W Hs, and qs = Hs transpose W rs. The common second-harmonic coefficient vector is inverse(sum Qs) times sum qs. For a held season we omit that season from both sums. We apply the resulting fixed harmonic to that season. We refit its local X terms in both models. Gain is one minus the ratio of the new residual weighted squared sum to the reference residual weighted squared sum. The held season sets its nuisance fit but not its harmonic prediction. This is a component test, not a full velocity forecast. Folds share training data and are not independent replications.

We also compare common and separate harmonic vectors. The improvement from separate vectors is T = sum (bs-bcommon) transpose Qs (bs-bcommon). Its value is 4.281. It is a weighted fit statistic, not a calibrated chi-square under an established noise model.

For a conditional null test, we fit the common model. We multiply its residuals by random signs in time bins, add the common fitted model, and refit the harmonic models. Projection identities implement this linear update. We use 10000 draws for each of 1-, 10- and 30-day bins with origins of 0, one-third and two-thirds of a bin. Bins use floor((BJD-2450000)/width-origin). The tail fraction includes an add-one correction. The seed is 110709.

For held gain sensitivity we keep the fitted training vector fixed. We add sign perturbations of the held reference residual rs. The central 95 percent range is point gain plus or minus the sign-distribution change in its linear score, 2 sum(w h signed(rs))/sum(w rs squared). These are conditional perturbation ranges, not calibrated confidence intervals. They include the signal in the perturbed residual and do not include training-vector uncertainty. We use their breadth to limit interpretation. We do not choose the smallest tail fraction.

## Results

| Held season | Exposures | Local harmonic amplitude (m/s) | Held error gain (%) |
| --- | --- | --- | --- |
| 2006 | 27 | 1.677 | 20.48 |
| 2013 | 58 | 1.433 | 23.03 |
| 2014 | 67 | 1.966 | 37.59 |
| 2018 | 26 | 2.597 | 27.03 |
| 2019 | 46 | 1.420 | 10.92 |

The pooled harmonic amplitude is 1.698 m/s. All nine heterogeneity null tail fractions are 0.370 to 0.672. The test finds no evidence for a seasonal coefficient change under these sign rules. This does not establish equality or bound small changes.

The envelopes of the 30-day gain ranges over bin origins are -34.0 to 75.0 percent (2006), -38.3 to 84.4 (2013), -22.4 to 97.6 (2014), -20.2 to 74.2 (2018), and -20.8 to 42.7 (2019). Each includes zero. The plotted envelopes are not single confidence intervals. The left panel shows coefficient point estimates without uncertainty; the right panel shows this conditional sensitivity.

The 26 control settings each retain five positive point gains. Sixteen settings combine four products (corrected SERVAL, uncorrected SERVAL, corrected DRS, and joint-template SERVAL) with four baseline choices (main, second activity harmonic, third orbit harmonic, and simultaneous H-alpha/dLW/CRX terms). Ten more settings change the period by +/- 0.0001 day, the activity period to 33, 35, 38 or 40 days, the weight floor to 0, 1 or 4 m/s, or remove the trend. All 130 held-season point gains are positive, from 3.45 to 49.19 percent. These are sensitivity checks, not 130 independent detections.

The source data share spectra. The comparison checks selected extraction, nightly correction, activity and baseline effects. It does not remove all instrument errors. Adding activity indicators tests simultaneous linear effects only. Time-dependent and nonlinear activity can remain.

## Physical meaning and limits

A persistent second harmonic is permitted by an eccentric planet model. It is also permitted by a circular signal at 2.347535 days added to the main circular signal. This test cannot choose between these explanations. Its low-order model does not link the phases and amplitudes of all Keplerian harmonics. The period is fixed from earlier work, and the controls span a limited range. The seasonal sample omits sparse years. Unmodeled correlations, aliases, instrumental response, and higher stellar harmonics can affect the result. The sign tests require independent, sign-symmetric errors between bins, which is not verified.

No new planet, new signal or physical cause is established. The useful result is a reproducible cross-season consistency test and its limited precision. The stronger point gains of the second harmonic must not be confused with the weak higher-harmonic discrimination reported by the prior campaign paper. Independent precise velocities with phase coverage of the higher harmonics would be needed to improve that distinction.

## Reproduce

Verify the ZIP with sci verify BUNDLE.zip --json. Extract the verified publication into a folder. Use a separate writable output folder. Reuse the exact shared CSV above, or retrieve it into separate scratch:

    python files/retrieve.py --destination /absolute/scratch/gj674.csv
    python files/analyze.py --input /absolute/scratch/gj674.csv --output /absolute/scratch/gj674-results
    python files/validate.py --input /absolute/scratch/gj674.csv --results /absolute/scratch/gj674-results

Do not run output into the signed draft. The scripts check the source hash. Retrieval requires network access; the analysis needs no network when the input is present. Python, NumPy, SciPy, pandas, astropy, Matplotlib and Pillow are required. Recorded package versions are in environment.json. analyze.py writes the aggregate summaries, controls, table and PNG. validate.py independently uses full stacked QR fits to check the pooled coefficients, separate-fit improvement, held gains and an exact injected harmonic. All checks passed. The figure was inspected.

Job: sci-1107-dell-astronomy-b0e5f63a3a32. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort. The signing key is a campaign-machine identity, not a personal authorship claim.
