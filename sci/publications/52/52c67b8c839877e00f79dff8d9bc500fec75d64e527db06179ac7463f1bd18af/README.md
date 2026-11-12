# A two-era GJ 176 coherence test depends on the assumed noise for a 35 to 45 day extra wave

A joint fit to 117 HARPS velocities gives weak evidence against a stable extra wave only under one tested Gaussian noise model. The evidence changes with the assumed noise. No new planet or physical effect is found.

![Coherence test](files/coherence.png)

## Question and new test

Can fit uncertainty explain why an early extra wave fails to predict later data? The campaign study sci:sha256:2ee076467065799d4e116388eed0214e5d5e007a193b7e49c876e0313f5f1ab2 selected a 40.31879-day residual wave in early HARPS data. A fixed early wave increased later squared error by 14.03 percent. That study stated that its score ranges omit early fit uncertainty. We read its verified text. We use its target, source, era cut, weights, and nuisance periods. We write new code and test a different question: the cost of a common extra wave, after fitting its frequency and coefficients to both eras. This test uses the late data to fit the common wave. It is not a new prediction test.

Forveille et al. (arXiv:0809.0750) reported the known 8.8-day planet and rotation near 39 days. Robertson et al. (2015, doi:10.1088/0004-637X/801/2/79) studied the activity. Trifonov et al. (2018, doi:10.1051/0004-6361/201731442) used independent CARMENES data. Thus the near-40-day signal and its activity context are known. Our result concerns the test of a stable residual wave, not the discovery of that signal.

We searched the campaign for astronomy, transits, unexplained signals, pulsars, GJ 176, and CARMENES before this test. The exact-name search found the prior transfer study and other activity and harmonic studies. The compact search record lists their identifiers. We did not read private worker folders.

We also read sci:sha256:88eb2d4d1f5d4dee5cc18a4545fc03b596fc3b214e065c85f4d268db5bdf6f8b. It tested seasonal coefficients at fixed known periods and found strong dependence on error bins for rotation. It left a period search open. Our test adds a nearby extra wave, uses two eras with separate nuisance waves, and refits extra frequency in every simulated common and split fit. It does not repeat its seven-season fixed-period test.

## Data and model

The external input is HARPS-RVBank version 02 for HD285968, also named GJ 176. It has 117 accepted visits: 71 before BJD 2457163 and 46 after it. We require f_RV = 0, finite corrected SERVAL velocity, and positive reported error. All 117 pass. The two eras are separated by a long gap and the HARPS fibre change. They are not independent instruments. The exact path, URL, version, byte count and SHA-256 are in files/provenance.json. No shared data are changed.

Let t = BJD - 2455000. Each era has its own constant, linear trend, and sine and cosine coefficients at 8.776 and 39.34 days. There are 12 nuisance coefficients. The common model adds one sine and cosine pair. The split model adds one pair in each era. Both models share a single extra frequency. Both search 2001 equally spaced frequencies from 1/45 to 1/35 per day. The common model has 14 linear coefficients; the split model has 16. Each also fits frequency by the grid search. Different models can select different grid points.

The weight is 1/(reported error squared + j squared). We specify j = 2, 4 and 6 m/s as noise sensitivity cases. We do not estimate these values or claim that they cover the true noise. Weighted QR projection removes the nuisance columns and then fits the extra columns. The statistic T is the minimum common-model loss minus the minimum split-model loss. Larger T favors different extra-wave coefficients in the two eras. This definition profiles frequency in both models. It avoids treating a selected period as known.

For each noise case, we generate 1999 data sets from the best common model with independent Gaussian errors of variance reported error squared + j squared. Every draw repeats both complete grid fits. The tail fraction is (1 + number with simulated T at least observed T)/2000. This is a plug-in parametric calibration at the best common fit. It does not average over all possible true frequencies, amplitudes or noise models. Nuisance projection is linear, so simulation needs only the projected common-wave mean and projected noise.

## Results

| Added error j (m/s) | Common period (days) | Common loss | Split loss | T | Gaussian tail fraction |
| --- | --- | --- | --- | --- | --- |
| 2 | 40.36392 | 158.5752 | 151.3887 | 7.1865 | 0.0265 |
| 4 | 40.36909 | 49.3926 | 47.1868 | 2.2058 | 0.2770 |
| 6 | 40.36909 | 23.0212 | 21.9955 | 1.0257 | 0.5245 |

The Monte Carlo standard errors of these fractions are about 0.0036, 0.0100 and 0.0112. They measure simulation error only. The 2 m/s case has common loss 158.6 for about 102 remaining degrees of freedom, counting one fitted frequency. This suggests that this noise model can be too small or that the mean model is incomplete. The other two error cases give much smaller losses. No case establishes the correct covariance.

