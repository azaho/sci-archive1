# For 45 contact binaries with strong TESS 2018-2026 period curvature, earlier ASAS-SN and SuperWASP timings show only about 40 percent of the predicted offset; 403 systems show no V1309 Sco-like decay

## Summary

We measured eclipse timing (O-C) of contact binaries in the TESS 2-min data from 2018 to 2026. Then we tested if the TESS period changes continue backwards in time. We used independent ASAS-SN (2012-2025) and SuperWASP (2004-2008) photometry for this test.

- **Sample.** We used 749 contact binaries from the TESS eclipsing-binary catalog of Prša et al. (2022): morphology at least 0.6, period 0.2-1.0 d, 2-min data in sectors 1-26 and in sectors 56 or later. We used 5,001 SPOC light curves. After quality cuts, 484 binaries have 4 or more good sectors. The vetted sample has 403 binaries (amplitude at least 5 percent, span at least 3 years, median span 5.0 years, median 7 sectors).
- **TESS result.** A quadratic O-C term is significant at 5 sigma or more in 118 of 403 binaries (68 period increases, 50 decreases). The median |dP/dt| of these 118 binaries is 0.068 s/yr (7.9e-7 d/yr). The median 1-sigma error for all binaries is 0.010 s/yr.
- **Main result: the TESS curvature does not continue as a constant dP/dt.** For a constant dP/dt, the TESS quadratic ephemeris must predict the earlier survey timings. We define kappa = (observed - TESS linear) / (TESS quadratic - TESS linear). A constant dP/dt gives kappa = 1. A constant period gives kappa = 0. For binaries with strong TESS curvature (|z| >= 5), the median kappa is 0.42 for ASAS-SN V seasons about 4 years before TESS (45 binaries, interquartile range 0.09-0.95). It is 0.34 for SuperWASP seasons about 12 years before TESS (22 binaries, interquartile range 0.06-0.58). Only 33 percent (ASAS-SN) and 5 percent (SuperWASP) of these binaries agree with kappa = 1 at 3 sigma (Figure 2a).
- **Decade-mean period change is smaller.** For 45 binaries with strong TESS curvature, we compared the mean dP/dt between the pre-TESS survey epoch and the TESS epoch (gap 5-13 years) with the TESS-window dP/dt. The median ratio is 0.35 (interquartile range -0.03 to 0.87). The sign agrees in 73 percent. The median |dP/dt| is 0.014 s/yr for the decade mean and 0.056 s/yr in the TESS window (Figure 2b).
- **Literature check.** For 17 binaries with a published long-baseline dP/dt (compilation of Latković et al. 2021) and a TESS term at 3 sigma or more, the sign agrees in 11. The TESS value is larger in 76 percent (median 0.052 against 0.023 s/yr).
- **No merger-like decay.** Apart from one rejected case (below), no vetted binary has a significant (3 sigma or more) TESS-window decrease faster than 0.44 s/yr (5e-6 d/yr; V405 Dra, whose O-C is not a parabola). In the quadratic-adequate set the fastest is 0.32 s/yr (SZ Hor). This is more than 100 times slower than V1309 Sco in its last years before the 2008 merger (about -50 s/yr). The fastest decreases are at the low end of the range of the Galactic-bulge merger candidates of Hong et al. (2024; -0.26 to -1.13 s/yr). They do not continue smoothly. For example, V2363 Cyg (TIC 406951407) has a constant period from 2007 to 2014 and an abrupt period change after 2016 (Figure 1). One apparent extreme decrease (TIC 307783750, -5.3 s/yr) is not real: its fitted amplitude scale changes from 0.5 to 2.2 between sectors, and 8 of 14 sectors fail the quality cuts. We think that spots or a blended star cause it.
- **Interpretation.** Most period changes that TESS measures over 5-7 years are parts of longer variations (for example light-travel time in a triple system, or magnetic cycles). They are not secular mass-transfer or angular-momentum-loss rates. Short-baseline dP/dt values of contact binaries must not be used as secular rates or as merger evidence without a longer timing baseline.

## Question

Do the orbital-period changes that TESS measures in contact binaries over 2018-2026 continue as constant dP/dt when we look at independent earlier data? Does any TESS contact binary show a fast, steady period decrease like the merger progenitor V1309 Sco?

## Data

