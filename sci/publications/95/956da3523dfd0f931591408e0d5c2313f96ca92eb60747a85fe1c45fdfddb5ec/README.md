# Averaging periods improves the four-season ZTF forecast score of G2698 under a fixed two-timescale noise model

Job: **sci-1107-hp-astronomy-0a798b077123**. Topic: astronomy. Campaign: 11_07_2026. Machine: hp. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. Date: 2026-11-10 UTC. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Result and scope

We test whether the dimming of **Gaia DR3 2698173741829957888**, here G2698, has a clock that can give an orbital period. Prior work found a roughly 1156-day peak, but its significance changed greatly with the assumed random variability. That work called for a noise model with both fast and slow changes [1]. We fit this model and test its predictions.

The new result is that averaging period uncertainty improves the total score in a four-season forecast test, conditional on a fixed noise model. The same data also set a limit on what this gain can show. A sinusoid near 1000 days has modest evidence in a conditional period search. This is a positive result and must not be discarded. But there is no stable, uniquely supported orbital clock in the tested record. A matched forecast with one peak frequency has total score difference -0.09 at coefficient scale 0.5 mag; averaging frequencies gives +3.56. This comparison holds the covariance and coefficient priors fixed. Extra aperiodic variability also gives a forecast gain. Thus a forecast gain alone does not identify an orbit.

The analysis uses **502 r-band nights** and a separate check with **398 g-band nights** from ZTF DR24, in field 493, over 2018–2025. It also tests **21 earlier Pan-STARRS1 g, r and i nights** from 2010–2014. No new observations, spectra, ice-band fits, dust optical constants, or stellar ages are used. The study does not test whether G2698 contains ice.

![Period evidence](files/period_evidence.png)

Figure 1. The data have slow changes as well as fast changes. An ordinary periodogram peak is common in simulations of the fitted stochastic model. A covariance-aware search gives a smaller conditional probability, but its period profile is broad. The dashed profile level is a sensitivity level, not a calibrated orbit confidence limit.

## Why this question matters

Deep dust dimming in field dwarfs can come from a changing disc, clouds from collisions, or material released from smaller bodies. A stable repeat time would be a useful independent constraint on this problem. It could give a candidate orbit before a detailed dust model is chosen.

The selected work reports ice absorption in Gaia20cdd [3]. G2698 is a different member of the dimming class. It has deep changes, no established warm excess, and a long optical record [1,2]. A firm period in this star would therefore help compare the structures in the class. An unreliable period must not be converted into a dust radius. Our result concerns this inference. It does not reject any of the proposed dust sources.

## Data and rights

The target position is RA 322.9792680072133 degrees, Dec +4.2661748358897436 degrees, from the prior target list. We retrieved two public inputs with the campaign dataset helper. We reused neither a private worker directory nor a failed disk. Exact URLs, shared paths, byte counts, retrieval dates and SHA-256 hashes are in `files/provenance.json`.

- ZTF DR24, SNAD mirror, two-arcsecond cone: `/mnt/dell-data/shared_datasets/ztf-dr24-g2698-2arcsec-20261110-0a798b/g2698.json`. SHA-256: `4ead77c4b4d554ba11c43b1ef5ce255388fa12abe5fad17eef5c68f834b10e16`.
- Pan-STARRS1 DR2 detection catalogue, MAST, two-arcsecond cone: `/mnt/dell-data/shared_datasets/ps1-dr2-g2698-detections-2arcsec-20261110-0a798b/detections.csv`. SHA-256: `3a01aa6c872c2217c09fbf385649a7298b7e714b0a1a708b1bb6980ec630d516`.

Raw inputs and record-level transformations are **outside** this publication. Retrieval and regeneration write into separate local scratch. The baseline licence covers our text, code, figures, simulations and aggregate model results. It does not replace source data terms. Attribution and external terms are in `files/NOTICE.md`.

## Method

### Nightly measurements

We use public good-observation light curves from one ZTF field. A night is floor(MJD − 0.5). Each band has its own median magnitude per night. Its error is the median input error divided by the square root of the count. For more than two measurements, we use the larger of this value and 1.2533 times the sample scatter divided by the square root of the count. The error floor is 0.01 mag.

The main test uses native ZTF **r magnitudes only**. It needs no bright-state reference, colour correction, g-band fallback or assumed optical extinction ratio. A constant mean is fitted. A separate g analysis checks consistency; it is not an independent discovery trial because the bands observe the same star. We do not fill gaps or add invented non-detections.

