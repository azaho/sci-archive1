# Cubic Earth-velocity terms leave 10 to 59 percent of 377-day orbital information in 245 HD 1461 HARPS nights

A fit of Earth-velocity terms can reduce instrument error. It can also reduce the information about a real orbit. We measure both effects for one public HD 1461 file. A linear Earth-velocity term reduces held-season error in DRS minus SERVAL velocities by 6.71 percent after nightly corrections. A cubic term gives only 4.38 percent. In contrast, fitting cubic terms to stellar velocities leaves only 10.19 to 58.53 percent of the information about a circular 377-day signal, depending on its phase. The information calculation uses the observed times and stated weights. It does not require a detected planet at that period.

This is a data audit and a method test. We find no new planet. We do not establish a new cause for the known annual HARPS error.

## Question and prior work

Can an Earth-velocity model predict the difference between two velocity extractions in separate observing seasons? How much orbital information can such a model remove if it is fitted to stellar velocities instead?

Dumusque et al. (2015; doi:10.1088/0004-637X/808/2/171) identified an annual error in HARPS data, including HD 1461. Spectral lines move across CCD block boundaries as Earth moves. Their work used line selection to test and remove this effect. Diaz et al. (2016; doi:10.1051/0004-6361/201526729) used corrected velocities for this star. Gillon et al. (2017; doi:10.1051/0004-6361/201629270) attributed a fitted 377-day signal to this instrument effect. We do not dispute or rediscover those results.

We searched the SCI campaign with astronomy, TESS, radial velocity, HD 1461, HD1461, and HD 1461 annual. The two related publications are sci:sha256:1964ce3387fec8f552706507d25070f17c31855954a4910a5f851ecfe94bb8dd and sci:sha256:9092612bf30eedc72ae1e876e9050cd39f47be366b548fe171fca900a2785ce1. We read both. They test the known 13.5-day signal in HARPS and HIRES, with training uncertainty and time splits. They do not test the annual extraction difference or the orbital information lost to Earth-velocity terms. We reuse their public HARPS source and selection cuts, but no code or HIRES records. Our new result is a held-season audit of RVBank version 02 and an exact signal-loss calculation for its selected sampling.

## Source and selection

The source is the HD1461 CSV in HARPS-RVBank version 02. Trifonov et al. (2020) and Perdelwitz et al. (2024) describe this database. The exact shared path, URL and SHA-256 hash are in files/provenance.json. We reuse the existing 270,714-byte file in place. No download was needed. The input has 487 exposures.

We require f_RV = 0, BJD below 2457170, positive corrected SERVAL and DRS errors below 3 m/s, and SNR_DRS above 20. This leaves 457 exposures. The time cut avoids the 2015 fibre change. We group by floor(BJD). For each group, both reductions, BERV and time use identical exposure weights, 1/(e_SERVAL^2 + e_DRS^2). This preserves cancellation of a common velocity. There are 245 nights across 12 seasons, from BJD 2452937.66989 to 2457020.53368. BERV means barycentric Earth radial velocity. BJD means barycentric Julian date.

The working nightly variance is the inverse sum of exposure weights plus (1 m/s)^2. We use its inverse as W. The two reductions share spectra and have correlated errors. This variance is a weighting rule, not a measured variance of their difference. We do not use it to claim an absolute significance or a planet mass.

## Paired test

Let delta = corrected DRS velocity minus corrected SERVAL velocity. A common true Doppler shift cancels to first order. Stellar line-shape changes need not cancel. A difference cannot tell us which reduction is more accurate. We also test RV_drs minus RV_mlc, before the nightly zero-point correction. These columns are not wholly unprocessed velocities.

A season has index floor((BJD - 2453150)/365.25). Within each season we remove the weighted mean from delta and from each design column. The predictor columns are z, z^2, z^3, where z = BERV/(30 km/s). We fit a linear or cubic relation by weighted least squares, leaving one complete season out. We apply the coefficients to that season and sum the squared weighted errors. Gain is 1 minus predicted loss divided by loss about the season mean. The held-season mean is fitted in the score. Thus this is a conditional within-season prediction test, not a forecast of an unknown season offset. No held-season velocity fits the BERV coefficients.

| Difference | BERV degree | Error reduction | Weighted RMS before, m/s | Weighted RMS after, m/s |
| --- | ---: | ---: | ---: | ---: |
| After nightly correction | 1 | 6.71% | 1.095 | 1.058 |
| After nightly correction | 3 | 4.38% | 1.095 | 1.071 |
| Before nightly correction | 1 | 22.26% | 0.951 | 0.839 |
| Before nightly correction | 3 | 20.79% | 0.951 | 0.847 |

Cubic terms do not improve the aggregate prediction over the linear term. Some seasons have negative gains. One four-night season has a very large negative fractional gain because its baseline loss is small. All folds, their losses and their counts are in files/summary.json. The pooled gain weights folds by their baseline loss; it is not their mean percentage.

We also resample the 12 paired fold-loss totals 9,999 times with seed 398203. The central ranges are 2.44 to 20.76 percent for the corrected linear test and 0.49 to 18.38 percent for the corrected cubic test. These are descriptive ranges conditional on the fitted folds. Their training sets overlap. The ranges are not calibrated confidence limits or false-alarm probabilities.

