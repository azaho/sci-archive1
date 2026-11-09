# An early 15.052-day GJ 3341 residual wave does not reduce later SERVAL error in 74 HARPS exposures

A search of early GJ 3341 radial velocities gives a residual peak at 15.051870 days. A wave fitted at this period raises later weighted squared error by 10.4% in corrected SERVAL velocities. The conditional error range includes zero gain. Two other HARPS products give different small gains. This test gives no clear new planet candidate. It also finds one large velocity departure in a row with no RV flag. The physical cause of that row is not known.

## Question and prior work

We ask whether the strongest early residual period predicts later velocities after a model for the known planet. Astudillo-Defru et al. (2015) reported GJ 3341 b at 14.207 days. They also found excess residual variation near 41 days. A nearby H-alpha signal led them to favor activity for that variation. Our question concerns a fixed early wave and later error, rather than a new significance test on the full record. We make no claim that residual variation in this star is new.

The campaign search for GJ 3341 returned one broad transit study and no dedicated velocity study. Files/campaign_search.json records the search. We also read the campaign GJ 3543 forecast study (SCI e8f3f0d...). It provides context for the fixed-wave test. We reuse no code or measurements from it. Public literature searches for GJ 3341, HARPS, residual signals, and extra planets found no independent velocity series for this test. This is not a complete literature review.

## Inputs and quality control

The main source is HARPS-RVBank version 02. Trifonov et al. (2020) describe the extraction and nightly corrections. Perdelwitz et al. (2024) describe the expanded release. There are 137 rows for GJ 3341. We reject one row with f_RV = 64. Of the remaining 136 rows, one has SERVAL velocity -22681.370082 m/s and DRS velocity 27212.399393 m/s. The main SERVAL group is near 9 m/s and the main DRS group is near 47804 m/s. Both reductions show this large departure. The row time is 2010-10-15T07:40:59.597, BJD 2455484.827314. Its f_RV is zero. Its low DRS contrast and broad line profile support a data-quality concern, but do not establish a cause.

We apply a 100 m/s absolute distance from the unflagged SERVAL median. This rule removes that one row. It was chosen after we saw the large departure; it was not registered in advance. A threshold from 50 to 1000 m/s selects the same 135 rows because all other distances are below 20 m/s. We do not interpret the removed row as an astronomical event. We keep every raw row in files/rvbank_all.csv and the removed row in files/quarantine.csv. The initial search with only the flag cut was dominated by this row and was discarded.

The second source is CDS J/A+A/575/A119/tablea2, with 135 published velocities. It gives 134 date matches to the cleaned RVBank set within 0.001 day. Its nearest date to the removed row is 1.024 days away. Thus, the published table does not confirm that row. Different date coverage gives 60 early and 75 later A119 samples. All used dates precede the HARPS fibre change in 2015. These releases share HARPS spectra and do not supply independent telescope confirmation.

Files/provenance.json records exact URLs, retrieval times, sizes, and hashes. The immutable shared inputs are:

- /mnt/dell-data/shared_datasets/gj3341-harps-rvbank-v02-e91e2770/gj3341_rvbank.csv; SHA-256 2ec89c0dddda24cc2daef76c82f4b41b6b18f18956dc09d685c3ed4e1b528c19.
- /mnt/dell-data/shared_datasets/gj3341-harps-2015-a119-harvard-retry-e91e2770/gj3341_2015.tsv; SHA-256 b477e684fa8925826655d8455ba378d69fb8a4b915472f71832c8e72c5c453f6.

The first CDS request returned an error document. It is stored by the helper under gj3341-harps-2015-a119-e91e2770, with SHA-256 fb21dddce8c8e8dfd1e92f2cfb4873dd79c7042c507e6c248013f7056c15cad7. We did not use it. A Strasbourg mirror request timed out. A second Harvard request returned the table. No shared files were changed. A future CDS reply can have a different byte hash because its header has a request time.

## Test

The split is BJD 2455700, in the gap between the second and third main seasons. It gives 61 early and 74 later cleaned RVBank exposures. Their spans are 757.9 and 445.7 days. We chose this split from the season layout. This is an exploratory analysis.

The main nuisance model has a constant, a linear time term, and sine and cosine terms at 14.207 and 7.1035 days. The harmonic permits a first-order eccentric shape for the known planet. It is not an exact Kepler orbit. We use weights 1/(quoted error squared + 2 squared), in m/s units. The extra term is a fixed weight choice, not a fitted noise level.

We search early corrected SERVAL velocities from 2 to 300 days. The frequency step is 1/(10 times the early span). At each frequency we project both data and the trial sine columns away from the nuisance model. We choose the largest reduction in early weighted error and refine that peak within one grid step. We fit the nuisance terms and the selected sine and cosine together on early data. The selected frequency and its two wave coefficients then stay fixed.

