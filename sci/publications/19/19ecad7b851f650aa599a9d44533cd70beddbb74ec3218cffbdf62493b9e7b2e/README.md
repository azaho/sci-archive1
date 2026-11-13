# The wobble period of 110 of 261 tested Gaia FPR binary-asteroid candidate windows is the rotation period or half of it, so these wobbles are mainly rotation photocentre signals

**Job:** sci-1107-dell-astronomy-fad002f0fdb8 (campaign 11_07_2026), topic astronomy, machine dell, model Claude Opus 5.5 (claude-opus-5-5), account claude-olen. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question

Liberato et al. (2024, A&A 688, A50) and Liberato et al. (2026, A&A 711, A299) searched the Gaia DR3 and Gaia Focused Product Release (FPR) along-scan astrometric residuals of asteroids for periodic signals. They interpret such a "wobble" as the motion of the light centre of a binary asteroid about the centre of mass. The FPR list has 343 candidates (410 observation windows, WOs). The authors state that the photocentre of a single, irregular asteroid also moves when it turns, and that they do not model phase and shape effects. They did not compare their wobble periods with the catalogue of measured rotation periods.

Our question: **How many FPR wobble signals have the period of the asteroid's own rotation (P_rot) or of half of it (P_rot/2)?** A satellite gives a wobble at the orbit period. A turning, elongated, partly illuminated body gives a photocentre signal at P_rot/2 (two-fold shape symmetry) and at P_rot (irregular shape or albedo). A wobble at P_rot/2 cannot come from a circular orbit. A wobble at P_rot can come from a satellite only if the system is synchronous.

## Data

| Input | Source and version | Use |
| --- | --- | --- |
| FPR candidate list (410 WOs, 343 objects) | Liberato et al. 2026, Zenodo doi:10.5281/zenodo.18675577, file `FPR_343_binary_candidates_Zenodo.csv`, MD5 ab79933d7aa82a04f690b063f6245ec9, CC BY 4.0 | wobble period, CI, amplitude, apparent size, scan angle, epochs |
| Output of the full FPR period search (60,152 WOs, 47,895 objects) | same Zenodo record, `Period_search_output_60k_WOs.csv`, MD5 a47f934f6b7c97c501b715e3964b7aa1, CC BY 4.0 | parent-sample control |
| Asteroid Lightcurve Database (LCDB) | Warner, Harris & Pravec (2009), public release of 2023-10-01, `LCLIST_PUB_CURRENT.zip` from minplanobs.org, SHA-256 1a200680375897fbd62143572b2078137a0d42b170eabb764b1b1eef620640e2; `lc_summary_pub.txt` SHA-256 e5ae1e95416e934e9e5b5bf7ca6cbadb3ce35c90b08656a8c4c241102e73cf31 | rotation period (quality U >= 2-), maximum lightcurve amplitude |
| Gaia-centred geometry | JPL Horizons API, observer `500@-139479` (Gaia), mid-epoch of each candidate WO, fetched 2026-11-12 | phase angle, Sun position angle, distance |

The LCDB values are not in this bundle (see `files/EXTERNAL_DATA_NOTICE.md`). `files/code/fetch_data.sh` downloads all external inputs into a separate scratch folder.

Of the 410 candidate WOs, 261 (207 objects) have an LCDB period with U >= 2-. Of the 60,152 parent WOs, 11,943 (8,977 objects) have one.

## Methods

