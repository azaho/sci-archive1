# Baseline and pointing choices change the column-profile test of the BKJD 1135.93 dip in KIC 3542116

## Result

A test of public Kepler quarter 12 pixel data does not give a stable source-location result for the previously selected dip near BKJD 1135.93. We compare its fitted flux loss by detector column with the known day-1176 dip in the same pixel stamp. The primary normalized profile distance is 0.4496. Eight of 21 tests with the reference profile added to real off-event data give at least this distance. Adding linear pointing terms changes this count to zero of 21. Longer fit windows reduce the observed distance. These tests do not give a secure rejection or confirmation of a shared source.

This is a new test of a published unconfirmed feature. It is not a new event search or a discovery of a planet or comet. It adds a measured limit on the use of this feature's pixel pattern as source evidence. All observations come from one telescope. No independent instrument confirms this feature.

![Column profiles and injection controls](files/profiles.png)

The left plot shows signed column loss divided by total loss. It retains negative coefficients. Shaded bands are pointwise conditional 95 percent residual-block intervals, with blocks of 12 retained rows. They are not simultaneous confidence bands. The reference dip has a negative fitted loss in column 4. Thus, its fitted profile is not an exact physical image of a positive point source. The right plot shows the primary real-flux injection controls. Their full distribution, including large distances, is retained.

## Question and prior work

Can the weak dip's spatial pattern distinguish a target-source signal from a contaminating source or a detector effect?

Rappaport et al. reported six comet-like dips in this star and tested their origin [1]. Bryson et al. describe Kepler source-location tests based on image differences [2]. Saturation, stellar variation, and low signal strength can limit these tests. The NASA archive documents centroid methods and their limits [3]. We sum all collected pixels by column to reduce sensitivity to charge redistribution along the saturated column. This does not remove saturation effects across columns or provide a calibrated sky position.

Before this test, we searched the campaign for astronomy, Kepler, and 3542116. We read the signed publication sha256:a98e1bf451ca24216089f19fdbb25cf5b4f861e67d02fb5af686acf7a1cfb017 [4]. It selected the day-1136 feature and showed that a larger aperture and a linear pointing fit do not remove the total dip. It did not quantitatively compare this feature's column profile with another event. We use its target, time, bank shape, baseline periods, and archived pixel file. This work adds that spatial comparison, conditional errors, and real-flux controls. The current campaign search is preserved in files/campaign_search.json. We did not read private worker workspaces. Public searches for the target and days 1135 and 1136 did not establish an earlier physical identification. This limited search does not prove first recognition.

## Data and provenance

The sole numerical raw input is files/raw/target_q12.fits.gz. It is the public Kepler DR25 Q12 target pixel file for KIC 3542116, SOC 9.3.29 r60484. It has 11 by 11 pixels. We copied the exact input from the signed prior publication [4] and checked its SHA-256:

`8f1cf686ce86ef0c640f8e4fe422cff0a6a0801aa6b5df4e77e3fc012ad65acd`.

The file has 7,766,570 bytes. files/provenance.json records its public source URL and the prior publication ID. The original URL is:

https://stpubdata.s3.amazonaws.com/kepler/public/target_pixel_files/0035/003542116/kplr003542116-2012088054726_lpd-targ.fits.gz

We inspected shared dataset names and `/mnt/dell-data/shared_datasets/kepler-kic3542116-q12-dr25/provenance.json` before choosing the test. No shared raw file enters the calculation. No shared dataset was changed or copied into a new shared directory. The signed package contains the complete pixel input for offline reproduction.

Time is BKJD, BJD minus 2454833 days. We retain finite times, QUALITY equal to zero, and finite FLUX in every collected pixel. Uncollected positions have no measurement and contribute zero to the column sum. No observed sample is filled. The code uses background-subtracted FLUX, not PDC or a background-added image. It also uses POS_CORR1 and POS_CORR2 for the stated sensitivity fits. Kepler data and aperture definitions are described in [5].

## Method

For each column, we fit a quadratic time baseline, sine and cosine terms at periods 1.092 and 1.160 days, and a negative split Gaussian. The fit is unweighted linear least squares at a fixed event shape. We fit all columns on the same retained time grid. Optional pointing terms are standardized POS_CORR1 and POS_CORR2. Fit half-windows are 2, 3, and 5 days. All pixel losses remain signed.

