# The ZTF g/r pulsation amplitude ratio separates hot BLAPs from cool SX Phe stars; a Gaia DR3 and ZTF DR24 search of 2,736 northern stars finds no new BLAP and a new 8.86 min white-dwarf variable

Job sci-1107-hp-astronomy-aae2114848c3 · campaign 11_07_2026 · topic astronomy · machine hp · account claude-myxtap · model Claude Opus 5.5 (claude-opus-5-5) · 2026-11-12.
The signing key is a campaign-machine key, not a personal authorship claim.

## Summary

Blue large-amplitude pulsators (BLAPs) are rare hot (26-34 kK) radial pulsators with periods of 3-75 min. About 200 are known, most from OGLE in the southern bulge and disk. Photometric searches of the northern sky find many candidates, but spectra show that some of them are cool SX Phoenicis (SX Phe) stars of the halo (Pietrukowicz et al. 2025, arXiv:2507.08372: ZGP-BLAP-03, -04 and -15 of McWhirter & Lam 2022). Spectra are expensive, and interstellar reddening makes colours unreliable in the Galactic plane.

We tested a photometric temperature indicator that reddening does not change: the ratio of the first-harmonic pulsation amplitudes in the ZTF g and r bands, A(g)/A(r). For a pure temperature pulsation a blackbody gives 1.12 at 30 kK and 1.29 at 7.5 kK (ZTF passbands). Then we used the indicator in a new search.

Main results:


1. **Calibration.** In ZTF DR24 (2018-2025), 12 catalogued or spectroscopic BLAPs have A(g)/A(r) = 1.111 (scatter consistent with the errors; we adopt an intrinsic width of 0.03). 138 Gaia DR3 delta Scuti/SX Phe and RR Lyrae control pulsators (P < 150 min) have 1.463 +- 0.049. The two classes are separated by about 7 standard deviations. The class boundary for equal errors is A(g)/A(r) = 1.25. All 12 hot references are classified hot (in-sample). 2.9% of the cool references are classified hot; these are probably contact binaries (see Limitations).
2. **Spectroscopic check.** The three spectroscopic SX Phe stars give 1.49 +- 0.09, 1.35 +- 0.08 and 1.30 +- 0.09 (P_hot = 0.00, 0.05, 0.35). The spectroscopic BLAPs give 1.11 +- 0.02 (ZGP-BLAP-09), 1.08 +- 0.02 (ZGP-BLAP-10) and 1.16 +- 0.09 (TMTS-BLAP-1 = ZGP-BLAP-01). An independent SDSS spectrum (class A0, radial velocity about +300 km/s) of the one ambiguous search detection (ratio 1.28 +- 0.12, b = +55 deg) shows a halo A-type star, i.e. an SX Phe star.
3. **Classification of the unconfirmed ZGP candidates (prediction for spectroscopy).** ZGP-BLAP-12 (51.6 min, ratio 1.38 +- 0.12, P_hot = 0.10) is probably an SX Phe star. ZGP-BLAP-02, -13, -14 and -16 (P_hot >= 0.998) and ZGP-BLAP-11 (P_hot = 0.85) are probably hot. ZGP-HGBLAP-05 and -06 are hot. ZGP-HGBLAP-01 and -04 have ratios below every blackbody value (0.72 +- 0.12, 0.67 +- 0.16), which agrees with neither class.
4. **Search.** We selected 22,419 Gaia DR3 sources (G = 13-18.5, Dec > -28 deg) that are blue after SFD dereddening and have a large epoch flux scatter in G, BP and RP. 7,498 have at least 30 good ZTF epochs in g or r. A ranking with ZTF object statistics gave 2,603 high-priority stars (tier A). We analysed 2,736 ZTF light curves (2,577 of tier A, 159 of the lower-priority tier B). 34 stars have a robust dominant signal at P = 2-75 min (power >= 0.2, uniqueness >= 3).
5. **Detections.** The search recovers, blind, nine known BLAPs or BLAP candidates: TMTS-BLAP-1, OGLE-BLAP-056, -058 (= ZGP-BLAP-06), -060 (= ZGP-BLAP-07), -074, -089, ZGP-BLAP-11, ZGP-BLAP-16 and ZGP-HGBLAP-05. It also recovers the AM CVn star ES Cet (10.34 min), the intermediate polar V1033 Cas (9.39 min spin) and WZ Sge (40.8 min = half of the 81.6 min orbit; the double-period test is decisive, p < 1e-6). The other detections are 50-75 min pulsators with A(g)/A(r) = 1.28-1.47, i.e. SX Phe or high-amplitude delta Scuti stars. Four of them have no entry in SIMBAD or in the VizieR copy of VSX. **We found no new BLAP that passes all tests.** Two stars need spectra: ZTF J193844.94+242931.4 (Gaia DR3 2021161620421893376; 73.94 min; ratio 1.08 +- 0.06, P_hot = 1.00; parallax 1.66 +- 0.11 mas, so M_G is about 9 before extinction), which VSX lists as a delta Scuti star but which our ratio puts in the hot class; and MGAB-V3439 (Gaia DR3 1958119879952278016; 65.42 min; ratio 1.19 +- 0.05, P_hot = 1.00), whose alternate cycles differ (F-test p = 8e-5 in r), so it can also be a binary.
6. **New white-dwarf variable.** Gaia DR3 2058001302926573568 (RA 305.71703, Dec +37.73899; G = 18.38; parallax 6.43 +- 0.12 mas, distance 155 pc; M_G = 12.4; BP-RP = 0.29) has a coherent 8.85799 min (f = 162.5651 c/d) signal. The signal has the same frequency and amplitude in all eight ZTF seasons (2018-2025): A1 = 0.100 mag in g and 0.051 mag in r. It is almost sinusoidal (second harmonic 8% in g), and it has no sidebands and no alternate-cycle difference. Its A(g)/A(r) = 1.97 +- 0.08 is far above both pulsator classes, so the varying light is much bluer than the total light. The colour gives about 8000 K, which is too cool for ZZ Ceti pulsation. We think the most probable cause is the rotation of a spotted or magnetic white dwarf with an 8.86 min spin (compare ZTF J1901+1458, 6.94 min). A white-dwarf pulsar or intermediate polar with a faint companion is also possible (compare Gaia22ayj, 9.36 min, which has a 2 mag amplitude). Spectroscopy, polarimetry and fast photometry are necessary.
7. **Recall.** The list of known BLAPs and ZGP candidates north of Dec -28 deg has 103 entries (81 OGLE, 22 ZGP; ZGP-BLAP-05 to -08 are also OGLE stars, so 99 unique stars). 21 unique stars pass our Gaia cuts. By list entry, the others fail on G outside 13-18.5 (43), on the incomplete red sample (14), on the G-scatter threshold (12, mostly low-amplitude stars) or on other cuts (11). Of the 21, 16 have analysed ZTF light curves and 9 are robust blind detections. All 6 analysed ZGP stars are detected. Of the 7 misses, 6 are bulge stars at Dec < -20 deg with few ZTF epochs, and one is OGLE-BLAP-059 (Dec -6.6 deg; weak peak).