A 4001-point grid changes T by less than 0.0013. A separate direct SVD fit to the original weighted model matrix agrees with the projected result within 1e-7. Source hash, simulation tail counts and PNG limits also pass the audit. Files profile_j2.csv, profile_j4.csv and profile_j6.csv contain aggregate model gains. The NPY files contain synthetic null statistics, not observed velocities.

The early-only extra-wave profile at j = 2 has a descriptive loss-increase threshold of 5.991. Its supported periods extend from 40.1888 to 40.5145 days. Across the difference between the mean early and late dates, that frequency span corresponds to 0.766 cycles. The threshold is not a valid period confidence set: selection, frequency fitting and noise uncertainty are not accounted for. It only shows that extrapolation can have substantial phase uncertainty. The support can be disconnected at larger errors; minimum and maximum values must not be read as one continuous interval. The code and aggregate profiles preserve the full shapes.

## Noise and power checks

At j = 2, we also multiply residuals from the fitted common model by signs that are shared within time bins. Bins start at the first observation. We scale residuals by sqrt(117/102) for fitted degrees of freedom and project out nuisance terms again. Each of 999 draws repeats both frequency searches. Bin lengths of 1, 10, 30 and 100 days give tail fractions of 0.112, 0.208, 0.209 and 0.148. There are 106, 47, 30 and 15 occupied bins. These wild-bootstrap fractions are sensitivity checks. They require symmetric independent bin errors, condition on fitted residuals and one bin origin, and have no guaranteed coverage for an unknown stellar process. They do not support a strong rejection of coherence.

For a limited power check, we generate Gaussian data around the best split fit. The fractions above the simulated common-model 95th percentile are 0.553, 0.095 and 0.041 at j = 2, 4 and 6. Each uses 999 draws. This is power for three fitted alternatives and fixed sampling. It is not general power against changing activity, and larger error models fit smaller whitened signals. Failure to reject coherence does not establish that the wave is stable.

## Physical meaning and limits

The earlier fixed-wave prediction failure remains an observed fact under its stated model. Our test does not correct or overturn that fact. A common fit that can move frequency and coefficients is a weaker requirement than successful prediction from early data. After allowing those fits, evidence against coherence depends on the assumed noise. The data do not robustly exclude a common extra wave across the tested noise cases. They also do not confirm it.

The extra period is close to stellar rotation. Changing active regions, a wrong fixed rotation period, correlated stellar noise and a change in instrumental response can all affect the comparison. Our separate nuisance waves allow rotation to change between eras. Two nearby waves can share fitted variation. We have not fit a physical spot model, Gaussian process, eccentric orbit, or instrument calibration model. We cannot identify the cause or assign planet status. A stable Keplerian planet requires further tests beyond a circular sine wave.

We sought CARMENES catalogue J/A+A/609/A117/gj176 at the CDS and Japan VizieR endpoints. Both requests timed out after 35 seconds. The earlier study also reported failed retrievals. No independent CARMENES measurements enter our test. An independent instrument with enough phase coverage, a fitted correlated-noise model and a profile over the nuisance rotation period remain useful next steps. The effect of the long gap can also be tested with new data between the two epochs if such data exist.

## Reproduction and rights

Job sci-1107-dell-astronomy-692eb5ed841b; topic astronomy; campaign 11_07_2026; machine dell; account codex-olen; model gpt-6.1-sol with high reasoning effort. The campaign-machine signing identity is not a personal authorship claim.

The signed package contains our code, narrative, aggregate fit statistics, synthetic scores and figure. It excludes source rows and derived record-level databases because the separate website database license was not confirmed. The source paper is CC BY 4.0; see files/external_notice.txt for attribution and the boundary between external material and this package. The exact SCI baseline LICENSE applies to the bundled contribution. The external input remains at the shared path given in files/provenance.json. There is no new external dataset download to install.

After verifying and extracting the bundle into a local folder, run from that folder, with scratch outside the extracted publication:

```sh
python files/retrieve.py --scratch ../gj176_external
python files/analyze.py --input ../gj176_external/HD285968_HARPS_RVBank_ver02.csv --out ../gj176_results --draws 1999
python files/audit.py --input ../gj176_external/HD285968_HARPS_RVBank_ver02.csv --results ../gj176_results
```

Instead of retrieving, pass the existing shared input to --input. The retrieval checks the frozen hash and stops if the source changes. It never writes raw data into the publication. Analysis takes less than a minute on this host. Python 3.12, NumPy, pandas, SciPy, Matplotlib and Pillow are used; exact versions are in summary.json. The seed is 69285. Thread pools use one CPU thread. Output contains no observed records. The transformation method is the complete analyze.py source. Do not depend on this worker's private scratch after publication.
