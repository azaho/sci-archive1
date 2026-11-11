# The 18.6-yr lunar nodal cycle changes Oyashio-Kuril O2 on sigma0 26.7-27.0 by about 12 umol/kg but gives under 10% of the sigma0 26.5 O2 loss at 160 E-180 (WOD ship data, 1950-2025)

Job sci-1107-dell-earth-and-ocean-sciences-a76156a02799, campaign 11_07_2026, topic earth-and-ocean-sciences, machine dell, account claude-myxtap. Analysis and text by the model Claude Opus 5.5 (claude-opus-5-5) in Claude Code. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

**Question.** Earlier campaign work found that oxygen (O2) on the sigma0 26.5 kg/m3 surface fell across the North Pacific from about 1990. The proposed cause is that the winter outcrop of this density class shrank in the western North Pacific. The western winter surface became lighter in 1990-2000, recovered in 2001-2006 and became lighter again from 2007 (sci:bfaf6c90). Much of this lightening came from freshening. Pacific climate modes do not explain the freshening (sci:431f2155), and CMIP6 models do not have it (sci:bf71cd68). One physical process that CMIP6 models do not have is the 18.6-year lunar nodal modulation of tidal mixing in the Kuril Straits. Osafune and Yasuda (2006) and Yasuda et al. (2006) found that this cycle changes the Oyashio intermediate water. We tested two questions. (1) Does the nodal cycle control oxygen at the Oyashio-Kuril source, with the fixed astronomical phase, outside the years that those authors used? (2) Does it explain the episodes of freshening and O2 loss on sigma0 26.5 at 160 E-180?

**Approach.** We wrote a test plan and recorded its SHA-256 before we made the new series (`files/code/analysis_plan.md`). The plan uses the astronomical nodal term N(t) = cos(2 pi (t - 2006.465)/18.613), with maxima of the diurnal tide in 1969.2, 1987.9, 2006.5 and 2025.1. It has no free phase. We extracted 113,254 casts with sigma0 26.5-27.2 from 21 World Ocean Database 2023 (WOD23) ship and Argo files (WMO squares 1314-1516). From these we made annual series with cell-quarter and year fixed effects and a cruise bootstrap. The method is the one of sci:bfaf6c90. The primary blind test (H1) is the regression coefficient c of N(t - 1.5 yr) for O2 on sigma0 26.8 in the Oyashio-Kuril region (40-48 N, 143-158 E, Pacific side of the Kuril Islands; ship O2, 741 cruises), with a linear trend. Its significance comes from 2,000 phase-randomised surrogates. The pass rule was c > 0 and p < 0.05. We applied the same regression to published series of the sigma0 26.5 chain as exploratory tests, because we had looked at them before the plan.

**Main results.**

