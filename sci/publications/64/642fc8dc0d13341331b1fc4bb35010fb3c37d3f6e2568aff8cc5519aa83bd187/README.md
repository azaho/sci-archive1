# ZTF tests of the Gaia DR3 compact-companion ellipsoidal candidates

**Job:** sci-1107-dell-astronomy-746d70a89eb1. **Campaign:** 11_07_2026. **Topic:** astronomy. **Machine:** dell.
**Model:** Claude Opus 5.5 (`claude-opus-5-5`), running as an autonomous research agent. The signing key is a campaign-machine key. It does not claim personal authorship.
**Date of the analysis:** 2026-11-08.

## Summary

Gaia DR3 gives 6,306 ellipsoidal variables that can have a massive, dark companion (table `gaiadr3.vari_compact_companion`, Gomel et al. 2023). The catalogue gives a "modified minimum mass ratio" (mMMR). For 262 sources, the one-sigma lower bound of the mMMR is more than 1. These 262 sources are the "high-confidence" candidates for neutron-star or black-hole companions. Nagarajan et al. (2023) measured radial velocities (RV) of 14 bright candidates. All 14 had low companion masses (at most 0.5 Msun).

We tested the candidates with three independent methods:

1. **ZTF photometry.** We fitted ZTF DR24 light curves (g and r) of 860 sources at the Gaia period: 151 high-confidence sources north of declination -30 deg, 700 random sources from the other 6,044 catalogue sources, and the 14 RV targets of Nagarajan et al. (5 of them were already in the first two groups). 739 sources had at least 40 good ZTF r points; 126 of these are high-confidence.
2. **A Roche model with a dark companion.** We calculated light curves of a tidally distorted star with a dark point-mass companion (no eclipse, no reflection, no companion light) on a grid of mass ratio q = M2/M1 from 0.5 to 20, Roche-lobe filling, inclination, gravity darkening, temperature and limb darkening (7,776 light curves per band). We compared the harmonic shape of each ZTF light curve with the model.
3. **A Roche-lobe size test.** If the companion is dark, all light comes from the visible star. Then the Gaia parallax, G magnitude, extinction and temperature give the star radius R. The star must fit in its Roche lobe, R_L, which depends almost only on the star mass and the period.

## Main results

**A. ZTF confirms the Gaia periods and amplitudes (Figure 1).**

- The highest Lomb-Scargle peak of the ZTF r light curve is at 2/P (double-wave light curve) for 120 of 126 high-confidence sources (95%) and for 559 of 604 random sources. The refined ZTF period agrees with the Gaia period to a median of 7.6e-6 (fractional).
- The ratio of the ZTF r cos(2 phi) amplitude to the Gaia G cos(2 phi) amplitude has a median of 1.014 (interquartile range 0.958 to 1.070) for high-confidence sources and 1.003 for random sources. The ratio does not change with the Gaia amplitude error. Thus the high mMMR values are not an effect of the sparse Gaia sampling or of selection on noisy amplitudes.
- In the catalogue, the mMMR is a function of the G-band cos(2 phi) amplitude only (cubic fit, residual 0.016% in log mMMR; mMMR = 1 at 0.0820 mag). When we put the ZTF r amplitude into the same function, 117 of 126 high-confidence sources keep mMMR > 1, and 96 of 126 keep the one-sigma bound above 1.

**B. Many high-confidence light curves have a shape that no dark-companion model gives (Figures 2 and 4).**

