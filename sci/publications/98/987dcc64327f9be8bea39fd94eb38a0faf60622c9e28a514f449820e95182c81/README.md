# Gaia DR3 eclipsing binaries that match TESS planet candidates in period and epoch: 10 probable nearby-eclipsing-binary false positives among 8151 TOIs

## Summary

The TESS Objects of Interest (TOI) list contains many planet candidates (PC). The TESS pixels are 21 arcsec wide, so the light of a faint nearby eclipsing binary (EB) can mix with the light of the target star. The diluted eclipse can then look like a planet transit. Gaia DR3 gives periods and eclipse epochs for 2.2 million EBs. We used these data to do a test on all TOIs.

For each of 8151 TOIs, we found all Gaia DR3 EBs (`gaiadr3.vari_eclipsing_binary`) within 3 arcmin. For each TOI-EB pair, we did three tests:

1. **Period test.** The TOI period is equal to the EB period multiplied by a small ratio (1, 2, 1/2, 3, 1/3, 3/2, 2/3). The relative deviation must be less than 1e-3, and the difference must be less than 10 times the quoted uncertainty.
2. **Epoch test.** We propagated the Gaia primary-eclipse time to the TOI transit epoch. The phase gap to the nearest Gaia eclipse (primary or secondary) must be less than 0.05.
3. **Dilution test.** The undiluted eclipse depth that the EB must have to make the TOI depth must be less than 1. We compare it with the Gaia G eclipse depth.

A pair that passes tests 1 and 2 is "Tier A". A pair that passes only test 1 is "Tier B". To measure the rate of chance matches, we did the same search around control positions. Each control position is 0.5 deg from its TOI, in a random direction.

**Main results**

* The TOI cones contain 4591 TOI-EB pairs (2274 TOIs have one or more EBs in the cone). The control cones contain 4588 pairs. There are 164 period matches in the TOI cones and 12 in the control cones. There are **132 Tier A matches in the TOI cones and 0 in the control cones** (Figure 1). Thus most Tier A matches are not chance coincidences. The expected number of chance Tier A matches in the full sample is less than 3 (95% upper limit from 0 control matches).
* The TOI epochs agree with the propagated Gaia eclipse times. This independent test confirms the convention `T_prim = 2455197.5 + reference_time + derived_primary_ecl_phase / frequency` (BJD).
* Tier A matches occur for **121 of 604 (20%) TFOPWG false positives (FP)** that have an EB in the cone. They occur for **0 of 226 confirmed or known planets (CP and KP)** and for 0 of 107 ambitious planet candidates (APC) (Figure 2). This shows that the method finds real contamination and does not reject real planets in this sample.
* **11 TOIs that have the TFOPWG disposition PC have a Tier A match** (Table 1). For 10 of them, the EB is a separate Gaia star 4.5 to 16 arcsec from the target. The Gaia eclipse is deep enough to make the TESS signal after dilution. These 10 TOIs are probably nearby-eclipsing-binary (NEB) false positives. For one TOI (3142.01), the EB is the target star. This puts the signal on the target star, but the data do not tell us if it is a planet or an EB.
* **Independent confirmation for TOI 1546.01** (a "potential level 1" candidate, 3 Earth radii, T = 9.9). The Gaia EB 384251315018012800 (G = 17.7, 10.8 arcsec away) has 1504 good ZTF measurements (g and r). A box-least-squares search of the ZTF data gives P = 1.1328272 d (Gaia: 1.132826 d; TOI: 1.13345 +- 0.0006 d) and a 0.6 mag eclipse. The TOI transit epoch is 0.41 h from the eclipse time that the ZTF ephemeris predicts (Figure 4). The TOI period has a large uncertainty. Thus the ZTF fold on the TOI period does not show the eclipse, but the fold on the ZTF period does.
* **TESS pixel tests.** We made difference images (mean out-of-transit flux minus mean in-transit flux) from TESS FFI cut-outs. For the two Tier A pairs with separations of 0.8 px (TOI 1960.01 and 2541.01), the difference-image centroid is on the Gaia EB and not on the target (Figure 3). For the other Tier A pairs, the separation is less than 0.55 px and TESS cannot resolve the two stars. The centroid is nearer to the EB than to the target in all usable sectors, but this is weak evidence. For the wide Tier B pairs TOI 699.01 (57 arcsec) and 6496.01 (79 arcsec), the signal is on the target and not on the EB. Thus these Tier B period matches are chance coincidences. This agrees with the control result.

