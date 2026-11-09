# Gaia DR3 and ZTF timing of 11,668 Mira-like stars (2014-2025): a weak persistent period-change signal, no confirmed rapid period change, and a biased O-C extrapolation test

Job: sci-1107-dell-astronomy-e15334b417dc. Topic: astronomy. Machine: dell. Model: Claude Opus 5.5 (claude-opus-5-5), account claude-andrii, campaign 11_07_2026. The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Some Mira variables change their pulsation period quickly. T UMi is an example: its period decreased by about 1 percent per year after the probable onset of a helium-shell flash (thermal pulse) [Molnar et al. 2019]. Most Mira stars with known period changes are bright stars with a century of visual data [Templeton et al. 2005]. The large population of fainter Gaia long-period variables (LPVs) has no such record.

We asked two questions:

1. Do fainter Miras in the Gaia DR3 LPV catalogue show period changes from 2014 to 2025 that continue across independent surveys? Gaia DR3 covers 2014.6-2017.4, and ZTF DR24 covers 2018.2-2025.8.
2. Which individual stars show a rapid period change (|dP/dt|/P of 1 percent per year or more) that both surveys support? These stars are thermal-pulse candidates.

## 2. Data

- **Gaia DR3 LPV catalogue** (`gaiadr3.vari_long_period_variable`, joined to `gaia_source` and `vari_summary`), ESA Gaia TAP, queried 2026-11-09. Selection: a period is given, amplitude > 0.4 mag, Dec > -28 deg, and 12.5 <= G <= 18.5. This gives 38,344 stars (`files/data/gaia_lpv_amp04.csv`). The ZTF stage used amplitude >= 0.8 mag and 100 < P < 700 d, which gives 28,851 stars (`files/data/fetch_list.csv`).
- **ZTF DR24 light curves** (zg and zr) from the SNAD mirror, `https://db.ztf.snad.space/api/v3/data/dr24/circle/full/json?ra=..&dec=..&radius_arcsec=2.0`, fetched 2026-11-09. The SNAD mirror returns only good-quality points. The raw files total 339 MB, which is too large for this bundle. `files/provenance/sha256_raw_inputs.txt` gives the SHA-256 of every raw batch file, and `files/scripts/01_fetch_ztf.py` downloads them again. The bundle includes the raw ZTF light curves of the four flagged stars.
- **Gaia DR3 G-band epoch photometry** from the AIP Gaia TAP mirror (`https://gaia.aip.de/tap/sync`, table `gaiadr3.epoch_photometry`), fetched 2026-11-09 with `03_fetch_gaia_epochs.py`. The total is 32 MB. Hashes are in `files/provenance/`, and the bundle includes the epochs of the four flagged stars.
- **VSX** (B/vsx at vizier.cfa.harvard.edu) and Gaia DR3 neighbours were used only to vet the flagged stars.

No shared campaign dataset applied to this question. We put no new shared dataset into `datasets/`, because the data came from about 29,000 API calls and not from one URL.

## 3. Method

**ZTF O-C curves (`02_oc_fit.py`).** For each star we used the zr band and removed points brighter than 12.8 mag (saturation). The method then has four steps:

1. A multi-harmonic periodogram gives the ZTF period. The light-curve model is a 3-harmonic template with per-field offsets and a quadratic mean-magnitude trend.
2. We cut the data into segments of 0.6 P or at least 100 d inside each observing season. For each segment we fit a time shift with a free offset and a free amplitude. These shifts form the O-C curve.
3. We fit O-C(t) = a + b t + c t^2 by generalized least squares. The noise model is white timing noise plus a Brownian phase random walk (the Eddington-Plakidis model of random cycle-length changes). Maximum likelihood gives both noise levels. Then dP/dt = 2 P c, and z = c / se(c).
4. We also measured periods separately in the first half and the second half of the ZTF data (P_h1 and P_h2).

**Gaia timing (`04_gaia_timing.py`).** We fit each star's own ZTF template to its Gaia G epochs. This gives (i) the time shift of the Gaia light curve relative to the linear ZTF ephemeris, and (ii) a Gaia-era period from a fit with a free period.

**Two population tests.**

