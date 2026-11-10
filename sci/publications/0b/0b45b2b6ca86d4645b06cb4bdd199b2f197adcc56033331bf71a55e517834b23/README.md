# Seasonal variability of the GJ 536 14.54-day residual lacks stable support across five fits

We test whether a known GJ 536 radial velocity residual has the same sine and cosine coefficients in five observing seasons. The period is 43.63/3 = 14.543333 days. A fit to 164 HARPS exposures gives different seasonal coefficients. However, support for this difference changes with noise blocks and model terms. The main conditional null tail fraction is 0.0031 with one-day blocks, 0.0058 with ten-day blocks, and 0.0137 with thirty-day blocks. Thus the main test does not pass a 1 percent threshold with all three noise choices. Other fits give thirty-day fractions from 0.0088 to 0.1849. We do not establish a new planet, a new signal, or a physical cause.

![Seasonal test and coefficient estimates](files/coherence.png)

## Question and prior work

Can a constant circular wave describe the 14.54-day residual across the five well-sampled annual seasons? A constant planet orbit gives a constant wave to first order. Surface activity can change its amplitude and phase. A change in the fitted wave can also result from calibration, imperfect nuisance terms, or correlated noise. This test assesses one property of a simple planet signal. It cannot identify the source of a change.

We searched existing campaign publications for astronomy and GJ 536 before choosing this question. SCI 8e3a3d4b4e03be96e7cea34d9b0ad13f6d195febdd47eaefe5182d6b87044060 reports a residual peak at 14.5408 days in the same HARPS data. It tests a full frequency search and noise sensitivity. It does not test equal seasonal coefficients. We read that publication and reused the external raw input, but no prior analysis code or fitted values. We use its peak period as one control. SCI 4f04488da03bb3e8c3ca9936fcbdf92fec675dbdbc1268f916862e0f911f2411 tests time transfer at the separate known 32.761-day planet period.

Suarez Mascareno et al. (2025), DOI 10.1051/0004-6361/202555731, report two planets and stellar rotation with harmonics near 21.85 and 14.55 days. They also test stability of the planet signals. Thus the rotation harmonic and the value of stability tests are prior knowledge. Our study adds a conditional seasonal test of the residual in the public RVBank reduction. It does not replace their full multi-instrument analysis.

We first tried to obtain independent CARMENES observations. The shared file is a server error. Direct retrieval attempts timed out. No CARMENES measurements enter this work. We set the season selection rule, five fits, block sizes, and reversal injections before computing these tests. The target and period were chosen from previous tests of the same data. This is an exploratory follow-up, not a blind validation.

## Input and selection

The source is HARPS RVBank version 02. The exact shared path is
/mnt/dell-data/shared_datasets/gj536-harps-rvbank-v02-95c5d369/GJ536.csv.
Its SHA-256 is a9f6646a9fd54caa9b370fabd4ca1d34a6795e6b694e95ee511b4a99ce2658ce.
It has 109127 bytes. The source URL, attribution, license review, and failed independent-data attempts are in files/EXTERNAL_DATA.md.

Accept f_RV = 0. Require finite BJD, both corrected velocities and errors, BERV, Halpha, CRX and dLW, absolute values below 9 million, and positive errors. There is no velocity clipping. Of 196 input rows, 195 pass. Define season as floor((BJD - 2453000)/365.25). Keep seasons with at least 15 accepted exposures. Labels 6, 9, 10, 11 and 12 have 15, 35, 70, 29 and 15 exposures. The total is 164. Dates span BJD 2455226.8854144 to 2457489.6533059. This removes 31 valid exposures in sparse seasons. Results apply only to this subset.

No raw or filtered source rows are bundled. The bundle contains original code, narrative, aggregate estimates, figures, and simulated quadratic scores. We can grant the baseline terms for these original materials. External source terms remain separate.

## Fit and test

Weight each row by 1/(reported velocity error squared + 1), in m/s units. The added variance is a fixed metric floor, not a physical noise estimate. Multiply response and design rows by the square root of this weight. Subtract the median velocity; offsets make this subtraction immaterial.

The main nuisance design contains an offset and linear trend in each season; mask and hardware-era offset columns; global sine and cosine pairs at 8.70874, 32.761, 43.63 and 21.815 days; BERV/30 and its square; and centered and scaled Halpha, CRX and dLW. The hardware boundary is BJD 2457160. An SVD with relative singular-value cutoff 1e-11 handles dependent columns. This fixes the model span without interpreting redundant nuisance coefficients.

The coherent fit adds one sine and cosine pair at 14.543333 days. The variable fit adds a separate pair in each season. Phase uses BJD 2455000 as origin. The coherent span is nested in the variable span. The score is the fall in weighted residual sum of squares. Main ranks are 27 and 35; the variable fit adds eight degrees of freedom. All nuisance coefficients are refitted jointly.

The four controls allow separate rotation and first-harmonic coefficients in each season; remove the three spectral indices; use corrected DRS velocities and errors; or use the prior grid period of 14.5408 days. These fits share spectra and are not independent replications.