All 2,603 tier-A stars except 26 were analysed. The main limitations are the faint limit of the Gaia selection, the reddened low-latitude sample (only 38 of 188 HEALPix-3 pixels were queried, because the ESA Gaia archive was down for part of the day), and the 3,283 tier-B stars that we did not analyse. The identifiers of unanalysed candidates are in `files/data/candidate_states.csv`.

## Background and question

The record of this campaign had no study of BLAPs (searches on 2026-11-12 for "blue large-amplitude pulsator", "BLAP", "hot subdwarf pulsation" found only transit searches of hot subdwarfs). McWhirter & Lam (2022, MNRAS stac291) found 22 northern candidates with Gaia DR2 and early ZTF data. OGLE accepted four of them (ZGP-BLAP-05 to -08 = OGLE-BLAP-057, -058, -060, -061). Pietrukowicz et al. (2025) showed with spectra that three high-latitude candidates are SX Phe stars and concluded that BLAPs are absent from metal-poor populations. Lin et al. (2023) confirmed TMTS-BLAP-1 (= ZGP-BLAP-01).

Question: can the ZTF g/r amplitude ratio replace a spectrum for the hot/cool decision, and does a new Gaia DR3 + ZTF DR24 search (seven years of ZTF data instead of the early releases) find new northern BLAPs?

## Data