- **Test A (phase).** We compare the Gaia time shift with the shift that the ZTF quadratic O-C predicts at the Gaia epoch (quadratic prediction minus linear prediction).
- **Test B (period).** We compare the within-ZTF period change (P_h2 - P_h1) with the change from Gaia to ZTF ((P_h1+P_h2)/2 - P_Gaia). Test B has no term that is common to the Gaia and ZTF quantities. The only shared quantities are the two ZTF half-periods.

For both tests we use the Spearman rank correlation with 95% bootstrap intervals. A persistent period change gives a positive correlation.

**Null models.**

1. A Gaussian O-C simulation (`06_null_sim.py`) uses each star's real segment times, Gaia epochs, and fitted noise.
2. A light-curve-level simulation (`05b_injection_gaia.py`) uses 3,000 random sample stars. It keeps their real ZTF and Gaia time stamps, errors, and templates. It adds a 2% cycle-length jitter, a 15% cycle amplitude jitter, and a 0.1 mag cycle mean-level jitter. We ran it with no period change and with a constant dP/dt/P drawn from N(0, 1%/yr). The full pipeline then runs on these synthetic stars with the same cuts as the data.

**Quality sample.** We kept stars with ZTF/Gaia period ratio 0.9-1.1, P < 600 d, at least 6 O-C segments, at least 20 Gaia epochs, a Gaia span of at least 0.8 P, an unambiguous Gaia phase (delta chi2 > 9), and a Gaia shift error below 0.05 P. This leaves 11,668 stars. 4,643 of them have at least 9 O-C segments ("well-sampled"); the others have about one segment per season.

## 4. Results

### 4.1 The simple phase extrapolation test gives false signals

In a 360-star pilot from one sky region, Test A gave rho = 0.28. The Gaussian O-C null gave 0.00 +- 0.06. That looked like strong evidence that period changes persist. The full sample did not confirm it:

| Test A (rho, 95% CI) | data | light-curve simulation, no period change | simulation, constant dP/dt |
| --- | --- | --- | --- |
| <= 8 segments | -0.046 [-0.072, -0.021] | 0.023 [-0.034, 0.076] | 0.71 |
| >= 9 segments | 0.195 [0.164, 0.225] | 0.122 [0.068, 0.185] | 0.82 |
| all | 0.032 [0.012, 0.052] | 0.061 [0.019, 0.101] | 0.76 |

The light-curve simulation has no period change, but it still gives correlations of the same size and sign pattern as the data. The sign depends on period, declination and segment count. Thus Test A is dominated by a method artifact.

We think the cause is this. With partial-cycle coverage, the segment time shifts have errors that are correlated within one cycle and that depend on which part of the cycle each season covers. These errors enter both the prediction and the Gaia offset through the shared linear ephemeris. A Gaussian O-C null with independent errors does not show this effect. Persistence tests of this type need light-curve-level nulls.

### 4.2 Test B shows a weak persistent component

| Test B (rho, 95% CI) | data (own Gaia fit) | data (DR3 catalogue period) | simulation, no change | simulation, constant dP/dt |
| --- | --- | --- | --- | --- |
| <= 8 segments | -0.002 [-0.029, 0.026] | -0.025 [-0.047, 0.001] | -0.072 [-0.128, -0.015] | 0.68 |
| >= 9 segments | 0.080 [0.049, 0.109] | 0.095 [0.066, 0.130] | -0.047 [-0.106, 0.015] | 0.81 |
| all | 0.021 [0.003, 0.042] | 0.010 [-0.010, 0.030] | -0.063 [-0.104, -0.023] | 0.73 |

In well-sampled stars, the direction of the within-ZTF period change agrees weakly with the direction of the Gaia-to-ZTF change. The value is the same with the published DR3 catalogue periods, which come from an independent pipeline. The noise-only simulation gives a value of zero or below. The effect is about 10 times smaller than for a population with constant dP/dt of 1%/yr. Thus most of the measured period changes are noise, and only a small part persists over about 10 years.

### 4.3 The population spread of dP/dt is small

The robust spread of the within-ZTF fractional period change (P_h2 - P_h1)/P is:

| | data | simulation, no change | simulation, constant dP/dt (sd 1%/yr) |
| --- | --- | --- | --- |
| well-sampled | 0.0125 | 0.0144 | 0.0377 |
| all | 0.0161 | 0.0180 | 0.0385 |

