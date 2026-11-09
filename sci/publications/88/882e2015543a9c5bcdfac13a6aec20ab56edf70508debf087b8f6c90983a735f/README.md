# Later ZTF data and Gaia DR3 data do not follow the published sinusoids of 36 periodic-quasar binary black-hole candidates

Job: sci-1107-dell-astronomy-b3008d13ae9f. Campaign: 11_07_2026. Topic: astronomy. Machine: dell. Model: Claude Opus 5.5 (claude-opus-5-5). Date of analysis: 2026-11-09. The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Foustoul et al. (2025, A&A 699, A55; arXiv:2505.06656) report 36 quasars with sinusoidal optical variation over 3 to 5 cycles in CRTS (2005-2013) and ZTF (2018 to mid 2022) data. They propose these quasars as sub-parsec massive black-hole binary (MBBH) candidates. 26 of the 36 come from the CRTS list of Graham et al. (2015). The other 10 come from the ZTF periodic-variable catalogue of Chen et al. (2020).

A binary orbit gives a coherent period. Thus the fitted sinusoid must predict data that the authors did not use. Foustoul et al. did not make such a test. We ask:

1. Does the sinusoid at the published period predict Gaia DR3 G-band epochs from 2014.6 to 2017.4? These epochs fall in the gap between CRTS and ZTF. No selection step used them.
2. Does it predict ZTF epochs after the end of the published ZTF data (MJD 59800, August 2022) to October 2025?
3. Is the prediction better than red noise alone, and better than the prediction at random periods?

## 2. Data

All data are public. We did not use private data.

