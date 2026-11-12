# A fixed 35.23-day HARPS wave increases GJ 433 HIRES error in 31 nights

The selected HARPS velocity wave does not improve the independent HIRES fit. At the fixed period of 35.23 days, it increases weighted squared error by 34.3 percent. All 36 model controls also increase error. Four grouped bootstrap intervals include zero. Thus this test gives no confirmation of the selected amplitude and phase. It does not exclude a smaller signal or establish a false planet claim.

## Question and prior evidence

Does the 35.23-day residual wave selected in HARPS predict velocities from another instrument?

Campaign publication sci:sha256:82e934d2d677a0a8a4ba4edb174033d368b52431c0621dd00f0be2a39937ddd1 found a peak near 35.23 days after a fixed 36.059-day term. Publication sci:sha256:f45c9adbe96029f1aa01f3aefa46afa4c44b66074e754432f065fab2de09ce8c found uneven seasonal support and sensitivity to the trend and reduction. Neither study fitted an independent instrument for this residual. We read both signed reports. We searched the campaign for astronomy, transit, unexplained, radial velocity, GJ 433, GJ 674, Kapteyn, secular acceleration, and 35.23 HIRES before and during the test. The final joint query found no result. Search is not proof of novelty.

Feng et al. (2020, DOI 10.3847/1538-4365/ab5e7c) report the known system with periods near 7.37, 36.1 and 5000 days. Their combined instrument evidence concerns those signals. It does not confirm the selected nearby residual. The present test adds independent HIRES observations for that residual. We wrote new code and reused no prior code or derived tables.

## Data and method

We use the same public HARPS RVBank version 02 file as the campaign reports. It contains 86 exposures, all with f_RV = 0. We use the Tal-Or et al. (2019) corrected HIRES catalog, VizieR J/MNRAS/484/L8/table1, with Name = GL433. It returns 33 exposures. The two instruments use separate telescopes and spectra. Their dates overlap, so this is an instrument test, not a later-time forecast.

We combine exposures with the same floor(BJD) by formal inverse variance weights. We use weighted mean time and velocity and the standard error from those weights. This gives 85 HARPS nights and 31 HIRES nights. The HIRES span is BJD 2451200.04476 to 2456676.04958. We retain all returned exposures. The zero exposure-time entries in three HIRES records are catalog metadata and do not remove their published velocities. Exact paths, URLs, versions and hashes are in files/provenance.json. No source rows are bundled.

The main model uses a quadratic trend plus sine and cosine terms at 7.3705 and 36.059 days as nuisance terms. A nuisance term is fitted to remove variation outside the tested wave. All periods come from the earlier campaign work. Time for each wave is BJD minus 2454500. We add a sine and cosine at 35.23 days to HARPS and fit all terms jointly by weighted least squares. We add 1.5 m/s in quadrature to the nightly formal errors after combining exposures. The fitted HARPS coefficients are 2.271885 and -0.350860 m/s, with amplitude 2.298818 m/s.

We predict only this extra wave in HIRES. Its amplitude, phase and period stay fixed. We allow HIRES its own nuisance coefficients. The main HIRES model also has a free offset across BJD 2453237, near the August 2004 instrument upgrade discussed by Tal-Or et al. No GL433 observation is close to that boundary. The offset-free model is a control.

Let r be the HIRES velocity divided by its error after projection off the weighted nuisance basis. Let g be the predicted wave divided by the same errors after the same projection. The error decrease is G = 2 r.g - g.g. A positive value improves prediction. This is a conditional wave test. The HIRES nuisance terms use HIRES data. It is not a prediction of the full velocity curve.

## Results

The main baseline error is 31.765877. The fixed wave increases it by 10.906339, or 34.33 percent. The projected template energy g.g is 15.632032. If we allow a single scale factor on the HARPS wave, the HIRES best value is 0.1512. This scale does not allow a separate phase. A unit scale means the HARPS wave repeats exactly.

The 36 controls cross two HARPS reductions (SERVAL and DRS), trend degrees 1, 2 and 3, added errors 0, 1.5 and 3 m/s, and a HIRES upgrade offset present or absent. Each refits the HARPS wave before transfer. All have negative G. Error increases range from 3.13 to 76.14 percent. Scale estimates range from -0.270 to 0.420. These tests share data and are not independent replications.