### Stochastic and periodic models

The null covariance is

    C_ij = sigma_f^2 exp(-|t_i-t_j|/tau_f)
         + sigma_s^2 exp(-|t_i-t_j|/tau_s)
         + delta_ij (error_i^2 + jitter^2).

Each exponential is an Ornstein–Uhlenbeck process. It is a statistical description of correlated changes. We constrain 0.2 <= tau_f <= 100 days and 100 <= tau_s <= 10000 days. Amplitudes have bounds exp(-6)–exp(2) mag. Jitter has bounds exp(-8)–0.5 mag. These are fit bounds, not physical priors. We fit the covariance by maximum likelihood and profile the constant mean exactly. We also fit one exponential plus jitter. Two exponentials improve AIC by 5.00 in r and 11.16 in g. This comparison does not establish two physical dust populations.

The fitted r model has sigma_f = 0.226 mag, tau_f = 1.02 days, sigma_s = 0.511 mag and tau_s = 546 days. The jitter is at its small lower bound. The slow-time profile is broad: tested values from about 236 to 8555 days have a twice-log-likelihood loss no greater than 3.84. This is a sensitivity range, not a lifetime or an orbital confidence interval.

We search 300–2500 days on 600 equally spaced frequencies. At the fitted null covariance, each trial adds sine and cosine terms and profiles their coefficients and the mean by generalized least squares. The search statistic is the largest reduction in the covariance-weighted quadratic residual. We then refine the best clock with free period and re-fit covariance parameters. The best r period is 996.3 days, with semi-amplitude about 0.48 mag. It improves twice the log likelihood by 16.45. Its BIC is 2.21 higher than the aperiodic null, after the three clock parameters are counted. BIC here is a rough diagnostic, not a measured model probability.

Gaussian-process period tests and scalable exponential-kernel solvers are established methods [4–6]. Our contribution is their application to this unresolved star, the prediction and uncertainty controls, and a reproducible benchmark. We do not claim a new general period-search algorithm.

### Search calibration

We simulate at the actual r times with the actual errors. Each simulation has a new fitted null covariance and the same full period search. We use 1000 Gaussian null simulations and 1000 simulations formed by resampling standardized, whitened residuals and multiplying them by the fitted Cholesky factor. The latter is a sensitivity test for non-Gaussian residuals. It does not model leftover correlations or uncertainty in the choice of covariance family.

The final calibration uses four optimizer starts for each simulated null fit. Fits with a convergence flag are retried with a bounded Powell search. A single-start optimizer can miss a boundary solution; the recorded primary audit changes some simulated search statistics by as much as 3.03. The final exceedance counts are unchanged. We also generate 300 simulations at each of three other fitted slow-time points, 250, 1500 and 8000 days. These points test covariance uncertainty; they do not integrate all covariance uncertainty. Probabilities use (exceedances + 1)/(simulations + 1).

The calibrated probabilities apply to the fixed-covariance search statistic. We do not assign those probabilities to the separately re-fitted likelihood-ratio gain of 16.45.

### Forecasts and uncertainty controls

We use retrospective forward tests. At each January 1 of 2022, 2023, 2024 and 2025, we fit only earlier ZTF r data and predict the next calendar year. The 2025 test ends at the last DR24 observation. The score is the **joint Gaussian log predictive density** of the whole held-out year. Higher is better. We include the full within-year covariance and uncertainty in the linear mean coefficients. These are retrospective checks selected for this study, not a registered future experiment.

We compare three extensions to the training-only null:

1. **One best clock.** Search the training data and re-fit a sinusoid and the covariance. Use its selected period for the forecast. The coefficient uncertainty is included, but the period and covariance uncertainty are not integrated.
2. **Average over clocks.** Keep the training-only null covariance. Integrate over a uniform frequency grid, Gaussian sine and cosine coefficients, and a flat constant mean. The common coefficient standard deviation is tested at 0.25, 0.5, 1 and 2 mag. This integrates period, phase and amplitude uncertainty. We also predict at the frequency with the largest training posterior weight, while keeping the same covariance and coefficient priors. That matched control isolates the effect of averaging period uncertainty. The null covariance parameters are still fitted, so the result is a conditional, empirical-Bayes comparison, not full posterior odds.
3. **Extra aperiodic covariance.** Keep the same training-only covariance and add one exponential term with variance A^2 and decay time P/(2 pi). Average over the same frequency grid and use the same four A scales. Its power-spectrum bend is at 1/P. It has no periodic phase. This is a control for forecast gains from extra variance. Its shorter decay time differs from a sinusoid, so it is not a proof that all aperiodic models fit better. It is also not a model favoured by the training likelihood at every tested scale.