| Data | Source and version | Use |
|---|---|---|
| Candidate list (36) | Table 4 of Foustoul et al. 2025, read from the arXiv v1 LaTeX source (arXiv:2505.06656) | published periods, identifiers |
| Graham et al. 2015 list (111) | VizieR J/MNRAS/453/1562 (CfA mirror, retrieved 2026-11-09) | coordinates, Graham periods |
| Coordinates of 10 ZTF-selected candidates | VizieR J/ApJS/249/18 tables 2 and 3 (Chen et al. 2020), match on truncated J names | coordinates |
| ZTF DR24 light curves | IRSA ZTF DR24 HATS Parquet copy on AWS S3 (`s3://ipac-irsa-ztf/ztf/enhanced/dr24/lc/hats/`, DOI 10.26131/IRSA598), objects within 1.5 arcsec | training and forward hold-out |
| Gaia DR3 source match and G epoch photometry | `gaiadr3.gaia_source` and `gaiadr3.epoch_photometry` on the AIP TAP mirror (https://gaia.aip.de/tap), 1.5 arcsec cone | Gaia hold-out |

The IRSA web service did not accept connections from this host on 2026-11-09. Thus we read the S3 Parquet copy of the same release. The CRTS (CSDR2) web forms did not work (name resolver error, coordinate search 404, multi-cone time out). Thus we do not use CRTS data directly. Section 5 explains how we model the effect of the CRTS-based period selection.

Coverage of the 36 candidates: all 36 have ZTF r and g data. Training has 179 to 779 nightly r points (median 335). The forward hold-out has 19 to 368 nightly r points (median 130), from MJD 59801 to 60970. 31 candidates have Gaia DR3 epoch photometry (15 to 36 nights, median 20, MJD 56865 to 57901). Five candidates have no Gaia epoch photometry (`has_epoch_photometry` = False).

`files/data/provenance_sha256.csv` gives the SHA-256 hash of every raw file that we used. `files/data/ztf_dr24_extracts.tar` and `files/data/gaia_dr3_epoch_photometry_aip.tar` hold the raw extracts.

## 3. Method

Light-curve preparation (`code/lcio.py`). ZTF: keep `catflags` = 0 and magerr < 0.5. Average each ZTF object (field, CCD and filter) per night with inverse-variance weights. Remove 5-sigma outliers from a 9-night running median. Gaia: remove transits with `variability_flag_g_reject`, convert flux errors to magnitude errors, and average per night. Add 0.02 mag in quadrature to Gaia errors (0.04 mag as a sensitivity test).

Models (`code/gpmodel.py`). We fit two models to the ZTF r training data (MJD <= 59800):

- S: sinusoid at the published period P, plus a damped random walk (DRW, celerite2 RealTerm), plus one offset per ZTF object, plus a white jitter term.
- D: the same model without the sinusoid.

The offsets and the sinusoid coefficients are linear terms. We solve them by generalized least squares. We fit the DRW amplitude, the DRW time scale and the jitter by maximum likelihood. The period stays fixed at the published value.

Predictions. For each hold-out we compute the Gaussian predictive distribution of each model. It includes the DRW covariance and the uncertainty of the linear terms (universal kriging).

- Gaia hold-out: one free offset for the Gaia G band (marginalized with a flat prior). The sinusoid amplitude in G is the same as in r.
- Forward ZTF hold-out: the same ZTF objects and the fitted offsets. No free parameter.

Score. Delta = log predictive density of the hold-out data under S minus under D, in nats. Delta > 0 means that the published sinusoid predicts better than red noise alone. We repeat the same analysis in the g band for the forward hold-out.

Random-period null (`code/10_holdout_test.py`). For each source we repeat the S model at 200 random periods (r band; 100 in g) from a uniform distribution on 500 to 2500 d. This is the period prior of Foustoul et al. The percentile of the published-period score among the random-period scores is a second test statistic.

Calibration simulations (`code/11_simulate.py`, `code/12_simulate_crts.py`). We simulate each of the 31 candidates with Gaia data on its own real time sampling and errors, 6 times for each scenario:

- H0a, DRW with a ZTF period search: a DRW light curve with the parameters of the D fit. The "published" period is the best training-likelihood period on a 61-point grid in 500-2500 d.
- H0b, DRW with CRTS+ZTF sinusoid selection: a DRW light curve that we also sample at simulated CRTS epochs (2005-2013, 0.07 mag errors). The "published" period is the best pure-sinusoid chi-square fit to CRTS+ZTF (401-point grid), as in Foustoul et al. This null includes the information that CRTS data near 2013 give about the Gaia era.
- H1, coherent sinusoid: the published period with the fitted S amplitude (and with half of it), a random phase, and DRW noise with the S parameters.

Mixture limit (`code/33_mixture.py`). We put each candidate in a category from the signs of the two Delta values. We use the pooled category probabilities from H0 and H1 to fit the fraction f of candidates with a coherent sinusoid. We give the 95% one-sided likelihood-ratio upper limit on f.

Sample B (`code/32_sample_B.py`). We apply the same pipeline to the Graham et al. 2015 list at the Graham periods (100 random periods per source). This includes the 26 sources that Foustoul et al. kept and the other Graham candidates.

## 4. Results

### 4.1 The 36 candidates of Foustoul et al. 2025

| Hold-out | Sources | S better than D | Median Delta (nats) | Sum of Delta (nats) | Mean percentile among random periods |
|---|---|---|---|---|---|
| Gaia G, 2014.6-2017.4 | 31 | 9 | -1.6 | -180 | 0.50 |
| ZTF r, Aug 2022 - Oct 2025 | 36 | 3 | -13.8 | -804 | 0.26 |
| ZTF g, Aug 2022 - Oct 2025 | 36 | 2 | -16.7 | -1396 | 0.25 |

No candidate has Delta > 0 in both the Gaia and the forward ZTF r hold-outs. The three forward-positive candidates (J082716+490534, J081133+065558, J122728+322508) have Delta = +0.85, +0.76 and +0.08 nats. These values are small. The sinusoid of J082716+490534 predicts the sign of the 2022-2025 brightening but not its size (Figure 1).

Comparison with simulations on the same sampling (186 simulations for each scenario):

| Statistic | Real data | H0a DRW, ZTF search | H0b DRW, CRTS+ZTF selection | H1 sinusoid, fitted amplitude | H1 sinusoid, half amplitude |
|---|---|---|---|---|---|
| Gaia: fraction Delta > 0 | 0.29 (9/31) | 0.12 | 0.18 | 0.73 | 0.60 |
| Gaia: median Delta | -1.6 | -3.9 | -2.5 | +2.2 | +0.5 |
| Forward ZTF r: fraction Delta > 0 | 0.08 (3/36) | 0.07 | 0.15 | 0.72 | 0.64 |
| Forward ZTF r: median Delta | -13.8 | -7.9 | -4.8 | +2.0 | +0.8 |
| Forward ZTF r: mean percentile | 0.26 | 0.22 | 0.33 | 0.79 | 0.74 |
| Both Delta > 0 | 0/31 | 0.005 | 0.024 | 0.56 | 0.43 |

The forward ZTF result agrees with the red-noise nulls. It does not agree with a coherent sinusoid. The published periods rank below the median of random periods (mean percentile 0.26), as the nulls with a period search predict (0.22 and 0.33). The reason is that a period search selects sinusoids that fit the training data well, but these sinusoids then extrapolate badly.

The Gaia result is between the nulls and H1. Against H0a, the Gaia positive fraction is higher than expected (binomial p = 0.011). Against H0b, which includes the CRTS-based selection, the excess is not significant (binomial p = 0.10; Mann-Whitney test of Delta values p = 0.71). The percentile test against H0b is marginal (p = 0.047). The Gaia result is far from H1 (all tests p < 0.0001). Thus the Gaia data do not support coherent sinusoids. A weak Gaia excess is possible. A plausible cause is that the CRTS data up to late 2013 constrain the light curve near the start of the Gaia window. Our H0b uses only an approximate CRTS sampling.

Mixture limit on the fraction f of candidates with a coherent sinusoid (`results/mixture_A.csv`):

| Null (H0) | Signal (H1) | Best-fit f | 95% upper limit on f | Candidates (of 36) |
|---|---|---|---|---|
| DRW, ZTF period search | full fitted amplitude | 0.00 | 0.14 | 5.1 |
| DRW, ZTF period search | half amplitude | 0.00 | 0.19 | 6.8 |
| DRW, CRTS+ZTF sine selection | full fitted amplitude | 0.00 | 0.08 | 3.0 |
| DRW, CRTS+ZTF sine selection | half amplitude | 0.00 | 0.10 | 3.7 |

The best-fit fraction is zero for all four combinations. At most 3 to 7 of the 36 candidates can carry a coherent sinusoid with the fitted (or half the fitted) amplitude.

### 4.2 The Graham et al. 2015 sample at the Graham periods

| Group | Hold-out | Sources | Delta > 0 | Median Delta (nats) | Sum of Delta (nats) | Mean percentile |
|---|---|---|---|---|---|---|
| kept by Foustoul+2025 | Gaia | 26 | 5 | -1.0 | -129 | 0.48 |
| kept by Foustoul+2025 | forward ZTF r | 26 | 3 | -10.4 | -360 | 0.32 |
| kept by Foustoul+2025 | forward ZTF g | 26 | 3 | -10.9 | -442 | 0.31 |
| other Graham+2015 | Gaia | 70 | 27 | -0.7 | -66 | 0.52 |
| other Graham+2015 | forward ZTF r | 71 | 13 | -1.4 | -923 | 0.48 |
| other Graham+2015 | forward ZTF g | 68 | 16 | -1.6 | -645 | 0.47 |
| all | Gaia | 96 | 32 | -0.7 | -194 | 0.51 |
| all | forward ZTF r | 97 | 16 | -2.4 | -1282 | 0.44 |
| all | forward ZTF g | 94 | 19 | -2.3 | -1087 | 0.42 |


The 26 sources that Foustoul et al. kept do worse in the forward ZTF r hold-out than the other Graham candidates (median Delta -10.4 against -1.4 nats; Mann-Whitney p < 0.001). For most of the other Graham candidates, the fitted sinusoid amplitude in ZTF is near zero, so S and D give almost the same prediction. The kept sources have larger fitted amplitudes, so their sinusoids make confident predictions. These predictions fail.

Nine Graham candidates have Delta > 0 in both hold-outs. Seven of them have a fitted r amplitude below 2 sigma (0.00 to 0.08 mag), so the score gain carries almost no period information. The other two (SDSS J121457.39+132024.3, 0.14 +/- 0.06 mag; HS 1630+2355, 0.06 +/- 0.02 mag) have published-period percentiles of only 0.59 to 0.88 among random periods. HS 2219+1944 (z = 0.211) has the largest gains (Gaia +63.8, ZTF r +34.6, ZTF g +6.3 nats). But it has only 51 training nights and 13 forward nights in r (the r and g data come only from the secondary ZTF field 1642), its fitted amplitude is 0.08 +/- 0.08 mag, and 18% of random periods give a better Gaia score. SDSS J161013.67+311756.4 and 4C 50.43 have forward gains of +4.3 and +5.1 nats but amplitudes of 0.02 and 0.01 mag. No Graham candidate passes all of these criteria: Delta > 0 in both hold-outs, a published-period percentile above 0.95 in both, and an amplitude above 3 sigma.

## 5. Interpretation

- The 36 candidates were selected because a sinusoid fits their CRTS and ZTF data. A DRW light curve with a period search gives the same kind of fit. Data that the selection did not use (ZTF after August 2022 and Gaia 2014-2017) do not follow the published sinusoids. The forward ZTF scores are as bad as those of DRW light curves with a period search.
- This agrees with a parallel campaign study (sci:sha256:1370d3912bd4d2bdf79365974bcc74ab344974c87e0c5761ea4750f332d99c15), which found that the 86 ZTF candidates of Chen et al. (2022) do not continue their sinusoids in ZTF data after March 2022 (95% upper limit on the coherent fraction about 6-28%). That study used a different candidate sample and no Gaia data. It also agrees with the result of El-Badry, Hogg and Rix (arXiv:2509.10601) for Gaia-selected candidates and with the theoretical expectation that red noise produces false periods in 2-5 cycles (Vaughan et al. 2016).
- The result does not exclude binary black holes in these quasars. It excludes coherent sinusoids with the fitted amplitudes for most of the 36 sources. A binary could give a weaker, non-sinusoidal or changing signal.

## 6. Limitations

- We did not reproduce the CRTS+ZTF fits of Foustoul et al., because the CRTS service did not work. We fit the phase and amplitude from ZTF alone at the published period. The published phases are not tabulated.
- The ZTF data end of Foustoul et al. (MJD 59800) is an estimate from their light-curve figures. If their data ended earlier, a small part of our training set is also new data. This does not change the forward hold-out after MJD 59800.
- The Gaia G band differs from ZTF r. We assume the same sinusoid amplitude in G and r. A free Gaia offset absorbs the mean colour.
- The DRW model is a simple red-noise model. Real quasar variability can have a steeper high-frequency power spectrum.
- H0b uses a generic CRTS sampling and a 0.07 mag error, not the real CRTS epochs of each source.
- The 1.5 arcsec ZTF match radius can miss objects for quasars in extended host galaxies (for example HS 2219+1944).
- The simulations use 6 realizations per source and scenario (186 per scenario in total). The limits on f have Monte Carlo uncertainty of a few percent.
- Five of the 36 candidates have no Gaia epoch photometry.

## 7. Files

- `files/figures/fig1_examples.png`: three example light curves with the S and D predictions.
- `files/figures/fig2_per_source_scores.png`: Delta for each candidate, with the random-period range.
- `files/figures/fig3_vs_simulations.png`: distributions of Delta and percentiles, real and simulated.
- `files/figures/fig4_graham_sample.png`: Graham et al. 2015 sample at the Graham periods.
- `files/results/summary_A.csv`, `summary_B_labeled.csv`: scores for each source (columns: `r_d_lp_gaia` = Gaia Delta, `r_d_lp_fwd` = forward ZTF r Delta, `*_pct_*` = percentile among random periods, `r_amp` = fitted r amplitude in mag).
- `files/results/stats_A.csv`, `stats_B.csv`, `gaia_excess_tests.csv`, `mixture_A.csv`, `strict_pass.txt`: aggregate statistics.
- `files/results/sim_A_flat.csv` (H0a and H1), `sim_A_crts_flat.csv` (H0b), `sim_A_half_flat.csv` (H1 at half amplitude): one row per simulation.
- `files/results/res_A.tar`, `res_B.tar`: full per-source JSON results (fits, predictions, random-period scores). `files/results/sims.tar`: per-simulation scores.
- `files/code/`: all code. `files/data/`: inputs, raw extracts and hashes.

## 8. How to reproduce

Python 3.12 with numpy, scipy, pandas, astropy, pyarrow and matplotlib, plus `pip install --target pylib celerite2==0.3.3 emcee astropy-healpix`. Set `PYTHONPATH=pylib:code`, `OMP_NUM_THREADS=1`.

```
python code/01_candidates.py                       # parse Table 4 of arXiv:2505.06656 (needs raw/arxiv/foustoul/main.tex) + Graham VizieR table
python code/02_resolve_chen.py                     # or use data/chen_resolved_raw.txt
python code/03_gaia_match.py derived/foustoul36.csv derived/gaia_match_f36.csv   # AIP TAP; rename datalinkID to source_id
python code/04_ztf_s3.py derived/ztf_targets.csv raw/ztf_dr24 6                    # ZTF DR24 from S3 (about 25 s per target)
python code/05_gaia_epoch.py derived/gaia_match_f36.csv derived/gaia_match_g111.csv
python code/10_holdout_test.py derived/sample_A_foustoul36.csv derived/res_A 200 8
python code/10_holdout_test.py derived/sample_B_graham111.csv derived/res_B 100 6
python code/20_summarize.py derived/res_A derived/summary_A.csv
python code/20_summarize.py derived/res_B derived/summary_B.csv
python code/11_simulate.py derived/res_A derived/sim_A 6 50 10
AMP_SCALE=0.5 python code/11_simulate.py derived/res_A derived/sim_A_half 6 30 10
python code/12_simulate_crts.py derived/res_A derived/sim_A_crts 6 30 6
python code/31_fig_summary.py; python code/34_gaia_excess.py; python code/33_mixture.py half; python code/32_sample_B.py; python code/35_strict_pass.py
python code/30_fig_examples.py F00,F11,F15 figs/fig1_examples.png
```

To skip the downloads, unpack `data/ztf_dr24_extracts.tar` and `data/gaia_dr3_epoch_photometry_aip.tar` into `raw/`. Simulations use fixed seeds, but the DRW sampler of celerite2 uses the global numpy random state.

## References

- Foustoul, Webb, Mignon-Risse et al. 2025, A&A 699, A55, doi:10.1051/0004-6361/202452818, arXiv:2505.06656.
- Graham et al. 2015, MNRAS 453, 1562, doi:10.1093/mnras/stv1726.
- Chen et al. 2020, ApJS 249, 18, doi:10.3847/1538-4365/ab9cae.
- El-Badry, Hogg and Rix 2025, arXiv:2509.10601.
- Vaughan et al. 2016, MNRAS 461, 3145, doi:10.1093/mnras/stw1412.
- Gaia Collaboration 2023, A&A 674, A1 (Gaia DR3). ZTF DR24: doi:10.26131/IRSA598.
- Foreman-Mackey et al. 2017, AJ 154, 220 (celerite).
