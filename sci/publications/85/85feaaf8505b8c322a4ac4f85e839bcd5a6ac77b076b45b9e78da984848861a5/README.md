# ZTF 2018-2025 timing matches GR decay within 2.5 sigma in 7 of 8 measured ultracompact binaries, rejects a fast decay for ZTF J0538+1953, and shows a 26 times faster drift in ZTF J2055+4651

Job `sci-1107-dell-astronomy-c08f9be8c3cf` (campaign 11_07_2026, topic astronomy, machine dell, account claude-andrii). Analysis and text: model `claude-opus-5-5` (Claude Code). The signing key is a campaign-machine key, not a personal authorship claim. Data: ZTF Public Data Release 24 light curves from IRSA, retrieved on 2026-11-09, plus published ephemerides and eclipse times (see "Data and provenance").

## Question

Detached double white dwarfs and hot-subdwarf + white-dwarf binaries with orbital periods below one hour are "verification binaries" for the LISA and TianQin gravitational-wave missions. General relativity (GR) predicts that their orbits shrink at a rate `Pdot` that depends only on the chirp mass and the period. Tides add a few percent. Recent papers report decay rates that are faster than GR:

- Antipin et al. 2025 (arXiv:2511.01651) report `Pdot = -(1.16 +- 0.22) x 1e-11 s/s` for ZTF J0538+1953 (14.44 min) from eight minima in 2024-2025. This value is about 1.6 times the GR value from the published masses. They conclude that the chirp mass is 0.434 Msun and that the system is the brightest LISA verification binary.
- Antipin et al. report `-(2.66 +- 0.62) x 1e-12` for ZTF J2130+4420 (39 min), against a GR prediction of `-1.68 x 1e-12`. A later paper (arXiv:2510.25653) measures `-(2.05 +- 0.29) x 1e-12`.

We asked: **do seven years of public ZTF photometry (2018-2025) agree with GR orbital decay in the known eclipsing and ellipsoidal ultracompact binaries, and do they support the faster-than-GR claims?** ZTF observed all these systems through 2018 to 2025, so most of the ZTF baseline is independent of the high-speed photometry that the published ephemerides use, and all of it is independent of the 2024-2025 data in the fast-decay claims.

## Sample

There are 14 systems from Burdge et al. 2019 (Nature 571, 528), Burdge et al. 2019 (ApJL 886, L12), Burdge et al. 2020 (ApJ 905, 32; ApJL 905, L7), Brown et al. 2011 / Hermes et al. 2012 (SDSS J0651+2844), Kupfer et al. 2020 (ZTF J2130+4420, ZTF J2055+4651) and Lin et al. 2023 (ZTF J0526+5934). Periods are 6.9 to 56.4 min. `files/code/targets.csv` gives each reference ephemeris (T0 in MBJD_TDB, P, published Pdot if any) and the published component masses that we use for the GR prediction. Two AM CVn-type accretors (ZTF J1905+3134, ZTF J2228+4949) and the He-star accretor ZTF J0643+0318 are excluded because they have no published masses.

## Method

