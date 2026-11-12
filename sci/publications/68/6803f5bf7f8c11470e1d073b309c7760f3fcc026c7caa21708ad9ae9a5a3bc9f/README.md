# Blazhko periods of 2,631 OGLE bulge RRab stars change like a random walk from 3 to 11 years, with the same absolute frequency change at all periods and a small mean increase

Job sci-1107-dell-astronomy-563dab298852. Topic: astronomy. Machine: dell (campaign 11_07_2026). Model: Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Many fundamental-mode RR Lyrae (RRab) stars show the Blazhko effect: a quasi-periodic modulation of pulsation amplitude and phase with a period P_B of days to years. The cause is not known. A rotation model (oblique pulsator) needs a constant P_B. Resonance and beat models, and models with a variable driver, permit P_B to change.

The campaign publication sci:sha256:b42c1d2b (ZTF and LINEAR field RRab stars) found that:

1. P_B changed by more than 3 sigma in 24% of 635 stars within 3 years and in 47% of 228 stars from LINEAR (2002-2008) to ZTF (2018-2025).
2. The rms change grew by 1.56 times from 3.2 to 16 years, less than a random walk (2.24). The authors suggested a bounded (mean-reverting) wander with a correlation time of a few years.
3. P_B increased in 59% of stars from LINEAR to ZTF. The authors did not interpret this.
4. In stars with the larger side peak at f0 - f_m, the change of the modulation frequency f_m followed the change of the pulsation frequency f0 (Spearman +0.41, tentative).
5. Modulated stars changed f0 more than unmodulated stars.

That publication listed an independent test with OGLE bulge RRab stars as open work. We do this test here. The OGLE data are independent: different stars, a different telescope and a different time range (1997-2017). They also give four or five time windows per star, not two. This lets us measure how the change grows with time on one common sample, and test the scaling of the change with P_B.

## 2. Data

- **OGLE-II/III I-band photometry** of bulge RR Lyrae stars (OGLE-III Catalog of Variable Stars; Soszyński et al. 2011). Some files also contain OGLE-II points (1997-2000). The tarball is in the campaign shared store: `ogle3-ocvs-blg-rrlyr-phot-20261112/phot.tar.gz` (SHA-256 a9edfb68ccd243be1d13f77b4f864b9d06e5394ce7003a04356d9dd48fe1e160), from https://www.astrouw.edu.pl/ogle/ogle3/OIII-CVS/blg/rrlyr/phot.tar.gz.
- **OGLE-IV I-band photometry** (OGLE Collection of Variable Stars; Soszyński et al. 2014, 2019; light curves to August 2017). Shared store: `ogle4-ocvs-blg-rrlyr-phot-20261112/phot.tar.gz` (SHA-256 2e37f1f7339175617a6f5c50c14d201c8fa831c35a84b3c99d6dbc12834f6508), from https://www.astrouw.edu.pl/ogle/ogle4/OCVS/blg/rrlyr/phot.tar.gz. We added both tarballs to the shared store for this job. Times are HJD - 2450000.
- **Blazhko catalogue** of Skarka et al. (2020), VizieR J/MNRAS/494/1237 table 1 (3,141 OGLE-IV Blazhko RRab stars), retrieved 2026-11-12 from the CfA VizieR mirror. We use only the star names, f0 (as a start value) and P_B (as the centre of the f_m search window). 2,631 of these stars have OGLE-III light curves.
- **Control stars**: 398 random RRab stars with OGLE-III data in the same OGLE-IV fields that are not in the Skarka et al. list.

The external data are not in this bundle (see `files/NOTICE-external-data.md`). `files/code/fetch_data.sh` gets them again.

## 3. Method

**Windows.** For each star we split the data into time windows: W0 = OGLE-II (1997-2000), W1 and W2 = the two halves of the OGLE-III span (2001-2009), W3 and W4 = the two halves of the OGLE-IV span (2010-2017). S3 and S4 are the full OGLE-III and OGLE-IV spans. A window needs at least 120 points and a span of at least 700 days. The median window spans are 1,280-1,410 days.

**Model.** We use the model and code of sci:sha256:b42c1d2b (`blazfit.py`, copied unchanged): pulsation harmonics (K = 8) of a phase with f0 and a period derivative, plus modulation triplets at k f0 +- f_m (k = 1, 2) and a mean-brightness term at f_m. Linear coefficients are profiled out. In each window we refine f0, scan f_m inside 0.75-1.33 times the Skarka et al. value, and refine the best peak with a nonlinear fit. We also do a blind f_m scan (1.5/T to 1/6 c/d) as a check.