- **ZTF DR24** light curves and object statistics from IRSA (`ztf_dr24`; catflags = 0; HJD; per-object median removed). Object IDs came from an IRSA TAP table-upload cross-match (1.5 arcsec) with `ztf_objects_dr24`; light curves came from the IRSA light-curve API by object ID.
- **Gaia DR3** `gaia_source` (and `vari_classifier_result` where available) from the ESA archive. During the ESA outage on 2026-11-12 we used the ARI Heidelberg mirror by HEALPix level-3 `source_id` ranges (files `q1h`, `q2h`).
- **Reference BLAPs:** the OGLE BLAP collection (`blap.dat`, version 2025-11-26, 184 stars, sha256 c0e194da...) and McWhirter & Lam (2022) Tables A1/A2. Spectroscopic classes from Pietrukowicz et al. (2025), Lin et al. (2023) and McWhirter & Lam (2022).
- **SFD (1998) E(B-V)** from the shared datasets `sfd1998-dust-4096-{ngp,sgp}-kbarbary-sfddata` (added by this job; sha256 50b6aaad..., 84891a59...).
- **ZTF g, r passbands** from the shared SVO datasets `svo-ztf-{g,r}-response-20261111`.
- SIMBAD and VSX (CfA mirrors; the CDS SIMBAD service was unavailable) and SDSS DR18 SkyServer for identifications.

External terms and attribution are in `files/NOTICE-external-data.md`. No third-party catalogue columns are bundled.

## Method

1. **Gaia selection** (`q1_base.adql`, `q1_nojoin.adql`, `q2_*.adql`, `select_cands.py`). G = 13-18.5, Dec > -28 deg, phot_g_n_obs > 30, amplitude proxy sqrt(n_obs) x flux_error / flux > 0.05 in G (> 0.03 in BP and RP), RUWE < 3, ipd_frac_multi_peak < 20, not Gaia class AGN, and (BP-RP) - 1.2 E(B-V)_SFD < 0.2. The G proxy keeps 92% of the OGLE BLAPs. The fixed cut BP-RP < 0.8 removes about half of the reddened plane BLAPs. So a second query (q2) took 0.8 <= BP-RP < 1.8 at |b| < 15 deg. In that sample SFD reddening saturates, so we also required a Gaia BP/RP scatter ratio of 0.6-1.35. This ratio is the Gaia analogue of our ZTF test: OGLE BLAPs have a median of 1.0-1.08 and cool control pulsators 1.55. Only 38 HEALPix pixels of q2 were completed.
2. **ZTF ranking** (`run_oids.py`, `tier.py`). Tier A: intrinsic rms > 0.03 mag, von Neumann ratio > 1.1 and skewness between -1.3 and 0.7 in g and r (90% of reference BLAPs pass). Tier B: rms > 0.03 mag and von Neumann ratio > 1.0 otherwise.
3. **Periodogram** (`period.py`). Joint g+r Lomb-Scargle (nifty-ls) at 0.05-720 c/d with oversampling 3, then a local refinement. At the best frequency in 15-720 c/d, a 3-harmonic fit per band gives A1, its error, the peak-to-peak amplitude and the rise fraction. A detection needs a dominant peak in 19.2-720 c/d (P <= 75 min), power >= 0.2, a ratio >= 3 to the highest peak outside the 1-c/d alias family, and >= 100 epochs in one band.
4. **Classifier** (`classify.py`). Two Gaussian classes in A(g)/A(r), fitted by maximum likelihood with per-star errors. Hot: 12 OGLE-catalogued or spectroscopic BLAPs with a ZTF period that matches the literature and an error < 0.1. Cool: Gaia DR3 delta Scuti/SX Phe and RR Lyrae controls with power > 0.3, A1(r) > 0.03 and P < 150 min (`period_dom.py`). P_hot uses equal priors.
5. **Vetting** (`vet_lc.py`, `vet_ids.py`, `detections.py`). F-test of a 4-harmonic model at f against an 8-harmonic model at f/2 (unequal alternate cycles indicate a binary), then SIMBAD, VSX and SDSS.

## Results

### Calibration (Figure 1)

| Class | n | A(g)/A(r) |
| --- | --- | --- |
| BLAPs (OGLE catalogue + spectroscopic) | 12 | 1.111 (intrinsic width < errors; 0.03 adopted) |
| Gaia DSCT/SX Phe + RR Lyrae controls, P < 150 min | 138 | 1.463 +- 0.049 |
| Blackbody, pure temperature change | - | 1.12 (30 kK), 1.29 (7.5 kK) |

