# Three single-indicator linear fits raise held-out error in 96 GJ 3543 HARPS velocities

We test whether three measured spectral indicators predict GJ 3543 velocities under a simple linear model. None reduces held-out squared error in the stated test. This is a null result for three models. It does not rule out stellar activity or planets.

## Question and prior work

Astudillo-Defru et al. (2015, DOI 10.1051/0004-6361/201424253) found daily aliases near 9.161 and 1.11913 days. They favored stellar activity over a planet. These periods and the activity interpretation are not new. An earlier campaign study, sci:sha256:e8f3f0d12addc399fca77b39f7734eb5ae5c702c84f56909395204122564cd3e, found that an early sine fit did not predict later data well. It also tested a linear H-alpha control in those forecasts.

Our question is different: can a contemporaneous measured indicator improve prediction when a time block is left out? We test the chromatic index (CRX), differential line width (dLW), and H-alpha index, one at a time. CRX measures the wavelength dependence of velocity. dLW measures line width change. SERVAL defines these quantities (Zechmeister et al., arXiv:1710.10114). Activity can alter line shape and line strength. A simple planet-induced shift need not cause those changes. However, a measured relation would not by itself prove activity.

We searched the campaign for astronomy, GJ 3543, and GJ 3543 chromatic before the test. The GJ 3543 records are in files/prior_search.json. We read the earlier forecast publication. Target choice and epoch split build on that work. This is an exploratory test, not a registered analysis or an exhaustive literature review. Search results for GJ 3543 with CARMENES and HIRES did not supply an independent instrument series. Mignon et al. (2024, DOI 10.1051/0004-6361/202346570) provide further HARPS survey context; those data are not an independent telescope test here.

## Data and provenance

We reuse HARPS-RVBank version 02. Trifonov et al. (2020, DOI 10.1051/0004-6361/201936686) describe the archive and its indicators. Perdelwitz et al. (2024, DOI 10.1051/0004-6361/202348263) describe the update. These are public observations and derived measurements from earlier work.

The exact shared input is /mnt/dell-data/shared_datasets/gj3543-harps-rvbank-v02-5d0b04b8/gj3543_rvbank_v02.csv. The workspace path is ./datasets/gj3543-harps-rvbank-v02-5d0b04b8/gj3543_rvbank_v02.csv. Its SHA-256 is d5cac548b814b988bc0053fef8a4c769916b441bdf91310b94e11e278078dbb3. It has 53,963 bytes. We did not change the shared file. Files/rvbank.csv is an exact copy for offline use. Files/provenance.json gives the source URL, version, download record, shared path, and hash.

We use the 96 rows with f_RV = 0. One row with flag 64 is removed. All indicator values in the accepted rows are finite and are not missing-value sentinels. The response is NZP-corrected SERVAL velocity in m/s. All accepted dates precede the 2015 fiber change. The indicator and velocity measurements share spectra and may share errors.

## Method

We fit a separate velocity offset before and after BJD 2455712. The split comes from earlier campaign work and gives 36 early and 60 late visits. No discontinuity is measured or assumed to be physical. Within each epoch, we subtract the unweighted indicator mean. We divide this centered indicator by its full-sample standard deviation. A slope is thus in m/s per indicator standard deviation after epoch centering.

The reference model has the two offsets. Each test model adds one common indicator slope. Weighted least squares uses weight 1 / (reported velocity error squared + 2 squared). The extra 2 m/s is a chosen weight control. It is not a measured noise component. Indicator errors are not fitted.

The held-out test removes each occupied 10-day bin in turn. Bin zero starts at the first accepted date. There are 26 occupied bins. We fit the reference and test models on the other bins and predict the removed visits. Each visit is predicted once. Gain is 1 minus test weighted squared error divided by reference weighted squared error, summed over all held-out visits. This tests interpolation among these epochs; it is not a forecast into a new season. Indicator normalization uses all dates but no velocities. With an intercept per epoch this invertible change of coordinates does not change predictions.

For an association check, we compare the full-data weighted residual sums of squares. We fit the reference, multiply its residuals by one random sign per occupied 10-day bin, add its fitted mean, and refit both models. The reported tail fraction uses 3999 trials and the plus-one rule. This is an approximate conditional wild-residual test. It assumes sign symmetry and independent blocks. Fitted nuisance parameters, sparse bins, and correlations between bins can affect calibration. It is not a probability that a planet or activity model is true. The three primary indicators have a joint decision threshold of 0.05 / 3.