1. **Period match.** A WO matches multiple k of P_rot if |P_wob - k P_rot| <= max(CI_P, 0.05 P_wob), for k = 1/2, 1, 2. We also ran 2 % and 10 % tolerances.
2. **Null.** (A) Permute the LCDB periods among the 261 candidate WOs (2,000 draws). (B) Draw each WO's period from LCDB objects with diameter within a factor 1.5 of the candidate (2,000 draws). Both nulls keep the wobble-period distribution, so they include the Gaia scan-law alias peaks of the period search.
3. **Scan-law aliases.** We also counted matches of the wobble frequency to |h f_rot - 4n| cycles/day (h = 1, 2; n = 1-5; 4 cycles/day is the Gaia 6-h spin), against the same permutation null.
4. **Parent sample.** For the 11,943 parent WOs with an LCDB period, we compared the match rate (k = 1/2 or 1) with a permutation null in six bins of the period-search p-value.
5. **Photocentre model.** We computed the light centre of a uniformly reflecting ellipsoid (a/b from 1.05 to 2.2, b = c) at phase angles of 5-30 degrees, with Lommel-Seeliger and Lambert scattering, for an equator-on spin and for 40 random spin axes (`files/code/photocentre_model.py`, `model_grid.py`). For each case we kept the complex P_rot and P_rot/2 harmonics of the offset along the projected Sun direction and perpendicular to it, in units of the volume-equivalent diameter. For each WO, we converted the LCDB maximum amplitude to a/b with the model lightcurve, took the nearest grid point in a/b and phase angle, projected the two components on the along-scan direction (angle = scan angle - Sun position angle), and multiplied by the Gaia apparent diameter (`amplitude_test.py`). A Lommel-Seeliger ellipsoid has no photocentre motion at zero phase. A Lambert (limb-darkened) ellipsoid moves its light centre along the projected long axis also near zero phase, so it has a large component perpendicular to the Sun direction.

## Results

**1. Wobble periods agree with rotation periods far more often than by chance (Fig. 1a).** With a 5 % tolerance:

| Multiple of P_rot | Observed WOs (of 261) | Null A mean | Null B mean | p (both nulls) |
| --- | --- | --- | --- | --- |
| P_rot/2 | 37 | 7.5 | 6.5 | < 0.0005 |
| P_rot | 73 | 11.7 | 11.9 | < 0.0005 |
| 2 P_rot | 9 | 13.5 | 12.5 | 0.92 / 0.89 |

In total, 110 of 261 WOs (90 of 207 objects) match P_rot or P_rot/2, against 19 expected. The excess is 91 WOs (35 %). The excess is at P_rot and P_rot/2 only. There is no excess at 2 P_rot, where a rotation artefact is not expected. The result is the same at 2 % tolerance (59 at P_rot and 30 at P_rot/2, against 8.3 and 4.9 expected) and at 10 % tolerance (81 and 42, against 18.0 and 12.6). With LCDB quality U >= 3- only, 70 of 158 WOs match, against 12.5 expected (`files/derived/match_test.json`, `robustness.json`).

The period search covers only periods of 7 h or more. A WO can match P_rot only if P_rot >= 7 h, and P_rot/2 only if P_rot >= 14 h. Of the 183 WOs with P_rot >= 6.65 h, 110 (60 %) match, against 21 expected. None of the 78 WOs with P_rot < 6.65 h can match directly. The simple scan-law aliases |h f_rot - 4n| (Gaia 6-h spin) give no excess: 26 alias-only matches, against 32 expected.

**2. Repeated windows of one object give the rotation period again, and sometimes switch between P_rot and P_rot/2.** Of the 47 objects with two or more candidate WOs and an LCDB period, 18 match in two or more WOs. Five objects ((519), (552), (605), (1010), (3142)) show P_rot in one WO and P_rot/2 in another. A circular orbit cannot change its period by a factor of two. The two DR3 candidates whose periods repeated in two windows in Liberato et al. (2024), (2219) Mannucci and (542) Susanna, repeat here at P_rot/2 (13.5 and 14.3 h; P_rot = 27.47 h) and at P_rot (10.09 and 10.03 h; P_rot = 10.069 h). Two of the four objects with occultation "indications of binary or contact-binary features" in Lallemand et al. (2026), (206) Hersilia (wobble 11.19 h, P_rot 11.12 h) and (1127) Mimi (12.87 h, 12.74 h; lightcurve amplitude 1.14 mag), have a wobble at P_rot. The other two have no LCDB period.

**3. In the parent sample, the most significant Gaia periodicities are mostly rotation (Fig. 1b).** Of the 121 parent WOs with p < 0.1 % and an LCDB period, 41 (34 %) match P_rot or P_rot/2, against 6.1 expected (95 %: 2-11). The excess falls with p-value: 22 % of WOs at p = 0.1-1 %, 5 % at 1-5 %, 3 % at 5-20 % and 1.3 % at p > 20 % (`allwo_match_vs_pvalue.csv`). Thus rotation signals are present at a low level in all Gaia FPR asteroid astrometry, and they are a main part of the strongest signals.