The data spread is slightly smaller than the noise-only simulation, so our jitter settings are slightly too noisy. A conservative bound assumes that all observed spread is real period change. With this assumption, sd(dP/dt / P) <= 0.39 %/yr (well-sampled) and <= 0.50 %/yr (all), at 95% confidence.

### 4.4 No confirmed rapid period change

Candidate rule: |z| >= 5, |dP/dt|/P >= 1 %/yr, and a Gaia-era period on the predicted side of the ZTF period by at least 2 robust null standard deviations.

- Four stars pass (Table and Figure 3). No star in 2,594 noise-only simulated stars passes.
- In simulations with constant |dP/dt|/P >= 1 %/yr, the rule recovers 16.5% of stars. With 4 or fewer real cases in 11,668 stars, fewer than about 0.5% of the sample (95% Poisson limit, 9.15/0.165/11,668) can have a constant |dP/dt|/P >= 1 %/yr that this method can detect. This bound uses the simulation recovery rate and is approximate.

The four stars do not hold up as thermal-pulse candidates:

| Gaia DR3 | name (VSX) | P_Gaia fit (d) | P_ZTF first half -> second half (d) | VSX period (d) | ZTF r median | notes |
| --- | --- | --- | --- | --- | --- | --- |
| 4512680154664010112 | MGAB-V2377 | 392 | 412 -> 420 | 435 | 19.3 | 4 Gaia neighbours within 5", brightest 0.9 mag fainter |
| 2032245728434163072 | ZTF J194646.58+311319.3 | 463 | 502 -> 515 | 466 | 18.6 | 3 neighbours, brightest 1.4 mag fainter; the VSX period, which also comes from ZTF, is 466 d and does not agree with our 499-515 d |
| 4143466069845987328 | OGLE-BLG-LPV-257194 | 415 | 432 -> 464 | 442 | 19.2 | bulge field |
| 4110539377460567680 | OGLE-BLG-LPV-240271 | 286 | 297 -> 304 | 294.5 | 17.6 | 6 segments only |

All four stars have the following properties:

- very red colours (BP-RP 5.5-6.2) and faint ZTF r magnitudes, so their minima are near or below the ZTF detection limit;
- low Galactic latitude;
- at most 8 O-C segments, the sampling class in which Tests A and B show bias;
- an increasing period;
- a Gaia DR3 phase offset that does not follow the quadratic ZTF O-C extrapolation (Figure 3; offsets -31 to +29 d against predictions of +74 to +156 d);
- no ZTF g data adequate for an independent check.

The earlier VSX/OGLE periods do not continue a monotonic change: for example, 442 d (OGLE) -> 415 d (Gaia) -> 432-464 d (ZTF). We list these stars as a watch list for possible blending, minimum censoring, or real period meandering. We do not claim them as thermal-pulse candidates.

## 5. Limitations

- The light-curve simulation uses fixed jitter values. Its O-C noise is slightly larger than in the data (|z| >= 4 in 4.9% of null stars against 2.0% of real stars). The null bias of Tests A and B depends on these values, so the size of the Test B excess (about 0.08-0.13 in rho) is uncertain. Its sign in well-sampled stars does not depend on this choice, because rho > 0 in the data and rho <= 0 in the null.
- The simulation does not model blending, censoring of faint minima, or ZTF calibration changes. These effects can create false period changes in faint red stars.
- Only stars with Dec > -28 deg and G = 12.5-18.5 were analysed, and ZTF r saturates near 12.8 mag. Bright, well-known Miras (T UMi, R Hya, R Aql) are outside the sample. No known rapid-change Mira was available as a positive control, so we used injections instead.
- The ZTF baseline is 7.5 years, which is about 6-25 cycles. Changes that are slower than about 0.2%/yr, or that reverse within a decade, are not resolved.
- An exploratory analytic model (`scripts/exploratory/10_ou_fit.py`, pilot only) showed that the slope of Test A cannot separate period meandering on decade time scales from cycle-to-cycle correlated noise. The fitted noise model absorbs part of any signal. We do not use it for conclusions.

## 6. Figures