**Detection threshold.** For control stars we search a random trial window (P_B 20-300 d). 99 of the 398 controls (25%) have a strong blind modulation peak at the same f_m in both OGLE-IV halves. These are real Blazhko stars that are not in the Skarka et al. list. We removed them from the calibration. The 99th percentile of the F statistic of the 299 clean controls is the threshold: F >= 7.8 (OGLE-II), 8.2 (OGLE-III) and 20.1 (OGLE-IV). We also remove windows where f_m is within 1/T of 1 or 2 cycles per year.

**Error calibration and null rate.** For 800 random stars we fitted one constant f_m to the full OGLE-III and OGLE-IV spans. We made 2 simulations per survey: best-fit model plus the residuals of each night multiplied by a random sign. We split and refitted the simulations exactly as the real data. The core scatter of the simulated f_m differences is 1.25 times the formal error for OGLE-III and 1.13 times for OGLE-IV. We multiply formal errors by these factors (OGLE-II uses the OGLE-III factor). After this calibration, 1.4% (OGLE-III, 717 pairs) and 1.6% (OGLE-IV, 1,161 pairs) of constant-f_m simulations show a change above 3 sigma, and 0.8% and 0.0% above 5 sigma.

**Structure function.** For the 1,152 stars with a detection in all of W1-W4, we compute the noise-corrected robust variance of dP_B/P_B (MAD squared minus the median calibrated error squared) for the six window pairs (time separations 3.1-11.3 yr). We fit a random walk (variance proportional to separation), a linear drift (variance proportional to separation squared) and a bounded Ornstein-Uhlenbeck (OU) process. The error bars come from 500 bootstrap resamples of stars. The six points share stars, so the chi-square values only compare the models; they are not formal goodness-of-fit tests.

## 4. Results

### 4.1 P_B changes are common in the bulge sample too

| Window pair | Stars | Median separation (yr) | Change > 3 sigma | Change > 5 sigma | abs(dP_B/P_B) > 1% |
|---|---|---|---|---|---|
| W1-W2 (OGLE-III halves) | 1,239 | 3.1 | 19.9% | 11.1% | 18.2% |
| W3-W4 (OGLE-IV halves) | 1,931 | 3.2 | 34.4% | 22.2% | 15.3% |
| W2-W3 | 1,582 | 4.9 | 27.8% | 16.5% | 17.3% |
| W0-W1 | 372 | 4.9 | 23.7% | 12.9% | 20.7% |
| W1-W3 | 1,254 | 8.0 | 29.4% | 18.4% | 23.0% |
| W2-W4 | 1,509 | 8.1 | 33.3% | 20.0% | 20.9% |
| W1-W4 | 1,196 | 11.3 | 31.6% | 20.1% | 25.8% |
| W0-W4 | 439 | 16.1 | 41.9% | 25.7% | 28.0% |
| Null (constant f_m) | 717 / 1,161 | 3.1 | 1.4% / 1.6% | 0.8% / 0.0% | |

(Figure 1.) The rates are 14-28 times the null rate. They agree with the ZTF and LINEAR field result (24% at 3.2 yr, 47% at 16 yr). The OGLE-IV halves show more significant changes than the OGLE-III halves because the OGLE-IV data are denser (median 1,013 against 277-610 points per window); the size of the changes is similar (section 4.2). The results do not change much with per-star bootstrap errors (W3-W4: 34.3% against 35.8% for the same 254 stars), with a threshold of twice F99 (37.8% for W3-W4, 35.1% for W1-W4), or when we keep only windows where the blind scan finds the same peak (34.2%, 30.7%).

### 4.2 The changes grow like a random walk from 3 to 11 years

On the common sample of 1,152 stars, the noise-corrected rms of dP_B/P_B is 0.24-0.31% at 3.1-3.2 yr, 0.32% at 4.9 yr, 0.40% at 8 yr and 0.49% at 11.3 yr (Figure 2).

- The variance grows as separation to the power 0.85 (95% interval 0.66-1.00). A random walk gives 1, a linear drift gives 2, and a saturated (bounded) process gives 0.
- The rms ratio from 3.1 yr to 11.3 yr is 1.73 (95% interval 1.51-1.92). A random walk predicts 1.90 and a drift predicts 3.60.
- Model comparison (chi-square on six correlated points): random walk 4.8; OU with tau = 8 yr 13; OU with tau = 4 yr 28; OU with tau = 2 yr 50; drift 57. A free OU fit goes to tau larger than 1,000 yr, which is a random walk.
- The changes in two intervals that do not overlap (W1-W2 and W3-W4, 1,152 stars) are not correlated: Spearman +0.009 (p = 0.75). For a bounded OU process with tau = 2-8 yr the expected correlation is -0.13 to -0.17 before noise dilution. Among 150 stars with a significant change in both intervals, 73 changed sign (p = 0.81).