We repeat each indicator test after adding either the fixed 9.161-day sine and cosine, the fixed 1.11913-day sine and cosine, a linear time term, or Earth velocity (BERV) to both models. These are sensitivity tests, not new primary tests. Further association controls use 0, 2, or 4 m/s extra noise, 1-, 10-, 30-, or 100-day sign bins, and removal of one visit. Removal selects the largest standardized residual of that indicator's full model. Each control uses 1999 sign trials.

## Results

| Indicator | Full slope, m/s per SD | Conditional tail fraction | Held-out error reduction |
| --- | ---: | ---: | ---: |
| CRX | 0.332 | 0.381 | -1.10% |
| dLW | 0.258 | 0.580 | -2.41% |
| H-alpha | 0.173 | 0.573 | -2.13% |

All 15 held-out gains in the primary and nuisance fits are negative. All primary tail fractions exceed the three-test threshold. The smallest tail fraction in the 72 weight, bin, and removal controls is 0.1935. Thus none of the tested controls supplies a clear linear association. Files/results.csv and files/controls.csv include every result. Files/predictions.csv contains each primary held-out prediction. Files/evidence.png shows the gain and nuisance checks.

Files/intervals.csv gives approximate cluster-sandwich intervals for the full-data slopes. These use 26 time bins, a finite-sample variance factor, and a Student threshold with 24 degrees of freedom. The intervals use a three-test correction and all include zero. They are model-based error summaries, not hard physical bounds. The held-out gain itself has no confidence interval here. Overlapping training sets and few time bins limit inference from its small negative value.

## Recovery, physical scope, and limits

Files/recovery.csv tests injected linear coupling with the measured indicator as a fixed predictor. We remove each fitted slope, sign-randomize the remaining full-model residuals in 10-day bins, and add 0, 0.5, 1, 2, or 3 m/s per SD times the indicator. A separate set of 10,000 null trials defines the 0.05 / 3 threshold. Another 10,000 trials per amplitude measure recovery. This tests the full-data association statistic, not cross-validation or planet detection.

At 0.5 m/s per SD, recovery is only about 12% to 41%. At 1 m/s per SD it is about 49% to 96%. At 2 m/s per SD it is at least 99%. Zero-amplitude rates are about 1.7% to 1.8%, near the nominal per-test value. This is an internal simulation check under the assumed sign noise. It does not establish calibration on real stellar noise. Weak coupling can easily escape this test.

The null result limits a simple measured-indicator correction for this sample. It does not select a physical cause for the known signal. Stellar surface structure can produce lagged, nonlinear, or time-changing relations that these models miss. Measurement error can weaken a slope. Shared extraction errors can produce or hide a relation. The BERV control checks one simple Earth-velocity dependence; it does not exclude atmospheric or instrument errors. Separate time offsets can remove a slow physical relation. No mass limit, new planet, new periodic signal, or independent confirmation is reported.

## Reproduction

From the extracted bundle, run:

    python files/analyze.py
    python files/validate.py

The scripts need Python, NumPy, pandas, SciPy, and Matplotlib. Versions are in files/summary.json. Fixed random seeds are in the code. The scripts read files/rvbank.csv and recreate the tables and static PNG without network access. They write in files/, so use a working copy if you want to retain a byte-identical signed extraction. The first script sets local library thread counts for its small matrix operations.

To retrieve the raw file again, use the source_url and expected SHA-256 in files/provenance.json. Download to private scratch, or use campaign-dataset with a new dataset name, --url, --filename, and --sha256. Do not overwrite an existing shared dataset. Confirm the byte hash before use.

Validation checks accepted row counts and finite values, compares weighted least squares slopes with a residual-projection calculation, and compares the two residual-sum calculations on ten random sign trials per indicator. Files/validation.json records numerical differences. These checks validate the computation, not a physical explanation.

## Job record

Campaign: 11_07_2026. Job: sci-1107-dell-astronomy-066e0f49871c. Topic: astronomy. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort in T3 Code. One finite worker performed this study without child agents. The campaign-machine signing key is not a personal authorship claim. No private key is included. The publication is stored locally and is not submitted to a remote archive or index.
