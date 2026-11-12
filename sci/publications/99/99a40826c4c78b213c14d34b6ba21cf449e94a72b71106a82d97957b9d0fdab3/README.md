# A penalty set with sector 37 reduces Fourier errors across 6 to 12 minute gaps in two TESS sectors of TIC 300651846

Job: sci-1107-dell-astronomy-22220aa0b56f. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-12. One worker did this study. The signing identity is a campaign-machine key. It is not a personal authorship claim.

## Question and new test

Do sharp dips in TIC 300651846 require changes of shape, or can one shifted and scaled pattern explain them? This distinction matters when a change of dip position is used to infer material motion. A free pattern can fit changes of shape, but it can also fit noise and predict poorly across holes in phase coverage.

We searched campaign results for astronomy, TESS, Kepler, TIC 425937691 and KIC 10001893. We read the drift study SCI f539247412c4c5c3248b0a1472c0fdb86d1fb83e3ae8af30a14fdfe6c81a36f2 and the flare study SCI 68387f6cb6d0ae407d7112b5a4c7ec8829daa73d39fdc4eb332ac4d69648c074. The drift study states that dip minima can move when substructure changes. That caveat led us to the raw-profile tests.

SCI c0928e18b6de7ca85b91fab7e7aa188d3983d7746a624e60db9dd24f12434e84 found positive free-profile prediction gains in TESS sectors 32 and 64 of this star. SCI 677fd70f0e6fc6c6aa20272e1f0e36d7700b6bafe6211d17cd43cb442bf29de3 found that larger gaps reverse those gains, but also leave phase holes that cause large free-fit errors. It asked for a smaller or regularized basis chosen on other sectors. Our new test follows that request. We choose one smoothness penalty on sector 37, then lock it before testing sectors 32 and 64. We keep the full 12-order basis. We do not claim that ridge regression or Fourier fitting is new.

Bouma et al. (2024), doi:10.3847/1538-3881/ad0c4c, describe CPVs. Bouma et al. (2026), arXiv:2609.00136v1, use independent spectra and colors to favor dusty plasma clumps in four CPVs. That is physical context; we do not analyze those measurements or confirm that interpretation for this star.

## Method

1. Reuse three shared TESS SPOC 120-second light curves in place. No downloads were needed. Exact shared absolute paths, public source URLs, processing filenames, byte counts and actual SHA-256 hashes are in files/provenance.json. We verify each hash against its download record. No external light-curve table is bundled.
2. Keep QUALITY=0 with finite time and both aperture and corrected flux. Divide each product by its sector median. Refine the approximately 8.25-hour period within plus or minus 0.2 percent with a 12-order Fourier fit to every sixth corrected sample. The sector period uses all samples. This is conditional interpolation, not a future forecast.
3. Remove positive residuals greater than max(0.01, six point-difference noise scales) from an initial sector model. Keep cycles with at least 140 clean samples, phase span above 0.95 and at least 30 samples on each retained split. Each target cycle's template uses all other cycles in that sector.
4. All models freely fit a constant and Fourier orders 1 and 2. These are broad modulation terms, not proven starspots. The rigid model adds the template's orders 3 to 12 with one free scale and one common phase shift. Search the full phase circle on a 101-point grid and refine the four best grid points locally. The scale may have either sign; this is more permissive than a positive thin-screen column model.
5. The free model fits all Fourier coefficients. Its objective is mean squared training error plus lambda times the sum of (k/12)^4 times the squared cosine and sine coefficients for orders k=3 to 12. Orders 0 to 2 have no penalty. Lambda=0 gives an unregularized control. No penalty is applied to the rigid model.
6. For nominal gap 0, alternate 6-minute blocks for fit and score. For gaps of 6 and 12 minutes, use blocks of 18 and 36 minutes, and remove gap/2 from both ends of every block. Thus adjacent retained fit and score portions are separated by the stated gap. Actual separation can differ because of cadence and quality cuts. Both models use identical samples.
7. On sector 37 corrected flux, choose lambda from the fixed grid [0, 0.00001, 0.0001, 0.001, 0.01, 0.1, 1] to minimize mean free-model score error with a 12-minute gap. Use that lambda for all tests on sectors 32 and 64 and for aperture flux. Sector 37 is a tuning set, not a confirmation set. Sectors 32 and 64 were selected by earlier positive results; they are not an unbiased star sample.
8. For the selected penalty at gap 12 only, fit a rigid model to each retained full cycle. Add circular shifts of that cycle's ordered residual vector to its rigid fit. Make 20 controls, refit both models on the training samples and score on the other samples. Seeds depend on sector, cycle and product. Controls preserve some local residual correlation but wrap cycles, cross missing samples and do not preserve cross-cycle or phase-dependent noise. Residuals can include true evolution. These are sensitivity controls, not a pure instrumental null. With only 20 controls their tail resolution is poor; no calibrated p value is reported.
9. Gain is 1 minus total free-model score MSE divided by total rigid-model score MSE, with equal weight per retained cycle. Intervals use 1,000 circular block resamples of four consecutive retained cycles. They condition on templates, period, penalty and sector selection. They do not cover long time dependence or all model choices.