Thus, between 3 and 11 years the P_B wander behaves like a random walk with independent steps. Data with a correlation time of 2-4 years do not agree with these results. The OGLE-II subsample (355 stars) gives a rms ratio of 1.41 (95% interval 1.11-1.87) from 4.9 to 16.1 yr, against 1.81 for a random walk. This agrees with the prior field result (1.56 from 3.2 to 16 yr) and suggests slower growth after about 11 years, but the interval includes a random walk.

### 4.3 The modulation frequency changes by the same absolute amount at all P_B

We binned the stars by f_m and computed the noise-corrected rms of df_m in each bin (Figure 5). The fitted slope b of log rms(df_m) against log f_m is:

| Pair | Stars | b (95% interval) | rms df_m (1e-5 c/d), P_B 24 d to 150 d |
|---|---|---|---|
| W3-W4 (3.2 yr) | 1,931 | -0.08 (-0.23, +0.05) | 4.2-5.0 |
| W1-W2 (3.1 yr) | 1,239 | -0.01 (-0.25, +0.23) | 4.7-6.1 |
| S3-S4 (7.2 yr) | 1,826 | -0.02 (-0.11, +0.10) | 4.3-5.9 |
| W1-W4 (11.3 yr) | 1,196 | 0.00 (-0.18, +0.14) | 8.0-8.7 |

b = 0 means that f_m wanders by the same absolute amount (about 5e-5 c/d in 3 yr and 8.5e-5 c/d in 11 yr) for all P_B from 24 to 150 days. b = +1 means that P_B changes by the same fraction for all stars. The data reject b = +1 by a wide margin. The relative change of P_B is therefore about six times larger for P_B = 150 d than for P_B = 25 d.

### 4.4 The f_m change does not follow the f0 change

Between OGLE-III and OGLE-IV (S3-S4), 1,303 stars have a significant f0 change (more than 3 sigma). Their df_m and df0 are not correlated (Spearman +0.05, p = 0.09). In the subgroup with the larger side peak at f0 - f_m (n = 356), Spearman is +0.03 (p = 0.62) and the median-regression slope is -0.005; a fixed f0 - f_m side peak predicts +1. Thus we do not replicate the tentative +0.41 subgroup correlation of the field sample (Figure 3). The median abs(df_m)/abs(df0) is 3.4, and the relative change of P_B is about 400 times the relative change of the pulsation period.

### 4.5 Modulated stars change their pulsation frequency more

The median abs(df0) from OGLE-III to OGLE-IV is 9.6e-6 c/d for the Blazhko stars (n = 2,156) and 2.6e-6 c/d for the clean controls (n = 223; Mann-Whitney p = 6e-30; Figure 4). 16.3% of Blazhko stars and 1.8% of controls changed f0 by more than 5e-5 c/d. The result is the same with f0 from the full modulation model (median 9.7e-6 c/d, typical error 1.3e-6 c/d). This replicates the field result (1.36e-5 against 6.2e-6 c/d).

### 4.6 A small mean increase of P_B

P_B increased more often than it decreased, and the median increase grows with separation (Figure 6):

| Pair | Separation (yr) | Median dP_B/P_B | Increase, all stars (p) | Increase, changes > 3 sigma (p) |
|---|---|---|---|---|
| W1-W2 | 3.1 | +2.4e-4 | 53.3% (0.02) | 54.5% of 246 (0.18) |
| W3-W4 | 3.2 | +1.3e-4 | 52.5% (0.03) | 53.1% of 665 (0.12) |
| W2-W3 | 4.9 | +1.8e-4 | 52.4% (0.06) | 56.5% of 439 (0.007) |
| W1-W3 | 8.0 | +3.1e-4 | 53.5% (0.01) | 57.1% of 368 (0.008) |
| W2-W4 | 8.1 | +2.0e-4 | 52.2% (0.09) | 56.5% of 503 (0.004) |
| W1-W4 | 11.3 | +5.4e-4 | 55.7% (9e-5) | 59.5% of 378 (2.5e-4) |
| S3-S4 | 7.2 | +2.5e-4 | 55.0% (2e-5) | 57.6% of 752 (4e-5) |
| W0-W4 | 16.1 | +2.6e-4 | 52.8% (0.25) | 60.3% of 184 (0.006) |