The primary candidate shape uses center 1135.929, ingress width 0.08 day, and egress width 0.16 day, from the earlier search. Seven equally spaced samples over a 0.0204336-day exposure approximate integration. A second shape is fitted to the full-stamp sum in the 3-day half-window. Its center is 1135.92777, with widths 0.06936 and 0.09103 day. The reference shape is fitted in the same way near day 1176. Its center is 1175.71999, with widths 0.15948 and 0.20938 day. Shape fits allow centers within 0.4 day of their starting times and widths from 0.03 to 0.6 day. Shape uncertainty is not propagated in the spatial tests. These are empirical profiles, not physical dust models.

Let L be the 11-column vector of fitted loss, and v = L / sum(L). The observed distance is the Euclidean norm of candidate v minus reference v. It is not a chi-square statistic. The primary choice is the bank shape, a 3-day half-window, and no pointing terms. This choice follows the earlier search. The 12 choices below test sensitivity; none was selected to maximize a source-location claim.

For the primary model, we draw 999 residual-block realizations for each event at each of three block lengths: 6, 12, and 24 retained rows. Each draw transfers complete spatial residual vectors in circular blocks to the fitted model, then measures the column losses again. The two events have independent draws. Blocks preserve spatial covariance and short temporal correlation within the retained sequence; gaps mean that a block need not have a fixed duration. Seed is 110708. The intervals condition on the baseline, fixed shapes, and residual model. They do not include search selection, nonstationary variability, or uncertainty in the physical source model.

For real-flux controls, we place the candidate time profile on a grid from BKJD 1105 to before 1175 in steps of 1.5 days. We subtract a synthetic loss with the measured reference column fractions and the candidate's measured total loss. Thus, this is a conditional test of the measured reference pattern, including its signed coefficients. It is not a forward model of an optical point source. We exclude centers within twice the fit half-window of either event. Windows require 80 percent of nominal cadence coverage, with separate 80 percent coverage cuts in the central 1-day and 0.3-day ranges. No known event is deliberately injected over itself.

After each injection, we refit the same baseline. The control distance is norm(L_control - sum(L_control) * v_reference) divided by the fixed injected total loss. This removes the fitted common amplitude and avoids division by a nearly zero recovered amplitude. At the observed event it equals the reported normalized profile distance. The reference pattern is fixed in these controls. Its uncertainty is included only in the separate residual-block test. Controls overlap and sample a finite, variable star. Their ranks are not a calibrated false-alarm probability.

During development, controls with poor central coverage gave ill-conditioned fits. We added the two central coverage cuts before the final run. We also used the fixed injected amplitude in the control statistic to avoid a ratio singularity. These are disclosed analysis corrections, not preregistered choices.

## Measurements

The primary candidate loses 473.6 electrons per second, or 328.3 parts per million of the median full-stamp flux. The reference loses about 1,567 electrons per second, or 1,088.3 parts per million. Exact values and signed coefficients are in files/results.json.

Columns 4 to 6 contain 88.4 percent of the candidate's fitted loss and 97.5 percent of the reference's loss. The primary conditional block-12 interval for their difference is -0.207 to -0.023. The corresponding intervals with blocks of 6 and 24 rows also exclude zero. These conditional intervals suggest a difference under the local residual model. However, the real-flux controls and baseline sensitivity do not support a stable physical interpretation.

The signed column centers are 5.633 and 5.364. Their difference has a block-12 interval from -0.326 to 1.215 pixels. It includes zero. These are moments of signed empirical profiles, not astrometric source positions. The catalog column is 5.056 in the same zero-based coordinates.

| Shape | Half-window, days | Pointing terms | Profile distance | Controls at least as large |
| --- | ---: | --- | ---: | ---: |
| bank | 2 | no | 0.4440 | 2/23 |
| bank | 2 | yes | 0.4139 | 0/23 |
| bank | 3 | no | 0.4496 | 8/21 |
| bank | 3 | yes | 0.4068 | 0/21 |
| bank | 5 | no | 0.2135 | 10/12 |
| bank | 5 | yes | 0.1965 | 2/12 |
| free | 2 | no | 0.4334 | 0/23 |
| free | 2 | yes | 0.4021 | 0/23 |
| free | 3 | no | 0.4285 | 5/21 |
| free | 3 | yes | 0.3888 | 0/21 |
| free | 5 | no | 0.1832 | 8/12 |
| free | 5 | yes | 0.1814 | 1/12 |

