# The Crause et al. (2007) pulsation ephemerides do not predict R Coronae Borealis decline onsets after 2006, and ASAS-SN onsets of 22 stars show no significant common pulsation phase

Job `sci-1107-dell-astronomy-f23bcea3fcda`, topic astronomy, machine dell, model Claude Opus 5.5 (`claude-opus-5-5`), campaign 11_07_2026. The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

R Coronae Borealis (RCB) stars are hydrogen-deficient supergiants. Sometimes carbon dust forms near the star, and the star then fades by several magnitudes. The cause of the dust events is not known. One proposal is that pulsation shocks start them. If this is true, the decline onsets occur at one phase of the pulsation cycle.

Crause, Lawson & Henden (2007, "CLH") fitted linear ephemerides `JD_n = JD0 + n P` to the decline onsets of five RCB stars. P was the pulsation period. They reported that all onsets agreed within about 10 d. Percy & Dembski (2018, "PD18") measured 17 later onsets and said that they "continue to be locked ... with some scatter". Crawford et al. (2025) found no periodicity in a Fourier spectrum of the onsets, except some for RY Sgr, and they found that the R CrB and SU Tau onsets agree with a Poisson process. No study made a formal forward test of the fixed CLH ephemerides. No study measured the pulsation phase at onset for many RCB stars with a calibrated method.

We ask three questions:

1. Do the fixed CLH ephemerides predict the onsets that occurred after the CLH data?
2. Can a pulsation phase at onset be measured without bias from survey photometry?
3. In ASAS-SN (2014-2026) and ASAS-3 (2000-2009) data, do decline onsets of many RCB stars occur at a common pulsation phase, or at a fixed phase for each star?

No campaign publication on RCB stars existed before this work (campaign search on 2026-11-11 with several queries).

## 2. Main results

**A. Forward test of the CLH ephemerides (Figure 3).** We used the CLH periods and recovered JD0 from the PD18 Table 1 predicted times (the recovered JD0 values agree within 0.5 d between rows). The 17 PD18 onsets after the CLH data (2005-2016; R CrB, RY Sgr, S Aps, V854 Cen) give:

| Test | Value | p (uniform phases) |
| --- | --- | --- |
| Rayleigh Z | 0.68 (R = 0.20) | 0.51 |
| V-test toward the predicted phase | u = -1.04 | 0.85 |
| mean abs(O-C) | 12.1 d (random phases: 10.7 d) | P(random <= observed) = 0.83 |

Thus the later onsets are not closer to the ephemerides than random times. We simulated locking with a total scatter (CLH scatter plus timing error) of 5, 6.4, 8 or 10 d. The probability to get a mean abs(O-C) of 12.1 d or more is below 2e-5, below 2e-5, below 2e-5 and 0.0009. The V-test has power 1.00, 1.00, 0.95 and 0.66 for these cases. Thus the data reject locking at the CLH level of 10 d or less. Our ASAS-SN onset of S Aps (JD 2459995.3, 2023 February) has O-C = -18.8 d (phase -0.44). With it, n = 18, Z = 0.95 (p = 0.39) and V-test p = 0.91.

**B. A pulsation model fitted up to the onset gives false locking at minimum light (Figure 2a).** The early fade of a decline is slow. In our 61 timed ASAS-SN onsets, the median time from the first departure from the pulsation model (0.15 mag) to the 1-mag level is 19 d (interquartile range 6-30 d). When a sinusoid is fitted to data that end at the onset, the fit takes this slow fade as the descending branch of the pulsation. The onset then falls near pulsation minimum. We injected synthetic declines at uniformly random times into real maximum-light data of the same stars. This naive method gave a phase concentration R = 0.42 at phase 0.48 for 7,189 injections. With the same method, 52 real ASAS-SN onsets in 32 stars give R = 0.55, Z = 15.6, mean phase 0.48 and p = 1.6e-7 against uniform phases. Against the injection null, p = 0.068. Thus a naive analysis "detects" locking at minimum light, but the method causes it.

**C. Calibrated population test (Figures 1, 2b, 4).** Our main method uses one pulsation period per star. We find it with a Lomb-Scargle search (30-110 d) of all clean maximum-light data. We then fit a local sinusoid (period within +-5 % of the star period, plus a linear trend) to data that end 20 d before the departure, and we extrapolate it. The onset is the midpoint between the last point within the threshold of the model and the next point. We iterate until the fit window and the onset agree. The quality cuts are: onset time error 5 d or less, pulsation S/N 5 or more, fit window span 1.2 P or more, 20 or more points. The same cuts apply to real and injected declines. For the injections, the phase error (measured minus true local phase) has a standard deviation of 0.14 cycle, and 59 % are within 0.1 cycle.

