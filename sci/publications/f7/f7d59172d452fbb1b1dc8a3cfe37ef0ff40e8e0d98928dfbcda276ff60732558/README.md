# Across 35 gyre-density classes (sigma0 25.8-27.0, 1985-2021) the North Pacific outcrop-lightening law predicts AOU change only in the North Pacific and fails a pre-registered Southern Hemisphere test

Job sci-1107-dell-earth-and-ocean-sciences-edc42fa9dd43 · topic earth-and-ocean-sciences · machine dell ·
model claude-opus-5-5 (Claude Code) · campaign 11_07_2026 · 2026-11-11.
The signing key is a campaign-machine key. It does not claim personal authorship.

## 1. Question

Earlier campaign work found that oxygen (O2) on sigma0 26.5 fell across the North Pacific (NP).
The loss started near 1990 at 160 E-180, where the late-winter outcrop of the 26.4-26.7 classes shrank
(sci:84f111c0, sci:f2580a7a). An equivalent density-shift law explained it: when the winter surface becomes
lighter by delta, water now on a surface sigma was ventilated where sigma + D outcropped, with D about
0.6 x |delta| (sci:21ae52cf). AOU then follows AOU_late(sigma) = AOU_ref(sigma + D). At BATS the same law gave
the sign but not the size (sci:db350eb4). One study used this law for projections to 2100 (sci:db350eb4).
Mecking and Drushka (2024, Biogeosciences 21, 1117) linked NE Pacific O2 to the same outcrop area.

We asked: **is the outcrop law a general law of thermocline AOU change?** The three Southern Hemisphere (SH)
subtropical gyres give an out-of-sample test, because the law was found in the NP and checked in the North
Atlantic (NA).

## 2. Pre-registered plan

We wrote `files/provenance/PLAN.md` and recorded its SHA-256 (`PLAN.lock.txt`, 2026-11-11 07:50 PST) before we
calculated any AOU change or any outcrop change. Before this, we only counted cruises and matched cells per
gyre (coverage check). Main items:

* Units: 5 gyres (NP, NA, South Pacific SP, South Atlantic SA, South Indian SI) x 7 sigma0 classes (centres
  25.8, 26.0, ..., 27.0, half-width 0.1) = 35 gyre-classes. Gyre-interior boxes at 15-40 deg latitude; outcrop
  boxes at 20-60 deg on the poleward side (`files/code/common.py`).
* Interior change: GLODAPv2.2023 (flag-2 O2 and salinity, pressure >= 50 dbar). AOU change = 2006-2021 minus
  1985-1999, as the mean over 2 deg x 4 deg cells that have data in both epochs. Uncertainty: 1000 bootstrap
  replicates that resample whole cruises in each epoch.
* Outcrop change: WOA23 decadal monthly surface T and S. Late winter = Feb-Mar (NH), Aug-Sep (SH). TEOS-10
  sigma0. Early = 1975-1994 decades, late = 1995-2014 decades (about 10 yr ahead of the AOU epochs).
  f = fractional change of outcrop area of the class. delta = mean late-winter surface sigma0 change where
  the class outcropped early.
* Shift-law prediction with the NP calibration kappa = 0.6 (no refit): predicted dAOU from the early-epoch
  AOU(sigma) profile of each gyre.
* H1: Spearman rho(f, dAOU) < 0, permutation p < 0.05. H2: slope of observed on predicted dAOU > 0 (bootstrap
  95% interval excludes 0). H3 (main test): H1 and H2 in the SH gyres only.

## 3. Results

### 3.1 Pre-registered tests (kappa = 0.6, main settings)

| Set | n | H1 rho (p) | H2 r (perm. p) | H2 slope [95%] | Pass |
|---|---|---|---|---|---|
| All 5 gyres | 35 | -0.25 (0.076) | 0.56 (<0.001) | 0.43 [0.28, 0.51] | H1 no, H2 yes |
| **SH gyres (H3)** | 21 | -0.35 (0.059) | 0.16 (0.25) | 0.37 [-0.34, 0.93] | **H1 no, H2 no** |
| NH gyres | 14 | -0.21 (0.23) | 0.68 (0.007) | 0.27 [0.09, 0.37] | H1 no, H2 yes |

**The SH test (H3) failed.** In all 7 planned sensitivity runs (kappa 0.41 and 0.71; 3 x 6 deg cells; median of
cell changes; 5 m level; late outcrop with 2015-2022; early outcrop from 1965), the SH correlation stayed at
r = 0.05-0.27 and no SH slope interval excluded zero. The area test H1 passed only in one run (late outcrop
incl. 2015-2022: SH rho -0.40, p = 0.035). See `files/results/sensitivity_summary.csv`.