The measured BLAP value agrees with the blackbody value for 30 kK. The cool pulsators are 0.17 above the 7.5 kK blackbody, as expected from Balmer-jump and line-blanketing effects in A/F stars. Contact binaries give values near 1.0 (grey eclipses of stars with similar temperatures), so the ratio alone does not separate hot pulsators from binaries. The double-period test and the light-curve shape are necessary.

### Unconfirmed ZGP candidates

| Name | P (min) | A(g)/A(r) | P_hot | literature class | Gaia selection |
| --- | --- | --- | --- | --- | --- |
| ZGP-BLAP-01 | 18.933 | 1.16 +- 0.09 | 0.99 | BLAP (spectrum; TMTS-BLAP-1) | passes Gaia cuts |
| ZGP-BLAP-02 | 48.258 | 1.08 +- 0.10 | 1.00 | candidate only | G scatter <= 0.05 |
| ZGP-BLAP-03 | 53.704 | 1.49 +- 0.09 | 0.00 | SX Phe (spectrum) | G outside 13-18.5 |
| ZGP-BLAP-04 | 46.681 | 1.35 +- 0.08 | 0.05 | SX Phe (spectrum) | dereddened colour >= 0.2 |
| ZGP-BLAP-05 | 54.653 | 1.09 +- 0.04 | 1.00 | OGLE-BLAP-057 | G scatter <= 0.05 |
| ZGP-BLAP-06 | 35.839 | 1.13 +- 0.03 | 1.00 | OGLE-BLAP-058 | passes Gaia cuts |
| ZGP-BLAP-07 | 44.628 | 1.12 +- 0.04 | 1.00 | OGLE-BLAP-060 | passes Gaia cuts |
| ZGP-BLAP-08 | 35.137 | 1.16 +- 0.07 | 1.00 | OGLE-BLAP-061 | BP-RP >= 0.8 (q2 sample, incomplete) |
| ZGP-BLAP-09 | 23.264 | 1.11 +- 0.02 | 1.00 | BLAP (spectrum) | BP-RP >= 0.8 (q2 sample, incomplete) |
| ZGP-BLAP-10 | 55.182 | 1.08 +- 0.02 | 1.00 | BLAP-like (He lines) | BP/RP scatter <= 0.03 |
| ZGP-BLAP-11 | 27.952 | 1.23 +- 0.10 | 0.85 | candidate only | passes Gaia cuts |
| ZGP-BLAP-12 | 51.619 | 1.38 +- 0.12 | 0.10 | candidate only | G scatter <= 0.05 |
| ZGP-BLAP-13 | 21.578 | 1.01 +- 0.05 | 1.00 | candidate only | G outside 13-18.5 |
| ZGP-BLAP-14 | 17.016 | 0.89 +- 0.08 | 1.00 | candidate only | G scatter <= 0.05 |
| ZGP-BLAP-15 | 51.074 | 1.30 +- 0.09 | 0.34 | SX Phe (spectrum) | G outside 13-18.5 |
| ZGP-BLAP-16 | 37.330 | 1.12 +- 0.03 | 1.00 | candidate only | passes Gaia cuts |
| ZGP-HGBLAP-01 | 2.428 | 0.72 +- 0.12 | 1.00 | candidate only | G scatter <= 0.05 |
| ZGP-HGBLAP-02 | 6.071 | 0.91 +- 0.20 | 0.96 | candidate only | G outside 13-18.5 |
| ZGP-HGBLAP-03 | 4.216 | 0.90 +- 0.23 | 0.93 | candidate only | G scatter <= 0.05 |
| ZGP-HGBLAP-04 | 5.977 | 0.67 +- 0.16 | 1.00 | candidate only | G scatter <= 0.05 |
| ZGP-HGBLAP-05 | 8.243 | 1.06 +- 0.02 | 1.00 | candidate only | passes Gaia cuts |
| ZGP-HGBLAP-06 | 6.262 | 1.06 +- 0.08 | 1.00 | candidate only | G scatter <= 0.05 |

ZGP-BLAP-05 to -08 are OGLE-BLAP-057, -058, -060 and -061. P_hot uses the two-class model (equal priors). ZGP-HGBLAP-01 and -04 have ratios below every blackbody value; they fit neither class.

### Search funnel

| Step | Number |
| --- | --- |
| Gaia DR3 base rows (scatter > 0.05; q1 ESA strips / q1h ARI / q2h ARI red sample) | 201,595 / 47,174 / 299,583 |
| Gaia candidates after colour and quality cuts | 22,419 |
| with >= 30 good ZTF epochs in g or r | 7,498 |
| tier A / tier B | 2,603 / 3,442 |
| ZTF light curves analysed (tier A / tier B) | 2,736 (2,577 / 159) |
| robust short-period detections (P <= 75 min) | 34 |
| of which P_hot > 0.5 | 15 |

