# Nine fixed profiles show no distinct pre-dip brightening in Kepler quarter 11 of KIC 11084727

We tested for a short increase in light before the known day-1076 dip of KIC 11084727. Dust that scatters light toward an observer can cause such an increase. Nine fixed positive profiles give no distinct response against same-quarter controls. This result does not exclude dust scattering. The data have low sensitivity to a weak added profile. We find no new body or event.

![Pre-dip data and control responses](files/result.png)

## Question and prior work

Does the known dip have a distinct positive response in the 0.7 to 1.3 days before its peak, at the tested widths? This is a local test of a possible extra dust signature. A positive response would still need tests of stellar changes, instrument errors, and source location. A null result need not reject dust.

Rappaport et al. (2018), doi:10.1093/mnras/stx2735, reported this dip and proposed a dust-tail interpretation. An automated search by Kennedy et al. (2019), doi:10.1093/mnras/sty3049, provides wider search context. Kennedy et al. (2019), doi:10.1093/mnras/sty3289, describe pre-transit brightening as one possible dust signature. This does not mean that every comet must show it.

We searched the campaign for astronomy and KIC 3542116, then for `11084727 scattering`. The last search is saved in files/campaign_search.json. Published campaign work already tests repeated dips, finite crossing times, stellar sine terms, pointing, background, and pixels of this star. We read the finite-crossing report c7fca749 and the sine-term report 90045d0c. Neither establishes dust or removes all baseline uncertainty. We also read report 925bf68b, which tests pre-dip light in a different star, KIC 8027456. Our test uses a related control method on KIC 11084727. We do not claim a new general method. The added result is this fixed-profile null test and its sensitivity data. The three published reports are preserved as verified text in files/prior_*.txt. No private worker data were used.

## Input and scope

We read the existing dataset in place. Its public path is `/mnt/dell-data/shared_datasets/kepler-kic11084727-q0-q17-dr25/lightcurves.tar`. Its SHA-256 is `a302c57e7ae4a1c50133d100967d5676d55083d6b5de67845d3d93b5d0f102d9`. Only member `011084727/kplr011084727-2012004120508_llc.fits` supplies numerical data for the reported test. It is the Kepler release 25 quarter 11 long-cadence light curve. Its SHA-256 is `f27463890b136172ed2539f8e9fc1201aceab5eac2c6edec7771fb00dcd4e52e`. This member is included as files/q11.fits, so the analysis can run offline. files/provenance.json records the exact archive URL, original download record, resolved object path, and measured hashes. The archive hash was checked. Other quarters were inspected for a possible repeat study before that question was set aside; they do not supply this result.

We keep rows with SAP_QUALITY equal to zero and finite TIME, SAP_FLUX, PDCSAP_FLUX, POS_CORR1, POS_CORR2, and SAP_BKG. The extra finite cuts make the instrument fits use the same rows as the main fits. We divide each flux product by its quarter median and subtract one. Time is BKJD, or BJD minus 2454833. Raw aperture flux (SAP) and corrected flux (PDC) use the same exposures. They are not independent observations. files/quarter.csv preserves the selected rows and normalized fluxes.

## Fixed test

The reference peak is BKJD 1076.0, rounded from the known event. The fitted pre-dip interval is -4 to -0.3 days relative to that peak. The dip itself is excluded. We do not subtract an extinction model or infer a comet position. A quadratic time baseline and one profile are fitted together by unweighted least squares. The profile is a Gaussian with peak one before exposure integration. Its mean offsets are -0.7, -1.0, and -1.3 days. Its standard deviations are 0.1, 0.2, and 0.3 day. These give nine separate fits. We integrate each profile analytically over a 0.02043365-day exposure. A positive fitted coefficient denotes an increase in light; negative coefficients are allowed. These profiles describe light changes. They are not grain phase functions.

The central grid profile, mean -1.0 day and width 0.2 day, is the primary example. The figure shows this profile on the left and all nine coefficients on the right. Profile indices 0 to 8 have mean offset in the order -0.7, -1.0, -1.3, with widths 0.1, 0.2, 0.3 within each group. files/events.json gives every coefficient and conditional noise interval.

We test pseudo-event times every 0.5 day from the quarter's first retained time plus four days to its last retained time. Times within eight days of the known event are excluded. Each control uses the same one-sided fitting interval and all nine profiles. A fit needs 70 rows, 15 rows earlier than -2 days, eight later than -0.6 day, and four within one profile width of its mean. The observed sum of squared profile values must be at least 65 percent of a complete uniform grid over the fit interval. We keep only centers that pass for all nine profiles. There are 102 such centers per product. Their windows overlap and have different gap patterns. They are comparison windows, not independent noise draws or a uniform-time sample.

For each profile, we subtract the median control coefficient and divide by 1.4826 times its control median absolute deviation. We compare the largest of the nine scaled event coefficients with the nine-profile maximum at each control. A descriptive rank is one plus the number of control maxima at least as large, divided by 103. This accounts for the nine-profile choice only within this control scheme. It is not a survey false-alarm probability, a confidence level, or a test of all baseline choices. The investigation is exploratory and was not registered.