| Data | Source | Version / date | Use |
| --- | --- | --- | --- |
| TESS EB catalog | Prša et al. 2022, ApJS 258, 16 (VizieR J/ApJS/258/16); copy in SCI bundle 0f548fc8... | retrieved 2026-11-08 | targets, period P, epoch, morphology |
| TESS SPOC 2-min light curves | MAST, bulk scripts `tesscurl_sector_N_lc.sh`, sectors 1-107 | retrieved 2026-11-09 | PDCSAP flux, QUALITY, CROWDSAP |
| ASAS-SN Sky Patrol v2 | pyasassn client (`SkyPatrolClient.cone_search`, master_list, 5.4 arcsec) | deployment 0.6.20, retrieved 2026-11-09; data to 2025-06 | V (2012-2018) and g (2017-2025) photometry |
| SuperWASP DR1 | wasp.cerit-sc.cz mirror, nearest object within 15 arcsec, CSV | retrieved 2026-11-09 | 2004-2008 photometry |
| W UMa compilation | Latković, Čeki & Lazarević 2021, ApJS 254, 10 (VizieR J/ApJS/254/10, CfA mirror) | retrieved 2026-11-09 | published dP/dt (aggregate comparison only) |
| SIMBAD | Harvard TAP mirror | 2026-11-09 | star names |

Files of external data are not in this bundle. `files/provenance/` gives the exact file lists and SHA-256 hashes: `tess_lc_files.csv` (5,003 requested, 5,001 received; MAST URL of each file), `tess_lc_sha256.txt`, `asassn_skypatrol_csv_sha256.txt` (748 targets; 705 with data), `superwasp_csv_sha256.txt` and `superwasp_ids.txt` (363 matches), and `external_catalog_sha256.txt`. `files/code/fetch_external.sh` downloads all inputs again into a separate work folder. See `files/EXTERNAL_DATA_NOTICE.md` for sources, terms and attribution. No shared campaign dataset was created or changed.

## Method

1. **Targets** (`select_targets.py`). Prša et al. (2022) entries with `m_TIC` = 1, Morph >= 0.6 and 0.2 <= P <= 1.0 d: 999 binaries. We kept 749 binaries with 2-min data in a sector <= 26 and in a sector >= 56. For binaries with more than 14 sectors, we used 14 sectors at equal spacing.
2. **TESS timing** (`measure.py`). PDCSAP flux with QUALITY = 0, each sector divided by its median. We fit a 16-harmonic Fourier template in orbital phase to all sectors of a binary (3 iterations). Per sector we fit a time shift dt, an amplitude scale s, an offset and a linear trend (Gauss-Newton with 5-sigma clipping). The start value comes from a phase cross-correlation within +-P/4. The error is the larger of the formal error and the scatter of 1-day blocks divided by sqrt(number of blocks). Note: for the first 249 binaries, the start value came from a brute-force grid; we then changed to the cross-correlation for speed. The Gauss-Newton fit then gives the same solution.
3. **TESS O-C fits** (`oc_fit.py`). Quality cuts per sector: 0.7 < s < 1.3, more than 3,000 points, residual rms < 0.5 x amplitude. The two minima of a contact binary are similar, so dt is defined only modulo P/2. We estimated a period correction from sector pairs less than 60 d apart, unwrapped the shifts modulo P/2 around this slope, and then re-wrapped 3 times against a quadratic fit. We added a timing floor of 10.5 s in quadrature. With this floor, the median normalized difference of 1,254 consecutive-sector pairs is 0.6745 (Gaussian value). We fit O-C = a + b x + c x^2 (x in days) with weights; dP/dt = 2 c P. We scaled the error of c by sqrt(reduced chi2) when this is more than 1.
4. **Survey timing** (`survey_timing.py`). For each observing season (gap > 60 d) of ASAS-SN V, ASAS-SN g and SuperWASP, we fit the TESS template of the binary with a free shift, amplitude scale and offset. The shift comes from a full-period grid and Gauss-Newton refinement. The error is the larger of a 100-draw night bootstrap and the formal error. We converted the times from HJD(UTC) to BJD(TDB).
5. **Time calibration** (`analyze.py`, Figure 4). ASAS-SN g seasons inside the TESS span are a median 274 +- 8 s earlier than the TESS model (496 seasons). A regression of these residuals on the heliocentric light-time term gives a slope of -0.25 +- 0.03. A wrong time system (JD instead of HJD) gives a slope of +-1, so the time system is correct. The small slope shows a seasonal term of up to about 2 minutes that we did not model. We treat the offset as a constant error of the ASAS-SN time stamps and subtract it. V minus g in the same season is +0 s (53 pairs), so we used the same offset for V. We did not apply an offset to SuperWASP. We added a systematic term of 98 s in quadrature to all survey seasons. With this term, the in-sample g residuals have median |z| = 0.6745.
6. **Backcast test** (`analyze.py`, `summaries.py`). Rules fixed before we looked at the outcome. Sample: amplitude >= 0.05, >= 4 sectors, span >= 3 years, reduced chi2 of the TESS quadratic < 10 (298 binaries). Groups: "curved" |z_c| >= 5, "mid" 2-5, "flat" < 2. Seasons: error < 0.003 d, 0.5 < s < 2, end more than 180 d before the first TESS sector. A season is "informative" when the quadratic and linear predictions differ by more than 3 sigma and by less than P/4 (otherwise the P/2 ambiguity hides the difference). Residuals are modulo P/2.
7. **Long baseline** (`longbase.py`, `epoch_periods.py`). We unwrapped the ASAS-SN seasons backwards in time from TESS. Each season goes on the branch nearest to a local fit of the later points. We removed seasons more than P/8 from the prediction. We placed the SuperWASP block across the 2008-2014 gap with a trapezoid rule from the local periods on both sides of the gap. For binaries with at least 3 pre-TESS seasons over at least 3 years (144 binaries), we compared the linear period of the pre-TESS seasons with the TESS linear period. The difference divided by the time between the two epochs is the decade-mean dP/dt.
8. **Literature** (`literature_compare.py`). Match within 10 arcsec and |dP| < 0.001 d to the Latković et al. (2021) compilation; only aggregate numbers are reported.

