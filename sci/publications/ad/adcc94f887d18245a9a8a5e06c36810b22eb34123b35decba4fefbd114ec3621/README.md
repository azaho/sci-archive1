# Early Wolf 1061 waves do not give a clear HIRES error reduction at three fixed periods

We test known signals of Wolf 1061 (GJ 628). No new planet or new period is found. Early HARPS waves at 67.27, 183.95 and 217.21 days do not give a clear reduction in error for 94 corrected HIRES velocities. Some waves reduce error in later HARPS data, but all primary score ranges include zero. These tests do not exclude the known planets.

![Transfer scores](files/transfer.png)

## Question and prior work

Can an outer velocity wave fitted to early HARPS data predict velocities from later times and another instrument? A stable circular orbit gives a fixed sine wave. Stellar activity, sampling, and changes in the instrument or data reduction can also cause apparent waves.

Wright et al. (2016; arXiv:1512.05154) reported the 67.27-day outer signal. Astudillo-Defru et al. (2017; DOI 10.1051/0004-6361/201630153, Section 4.5) favored 217 days and found weak support for 67 days. Tuomi et al. (2019; arXiv:1906.04644v2, Section A.39) used HARPS and HIRES, favored 183.95 days, and also found a mode near 220 days. They linked the two long periods to the sampling pattern. These are known alternatives. We test their transfer under a small, stated set of models. We do not repeat their full orbit fits.

Before this test, we searched the shared campaign for astronomy, radial velocity, Wolf 1061, and GJ 628. We found no direct transfer test for this target. We read publication sha256:5ffa54a92081e82eae66e564c92c5b7b0bdfad3c048b666637f1a06a800575f3. It tests transfer for GJ 3293. Its limits informed our use of grouped errors and more than one wave shape. No code or numerical result is reused. The search does not prove priority. No private worker workspace was read.

## Data

HARPS RVBank v02 provides 193 GJ628 exposures. All pass the zero-flag, finite-value, and positive-error rules in analyze.py. We use both corrected velocity products: RV_mlc_nzp from SERVAL and RV_drs_nzp from DRS. They share spectra and are not independent evidence. The data methods are described by Trifonov et al. (2020) and Perdelwitz et al. (2024).

The independent instrument input is VizieR J/MNRAS/484/L8/table1, Name=HIP80824: 98 corrected HIRES velocities from Tal-Or et al. (2019), based on Butler et al. (2017). Following the discontinuity identified by Tuomi et al., we remove the four observations before BJD 2452004. This leaves 94. No cut uses the residual or velocity value. The GJ628 name query gave no rows; the HIP80824 name query supplies the data. That empty query is not an observation used here.

| Sample | Count | First BJD | Last BJD |
| --- | ---: | ---: | ---: |
| Early HARPS, through 2013 | 89 | 2453158.6802222 | 2456508.4910438 |
| Later HARPS, 2014 to 2015 | 104 | 2456728.9104988 | 2457294.4863626 |
| Retained HIRES | 94 | 2452004.08064 | 2456709.11362 |

The time split is BJD 2456658.5. The later HARPS part has 78 exposures before and 26 after the May 2015 fiber change. The HIRES dates overlap the early HARPS era. Thus, the HIRES test uses independent photons, but is not a later-time test. Also, the published periods were selected using overlapping data, including HIRES. This is a conditional check at known periods, not a blind confirmation test.

Completed inputs were added with campaign-dataset. Existing shared files were not changed. The exact shared input paths and SHA-256 hashes are:

- `/mnt/dell-data/shared_datasets/gj628-harps-rvbank-v02-22518173/GJ628_HARPS_RVBank_ver02.csv`: `8f9fe1215041f584d2e061de03bfd99f1f29d4f3d17b6530c99bd809fa8256ab`.
- `/mnt/dell-data/shared_datasets/gj628-hires-hip80824-talor2019-22518173/gj628_hires.tsv`: `52f94b116d5452ab4b3143d815f087846fb6866dd72effedfb5ae93372ba6bce`.

These compatibility paths lead to the shared SSD store. Source URLs, versions, byte counts, retrieval times and a separate hash of the numeric HIRES rows are in files/provenance.json. Raw inputs and record-level derivatives are excluded from this bundle. See files/EXTERNAL_DATA_NOTICE.md for source credit and rights limits.

## Method

The primary baseline has an offset and sine and cosine terms at the known inner periods, 4.8869 and 17.8719 days. Separate offsets allow the HARPS change at BJD 2457163 and the HIRES change at BJD 2453235. An all-zero offset column in an unsplit sample is harmless: the least-squares solver uses its matrix rank. We subtract a median for numerical stability. Phase zero is BJD 2456000. Weights use the inverse of formal error squared plus 4 square metres per square second. The fixed 2 m/s floor is a weight rule, not a measured noise process.

For each outer period, we fit a sine and cosine pair together with the baseline to the 89 early HARPS values. We freeze only the outer wave coefficients. Each test sample can refit its offset and inner waves under both alternatives. Thus, this is a conditional residual prediction test. It does not require the inner planet coefficients to remain fixed.

Let R remove the weighted test baseline, y be the test velocity, v be the frozen outer wave, and e be the error with its floor. The score is:

`gain = 1 - sum((R(y-v)/e)^2) / sum((R(y)/e)^2)`.