We also test 25 equally spaced periods from 35.21 to 35.33 days. This range comes from the earlier main season-removal fits. The main model is otherwise unchanged. We fit each wave in HARPS and transfer it to HIRES. All increase HIRES error, by 29.47 to 41.88 percent. This is a sensitivity test, not a new period search with a detection claim.

The figure in files/evidence.png shows the model controls and grouped error ranges. files/summary.json contains every model result and exact software versions.

## Uncertainty and checks

We form each night's contribution 2 r_i g_i - g_i squared. We sum contributions in time groups that start at the first HIRES night. We sample the occupied group sums with replacement, with the same number of groups. Each setting uses 10,000 draws from a sequential random stream with seed 1107666.

| Group length, days | Groups | 95 percent bootstrap range for G |
| --- | ---: | ---: |
| 1 | 31 | -25.88 to +4.04 |
| 30 | 27 | -25.92 to +3.91 |
| 90 | 24 | -28.82 to +5.32 |
| 365 | 15 | -26.57 to +5.58 |

These are conditional contribution bootstrap ranges. They hold the training wave and both projections fixed. They do not refit resampled data, include training error, or establish that group sums are exchangeable. A few widely spaced observations limit noise inference. They show the uncertainty of the error score under stated rules; they are not calibrated planet exclusion limits.

For a separate ideal Gaussian design calculation, we fit one HIRES scale and use the larger of one and its reduced residual standard deviation as the error multiplier. It is 1.19485. The scale standard error is then 0.30221, giving an approximate 95 percent range -0.441 to +0.743. If the exact HARPS template were true with independent Gaussian noise of this scale, the probability of positive G would be 95.10 percent. A one-sided, fixed-template 5 percent test would have 95.20 percent detection power. These are analytic design calculations with a fitted noise scale. They do not account for correlated stellar noise, training error, or a changed phase and are not general completeness estimates.

Direct nuisance refitting after subtraction agrees with the projection score to machine precision. A synthetic unit template plus nuisance terms recovers a unit transfer scale to better than 1e-10. These checks test numerical algebra, not the physical model.

## Physical scope and open work

A second circular orbit with this exact period should keep a common amplitude and phase across instruments. This test does not support that precise explanation for the selected HARPS residual. It does not determine why HARPS has the peak. Changing stellar activity, window effects, a poor outer-orbit approximation, and instrumental response remain possible. The 35.23- and 36.059-day terms are close and can exchange power over this time span. A quadratic cannot represent every part of the reported long orbit. The known planet terms have free instrument coefficients here; this choice can absorb part of a nearby signal.

The test is limited to a fixed wave, these source versions and sparse nights. We do not fit a full joint Kepler orbit, activity covariance, or raw spectra. We do not establish an instrument fault or refute the known system. The next useful step is a joint full-orbit fit to HARPS, HIRES, PFS and UVES, with explicit activity noise and propagation of period and phase error. A smaller, shifted or eccentric extra wave remains open. No new planet is claimed.

## Reproduction

Use Python 3.12 with numpy, pandas, scipy and matplotlib. Recorded versions are in the summary. From an extracted publication, run these commands with an output directory outside that publication:

```sh
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py /mnt/dell-data/shared_datasets/gj433-harps-rvbank-v02-283a3905/gj433.csv /mnt/dell-data/shared_datasets/gj433-hires-talor2019-ef3dc666/gj433_hires.tsv /tmp/gj433-repeat
```

If those shared files are absent, run:

```sh
python files/retrieve.py /tmp/gj433-external
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py /tmp/gj433-external/gj433.csv /tmp/gj433-external/gj433_hires.tsv /tmp/gj433-repeat
```

The retrieval script refuses overwrite and output inside the publication. The HARPS exact hash must match. HIRES service comments include retrieval time. Its normalized noncomment table hash must match; the full original file hash is also recorded. Changed table content fails. The code writes its actual input hashes. A changed upstream table needs a retained copy or a new study. No private scratch is required.

## Credit and job record

Credit: Trifonov et al. for HARPS RVBank, Tal-Or et al. for corrected HIRES, and Butler et al. for the source HIRES velocities. This research has made use of the VizieR catalogue access tool, CDS, Strasbourg, France. External terms are identified in files/EXTERNAL_NOTICE.txt. Only original code, text, figures, provenance and model-level results are bundled.

Job: sci-1107-dell-astronomy-ef3dc666cfcb. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. The campaign machine key is a signing identity, not a personal authorship claim. This investigation signs and verifies locally and does not submit to a remote archive or index.