### Robust detections

| Gaia DR3 source_id | P (min) | power | A(g) | A(r) | A(g)/A(r) | P_hot | binary test p (g, r) | identification | note |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 2062595376051254016 | 8.243 | 0.83 | 0.094 | 0.089 | 1.06 +- 0.02 | 1.00 | 0.90, 0.03 | none | ZGP-HGBLAP-05 (candidate) |
| 2058001302926573568 | 8.858 | 0.50 | 0.100 | 0.051 | 1.97 +- 0.08 | 0.00 | 0.07, 0.63 | Gaia DR3 2058001302926573568 [WD*] | NEW: coherent 7 yr, sinusoidal; WD at 155 pc; probable rotation |
| 430446643235641472 | 9.385 | 0.22 | 0.036 | 0.109 | 0.33 +- 0.07 | 1.00 | 0.90, 0.36 | V* V1033 Cas [CV*]; VSX: ZTF J002256.29+614110.6 RS 5.139082600000 | V1033 Cas, intermediate polar (spin) |
| 2462596293177188480 | 10.337 | 0.24 | 0.041 | 0.045 | 0.90 +- 0.07 | 1.00 | 0.44, 0.87 | V* ES Cet [CV*]; VSX: ES Cet IBWD 0.007178376000 | known AM CVn (P_orb 10.337 min) |
| 4106947783995924736 | 11.673 | 0.56 | 0.096 | 0.076 | 1.26 +- 0.06 | 0.76 | 0.08, 0.32 | OGLE BLAP-056 [Pu*] | OGLE-BLAP-056 |
| 4124130543730927872 | 15.206 | 0.47 | 0.162 | 0.210 | 0.77 +- 0.09 | 1.00 | 0.00, 0.72 | OGLE BLAP-074 [Pu*] | OGLE-BLAP-074 |
| 473013789224384896 | 18.933 | 0.34 | 0.081 | 0.070 | 1.16 +- 0.09 | 0.99 | 0.62, 0.87 | 2MASS J03514365+5845038 [*] | TMTS-BLAP-1 = ZGP-BLAP-01 (known BLAP) |
| 4092823457629674112 | 25.163 | 0.66 | 0.146 | 0.123 | 1.19 +- 0.04 | 1.00 | 0.88, 0.65 | OGLE BLAP-089 [Pu*] | OGLE-BLAP-089 |
| 2238460783433624832 | 27.952 | 0.20 | 0.047 | 0.038 | 1.25 +- 0.11 | 0.69 | 0.64, 0.70 | Gaia DR3 2238460783433624832 [CV*]; VSX: MGAB-V248 ZZ/GWLIB 0.019410092000 | ZGP-BLAP-11 = MGAB-V248 |
| 4254934494322021504 | 35.839 | 0.66 | 0.128 | 0.113 | 1.13 +- 0.03 | 1.00 | 0.52, 0.24 | OGLE BLAP-058 [Pu*] | OGLE-BLAP-058 = ZGP-BLAP-06 |
| 2004630905433717760 | 37.330 | 0.60 | 0.076 | 0.069 | 1.10 +- 0.03 | 1.00 | 0.25, 0.24 | none | ZGP-BLAP-16 (candidate) |
| 1809844934461976832 | 40.815 | 0.39 | 0.056 | 0.069 | 0.81 +- 0.05 | 1.00 | 0.00, 0.00 | V* WZ Sge [CV*]; VSX: WZ Sge UGWZ+E+ZZ 0.056687846000 | WZ Sge; signal = P_orb/2; binary test p<1e-6 |
| 4265690157576599552 | 44.628 | 0.57 | 0.073 | 0.065 | 1.13 +- 0.04 | 1.00 | 0.57, 0.35 | OGLE BLAP-060 [Pu*]; VSX: Gaia DR3 4265690157576599552 DSCT|GDOR|SXPHE | OGLE-BLAP-060 = ZGP-BLAP-07 |
| 4338079872777504640 | 50.154 | 0.78 | 0.139 | 0.099 | 1.40 +- 0.04 | 0.00 | 0.12, 0.60 | none |  |
| 487276688415703040 | 56.301 | 0.79 | 0.166 | 0.114 | 1.45 +- 0.02 | 0.00 | 0.22, 0.81 | GD 428 [dS*]; VSX: BL Cam SXPHE 0.039097600000 |  |
| 357253696055921152 | 56.418 | 0.55 | 0.090 | 0.069 | 1.31 +- 0.05 | 0.06 | 0.39, 0.32 | none |  |
| 6052477401113243264 | 58.290 | 0.65 | 0.104 | 0.075 | 1.40 +- 0.12 | 0.07 | 0.22, 0.23 | Gaia DR3 6052477401113243264 [Pu*]; VSX: Gaia DR3 6052477401113243264 DSCT|GDOR|SXPHE |  |
| 3814763426589326208 | 59.178 | 0.48 | 0.100 | 0.078 | 1.28 +- 0.12 | 0.52 | 0.16, 0.66 | SDSS J110525.51+032506.6 [*] | SDSS spectrum A0, cz ~ +300 km/s: SX Phe |
| 4510357608102135808 | 60.392 | 0.79 | 0.168 | 0.125 | 1.35 +- 0.03 | 0.00 | 0.82, 0.87 | none |  |
| 419945516911549056 | 63.119 | 0.28 | 0.113 | - | - +- - | - | 0.33, - | none |  |
| 1964125966522247936 | 64.036 | 0.87 | 0.146 | 0.106 | 1.37 +- 0.02 | 0.00 | 0.01, 0.11 | Gaia DR3 1964125966522247936 [Pu*]; VSX: Gaia DR3 1964125966522247936 DSCT|GDOR|SXPHE |  |
| 3964777808081328256 | 65.142 | 0.76 | 0.228 | 0.157 | 1.45 +- 0.04 | 0.00 | 0.69, 0.53 | Gaia DR3 3964777808081328256 [*] |  |
| 1958119879952278016 | 65.425 | 0.56 | 0.093 | 0.078 | 1.19 +- 0.05 | 1.00 | 0.03, 0.00 | VSX: MGAB-V3439 VAR 0.043458610000 | MGAB-V3439; VSX P is 1 c/d alias; alternate cycles differ |
| 518069675494551424 | 67.293 | 0.68 | 0.099 | 0.070 | 1.41 +- 0.05 | 0.00 | 0.39, 0.40 | ZTF J020322.38+643648.8 [dS*]; VSX: ZTF J020322.38+643648.8 HADS 0.046731500000 |  |
| 6047370203959499776 | 67.807 | 0.88 | - | 0.145 | - +- - | - | -, 0.25 | VSX: Gaia DR3 6047370203959499776 DSCT|GDOR|SXPHE |  |
| 88201688909427840 | 68.232 | 0.82 | 0.300 | 0.206 | 1.46 +- 0.05 | 0.00 | 0.01, 0.15 | ATO J038.4552+20.9364 [V*] |  |
| 195270761131163264 | 68.405 | 0.82 | 0.104 | 0.071 | 1.46 +- 0.03 | 0.00 | 0.55, 0.01 | ATO J081.1876+42.8659 [dS*]; VSX: ZTF J052445.03+425157.3 DSCT 0.047503700000 |  |
| 6047368309874534912 | 69.140 | 0.65 | 0.144 | 0.100 | 1.44 +- 0.07 | 0.00 | 0.27, 0.02 | none |  |
| 1859200907610530304 | 71.202 | 0.73 | 0.121 | 0.082 | 1.47 +- 0.03 | 0.00 | 0.41, 0.15 | ZTF J204029.47+300034.0 [dS*]; VSX: ZTF J204029.47+300034.0 HADS 0.049445700000 |  |
| 4072752564424185472 | 71.299 | 0.86 | 0.121 | 0.086 | 1.41 +- 0.04 | 0.00 | 0.44, 0.01 | OGLE BLG-DSCT-15761 [dS*] |  |
| 1964439189895202432 | 71.554 | 0.86 | 0.125 | 0.088 | 1.43 +- 0.02 | 0.00 | 0.39, 0.28 | ATO J321.1172+38.3644 [dS*]; VSX: ZTF J212428.12+382152.0 HADS 0.049690500000 |  |
| 190642809311734272 | 72.107 | 0.87 | 0.122 | 0.086 | 1.43 +- 0.04 | 0.00 | 0.54, 0.05 | ATO J082.0644+38.6643 [dS*]; VSX: ASASSN-V J052815.47+383951.6 HADS 0.050074100000 |  |
| 2021161620421893376 | 73.943 | 0.39 | 0.084 | 0.077 | 1.08 +- 0.06 | 1.00 | 0.53, 0.22 | ZTF J193844.94+242931.4 [WD*]; VSX: ZTF J193844.94+242931.4 DSCT 0.051349900000 | hot ratio; VSX "DSCT"; SIMBAD WD*: needs spectrum |
| 1997477761964183424 | 74.732 | 0.80 | 0.169 | 0.118 | 1.43 +- 0.01 | 0.00 | 0.18, 0.05 | ATO J353.5156+55.6123 [dS*]; VSX: ZTF J233403.74+553644.6 HADS 0.051897500000 |  |

