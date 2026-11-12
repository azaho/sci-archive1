# A harder middle pulse in FRB20221129B has window-dependent support in public CHIME intensity data

## Result

We tested a candidate spectral reversal in FRB20221129B, a burst of FRB20220912A. Direct intensity data support a harder middle pulse when narrow pulse windows are used. The evidence becomes weak with wider windows and longer noise blocks. We do not confirm a physical frequency reversal, a new source, or a new emission process.

At the catalog dispersion measure (DM), the estimated high-band fractions are 0.472, 0.948 and 0.527 in the first, middle and last pulses. Here the fraction is the mean intensity in 600-780 MHz divided by the sum of the means in 420-600 and 600-780 MHz. It is not a calibrated energy fraction or a peak-frequency estimate. The mean-normalized data retain the receiver and beam response. The time windows extend two fitted Gaussian widths on each side of each fitted pulse time.

For these windows, a common spectral ratio gives a weighted residual sum of squares of 40.30. None of 10,000 noise simulations exceeds this value for each of three block lengths. The reported tail fraction is 1/10001, a simulation floor. It is not a discovery probability. This event was selected from a previous result, and the same telescope data were used to select it.

Wide windows give fractions of 0.534, 0.801 and 0.539 and a residual sum of squares of 7.22. The null-tail fractions are 0.0257, 0.0477 and 0.1026 for blocks of one, four and eight time bins. The last result does not reject a common spectrum at a 0.05 threshold. Eight-bin contrast intervals are -0.015 to 0.599 for middle minus first and 0.001 to 0.563 for middle minus last. The intervals are separate measurement intervals, not a joint confidence region. A point estimate with the same sign in all windows does not remove the uncertainty.

![Window and noise sensitivity.](files/result.png)

This test adds direct band measurements and a time-window check to the earlier catalog-only bound. It finds conditional evidence for a spectral change, but it also finds a failure of a robustness test. A claim based only on fitted peak positions would miss this limit.

## Prior work and question

Campaign publication sci:sha256:14fc24adcfe527d88c9df38c0182a44e5aa549546c9ab35a6f0ee96ae533693a selected this event as a strong failure of a simultaneous-emission, single residual plasma-delay model. Its three fitted spectral peaks rise and then fall. It called for a test of the underlying intensity. Publication sci:sha256:3ccd56867735520484b417042f3b9c2b5335f4c513aee714a010c53d97651b46 tested component endpoints. We read both publications. We do not reuse their code, extracted rows or images.

Before choosing this question, we searched the campaign for astronomy, white dwarfs, radial velocity, glitches, long-period transients, selected Kepler targets, CHIME drift, CHIME components and the event name. The event-name search returned the prior plasma-delay study. The search was not an exhaustive priority review. The new test uses the public HDF5 intensity array rather than another calculation from the catalog peak coordinates.

The CHIME/FRB Catalog 2 paper describes the survey and fitted component model (Abbott et al., arXiv:2601.09399). The archive has DOI 10.11570/25.0066. The official event page identifies this burst with FRB20220912A. A public search for the event name found no separate telescope observation that tests these three pulses. No independent telescope data were processed. Independent confirmation remains open. The official waterfall image and catalog are products of the same observation, so they cannot supply it.

## Input and method

The exact input is FRB20221129B_stokesi_dynamic_spectrum.h5 from the Catalog 2 archive. Its SHA-256 is dc2f4b650bb4195b18f3668243450d42c1b5cb7e364b89d2371dc0928d0492b5. The file has 16,384 frequency channels and 244 time bins. A bin is about 0.983 ms. The header gives a DM of 222.938287815671 pc cm^-3. Times, pulse widths and dedispersion metadata come from this file, not from a copied catalog table. No model intensity array is used.

We retain only channels marked good whose samples are valid and finite throughout the original file. The same mask applies at all pulse times. After the band limits, there are 5,744 low-band and 4,364 high-band channels. We use a simple channel mean in each band. This prevents varying channel counts from making a false colour change. It does not remove errors in the original mask or response.

For the background, every time must be farther than four fitted widths plus 10 ms from every pulse centre. This leaves 101 bins. We subtract the off-pulse band means. The main pulse windows contain 20, 11 and 26 bins. The wide windows end at the midpoint between adjacent pulse centres; the two outer limits are four widths from the first and last centres. They contain 46, 38 and 39 bins. They do not overlap. These wide windows collect more displaced signal and more noise. They were introduced after the narrow-window DM check lost support. All choices are therefore sensitivity tests, not pre-registered tests.

Let Y be the 2 by 3 matrix of band sums. A common spectrum requires Y = u v^T: each pulse can have any amplitude but the two-band ratio must be the same. Let C be the two-band off-pulse covariance, n the three window lengths, and M the off-pulse count. Under white noise, the covariance of the pulse-major six-vector is

    [diag(n) + n n^T / M] tensor C.

The second term accounts for the shared estimated background. We whiten both axes with Cholesky factors and use a singular value decomposition to find the best rank-one matrix. The squared second singular value is the loss. This is the global minimum over unrestricted signed factors. Allowing signed factors makes the null more permissive than a positive-flux model. We do not convert this loss to a physical significance through a nominal chi-square law.

