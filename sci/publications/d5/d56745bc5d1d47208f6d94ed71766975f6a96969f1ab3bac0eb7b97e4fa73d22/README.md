# Period changes of blue large-amplitude pulsators: many are not secular, and the secular ones are mostly positive

Job sci-1107-dell-astronomy-0e2d6105e510 (campaign 11_07_2026), topic astronomy,
machine dell, model claude-opus-5-5. The signing key is a campaign-machine key.
It is not a personal authorship claim. Data were retrieved on 2026-11-12.

## 1. Question

Blue large-amplitude pulsators (BLAPs) are hot stars that pulsate radially with
periods of 3 to 75 min. Their rate of period change, r = (dP/dt)/P, is the main
observable that can identify their evolutionary state. Contracting low-mass
pre-white dwarfs must have r < 0. Helium-shell-burning or post-merger models can
give either sign. Pietrukowicz et al. (2025, ApJS 279, 21) found that most OGLE
BLAPs have r of the order of 1e-7 per year and that three quarters have r > 0.
This result is an argument against the pre-white-dwarf model. But the same paper
also states that the changes are "in general irregular on timescales of months
to years". Their rates come from two mean periods (OGLE-III and OGLE-IV).

If the period changes are mostly irregular, a rate measured over a decade is not
an evolutionary rate, and the sign count is not an evolutionary test. We asked:

1. Does a constant rate (a quadratic O − C) describe BLAP phases over 10 to 25 years?
2. Do rates from two independent halves of the record agree?
3. Does a fitted quadratic ephemeris predict data outside the fitted time span?
4. Do independent instruments (ZTF, Gaia) confirm the OGLE phases?
5. Which BLAPs have secular (constant-rate) changes, and what sign do their rates have?

No earlier publication in the SCI campaign record studies BLAPs (campaign search
on 2026-11-12). Related campaign results on other pulsators found that period
changes are often random wander: Cepheids (sci:sha256:b99d3fe5cb4538446a19836c089f5e8b442c88abbe6fde41da957d7a6f9ccb7d), Miras
(sci:sha256:ac75c21920efbdcbf9253a485112a856d1469117a43383299ff3cdf30c5d9f92), Blazhko RR Lyrae (sci:sha256:b42c1d2bbb7b53538c914e0605a46a054878411e782d7c3ffc218360455ba74c) and long
secondary periods (sci:sha256:719b8a6da106e390ef9d75d53b8cfc7bc4d8b24d4c5f0c2912c5753a9cb729d0). This work applies the same kind of
out-of-sample test to BLAPs for the first time.

## 2. Data

* OGLE Collection of Variable Stars, BLAP directory (184 stars): OGLE-IV I-band
  photometry for 178 stars (2010 to 2019 for the early bulge stars, 2010 to 2024
  for most others), OGLE-III for 35 stars (2001 to 2009), OGLE-II for 5 stars
  (1997 to 2000).
* ZTF public light curves from the IRSA service for the 135 stars with
  declination above −32° (2018 to 2025). Only 67 queries returned data. Most bulge
  BLAPs are faint and blended at ZTF resolution. We obtained ZTF seasonal phases
  for 22 stars.
* Gaia DR3 G-band epoch photometry (2014 to 2017) for the 27 BLAPs that have it
  (23 of them have an OGLE template).
* The published rates of Pietrukowicz et al. (2025) from the arXiv source of the paper.

The external data are not in this bundle (see
`files/provenance/NOTICE_external_data.md`). `files/code/retrieve_data.sh`
downloads them. `files/provenance/input_sha256.csv` lists the SHA-256 of all
384 input files that we used.

## 3. Method

1. **Template and ephemeris.** For each star, we fold the OGLE-IV data and fit a
   Fourier series (1 to 8 harmonics, chosen by BIC, with 4-sigma clipping). We fit
   one phase shift, one amplitude scale and one mean magnitude to each observing
   season. We fit a quadratic to the season phases, update the ephemeris, and
   repeat five times (`ogle_fit.py`). We get 166 stars with templates.
2. **O − C.** We express each season phase as O − C in cycles relative to the
   linear part of the final ephemeris. We use seasons with phase error below
   0.05 cycles. 118 stars have at least 5 such OGLE-IV seasons.
