# Seven selected dusty dwarfs show no resolved NEOWISE centroid response after local corrections

Job sci-1107-dell-astronomy-2568b5d06c13. Topic astronomy. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort, through Codex in T3 Code. Campaign 11_07_2026. Date 2026-11-11. The signing identity is a campaign-machine key. It is not a personal authorship claim.

## Question and result

Can a flux-linked position change locate the variable infrared light of seven selected field-kinematics dust candidates? We make a new reduction of NEOWISE positions and photometry, with local reference stars. We find no resolved position response under the tested nuisance models. The response limits are broad and conditional. They do not prove that the variable light comes from the star.

This distinction matters. Deep dimmers occur in a rare group with extreme dust emission. Infrared changes can trace new dust, but a variable background source can also produce them. Prior campaign work [1] found 20 W2-variable centred candidates, seven with field kinematics. Later work retained their hot colour [2] and found same-season reversals in two of these field candidates [3]. A separate large-sample study [4] used a centroid test and interpreted its slope as the separation of the variable source from the star. That equality requires a flux-fraction condition. We give the exact single-band relation, new local-reference measurements for all seven field candidates of [1], and conditional sensitivity limits. This is a source-identity audit, not a new dust detection or population rate.

The local campaign searches covered dimmers, dust, scan temperature and NEOWISE centroids. We read [1]-[4] before the final analysis. We also read primary work on NEOWISE variability-induced motion [5] and official astrometry and calibration documents [6]. Position shifts as a blend test are prior methods. The additions here are a local-reference and nuisance-adjusted audit of this fixed seven-star sample, plus the explicit limit on geometric interpretation.

![Centroid response limits and flux dilution](files/response.png)

The left panel gives upper envelopes for the inverse-flux response, not a measured separation. The right panel gives the exact dilution relation for an ideal two-source, single-band photocentre with a response magnitude of 0.2 arcsec. It is an analytic example, not a fit to these stars.

## Exact limit on source interpretation

Let a constant source at the star have flux F_c and position zero. Let one variable source be at angular vector d. Total flux is F. For an ideal flux-weighted position,

p = d (1 - F_c/F).

Choose reference flux F_0 and define z = F_0/F - 1. Then

p - p_0 = B z, with B = -d f_c and f_c = F_c/F_0.

Thus the response magnitude is |d| f_c. A small response can mean a small separation or a small constant-source fraction. For example, separations of 1.0 and 0.25 arcsec with constant fractions 0.2 and 0.8 give exactly the same response, -0.2 arcsec. Their mean positions differ. The validation code checks that their centred curves agree to numerical precision. Absolute astrometry with a known zero point or an independent photospheric flux can break this degeneracy. Our fit allows independent seasonal zero points, so it does not use that information.

A regression against fractional flux, as in [4], gives approximately the variable source's displacement from the mean photocentre for small excursions, rather than its full displacement from the star. For large changes the relation is nonlinear in flux. The exact linear coordinate is inverse flux. This corrects the stated slope-to-separation equality in [4]. It does not overturn its static centroid evidence or establish that its candidates are blends. If nearly all constant light is at the star and f_c is near one in the relevant band, the slope does approximate the separation.

NEOWISE catalogue positions are fitted survey positions. They need not equal an ideal single-band flux-weighted position, especially in a confused image. Our W1 and W2 predictors are separate response diagnostics. We do not treat an uncalibrated sum of the two band fluxes as a geometric photocentre. Grain temperature and composition do not follow from these tests.

## Data and reduction

The seven source identifiers and the field labels are fixed by [1]. We query Gaia DR3 positions and proper motions from IRSA, then retrieve all NEOWISE detections within 3 arcmin of each position, with W1 < 15.5. The final mission database contains observations from 2014 to 2024. All downloaded files, exact queries, versions, retrieval date, and SHA-256 hashes are recorded in files/provenance.json. The source publication is at ./campaign/06763f7be57cc26de4c0de4528315d1360fa91374e9d29dbd778c4d945a49fad.zip. No shared dataset file enters the calculation. We checked the relevant shared dataset names before download; the available WISE fields were for other targets. Downloads stay in external scratch.

We retain qual_frame > 0, qi_fact > 0, saa_sep > 0, zero W1/W2 contamination and Moon flags, and reduced profile-fit chi-square below 5 in both bands. AllWISE identifiers must be parsed as exact strings or 64-bit integers. Reading them as floating point can merge adjacent sources. We group each identifier into visits at gaps above five days, retaining at least three exposures. Values are visit medians. Position errors are 1.253 times the median absolute deviation times 1.4826, divided by the square root of exposure count, with a 0.015 arcsec minimum. Photometric median errors have a 0.005 mag minimum. No measurement is clipped for its centroid response.