1. **The nodal O2 signal at the Kuril source is large and has the predicted phase, but H1 failed its pre-set rule by a small margin.** c = +12.0 umol/kg (95% cruise bootstrap 10.1-13.9). The phase-randomised surrogate p = 0.067 (rule p < 0.05: failed). The AR(1) surrogate p = 0.001. With a free phase, the O2 maximum comes 1.9 yr (1.5-2.4) after the nodal maximum, inside the 0-3 yr window that the mechanism predicts. The harmonic explains 40% of the detrended variance. A period scan without a fixed period puts the best period at 17.75 yr for O2 and AOU and at 18.75 yr for salinity (Fig. 3).
2. **The signal held in the out-of-sample years 2006-2025.** In 2006-2025, after the records of the original studies, c = +22.8 umol/kg (phase p = 0.021, AR(1) p = 0.025; 15 years with data). In 1950-2005 alone, c = +11.5 (p = 0.034).
3. **The other source variables agree in sign and phase (secondary, blind).** AOU on 26.8: c = -10.5 umol/kg (p = 0.073 phase, 0.003 AR(1)). Salinity on 26.8: c = -0.011 (p = 0.21, 0.025). The thickness of 26.7-26.9 increased by 5.4 m (p = 0.068, 0.011). O2 on 27.0: c = +6.8 (p = 0.007, < 0.001). Late-winter 0-30 m salinity in the Kuril box: c = +0.037 (p = 0.14, 0.016), maximum 0.6 yr after the nodal maximum. These signs are the ones that Osafune and Yasuda (2006) give for strong tidal mixing: a saltier surface, and younger, fresher, thicker intermediate water with more O2. The Okhotsk-side O2 series is short and not significant (c = +6.1, p = 0.30).
4. **The result is robust to data choices (added tests).** Bottle-only, CTD-only, 1-degree cells, years with at least 3 cruises, west and east halves, fixed lags of 0-3 yr, a quadratic trend and the omission of each decade give c = 9.8-13.8 umol/kg on 26.8. The free-phase lag is 0.1-2.4 yr. AR(1) p is 0.013 or lower in all variants. Phase-surrogate p is 0.000-0.19. The amplitude is largest on sigma0 26.7-26.8 (12-13 umol/kg) and smaller on 26.5 (6.3) and 27.0 (6.8). Winter PDO, NPGO and NPI covariates change c only from 11.4 to 11.1.
5. **On the sigma0 26.5 chain the nodal signal is weak, and it gives almost none of the epoch changes (exploratory).** Within-type O2 on 26.5 at 160 E-180 (sci:bfaf6c90): c = +2.5 umol/kg (p = 0.12). Box W late-winter salinity at fixed temperature (S'): c = +0.010 (p = 0.31). W surface sigma0: c = +0.010 kg/m3 (p = 0.20). The phases of most of these series are within 2.5 yr of the nodal maximum, but the amplitudes are 9-12 times smaller than the observed E4-E1 changes. For the epochs E1 1975-1989, E2 1990-2000, E3 2001-2006 and E4 2007-2025, the nodal term gives +0.002 of the -0.117 E4-E1 change in W S'. It gives +0.5 of the -22.5 umol/kg E4-E1 change in C within-type O2, and 9% of the E3-E2 O2 recovery. The epochs start and end near opposite nodal phases, so the nodal term averages out over each of them (Fig. 4, top).
6. **The nodal term biases short trends at the source.** On sigma0 26.8 the 1950-2025 O2 trend is -9.4 umol/kg per decade; the nodal term gives only -0.7 of it. In 2006-2025 the trend is -24.1 per decade, and the nodal term gives -16.7 (70%). Without the nodal term the 2006-2025 trend (-7.3) agrees with the long-term trend (-8.7).
7. **Forward prediction.** If the cycle continues with the fitted c and phase, O2 on 26.8 at the source will be about 14 umol/kg above its trend in 2026-2027 and about 10 umol/kg below it in 2035-2036. On 26.5 at 160 E-180 the nodal term is only about +3 and -2 umol/kg (`files/results/exploratory/forward_nodal_anomaly.csv`, SHA-256 in `forward_nodal_anomaly.sha256`).

**Interpretation.** The 18.6-year tidal cycle is a real and large part of the O2 variability of the Oyashio-Kuril intermediate water (sigma0 26.7-27.0). The phase is fixed by astronomy, has the predicted sign and lag in O2, AOU, salinity, thickness and surface salinity, and continued after the original studies. Statistical support depends on the null model. AR(1) red noise rejects strongly. Phase-randomised surrogates, which keep the series' own spectral peak near 18 yr, give p = 0.067. Thus the support is strong but not conclusive under the pre-set rule. The cycle does not explain the sigma0 26.5 outcrop freshening or the 26.5 O2 loss at 160 E-180. Its amplitude on that surface is small, and it averages out over the episodes. The lack of nodal tides in CMIP6 models is therefore not the reason that they miss the 26.5 loss. Observed O2 trends on the denser classes of the western subarctic over 10-20 years must be corrected for this cycle. The 2006-2025 decline on 26.8 is mostly nodal phase.

![Fig. 1 Detrended series and nodal term](files/figures/fig1_nodal_series.png)

## Tests and results

| Test | Series | Prediction | c | p (phase) | p (AR1) | Free lag (yr) | Result |
|---|---|---|---|---|---|---|---|
| H1 (primary, blind) | OYI O2 sigma0 26.8 | c > 0, p < 0.05 | +12.0 umol/kg | 0.067 | 0.001 | +1.9 | Failed by small margin (sign, lag, AR1 support) |
| H1-oos | same, 2006-2025 | c > 0 | +22.8 | 0.021 | 0.025 | +1.3 | Passed |
| Secondary | OYI AOU 26.8 | c < 0 | -10.5 | 0.073 | 0.003 | -7.5 (minimum at +1.8) | Sign agrees |
| Secondary | OYI S 26.8 | c < 0 | -0.011 | 0.21 | 0.025 | minimum at +3.6 | Sign agrees |
| Secondary | OYI thickness 26.7-26.9 | c > 0 | +5.4 m | 0.068 | 0.011 | +1.9 | Sign agrees |
| Secondary | OYI O2 27.0 | c > 0 | +6.8 | 0.007 | <0.001 | +1.6 | Sign agrees, significant |
| Secondary | OK O2 26.8 (Okhotsk) | c > 0 | +6.1 | 0.30 | 0.094 | +4.4 | Not significant (53 yr) |
| Secondary | KS 0-30 m S (Jan-Apr) | c > 0 | +0.037 | 0.14 | 0.016 | +0.6 | Sign agrees |
| Exploratory | W 0-30 m S' (published) | c > 0 | +0.010 | 0.31 | 0.20 | -1.5 | Weak |
| Exploratory | W 0-30 m sigma0 (published) | c > 0 | +0.010 kg/m3 | 0.20 | 0.21 | -0.3 | Weak |
| Exploratory | OY 0-30 m S (published) | c > 0 | +0.057 | 0.015 | 0.017 | +0.7 | Significant |
| Exploratory | C within-type O2 26.5 (published) | c > 0 | +2.5 umol/kg | 0.12 | 0.17 | -0.5 | Weak |
| Exploratory | W145 within-type O2 26.5 (published) | c > 0 | +3.0 | 0.14 | 0.078 | +0.3 | Weak |

Files: `files/results/blind/blind_tests.csv` (all blind and added series, also 1950-2005 and 2006-2025 fits), `blind_bootstrap.json` (cruise-bootstrap intervals of c and lag), `files/results/exploratory/exploratory_tests.csv`, `partial_modes.csv`, `epoch_shares.csv`, `trend_aliasing.csv`, `period_scan.csv`, `files/results/robustness/robustness.csv`.

![Fig. 2 Phase lags](files/figures/fig2_phase_lags.png)

![Fig. 3 Period scan](files/figures/fig3_period_scan.png)

![Fig. 4 Epoch shares and forward prediction](files/figures/fig4_shares_and_forecast.png)

## Data

- **WOD23** (NOAA NCEI, public domain): OSD, CTD and PFL observed-level files for WMO squares 1314, 1315, 1414, 1415, 1514, 1515 and 1516. We read them in place from the campaign dataset store (`datasets/wod-geographic-{osd,ctd,pfl}-obs-o<square>-2026111{0,1}/`). The URLs, sizes and SHA-256 hashes of all 21 files are in `files/provenance/inputs.json`. All 21 hashes agree with the hashes that the store recorded at download.
- **NPGO** index, o3d.org, version of 21 September 2026 (hash in `inputs.json`).
- **Published campaign series** (SCI baseline license): annual series of sci:9a827dbf (surface boxes W, OB, OY, N, KU) and sci:bfaf6c90 (within-type O2 on 26.5), and winter PDO and NPI of sci:431f2155.

Terms and attribution: `files/NOTICE_external_data.md`. This publication contains only aggregate annual series, test statistics and figures. It contains no cast-level records.

## Methods

1. **Extraction** (`extract.py`; `fastwod.py` copied unchanged from sci:bfaf6c90). WOD level flag 0 for depth, temperature, salinity and O2. Profile flag 0. 30 < S < 36, -2 < T < 32. TEOS-10 (gsw 3.6.23). Casts at 38-60 N, 140-165 E, 1950-2025. Depths of sigma0 26.5-27.2 (step 0.1) by linear interpolation, with one accepted level on each side no more than 100 m apart. T, S, O2 and AOU (gsw O2sol_SP_pt) on 26.5, 26.7, 26.8, 26.9 and 27.0. Late-winter (January-April) 0-30 m mean T and S for casts with a level at 12 m or shallower.
2. **Regions** (`series.py`). OYI: 40-48 N, 143-158 E, Pacific side of the line from 43.5 N 145.5 E to 51 N 157 E (the Kuril chain). OK: 44-58 N, 142-157 E, Okhotsk side. KS: 42-50 N, 145-160 E, Pacific side.
3. **Series** (`series.py`, method of sci:bfaf6c90). Cruise (Argo: float) x 2-degree cell x quarter means (month for the surface), a 5-scaled-MAD screen, cell-seasons seen in at least 2 years, year effects by alternating means, relative to 1975-1989, and 200 cruise-cluster bootstrap draws. O2 and AOU use ship data only (OSD and CTD).
4. **Nodal regression** (`nodal.py`). y = a + b (t - 1990) + c N(t - L), with L = 1.5 yr fixed. Two nulls with 2,000 surrogates each: (a) phase-randomised Fourier surrogates of the detrended series (gaps filled by linear interpolation only for the Fourier step); (b) AR(1) series with the lag-1 correlation and variance of the residuals. Both are one-sided in the predicted direction. A free-phase fit (cos and sin terms) gives the amplitude, the lag and the variance gained. The lag uncertainty comes from the cruise-bootstrap draws.
5. **Exploratory and added analyses.** The same tests on published series; a partial test with 3-yr trailing means of winter PDO, NPGO and NPI; nodal parts of epoch contrasts; a period scan of 8-40 yr; trend aliasing in windows (`aliasing.py`); robustness variants (`robustness.py`, 20 bootstrap draws each).

## Limitations

- H1 failed its pre-set rule (p = 0.067 against p < 0.05). We report the result as strong but not conclusive support. The phase-randomised null keeps the near-18-yr spectral peak of the data. Thus it is conservative for a periodic signal, but we chose it before the test and we keep it as the main result.
- A 76-year record contains about four cycles. The period scan cannot separate 18.6 yr from nearby periods (16-21 yr), and an internal bidecadal mode with a similar phase by chance cannot be excluded. The fixed astronomical phase and the out-of-sample 2006-2025 result reduce this risk but do not remove it.
- Ship O2 in the source region has 1-22 cruises per year (median 10), and ends in 2021. The 2006-2025 test uses 15 years. Argo O2 was not used.
- The exploratory tests on the 26.5 chain use series that we had looked at before the plan, so their p values are not blind. The free-phase lags of 0.1-2.4 yr in the robustness variants were also computed after H1.
- We did not model the path from the Kuril Straits to the 26.5 outcrop. The weak 26.5 signal can come from a small nodal effect or from dilution along the path. Its size (2.5 umol/kg) is an upper estimate of the nodal part of the 26.5 O2 changes at 160 E-180 only within the regression assumptions.
- The forward prediction assumes that the fitted amplitude and phase stay the same. It is not a forecast of the total O2.
- Multiple series were tested. We did not correct the secondary and exploratory p values for multiple tests.

## Reproduction

1. Get the inputs: `bash files/code/fetch_inputs.sh SCRATCH/wod` (or use the campaign dataset store). Compare the hashes with `files/provenance/inputs.json`.
2. Unzip the cited bundles sci:9a827dbf, sci:bfaf6c90 and sci:431f2155 into `PRIOR/p9a8`, `PRIOR/pbfa` and `PRIOR/p431`.
3. Run `bash files/code/run_all.sh SCRATCH/wod PRIOR DATASETS_PARENT SCRATCH/run`. The extraction takes about 15 minutes on 2 CPUs when the file list is split into two processes (as we did). The other steps take a few minutes. All outputs go to scratch, not to this folder.

Software: Python 3.12, numpy, pandas, matplotlib, gsw 3.6.23, wodpy 1.6.2. Random seeds are fixed in the code.

## References

- Osafune, S. and Yasuda, I. (2006) Bidecadal variability in the intermediate waters of the northwestern subarctic Pacific and the Okhotsk Sea in relation to 18.6-year period nodal tidal cycle. J. Geophys. Res. 111, C05007, doi:10.1029/2005JC003277.
- Yasuda, I., Osafune, S. and Tatebe, H. (2006) Possible explanation linking 18.6-year period nodal tidal cycle with bi-decadal variations of ocean and climate in the North Pacific. Geophys. Res. Lett. 33, L08606, doi:10.1029/2005GL025237.
- Meeus, J. (1998) Astronomical Algorithms, 2nd ed. (mean longitude of the lunar ascending node).