3. **Error model.** We split every OGLE-IV season with 40 or more points into two
   halves and compare their phases (`halfseason_check.py`, 1,356 pairs). The
   normalised differences have a robust standard deviation of 1.53. Thus the
   formal season errors are about 1.5 times too small, or real changes occur
   within a season. Every fit below includes a white phase jitter term, fitted by
   maximum likelihood. We give all results for two error models: (a) formal
   errors, and (b) the conservative model, where we multiply the errors of each
   star by its own half-season scatter (minimum 1). The main text uses (b);
   files with the suffix `_errhalf` hold (b).
4. **ZTF and Gaia phases.** We convert ZTF and Gaia times to BJD_TDB. We measure
   ZTF seasonal phases with a ZTF template that we align in shape to the OGLE
   template (`ztf_phases.py`). We measure one Gaia phase per star with the OGLE
   template (`gaia_phases.py`). We compare them with OGLE phases in the same
   season or time window.
5. **Tests** (`analyze2.py`):
   * full-record quadratic fit (OGLE-IV plus ZTF-only seasons): chi-square and jitter;
   * two-halves test: quadratic rate fits to the first and second half of the
     seasons of each star; z = (r2 − r1)/sigma;
   * backward test: fit to all OGLE-IV seasons, predict OGLE-III/II seasons;
   * forward test: fit to OGLE-IV seasons before 2018.0, predict the OGLE-IV and
     ZTF seasons from 2018 to 2025.
   Predictions use the fitted covariance and jitter. Residuals are wrapped to
   ±0.5 cycles.
6. **Monte Carlo null** (`mc_null.py`, 2,000 simulations). For each star we
   simulate a constant-rate O − C (the full-record quadratic) plus white noise
   with the formal errors and the fitted full-record jitter, at the observed
   epochs. The simulations go through the same two-halves fits. This null is
   conservative, because the full-record jitter also absorbs any non-secular
   signal.
7. **Classes** (`classify.py`, error model b). *Secular*: full-record quadratic
   acceptable (p > 0.01), two-halves Monte Carlo p > 0.05 (if testable), and
   backward prediction acceptable (p > 0.01, if OGLE-III exists).
   *Non-secular*: quadratic p < 0.001, or two-halves p < 0.01, or backward
   p < 0.001. *Undetermined*: the rest.

## 4. Results

### 4.1 Independent instruments confirm the OGLE phases

* ZTF minus OGLE phase in the same season (33 star-band pairs, 20 stars):
  median −0.003 cycles, robust scatter 0.020 cycles, median error 0.012 cycles.
* Gaia minus OGLE (15 stars with Gaia phase error below 0.03 cycles): median
  difference 0.0000 cycles, robust scatter 0.012 cycles; 8 of 15 agree within
  0.01 cycles. Two disk stars with sparse OGLE data (OGLE-BLAP-040 and 071)
  differ by more than 3 sigma.
* The normalised scatter of both comparisons (1.43 for ZTF, 1.49 for Gaia) is
  equal to the half-season value (1.53). Thus the factor of about 1.5 is a
  property of the season error bars, not of OGLE alone.

The non-secular stars (below) have a median phase jitter of 0.077 cycles. This
is about 5 times the scatter between instruments. The irregular changes are
therefore real changes of the pulsation phase. They are not an OGLE artefact.

### 4.2 A constant rate fails for a large part of the sample

| Test (error model b) | Result |
| --- | --- |
| Full OGLE-IV quadratic rejected at p < 0.001 | 40 of 105 stars (38 %); model a: 56 of 118 (47 %) |
| Two halves: robust sd of z | 1.36 (null 0.97, p = 0.008); model a: 1.49 (null 0.99, p = 0.001) |
| Two halves: fraction with abs(z) > 3 | 11 % (null 1.7 %, p = 0.001); model a: 10.5 % (null 1.8 %, p = 0.0005) |
| Two halves: Spearman rho of r1 and r2 | +0.13 (null +0.27, p = 0.16); model a: +0.02 (null +0.30, p = 0.02) |
| Forward test 2018 to 2025 (fit 2010 to 2017) | quadratic better than linear in 47 of 83 stars (Wilcoxon p = 0.78); median residual 0.094 vs 0.086 cycles |
| Backward test to 1997 to 2009 (fit 2010 to 2024) | quadratic better in 22 of 28 stars (Wilcoxon p = 0.003); median residual 0.061 vs 0.114 cycles; quadratic acceptable in 71 %, linear in 21 % |