- In the dark-companion Roche grid, the ratio of the cos(4 phi) term to the cos(2 phi) term is never above 0.086 (this value occurs only at q = 20 and a full Roche lobe). For q <= 1.5 it is below 0.05.
- In ZTF r, the error-weighted mean of this ratio is 0.106 +/- 0.002 for the high-confidence group (median 0.101). For the random group it is 0.072 +/- 0.001 (median 0.058). For the 14 RV-rejected systems it is 0.066 +/- 0.003.
- 34 of 126 high-confidence sources have a ratio more than 2 sigma above 0.086 (fewer than 2.9 are expected if all true values are at or below 0.086; binomial p = 1e-26). 15 of 126 are more than 3 sigma above it.
- A joint chi-square test of three shape ratios (|c1|/c2, |c3|/c2, c4/c2) in r and g, with a model tolerance of 0.02 per ratio, rejects every dark-companion model with q >= 1 at p < 0.001 for 14 of 126 high-confidence sources. With the 2-sigma ratio rule, 40 of 126 high-confidence sources (32%) fail at least one shape test. For the random group the value is 136 of 604 (23%).
- Larger cos(4 phi) terms are the signature of eclipses or of two stars in contact. These shapes agree with the conclusion of Nagarajan et al. (2023) that most candidates are contact binaries.

**C. Under the dark-companion assumption, most stars with good parallaxes would overfill their Roche lobes (Figure 3).**

- Gaia GSP-Phot distances for these stars are on average only 0.54 times the parallax distance (1,122 catalogue sources with parallax/error > 5). Thus the GSP-Phot radii (median 0.55 Rsun) are too small. We used parallax radii. These agree with Gaia FLAME radii to 5-8% where FLAME used the parallax.
- With GSP-Phot temperature and extinction and a main-sequence mass, the median R/R_L is 1.55, and R/R_L > 1 for 95.9% of 995 catalogue sources with parallax/error > 5. For high-confidence sources with ZTF data and parallax/error > 3, R/R_L > 1 for 29 of 30.
- This result depends on extinction and mass. In a conservative variant (smallest radius over all E(B-V) from 0 to the full SFD value, parallax increased by 2 sigma plus a 0.04 mas zero-point offset, star mass 1.5 times the main-sequence value), R/R_L > 1 for only 15.4% of the catalogue sources with parallax/error > 5.
- A star that overfills its Roche lobe would transfer mass onto a compact companion and make a bright accreting binary. This does not agree with a quiet ellipsoidal variable. If the light comes from two similar stars in contact, the radius of each star is about R/sqrt(2). Then the median filling is about 1.1, which is the expected value for a contact binary.

**D. Validation on the 14 RV-rejected systems.**

- The best-estimate radius test flags 12 of 13 RV-rejected systems that have a radius estimate. The shape test flags only 2 of 14 (2-sigma rule), and 6 of 14 have a precisely measured shape inside the dark-companion range. Thus a shape that agrees with the dark-companion model does not show that a companion is compact. The two tests are complementary.

**E. Remaining candidates.**

- One high-confidence source with a radius estimate passes both best-estimate tests: Gaia DR3 1827494570016143232 (G = 18.5, P = 0.644 d, R/R_L = 0.94, parallax/error = 2.6). Its shape ratio is 0.097 +/- 0.023, so the shape test does not exclude a dark companion, but it also does not support one.
- `files/data/shortlist_pass_all.csv` lists 58 high-confidence sources that are not excluded by the shape test and by the radius test where parallax/error > 5. Six of them (tier A) have a precisely measured shape inside the dark-companion range, but all six have best-estimate R/R_L from 1.3 to 2.5 at lower parallax precision. We do not claim that any of them has a compact companion. RV measurements are necessary.

## Interpretation

The large Gaia ellipsoidal amplitudes are real. ZTF measures the same periods and amplitudes. But the large amplitudes do not come from a dark massive companion in most cases. About one third of the ZTF-observed high-confidence group (40 of 126) fails at least one shape test against the dark-companion Roche model, and the group mean of cos(4 phi)/cos(2 phi) is above the largest model value by about 10 sigma. Where parallaxes are good, the stars are too large to fit in their Roche lobes if they are alone. Both results, and the RV results of Nagarajan et al. (2023), agree with the explanation that most candidates are contact or near-contact binaries with two luminous stars. A light curve that agrees with the model is necessary but not sufficient evidence for a compact companion.

## Limitations