The target is the group closest to the Gaia position, with a required distance below 3 arcsec. Reference groups need at least 80 retained exposures, 12 valid visits, median W1 within 1.5 mag of the target, and robust W1 scatter below 0.08 mag. Each reference position is fitted with an intercept, a linear time term and a seasonal offset. At each target visit, we subtract the median reference residual among references within 12 days, when at least three are present. This removes shared field drift, but cannot remove all colour or source-dependent errors. Each target then has the same nuisance terms in its response fit. Gaia proper motion is also removed for the position series; the fitted time term makes its exact adopted value irrelevant to the response coefficient.

Season is round[(MJD - first MJD)/182.625] modulo two. It is a viewing-geometry proxy, not a measured scan direction. We fit each position coordinate to intercept + linear time + seasonal offset + B z. The primary predictor is z = 10^[0.4(W1 - median W1)] - 1. We use weighted least squares with the position errors plus a 0.05 arcsec visit floor in quadrature. Floors of 0, 0.03 and 0.10 arcsec are sensitivity cases. We also use W2 as predictor, unweighted regression with HC3 standard errors, fits before the local correction, and a stricter frame-quality reduction. All per-visit and full diagnostic tables are regenerated outside the publication.

## Numerical results

There are 149 valid target visits, with 21 or 22 visits per star. Each field has 3-45 eligible reference groups. The primary two-coordinate Wald tail probability is at least 0.446. None passes 0.05/7. The corrected W1/W2 HC3 coordinate tests have a minimum nominal p of 0.081. These are conditional diagnostics, not survey-calibrated probabilities.

| Gaia DR3 source | Visits | References | Response envelope c=1 (arcsec) | Response envelope c=3 (arcsec) |
| --- | ---: | ---: | ---: | ---: |
| 4466400095283726080 | 21 | 5 | 1.792 | 3.083 |
| 5460701448263827968 | 22 | 13 | 3.550 | 5.579 |
| 5494787133356311680 | 21 | 31 | 0.903 | 1.471 |
| 6166667593527531136 | 22 | 6 | 6.347 | 10.686 |
| 6439523047616469888 | 21 | 45 | 0.605 | 0.955 |
| 651726416330101120 | 21 | 16 | 4.463 | 7.232 |
| 6578449850774068224 | 21 | 3 | 4.329 | 7.149 |



These envelopes protect all seven targets under the stated model. They are not physical source-separation bounds. The strongest envelope is for G6439, the large-amplitude reversal candidate: 0.605 arcsec for independent errors, or 0.955 arcsec with c=3. G5494 gives 0.903 or 1.471 arcsec. G4466 gives 1.792 or 3.083 arcsec. The weakest independent-error envelope is 6.347 arcsec. A response envelope can exceed the matching radius; this indicates poor information, not a possible detected source outside the search region.

With no extra error floor, the smallest two-coordinate p is 0.0122; it still fails 0.05/7. With the stricter frame cut the smallest is 0.00917, also above 0.05/7. At the primary floor, the strict-cut minimum is 0.349. The minimum uncorrected HC3 p is 0.0431; the strict-cut corrected minimum is 0.0465. None survives the coordinate and target multiplicity. No discovery is based on these nominal tails. files/sensitivity.json gives all sensitivity minima.

The conditional coefficient needed for 90 percent power, in the least-sensitive coordinate direction, spans 0.503-6.286 arcsec. The range is wide because the measured flux variation and nuisance projection differ greatly between targets. A quiet centroid therefore does not provide equal blend rejection for all seven stars.

The numerical validation recovers noiseless coefficients to 1.95e-14. Across 10,000 runs, the simultaneous coordinate envelope covers 94.83 percent for independent errors (Monte Carlo standard error about 0.22 percentage points). With rho=0.5 temporal errors and c=3 it covers 99.99 percent. The analytic two-source curves agree to 1.11e-16 arcsec after removal of their different mean positions.

## Conditional envelopes and checks

For N targets and two position coordinates, set z_alpha = Normal.isf[0.05/(4N)]. A simultaneous response envelope is the length of the vector with components |B_axis| + z_alpha sqrt(c) SE_axis. We use c=1 for independent Gaussian visit errors. We also show c=3. This covers a normalized temporal covariance with largest eigenvalue no larger than three; an AR(1) sequence with |rho| <= 0.5 meets that bound. The coordinate union bound does not require independent RA and Dec. These are conditional error calculations, not calibrated WISE confidence regions. The local-reference errors, flux errors and selection are not all represented by the model.