| Sample | Onsets / stars | Rayleigh Z | mean phase | p (injection null) |
| --- | --- | --- | --- | --- |
| main: ASAS-SN 2014-2024 + ASAS-3 2003-2008 | 27 / 22 | 2.23 | 0.40 | 0.096 |
| ASAS-SN only | 25 / 20 | 1.63 | 0.40 | 0.19 |
| gap G = 30 d (ASAS-SN) | 23 / 19 | 0.77 | 0.58 | 0.58 |
| threshold 0.25 mag (ASAS-SN) | 25 / 20 | 1.38 | 0.42 | 0.24 |
| stars with injection phase accuracy R >= 0.7 | 15 / 13 | 0.31 | 0.41 | 0.72 |
| free local period (30-110 d), comparison | 32 / 23 | 0.62 | - | 0.83 |

Phase 0 is pulsation maximum light. The V-test toward maximum light (the Pugach 1977 and PD18 proposal for RY Sgr) gives p = 0.94 for the main sample. The five same-star onset pairs give a mean pair cosine of 0.28 (p = 0.26). We find no significant common onset phase. The weak p = 0.096 of the main sample does not persist in the variants.

**Power and limits (Figure 4).** If all onsets have one common phase with an intrinsic scatter of 0.05, 0.10, 0.15 or 0.20 cycle, the test detects it (p < 0.05) with probability 0.87, 0.75, 0.50 or 0.27. The observed Z is lower than in 92 % of the simulations for full locking with 0.05-cycle scatter. Thus the data do not reject full common locking at 95 %. The test of a separate phase for each star has almost no power (5 pairs). These limits apply to the measured departure time, which includes the variable delay of the slow early fade.

**D. Pulsation periods are poorly defined.** For 35 stars with a VSX period, our ASAS-SN period agrees within 10 % for 8 stars and is near a factor-2 alias for 7 stars. With a free local period, the injected phase error is 0.23 cycle (uniform noise: 0.29). This agrees with Feast et al. (2019) and Crawford et al. (2025): most RCB "pulsations" are not coherent, so a pulsation phase at onset is often not well defined.

## 3. Interpretation

The fixed CLH ephemerides fail as forecasts. The scatter of the later onsets about them is the scatter of random times. This agrees with the Fourier result of Crawford et al. (2025), and it is a direct forward test. A shock-triggered dust model that needs onsets at a fixed phase of a coherent period is not supported for R CrB, S Aps and V854 Cen, and the single RY Sgr onset after 2006 is also off by 13 d. The ASAS-SN onsets of 22 other RCB stars show no common phase, but this test is weak. Three properties limit any such test: the slow early fade (median 19 d, about one third of a cycle) makes the onset time depend on its definition; the pulsations are semi-regular; and a pulsation model fitted up to the onset gives a strong false signal. Earlier phase results that used visual data and a fit near the onset need a test of the same kind.

## 4. Limitations

- The population sample is small (27 onsets in 22 stars). Most declines are excluded because the onset is in a seasonal gap, the star was still recovering from an earlier decline, or the pulsation S/N is low.
- Stars brighter than V = 9 (R CrB, RY Sgr, V854 Cen, XX Cam) are saturated in ASAS-SN and are excluded from Part C. The only ASAS-SN onset of a CLH star is that of S Aps. For UW Cen we have no CLH zero point (no PD18 rows), so we did not test it.
- The PD18 onsets are AAVSO visual times with about 4 d uncertainty. We did not remeasure them, because the AAVSO data service refused automated access (HTTP 403).
- The injected declines use a power-law fade `(t/T1)^p` with T1 drawn from the real lags and p from 1 to 3. Real fades can differ.
- The "true" phase of an injection comes from a sinusoid fit around the start time with the same star period. Thus the phase accuracy is relative to a local sinusoid model.
- ASAS-SN V (2014-2018) and g (2018-2026) data are combined on one relative magnitude scale per camera and filter. The pulsation amplitude in g is somewhat larger than in V.
- ASAS-SN has single-camera null-flux artefacts. We used a cross-camera and a sustained-fade test. RS Tel shows many such artefacts, and its events failed the tests.
- The power study assumes locking of the start of the fade. It does not test locking with phase-dependent fade speeds.

## 5. What is open

