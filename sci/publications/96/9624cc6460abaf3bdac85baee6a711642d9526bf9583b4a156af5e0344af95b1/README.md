# Southern Hemisphere gyres do not follow the North Pacific surface-density rule for sigma0 26.5 AOU change (GLODAP, WOA23, ERSSTv5, 1985-2023)

Job: sci-1107-dell-earth-and-ocean-sciences-e4e322cfa108. Topic: earth-and-ocean-sciences. Machine: dell (campaign 11_07_2026).
Model: Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Earlier campaign work linked the oxygen (O2) loss on sigma0 26.5 in the North Pacific (NP) to a lighter late-winter
surface and a smaller winter outcrop of the ventilated density classes (sci:84f111c0, sci:bfaf6c90, sci:9a827dbf).
Two rules turn the surface change into an AOU change:

- **Shift rule** (sci:21ae52cf): AOU on class c changes as if the AOU profile moved by a density offset
  delta = f x (lightening of the late-winter surface where class c outcrops), with f = 0.40-0.70 (central 0.55).
- **Area rule** (sci:bf71cd68): ventilation rate is proportional to the winter outcrop area of the class, so
  AOU_new = AOU_ref x A_ref / A_new.

Both rules came from the NP (and were checked in the North Atlantic, NA, by sci:dcfc9b0b). No test used another basin.
**This study asks: do the three Southern Hemisphere (SH) subtropical gyres show AOU changes on sigma0 26.0-26.8 with the
sign and size that these rules give from their own late-winter surface changes?** The SH is an out-of-sample test.
A pass would make the mechanism general. A fail would show that a different process controls the SH changes, or that
the rule is specific to the NP.

## 2. Pre-registration

We wrote `files/PREREGISTRATION.md` before we calculated any SH AOU change. It fixes the boxes, epochs, surface decades,
predictors, the f value and three tests (T1 sign, T2 size, T3 class pattern). Sections 4.1-4.2 give the pre-registered
results. All other analyses (sections 4.3-4.5) are post hoc. We identify them as post hoc.

## 3. Data and method

- **AOU on density classes.** GLODAPv2.2023 bottle data (Pacific, Atlantic, Indian files; flag-2 O2 and salinity).
  For each cast we interpolate AOU, O2, salinity, theta and pressure linearly to sigma0 classes 25.6-27.2 (step 0.1),
  at the shallowest crossing, with brackets at most 150 dbar apart (`glodap_isopycnal.py`; 19,089 Pacific,
  15,132 Atlantic and 5,180 Indian casts give class values).
- **Interior boxes.** S Pacific (SP) 15-40 S, 160 E-75 W; S Indian (SI) 15-40 S, 35-115 E; S Atlantic (SA)
  15-40 S, 50 W-15 E. NH controls: NP 15-45 N, 140 E-120 W; NA 15-45 N, 80-15 W.
- **Epochs.** E1 1985-1997 (WOCE), E2 2003-2012, E3 2013-2023. The change is the mean, over 2 x 2 degree cells that have
  data in both epochs, of the epoch-mean difference (cell-matched). Uncertainty: cruise-block bootstrap (1,000 draws,
  90% interval).
- **Late-winter surface.** WOA23 decadal monthly objectively analysed T and S at 0-10 m (NCEI OPeNDAP). Late-winter
  sigma0 (TEOS-10) is the maximum over Jan-Apr (NH) or Jul-Oct (SH). Formation bands: 25-55 degrees poleward,
  same longitudes as the box. For each class, d_s = area-weighted mean surface sigma0 change over the cells whose
  earlier-decade surface sigma0 is within c +- 0.1.
- **Surface decades.** Pre-registered with a 5-10 yr lead (E1 <- 1985-94, E2 <- 1995-2004, E3 <- 2005-14). Sensitivity
  without lead (E1 <- 1985-94, E2 <- 2005-14, E3 <- 2015-22).
- **Core class.** Tests use the class mean over 26.4-26.6.

## 4. Results

### 4.1 Pre-registered tests fail in the SH (T1 1/6, T2 0/6; T3 5/6)