## Table 1. PC and APC TOIs with a Gaia DR3 EB period match

Columns: TOI; tier; TIC; Gaia DR3 source_id of the EB; separation (arcsec); TESS magnitude of target / estimated TESS magnitude of EB; TOI period (d); Gaia EB period (d) (ratio r = P_TOI / P_EB); relative period deviation; epoch phase gap; TOI depth (ppm); undiluted EB depth needed / Gaia G primary depth (fraction); false-alarm probability (FAP) for this TOI cone; TESS pixel test; ExoFOP comment (first 90 characters, 2026-11-08 table).

| TOI | Tier | TIC | Gaia DR3 EB | sep | T_tgt / T_EB | P_TOI | P_EB (r) | dP/P | phase gap | depth | need / Gaia | FAP | TESS pixel test | ExoFOP comment |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 2998.01 | A | 34737413 | 5411522075563154816 | 10.6 | 12.5 / 17.7 | 1.529712 | 1.529711 (1) | 6.2e-07 | 0.002 | 2410 | 0.28 / 0.40 | 2.3e-08 | unresolved (0.54 px); centroid nearer EB | found in faint-star QLP search |
| 3063.01 | A | 463103749 | 5258610764422238208 | 4.5 | 12.6 / 16.2 | 1.951292 | 3.902597 (1/2) | 3.4e-06 | 0.001 | 6703 | 0.20 / 0.26 | 5.2e-08 | unresolved (0.22 px); centroid nearer EB | faint-star QLP; Rp/Rs 7.2% - may be EB |
| 2541.01 | A | 31054498 | 2956998401052982272 | 15.8 | 9.9 / 16.0 | 1.411842 | 1.411834 (1) | 5.7e-06 | 0.004 | 520 | 0.14 / 0.20 | 9.6e-08 | signal on EB (0.78 px) | Weak odd-even difference. Apparent secondary eclipse ... |
| 3258.01 | A | 369789627 | 5190786869949701248 | 5.5 | 12.7 / 17.5 | 1.227961 | 1.227967 (1) | 5.2e-06 | 0.003 | 2260 | 0.20 / 0.27 | 1.2e-07 | unresolved (0.26 px); centroid nearer EB | found in faint-star QLP search |
| 3143.01 | A | 384244834 | 5853391820057551616 | 10.4 | 12.0 / 15.3 | 2.990237 | 2.990223 (1) | 4.5e-06 | 0.001 | 6460 | 0.14 / 0.19 | 2.1e-07 | unresolved (0.51 px); centroid nearer EB | found in faint-star QLP search |
| 4870.01 | A | 446135868 | 5409588485596696832 | 5.7 | 13.4 / 15.7 | 1.811917 | 1.811911 (1) | 3.3e-06 | 0.011 | 5510 | 0.05 / 0.09 | 5.4e-07 | unresolved (0.28 px); centroid nearer EB | possible offset on nearby TIC 446135867 (Tmag~15.7) |
| 1960.01 | A | 318828309 | 5336073557657050624 | 15.7 | 9.2 / 13.9 | 5.341820 | 5.341862 (1) | 7.9e-06 | 0.004 | 330 | 0.03 / 0.10 | 1.7e-06 | signal on EB (0.80 px) | centroid offset centered on another star; likely EB |
| 4876.01 | A | 458300989 | 5352014650847002368 | 6.6 | 12.5 / 16.0 | 4.137954 | 4.138048 (1) | 2.3e-05 | 0.004 | 2610 | 0.07 / 0.11 | 3.9e-06 | unresolved (0.33 px); centroid nearer EB | found in faint-star QLP search |
| 3142.01 | A | 387791274 | 5854299913520272000 | 0.0 | 13.2 / 13.0 | 1.153656 | 2.307265 (1/2) | 2.0e-05 | 0.016 | 40190 | 0.04 / 0.04 | 5.2e-06 | EB is the target star | found in faint-star QLP search |
| 1546.01 | A | 194203348 | 384251315018012800 | 10.8 | 9.9 / 17.4 | 1.133450 | 1.132826 (1) | 5.5e-04 | 0.012 | 490 | 0.52 / 0.57 | 5.2e-05 | no usable sector; ZTF confirms EB ephemeris | Potential level 1; some depth-aperture correlation |
| 5008.01 | A | 150531994 | 5958084289208324992 | 6.0 | 12.9 / 15.7 | 2.775536 | 2.775797 (1) | 9.4e-05 | 0.017 | 12834 | 0.17 / 0.17 | 1.3e-04 | unresolved (0.28 px); centroid nearer EB | found in faint-star QLP search |
| 2960.01 | B | 462072242 | 5356287907109585920 | 3.8 | 13.0 / 15.8 | 2.091662 | 2.091549 (1) | 5.4e-05 | 0.050 | 5500 | 0.08 / 0.15 | 6.3e-05 | unresolved (0.19 px); centroid nearer EB | found in faint-star QLP search; v-shaped |
| 745.01 | B (APC) | 444842193 | 5307767829042171904 | 121.5 | 10.5 / 16.3 | 1.079093 | 0.719440 (3/2) | 6.2e-05 | 0.224 | 573 | 0.11 / 0.09 | 1.6e-04 | low S/N; S/N at EB negative | odd-even and v-shaped; likely EB |
| 7583.01 | B | 110110529 | 5615002267248643712 | 6.7 | 11.8 / 18.0 | 0.718031 | 0.717326 (1) | 9.8e-04 | 0.029 | 1364 | 0.39 / 0.72 | 2.2e-04 | unresolved (0.32 px) | found in faint-star QLP search |
| 699.01 | B | 149302744 | 4757624956991398528 | 57.3 | 9.8 / 17.2 | 14.801138 | 29.589672 (1/2) | 4.3e-04 | 0.132 | 317 | 0.28 / 0.10 | 4.3e-04 | **signal on target, not on EB** | potential L1 planet; possible multi |
| 6854.01 | B (APC) | 55363630 | 4663616364928126336 | 175.7 | 13.1 / 18.6 | 2.766348 | 1.384425 (2) | 9.0e-04 | 0.115 | 2476 | 0.38 / 0.14 | 1.6e-03 | low S/N | found in faint-star QLP search |
| 6496.01 | B | 374741750 | 5256696926975886976 | 79.1 | 13.1 / 18.3 | 0.994221 | 0.497602 (2) | 9.9e-04 | 0.056 | 7298 | 0.83 / 0.21 | 2.6e-03 | **signal on target, not on EB** | found in faint-star QLP search |