A median regression through the origin gives +3.4e-5 per year. The constant-f_m simulations give +0.4e-5 (OGLE-III halves, 50.2% increases) and +5.7e-5 (OGLE-IV halves, 52.4%, p = 0.09). Thus the 3-year values are of the same size as a possible method offset, but the 11-year value is about 10 times larger.

We tested three artefact explanations:

- Wrong-peak picks in the sparser OGLE-III windows. The search window is wider above f_ref than below it, so wrong picks would give a high f_m in OGLE-III and an apparent P_B increase. But the excess stays when we keep only changes below 2% (W1-W4: 56.4%, p = 5e-5), and when the blind scan agrees with the local peak in both windows (55.1%, p = 6e-4). The excess is absent in the lowest third of OGLE-III F values (50.4%) and present in the middle and high thirds (59%, 58%).
- Selection in the later epoch. The catalogue selects stars with strong modulation in OGLE-IV. Within stars, a P_B increase comes with a small decrease of the relative modulation amplitude (Spearman -0.06 to -0.09 in four of five pairs, p = 1e-4 to 0.04). So a selection by strong modulation in the later epoch prefers recent P_B decreases. It cannot make the increase. The excess also does not depend on the OGLE-IV detection strength (54-57% in all thirds).
- Time-scale errors. A relative change of 5e-4 needs a time-scale error of the same size between surveys. This is not possible for HJD times.

The prior field sample showed the same sign (59% increases from LINEAR to ZTF). We do not know the cause. The mean rate (3.4e-5 per year, an e-folding time of about 30,000 yr) is much too fast for stellar evolution.

## 5. Interpretation

1. The Blazhko period of bulge RRab stars is not a stable clock. This independently confirms the field result of sci:sha256:b42c1d2b with different stars, instruments and years. A rotation period cannot change by percents in a few years, so a rotation clock can explain at most the minority of stars without a measured change.
2. Between 3 and 11 years the wander grows like a random walk with independent steps. A bounded process with a correlation time of 2-4 years, the explanation suggested for the field data, does not agree with these OGLE data. Slower growth after about 11 years is possible (OGLE-II subsample) but not shown.
3. The modulation frequency, not the period, wanders by a fixed absolute amount. This is natural if f_m is a difference of two frequencies (for example a radial mode and a nonradial or resonant mode, or a detuning in a resonance model), and one of them wanders by about 5e-5 c/d in 3 years. Because f0 changes much less (median 1e-5 c/d in 7 years), the wandering component cannot be the radial mode. Models where P_B changes by a fixed fraction (for example a rotation period with differential rotation, or a cycle that scales with its length) do not fit.
4. The f_m change does not follow the f0 change. So a fixed nonradial-mode frequency is not the explanation. The tentative subgroup result of the field sample is not replicated.
5. Modulated stars have about four times larger pulsation-frequency changes. The same process that moves f_m probably also disturbs the pulsation.

## 6. Limitations

- The sample is the Skarka et al. (2020) catalogue, which found P_B in OGLE-IV data. We search f_m only within 0.75-1.33 times the catalogue value. Larger changes, and stars that lost or gained their modulation, are outside the test. 20.5% of OGLE-III P_B values differ from the catalogue value by more than 1%, and 6.3% by more than 5%.
- 25% of random non-catalogue RRab in the same fields are also modulated. The catalogue is not complete, and its selection may favour some kinds of stars.
- The model has one modulation frequency and k = 1, 2 triplets. Stars with two modulation periods can swap peaks between windows. The null simulations include unmodelled structure only as noise. We made 2 simulations per star and survey for 800 stars; the null rates have Poisson uncertainty (for example 1.6% of 1,161 pairs).
- There is no null simulation for pairs between surveys (OGLE-II to OGLE-III/IV, OGLE-III to OGLE-IV). We use the inflation factors from each survey. OGLE-II uses the OGLE-III factor.
- The structure-function points share stars; the chi-square values compare models but are not exact tests. The noise correction depends on the calibrated errors. The OGLE-III halves give a larger rms than the OGLE-IV halves at the same separation (0.31% against 0.24%), which can mean that OGLE-III errors are still slightly underestimated.
- The mean P_B increase is small. Within OGLE-IV, the constant-f_m simulations show an offset of the same size as the 3-year values (p = 0.09). Only the long-separation excess is clearly above the possible method offset. We have no mechanism for it.
- Control stars have random trial windows. Their F distribution depends on sampling and blending. We do not correct for blending in crowded bulge fields. Blending changes amplitudes but not frequencies.
- Changes faster than about 1.5 years are averaged by the window length.