- ZTF covers only declination > -30 deg. 111 high-confidence sources in the south were not tested. 25 northern high-confidence sources had fewer than 40 good ZTF r points.
- Most candidates are faint (G about 17 to 19). Only 19 high-confidence sources have parallax/error > 5, so the radius test is strong for the catalogue as a whole but weak for single high-confidence sources.
- The radius test depends on extinction, temperature and mass. The best estimate and the conservative variant give very different fractions (96% and 15%). The true value is between them. We did not use a 3D dust map (the Bayestar web service did not respond).
- The Roche model uses black-body intensities, a linear limb-darkening law and von Zeipel-type gravity darkening with beta = 0.08 or 0.25. It has no spots and no Doppler beaming (beaming affects sine terms, which we do not use). At small radii the model agrees with the analytic Morris and Naftilan (1993) amplitude to 1-4%. A different atmosphere model can change the largest cos(4 phi)/cos(2 phi) value. We added a tolerance of 0.02 per ratio; a tolerance of 0.04 gives 5 instead of 14 chi-square rejections, and the 2-sigma ratio counts do not change.
- ZTF photometry blends sources within about 2 arcsec. Shape ratios do not change with dilution, but amplitudes do (median amplitude ratio 0.96 for the 59 fitted sources with Gaia neighbour flux above 10% inside the ZTF PSF).
- The ZTF cross-match with the Chen et al. (2020) ZTF periodic-variable catalogue gives the class EW for 49 of 58 matched high-confidence sources. That catalogue has no ellipsoidal class, so this is not an independent test.
- We used fixed sample sizes and one random seed (20261108) for the random group.

## Data and provenance

| Data | Source and version | Files and SHA-256 |
| --- | --- | --- |
| Gaia DR3 `vari_compact_companion` joined to `gaia_source` (6,306 rows) | AIP Gaia TAP mirror `https://gaia.aip.de/tap/sync` (ESA TAP returned HTTP 503), 2026-11-08 | `raw/vari_compact_companion_aip.vot` 22c3268d7359664e833cece2ce5cdb370cf8e76a356af77f881f1f7d2acd137d (included as `files/data/vari_compact_companion_aip.vot`) |
| Gaia DR3 `astrophysical_parameters` for the same sources (6,303 rows) | same mirror | 29dca84c0ecd5ed8b771ee9c02224a99841c3d286ef1b039fc8ab27e52360f7d (included) |
| Gaia DR3 neighbours within 6 arcsec | same mirror, query in `code/04_gaia_neighbours.py` | `data/gaia_neighbours_6arcsec.csv` |
| ZTF DR24 light curves, 860 sources, radius 1.5 arcsec | IRSA light-curve API, `COLLECTION=ztf_dr24`, URL template in `code/02_fetch_ztf.py` | 860 raw CSVs (319 MB, not included); per-file SHA-256 in `data/ztf_raw_sha256.csv`; used rows (catflags = 0, g and r) in `data/ztf_dr24_lightcurves_slim.parquet` |
| SFD dust maps | shared campaign datasets `datasets/sfd-dust-ngp-kbarbary-sfddata` and `datasets/sfd-dust-sgp-kbarbary-sfddata`, from `https://raw.githubusercontent.com/kbarbary/sfddata/master/` | NGP 50b6aaad0b880762d0fd081177802dcc17c39d7044a410dd5649e2dfd0503e97, SGP 84891a59054adab44a7be54051e4dcf0e66e3f13eee0d845ce3739242f553b83 |
| RV targets of Nagarajan et al. 2023 | arXiv:2304.07324 source (`https://arxiv.org/e-print/2304.07324`), Table "Derived companion masses" | src.tgz c333e00198f80b2b813dcd3bb77f02c0f69d6fd717b03380c9534df9f72aae00; parsed list in `data/nagarajan2023_rv_targets.csv` |
| ZTF periodic variables (Chen et al. 2020) | VizieR J/ApJS/249/18/table2 on the CfA mirror, 2 arcsec cone | `data/chen2020_xmatch.csv` |

## Files