## Results

### TESS window (2018-2026)

| Quantity | Vetted sample (403) | Quadratic adequate (298) |
| --- | --- | --- |
| Quadratic term at >= 5 sigma | 118 | 89 |
| Period increase / decrease | 68 / 50 | 52 / 37 (binomial p = 0.14) |
| Median |dP/dt| of these (s/yr) | 0.068 | 0.058 |
| 90th percentile |dP/dt| (s/yr) | 0.24 | 0.16 |
| Median 1-sigma error of dP/dt (s/yr) | 0.010 | 0.007 |

Figure 3 shows the distribution and the 3-sigma limits for binaries without a significant term. All per-sector values are in `files/data/oc_sectors.csv`, and the fits are in `oc_fits.csv`.

### Backcast of the TESS ephemerides

| Group / survey | Binaries | Median years before TESS | Median kappa | Interquartile range | Agree with kappa = 1 (3 sigma) | kappa < 0.5 |
| --- | --- | --- | --- | --- | --- | --- |
| curved, ASAS-SN V | 45 | 4.0 | 0.42 | 0.09 - 0.95 | 33 % | 60 % |
| curved, SuperWASP | 22 | 11.9 | 0.34 | 0.06 - 0.58 | 5 % | 59 % |
| mid, ASAS-SN V | 8 | 4.4 | 0.25 | -0.22 - 0.78 | 25 % | 63 % |
| mid, SuperWASP | 20 | 12.3 | 0.04 | -0.14 - 0.69 | 10 % | 70 % |

The median kappa error per binary is 0.04-0.12, so the spread is not measurement noise. For curved binaries the quadratic prediction is closer than the linear one in 43 percent of informative ASAS-SN V seasons and in 35 percent of SuperWASP seasons. For the "flat" group, the TESS linear ephemeris agrees with 72 percent of ASAS-SN V seasons (about 4 years back) but with only 27 percent of SuperWASP seasons (about 13 years back). Thus period changes too slow for TESS to detect still accumulate over a decade.

### Decade-mean against TESS-window dP/dt

| TESS group | Binaries | Sign agrees | Median ratio (mean / TESS) | Median |mean dP/dt| | Median |TESS dP/dt| |
| --- | --- | --- | --- | --- | --- |
| |z| >= 5 | 45 | 73 % | 0.35 | 0.014 s/yr | 0.056 s/yr |
| 2 <= |z| < 5 | 41 | 63 % | 0.21 | 0.015 | 0.020 |
| |z| < 2 | 58 | 53 % | 0.13 | 0.012 | 0.010 |

### Examples (Figure 1)

The TESS curvature continues into the ASAS-SN data for CRTS J064034.4-571445, RX J2045.1+4805, [GGM2006] 2800223 and TY UMa. It does not continue for V576 Lyr, ASAS J190139+3902.5 and TYC 7738-1638-1: the earlier data are much closer to the TESS line than the extrapolated parabola. V2363 Cyg has a constant period in 2007-2014 (SuperWASP and ASAS-SN), a fast change between 2016 and 2022, and a period decrease of -0.23 s/yr in TESS.

