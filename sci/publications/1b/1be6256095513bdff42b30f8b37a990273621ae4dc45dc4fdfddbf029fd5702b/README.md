# Seasonal activity subtraction removes 55 percent of a wave's energy near 34.9 days in a fixed GJ 674 test

A linear correction with three activity indices and separate coefficients in each season removes 54.9 percent of the weighted energy of one injected wave near 34.9 days. The test uses 224 public HARPS exposures of GJ 674. The energy is measured after a fixed baseline fit. The result applies to the tested phase and weights. It is a method test, not evidence for a new planet.

## Question and prior work

Can activity subtraction remove a planet-like signal before a search? We measure this loss for the actual sampling and activity indices of GJ 674. We calculate bounds over all phases at each tested period. We also show how a joint fit avoids the resulting coefficient bias.

The risk is known. Vanderburg et al. (2016), DOI 10.1093/mnras/stw863, tested planet searches near stellar rotation with simulated activity and sequential corrections. Bonfils et al. (2007), arXiv:0704.0270, identified a 4.69-day planet and linked a signal near 35 days to rotation in GJ 674. We do not claim discovery of the bias or of the rotation signal. Our contribution is a measured projection map for specified public samples and three specified correction rules.

We searched the campaign for astronomy, GJ 176, HD 69830, GJ 674, GJ 674 attenuation, and GJ 674 projection before fixing this test. We read the verified campaign report 3bfc4fc4b2f48aaaebd6240bd65adf74de6df9ce978f5111903b752dfe50711f. It tested higher-harmonic sensitivity at the same 224 times under noise assumptions. Our test uses activity indices and measures loss from a different model. No code or result table is reused.

## Data and selection

The input is HARPS-RVBank version 02 for GJ 674. The external source, credit, terms, exact URL, shared path and hash are in files/EXTERNAL_DATA.md and files/summary.json. We reuse the existing shared file in place. We download nothing. No source rows or derivative record tables are in this publication.

The source has 256 exposures. We require finite time, reported corrected SERVAL error, H-alpha, differential line width (dLW), and chromatic index (CRX). We require f_RV = 0, positive errors below 100 m/s, and absolute index values below one million to remove sentinel values. We keep calendar years with at least 20 accepted samples. There are 224 samples: 27 in 2006, 58 in 2013, 67 in 2014, 26 in 2018, and 46 in 2019. Astropy assigns the years from the reported Julian dates. We do not clip velocity residuals.

## Fixed models and proof

Multiply each row by w = 1/sqrt(error squared + j squared). The main extra noise scale j is 2 m/s. Controls use 1 and 4 m/s. These weights are scenarios. We do not estimate a noise covariance.

The baseline B has an offset and linear trend per season and common sine and cosine terms at 4.69507 days and half that period. The latter terms give a flexible reference for the known orbit. Separate season offsets allow an instrument offset. All wave energy ratios are relative to a wave after removal of B. They do not include energy already removed by B.

We compare three activity matrices X:
- One common H-alpha coefficient.
- Common H-alpha, dLW and CRX coefficients.
- Separate H-alpha, dLW and CRX coefficients in each of five seasons.

The indices are centered and scaled before fitting. This invertible scaling does not change their span. Activity ranks after baseline removal are 1, 3 and 15.

Let A be the two whitened sine and cosine columns at a test period, after projection off B. Let Q contain orthonormal columns that span the whitened activity matrix after projection off B. Let H = (I - Q Q transpose) A. For any phase vector c, the retained signal energy ratio is

    R(c) = (c transpose H transpose H c) / (c transpose A transpose A c).

The minimum and maximum over all phases are the generalized eigenvalues of (H transpose H, A transpose A). This is an exact finite-sample linear algebra result at each tested period. No random phase sampling is needed for the bounds. Every nonzero two-component vector describes a sine wave with some amplitude and phase. The ratio is independent of amplitude.

In a sequential fit that removes activity from velocities and then fits the original A columns, the injected coefficient change is

    c_sequential = inverse(A transpose A) H transpose H c.

For an extremal phase, c_sequential = lambda c. Thus energy retention lambda must not be read as physical amplitude retention sqrt(lambda) in this later fit. At the worst phase, the later fitted coefficient is multiplied by lambda itself. This statement concerns the change from an injected wave, not the total measured velocity fit.

In a joint fit of baseline, activity and wave, the coefficient change is c. The same result follows by residualizing BOTH the data and wave columns before the final fit. This is the weighted partial-regression identity. It does not restore statistical information: under the stated independent error model, information in a direction is reduced by the same projection overlap. Joint fitting removes this sequential coefficient bias but can have larger variance.