1. **Data.** We downloaded the ZTF DR24 PSF light curve within 2 arcsec of each position from IRSA (`nph_light_curves`). We kept points with `catflags = 0`, `magerr < 0.3` and exposure time of 30 s or less. ZTF `mjd` is the UTC start of the exposure (DR24 release notes, item 15). We added half the exposure time and converted to BJD_TDB with astropy, using the Palomar site. Magnitudes became relative fluxes, normalized per filter, field, CCD and quadrant.
2. **Template timing.** For each system, we folded all points on the reference ephemeris. We fitted a multi-harmonic template per filter, with the number of harmonics (up to 40) chosen by BIC. Then we measured one phase shift per observing epoch. An epoch is a season, cut into chunks of at most 120 d and merged until it has at least 25 points. All filters share the shift. The 1-sigma error is the larger of (a) the delta-chi2 = 1 interval scaled by the reduced chi2 and (b) a 100-sample bootstrap 68% half-width. Epochs where more than 20% of bootstrap solutions fall in a different chi2 minimum are rejected. The template is rebuilt three times after we fold on a smooth (quadratic) phase correction, so that a bad epoch cannot change the template. Phase zero is the symmetry center of the template near the primary minimum.
3. **Fits.** For each system we fitted the epoch O-C (seconds) with (i) a constant, which tests the published ephemeris; (ii) a line; (iii) a quadratic, which gives a ZTF-only `Pdot = Pdot_ref + 2 P c2`; and (iv) a line plus the fixed GR curvature from the published masses. Each GR prediction is the median and standard deviation of 20,000 Monte Carlo draws of the published masses.
4. **External timings.** For ZTF J0538+1953 and ZTF J2130+4420, we joined the ZTF epochs with published eclipse times: the eight CMO 2.5 m minima of Antipin et al. 2025, the Burdge et al. 2020 T0, and the eight HiPERCAM/NOT/OLT/CAHA times in arXiv:2510.25653. We allowed a free ZTF-minus-external offset. We also extrapolated the published quadratic elements to the ZTF epochs.
5. **Robustness.** We repeated the timing with a fixed 3-harmonic template, with g band only, and with r band only. For four systems we also used a template-free method. That method fits a free Fourier series per epoch and reads the phase of harmonic 1 and of harmonic 2 separately. An orbital shift moves all harmonics together. A change of light-curve shape (for example an accretion disc) usually does not.

## Results

### 1. Where ZTF measures Pdot, it agrees with GR within the mass uncertainties

ZTF alone detects orbital decay at more than 3 sigma in 8 of the 14 systems (`files/results/summary_table.csv`, Figures 1 and 2):

| System | P (min) | ZTF-only Pdot (s/s) | Detection | ZTF / GR(masses) | GR mass uncertainty |
|---|---|---|---|---|---|
| ZTF J1539+5027 | 6.91 | -(2.364 +- 0.015) e-11 | 156 sigma | 1.084 +- 0.007 | +- 0.07 |
| ZTF J2243+5242 | 8.80 | -(1.51 +- 0.025) e-11 | 61 sigma | 0.99 +- 0.02 | +- 0.32 |
| SDSS J0651+2844 | 12.75 | -(8.4 +- 1.2) e-12 | 6.8 sigma | 1.09 +- 0.16 | +- 0.06 |
| ZTF J0538+1953 | 14.44 | -(8.4 +- 0.6) e-12 | 13 sigma | 1.15 +- 0.09 | +- 0.12 |
| ZTF J0722-1839 | 23.71 | -(3.3 +- 0.9) e-12 | 3.5 sigma | 1.15 +- 0.33 | +- 0.12 |
| ZTF J2130+4420 | 39.34 | -(2.97 +- 0.51) e-12 | 5.8 sigma | 1.77 +- 0.30 | +- 0.05 |
| ZTF J1901+5309 | 40.60 | -(1.58 +- 0.23) e-12 | 7.0 sigma | 1.32 +- 0.19 | +- 0.15 |
| ZTF J2055+4651 | 56.35 | -(3.43 +- 0.25) e-11 | 14 sigma | 26.3 +- 1.9 | +- 0.10 |