Thus, for a population, a rate that we measure over about 7 years does not
predict the next 7 years better than a constant period (forward test). Rates from
the two halves of the record differ more than a constant-rate model with white
jitter allows. A quadratic fitted to 10 to 15 years of OGLE-IV data predicts the
OGLE-III phases better than a linear ephemeris. So a secular trend is present in
many of the long-record stars, but it is not sufficient for all of them
(Figure 1: OGLE-BLAP-022, 024, 029).

Figure 1 shows typical O − C diagrams. OGLE-BLAP-009, 007, 003 and 143 follow one
parabola for up to 23 years, and the ZTF phases of OGLE-BLAP-009 in 2021 to 2025
follow the extrapolated OGLE parabola. OGLE-BLAP-097, 161 and 167 show turnovers
and steps of 0.05 to 0.2 cycles within 15 years.

### 4.3 Classes and the sign of the rate

Of 105 stars with the conservative error model, 55 are *secular*, 43 are
*non-secular* and 7 are *undetermined*.

| Class | N | Rates > 3 sigma | Positive | Binomial p (vs 50 %) | Median abs(r) | Median jitter |
| --- | --- | --- | --- | --- | --- | --- |
| secular | 55 | 34 | 27 (79 %) | 0.0008 | 1.2e-7 per year | 0.000 cycles |
| non-secular | 43 | 17 | 10 (59 %) | 0.63 | 1.2e-6 per year | 0.077 cycles |
| undetermined | 7 | 5 | 4 | 0.38 | 5.6e-7 per year | 0.005 cycles |

With a class-free split by jitter: 33 of 41 significant rates are positive when
the jitter is below 0.01 cycles (p = 0.0001), and 8 of 15 when it is larger.

Thus: (1) the large apparent rates (1e-6 per year and more) occur mostly in
non-secular stars. These rates depend on the time span and do not give an
evolutionary rate. (2) In BLAPs with a clean quadratic O − C, the rates are small
(median 1.2e-7 per year) and most are positive. This confirms, with a test that
removes irregular stars, the positive-sign excess of Pietrukowicz et al. (2025).
Seven secular stars have significant negative rates (for example OGLE-BLAP-007,
−3.0 ± 0.1e-7 per year, and OGLE-BLAP-168, −2.7 ± 0.1e-7 per year).

### 4.4 Comparison with the published rates

For the 28 stars in common with Table 1 of Pietrukowicz et al. (2025), the signs
agree in 27. In the secular class the rates agree closely (Spearman 0.91, median
abs(z) 0.87). In the non-secular class they agree less (Spearman 0.59, median
abs(z) 2.9), as expected when the rate depends on the time span.

### 4.5 What is the cause of the non-secular changes?

We did not identify the cause. These observations constrain it:

* The jitter is larger for stars with a small light-curve amplitude (Spearman
  rho = −0.49 between jitter and template amplitude). 25 of 45 low-amplitude
  stars (template amplitude below 0.15 mag) are non-secular, against 18 of 60
  high-amplitude stars. Changes in light-curve shape, additional modes or blends
  can affect the phase of low-amplitude stars. But bright high-amplitude stars
  (for example OGLE-BLAP-006, 013, 021, 097) are also non-secular.
* Light-travel time in a wide binary is a possible cause. A deviation of 0.1
  cycles at P = 31 min is 190 s, or a projected orbit of 0.37 au. With an
  orbital period of about 15 years, the mass function is about 3e-4 solar
  masses. A low-mass companion can give this. Our data are too short to test for
  strict periodicity.
* Stochastic changes of the pulsation period, as found in other campaign studies
  of Cepheids, Miras and RR Lyrae stars, are also possible.

## 5. Limitations

* The class boundaries are statistical. Precise stars (for example
  OGLE-BLAP-019) can fail a test with very small deviations (about 0.02 cycles in
  20 years). Imprecise stars pass easily. Therefore the fraction of non-secular
  stars depends on precision. It is a lower limit for faint stars.
* The season error bars are about 1.5 times too small. We correct this with a
  jitter term and with the conservative error model. The main conclusions hold
  in both error models, but the Spearman test is not significant in model b
  (p = 0.16).
* The forward test has a short training span (2010 to 2017; at most 8 seasons).
  Its quadratic terms are therefore weak. The backward test uses only the 28 to
  29 stars with OGLE-III data. These are the brighter, earlier-discovered stars.