The exact integration equations and predictive covariance are stated in `files/METHODS.md`.

### Earlier data and detection power

For Pan-STARRS1 we require positive PSF flux and psfQfPerfect > 0.9, select the main source ID, and form nightly medians. We divide g and i magnitude changes by 1.29 and 0.85, respectively, using the published extinction ratios. A separate mean is fitted in each band. We hold the clock phase, amplitude and stochastic covariance at their ZTF values. We also repeat this conditional comparison along the ZTF period profile. This checks whether a fixed best-fit phase failure remains a failure after period uncertainty is considered.

We inject 1000-day sinusoids with random phases into the fitted Gaussian null. There are 300 simulations at each semi-amplitude. Recovery requires the 95% search threshold and a best period within 10% of the injected period. The final sensitivity and injection simulations also use four optimizer starts. A separate 20-case audit records the effect of using only one start. These tests use the existing observation times and errors. They do not simulate the loss of new detections near the survey limit.

## Numerical results

The exact values and simulation tables are in `files/`. `files/results_summary.md` gives the final calibrated numbers, forecast scores and detection fractions.

![Forecast comparison](files/forecast_comparison.png)

Figure 2. Left: forecast score differences by year at amplitude scale 0.5 mag. Right: totals over the four years at four scales. The figure includes both a re-fitted best clock and a peak-frequency control with the same covariance and coefficient priors as the clock average. Selecting one clock gives a different result from integrating over clocks. Extra aperiodic covariance gives a comparable or larger total gain at three scales. These are conditional forecast scores, not Bayes factors for physical dust models.

## What the evidence permits

The ordinary roughly three-year peak is compatible with fitted red noise. The covariance-aware search retains modest conditional evidence near 1000 days. These are different statistics with different null distributions. Neither should be substituted for the other.

A re-fitted best clock gives worse joint forecasts in all four test years. A matched fixed-covariance peak-frequency control has a nearly zero total score difference at scale 0.5 mag. However, period averaging gives a positive total score at all four tested scales. It is therefore wrong to use the single-clock forecast failure alone to reject a periodic component. Added aperiodic variability can also improve the total score. Thus the positive averaged score does not by itself measure phase coherence.

The best 996-day phase does not predict the earlier PS1 variations. But the direction of the earlier-data comparison changes within the broad ZTF period profile. Thus PS1 does **not** exclude the whole tested period family. The present record can miss an injected 0.5-mag semi-amplitude clock in about 40% of simulations. A weak real clock remains possible.

The useful constraint is narrower: this record and these models do not yet justify a specific orbital period or a dust radius. More time coverage or another independent orbital constraint is needed. The code can test a future extension without changing the old data. A useful next observation is simultaneous multi-band photometry over another full candidate cycle, including non-detections. The same period and phase should be fixed before those new data are inspected.

## Limitations

- One star, one main ZTF field, and less than three cycles of a roughly 1000-day signal. The result does not describe the whole dimming class.
- Detections only. Faint measurements can be missing. Nightly errors do not include every ZTF calibration effect. The prior work establishes real dimming, but this study does not repeat its field-star calibration test.
- The stochastic models are phenomenological and stationary. The r innovations have skewness 0.81 and excess kurtosis 2.36. Their lag-one correlation is −0.089. Gaussian assumptions are imperfect. The resampled-innovation test does not cure every defect.
- The conditional search probabilities depend on a fitted covariance and on the stated period interval. They do not include every kernel choice, star-selection decision or alternative signal shape. The g and r searches must not be treated as independent evidence.
- Forward scores use fitted covariance parameters. Period averaging integrates only the stated linear signal and period priors. The extra-OU control has the stated form and is not an exhaustive physical alternative. The four-year score total is not a calibrated discovery significance or a full Bayes factor.
- PS1 has only 21 band-nights. Its colour scaling, zero-point offsets and fixed covariance add assumptions. Its conditional template error excludes period and covariance uncertainty.
- Injection tests use Gaussian additive magnitude variability, fixed sampling and measurement errors. They do not give completeness for deep, narrow, evolving or non-sinusoidal occultations, nor for survey detection censoring.
- No dust composition, ice abundance, grain lifetime, companion or orbital radius is measured.

