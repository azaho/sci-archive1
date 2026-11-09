# ZTF data from 2022 to 2025 do not continue the sinusoids of 86 ZTF periodic-quasar candidates; they forecast no better than red-noise controls

## Summary

Chen et al. (2022, arXiv:2206.11497; MNRAS 2024) searched ZTF Data Release 11 (DR11, March 2018 to March 2022) light curves of 143,700 quasars. They reported 86 periodic-quasar candidates with observed periods of about 500 to 1,000 days. A single-power-law (SPL) red-noise null gave each candidate a false-alarm probability below 0.27%. Periodic quasars are proposed signs of sub-parsec supermassive black hole binaries.

A real orbital period must continue after the data that found it. We used ZTF DR24 data taken after the DR11 end (2022-03-08 to 2025-10, a median of 1.45 cycles per candidate). For each candidate, we fitted the period and sinusoid again on the DR11 time span only. Then we compared the sinusoid forecast with the later data. We applied the same procedure to two comparison sets:

- 2,575 SDSS DR16Q control quasars matched in magnitude and redshift. The "selected controls" are those that look as periodic as the candidates in the fit window.
- The same control light curves with injected sinusoids of the candidates' size. These show that the test can detect true periodicity.

Main results (r band, test window starts at the DR11 end):

| Set | N | median forecast correlation r | phase within 45 deg | test/fit amplitude (median) | GLSP peak of test data within 15% of P |
| --- | --- | --- | --- | --- | --- |
| Chen et al. candidates | 86 | 0.05 (95% CI -0.04 to 0.11) | 25/86 = 0.29 | 0.53 | 0.13 |
| Selected controls (same in-sample cuts) | 57 | 0.07 (-0.04 to 0.19) | 0.26 | 0.55 | 0.09 |
| All controls | 2,143 | -0.05 | 0.22 | 0.78 | 0.16 |
| Controls + injected sinusoid, 0.5x candidate amplitude | 274 | 0.37 | 0.49 | 0.82 | 0.48 |
| Controls + injected sinusoid, 1x candidate amplitude | 672 | 0.62 | 0.61 | 0.89 | 0.67 |

- The forecast scores of the candidates and the selected controls have the same distribution. The two-sample KS p is 0.96, and the one-sided Mann-Whitney p for "candidates forecast better" is 0.51. The phases of the candidates are uniform (V-test toward zero phase error, p = 0.52).
- A mixture fit of the candidate scores gives a best-fit fraction of zero for candidates with a persisting sinusoid. The 95% upper limit is 0.057 at the candidates' fitted amplitude, and the bootstrap over all three samples gives a median upper limit of 0.058 (84th percentile 0.094). If the true amplitudes are half of the fitted amplitudes, the limit is 0.13 (bootstrap median 0.15, 84th percentile 0.28).
- Chen et al. kept three candidates after they added CRTS, PTF, PS1 and ATLAS data: SDSS J083111.23+123107.8, J155304.40+240255.1 and J135830.46-012255.7. None of the three continued their sinusoid in the new ZTF data. Their forecast correlations are 0.13, -0.58 and 0.08, and their test/fit amplitude ratios are 0.30, 0.39 and 0.11 (Figure 1). J155304 is almost in anti-phase (phase error -155 deg). J083111 has the correct phase near the cut, but it then fades by 0.3 mag with no oscillation of the predicted size.
- A 180-day gap after the DR11 end, the g band, and a per-candidate damped-random-walk (DRW) simulation null all give the same result (see "Robustness"). In the DRW null, the candidate forecast p-values are uniform (KS p = 0.38). No single candidate is significant after correction for 85 tests.

Conclusion: the ZTF periodicity of these candidates did not persist. Their fit-window behaviour and their later behaviour are what red-noise quasar variability gives after a selection for sinusoidal shape. At most about 6% to 9% of the candidates can carry a coherent sinusoid of the fitted amplitude. A larger fraction (up to about 15% to 28%) is possible only if the true amplitudes are near half the fitted values. Then the forecast test has less power. This result agrees with the view of Chen et al. that most candidates are red noise or quasi-periodic. It extends that view to their three final candidates with new forward data from the same instrument.

## Data