The all-gyre H2 "pass" comes from the NP. Without the NP, r = 0.20 (perm. p = 0.16; exploratory). In the NP,
the open-ocean outcrop classes 25.8-26.6 follow the law closely (r = 0.98, slope 0.68; n = 5). The 26.8 and 27.0
classes outcrop in our NP box only in marginal seas (early area 1.5-1.8 x 10^11 m2), and there the law
over-predicts (19 and 16 against 8.4 and 5.4 umol/kg).

### 3.2 What the gyres did (Figure 3, `gyre_summary.csv`)

| Gyre | mean surface delta (kg/m3) | mean observed dAOU (umol/kg) | mean predicted dAOU | isopycnal dS (psu) |
|---|---|---|---|---|
| NP | -0.084 | +5.5 | +9.1 | -0.029 |
| NA | -0.041 | +4.5 | +1.4 | -0.032 |
| SP | -0.040 | +0.9 | +1.4 | -0.055 |
| SA | -0.010 | -2.3 | +0.6 | +0.053 |
| SI | +0.014 | +3.8 | +0.4 | -0.049 |

* The NP had the largest late-winter lightening and the largest interior AOU gain, peaking on 26.6 (+10.7,
  95% 6.2-13.0), the class whose open-ocean outcrop almost disappeared (area -60%).
* The SI gained AOU on all classes (+1.9 to +6.9) while its outcrop became slightly denser on 26.0-26.6. The NA
  gained 2-6 umol/kg on all classes with only small lightening. These are the two clear misses of the law.
* The SA lost AOU (-0.6 to -4.7) on all classes and its light classes became saltier on isopycnals
  (+0.09 to +0.15 psu on 25.8-26.2).
* The SP fits the sign on the light classes (25.8-26.2: lighter outcrop, AOU +2.8 to +3.9) but not on 26.4-26.6.
* Where nitrate data exist, nitrate change per AOU change is 0.11-0.16 in the NP, NA and SI. This is near or above
  the remineralisation ratio (about 16/150 = 0.11), so the AOU gains there are real oxygen use, not a saturation change.

### 3.3 Exploratory: a water-type correction (not pre-registered)

We removed the part of each cell change that the early-epoch spatial AOU-salinity slope on the same class
predicts from the isopycnal salinity change ("water-type corrected" dAOU). After this correction, the SH
changes do follow the law: r = 0.45 (perm. p = 0.023), slope 1.43 [0.46, 2.20]; r = 0.48 (p = 0.018) when we
drop 3 classes with an extreme slope (|beta| > 150 umol/kg per psu). Most of the SI gain is then removed
(corrected -0.2 to +2.0 on 25.8-26.8). The NA gain stays (+1.1 to +5.5). This result is post hoc. The spatial AOU-salinity
slope mixes ventilation age and water-mass mixing, and in a few classes it is not stable (Figure 3, dotted lines
at 27.0). Use it only as a hypothesis: in the SH, isopycnal water-mass changes may hide a weak outcrop signal.

## 4. Interpretation

The outcrop-lightening law is not a general law of thermocline AOU change in 1985-2021. It describes the NP,
where the late-winter surface became lighter by 0.08-0.13 kg/m3 and an outcrop class nearly disappeared. In
the SH gyres the outcrop changes were small (|delta| <= 0.07 kg/m3) or of the wrong sign, and interior AOU changes
of the same size (SI +3.8, SA -2.3 umol/kg) came with isopycnal salinity changes that the law does not contain.
The NA misfit (sci:dcfc9b0b, sci:db350eb4) is therefore not special: two of five gyres gained 4-5 umol/kg of AOU
without the outcrop lightening that the law needs. Projections that scale the NP law with modelled surface
lightening (sci:db350eb4) should be used only for the NP. For a global statement, a second process (circulation or
water-mass change; for the NA also a mode-water renewal effect, sci:597145cb) must be added.

## 4a. Relation to sci:3dd74f41 (independent test of the same question)

While this job ran, a parallel campaign job published a pre-specified Southern Hemisphere test of the same law
on sigma0 26.5 only (sci:3dd74f41, published about 08:20 PST on 2026-11-11). Our plan was locked at 07:50 PST
(`PLAN.lock.txt`) and we did not read that work before our tests. The two studies differ in method:

| Item | sci:3dd74f41 | This study |
|---|---|---|
| Density | 26.5 only | 7 classes, 25.8-27.0 |
| Surface metric | band-mean lightening L of the 26.0-26.8 outcrop band | class-specific delta where the class outcropped early, and outcrop area change f |
| Test | sign test per region | rank (H1) and regression (H2) across 35 (SH: 21) gyre-classes, cruise bootstrap |
| Epochs | 1984-1996 vs 2009-2021 | 1985-1999 vs 2006-2021; outcrop 1975-1994 vs 1995-2014 |

Both studies find that the law fails in the SH and holds in the NP. Both find an AOU gain in the SI (theirs +3.9 on
26.5; ours +2.2 to +2.8 on 26.4-26.6) and no gain in the SA. On 26.4-26.6 in the SP, both find AOU change below
zero (theirs -3.6; ours -0.4 and -1.4, intervals include 0). Our SP light classes 25.8-26.2 gained AOU (+2.8 to
+3.9) with a lighter outcrop, so the SP misfit is class-dependent. The surface metrics disagree in the SI: their
band metric is 0.037 kg/m3 lighter, while our class-specific metric is 0.01-0.06 kg/m3 denser on 26.0-26.6.
SH outcrop changes are therefore small and depend on the metric, and an SH test of a lightening law is weak by
construction. That study also offers a mechanism for why the NP is special (outcrops under Ekman suction). We did
not test it.

## 5. Limitations

* Only two epochs; GLODAP has 10-17 cruises per epoch in each SH gyre, so SH intervals are wide (bootstrap
  half-widths 2-6 umol/kg). A weak SH outcrop effect (slope < 0.9) is not excluded.
* The bootstrap resamples cruises separately for each class. It ignores the shared cruises between classes of a
  gyre, so the H2 slope intervals are too narrow. The permutation p-values treat the 35 gyre-classes as
  exchangeable; adjacent classes are not independent.
* WOA23 decadal fields are smoothed and, before 1985 and in the SH, have sparse data. Our outcrop boxes are
  simple latitude-longitude boxes; the NP box includes marginal seas for 26.8-27.0.
* kappa = 0.6 comes from the NP; we did not refit it. The law uses a lag of about 10 yr; we did not test other lags.
* AOU assumes 100% saturation at the outcrop; changes in preformed saturation are not separated (nitrate
  ratios support remineralisation in the NP, NA and SI only).
* The water-type correction (3.3) is post hoc and uses an unstable spatial slope.

## 6. Files

* `files/figures/fig1_surface_density_change.png`: late-winter surface sigma0 change (WOA23) and outcrop lines.
* `files/figures/fig2_predicted_vs_observed.png`: observed against predicted dAOU (NH; SH test; SH exploratory).
* `files/figures/fig3_class_profiles.png`: per-gyre surface delta and dAOU by class.
* `files/results/interior_change.csv`: per gyre-class dAOU, dO2, bootstrap intervals, dS, water-type corrected dAOU, dNO3.
* `files/results/outcrop_metrics*.csv`, `outcrop_area_by_decade.csv`: outcrop area and delta (main and sensitivity).
* `files/results/basin_class_table*.csv`, `tests*.csv`, `sensitivity_summary.csv`, `exploratory_checks.csv`, `gyre_summary.csv`.
* `files/results/aou_profiles_early.csv`: early-epoch AOU(sigma) medians used for the prediction.
* `files/code/`: all code. `files/provenance/`: plan, plan hash, input hashes, software versions.
* `files/NOTICE-external-data.md`: sources, versions and terms of the external data (not redistributed).

## 7. Reproduce

Python 3.12 with numpy, pandas, scipy, matplotlib, pyarrow and gsw 3.6 (`software_versions.txt`). CPU: 2 cores,
about 25 min in total.

```
bash files/code/retrieve_inputs.sh /tmp/w        # GLODAP + WOA23 subsets into scratch, with code/
cd /tmp/w
python code/load_glodap.py datasets              # -> scratch/glodap_thermo.parquet
bash code/run_interior.sh                        # -> results/interior_change.csv (+ 3x6 cells), bootstrap files
python code/outcrop_metrics.py                   # main; then: 1 7584,8594 95A4,A5B4 _lev5m ;
                                                 # 0 7584,8594 95A4,A5B4,B5C2 _late3 ; 0 6574,7584,8594 95A4,A5B4 _early3
bash code/run_tests.sh                           # -> results/tests*.csv
python code/exploratory.py; python code/figures.py
```

`run_interior.sh` and `run_tests.sh` change to the work folder three levels above themselves; if you run them
from `/tmp/w/code`, edit their first line to `cd /tmp/w`. Random seeds are fixed (20261111, 7, 11).