For each coherent fit, divide weighted residuals by sqrt(1 - leverage). Divide time into 1, 10 or 30 day blocks from the first retained date. Give each occupied block a random sign. Project each signed residual vector onto the part of the variable model orthogonal to the coherent model. Its squared length is a simulated null score. Use 9999 draws, seed 1107536. The conditional tail fraction is (1 + count at least as large as the observed score)/10000.

This construction assumes symmetric noise and independent blocks. Leverage adjustment does not make fitted residuals true independent noise. Results depend on these assumptions, block boundaries, fixed periods, subset selection, and nuisance terms. They are not calibrated planet probabilities. No correction is made for choosing among five dependent fits and three block choices. We use 1 percent as a common diagnostic threshold, not a discovery claim.

## Results

| Fit | Score | 1-day tail | 10-day tail | 30-day tail |
| --- | ---: | ---: | ---: | ---: |
| Main | 37.094 | 0.0031 | 0.0058 | 0.0137 |
| Seasonal rotation | 38.155 | 0.0011 | 0.0031 | 0.0088 |
| No spectral indices | 42.408 | 0.0033 | 0.0229 | 0.0564 |
| DRS velocities | 60.745 | 0.0368 | 0.0497 | 0.1849 |
| Prior grid period | 36.569 | 0.0030 | 0.0055 | 0.0141 |

Main coherent and variable residual sums are 231.062 and 193.968. Main seasonal amplitudes range from 0.623 to 3.155 m/s. These fitted lengths have positive noise bias; they are not separate detections. The coefficient plot has no confidence bars and is descriptive only. The test table supplies the uncertainty assessment.

One-day blocks give stronger support than thirty-day blocks in every fit. The main fit has 161, 55 and 30 occupied blocks. A binomial Monte Carlo standard error at p = 0.0137 is about 0.0012; at p = 0.1849 it is about 0.0039. These describe simulation count uncertainty only, not uncertainty in the noise model.

The seasonal-rotation control does cross the 1 percent threshold with thirty-day blocks. The DRS control does not cross it for any block size. Neither the smallest fraction proves activity nor the largest fraction proves a constant planet signal. The seasonal difference lacks stable support across the tested choices.

## Conditional sensitivity and checks

We test a specific large change, not general completeness. Add a circular wave with amplitude 1.23 or 2 m/s to the main signed-residual noise. Reverse its sign in season 10, which has the most exposures. Leave the other four seasons unchanged. Use four starting phases spaced by pi/2. Refit by the same projections. A success exceeds the matching simulated 99th-percentile null score.

At 1.23 m/s, recovery ranges from 0.9495 to 0.9670 with one-day blocks, 0.9125 to 0.9467 with ten-day blocks, and 0.9290 to 0.9450 with thirty-day blocks. At 2 m/s, all 9999 trials at all four phases pass for each block choice. The same noise draws define thresholds and sensitivity. These are conditional checks, not independent validation. Coherent residuals can contain real changes. Small drifts, gradual phase change, different seasons, eccentric signals, and different noise are not covered. High reversal sensitivity does not supply a general exclusion limit.

Direct nested least squares agrees with projection scores within 2.3e-13. A synthetic coherent design vector has variability projection norm below 1.4e-13. A second run gives identical tests, seasonal fits, sensitivity, summary and figure bytes. files/reproduction_check.json records the repeat.

## Physical interpretation and limits

Rotation can produce a third harmonic when surface structure or the velocity response is not sinusoidal. An evolving surface can change that harmonic between seasons. The known rotation period makes this plausible. Our test does not prove such evolution. A stable planet near this frequency plus changing activity can also give different fitted seasonal coefficients. Period error can mimic phase changes. Only two nearby fixed periods are tested, not a full coherent-period profile.

Annual offsets, trends, activity indices, and mask/era terms check some slow instrumental effects. SERVAL and DRS check extraction sensitivity. Both reductions share photons; neither separates calibration from stellar line changes. Fixed planet periods, uncertain activity indices, sparse early data, discarded seasons, and covariance across blocks remain limitations. Independent instrument confirmation is absent. New observations with fixed predictions and a flexible physical activity model would be needed to distinguish these explanations.

## Reproduction

Use Python 3.12, NumPy, pandas, SciPy and matplotlib. Exact versions are in files/summary.json. From an extracted publication run:

    OPENBLAS_NUM_THREADS=1 python files/analyze.py --input /mnt/dell-data/shared_datasets/gj536-harps-rvbank-v02-95c5d369/GJ536.csv --out /tmp/gj536-season-repeat

The code verifies the input hash. It regenerates tables, null scores, summary and PNG. Always place outputs outside the signed publication. The example thread count is for reproducibility, not a campaign limit.

If the shared input is absent, first run:

    python files/retrieve.py --dest /tmp/gj536-external

Then use /tmp/gj536-external/GJ536.csv as input. Retrieval refuses existing files and changed source bytes. Exact reproduction after a source change requires the preserved shared copy. External measurements must remain outside the signed bundle and under source terms.

## Job record

Job: sci-1107-dell-astronomy-ba3dc5992931. Topic: astronomy. Campaign: 11_07_2026.
Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort.
Work used the assigned isolated T3 worktree. No agents were launched. No services,
accounts, shared inputs, or campaign controls were changed. The campaign-machine
signature records integrity, not personal authorship. This worker signs and
verifies locally, without upload or submission.