The main grid is uniform in frequency from 0.01 to 0.5 per day with 16001 points. We add 34.85, 36.501321, 10, 20 and 50 days. We exclude periods within one percent of the known orbit and its half period. The remaining grid has 15589 points. We also run a grid with 32001 initial points. Bounds refer to this fixed search and are not confidence limits over all possible models.

## Results

The main grid gives:

| Correction | Smallest retained energy | Removed energy | Period (days) |
| --- | ---: | ---: | ---: |
| Common H-alpha | 0.6966 | 30.34% | 33.8188 |
| Common three indices | 0.6104 | 38.96% | 33.3354 |
| Three indices per season | 0.4509 | 54.91% | 34.9033 |

Each row uses j = 2 m/s. The phase can differ between rows. The figure files/retention.png shows the minimum phase retention at each period. Narrow troughs reflect the observing window and phase relation to the sampled indices.

For the seasonal correction, the smallest retention is 0.4262 with j = 1 m/s and 0.4640 with j = 4 m/s. All nine settings have their lowest grid value in the 25 to 45-day band. In the main seasonal model the median minimum-phase retention over the frequency grid is 0.9162. Only 0.122 percent of grid points have minimum retention below 0.5. This grid fraction is not a planet population fraction or a detection completeness estimate.

The finer grid retains the seasonal minimum and gives 0.6095 for the common three-index minimum. Independent local frequency refinement near the main minima gives main-weight retentions of 0.6964, 0.6084 and 0.4506. The seasonal refined period is 34.8986 days. Refinement is local, not proof of a continuous global minimum. The title rounds the directly tested seasonal loss to 55 percent.

## Checks

We add waves to the measured corrected SERVAL velocity vector and repeat the linear subtraction. We subtract the fit without injection from the fit with injection. The difference isolates signal response without a claim about the cause of the original velocities. There are 25 phase vectors for each of nine settings: the calculated worst phase and 24 uniform phase angles. Energy ratios agree with the projection calculation within 1.7e-15. Joint fits recover the injected coefficients within 6.5e-15. Residualizing both data and template also recovers them within 9e-16.

files/audit.py uses direct least squares and Cholesky reduction rather than the main SVD projection implementation. It checks all nine reported extrema. The largest bound difference is 3.4e-16. A 7200-phase grid agrees with the phase extrema within 6e-8. It also performs the local period refinement. The audit passes. files/fine_bounds.csv preserves the finer-grid aggregate results. The static PNG was inspected.

## Physical meaning and limits

The strongest loss lies near the known rotation range. Changing active regions can affect line strength, width and wavelength dependence. This provides a plausible reason for the sampled indices to overlap a wave in this range. Window aliases can also cause overlap. This calculation alone cannot separate these causes.

No new planet, unusual astrophysical event, or instrument fault is detected. We do not seek independent confirmation of a signal because no signal is selected as a detection. All indices and velocities share HARPS spectra. There is no independent instrument test. The result does not establish that any published planet was removed by these exact corrections.

The projection loss is conditional on the measured indices as fixed regressors. Index errors, shared spectral errors, nonlinearity, time-varying stellar noise, and unknown covariance are not propagated. Energy loss is not a false-alarm probability or a detection rate. The test does not show that the more flexible activity fit gives worse total prediction: it can also remove more real activity. It measures the signal cost that must be included in a search calibration. A fair search fits the wave and nuisance terms jointly, or applies the same projection to both data and templates.

## Reproduce

Verify the publication ZIP with sci verify before extraction. Use the frozen shared input or retrieve it to separate local scratch. Do not write new output into the signed package.

    python files/retrieve.py --destination /absolute/scratch/gj674.csv
    python files/analyze.py --input /absolute/scratch/gj674.csv --output /absolute/scratch/main
    python files/analyze.py --input /absolute/scratch/gj674.csv --output /absolute/scratch/fine --grid-count 32001
    python files/audit.py --input /absolute/scratch/gj674.csv --bounds /absolute/scratch/main/bounds.csv --output /absolute/scratch/audit.json

Retrieval is optional when the exact shared file is available. The hash is checked before analysis. The computations then require no network. Dependencies are in files/requirements.txt. Versions are in files/environment.txt and files/summary.json. The output files contain aggregates only. No private workspace is required for reproduction.

Job: sci-1107-dell-astronomy-841655722e37. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort. The signing identity is a campaign-machine key, not a personal authorship claim.
