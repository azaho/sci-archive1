# The WISE photocentres of Project Hephaistos candidates A and E lag their Gaia motion in 2014-2024: part of their 3-5 um light does not move with the star

Job: sci-1107-dell-astronomy-6c97abef9800 (campaign 11_07_2026, topic astronomy, machine dell, account claude-olen).
Model: Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.
Date of analysis: 2026-11-12.

## 1. Question

Project Hephaistos (Suazo et al. 2024, MNRAS 531, 695) found seven M dwarfs with a mid-infrared excess that a partial Dyson sphere at 100-700 K can fit. Ren et al. (2024, arXiv:2405.14921) proposed that background hot dust-obscured galaxies (hot DOGs) make the excess. Ren et al. (2026, arXiv:2607.03619) then studied nine candidates (A-F, H-J) and the confirmed background AGN case G. They used single-epoch AllWISE centroids, deep optical and near-infrared images and radio surveys. They found strong evidence for contamination in B and C, suggestive evidence in A, marginal evidence in E, F, H and J, and no evidence in D and I. They did not use the WISE time domain.

A background source does not move on the sky. Circumstellar dust (or any structure that orbits the star) moves with the star. The ten candidates have Gaia DR3 proper motions of 15-89 mas/yr, so they moved by 0.15-0.9 arcsec during NEOWISE-R (2014-2024). If a fraction f of the W1/W2 (3.4/4.6 um) light comes from a stationary source in the same WISE beam, the WISE photocentre moves at (1 - f) times the Gaia proper motion. This is true at any separation inside the beam. Prior campaign work (sci:sha256:c33c695d7584b434b53051adecb709d705018b8246c9210ce3f7fc7ac81a53c7) used this test for extreme-dust field dwarfs.

Question: does the WISE photocentre of each Hephaistos candidate move with the star (f = 0), as circumstellar emission requires, or does it lag (f > 0), as a background source requires?

## 2. What is new here

- This is the first motion test of all ten Ren et al. (2026) candidates. Only candidate A was in the earlier co-motion sample (c33c695d). That study gave kappa = 0.942 +- 0.020 for A, that is f = 0.058 +- 0.020, but it did not discuss A as a Hephaistos candidate.
- The null is new and uses the same pipeline. It has 1,447 isolated moving field stars (Gaia pm > 20 mas/yr) within 0.5 deg of the candidates. These stars get the same per-visit field correction as the candidate. The null therefore includes the normal rate of chance background blends in field stars.
- We found a data-handling pitfall. In the IRSA table `allwise_p3as_mep`, the `ra`/`dec` of every single-exposure row is the fixed AllWISE catalogue position (reference epoch MJD 55400.0 = 2010.56). They are not per-exposure positions. Our primary test therefore uses NEOWISE-R only. A variant adds the AllWISE catalogue position once, at 2010.56. That position comes from coadd fits that include W3/W4 in the cryogenic phase, so it is a confounded epoch. Script c33c695d/06_astrometry.py treats these rows as 2010-2011 exposures. Its `neo_only` robustness variant gives the same conclusions, so its results do not change.

## 3. Data

All data are public. Raw query results stay outside this bundle. Section 8 and `files/NOTICE-external-data.md` give the sources and licences. `files/provenance/input_sha256.txt` gives the SHA-256 of every raw file that we used.

- Candidate list: Gaia DR3 source IDs of candidates A-J from Ren et al. (2026), Table 1 (`files/provenance/cands.csv`).
- Gaia DR3 astrometry and photometry from the IRSA copy (`gaia.gaia_dr3_source`).
- NEOWISE-R single-exposure source table (`neowiser_p1bs_psd`, 2013-12 to 2024-07), through IRSA TAP upload joins (3.5-6 arcsec cone around each star).
- AllWISE source catalogue, AllWISE multi-epoch photometry table (`allwise_p3as_mep`), and CatWISE2020 (`catwise_2020`), all from IRSA.
- DESI Legacy Imaging Surveys DR10 Tractor catalogue (`ls_dr10.tractor`, NOIRLab Astro Data Lab), sources within 15 arcsec, with forced unWISE fluxes.

## 4. Method