The full table with all columns is `files/results/final_candidate_table.csv`.

**Interpretation of each group**

* **Probable NEB false positives (10, Tier A, off-target):** 2998.01, 3063.01, 2541.01, 3258.01, 3143.01, 4870.01, 1960.01, 4876.01, 1546.01, 5008.01. For 1960.01 and 4870.01, the ExoFOP comments already report a centroid offset on a nearby star. Our result identifies the Gaia source and confirms its period and epoch. For 3063.01, ExoFOP says "may be EB". For 2541.01 and 1546.01, the comments report odd-even or depth-aperture effects but do not name a source. For 2998.01, 3258.01, 3143.01, 4876.01 and 5008.01, the comment field does not mention contamination. These TOIs still have the disposition PC in both the NASA Exoplanet Archive and the ExoFOP tables that we used.
* **On-target signal (1):** 3142.01. The Gaia EB is the target star (separation 0.003 arcsec). Gaia finds P = 2.307 d with a primary eclipse of 0.046 +- 0.002 mag and a secondary eclipse of 0.028 +- 0.016 mag at phase 0.50. TESS finds half of this period (1.154 d) with a depth of 4.0%. The two Gaia depths agree within 1.2 sigma. Thus the data agree with an EB at 2.307 d and also with a transit at 1.154 d. The Gaia RUWE is 1.70, which can indicate an unresolved binary. This result removes the NEB explanation, but it does not classify the signal.
* **Probable match, just outside Tier A:** 2960.01. The period agrees to 5e-5 and the phase gap is 0.0500, at the limit. The TESS centroid agrees with both stars (separation 0.19 px).
* **Probable chance matches (Tier B):** 699.01 and 6496.01 (signal on the target in TESS pixels); 7583.01 (the period difference is 182 times the quoted uncertainty, and ZTF shows no dip at the TOI ephemeris); 745.01 and 6854.01 (wide separations, phase gap > 0.1, low pixel S/N). We do not claim that these TOIs are false positives.