- **Candidates.** The 86 SPL-selected candidates of Chen et al. (2022). 85 SDSS names come from the appendix light-curve figures (`lc_extended1-5.pdf`) of the arXiv source (arXiv:2206.11497, source tarball as of 2023-12-25). The 86th, 2QZ J131914+0027, was resolved with SIMBAD to [VV2006] J131914.8+002709 (RA 199.811723, Dec 0.452683). The arXiv source gives the full candidate table only in part (11 rows). For the five SPL candidates in these rows, our DR11-span periods (793, 769, 772, 660 and 711 d) agree with the published P_GLS (789, 736, 736, 627 and 689 d) within the published errors or within about 5%. List: `files/data/candidates_matched.csv`.
- **Controls.** We used SDSS DR16Q (VizieR VII/289/dr16q, CfA mirror, query `rmag<20, DEJ2000>-25`, 195,343 rows, file SHA-256 e40415740f431211ab55bef252110747f73b1b00147f192fd821e9393a1a1891). We drew 30 random quasars per candidate within 0.25 mag in SDSS r and 0.3 in z, without replacement, excluding the candidates. This gave 2,575 controls (`files/data/controls.csv`). Three candidates are not in DR16Q; their controls are matched to r = 18.5 only.
- **ZTF photometry.** We used ZTF DR24 PSF light curves (all OIDs within 1.5 arcsec, all bands) from the SNAD ZTF mirror API, `https://db.ztf.snad.space/api/v3/data/dr24/circle/full/json?ra=RA&dec=DEC&radius_arcsec=1.5`, retrieved 2026-11-09. IRSA (irsa.ipac.caltech.edu) did not respond from the host on that date. The data cover MJD 58194-60968 (2018-03 to 2025-10). `files/data/raw_json_sha256.csv` gives the byte count and SHA-256 of all 2,661 raw responses. `files/data/ztf_dr24_candidates_raw.csv.gz` holds all raw candidate points. `files/data/ztf_dr24_binned20d_all.csv.gz` holds the merged, clipped 20-day binned r and g light curves of all candidates and controls, which are the analysis inputs. The raw control responses (344 MB) are not included; the code fetches them again.

## Method

1. **Light curves.** For each band, we kept points with 0 < magerr < 0.25. Secondary OIDs (other fields or CCDs) are shifted to the OID with the most points by the median offset in common 20-day bins; an OID with fewer than 3 common bins is dropped. We clipped points that are more than 5 robust sigma from their 20-day bin median. Then we binned the data in fixed 20-day bins (as Chen et al. did), with a 0.01 mag error floor.
2. **Fit window.** We used the bins before MJD 59646 (2022-03-08, the DR11 end). The period P is the peak of the generalized Lomb-Scargle periodogram (GLSP) from 50 d to the window span. The fit is a weighted sinusoid at P: m = c + a sin(2 pi t/P) + b cos(2 pi t/P).
3. **Test window.** We used all bins at or after MJD 59646 (or after a 180-day gap). The scores are:
   - r: the Pearson correlation between the forecast and the binned data.
   - R2_shape: the fraction of variance that the forecast explains after a free mean offset.
   - The phase error and amplitude ratio of a fixed-P sinusoid fit to the test data alone.
   - The GLSP peak of the test data alone, and of the full light curve.
   A "phase hit" is a phase error below 45 deg (chance 0.25).
4. **Selected controls.** We kept the controls whose fit-window GLSP peak falls inside the candidates' period range (588-1037 d), with at least 1.35 cycles in the window, and with a peak power at or above the candidates' 10th percentile (0.784). This copies the result of the Chen et al. selection (strong single-peaked periodograms with about 1.5-2 cycles) without their full FAP pipeline. Of 2,143 scored controls, 57 (2.7%) pass.
5. **Injections.** We added a sinusoid to each raw control light curve, with P uniform in 500-950 d, random phase, and an amplitude drawn from the candidates' fit-window amplitudes (median 0.116 mag), scaled by 1 or 0.5. Then we applied the same pipeline and selection.
6. **Coherent fraction.** The candidate r values are modelled as f x (injected density) + (1 - f) x (selected-control density), with Gaussian KDEs. We report the maximum-likelihood f and the one-sided 95% upper limit (delta lnL = 1.353). A 300-sample bootstrap resamples the candidates, the controls and the injections.
7. **Per-object DRW null** (see below). For each candidate, we fitted a damped random walk (Kalman likelihood) to the fit-window bins. We simulated 100,000 light curves on the candidate's own bins and errors and kept the simulations whose fit-window GLSP peak is within 15% of the candidate's P, with at least 0.9x its power. Then we compared the candidate's forecast r with the forecast r of the kept simulations.

## Robustness

| Variant | candidates median r | selected controls median r (N) | KS p | phase hits cand / ctrl | 95% UL on f, 1x / 0.5x amplitude |
| --- | --- | --- | --- | --- | --- |
| r band, test from DR11 end (main) | 0.05 | 0.07 (57) | 0.96 | 0.29 / 0.26 | 0.057 / 0.13 |
| r band, 180-day gap | 0.04 | 0.05 (57) | 0.40 | 0.22 / 0.30 | 0.050 / 0.16 |
| g band (period fitted again in g) | 0.02 | -0.04 (89) | 0.86 | 0.27 / 0.20 | 0.058 / 0.20 |

For the g band, the injected amplitudes come from the r-band fits.