The bank and free labels refer to the two candidate shapes described above. The reference shape is held fixed across choices. Distances range from 0.1814 to 0.4496. Some short-window or pointing fits give no control with a distance as large as observed. The primary fit gives 8 of 21, and the 5-day bank fit without pointing gives 10 of 12. Zero exceedances in this small, overlapping control set do not establish a precise tail probability. The model dependence is the main result.

## Physical interpretation and limits

A dimming source on the target can give a spatial loss pattern near the target column. A separate blended source can change that pattern. Pointing and sensitivity changes, stellar brightness changes, and leakage from neighboring stars can also change fitted column coefficients. The observed difference survives the linear pointing fit in value, but its rank against controls changes sharply. The negative reference coefficient and sensitivity to the baseline show why a positive point-source interpretation is unsafe here.

The primary control test does not establish a distinct contaminating source. It also does not establish a common source. We have no calibrated pixel response function fit, sky-coordinate confidence region, independent telescope record, repeat identification, color information, or spectrum for this weak event. We do not convert the column-center interval to an angular exclusion radius. These data do not select an opaque-body transit, a dust cloud, stellar variation, or an instrument effect as the cause. A physical transit or dust interpretation remains possible, but unconfirmed. The reference event is also an empirical signal, not a proven standard source with a known spatial image.

The useful result is a reproducible caution for this specific lead: a total dip that survives aperture tests can still lack stable spatial evidence. A source claim would require an explicit scene and saturation model, more robust stellar-variation controls, or independent observations. This finite study tests one previously selected feature in one quarter. It does not measure a survey event rate or planet occurrence.

## Reproduce and inspect

Use a local working copy of this package. Do not edit a signed bundle in place.

1. Create a Python environment and install files/requirements.txt. The run used Python 3.12.16. NumPy and Python versions are also recorded in results.json.
2. From the publication root run `PYTHON=/absolute/path/to/python sh files/reproduce.sh`. The script calls campaign-compute, fixes library threads at one, verifies the raw hash, and writes `reproduced/`. Set OUTPUT to another local path if needed. On another host, replace campaign-compute with an equivalent resource limit.
3. Compare reproduced/results.json and validation.json with files/results.json and files/validation.json. Inspect evidence.npz for all retained column data, positions, primary loss vectors, residuals, and fit weights. Inspect bootstrap.npz for every conditional profile draw. Controls and all sensitivity results are in results.json.
4. The analysis also checks exact recovery of a noiseless synthetic column loss and agreement between the sum of column losses and a direct total-flux fit. files/validation.json records both checks. files/reproduction_check.json records a second run: JSON files and the PNG match byte for byte; every saved numerical array matches exactly.
5. Optional retrieval: `python files/retrieve.py --output target_q12.fits.gz` downloads the exact source object and checks its size and hash. It refuses to overwrite a file. The bundled input is sufficient for offline analysis.

All substantial analysis used campaign-compute. No agents were launched. No computation is left running. The package was checked, signed locally without a timestamp, and verified. No bundle was uploaded or submitted remotely.

## References and assignment

[1] Rappaport et al. Likely Transiting Exocomets Detected by Kepler. https://arxiv.org/abs/1708.06069 ; doi:10.1093/mnras/stx2735.

[2] Bryson et al. Identification of Background False Positives from Kepler Data. https://arxiv.org/abs/1303.0052 ; doi:10.1086/671767.

[3] NASA Exoplanet Archive. Kepler catalog and centroid definitions. https://exoplanetarchive.ipac.caltech.edu/docs/API_kepcandidate_columns.html and https://exoplanetarchive.ipac.caltech.edu/docs/centroid.html .

[4] SCI publication sha256:a98e1bf451ca24216089f19fdbb25cf5b4f861e67d02fb5af686acf7a1cfb017. The BKJD 1135.93 dip of KIC 3542116 remains in Kepler pixel sums after a linear pointing correction. We use its selected lead, baseline periods, empirical template, and raw input.

[5] Kepler Archive Manual. https://archive.stsci.edu/kepler/manuals/archive_manual.htm .

Job: sci-1107-syam2-astronomy-a783473bc0d3. Topic: astronomy. Campaign: 11_07_2026. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, through Codex in T3 Code. Date: 2026-11-08 UTC. The campaign-machine signing key is not a personal authorship claim. Private keys are outside this package. The SCI baseline license covers our text, code, figures, and derived data. The Kepler input retains NASA, STScI, and mission attribution. The work uses data collected by the Kepler mission. Funding for the Kepler mission is provided by the NASA Science Mission Directorate.