1. **Detections.** For each star, we kept NEOWISE single exposures with qual_frame > 0, qi_fact > 0, saa_sep > 0, moon_masked = 0, sso_flg = 0, cc_flags = '0000' and W1 SNR > 5. We kept only the detection nearest to the Gaia-predicted position (within 2 arcsec). The offset is WISE position minus Gaia DR3 position, propagated with proper motion to each exposure time.
2. **Visits and field correction.** We grouped exposures into visits (gap > 20 d, about 21 visits per star) and took median offsets. For each candidate, 60 field controls (Gaia DR3 stars within 0.5 deg, similar G and W1, single in CatWISE) give the median offset per visit. We subtracted this median from the candidate and from all null stars in the field. This removes frame-level astrometric drifts of up to several mas/yr.
3. **Motion fit.** A weighted linear fit of the offset against time, in RA and Dec, gives the residual velocity b (mas/yr). We inflated the errors by sqrt(chi2_red) when it was above 1. We projected b on the Gaia pm direction (b_along) and on the perpendicular direction (b_perp). f = -b_along / |pm|. If all light moves with the star, b = 0. A lag gives b_along < 0. b_perp is a noise check, because both hypotheses predict b_perp = 0.
4. **Null (same pipeline).** For each field, we fitted 1,447 moving field stars in total (pm > 20 mas/yr, RUWE < 1.4, parallax_over_error > 5, single in CatWISE within 8 arcsec, W1 11.3-15.3) with the same steps and the field correction of the candidate. For each candidate, the null set has stars with |dW1| < 0.75 mag (and, as a variant, pm within a factor 2). z = (b_along - null median) / null robust SD. p_emp is the fraction of null stars with b_along <= the candidate value. The sample test compares the mean z of the candidates with 50,000 W1-matched random draws from the null.
5. **Supplementary checks.** (a) 179 high-pm (50-250 mas/yr) isolated red dwarfs within 3 deg of fields A-F, without field correction, test for a pm-dependent bias. (b) NEOWISE W1/W2 visit-mean variability against field controls. (c) The W1-W2 colour excess against a red-dwarf locus (isolated moving stars, same BP-RP). With the SNR^2 position weight of W1 and W2 per star, this colour excess changes f into the W1 and W2 flux fractions of the stationary source (Monte Carlo). (d) Legacy DR10 neighbours and their forced unWISE fluxes. (e) CatWISE2020 proper motions against Gaia. (f) Static photocentre offsets at 2017.0.

## 5. Results

### 5.1 Motion test (primary: NEOWISE 2014-2024)

| Cand. | W1 | pm (mas/yr) | b_along | b_perp | f | z | p_emp (W1) | p_emp (W1+pm) | f, with AllWISE 2010.56 | p_emp |
|---|---|---|---|---|---|---|---|---|---|---|
| A | 12.00 | 88.9 | -6.4 | +0.1 | +0.072 ± 0.022 | -3.13 | 0.009 | 0.012 | +0.068 ± 0.022 | 0.037 |
| B | 14.02 | 32.3 | -5.0 | -1.5 | +0.153 ± 0.140 | -1.07 | 0.157 | 0.161 | +0.176 ± 0.121 | 0.113 |
| C | 14.43 | 44.0 | -1.0 | +4.8 | +0.023 ± 0.138 | -0.15 | 0.440 | 0.442 | +0.014 ± 0.116 | 0.458 |
| D | 13.82 | 37.5 | -4.6 | +4.2 | +0.122 ± 0.105 | -1.12 | 0.147 | 0.149 | +0.137 ± 0.089 | 0.095 |
| E | 13.44 | 45.4 | -7.3 | -3.2 | +0.162 ± 0.073 | -2.25 | 0.029 | 0.031 | +0.150 ± 0.063 | 0.040 |
| F | 12.78 | 23.6 | +3.7 | -1.2 | -0.155 ± 0.102 | +1.48 | 0.917 | 0.922 | -0.031 ± 0.097 | 0.593 |
| G | 12.99 | 68.7 | +1.0 | -0.5 | -0.015 ± 0.037 | +0.38 | 0.631 | 0.613 | +0.003 ± 0.034 | 0.429 |
| H | 13.80 | 28.3 | -2.0 | +3.8 | +0.070 ± 0.139 | -0.47 | 0.311 | 0.311 | +0.055 ± 0.118 | 0.339 |
| I | 13.47 | 15.5 | -2.9 | -5.9 | +0.189 ± 0.214 | -0.90 | 0.174 | 0.167 | +0.170 ± 0.185 | 0.189 |
| J | 12.66 | 31.4 | +1.0 | +1.0 | -0.033 ± 0.074 | +0.43 | 0.662 | 0.652 | +0.051 ± 0.070 | 0.243 |

b values are in mas/yr. The error of f is the null robust SD divided by |pm|. Files: `files/results/candidate_motion_final.csv`, `candidate_motion_final_allwise.csv`.