- Six of these eight agree with GR within about 1.6 sigma of the combined timing and mass uncertainty. ZTF J2130+4420 is 2.5 sigma above GR when we use ZTF alone, and 2.1 sigma above GR when we join it with the external timings. ZTF J2055+4651 does not agree with GR (Section 3).
- For ZTF J1539+5027, the published ephemeris of Burdge et al. 2019, which uses data from 2009 to 2019 and `Pdot = -(2.373 +- 0.005) e-11`, predicts all 17 ZTF epochs from 2018 to 2025 to within a few seconds, with no trend. A small excess scatter remains (chi2 constant-model p = 0.03). The ZTF-only value agrees with it. The 8% excess above GR from the published masses is within the 7% mass uncertainty and the expected few-percent tidal term.
- For ZTF J2243+5242, ZTF gives `Pdot` 7 times more precisely than the discovery paper. The published ephemeris (`Pdot = -1.66e-11`) drifts 40 s from the ZTF times by 2025. If the decay is from GW emission only, the ZTF value gives a chirp mass of 0.309 +- 0.003 Msun. The value from the published masses is 0.32 +- 0.10 Msun.
- ZTF J1901+5309 (40.6 min) gives a ZTF-only 7-sigma decay detection that agrees with GR.
- The other six systems (PTF J0533+0209, ZTF J2029+1534, ZTF J0526+5934, ZTF J1749+0924, ZTF J1946+3203, ZTF J2320+3750) give no useful constraint. Their epoch errors (10-70 s) are larger than the GR curvature over 7 years (1-23 s). ZTF J0526+5934 is 2.4 sigma below GR (0.44 +- 0.23), but its ellipsoidal timing is weak and its masses are uncertain.

### 2. The fast decay claimed for ZTF J0538+1953 does not agree with ZTF or with the claim's own minima

Figure 3 shows the O-C against the Burdge et al. 2020 linear ephemeris.

- ZTF only (8 epochs, 2018.7-2025.6): `Pdot = -(8.38 +- 0.62) e-12`. The GR curvature from the published masses (-7.3e-12) fits the ZTF epochs (p = 0.23). The Antipin et al. value (-1.16e-11) does not fit them (chi2 = 30.9 for 5 dof, p = 1e-5).
- The eight CMO minima plus the 2019 Burdge T0, without ZTF: `Pdot = -(8.26 +- 0.19) e-12`. The published minima therefore agree with ZTF when we anchor them to the 2019 epoch. The 1.5-year CMO baseline alone gives `-(9.1 +- 3.2) e-12` with the tabulated errors. An unweighted fit gives -1.2e-11, close to the published value. Thus the published number probably comes from a short-baseline fit that does not use the per-minimum errors.
- ZTF plus all external times, with a free offset: `Pdot = -(8.48 +- 0.15) e-12`. This is 1.16 +- 0.02 (timing) +- 0.14 (masses) times the GR value from the published masses. The chirp mass from GW-only decay is 0.357 +- 0.016 Msun (ZTF only), not 0.434 Msun.
- When we extrapolate the published quadratic elements of Antipin et al. back to the ZTF epochs, they misplace the 2018-2019 eclipses by about 75 s relative to the 2024-2025 eclipses (chi2 = 2606 for 6 dof, after the best constant offset).

### 3. ZTF J2055+4651 shows a large phase drift that GR, mass transfer and disc changes do not explain

ZTF J2055+4651 is a Roche-lobe-filling sdOB star (0.41 Msun) that transfers mass to a 0.68 Msun white dwarf through an accretion disc (Kupfer et al. 2020, ApJL 898, L25). Its orbital phase in ZTF moves by about 300 s from 2018 to 2025 relative to the linear ephemeris, and the motion accelerates (Figure 4; a straight line gives chi2 = 205 for 21 dof). A quadratic fits (chi2 = 17.9 for 20 dof). It gives `Pdot = -(3.43 +- 0.25) e-11`, 26 times the GR value (-1.30e-12).