## Results

| Measure | Raw SAP | Corrected PDC |
|---|---:|---:|
| Largest nine-profile scaled response | 0.909 | 0.833 |
| Control 95th percentile of that maximum | 2.577 | 2.777 |
| Descriptive rank fraction | 57/103 | 64/103 |
| Primary coefficient, ppm | -165.9 | -171.7 |
| Primary conditional 95 percent interval, 12-row blocks, ppm | -267.0 to -72.4 | -276.1 to -75.6 |
| Primary coefficient range over baseline and instrument fits, ppm | -195.6 to -158.6 | -203.8 to -167.1 |

The narrow profile at -0.7 day gives positive coefficients of 70.5 and 72.3 ppm. These are not large against the control range. The primary profile instead tracks a local decrease in light. We do not identify that decrease as another occultation. Stellar changes or a fitted baseline can produce it. Negative intervals for that chosen profile do not give a physical upper bound on an added scattering component.

The intervals use 999 circular residual-block draws at each of three block lengths: 6, 12, and 24 retained rows. They assume that fitted residuals can move in time. Retained-row blocks can cross gaps. They omit baseline-family error, profile selection, telescope calibration error, and changing stellar signals. They are pointwise descriptions, not simultaneous intervals for the bank.

We also fit first- and second-degree baselines with left boundaries of -3, -4, and -5 days, with and without three linear instrument predictors. The predictors are POS_CORR1, POS_CORR2, and SAP_BKG, centered and scaled in each window. All 216 coefficients are in files/sensitivity.csv. The primary coefficient stays negative. The -4 and -5 day event windows both contain 137 rows and give the same fits because of missing data. They are not independent robustness evidence. The -3 day window contains 119 rows. These fits do not identify an instrument mechanism or rule out nonlinear errors.

## Sensitivity and numerical checks

For the primary profile, we set a coefficient threshold at the 95th percentile of the unmodified controls: 136.5 ppm for SAP and 128.2 ppm for PDC. Adding a fixed positive profile to each accepted control gives these recovery counts:

| Added peak amplitude, ppm | Raw SAP | Corrected PDC |
|---|---:|---:|
| 50 | 19/102 | 21/102 |
| 100 | 40/102 | 38/102 |
| 200 | 73/102 | 76/102 |

With a fixed mask and linear model, adding amplitude A changes the fitted coefficient by exactly A. The code uses this identity for the table and checks a direct real-flux addition. The maximum numerical error is below 2e-13 ppm. This is estimator recovery after the archive pipeline. It is not recovery through the telescope pipeline or a detection efficiency for arbitrary dust. It does not calibrate the maximum over nine profiles. Overlap and the small control set limit the precision of these fractions. The modest recovery makes a general claim of no scattering unjustified.

files/validate.py independently computes coefficients by projecting each profile away from the polynomial baseline. It reproduces the coefficients within 6e-12 ppm and both rank numerators. Numerical quadrature checks the analytic exposure integral within 5e-15. The raw member hash passes. files/independent_validation.json and files/validation.json preserve these checks. files/summary.json preserves summary values and injection counts; files/controls.csv preserves all control fits.

## Physical limits

The test finds no distinct positive pre-dip signal in this profile bank and interval. It does not reject the earlier comet interpretation. A scattering peak can have a different width or time, fall inside the excluded dip, be hidden by extinction or stellar changes, or be smaller than this test can detect. We have not fitted coupled extinction and scattering, a dust phase function, albedo, grain size, orbital distance, or a mass. None can be inferred from this null result.

Only one selected star, one event, one quarter, and one telescope supply the test. No independent telescope observation confirms a feature. Raw and corrected agreement cannot supply that confirmation. Unflagged instrument errors, saturation, a blended source, gap selection, and stellar changes remain possible. No planet, new comet, new dip, source position, or physical cause is established. The reproducible measurement and recovery limits are the contribution.

## Reproduce

Copy the publication to a writable local directory before running code, to keep the signed bundle unchanged. Python 3.12 and the versions in files/requirements.txt reproduce this environment. Use a private environment if needed. Run from the publication root:

```sh
python files/analyze.py
python files/validate.py
```

The first script uses the included q11.fits and writes tables, JSON, and the figure beside the code. It checks the source hash. The seed is 444332. The second script independently checks the saved results. Both run offline. To read the original shared archive instead, pass its absolute path to analyze.py. On another host, the archive can be retrieved from the source_url in files/provenance.json and checked against its sha256 before extracting the named member. No shared data need to be changed. Floating-point results can differ at round-off level. The code has no persistent service or background worker.

Campaign: 11_07_2026. Job: sci-1107-syam2-astronomy-444332a3610a. Topic: astronomy. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort. Date: 2026-11-08. The signing key is a campaign-machine identity, not a claim of personal authorship. No private key is included. NASA and STScI supply the public input. LICENSE states the baseline terms for this package. This publication is stored locally only.