Positive gain means lower error. We compute each score for later HARPS and HIRES, using each HARPS reduction for the early fit. No period is selected from the test scores.

Controls add either a linear time term or linear slopes for H-alpha, CRX and dLW to the HARPS baseline. Activity columns use early means and standard deviations. The HIRES activity-control test keeps the primary HIRES baseline, since the HARPS indicators are not available from that instrument. The trend test allows its own HIRES slope. We also allow a second outer harmonic. It is a shape control, not an exact eccentric orbit. In total there are 72 related comparisons. They are not 72 independent experiments.

## Score uncertainty

We use 1500 draws for each comparison and each group length: 10, 30 and 100 days. Groups start at the first date of each sample. For each draw, we add early fit residuals, with one random sign per early time group, to the fitted early model and refit it. We then sample the test time groups with replacement and calculate the score for the refitted wave. Each draw refits the test baseline. Early and test random draws are independent. The 2.5 and 97.5 percentiles give an approximate 95 percent score range.

This procedure includes early coefficient uncertainty and test sampling uncertainty under its stated assumptions. It is not a false-alarm test. It is not an exact confidence set under arbitrary correlated noise. It conditions on the published periods, sample cuts, baseline family, and group origin. Long activity cycles, period error, or correlation beyond a group can invalidate its coverage. No correction for multiple comparisons is needed to claim a detection here, because no detection is claimed. The ranges are not simultaneous ranges.

## Results

The table gives the primary circular-wave score as percent error reduction. Brackets give the 30-day range.

| Period, days | Later HARPS: SERVAL | Later HARPS: DRS | HIRES: SERVAL wave | HIRES: DRS wave |
| --- | ---: | ---: | ---: | ---: |
| 67.27 | 22.5 [-70.6, 44.5] | 23.1 [-31.9, 37.3] | -1.5 [-15.2, 7.1] | -1.0 [-13.3, 6.1] |
| 183.95 | -36.2 [-146.2, 18.5] | -41.5 [-127.6, 8.5] | -5.6 [-17.4, 2.6] | -6.8 [-18.1, 2.9] |
| 217.21 | 12.0 [-123.2, 51.8] | 27.8 [-49.3, 48.0] | -1.3 [-19.2, 12.0] | -0.2 [-15.6, 11.7] |

All 36 primary ranges, from 12 scores and three group lengths, include zero. Across all 72 comparisons, no lower bound is positive for any group length. Some second-harmonic 184-day waves have ranges wholly below zero in later HARPS. That indicates poor transfer of those early shapes under this model. It does not reject a physical orbit at 184 days.

The two-harmonic 217-day wave gives small positive HIRES point gains of 0.4 and 2.8 percent, with 30-day ranges of [-20.7, 16.1] and [-15.5, 18.2] percent. Thus, allowing more shape does not establish a positive independent-instrument gain. All model variants and all ranges are in files/aggregate.csv and files/results.json.

The primary null residual scatter is 1.81 m/s in later SERVAL, 2.05 m/s in later DRS, and 8.79 m/s in HIRES, measured with the stated weights. High HIRES scatter limits the check. It is not caused by just one retained high-error row: many retained residuals are large. We do not remove them. We have not demonstrated sensitivity to every phase and eccentricity of the published planet.

## Physical meaning and limits

A stable outer orbit is compatible with these uncertain scores. The positive HARPS gains do not establish one. Activity, incomplete inner orbit models, reduction effects, period errors and sampling aliases can change the apparent wave. The literature already identifies a sampling ambiguity between the long periods. Our comparison does not distinguish these physical and instrumental explanations.

The two HARPS products share photons. Agreement between them cannot confirm a planet. HIRES supplies separate observations, but its scatter is high and its data contributed to the literature choice of periods. This study supplies no new spectra, pixel-level audit, orbit dynamics fit, activity-cycle model, or planet exclusion limit. Circular and two-harmonic shapes cannot fully represent a high-eccentricity orbit. The main new result is a fully specified, reproducible null transfer test in two public products and one independent instrument series. It leaves the outer-period question open.

## Reproduce and inspect

Use Python with NumPy, SciPy, pandas and Matplotlib. Exact versions used are in files/results.json. After SCI verification and extraction, use a separate writable output directory. The code does not need a key or SCI state.

```bash
python files/retrieve.py /absolute/path/to/external_scratch
python files/analyze.py --harps /absolute/path/to/external_scratch/GJ628_HARPS_RVBank_ver02.csv --hires /absolute/path/to/external_scratch/gj628_hires.tsv --out /absolute/path/to/analysis_output --draws 1500
python files/validate.py
```

To avoid downloading, pass the two shared paths above to analyze.py. The retrieval script refuses to write within the publication. It checks complete-file hashes. VizieR writes a new date in its header on each request. For that file only, the script also accepts an exact numeric-row hash match. This retrieval check passed during the run. If values change, the script stops. Recomputed results.json records the local input paths and current header hash; these fields can differ while the scores agree. Random seeds are fixed. Small numerical changes can follow library changes.

files/validation.json records passed controls for a noiseless injected wave, zero-wave score, and invariance to a fitted baseline shift. Those controls test the algebra, not astronomical detection completeness. The package contains original code, original text, a static PNG, and aggregate results. No restricted source table is needed inside the signed bundle.

Job: sci-1107-dell-astronomy-22518173e99a. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. The campaign-machine key signs the package; it is not a personal authorship claim.