- A test with denser photometry (ATLAS forced photometry, ZTF for stars fainter than 13 mag, and AAVSO V data for the bright stars) can increase the number of well-timed onsets. ATLAS c/o data are shown on the DREAMS RCB monitoring pages (https://dreams.anu.edu.au/monitoring/).
- RY Sgr has the largest and most coherent pulsation. A test of RY Sgr onsets after 2006 with AAVSO V data and this injection method is the most direct remaining test of pulsation triggering.
- A per-star test needs about 5 or more well-timed onsets per star. This needs several decades of dense data.

## 6. Data and provenance

- Star list: AAVSO VSX types RCB and RCB: (167 stars), from the `aavsovsx` table of ASAS-SN Sky Patrol v2 (query on 2026-11-11). Not bundled.
- ASAS-SN Sky Patrol v2 light curves (Shappee et al. 2014; Kochanek et al. 2017; Hart et al. 2023), retrieved with `skypatrol` 0.6.21 (`pyasassn.client.SkyPatrolClient.query_list`, catalog `aavsovsx`) on 2026-11-11/12. 167 files. Quality G, mag_err < 1, flux > 0 used. Not bundled.
- ASAS-3 V light curves (Pojmanski 2002) from `https://www.astrouw.edu.pl/cgi-asas/asas_cgi_get_data?<desig>,asas3`, 55 southern stars with V(max) 8-12.5, grades A and B, datasets within 30 arcsec. Not bundled.
- `files/results/raw_manifest.csv` gives the SHA-256, size and URL of each raw file that we used. The service notes that ASAS-SN Sky Patrol is rebuilding its catalogues (November 2026), so asas_sn_id values can change. Coordinates and names in a fresh VSX query identify the stars.
- `files/data/percy_dembski_2018_table1.csv`: onset times, cycle numbers and O-C values transcribed from Table 1 of Percy & Dembski (2018). These are factual values from that paper.
- No shared campaign dataset was used. The shared store had no RCB data on 2026-11-11.

## 7. Files

- `files/code/` - all code. `run_all.sh` gives the order of the steps. `rcb.py` (loaders), `phasefit.py` (local fits, onset timing, quality cuts), `events.py`, `onsets.py` (naive method), `onsets2.py` (main method), `periods2.py`, `inject.py`, `stats.py`, `naive_test.py`, `clh_test.py`, figure scripts, download scripts.
- `files/results/` - `events_raw*.csv` (decline candidates), `onsets2_pfix*.csv` (main onsets and phases; variants `_pfixG30`, `_pfixT25`; ASAS-3 `_asas3_pfix`), `onsets.csv` (naive method), `onsets2.csv`, `onsets2_asas3.csv` (free-period method), `star_periods*.csv`, `inject_*.csv` (all injections), `stats*.json`, `power_grid*.csv`, `real_used*.csv`, `naive_test.json`, `clh_test.json`, `clh_post_onsets.csv`.
- `files/figures/` - Figures 1-4.
- `files/NOTICE_external_data.md` - attribution and terms of the external data.

## 8. How to reproduce

```
uv venv --python 3.12 --system-site-packages venv && . venv/bin/activate
uv pip install skypatrol==0.6.21 astroquery
cp -r files/code scripts   # in an empty work directory outside the bundle
mkdir -p data && cp files/data/percy_dembski_2018_table1.csv data/
bash scripts/run_all.sh
```

The download steps write raw data into `scratch/` only. Compare the hashes with `files/results/raw_manifest.csv`. The injection steps use fixed seeds. On 2 CPUs the full run takes about 2 hours, most of it for the free-period comparison injections.

## 9. References

- Crause, L. A., Lawson, W. A., Henden, A. A. 2007, MNRAS 375, 301.
- Percy, J. R., Dembski, K. H. 2018, JAAVSO; arXiv:1809.04484.
- Crawford, C. L. et al. 2025, MNRAS (accepted version arXiv:2412.16393v2).
- Percy, J. R. 2019, arXiv:1903.05166 (ASAS-SN pulsation of RCB stars).
- Feast, M. W. et al. 2019, arXiv:1810.10823 (no coherent pulsation of R CrB in radial velocity).
- Pugach, A. F. 1977 (as cited by PD18 and Crawford et al. 2025).
- Shappee, B. J. et al. 2014, ApJ 788, 48; Kochanek, C. S. et al. 2017, PASP 129, 104502; Hart, K. et al. 2023, arXiv:2304.03791.
- Pojmanski, G. 2002, Acta Astron. 52, 397.
- Watson, C. L., Henden, A. A., Price, A. 2006, SASS 25, 47 (VSX).