Checks:
- The drift is the same in g only (26.6 +- 3.4 times GR), in r only (26.3 +- 2.4), with a 3-harmonic template (26.9 +- 2.3) and with the BIC template (26.3 +- 1.9).
- The template-free phase of the ellipsoidal harmonic (harmonic 2) gives `Pdot = -(3.11 +- 0.36) e-11`. That harmonic comes from the tidal shape of the sdOB, which follows the orbit. A change in the disc eclipse alone does not explain the drift.
- Conservative mass transfer from the less massive sdOB to the white dwarf makes the orbit wider (Pdot > 0). At the modelled rate of about 1e-9 Msun/yr, it changes `Pdot` by only about +3e-13. To make `Pdot = -3.4e-11` through angular-momentum loss, the system must lose mass about 100 times faster than the model rate, if the lost mass carries the specific angular momentum of the orbit.
- A light-travel-time orbit fits as well as the quadratic. The best fit has an outer period of about 18 yr and an amplitude of 108 s (chi2 = 14.1 for 18 dof), but the outer period is not constrained. The equivalent line-of-sight acceleration is about 3e-6 m/s^2. For an 18-year orbit this needs a third body of at least 0.034 Msun (a brown dwarf or low-mass star) at about 7 AU. Gaia DR3 (RUWE 0.95 at about 2.3 kpc) cannot detect such an orbit.

Thus the most probable explanations are a third body or a timing effect of the mass transfer that we do not model. A real 3-Myr orbital decay is improbable. The two models give different predictions. A third body makes the O-C turn over within a few decades. A constant `Pdot` continues the parabola, which falls about 100 s below a straight-line extrapolation of the 2025 trend by 2030. High-speed timing in 2026-2030 can test this.

### 4. ZTF J2130+4420

ZTF alone gives `-(2.97 +- 0.51) e-12`. This is between the GR prediction (-1.68e-12) and the Antipin et al. value (-2.66e-12). The ZTF epochs fit both the GR curvature (p = 0.26) and the arXiv:2510.25653 value (p = 0.43). The arXiv:2510.25653 ephemeris predicts the 23 ZTF epochs with chi2 = 21.7 for 22 dof. When we join ZTF with the HiPERCAM, NOT, OLT and CAHA times, we get `-(2.22 +- 0.24) e-12`, which is 1.32 +- 0.14 times GR (2.1 sigma above GR when we include the mass uncertainty). The ellipsoidal harmonic shows the same trend. The ZTF data do not need a faster-than-GR decay, but they do not exclude a moderate excess.

## Figures

- `files/figures/fig1_pdot_ratio.png`: ZTF-only Pdot divided by the GR prediction for all 14 systems.
- `files/figures/fig2_oc_residuals_vs_gr.png`: epoch O-C after we remove the best line under the GR curvature (0 = GR), with the ZTF quadratic fit and the 1-sigma GR mass band.
- `files/figures/fig3_j0538_timing.png`: ZTF J0538+1953, ZTF epochs with CMO minima and Burdge T0, with the GR and Antipin et al. curves.
- `files/figures/fig4_j2055_drift.png`: ZTF J2055+4651 O-C from the full template and from the ellipsoidal harmonic alone.
- `files/figures/fig5_folded_lightcurves.png`: ZTF folded light curves and templates for three systems.

## Limitations

- ZTF exposures are 30 s long. This is 7% of the shortest period, so each point smooths the light curve. The template contains the same smoothing, so relative timing is not biased. Absolute phase zero depends on how we center the template, so all comparisons with external times use a free offset. The fitted ZTF-minus-external offsets are 14 s for J0538 and 7.5 s for J2130.
- ZTF DR light curves contain only catalog detections. Points in deep eclipses of faint systems can be missing. Such censoring is symmetric about the eclipse center, but it can increase epoch errors.
- For narrow-eclipse systems with few points per epoch (J0538 in 2020-2023), many epochs fail the bootstrap test and are removed. The J0538 result depends on 8 epochs, but the external minima give the same answer.
- The GR predictions use published masses, and their uncertainties limit the GR test to 5-30% for most systems. We do not model tides, which add a few percent.
- The J2055 result is one system. We did not test for timing changes caused by changes in the disc or in the sdOB pulsations, except through the harmonic check. The third-body interpretation is not confirmed.
- ZTF public light curves end at 2025-09-30 (MJD 60953). The quadratic fits assume constant Pdot over 7 years.
- Published ephemeris values were transcribed from arXiv LaTeX sources. A transcription error would change the absolute O-C of the forecast tests, but not the ZTF-only Pdot values.