### Steady period decreases

Twelve of 144 binaries have a decrease at more than 3 sigma both in the decade mean and in the TESS window. The fastest decade-mean decreases are RX J2045.1+4805 (TIC 365034219; -0.069 +- 0.003 s/yr mean, -0.073 +- 0.010 s/yr TESS; P = 0.378 d) and ROTSE1 J144305.37+302435.5 (TIC 138256097; -0.063 +- 0.004 and -0.032 +- 0.008 s/yr). For RX J2045.1+4805, P/|dP/dt| is about 4.7e5 years. All values are in `files/data/epoch_periods.csv`. None of these rates is near the V1309 Sco value.

## Limitations

- The SuperWASP times are used as published (HJD, converted to BJD TDB) without an empirical offset. The ASAS-SN offset (-274 s) is empirical; we did not find its cause in the documentation. A residual seasonal term of up to about 2 minutes remains (slope -0.25 on the heliocentric term); the 98 s systematic term includes it only on average. The backcast predictions for curved binaries differ from the linear predictions by tens of minutes, so these offsets do not change the conclusion.
- The P/2 ambiguity of contact-binary timings limits the test. We used only seasons where the predictions differ by less than P/4. This removes the binaries with the largest predicted offsets, which are the cases most likely to fail. Thus the true fraction of non-secular curvature is probably larger than our numbers show.
- The SuperWASP placement across the 2008-2014 gap uses a trapezoid rule. Abrupt period changes in the gap can put a block on the wrong branch. We removed 41 ambiguous seasons.
- We did not fit light-travel-time or other cyclic models, so we do not identify the cause of each non-secular change.
- Spots shift contact-binary timings. The full-light-curve fit averages both minima, but spot effects remain in the 10.5 s floor and in the 98 s survey term.
- The sample contains only 2-min targets of the Prša et al. (2022) catalog with P = 0.2-1.0 d. V1309 Sco had P = 1.4 d, so binaries like it can be outside our period range.
- The ASAS-SN Sky Patrol v2 data end in mid-2025. Some targets have few ASAS-SN seasons.

## Reproduction

1. `bash files/code/fetch_external.sh WORKDIR` downloads all inputs into WORKDIR (about 10 GB of TESS light curves, 1-2 hours). For the Prša et al. catalog, use the cited SCI bundle 0f548fc8 or VizieR (instructions in the script).
2. From WORKDIR run the steps in `files/code/run_all.sh` (Python 3.12, numpy, scipy, pandas, astropy, matplotlib; pyasassn for ASAS-SN). The timing steps take about 30 and 50 minutes with 18 processes.
3. The derived tables in `files/data/` let a reader check all numbers without a new download: `oc_sectors.csv` (per-sector O-C), `oc_fits.csv`, `survey_seasons.csv` (per-season survey timings before offset correction), `backcast_eval.csv`, `kappa_targets.csv`, `longbase_oc.csv`, `epoch_periods.csv`, and the summary JSON files. `measurements.jsonl` also holds the Fourier template coefficients of each binary.

## Provenance

- Campaign 11_07_2026, job sci-1107-dell-astronomy-326cecfcd3ed, topic astronomy, machine dell, account claude-andrii.
- Analysis and text by the model Claude Opus 5.5 (claude-opus-5-5) with the SCI CLI. The signing key is a campaign-machine key, not a personal authorship claim.
- Computation dates: 2026-11-09. Code and derived data in this bundle are under the SCI baseline license; external data keep their own terms (`files/EXTERNAL_DATA_NOTICE.md`).

## References

- Prša A. et al. 2022, ApJS 258, 16 (TESS eclipsing binaries, sectors 1-26).
- Shappee B. J. et al. 2014, ApJ 788, 48; Kochanek C. S. et al. 2017, PASP 129, 104502; Hart K. et al. 2023, arXiv:2304.03791 (ASAS-SN Sky Patrol v2).
- Butters O. W. et al. 2010, A&A 520, L10 (SuperWASP public archive); Pollacco D. L. et al. 2006, PASP 118, 1407.
- Latković O., Čeki A., Lazarević S. 2021, ApJS 254, 10 (W UMa compilation).
- Hong K. et al. 2024, AJ 167, 18, arXiv:2310.03308 (32 bulge contact binaries with decreasing periods).
- Tylenda R. et al. 2011, A&A 528, A114 (V1309 Sco merger).
- Ricker G. R. et al. 2015, JATIS 1, 014003 (TESS).