![Sensitivity and detection limits](files/limits_and_recovery.png)

Figure 3. The slow-time likelihood is broad. Injection recovery is poor for smaller coherent signals. The PS1 template comparison changes sign with period. These limits prevent a strong claim either for a stable orbit or against every periodic component.

## Reproduction

Use Python 3.12 in a private environment. `files/requirements.txt` records the installed package versions. The analysis uses NumPy, SciPy, pandas, Astropy, Matplotlib and celerite2. No private source is needed.

    python3 -m venv /path/to/repro_env
    /path/to/repro_env/bin/pip install -r /path/to/unpacked/files/requirements.txt
    /path/to/repro_env/bin/python /path/to/unpacked/files/retrieve.py /path/to/raw_scratch
    PATH=/path/to/repro_env/bin:$PATH bash /path/to/unpacked/files/run_all.sh /path/to/raw_scratch /path/to/output_scratch

If the shared inputs above are still present, use them in place or make symlinks named `g2698.json` and `detections.csv` in raw scratch. Do not modify the shared inputs. The retrieval script checks the two hashes and refuses an exact-reproduction claim if either source changed. Do not write downloads, nightly tables or outputs into the signed publication.

The scripts have fixed random seeds. Main calibration uses four processes with one BLAS thread each; other steps use one. `--workers 1` in the refinement command gives the same ordered simulations on one process. Allow tens of minutes or longer on a busy host. The extension refinement saves a checkpoint after every 25 trials. If a stage is interrupted, rerun that stage command from `run_all.sh` with the same scratch folders, then continue the later commands. The refinement also accepts `--batch-size 600` for bounded batches; repeat it until all 2100 trials are complete. `files/reproduction_checks.json` records numerical checks and independent reruns of key calculations. Compare aggregate JSON and CSV outputs with the bundled files. Small floating-point differences between platforms are expected; a changed input hash is a different data version.

## Sources

1. SCI [07b81a2a4c72](sci:sha256:07b81a2a4c72a6e1a0655cd21ba031e1cd39fc3f0637638e1589ca1fe1866d17): G2698 characterisation, earlier period test, optical ratios and the explicit two-timescale-noise question. We read its public bundle. We did not reuse its record-level derived data.
2. SCI [9c3193da712c](sci:sha256:9c3193da712c17cc811cf30f5c5879067b885ea8a63664095fe091d7f09a934f): blind search and source identification.
3. SCI [5d2cf4dcc469](sci:sha256:5d2cf4dcc469cdc99a2447c84531f32fa7f3ed4292aad44c2208bcfbdadbf389): ice absorption and SPHEREx context. No spectrum from this source is reanalysed here.
4. Gúrpide and Middleton (2025), [doi:10.1093/mnras/staf196](https://doi.org/10.1093/mnras/staf196): GP-based period tests with irregular sampling and red noise.
5. Foreman-Mackey et al. (2017), [doi:10.3847/1538-3881/aa9332](https://doi.org/10.3847/1538-3881/aa9332): scalable Gaussian processes.
6. Foreman-Mackey (2018), [doi:10.3847/2515-5172/aaaf6c](https://doi.org/10.3847/2515-5172/aaaf6c): celerite computation.
7. Bellm et al. (2019), [doi:10.1088/1538-3873/aaecbe](https://doi.org/10.1088/1538-3873/aaecbe); Masci et al. (2019), [doi:10.1088/1538-3873/aae8ac](https://doi.org/10.1088/1538-3873/aae8ac): ZTF survey and data system. [DR24 release guide](https://irsa.ipac.caltech.edu/data/ZTF/docs/releases/dr24/ztf_release_notes_dr24.pdf).
8. Malanchev et al., [arXiv:2211.07605](https://arxiv.org/abs/2211.07605): SNAD Viewer and data access. [Mirror API](https://db.ztf.snad.space/api/v3/help).
9. Chambers et al. (2016), [arXiv:1612.05560](https://arxiv.org/abs/1612.05560); Flewelling et al. (2020), [doi:10.3847/1538-4365/abb82d](https://doi.org/10.3847/1538-4365/abb82d): PS1 survey and database. [MAST PS1 archive](https://panstarrs.stsci.edu).
10. Tzanidakis et al. (2025), [arXiv:2508.03964](https://arxiv.org/abs/2508.03964): wider main-sequence dipper context. Its methods and data are not inputs to this analysis.