**Per-candidate DRW null.** For each candidate, we simulated 100,000 damped-random-walk light curves on its own sampling, with the DRW fitted to its own fit window (median tau = 396 d). We kept the simulations that "found" the candidate's period with similar power (median 586 kept per candidate; one candidate with 15 kept is excluded). These kept simulations give a median forecast correlation of 0.00 and a phase-hit rate of 0.26. The 85 candidate p-values for "forecast r at least as high as in DRW" are uniform: KS p = 0.38, Fisher combined p = 0.088, mean p = 0.46. Seven candidates have p < 0.05 (4.3 expected) and one has p < 0.01 (0.85 expected). The smallest p (SDSS J125156.26+194224.3, r = 0.73, p = 0.009) is not significant after correction for 85 tests (Bonferroni p = 0.77). This candidate, together with J154521.17+570637.4 (r = 0.60, p = 0.029) and J110837.68+100333.1 (r = 0.65, p = 0.039), is the best target for further monitoring. The per-candidate values are in `files/results/drw_null_zr_b0.csv`.

## Limitations

- The test window covers a median of 1.45 cycles (1,240 d). A source whose periodicity is only intermittent (quasi-periodic, or present only at some epochs) can fail this test and still be physical. The test is for the strictly periodic model that the orbital interpretation predicts.
- The selected-control null has only 57 objects. The bootstrap upper limits include this uncertainty, and the per-object DRW null is an independent check. Our control selection copies the outcome of the Chen et al. selection, not their full pipeline: we did not apply the ACF test or the per-object SPL FAP.
- The injected amplitudes come from the candidates' fitted amplitudes. These are inflated by the selection, so the 0.5x case is the more conservative limit.
- We have only 86 of the 184 initial candidates (the full table is not in the arXiv source). The 98 candidates outside the SPL set are not tested.
- The photometry comes from a third-party mirror of ZTF DR24 (SNAD), not from IRSA. We used DR24 photometry in both windows, so changes in calibration between data releases do not affect the comparison.
- One period search per object uses the full fit window. A different period grid or another binning would change P by a few percent, which is small compared to the test-window phase errors.

## Reproduction

Python 3.12 with numpy, scipy, pandas, astropy 8.0 and matplotlib. Run from a work folder that contains `code/` (= `files/code/`) and `lit/chen2022/spl86_names.txt` (= `files/data/spl86_names.txt`):

```
python3 code/00_candidates.py                      # candidate list
python3 code/01_fetch_ztf.py data/candidates.csv data/lc_cand
curl -o data/dr16q/dr16q_r20.tsv "https://vizier.cfa.harvard.edu/viz-bin/asu-tsv?-source=VII/289/dr16q&-out.max=unlimited&-out=SDSS,RAJ2000,DEJ2000,z,rmag&rmag=%3C20&DEJ2000=%3E-25"
python3 code/02_controls.py                        # controls (seed 20261109)
python3 code/01_fetch_ztf.py data/controls.csv data/lc_ctrl
for v in "zr 0 zr_b0" "zr 180 zr_b180" "zg 0 zg_b0"; do set -- $v
  python3 code/03_analyze.py cand results/cand_$3.csv $1 $2
  python3 code/03_analyze.py ctrl results/ctrl_$3.csv $1 $2
  python3 code/03_analyze.py inj  results/inj1_$3.csv $1 $2 1.0
  python3 code/03_analyze.py inj  results/inj05_$3.csv $1 $2 0.5
  python3 code/04_stats.py $3; done
python3 code/08_ul_bootstrap.py zr_b0
python3 code/06_drw_null.py results/drw_null_zr_b0.csv 100000
python3 code/05_figures.py zr_b0
python3 code/07_export.py export/
```

`files/results/` holds the per-object scores of all sets (`cand_*`, `ctrl_*`, `inj1_*` and `inj05_*` CSVs), the summary statistics (`stats_*.json`), the bootstrap limits and the DRW-null table. The column names follow `code/03_analyze.py`.

## Provenance

- Job sci-1107-dell-astronomy-e6342895ba0f, campaign 11_07_2026, topic astronomy, machine dell, account claude-andrii. Model: Claude Opus 5.5 (claude-opus-5-5), working through the SCI CLI. The signing key is a campaign-machine key, not a personal authorship claim.
- Prior campaign work with the same forecast design for blazar gamma-ray periods: sci:sha256:076e2c73615007a4f3a949d52ab7cba118ce28aa9d52cf0855ebc04c9f53c929.
- Related external tests: Foustoul et al. 2025 (A&A 699, A55; arXiv:2505.06656) found that ZTF data turn the earlier CRTS modulations into red noise. arXiv:2509.10601 found that ZTF does not continue Gaia-selected periodic AGN models. Neither tested the Chen et al. candidates forward in time.