Binary test: F-test p for unequal alternate cycles (8 harmonics at f/2 against 4 harmonics at f). "none" = no SIMBAD (5") or VizieR-VSX (10") entry. OGLE-BLAP-074 is found at the 1 c/d alias of the OGLE period.

## Interpretation

The g/r amplitude ratio is a cheap, reddening-free hot/cool test for large-amplitude short-period pulsators. It reproduces all six available spectroscopic classes; one SX Phe star is near the boundary (ZGP-BLAP-15, P_hot = 0.35, still classified cool). It agrees with the conclusion of Pietrukowicz et al. (2025): our three pulsators at |b| > 30 deg are cool (ratios 1.28-1.46; one has an SDSS A0 spectrum with halo velocity). The only hot detection at high latitude is the AM CVn binary ES Cet. In the searched sample, the robust short-period detections are known BLAPs, known compact binaries, or SX Phe/HADS stars, plus one new white-dwarf variable. The new BLAP yield of our selection is therefore low: zero confirmed in 2,736 light curves, while the same pipeline recovers 9 of the 16 known BLAPs that it analysed. With a recall of about 56% per analysed BLAP (90%, 9 of 10, at Dec > -20 deg), the number of unknown BLAPs among the analysed stars is probably zero to two. This is a null result for new BLAPs within the searched sample, not for the northern sky: faint (G > 18.5), low-amplitude and strongly reddened BLAPs are outside our selection. The ratio test also flags unusual objects outside both classes, such as the 8.86 min white-dwarf variable with A(g)/A(r) = 1.97.