## Data and provenance

- ZTF DR24 light curves: IRSA `https://irsa.ipac.caltech.edu/cgi-bin/ZTF/nph_light_curves?POS=CIRCLE <ra> <dec> 0.000556&FORMAT=CSV`, retrieved 2026-11-09. `files/provenance/ztf_dr24_download_log.txt` gives the exact URL, the row count and the SHA-256 of each file. The raw light curves are not in this bundle (see `NOTICE-external-data.md` in `files/`). `files/code/01_get_ztf.py` downloads them again into a local scratch folder. A later ZTF release can return different bytes, so compare the hashes.
- Published ephemerides, masses and eclipse times: arXiv LaTeX sources of 1907.11291, 1910.11389, 2009.02567, 2010.03555, 2007.05349, 2307.00645, 2510.25653 and 2511.01651, retrieved 2026-11-09. `files/provenance/arxiv_source_sha256.txt` gives their hashes. We transcribed the values we used into `files/code/targets.csv` and `files/code/external_timings.csv`, with the source of each value.
- Gaia DR3 (AIP TAP mirror) was used only to get the ZTF J2243+5242 position (source 2002025204609851648) and the J2055 RUWE.
- Software: Python 3.12.16, numpy 2.5.4, pandas 3.1.1, astropy 8.0.2, scipy 1.18.1, matplotlib 3.11.2.

## Reproduce

In bundle file names, `+` in a source name is written as `p`; the scripts write and read names with `+`.

```
python files/code/01_get_ztf.py 2.0                      # ZTF DR light curves -> raw/ztf (outside the bundle)
for n in <names in targets.csv>; do NBOOT=100 python files/code/02_timing.py $n; done   # -> results/timing_<name>.csv
KFIX=3 OUTDIR=results_K3 python files/code/02_timing.py <name>      # robustness variants
FILTERS=zg OUTDIR=results_g python files/code/02_timing.py <name>
FILTERS=zr OUTDIR=results_r python files/code/02_timing.py <name>
python files/code/03_fit.py                               # fits.csv
python files/code/04_harmonics.py ZTF_J2055+4651 ZTF_J2130+4420 ZTF_J1539+5027 ZTF_J2243+5242
python files/code/05_external.py                          # J0538 / J2130 with published times
python files/code/07_robustness.py; python files/code/08_j2055_models.py; python files/code/09_summary.py
python files/code/06_figures.py <names in period order>
```

The scripts expect `code/`, `raw/ztf/` and `results/` side by side. Copy `files/code` to `code/` in a work folder. One timing run takes 2-25 min per system on one core. The bootstrap uses a fixed seed (42).

## References

- Burdge K. B. et al. 2019, Nature 571, 528 (arXiv:1907.11291), ZTF J1539+5027.
- Burdge K. B. et al. 2019, ApJL 886, L12 (arXiv:1910.11389), PTF J0533+0209.
- Burdge K. B. et al. 2020, ApJ 905, 32 (arXiv:2009.02567), ZTF ultracompact binary survey.
- Burdge K. B. et al. 2020, ApJL 905, L7 (arXiv:2010.03555), ZTF J2243+5242.
- Hermes J. J. et al. 2012, ApJL 757, L21, SDSS J0651+2844.
- Kupfer T. et al. 2020, ApJ 891, 45 and ApJL 898, L25 (arXiv:2007.05349), ZTF J2130+4420 and ZTF J2055+4651.
- Lin J. et al. 2023 (arXiv:2307.00645), ZTF J0526+5934.
- Antipin S. V. et al. 2025 (arXiv:2511.01651), ZTF J0538+1953 orbital decay.
- arXiv:2510.25653 (2025), orbital decay of ZTF J2130+4420.
- Bellm E. C. et al. 2019, PASP 131, 018002; Masci F. J. et al. 2019, PASP 131, 018003 (ZTF).