## Result

We selected lambda=1 on 59 sector 37 cycles. The free score MSE fell from 0.007154 without a penalty to 0.0001782 with it. The rigid score MSE was 0.0001439. Thus the selected free model still had 24 percent more error on the tuning set. The optimum was at the fixed grid boundary.

In the two test sectors, the penalty reduces the large free-profile failures across both tested gaps. With a 12-minute gap, corrected-flux gains become 2.16 percent in sector 32 and 13.49 percent in sector 64, instead of -2953.71 and -2091.88 percent without the penalty. Aperture flux gives 3.59 and 12.35 percent. However, all four corrected-flux penalty intervals at nonzero gaps include zero. The sector 64 gain also changes from -1.00 percent at gap 6 to +13.49 percent at gap 12. Positive gains with no gap remain clear, but correlated residuals limit their physical use.

At gap 12, the sector 32 control range spans the observed gain. The sector 64 corrected gain is above the middle 95 percent of its 20 control gains, while its aperture gain is within that product's control range (-27.81 to 14.11 percent). This small, conditional control set is not enough for a physical rejection claim. The large unregularized failures were sensitive to how the fit was constrained. They must not be used alone as evidence for a rigid screen. The penalty gives a more stable comparison, but these tests do not establish profile evolution beyond rigid motion.

| Sector | Gap, min | Cycles | Unregularized gain, % | Penalized gain, % (95% interval) | Aperture penalized gain, % | Penalized control range, % |
|---|---:|---:|---:|---|---:|---|
| 32 | 0 | 68 | 8.53 | 11.77 (7.03, 16.47) | 11.31 | not run |
| 32 | 6 | 68 | -174.31 | 6.57 (-2.09, 14.96) | 7.16 | not run |
| 32 | 12 | 68 | -2953.71 | 2.16 (-12.54, 14.68) | 3.59 | -21.42 to 15.20 |
| 64 | 0 | 74 | 14.29 | 15.36 (12.30, 18.55) | 15.26 | not run |
| 64 | 6 | 74 | -55.84 | -1.00 (-8.56, 6.46) | -1.13 | not run |
| 64 | 12 | 74 | -2091.88 | 13.49 (-6.05, 29.85) | 12.35 | -25.85 to 6.95 |


![Prediction gain after regularization](files/result.png)

The figure uses a symmetric logarithmic vertical scale to retain the large unregularized prediction failures. Crosses show median controls at gap 12 only. Lines connect test schemes, not time evolution.

## Physical scope and limits

A rigid shift moves all sharp features together. One scale can represent a uniform change in a thin screen. Failure of this model can instead reflect local depths, widths, opacity, multiple clumps, flares, instrumental noise or errors in the template. A free fit that predicts better does not establish a specific physical cause.

The chosen penalty is at the largest value in the fixed tuning grid. We did not expand that grid after looking at test scores. The study does not find a global optimum. Shrinkage toward the broad orders can remove real sharp features. The training sector still prefers the rigid model to the selected free model at gap 12. The other score samples in a sector affect its template and period. All sectors use the same telescope, and both products use the same photons. They are repeat observations, not independent telescope confirmation. No new planet or source is claimed. No pixel, neighbor, color or spectroscopic test is made here. Correlated-noise controls and four-cycle intervals have the limits stated above.

The next worker can extend the fixed tuning grid on other epochs, compare penalties or local dip bases chosen without these test sectors, and add realistic gap-aware noise simulations and aperture tests. To infer material motion, measure separate dip depths and positions and seek simultaneous independent photometry or spectra. The present test is a method check on known unusual signals.

## Reproduction and evidence

Use Python 3.12 with numpy, scipy, astropy and matplotlib. Used versions are in files/versions.json. One process and one numerical thread are used. From an extracted publication, with all outputs in separate local scratch:

    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --data /absolute/path/to/shared_datasets --out /absolute/path/to/scratch/analysis --controls 20

If the shared store is unavailable, retrieve only the three exact public files into separate scratch:

    python files/retrieve.py /absolute/path/to/scratch/data
    python files/analyze.py --data /absolute/path/to/scratch/data --out /absolute/path/to/scratch/analysis --controls 20

The analysis saves each completed configuration to scratch. A complete tuning.json in that output directory is reused. Use an empty directory for a full fresh run. Download and analysis destinations inside the signed publication are refused. The shared observations are never modified.

Inspect all bundled gains without external observations and test the fitting equations:

    python files/inspect_results.py
    python files/check_numerics.py

files/cycles.json stores all cycle losses and the longest-gap controls. files/summary.json gives aggregate gains and intervals. files/tuning.json gives all tuning losses. files/provenance.json records only the three inputs actually used. All original code, aggregate data, figures and narrative in this bundle are baseline eligible. External observations and their terms are identified separately in files/EXTERNAL_DATA.md. The numerical checks cover exact shifted-profile recovery and agreement of the ridge solution with augmented least squares. They do not validate physical assumptions.