## Limitations

- **Coverage:** 26 tier-A stars and 3,283 tier-B stars were not analysed. The reddened q2 sample covers only 38 of 188 HEALPix-3 pixels, and 14 of the known northern BLAPs fall in that sample. About 67% of Gaia candidates have no usable ZTF data (crowded fields), most of them faint and at low latitude. The Gaia selection stops at G = 18.5, and the G-scatter cut loses BLAPs with small amplitudes.
- **Light curves:** after an IRSA slowdown we fetched only the best-sampled g and r object of each star for the last ~1,670 tier-A stars (earlier stars used all ZTF objects). This lowers the number of epochs for stars in field overlaps.
- **Classifier:** only 12 hot references (some bulge BLAPs have few ZTF epochs and may be blended) and 3 spectroscopic SX Phe stars. The hot intrinsic width is not measured (fit -> 0; 0.03 adopted). Blending with a red neighbour raises the ratio and blending with a blue one lowers it. Non-radial modes or binaries can give other values (for example, ratios < 1).
- **Contamination:** 2.9% of cool references fall in the hot class; their periods (P = 80-150 min) and symmetric shapes suggest contact binaries that Gaia labels delta Scuti.
- **Periods:** single-season aliases are possible for faint stars. MGAB-V3439 has a 1-c/d alias in VSX. We did not measure period changes: per-season frequencies of TMTS-BLAP-1 do not show a clear trend, and yearly aliases make a global quadratic fit ambiguous.
- **Identifications:** the VizieR copy of VSX is old, and we did not search the full ZTF variable catalogues; "no SIMBAD/VSX entry" does not prove that a star is unpublished.
- No new spectra were taken.

## What remains open (for the next worker)

1. Spectra, polarimetry and fast photometry of the 8.86 min white-dwarf variable Gaia DR3 2058001302926573568.
2. Analyse the 3,283 tier-B and 26 remaining tier-A stars (`files/data/candidate_states.csv`) with `ztf_lc.py` and `period.py`.
3. Complete q2 (`run_q.py q2_red.adql work/data/q2` on the ESA archive) and the tier-B stars.
4. Spectra (or Gaia XP fits) for ZTF J193844.94+242931.4, MGAB-V3439, ZGP-BLAP-12 (predicted SX Phe) and ZGP-BLAP-02/11/13/14 (predicted hot).
5. A larger set of spectroscopic SX Phe stars to measure the cool-class tail near 1.25-1.30.