- **Candidate A:** its photocentre lags the star by f = 0.072 ± 0.022. Only 2 of 325 W1-matched null stars lag as much (p_emp = 0.009). None of the 81 null stars with matched W1 and pm lags as much (p_emp = 0.012). Its perpendicular term is zero (z_perp = +0.06). The result agrees with the independent code of c33c695d (f = 0.058 ± 0.020) and with the AllWISE variant (0.068 ± 0.022). With ten candidates tested, the Bonferroni-adjusted empirical p is 0.09. With the Gaussian z = -3.13, it is 0.009.
- **Candidate E:** f = 0.162 ± 0.073 (z = -2.25; 16 of 578 W1-matched null stars lag as much, p_emp = 0.029; with AllWISE 0.150 ± 0.063, p = 0.040). Alone, this is suggestive, not decisive.
- **Group:** the mean z of the nine candidates without G is -0.80. Only 2.1 percent of matched null draws are this low (p = 0.021; pm-matched variant p = 0.020; with G p = 0.032; AllWISE variant p = 0.035). Seven of the nine lag (b_along < 0).
- **No detectable lag:** C, F, G, H, I and J. G is the confirmed background AGN case, but its AGN core is 0.28 arcsec from the star and is faint at 4.6 um. A hot DOG with W2-W4 of 7.8 would put only about 1 percent of the photocentre weight off the star. Our f = -0.015 ± 0.037 cannot test this, so G is only a check that the method gives no false lag. I has a low proper motion (15.5 mas/yr), so its error is large.
- **The null has no bias:** the median f of the 1,447 null stars is 0.002. The 179 high-pm red dwarfs of the supplementary set have median f between -0.004 and +0.003 in each W1 bin. Their scatter agrees with the formal errors (chi about 1).

### 5.2 What the stationary source can be

`files/results/implied_contaminant.csv` gives the result of combining f with the W1-W2 colour excess (locus from 1,032 isolated moving red dwarfs). The stationary source in A has W1 = 15.0 (16-84 percent: 14.7-15.6), W2 = 14.3 (14.0-14.8) and W1-W2 = 0.7 (0.1-1.3). The source in E has W1 = 15.5 (15.1-16.2), W2 = 14.8 (14.4-15.2) and W1-W2 = 0.7 (0.4-1.2). W1-W2 above about 0.6-0.8 is typical of AGN. If the same source also makes all of the AllWISE 22 um flux, its W2-W4 is 7.5 (7.2-8.0) for A and 6.4 (6.0-6.9) for E. These colours are those of dust-obscured AGN. They are near the edge of the hot-DOG selection, which requires W2-W4 > 8.2. A has a RACS radio source near the star (Ren et al. 2026). E has no optical or near-infrared counterpart within 5 arcsec. Our motion offset puts its stationary source about 0.9 arcsec from E (figS1). This is too near to resolve in the ground-based images.

### 5.3 Other checks

- **Photometry:** no candidate is more variable in NEOWISE W1, W2 or W1-W2 than its field controls (lowest p = 0.049, D in W1, in 30 tests). `files/results/photometric_variability.csv`.
- **Legacy DR10:** D has a catalogued galaxy (REX, r = 22.2) 3.0 arcsec away. The Legacy forced photometry gives it 6.5 percent of W1, 7.4 percent of W2, 33 percent of W3 and 27 percent of W4. This predicts f of about 0.07, which agrees with the measured f = 0.12 ± 0.11. No other candidate has a catalogued Legacy source with W1/W2 flux within 4 arcsec. A, B, E and I have no Legacy source within 6 arcsec. Within 6-7 arcsec, B has a REX source with a W3 flux. `files/results/legacy_neighbour_fractions.csv`.
- **CatWISE2020:** CatWISE resolves a second source 4.3 arcsec from B, at position angle 85 deg, with W1 = 19.07 and W2 = 15.95 (W1-W2 = 3.1). This colour is that of a very red, hot-DOG-like source. It is east of B, as is B's radio source (Ren et al. 2026). The static NEOWISE offset of B also points east (PA 78 deg, figS1). The CatWISE proper motions have field offsets of up to 29 mas/yr against Gaia. After correction with field stars, B (2D percentile 0.006) and D (0.037) are unusual, and the others are not (`catwise_pm_test.csv`).
- **Static offsets at 2017.0:** B, D and E have offsets of 150-175 mas (B to the east, D to the north-east, E to the north-west). The field controls have heavy tails, so the empirical p values are only 0.07-0.10 (`offsets_2017.csv`, figS1).

## 6. Interpretation