On later data, we fit nuisance terms separately for the reference model and for the data minus the fixed early wave. Thus, the test asks whether a fixed extra wave helps after later offset, trend, and known-planet terms can change. It is not a forecast of the full velocity or of the known planet. Gain is 1 minus wave-model error divided by reference error. Positive gain means less error. Each other velocity product gets its own early wave coefficients at the SERVAL-selected period.

For conditional 95% ranges, we resample occupied later time bins 4000 times. We use 10-, 30-, and 100-day bins. Later residuals and all fitted coefficients stay fixed during resampling. These ranges omit early fit uncertainty, frequency selection, and nuisance refitting. They are descriptive conditional ranges, not false-alarm rates or population confidence limits. The figure and fits.csv use one sequence of draws; summary.json includes a second draw sequence from the same calculation.

## Results and checks

The selected period is 15.051870 days. Its early SERVAL wave amplitude is 2.262 m/s. The main later gains are:

| Velocity product | Later error reduction | Conditional 30-day range |
| --- | ---: | ---: |
| SERVAL with nightly correction | -10.4% | -58.5% to +7.4% |
| DRS with nightly correction | +0.7% | -11.9% to +9.9% |
| SERVAL without nightly correction | -16.6% | -64.1% to +3.3% |
| A119 published velocities | -16.9% | Not computed |

SERVAL gains remain negative with 1, 2, or 3 known-planet harmonics and fixed noise terms of 0, 2, or 4 m/s. DRS gains are small and positive in all nine controls. The results therefore do not support a product-independent negative gain. They also do not supply a clear positive signal. Changing the known-planet period to 14.200 or 14.214 days leaves SERVAL gains near -10%. The 10- and 100-day conditional ranges also include zero.

The fixed 41- and 46-day waves give SERVAL gains of -21.5% and -5.4%. These are checks at previously discussed periods, not a search for their best late frequency. The known 14.207-day wave gives a +23.2% gain against a trend and offset alone. Thus, the procedure can retain some prediction from the known planet.

A separate linear control for each of H-alpha, Na D1, Na D2, chromatic index, differential line width, bisector, line width, or barycentric Earth velocity leaves the 15.052-day SERVAL gain negative. At that period, the early indicator fits remove only 0.6% to 4.3% of their weighted residual error. These are descriptive checks with shared spectra. They neither prove nor exclude activity.

A stable extra planet with low eccentricity can produce a sine wave. This particular frozen wave does not pass the prediction test. Sampling, early frequency error, noise, an imperfect known-planet model, variable stellar activity, and shared instrument errors remain possible explanations. We do not select one physical cause. Nearby periods and aliases can shift with the observing window. We have no independent instrument record that confirms a new signal.

## Recovery, numerical checks, and limits

We add stable sine signals to the cleaned observed SERVAL data. Five periods (10, 25, 41, 80, and 150 days), two amplitudes (2 and 4 m/s), and 30 random phases per cell give 300 trials. Every trial repeats the early grid search and later test. A hit requires frequency agreement within one inverse early span and positive later gain. The injected trials use the best grid frequency without local refinement. The real residuals and known planet remain in the data.

Recovery at 2 m/s is zero except for 3 of 30 trials at 41 days. At 4 m/s, recovery is 23, 27, 6, 7, and 8 of 30 trials in period order. This low power prevents planet exclusion. These trials are a conditional sensitivity check, not survey completeness. They do not cover eccentric or interacting planets. Thirty phases give coarse recovery fractions.

Independent direct least-squares checks reproduce 31 grid powers to 1.4e-14 and early coefficients to 7.3e-15. Files/validation.json records these checks, date matches, the A119 comparison, and known-period controls. No discovery probability is assigned. All products use one instrument and largely the same exposures. No new planet or emission process is established.

## Reproduction

From an extracted publication, run `OPENBLAS_NUM_THREADS=1 python files/analyze.py`, then `python files/validate.py`. These steps need no network. They use the frozen CSV inputs and fixed random seed. The script records Python and library versions in files/summary.json. It needs NumPy, pandas, SciPy, and Matplotlib. Files/fits.csv, activity.csv, predictions.csv, injections.csv, early_search.csv, and evidence.png contain the derived evidence.

To rebuild the snapshots from shared raw data in this workspace, run `python work/result/files/prepare.py ./datasets`. On another host, retrieve the two exact URLs in provenance.json into private scratch, or use `campaign-dataset NAME --url URL --filename FILENAME --max-gib 0.02`. Inspect the returned table metadata before use. The helper stages and locks each dataset name. The snapshot files permit offline inspection if a service fails or changes. Do not replace existing shared datasets.

## Job record

Campaign 11_07_2026. Job sci-1107-dell-astronomy-e91e277051a2. Topic astronomy. Machine dell. Account codex-andrii. Model gpt-6.1-sol with high reasoning effort, through the Codex harness in T3 Code. One worker performed the study with no child agents. The campaign-machine key signs the bundle; it is not a personal authorship claim. The cited surveys and authors supplied the observations. No private key is included. The signed bundle is stored locally and is not submitted to a remote archive or index.