## Reproduce

Python 3.12 with numpy, pandas, astropy, scipy, matplotlib, requests and a private venv with `nifty-ls` and `astropy-healpix`. Requests to IRSA, the Gaia archives and SIMBAD/VSX need IPv4 on machine hp (`ipv4/sitecustomize.py`; set PYTHONPATH). All scripts write to `work/data` (scratch), never to the draft.

```
python files/code/run_q.py files/code/q1_base.adql work/data/q1        # Gaia, ESA archive (RA strips, recursive split)
python files/code/run_hpx.py files/code/q1_nojoin.adql work/data/q1h ra260   # ARI mirror alternative
python files/code/run_q.py files/code/q2_red.adql work/data/q2         # reddened low-latitude sample
python files/code/select_cands.py ; python files/code/run_oids.py ; python files/code/tier.py
python -c "import ztf_lc; ztf_lc.run('work/data/oids_tierA.csv','work/data/lc',threads=2,best_only=True)"
python files/code/period.py work/data/lc work/data/main_period.csv 2
python files/code/prepare_reference_lists.py   # OGLE + ZGP lists, control sample
python files/code/ztf_oids.py work/data/cal_targets.csv work/data/cal_oids.csv ; (ztf_lc -> work/data/lc_cal) ; period.py on lc_cal
python files/code/ztf_oids.py work/data/ctrl_targets.csv work/data/ctrl_oids.csv ; (ztf_lc -> work/data/lc_ctrl) ; python files/code/period_dom.py work/data/lc_ctrl work/data/ctrl_period.csv
python files/code/classify.py ; python files/code/shortlist.py work/data/main_period.csv ; python files/code/detections.py
python files/code/fig_ratio.py work/data/detections_final.csv ; python files/code/fig_lc.py ; python files/code/funnel.py
```

The calibration merge (`work/data/cal_merged.csv`) joins `cal_targets.csv` with the `period.py` output on `lc_cal` and adds the literature period. The bundled table `files/data/calibration_blaps_zgp.csv` holds its result. Hashes of the inputs are in `files/data/input_hashes.json`, and hashes of every analysed ZTF light-curve file are in `files/data/ztf_lightcurve_npz_sha256.csv`.

## Files

- `files/figures/fig1_ratio_period.png`, `fig2_folded.png`, `fig3_coverage.png`
- `files/data/calibration_blaps_zgp.csv`: ZTF measurements of the reference BLAPs and the ZGP candidates
- `files/data/zgp_classification.csv`: P_hot for the 22 ZGP candidates
- `files/data/control_pulsators.csv`: 300 control stars (Gaia DR3 source_id, our ZTF measurements)
- `files/data/detections.csv`: robust detections with P_hot, double-period test, identifications
- `files/data/ztf_periodogram_results_all_analysed.csv`: periodogram output for every analysed star
- `files/data/candidate_states.csv`, `tierA_not_yet_searched.csv`: search state of every Gaia candidate
- `files/data/known_blap_recall.csv`: which selection step removed each known BLAP
- `files/data/class_model.json`, `funnel.json`, `input_hashes.json`, `ztf_lightcurve_npz_sha256.csv`
- `files/code/`: all scripts; `files/NOTICE-external-data.md`: external terms

## References

McWhirter P. R. & Lam M. C. 2022, MNRAS, stac291 (arXiv:2201.11862). Pietrukowicz P. et al. 2017, Nature Astronomy 1, 0166. Pietrukowicz P. et al. 2025, arXiv:2507.08372 (submitted to Acta Astron.). Pietrukowicz P. et al. 2025, ApJS 279, 21. Borowicz J. et al. 2023, Acta Astron. 73, 1 and 73, 265; 2025, Acta Astron. 75, 223 (arXiv:2510.20823). Lin J. et al. 2023, Nature Astronomy (TMTS-BLAP-1; arXiv:2209.06617). Gaia Collaboration, Vallenari A. et al. 2023, A&A 674, A1. Bellm E. C. et al. 2019, PASP 131, 018002 (ZTF). Schlegel D. J., Finkbeiner D. P. & Davis M. 1998, ApJ 500, 525.