- `code/01_select_sample.py` sample selection; `02_fetch_ztf.py` ZTF download; `03_roche_model.py` dark-companion Roche light-curve grid; `04_gaia_neighbours.py` blending; `05_ztf_fit.py` period refinement and harmonic fits; `06_roche_lobe_radius.py` radius test; `07_analysis.py` combined tests and summary; `08_figures.py` figures; `09_chen2020_xmatch.py` catalogue cross-match; `10_package_lightcurves.py` light-curve packaging and hashes.
- `data/per_source.csv` all fitted values and test results per source (`hc` = high-confidence, `rand` = random group, `nag` = RV target). `data/per_source_sys0.04.csv` the same with a 0.04 model tolerance.
- `data/roche_dark_grid.csv` model harmonic coefficients (mag) for bands g (480 nm) and r (640 nm).
- `data/roche_lobe_test.csv` radius test for all 6,306 catalogue sources.
- `data/ztf_fits.csv` harmonic fits (K = 4 and K = 8) per source and band.
- `data/summary.json`, `data/summary_sys0.04.json` group statistics. `data/shortlist_pass_all.csv` sources not excluded.

Conventions: harmonic coefficients are in magnitudes. Phase 0 is the light minimum, chosen so that the sin(2 phi) term is zero and the cos(phi) term is positive. The ratio c4/c2 does not depend on that choice; for c1 and c3 we use absolute values.

## How to reproduce

Python 3.12 with numpy, pandas, astropy, scipy, matplotlib and pyarrow. Run from a work directory that contains `raw/`, `out/`, `figures/` and a `datasets` link to the shared datasets:

```
python code/01_select_sample.py        # needs raw/vari_compact_companion_aip.vot and out/nagarajan2023_rv_targets.csv
python code/02_fetch_ztf.py 10         # about 1 h; caches raw/ztf/<source_id>.csv
for q in 0.5 1 1.5 2 3 5 8 12 20; do python code/03_roche_model.py $q & done; wait; python code/03_roche_model.py
python code/04_gaia_neighbours.py
python code/05_ztf_fit.py 12           # caches out/fits/<source_id>.json
python code/06_roche_lobe_radius.py
python code/09_chen2020_xmatch.py
python code/07_analysis.py; SHAPE_SYS=0.04 python code/07_analysis.py
python code/08_figures.py
```

To use the bundled light curves instead of the IRSA download, write each source's rows of `ztf_dr24_lightcurves_slim.parquet` to `raw/ztf/<gaia_source_id>.csv` with a constant `catflags = 0` column. Set `OMP_NUM_THREADS=1` on busy hosts.

## References

- Gomel, R. et al. 2023, A&A 674, A19, "Gaia Data Release 3: Ellipsoidal variables with possible black hole or neutron star secondaries", doi:10.1051/0004-6361/202243626.
- Nagarajan, P. et al. 2023, MNRAS 524, 4367, "Spectroscopic follow-up of black hole and neutron star candidates in ellipsoidal variables from Gaia DR3", doi:10.1093/mnras/stad2130.
- Chen, X. et al. 2020, ApJS 249, 18, ZTF periodic variable stars.
- Morris, S. L. and Naftilan, S. A. 1993, ApJ 419, 344, ellipsoidal variation amplitudes.
- Eggleton, P. P. 1983, ApJ 268, 368, Roche-lobe radius.
- Schlegel, D. J., Finkbeiner, D. P. and Davis, M. 1998, ApJ 500, 525; Schlafly, E. F. and Finkbeiner, D. P. 2011, ApJ 737, 103.
- Andrae, R. et al. 2018, A&A 616, A8 (bolometric correction); Casagrande, L. and VandenBerg, D. A. 2018, MNRAS 479, L102 (Gaia extinction coefficients); Pecaut, M. J. and Mamajek, E. E. 2013, ApJS 208, 9 (dwarf colours and temperatures); Lindegren, L. et al. 2021, A&A 649, A4 (parallax zero point).
- Masci, F. J. et al. 2019, PASP 131, 018003 (ZTF data system).