## Figures

* Figure 1 (`files/figures/fig_matching_overview.png`): (a) relative period deviation for TOI pairs and control pairs; (b) epoch phase gap for period matches; (c) undiluted EB depth needed versus Gaia G depth.
* Figure 2 (`files/figures/fig_disposition_rates.png`): fraction of TOIs with a Tier A match, by TFOPWG disposition.
* Figure 3 (`files/figures/fig_pixel_tests.png`): TESS difference-image S/N maps for two Tier A pairs (signal on the EB) and two Tier B pairs (signal on the target).
* Figure 4 (`files/figures/fig_ztf_TOI1546.01.png`): ZTF BLS periodogram of the Gaia EB near TOI 1546.01, and folds on the ZTF and TOI ephemerides.
* Per-sector difference images: `files/results/diffimg/*.png`.

## Methods

1. **TOI list.** NASA Exoplanet Archive TAP table `toi`, retrieved 2026-11-07 (8151 TOIs). Columns: TOI, TIC, TFOPWG disposition, RA, Dec, TESS magnitude, period and error, transit midpoint and error, duration, depth, radius, stellar radius and temperature.
2. **Gaia cone search.** Gaia archive TAP (`gea.esac.esa.int`), ADQL join of an uploaded position table with `gaiadr3.gaia_source` (3 arcmin circle) and `gaiadr3.vari_eclipsing_binary`. We sent the query in chunks of 400 positions. Control positions are 0.5 deg from the TOI in a random direction (random seed 20261107).
3. **Matching.** `P_EB = 1/frequency` and `sigma_P_EB = frequency_error / frequency^2`. For each pair, we kept the ratio with the smallest relative deviation. Gaia times are BJD(TCB) - 2455197.5. The TCB-TDB difference (about 20 s) is not important here. The phase gap is measured in units of P_EB. For r = 1/2, the TOI ephemeris also predicts an event at EB phase 0.5.
4. **Dilution.** We estimated the TESS magnitude of the EB from Gaia G and BP-RP with the TIC-8 relation (Stassun et al. 2019). Flux fraction `f = F_EB / (F_target + F_EB)`. The needed undiluted depth is `depth_TOI / f`. This assumes that the aperture collects all flux of both stars and no other flux. This is a lower limit for off-centre EBs.
5. **False-alarm probability.** From the control pairs, the rate of chance period matches per pair is 1.94 per unit relative tolerance (measured at 1e-2; 2.6 at 1e-3). For each pair, `p = 1.94 * dP/P * min(1, 2 * n_phase * phase_gap)`, where n_phase is the number of tested eclipse phases (1 or 2). The FAP for a TOI cone is `1 - (1 - p)^N`, where N is the number of EBs in the cone. If you multiply the largest Tier A FAP (1.3e-4) by the 1431 PC and APC TOIs that have an EB in the cone, the expected number of chance matches is less than 0.2.
6. **TESS pixel test.** We downloaded 21 x 21 pixel FFI cut-outs from the MAST TESScut API. We used up to two sectors for each TOI and skipped sectors in which the propagated TOI ephemeris uncertainty is more than 0.3 transit durations. We subtracted a per-cadence background (the median of the faintest 30% of pixels). We removed the trend of each pixel with a running median of 1 day, with the transits masked. Then we made the image of mean flux near the transit (0.75 to 2.5 durations from mid-transit) minus mean in-transit flux (within 0.35 durations), divided by its standard error. The centroid is the flux-weighted mean of positive pixels within 2.5 px of the peak. A sector is "usable" if the peak S/N is 6 or more and the centroid is within 1.5 px of the target or the EB.
7. **ZTF test.** IRSA ZTF light-curve API, `catflags = 0`, nearest ZTF object to the Gaia position in each band. Box-least-squares search (astropy) on 20000 trial periods between the TOI and Gaia periods (+-0.5%).

## Limitations