## 7. What remains open

- OGLE-IV photometry after 2017 (not in the public catalogue files) would extend the baseline to about 25 years and test the slower growth after 11 years suggested by the OGLE-II subsample.
- The mean P_B increase needs a cross-survey null (for example injection of constant-f_m signals with OGLE-III and OGLE-IV sampling of the same star) and an independent sample (Kepler/K2, TESS, ASAS-SN).
- The fixed absolute wander of f_m should be compared with resonance-model simulations (for example the 9:2 resonance of Buchler & Kolláth 2011) that predict how detuning changes.
- The 99 modulated control stars (`files/results/controls_modulated_uncatalogued.csv`) can be added to Blazhko catalogues after a check.
- RRc stars (Netzel et al. 2018 list) can be tested in the same way.

## 8. Reproduction and provenance

Code is in `files/code/` (Python 3.12.16, numpy 2.5.4, scipy 1.18.1, pandas 3.1.1, matplotlib 3.11.2). Run:

```
bash files/code/run_all.sh <scratch_dir> <path to files/>
```

This gets the external data into `<scratch_dir>` (never into this publication), runs the main pass (`ogle_windows.py`, 2,631 stars), the control pass (398 stars), the null simulations (`nullsim.py`, 800 stars, 2 simulations per survey), then `results.py` and `figures.py`. Run time is about 3 hours on 2 CPUs. Random seeds are fixed (CRC32 of the star name; 20261112 for the bootstraps).

In the original run, the first 373 stars of the main pass used 4-8 night-wise bootstrap refits per window (`--nboot`); the rest used none. These bootstrap values give only the robustness check in section 4.1; the default `run_all.sh` uses none. The original run also made the blind scan in the full-survey windows S3/S4 for these stars; this has no effect on any result.

Files in this bundle (all are our own measurements, code and figures):

- `files/results/window_fits.csv.gz`: per star and window: f0, f_m, formal errors, F statistic, side-peak amplitudes, blind-scan peak, detection flag and calibrated error. The Skarka et al. catalogue values are removed; get them from VizieR.
- `files/results/pair_changes.csv.gz`: all window-pair changes (dfm, calibrated sigma, z, dP_B/P_B, df0).
- `files/results/pair_summary.csv`, `structure_function.csv`, `df0_modulated.csv`, `df0_controls.csv`, `controls_modulated_uncatalogued.csv`, `stats.json` (all numbers in this text).
- `files/results/null_simulations.jsonl.gz`: the constant-f_m simulation fits.
- `files/provenance/names_*.txt`: the star lists. `files/provenance/input_sha256.txt`: SHA-256 of all input files used (catalogues, tarballs, each light curve).
- `files/figures/`: Figures 1-6.

## 9. Figures

- Figure 1 (`files/figures/fig1_change_fraction_vs_lag.png`): fraction of stars with a P_B change above 3 and 5 sigma against the time separation, with the null rates and the prior field result.
- Figure 2 (`files/figures/fig2_structure_function.png`): noise-corrected rms of dP_B/P_B against separation for the common W1-W4 sample, with random-walk, bounded and drift fits.
- Figure 3 (`files/figures/fig3_dfm_vs_df0.png`): df_m against df0 from OGLE-III to OGLE-IV, by the dominant side peak.
- Figure 4 (`files/figures/fig4_df0_modulated_vs_control.png`): cumulative distributions of abs(df0) for Blazhko and control stars.
- Figure 5 (`files/figures/fig5_absolute_wander_vs_PB.png`): noise-corrected rms of df_m against P_B, with the fixed-fraction prediction.
- Figure 6 (`files/figures/fig6_population_drift.png`): median dP_B/P_B against separation, with the constant-f_m simulation values.

## References

Buchler & Kolláth 2011, ApJ 731, 24. Netzel et al. 2018, MNRAS 480, 1229. Shibahashi 2000, ASP Conf. Ser. 203, 299. Skarka et al. 2020, MNRAS 494, 1237. Soszyński et al. 2011, Acta Astron. 61, 1. Soszyński et al. 2014, Acta Astron. 64, 177. Soszyński et al. 2019, Acta Astron. 69, 321. Stothers 2006, ApJ 652, 643. Udalski, Szymański & Szymański 2015, Acta Astron. 65, 1. Prior campaign result: sci:sha256:b42c1d2bbb7b53538c914e0605a46a054878411e782d7c3ffc218360455ba74c.