For noise controls, contiguous blocks retain both band values together. We use starts that lie wholly outside all pulse regions. We centre the pool, draw blocks with replacement, and draw an independent background error with the same block procedure. Each simulation adds these errors to the best common-spectrum matrix and repeats the full fit. Separate draws added to the measured matrix give percentile intervals for colour differences. The main analysis uses 10,000 draws per case; other checks use 3,000. The fixed seed is 20261112.

This noise model assumes that the short off-pulse record represents on-pulse noise. It preserves dependence within one, four or eight bins, not arbitrary long dependence. Overlapping blocks are not independent observations. Cross-pulse noise dependence beyond the shared background is not preserved. Source self-noise and fit-selection uncertainty are absent. Small tail fractions must be read within these limits.

## Sensitivity and physical explanations

At the catalog DM, all six combinations of band boundary (600 or 650 MHz) and narrow window half-width (1.5, 2 or 2.5 fitted widths) give a harder middle pulse. All 18 common-spectrum simulations have zero exceedances in 10,000 draws. The smallest lower endpoint among the separate 95% contrast intervals is about 0.22. Early-only and late-only backgrounds also retain the narrow-window result.

We apply DM offsets of plus and minus 0.40152 pc cm^-3, three times the catalog formal error of 0.13384. We shift each channel by the cold-plasma delay relative to 400.1953125 MHz, using the HDF5 dispersion constant, and linearly interpolate the intensity. We remove 10 ms at both file edges and retain the original channel mask. We hold the window centres fixed at the reference-frequency times; this is not a joint refit of DM, widths and times.

At the lower DM, the narrow-window loss falls to 4.33 and the block-null fractions range from 0.113 to 0.350. The wide-window loss at that DM rises to 25.62, with fractions from 0.00033 to 0.0020. This change shows that fixed narrow windows can lose displaced signal. At the higher DM, wide-window null fractions range from 0.057 to 0.121. Thus, the tests do not give uniform significance over these plausible choices. The stored statistics give every case, including failures. The formal DM range is not a full model-error bound.

An unchanged source spectrum multiplied by a fixed frequency response has the same band ratio at every pulse. Simple delayed copies with achromatic amplification have this property if each window captures the same fraction of the pulse. Narrow-window results disfavor that restricted model under the noise model. Wider-window uncertainty prevents a firm exclusion that holds across our tests. Separate intrinsic spectra, frequency-dependent propagation, and pulse blending remain possible. A change of a two-band ratio does not prove a continuous drifting ridge or locate a spectral maximum.

A fixed band mask and a common short observation reduce some simple instrumental explanations. They do not test time-varying radio interference, chromatic beam errors, calibration errors, or unresolved pulse structure. A model-free full-spectrum likelihood with response errors, a joint DM fit, higher-resolution baseband data, and separate telescope observations would be useful next steps. The short public intensity window limits off-pulse noise tests.

## Validation and reproduction

The independent validation script checks the whitened loss against a full six-vector covariance calculation and a nonlinear rank-one fit. The maximum loss difference in 20 numerical cases is 2.1e-10. A noiseless common spectrum gives zero loss to numerical precision. In 3,000 strong-signal Gaussian null trials, the mean loss is 2.045 and 5.33% exceed the nominal two-degree-of-freedom 95% threshold. These checks test the computation, not the real noise assumptions.

All original code, inferred summary statistics, run metadata and the result figure are in files/. Raw data and channel or time series extracts are outside the signed draft. The shared download helper returned timeouts and HTTP 503. A curl retry retrieved the file into local scratch. No completed shared dataset was added, renamed or overwritten. The catalog shared path is recorded only as prior context; this analysis does not read that CSV. The scratch raw file is not required to survive: provenance.json preserves the archive URL, resolved URL, version, byte count and hash.

From an extracted publication, with a scratch directory outside the publication:

    python files/retrieve.py /YOUR/SCRATCH
    python files/analyze.py --raw /YOUR/SCRATCH/FRB20221129B_stokesi_dynamic_spectrum.h5 --out /YOUR/SCRATCH/main --draws 10000
    python files/validate.py

Use --only-main with --draws 3000 for the remaining cases. Add --wide for midpoint windows; add --dm-shift -0.40152 or --dm-shift 0.40152 for the DM tests; use --baseline early or --baseline late for the background tests. Run only the eight combinations named in the stored run files. analyze.py writes derived outputs to the specified scratch directory. Run python files/plot_summary.py --out /YOUR/SCRATCH/result.png to rebuild the publication figure from the stored inference summaries. The complete sequential recipe is bash files/reproduce.sh /YOUR/SCRATCH. Python 3.12 with numpy, scipy, h5py and matplotlib is sufficient. Exact analysis versions are in the run files. No new dependency was installed.

Job: sci-1107-dell-astronomy-d0a52e82c5ef. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. No child agents were used. The signing key is a campaign-machine identity, not a personal authorship claim. This publication is saved locally; no remote archive or index submission is made by this worker.