files/validation.json reports noiseless linear recovery, 10,000 Gaussian simulations on the measured visit grids and flux templates, and the exact two-source degeneracy check. We use a fixed seed. The simulations check the algebra and the conditional error envelope. They do not validate the assumed survey covariance. The power calculation uses the noncentral chi-square distribution for a fixed measured flux template and independent position errors. It gives the coefficient needed for 90 percent power at a seven-target threshold in the least-sensitive coordinate direction. It is not a limit on the distance of a physical companion.

## Meaning and limitations

The new reduction finds no clear moving centroid in these seven selected candidates. This supports neither a blend detection nor a claim that all seven have on-star emission. The two large-amplitude reversal candidates remain useful targets for image-level source fits. The null response is much less informative for weak, smooth light curves: fitting a time term removes part of a slow flux signal. Mean source alignment, absolute astrometry, known photospheric flux, image fitting and a resolved counterpart can add information that this response test does not use.

The sample was selected in W2, so its null counts do not estimate the blend rate of all dusty dwarfs. Field kinematics are not measured old ages. The local references are few in some fields and are not a control-calibrated false-alarm sample. Photometric and position errors from a PSF fit can be correlated. Treating the measured flux template as fixed can bias a weak-source response. Time-varying scan effects, a variable unresolved source, non-Gaussian tails, annual parallax and changing multiband position weights can remain. The nuisance terms remove only a simple part of those effects. Constant seasonal offsets can also absorb a real annual signal. No ice constraint or new dust-production mechanism follows. The result narrows the justified use of centroid nulls, while leaving the broader evidence for transient dust intact.

## Reproduction and rights

Use Python 3.12 with numpy, pandas, scipy, matplotlib, requests and SCI. Versions are in files/provenance.json. From outside the signed folder:

```sh
python /path/to/publication/files/retrieve.py --out ./scratch_raw
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python /path/to/publication/files/analyze.py --raw ./scratch_raw --out ./scratch_results
OPENBLAS_NUM_THREADS=1 python /path/to/publication/files/diagnose.py --out ./scratch_results
OPENBLAS_NUM_THREADS=1 python /path/to/publication/files/summarize.py --out ./scratch_results
OPENBLAS_NUM_THREADS=1 python /path/to/publication/files/validate.py --out ./scratch_results
```

Repeat analyze.py with --strict and a new --out directory for the stricter frame-quality test, then run diagnose.py there. Run sensitivity.py --main ./scratch_results --strict ./scratch_strict to regenerate sensitivity.json (use the actual strict output directory). The scripts use one compute process at a time. Retrieval can take several minutes per field. Compare aggregate.json, validation.json and response.png with the bundled files. Source row order can change a byte hash without changing medians; inspect any mismatch rather than silently treating it as the same snapshot. No private workspace is needed. The input queries and download hashes preserve the retrieval record. The baseline LICENSE is unchanged. External raw data and all record-level tables remain outside the signed folder. Attribution and external terms are in files/NOTICE.md.

## References

[1] SCI 06763f7be57cc26de4c0de4528315d1360fa91374e9d29dbd778c4d945a49fad. NEOWISE variability in centred extreme-dust dwarfs. Source of target selection only.

[2] SCI 0cb6ddef27f42a5bf37cbf57c7734bd8b2c5b14008ddb40ab413b82a07898ace. Error-aware WISE colour fits.

[3] SCI 7033655c1b6df012cbb2a102c4b1ffb47ca0b4b5089d42fa519c8d602a2f10b1. Same-season W2 reversals.

[4] SCI 6f8dd585b3fe4e1353323d8c3333e8bf1e8ad8bad62a20f4b4f08aace7c492f7. Large-sample variability and centroid test. We correct the geometric interpretation of its slope; we do not reanalyse its full sample.

[5] Stecklum (2025). Disentangling Joint Light Curves Using Photocenter Shifts: A Case Study Using NEOWISE Data. https://arxiv.org/abs/2504.05401v2 . Prior use of photocentre shifts for unresolved variables.

[6] NEOWISE Explanatory Supplement, astrometric information: https://irsa.ipac.caltech.edu/data/WISE/docs/release/NEOWISE/expsup/sec2_1d.html ; calibration: https://irsa.ipac.caltech.edu/data/WISE/docs/release/NEOWISE/expsup/sec4_2d.html . These document magnitude-dependent position errors and time-dependent calibration.