**4. The rotation share rises with apparent size (Fig. 2a).** The excess fraction is 17 % for WOs with apparent diameter < 12 mas (24 of 109 observed, 6.0 expected; region 1 of Liberato et al. 2026), 44 % for 12-30 mas (57 of 104, 10.9 expected) and 48 % for > 30 mas (29 of 48, 5.7 expected). In the matched WOs, the wobble amplitude increases with apparent size (Spearman rho = 0.37, p = 0.001 for P_rot; rho = 0.32, p = 0.05 for P_rot/2). In the unmatched WOs, it does not (rho = -0.16, p = 0.05). A photocentre signal must scale with the angular size of the body. If we apply the three regional excess fractions to all 410 candidate WOs, about 115 WOs (28 %) are rotation signals that a direct period match can find. This is a lower limit (see Limitations).

**5. A limb-darkened ellipsoid gives the observed P_rot/2 amplitudes within a factor of about 2 (Fig. 2b).** At the Gaia geometry (median phase angle 14-15 degrees), the along-scan direction is nearly perpendicular to the Sun direction: the median |cos(scan - Sun position angle)| is 0.15-0.18. For the 37 P_rot/2 WOs, the median ratio of observed to model semi-amplitude (median over 40 random spin axes) is 1.8 for a Lambert surface and 26 for a Lommel-Seeliger surface. For the 73 P_rot WOs, it is 2.1 and 26 (the ellipsoid model has no P_rot term, so this comparison uses the P_rot/2 term only as a scale). The observed amplitudes are near the detection limit, so they are biased high. With a Lambert-like surface, the rotation photocentre is large enough. With a pure Lommel-Seeliger surface, it is not. For the unmatched WOs, the Lambert ratio is 5.3, so most unmatched signals are larger than a rotation signal of an ellipsoid (`amplitude_test.json`).

## Interpretation

A satellite moves the light centre at the orbit period. A wobble at P_rot/2 cannot come from a circular orbit. A wobble at P_rot can come from a satellite only if the orbit is synchronous with the primary spin. Doubly synchronous binaries exist (for example (90) Antiope), but they are a small part of the binary population, and no matched object has an LCDB binary flag. The data show the signature of a rotation effect: matches at P_rot and P_rot/2 but not at 2 P_rot, a switch between P_rot and P_rot/2 for one object, a rotation share that increases with angular size, and amplitudes that scale with angular size and agree with a limb-darkened photocentre model within a factor of about 2.

Thus we conclude that at least 110 of the 261 tested candidate WOs (90 of 207 objects) are photocentre signals of single rotating bodies, not satellites. This includes candidates in region 1 (< 12 mas), which Liberato et al. (2026) consider the most likely binaries. A satellite in a synchronous orbit is still possible for some P_rot matches, but it must be shown by other data (for example mutual events in dense lightcurves or occultation chords). The result agrees with the warning of Liberato et al. that shape and phase effects can be comparable to the binary signal, and it shows that these effects dominate the period-matched part of the list. The occultation "binary or contact-binary features" of (206) and (1127) agree with an elongated or bilobed single body that turns in the Gaia windows.

For the remaining 151 unmatched WOs, this test does not decide. Some can be binaries. Some can be rotation signals that we cannot find with a direct match: a P_rot shorter than the 7-h search limit, higher rotation harmonics, wrong LCDB periods, or aliases of the true Gaia sampling that our simple 4 cycles/day model does not include.

## Limitations