| SH case (lead decades) | observed dAOU 26.4-26.6 (umol/kg, 90% CI) | surface d_s (kg m-3) | shift-rule prediction | T1 |
|---|---|---|---|---|
| SP E1-E2 | -0.5 (-5.9 to +3.8) | -0.074 | +3.2 | sign differs, not significant |
| SP E2-E3 | +1.5 (-1.7 to +4.0) | +0.013 | -0.5 | no prediction (< 1) |
| SI E1-E2 | +2.1 (+0.5 to +4.6) | +0.018 | -0.3 | no prediction |
| SI E2-E3 | +0.9 (-1.7 to +3.7) | -0.058 | +0.5 | no prediction |
| SA E1-E2 | -1.5 (-4.1 to +0.0) | -0.011 | +0.5 | no prediction |
| SA E2-E3 | +3.1 (+0.8 to +5.3) | -0.016 | +0.9 | no prediction |

T1 (sign right in at least 5 of 6) passed in 1 case. Five cases had a prediction below 1 umol/kg, which the
pre-registration scores as a fail. T2 (observed/predicted within 0.5-2 in at least 4 of 6) passed in 0 cases.
T3 (positive Spearman correlation across classes 26.0-26.8 in at least 4 of 6) passed with 5 of 6. T3 is a weak test,
because both the prediction and many other processes follow the shape of the reference AOU profile.
The area rule gave predictions of -10 to +25 umol/kg in the SH with no relation to the observed values
(`core_class_cases.csv`). The same code reproduces the known NP gain: NP E1-E3 observed +12.1 (+9.0 to +13.8)
against a shift-rule prediction of +10.0 (lead) or +15.3 (no lead) (Figure 2).

### 4.2 The SH surface changes in WOA23 before 2005 are mostly not observed

In the 1985-94 and 1995-2004 decades, only 3-13% of the SH 26.5 formation-band cells had any late-winter salinity
observation (SI 1995-2004: 38%). The NP had 58-69% and the NA 42-58% (Figure 1c). In data-poor cells the WOA23
objective analysis returns its first guess, so the pre-registered SH predictions for E1 and E2 are not measurements.
Only the 2005-14 to 2015-22 surface change is observed in the SH (71-92% of cells). In that pair the SH surface
changed by only -0.020 (SP), -0.001 (SI) and -0.012 (SA) kg m-3, against -0.047 (NP) and -0.075 (NA).

### 4.3 Post hoc: ERSSTv5 gives an observed thermal part of the pre-Argo SH surface change

ERSSTv5 late-winter SST (Feb-Mar NH, Aug-Sep SH) in the same 26.5 bands, converted to a thermal sigma0 change at
the WOA23 reference T and S, gives (1985-94 to 2005-14): SP -0.053, SI +0.002, SA -0.036, NP -0.014 and
NA -0.099 kg m-3 (Figure 1d; `surface_decade_pairs.csv`). Thus the SP and SA bands did become lighter by warming
before the Argo era; the SI band did not. Salinity is not observed before 2005 in the SH, so this is the thermal part only.

### 4.4 Post hoc: case-by-case the SH does not follow the rule

- **S Pacific: lighter surface, no AOU gain.** The SP band became lighter by about 0.05-0.09 kg m-3 (WOA23 total and
  ERSST thermal agree within 0.02). The shift rule gives +2.2 to +3.5 umol/kg for E1-E2 and E1-E3. Observed AOU on
  26.4-26.6 changed by -0.5 and -2.1. From E1 to E3 the SP AOU change split by class: +3.0 to +4.7 umol/kg on the
  lighter classes 25.6-26.2 (the rule gives +3.4 to +6.0, so these agree), and -1.3 to -5.1 on 26.4-26.9, where the
  rule gives -1.4 to +5.1 (Figure 3; `basin_class_changes.csv`). The 90% intervals on 26.4-26.6 include the
  predicted values, so the data do not exclude the rule there, but the central values have the opposite sign.
- **S Indian: AOU gain, no lighter surface.** Observed AOU rose by +2.1 (+0.5 to +4.6) from E1 to E2 and
  +5.8 (+0.8 to +9.8) from E1 to E3, uniform over 26.0-26.8. The ERSST thermal change was about 0, and the Argo-era
  surface did not change; the rule gives -0.1 to +0.7.