* **Gaia completeness.** Gaia DR3 classified only a subset of EBs, mostly with G < 19 and enough epochs. A TOI without a match can still be an NEB. The 20% match rate for known FPs shows this limit.
* **Not a final disposition.** A Tier A match is strong evidence for NEB contamination. It is not a full proof. A planet and an EB with the same period and phase within 3 arcmin are possible but rare (FAP values in Table 1). Final classification needs follow-up data, for example ground-based photometry of the EB at the predicted transit times.
* **Pixel test resolution.** For 8 of the 10 probable NEB pairs, the separation is less than 0.55 TESS pixels. Our simple centroid method cannot resolve the two stars. We did not do a PRF fit or quantify the centroid uncertainty.
* **Gaia epoch photometry.** The Gaia DataLink service returned HTTP 503 during this work. Thus we did not fold the Gaia epoch photometry directly. The epoch test uses the Gaia model parameters only.
* **ZTF coverage.** ZTF does not observe south of about -30 deg. Only three EBs had ZTF data. Only the TOI 1546.01 EB had enough points for a period search.
* **Dilution estimate.** The depth test uses Gaia-to-TESS colour relations and assumes full flux capture. Gaia's sparse sampling can underestimate eclipse depths.
* **Catalog snapshot.** The TOI and ExoFOP tables change with time. The results are for the versions that we list below.
* **Search radius.** We searched 3 arcmin only. A very bright EB farther away can also contaminate a TOI.

## Data provenance

* TOI table: NASA Exoplanet Archive TAP, URL in `files/PROVENANCE.md`. Shared campaign copy: `datasets/nasa-exoarchive-toi-ephemeris-20261107/toi.csv`, SHA-256 `e6198dd4a763291e4b99806cde2ae09cfb7e84293d91a7936eb322f0a6e325f6`.
* ExoFOP TOI table (dispositions and comments): `https://exofop.ipac.caltech.edu/tess/download_toi.php?sort=toi&output=csv`, retrieved 2026-11-08. Shared copy: `datasets/exofop-tess-toi-table-20261108/exofop_toi.csv`, SHA-256 `ef22793ad87770c1795ff8da2243289b45e9282ff0bfb1ec3384fba1fbfd366a`.
* Gaia DR3 query results (derived): `files/data/gaia_eb_near_toi.csv`, `files/data/gaia_eb_near_control.csv`.
* ZTF light curves (IRSA, retrieved 2026-11-08) for three EBs: `files/data/ztf_lc_gaia*.csv`.
* TESS FFI cut-outs: MAST TESScut API. We do not include them (size). The code downloads them again.
* SHA-256 values of all package files: `files/PROVENANCE.md` and the signed manifest.

## Reproduce

```
uv venv .venv --python 3.12
uv pip install --python .venv/bin/python -r files/code/requirements.txt
export OMP_NUM_THREADS=1
TOI=path/to/toi.csv              # see PROVENANCE.md for the URL and hash
EXOFOP=path/to/exofop_toi.csv
python files/code/01_query_gaia.py $TOI data both         # Gaia TAP, about 40 min
python files/code/02_match.py $TOI data/gaia_eb_near_toi.csv data/gaia_eb_near_control.csv out
python files/code/04_classify.py out $EXOFOP
python files/code/05_independent_lcs.py out cache         # ZTF and Gaia epoch photometry folds
python files/code/06_ztf_period.py cache/ztf_384251315018012800.csv 1546.01 1.13345 0.0006 2458764.83324 1.132826 1.894 out/ztf/ztf_bls_TOI1546.01.png
python files/code/07_run_diffimages.py out $TOI           # TESScut downloads, about 1 h
python files/code/08_summarize.py out
```

You can start at step 2 with the Gaia query results in `files/data/`.

## Context and prior work

Earlier work has used Gaia for TESS candidate vetting: Gaia DR3 spectroscopic orbits (arXiv:2310.12380), and Gaia photometry of sources in TESS apertures (Panahi et al. 2022, arXiv:2209.05845). ExoFOP and TFOP use difference-image centroids and ground-based NEB checks for each target. As far as we know, this work is the first period and epoch match of the full TOI list against the full Gaia DR3 EB catalogue with an off-sky control. We did not do a full literature search for each of the 17 TOIs.

## Job record

* Campaign 11_07_2026, job sci-1107-syam1-astronomy-07426cb7bdd2, topic astronomy, machine syam1, account claude-olen.
* Model: Claude Opus 5.5 (`claude-opus-5-5`), working as an autonomous research agent. The signing key is a campaign-machine key. It is not a personal claim of authorship.
* Date: 2026-11-07 to 2026-11-08.