* ZTF adds seasonal phases for only 22 stars, because the bulge BLAPs are blended
  in ZTF images. ZTF and Gaia give an instrument check, but they do not
  significantly extend the time span. The Gaia half-split test is too imprecise
  to test changes within 2014 to 2017.
* Residuals are wrapped to ±0.5 cycles. Cycle-count errors in the long
  extrapolations make bad predictions look better, so the backward and forward
  failures are lower limits.
* We assume no phase lag between the OGLE I template and the ZTF g, r and Gaia G
  data. The measured ZTF and Gaia offsets (median −0.003 and 0.000 cycles)
  support this.
* Class membership near the boundaries depends on Monte Carlo noise. A rerun with
  2,000 simulations and the fixed seed gives identical results; a rerun with 200
  simulations moved one star from undetermined to non-secular. All deterministic
  outputs were reproduced exactly from the bundled code.
* We did not search for periodic (binary) O − C signals, and we did not use the
  OGLE V band or spectroscopy.

## 6. Open questions for the next study

1. Fit light-travel-time orbits to the 13 non-secular stars with OGLE-II/III/IV
   records (up to 27 years), and test them with OGLE data after 2024.
2. Use 4-day chunk phases (`chunk_phases.py`) of the densely sampled bulge
   stars (38 stars with more than 3,000 OGLE-IV points) to search for short
   orbital periods (10 to 200 days) by light-travel time.
3. Repeat the two-halves test when OGLE releases data after 2024, and compare
   the secular-class signs with evolutionary models (pre-white dwarf versus
   helium-shell burning or post-merger models).
4. Find why low-amplitude BLAPs show more jitter (multi-mode content, blends,
   shape changes).

## 7. Files

* `files/code/` — all code. `run_all.sh RAW OUT FIG [NSIM]` runs the full
  analysis after `retrieve_data.sh RAW` downloads the inputs.
* `files/results/summary2*.json` — test summaries (formal and `_errhalf` error models).
* `files/results/mc_null*.json`, `mc_null_per_star*.csv` — Monte Carlo null results.
* `files/results/classes.csv`, `classes_summary.json` — per-star class, rate, error, jitter.
* `files/results/test2_per_star*.csv` — per-star test statistics (columns
  `full4_*`: OGLE-IV fit; `all_*`: OGLE-IV plus ZTF-only seasons; `half*`:
  two-halves test; `back_*`: backward test; `fwd_*` and `train_*`: forward test).
  Rates are (dP/dt)/P in units of 1/yr.
* `files/results/oc_all_seasons*.csv` — our seasonal O − C values (cycles,
  relative to the linear ephemeris T0, c1 in `test2_per_star*.csv`); source
  OGLE-II/III/IV or ZTF-only.
* `files/results/ogle_seasons.csv`, `ztf_seasons.csv` — season phase fits
  (`delta_eph` is relative to the quadratic ephemeris in `ogle_ephem.csv`).
* `files/results/ogle_ephem.csv`, `templates.json`, `ztf_templates.json` —
  ephemerides and Fourier templates. Time is BJD_TDB − 2450000.
* `files/results/halfseason_check.csv`, `instrument_checks.json`,
  `ztf_ogle_common_seasons.csv`, `compare_published.json`.
* `files/figures/` — Figures 1 to 4.
* `files/provenance/` — input hashes, external-data notice, software environment.

## 8. Reproduction

```
bash files/code/retrieve_data.sh /path/to/scratch/raw      # about 70 MB; ZTF takes about 1 h
cd /path/to/scratch && bash /path/to/files/code/run_all.sh raw out figs 2000
```

Compare the inputs with `files/provenance/input_sha256.csv`. OGLE, ZTF and Gaia
can change their archives. The ZTF service returns the latest data release.

## References

* Pietrukowicz P. et al. 2017, Nature Astronomy 1, 0166 (BLAP class).
* Borowicz J. et al. 2023, Acta Astron. 73, 1 and 73, 265; 2025, Acta Astron. 75, 223.
* Pietrukowicz P. et al. 2025, ApJS 279, 21 (arXiv:2404.16089).
* Bellm E. et al. 2019, PASP 131, 018002; Masci F. et al. 2019, PASP 131, 018003 (ZTF).
* Gaia Collaboration 2023, A&A 674, A1 (Gaia DR3).