- `files/figures/fig1_tests.png`: Tests A and B for data and simulations, by sampling class.
- `files/figures/fig2_period_change_spread.png`: distribution of the within-ZTF fractional period change for data and simulations.
- `files/figures/fig3_flagged_stars.png`: ZTF O-C, quadratic fit extrapolated back, and the Gaia DR3 offset for the four flagged stars.

## 7. Reproduction

Use Python 3.12 with numpy 2.5.4, pandas 3.1.1, scipy 1.18.1, astropy 8.0.2, matplotlib 3.11.2 and pyarrow 26.0.1. Run all scripts from one working directory that contains `data/` and `results/`.

1. Put `files/data/gaia_lpv_amp04.csv` in `data/`. To make it again, use the ADQL in section 8.
2. `python scripts/01_fetch_ztf.py 16` writes `data/fetch_list.csv` and `data/ztf/batch_NNNN.parquet` (about 1.5 h). Compare the files with `provenance/sha256_raw_inputs.txt`. The SNAD service can change, so the hashes may differ.
3. `python scripts/03_fetch_gaia_epochs.py` writes `data/gaia_epochs/chunk_NNNN.parquet` (about 17 min).
4. `python scripts/02_oc_fit.py zr 20` writes `results/oc_zr.parquet` (about 50 min at host load 70-100).
5. `python scripts/04_gaia_timing.py 20` writes `results/gaia_timing.parquet`.
6. `python scripts/07_population.py 500` writes `results/merged.parquet` and `population_stats.json`, with the Gaussian O-C null and the Test A strata.
7. The light-curve simulations: `python scripts/05b_injection_gaia.py results/oc_zr.parquet 10 3000 0 0.02 0.15 0.1 results/lcnull_B.parquet` and the same command with `0.01` in place of the first `0` and `results/lcinj_B.parquet` as the output. `lcnull_A` is the same as `lcnull_B` with 2,500 stars and without the period outputs.
8. `python scripts/13_final.py` writes `final_stats.json` and `candidates_final.csv`. `python scripts/11_candidate_checks.py results/candidates_final.csv` does the vetting. `python scripts/14_figures_bounds.py` makes the spread bounds and the figures.
9. `05_injection.py` is the O-C-only injection-recovery test on 150 pilot stars (`results/injection_lc_batch0.parquet`). It recovers -1, +0.5 and +2 %/yr changes without bias. The scatter is 0.46 %/yr with 2% cycle jitter.

The included results tables let you check every number in this README without the raw downloads. `merged.parquet` has one row for each quality-sample star with all O-C and Gaia quantities, including the O-C points as strings.

## 8. Gaia sample query

```
SELECT l.source_id, l.frequency, l.frequency_error, l.amplitude, l.median_delta_wl_rp, l.is_cstar,
  g.ra, g.dec, g.l AS glon, g.b AS glat, g.phot_g_mean_mag, g.bp_rp, g.parallax, g.parallax_error, g.ruwe,
  s.num_selected_g_fov, s.range_mag_g_fov, s.std_dev_mag_g_fov, s.mean_obs_time_g_fov, s.time_duration_g_fov
FROM gaiadr3.vari_long_period_variable l JOIN gaiadr3.gaia_source g ON g.source_id=l.source_id
JOIN gaiadr3.vari_summary s ON s.source_id=l.source_id
WHERE l.frequency IS NOT NULL AND l.amplitude>0.4 AND g.dec>-28 AND g.phot_g_mean_mag BETWEEN 12.5 AND 18.5
```

## References

- Templeton, Mattei & Willson 2005, AJ 130, 776, "Secular evolution in Mira variable pulsations" (arXiv:astro-ph/0504527).
- Molnar, Joyce & Kiss 2019, ApJ 879, 62, "Stellar evolution in real time: models consistent with direct observation of a thermal pulse in T Ursae Minoris" (arXiv:1905.00597).
- Lebzelter et al. 2023, A&A 674, A15, Gaia DR3 LPV catalogue (arXiv:2206.05745).
- Gaia Collaboration, Vallenari et al. 2023, A&A 674, A1.
- Bellm et al. 2019, PASP 131, 018002 (ZTF); Masci et al. 2019, PASP 131, 018003 (ZTF data system).
- Eddington & Plakidis 1929, MNRAS 90, 65.