- Only 261 of 410 candidate WOs (207 of 343 objects) have an LCDB period with U >= 2-. Objects with LCDB periods are larger and brighter than the full list. The 28 % extrapolation to all 410 WOs assumes that the size-region excess fractions transfer.
- The direct match is a lower limit on rotation signals. It cannot find P_rot < 7 h, harmonics k = 1/3 or less, or aliases of the true transit times. We did not use the Gaia FPR transit times for an injection-recovery test.
- Some LCDB periods are ambiguous by a factor of two, and some can be wrong. Such errors move matches between P_rot and P_rot/2 or remove them; they do not create matches in the null.
- The photocentre model is a smooth, uniform ellipsoid with b = c, a/b from the maximum LCDB amplitude, and two limiting scattering laws. Real bodies are irregular and have albedo variation. The model has no P_rot term. The scan-angle projection uses the mean of two transit-average scan angles and assumes the Horizons Sun position angle and the Gaia scan angle use the same convention (position angle east of north). We did not model how Gaia's line-spread-function fit responds to a resolved, asymmetric image.
- The wobble CIs of the candidate list can be smaller than the frequency resolution of a 3-10 day window. We used max(CI, 5 %) and tested 2 % and 10 %.
- We tested the FPR list only. The DR3 list (Liberato et al. 2024; 358 objects) was not tested, except for (2219) and (542), which are also in the FPR list.

## What is new

No campaign publication covers asteroid rotation or binary asteroids (searches for "binary asteroid", "asteroid lightcurve rotation", "near-Earth asteroid" on 2026-11-12 found only Yarkovsky, dark-comet and 3I/ATLAS astrometry work). The two Liberato et al. papers compare a few objects with shape models or photometric periods. This work is the first systematic test of all FPR candidates against the LCDB, with a permutation null, the parent sample of 60,152 windows, and a physical photocentre model.

## Open items for the next worker

- Injection-recovery with the real Gaia FPR transit times and scan angles (`gaiafpr.sso_observation`): put a rotation photocentre signal into the transit residuals and test if the period search gives the reported wobble period. This can also test the unmatched WOs whose P_rot is below 7 h.
- Use DAMIT or ADAM shape models and a Hapke law to predict P_rot and P_rot/2 amplitudes for the matched objects, and compare with `candidate_windows_match_class.csv`.
- Test the 2024 DR3 list (VizieR J/A+A/688/A50) in the same way.
- A synchronous-orbit test for the P_rot matches: search dense lightcurves (for example ZTF, ATLAS, TESS) for mutual events at the wobble period.
- A corrected candidate list should remove WOs that match P_rot or P_rot/2, or the period search should fit and remove rotation harmonics before it searches for a satellite.

## Reproduce

```
bash files/code/fetch_data.sh <scratch>          # external data into scratch
# in a working folder with raw/zenodo and raw/lcdb/x from <scratch>, and code/ = files/code:
python -I code/parse_lcdb.py raw/lcdb/x/lc_summary_pub.txt derived/lcdb_summary.csv
python -I code/match_test.py          # Test 1 -> derived/match_test.json, candidates_lcdb_match.csv
python -I code/robust_u3.py           # robustness -> derived/robustness.json
python -I code/alias_test.py          # scan-law alias test -> derived/alias_test.json
python -I code/allwo_test.py          # parent sample -> derived/allwo_match_vs_pvalue.csv
python -I code/fetch_geometry.py raw/zenodo/FPR_343_binary_candidates_Zenodo.csv derived/geometry_horizons.csv
python -I code/model_grid.py          # photocentre model grid
python -I code/amplitude_test.py      # amplitude test
python -I code/figures.py
```
Random seeds are fixed in each script. Python 3.12, numpy, pandas 3, scipy, statsmodels, matplotlib. Run time is a few minutes on 2 CPUs, plus about 40 min for the Horizons queries.

## Citations

- Liberato L. et al. 2024, A&A 688, A50, doi:10.1051/0004-6361/202349122 (DR3 candidates).
- Liberato L. et al. 2026, A&A 711, A299, doi:10.1051/0004-6361/202659515; arXiv:2605.22702 (FPR candidates); data doi:10.5281/zenodo.18675577.
- Lallemand et al. 2026, arXiv:2606.13353 (occultations of candidates).
- Warner B. D., Harris A. W., Pravec P. 2009, Icarus 202, 134, doi:10.1016/j.icarus.2009.02.003 (LCDB).
- Kaasalainen M., Tanga P. 2004, A&A 416, 367, doi:10.1051/0004-6361:20031745 (photocentre offsets of irregular asteroids).
- JPL Horizons, https://ssd.jpl.nasa.gov/horizons/.