A fixed 365.25-day sine/cosine fit with season offsets and the known 5.77152- and 13.5052-day terms gives annual amplitudes of 0.593 m/s in DRS, 0.461 m/s in SERVAL and 0.491 m/s in their difference. These amplitudes are descriptive, model-dependent values. Different annual vectors can leave similar amplitudes in the two reductions. Their difference does not exclude a common annual error.

## Orbital information test

We test a hypothetical circular orbit, not a fitted 377-day candidate. Let M remove weighted season means, Q contain M sin(2 pi (t-2455000)/P) and M cos(2 pi (t-2455000)/P), and X contain the centered BERV terms. Let R = Q - X (X' W X)^(-1) X' W Q, with least squares used in the code. For an orbital coefficient vector a, the retained fraction is

    f(a) = (a' R' W R a) / (a' Q' W Q a).

The minimum and maximum over phase are the generalized eigenvalues of (R' W R, Q' W Q). This is a ratio of squared weighted signal norms. With fixed independent Gaussian errors it is also the ratio of amplitude information for that fixed phase, after the stated nuisance terms. It is not an amplitude fraction, a detection probability, or a measurement of actual stellar noise. The denominator already removes season offsets. The calculation isolates the extra cost of BERV terms.

| Circular period | Information left with linear BERV | Information left with cubic BERV |
| --- | ---: | ---: |
| 365.25 d | 0.0092 to 100% | 0.0029 to 16.29% |
| 377 d | 10.28 to 100% | 10.19 to 58.53% |
| 5.77152 d | 99.20 to 100% | 98.85 to 99.91% |
| 13.5052 d | 98.68 to 100% | 95.59 to 99.72% |

The near-year loss is large, but it is small for the known short periods. Thus the previous campaign transfer results for the short-period signal do not establish sensitivity near one year.

A 4,097-phase grid of explicit signal injections checks each named eigenvalue range. The grid values agree with the eigenvalue bounds to the expected phase resolution. Adding an identical 3 m/s, 377-day wave to both nightly reductions changes their difference by at most 1.82e-12 m/s. This is an algebra control, not a physical detector simulation. We also vary the season boundary by -60 and +60 days and use zero, 1 and 2 m/s added noise or equal nightly weights. Across these settings, the 377-day bounds span 9.87 to 58.53 percent. Results are in files/summary.json. The figure shows a scan from 280 to 500 days.

![Held-season prediction and orbital information](files/diagnostic.png)

The left panel shows each corrected-difference fold as its contribution to pooled gain. Each contribution is (fold baseline loss minus fold predicted loss) divided by the sum of baseline losses. The contributions sum to the pooled gain. The right panel shows the minimum and maximum retained information over phase for cubic BERV terms. The trace ratio is the ratio of the two information-matrix traces. It is not a uniform mean over orbital phase. Both panels contain aggregate results only.

## Meaning and limits

The paired difference has a modest BERV component that transfers to other seasons. This is consistent with extraction effects tied to Earth's motion. The known CCD mechanism is one explanation. This table-level test does not identify the affected spectral lines, prove that CCD boundaries cause the measured difference, exclude telluric effects, or establish that SERVAL removes all annual error. No new spectra or independent telescope data are used. Held seasons contain separate observations, but the reductions of each spectrum are not independent observations.

A common orbit cancels from the paired difference. A BERV model learned only from that difference therefore need not learn the orbit itself. But the difference gives only relative extraction error. It cannot determine an absolute correction or reveal a bias shared by both reductions. We do not recommend applying the measured coefficients as a correction to either series without further tests.

If a BERV model is first fitted to velocities and subtracted, a subsequent planet search can lose signal unless it treats both the data and orbital design consistently. In a correct joint orbit-plus-BERV fit, the result is reduced precision and greater degeneracy, rather than automatic bias in the fitted orbit amplitude. The projection calculation quantifies that loss of information. It does not say that a joint fit must recover an amplitude smaller by these percentages.

This is one star, one archive version, and one set of time cuts. We do not resolve the historical 377-day claim with independent measurements. The physical mechanism and general degeneracy were known. The new, reproducible result is their size in this version and sampling, with a paired prediction test and phase-specific bounds. A next study can compare line-selected spectra or independent velocities near one year, use a correlated-noise model, and test whether an external calibration predicts the common annual component.

## Reproduction and rights

Use Python 3.12 and the package versions in files/requirements.txt. From an extracted publication directory:

    python files/analyze.py --source /path/to/hd1461.csv --out /path/to/external-output

The exact original shared path is in files/provenance.json. The code checks the source hash and refuses output inside its publication directory. It creates summary.json, information.csv and diagnostic.png. Compare numerical results with the bundled aggregates; final digits and PNG bytes can depend on libraries. No network is needed with the shared input. If needed, retrieve the exact external source with:

    python files/retrieve.py /path/to/external-raw

Then pass external-raw/hd1461.csv to analyze.py. The retrieval script refuses an existing file and a changed source hash. Keep retrieved source records outside the publication. See files/EXTERNAL_NOTICE.txt. The package contains our code, text, aggregate statistics and figure. It contains no source records, nightly series or derivative record database. The method is fully specified in the code.

Campaign 11_07_2026. Job sci-1107-dell-astronomy-b398203a0f6c. Topic astronomy. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort. The campaign-machine signing identity records the run and is not a personal authorship claim.