- **S Atlantic: mixed.** E1-E2 -1.5 (rule +1.5 to +2.5), E2-E3 +3.1 (+0.8 to +5.3; rule +0.6 WOA, +1.7 ERSST thermal).

The SH AOU changes on 26.4-26.6 were all small (-2 to +6 umol/kg, at most 1/2 of the NP E1-E3 gain), but their
pattern among the gyres does not follow the surface change.

### 4.5 Post hoc: pooled across basins, the rule gives the order of size but not the SH detail

With only the basin-intervals whose late-winter surface is observed (at least 40% of cells in both decades; no-lead
decades; E1-E2 and E2-E3), there are 7 cases: NP x2, NA x2, SP, SI, SA (Argo era). Observed and predicted correlate
(r = 0.78, one-sided permutation p = 0.02), with a fitted slope through zero of 0.56 (90%: 0.37-0.75), i.e. an
effective f of about 0.3, and chi-square 7.2 for 6 degrees of freedom (Figure 2b; `pooled_dose_response.json`).
This result depends on the contrast between the NH (large lightening, large AOU gain) and the Argo-era SH
(small change in both). It is post hoc, uses only 7 cases, and the SH cases alone carry no information on the slope.

## 5. Interpretation

The NP surface-density rule does not transfer as a quantitative, case-by-case predictor to the SH subtropical gyres.
The SP thermocline did not gain AOU on 26.4-26.8 when its winter outcrop band became lighter, and the SI gained AOU
without a lighter surface. This agrees with reports that SH thermocline ventilation changed in the 1990s-2000s with
the westerly winds, Ekman pumping and gyre spin-up, which the surface density of the outcrop band does not measure.
The rule remains consistent with the NP and, partly, the NA, where the surface lightening was larger (up to
0.13 kg m-3) and mostly by freshening (NP) or warming (NA). So the evidence supports the outcrop mechanism as an NP
process with a large forcing signal, not as a general law for subtropical thermocline AOU. For projections, this
means that the outcrop-scaled AOU gains in sci:bf71cd68 should not be applied to other basins without a separate test.

## 6. Limitations

- Pre-Argo SH late-winter surface salinity is not observed in WOA23 (3-13% of cells). We give only the thermal part
  from ERSSTv5. A fresher or saltier SH surface before 2005 could change the SP and SA predictions.
- GLODAP sampling: 5-13 cruises per SH basin and epoch; the cell-matched means use 19-162 cells. The 1998-2002 cruises
  (for example I05 in 2002) fall outside the pre-registered epochs.
- The SP box includes the eastern South Pacific oxygen minimum region east of 90 W; we did not separate it.
- AOU assumes 100% preformed saturation; preformed changes are not removed.
- Isopycnal changes include mixing (spice) changes; we did not use a within-type decomposition.
- The shift rule uses a single f from the NE Pacific and a 25-55 degree formation band; the true SH subduction regions
  (Subantarctic Mode Water and subtropical mode waters) may be narrower.
- Sections 4.3-4.5 are post hoc. The 40% coverage threshold was chosen after Figure 1c was made.

## 7. Reproduction

1. `bash files/code/get_data.sh <scratch>` downloads GLODAPv2.2023 (3 CSV), ERSSTv5 and the 168 WOA23 OPeNDAP subsets
   into a scratch folder outside the bundle (about 900 MB; the WOA23 fetch took about 15 min at 2 parallel streams).
2. `bash files/code/run_all.sh <scratch>` runs class extraction, the pre-registered analysis (`analysis.py`), the post hoc
   checks (`supplement.py`, `pooled.py`) and the figures. gsw 3.6.23 is needed (for example
   `pip install --target <dir> gsw==3.6.23` and `PYTHONPATH=<dir>`).
3. Compare with `files/results/*.csv|json`. Bootstrap seeds are fixed.

Files: `files/results/basin_class_changes.csv` (all basins, classes, intervals, surface variants),
`core_class_cases*.csv` (core class and tests), `pre_registered_tests.json`, `surface_decade_pairs.csv`,
`ersst_thermal_predictions.csv`, `pooled_dose_response.json`, `woa23_late_winter_surface.npz` (derived WOA23 field).
Provenance and hashes: `files/provenance/DATA_SOURCES.md`. External data terms: `files/NOTICE-external-data.md`.