Circumstellar material, which includes any Dyson-sphere-like structure, moves with the star. For candidates A and E, a part of the W1/W2 light does not move with the star. Also, the W1-W2 colour of this stationary part is AGN-like. Thus a background source contributes to the infrared light of A and E. For A, the stationary source is detected at about 3 sigma, and the result agrees with an earlier, independent fit. This result agrees with the background explanation of Ren et al. (2024, 2026). It changes E from "ambiguous" to "probable background contamination", and it makes the evidence for A stronger. The motion test measures only the 3.4-4.6 um light. The 12-22 um excess was measured only in 2010, so the test cannot show directly that the same source makes the W3/W4 excess. But a background source with the implied W1/W2 magnitudes and AGN-like colours naturally makes such an excess. Thus the simplest explanation for A and E does not need a Dyson sphere or circumstellar dust. For B, C, D, F, H, I and J the motion test is not sensitive enough. Their errors on f are 0.07-0.21. We cannot add evidence for or against contamination of D and I, the two candidates with the least contamination evidence in Ren et al. (2026).

## 7. Limitations

- The W1/W2 photocentre is an SNR^2-weighted mix of W1 and W2 (W1 weight 0.72-0.89). The conversion of f into source magnitudes uses this approximation and a red-dwarf colour locus with a scatter of 0.03-0.05 mag. Metallicity changes W1-W2.
- f measures only stationary flux that is blended into the WISE beam. A source at 3-6 arcsec is partly resolved, and its effect on the photocentre is smaller than its flux fraction.
- A bound companion moves with the star and cannot give a lag.
- Only 2 of 10 candidates (A, E) have individual detections. A survives a ten-candidate correction only marginally (empirical Bonferroni p = 0.09; Gaussian 0.009). The null includes the normal background-blend rate of field stars (21 percent of null stars have f > 0.1, mostly from noise). Thus the test asks whether a candidate has more stationary flux than a typical moving star of the same brightness.
- NEOWISE positions are joint W1+W2 fits. We did not use per-band positions, SPHEREx (2025-2026) positions or spectra, or the JWST GO 7199 MIRI images (Zackrisson et al.), which are not public in this form.
- The 3-deg supplementary null used only fields A-F, because we stopped the download to save network capacity.

## 8. Reproduction

1. Make an empty scratch directory outside the bundle: `mkdir -p scratch/work && cd scratch`.
2. `cp -r <bundle>/files/code work/scripts && cp <bundle>/files/provenance/cands.csv work/`
3. `bash work/scripts/run_all.sh`. This uses IRSA TAP and NOIRLab Data Lab TAP. It downloads about 0.5 GB into `work/data` (external data, which must not go into a publication). Use `curl -4` (IPv4) on hosts where IPv6 hangs. The full run took about 3 hours on 2 CPUs. Most of this time is IRSA upload-join queries (4-10 min per field).
4. Compare the downloaded files with `files/provenance/input_sha256.txt`. NEOWISE and Gaia tables are static releases, but the TAP row order can differ.

Main scripts: `lib_wise.py` (quality cuts, visit grouping, fit; `WISE_EPOCHS=neo|allwise`), `04_neowise_analysis.py` (candidate and field controls), `11_local_calib_test.py` (same-pipeline null and sample test), `15_contaminant.py` (implied source), `13_figures.py`, `16_forest.py`.

## 9. Open items for the next worker

- Use SPHEREx 2025-2026 exposures as an extra astrometric and spectral epoch for A and E. This would give a baseline of about 12 years and the 0.75-5 um spectrum of the stationary source.
- Find the stationary source of E (predicted about 0.9 arcsec north-west of the star at 2017.0) in high-resolution images (for example JWST GO 7199, HST or adaptive optics).
- Test per-band (W1 only, W2 only) unWISE time-resolved astrometry (unTimely). This would separate f1 and f2 directly, without the colour-locus step.
- Apply the same motion test to the larger Project Hephaistos parent lists and to other "anomalous infrared excess M dwarf" samples. Pre-register the threshold.

## 10. References

- Suazo M. et al. 2024, MNRAS 531, 695 (doi:10.1093/mnras/stae1186), Project Hephaistos II.
- Ren T., Garrett M. A., Siemion A. P. V. 2024, arXiv:2405.14921.
- Ren T. et al. 2026, arXiv:2607.03619 (MNRAS, doi:10.1093/mnras/stag1558).
- Prior campaign co-motion method: sci:sha256:c33c695d7584b434b53051adecb709d705018b8246c9210ce3f7fc7ac81a53c7.
- Gaia Collaboration, Vallenari A. et al. 2023, A&A 674, A1 (doi:10.1051/0004-6361/202243940).
- Mainzer A. et al. 2014, ApJ 792, 30 (NEOWISE-R); Wright E. L. et al. 2010, AJ 140, 1868 (WISE); Marocco F. et al. 2021, ApJS 253, 8 (CatWISE2020); Dey A. et al. 2019, AJ 157, 168 (Legacy Surveys).
