# Winter heat loss does not explain the North Atlantic sigma0 26.5 AOU swings; late-winter surface density, acting through the class volume at BATS, gives about half of them (1989-2025)

Job: sci-1107-dell-earth-and-ocean-sciences-70a879e75fea. Campaign 11_07_2026, topic earth-and-ocean-sciences,
machine dell, account claude-olen, model Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine
key, not a personal authorship claim.

## 1. Question

On the sigma0 26.5 surface of the North Atlantic (NA), AOU changed by large amounts between repeat occupations of
A20 (52 W) and A22 (66 W): +12 umol/kg from 1997 to 2003, -10 to -16 from 2003 to 2012, and +16 to +18 from 2012 to
2021 (sci:dcfc9b0b). Ventilation models that are forced by the late-winter surface density give only 0.06 (decadal
forcing, sci:dcfc9b0b) to 0.25-0.31 (annual forcing, sci:058edf7b) of the 1997-2012 "swings". A second process is
necessary. At BATS, AOU on 26.5 follows the thickness of the 26.5 density class (sci:597145cb).

We tested one candidate second process before we saw any result: the VOLUME of winter convective renewal, set by the
winter air-sea heat loss in the Eighteen Degree Water (EDW) formation region. Then, after this test failed, we did
labelled exploratory analyses to find which part of the swings the BATS class volume can explain, and which surface
quantity controls that volume.

Note: the first plan of this job (a Southern Hemisphere out-of-sample test of the North Pacific outcrop rule) was
stopped before any result was calculated, because sci:a60cb27a had already published that test.

## 2. Data

* Forcing. NCEP/NCAR Reanalysis 1 monthly net upward surface heat flux Q = lhtfl + shtfl + nlwrs + nswrs (NOAA PSL
  sign convention, upward positive). Index F_t = mean of Q over December(t-1) to March(t) over the ocean points
  (ERSSTv5 mask) of the box 30-40 N, 75-45 W (85 points). Variants: 33-40 N, 70-55 W; January-March.
* Competing forcing. The annual late-winter surface sigma0 maps of sci:058edf7b (WOA23 decadal backbone plus the
  ERSSTv5 interannual anomaly). O_t = fraction of box cells with sigma0 >= 26.45 ("outcrop index");
  sigw_t = box-mean late-winter sigma0 (used only in the exploratory part). All indices are standardized on 1981-2010.
* Target at BATS. Annual AOU on sigma0 26.5 and the thickness h of the 26.5 class (sci:597145cb, from BCO-DMO
  dataset 3782 v10), 1989-2025.
* Sections. The 11 GLODAP line-pair AOU changes on 26.5 of A05, A16N, A20 and A22 (sci:dcfc9b0b) and the mid-dates
  of the corresponding GLODAPv2.2023 cruises (files/inputs/cruise_dates.csv).

## 3. Methods

Pre-registered renewal box (files/code/analysis_plan.md, SHA-256 in analysis_plan.sha256, written before any index
was compared with AOU, thickness or sections):

A_t = (1 - r_t)(A_{t-1} + J) + r_t A0, with r_t = clip(rbar (1 + b z_t), 0, 0.95),

J = 4.6 umol/kg/yr (A22 CFC/SF6 oxygen utilization rate; variants 3.6 and 5.6). The value at a sampling time is
A_t + J s, with s the time after the end of winter t (end of March). Spin-up from 1950. rbar, b and A0 are fitted by
least squares on BATS 1989-2009. Models: M0 (b = 0), MQ (heat-loss index), MO (outcrop index), MQO (both).
Tests: H1 b > 0 and F-test p < 0.05 against M0 in training; H2 BATS 2010-2025 RMSE of MQ below M0 and MO, r >= 0.5;
H3 4/4 signs and median |model|/|observed| >= 0.5 for the four A20/A22 1997-2003 and 2003-2012 pairs;
H4 r(heat-loss index, class thickness) >= 0.4 and larger than for the outcrop index. Null: 999 random year orders
of the index, with refit.

Exploratory (added after the tests failed):
* E1. BATS as a proxy: the BATS annual AOU (and its thickness) interpolated to the cruise mid-dates, compared with
  the section changes.
* E2. Two-stage class-volume model: stage 1, h_t = c + phi h_{t-1} + kappa z_t, simulated from the observed 1989
  thickness only (no later observed h), fitted on 1990-2009; stage 2, AOU_t = alpha + beta h_t, fitted on observed
  1989-2009 values (beta = -0.156 umol/kg per m). Forcings: heat loss, outcrop index, box-mean late-winter sigma0,
  and variants (core box, linearly detrended sigma0, sigma0 minus its linear heat-loss part). Null: 999 random year
  orders of sigw with refit.

## 4. Results

### 4.1 Pre-registered tests: the heat-loss renewal hypothesis fails

| Test | Result | Pass |
|---|---|---|
| H1 training fit | b = 0.18, F = 7.05, p = 0.016 (but A0 at its bound, rbar 0.06: weakly constrained) | yes |
| H2 BATS 2010-2025 | RMSE MQ 14.4 vs M0 10.4 vs MO 8.4 umol/kg; r MQ 0.13 (MO 0.80) | no |
| H3 A20/A22 swings | 4/4 signs, median ratio 0.28 (MO 0.24, MQO 0.37); all 11 pairs: 7/11 signs, r 0.58 | no |
| H4 class thickness | r(heat loss, h) = 0.16; r(outcrop index, h) = 0.52 | no |
| Year-shuffle null | p = 0.99 (BATS RMSE), 0.49 (BATS r), 0.41 (section r), 0.17 (swing) | no skill |

All six pre-set variants (core box, January-March, J = 3.6 and 5.6, one-year lag, fit on 1989-2025) also fail
H2-H4 (files/results/preregistered/tests_*.json). With the full-period fit, b becomes negative (-0.12, p = 0.07).
The heat-loss index is physically sensible: it is largest in 2010 (+2.6 s.d.) and low in 2012 (-0.7 s.d.), and it
correlates with the BATS winter mixed-layer depth (r = 0.39). But it does not predict the thickness of the 26.5
class (r = 0.02 with the total EDW thickness). After 2013 the winter heat loss was near or above normal, while the
late-winter surface sigma0 was 1-2.4 s.d. low (Fig. 1).

### 4.2 Exploratory: what the BATS class volume explains

| Predictor of the 11 section changes | Signs | r | slope obs/model | A20/A22 swing ratio |
|---|---|---|---|---|
| BATS own AOU at the cruise dates (E1) | 10/11 | 0.89 | 1.04 | 0.75 |
| BATS observed 26.5 class thickness via stage 2 (E1) | 10/11 | 0.86 | 1.83 | 0.56 |
| Class-volume model, late-winter sigma0 (E2) | 10/11 | 0.87 | 1.72 | 0.44 |
| Class-volume model, heat loss (E2) | 6/11 | 0.34 | -0.82 | 0.08 |
| Pre-set MQ heat-loss box | 7/11 | 0.58 | 0.94 | 0.28 |
| sci:058edf7b annual outcrop-gap model, best sets | 9-11/11 | 0.81-0.84 | 1.7-2.7 | 0.25-0.31 |

* The swings are basin-coherent. The BATS series alone, sampled at the cruise dates, reproduces the section changes
  with slope 1.04. So the missing process acts at BATS too; it is not section noise.
* The observed 26.5 class thickness at BATS accounts for about three quarters of the BATS-represented swing (0.56 of
  0.75), and with the 1989-2009 relation it predicts BATS AOU in 2010-2025 with r = 0.95, RMSE 4.9 umol/kg.
* A class-volume model forced only by box-mean late-winter surface sigma0, with memory phi = 0.65 (e-folding about
  2.3 yr), predicts the 2010-2025 thickness (r = 0.91, shuffle p = 0.004) and AOU (r = 0.93, RMSE 8.0; shuffle
  p = 0.014), and gives 10/11 section signs (r 0.87, p = 0.028) and 0.44 of the swings (p = 0.007).
* The heat-loss index in the same model fails (6/11 signs, swing ratio 0.08). The part of late-winter sigma0 that is
  not linearly explained by heat loss still predicts thickness (r = 0.65) and the swings (0.43). The box-mean
  sigma0 index has a trend of -0.30 s.d. per decade; with it removed, the section result holds (10/11, r 0.86) but the
  swing ratio falls to 0.30 and the BATS 2010-2025 RMSE (10.5) is not better than M0 (10.4). The core box gives 0.29.
* All models stay about 10 umol/kg below the observed BATS AOU in 2015-2025 (Fig. 2), as noted in sci:597145cb.

## 5. Interpretation

The amount of winter heat loss over the EDW formation region does not control the renewal of the sigma0 26.5 class.
The late-winter surface density does. It contains the heat loss, but also the pre-winter upper-ocean heat content
and the post-2013 surface warming. The class volume integrates this forcing over 2-3 winters, and AOU follows the
volume. This class-volume memory, which fixed-geometry ventilation models do not have, increases the modelled
swings from 0.25-0.31 to about 0.44 of the observed size. The BATS observations show that the volume route can give
at most about 0.56 and the full BATS signal 0.75. Thus about half of the "second process" is the class-volume
renewal set by the late-winter density; the remainder is AOU variability inside the class that thickness does not
explain, or section sampling that BATS does not represent. This agrees with the North Pacific result (sci:a60cb27a,
sci:84f111c0) that oxygen on 26.5 follows the late-winter surface density, but in the NA the response acts through
the volume of a still-outcropping class, not through a full loss of the outcrop.

## 6. Limitations

* Only the heat-loss hypothesis was pre-registered; the class-volume results are exploratory and were found after
  the failure, with 3 free parameters fitted on 21 years. The shuffle nulls do not correct for the choice among
  the forcings that we tried (heat loss, outcrop fraction, sigma0, and four variants).
* One site (BATS) represents the 15-40 N sections; 11 line pairs, of which only 6 are A20/A22.
* The late-winter sigma0 index uses only an SST anomaly on a decadal WOA23 salinity backbone; NCEP R1 fluxes have
  known biases; one formation box.
* The renewal box has a weakly constrained fit (A0 at its bound); a different structure could behave otherwise.
* Stage 2 uses a linear AOU-thickness relation from 1989-2009; it does not include an oxygen budget or a
  respiration change.

## 7. Files

* files/code/: analysis_plan.md (pre-registration) and analysis_plan.sha256; load_glodap.py, cruise_dates.py,
  forcing.py (inputs); renewal_box.py (pre-set tests); explore_volume.py, forcing_explore.py (exploratory);
  figures.py; run_all.sh.
* files/inputs/: unchanged copies of the prior SCI aggregates used (see provenance), and the forcing and cruise
  tables made here.
* files/results/preregistered/: tests_<variant>.json, pairs_*.csv (section predictions), series_*.csv (model
  series 1950-2025), shuffle_main.csv.
* files/results/exploratory/ and exploratory_variants/: volume_tests.json, volume_pairs.csv, volume_series.csv,
  volume_shuffle.csv.
* files/figures/: fig1-fig4. files/provenance/inputs.json: source URLs and SHA-256 of all external inputs.
* files/NOTICE_external_data.md: licenses and attribution of external data.

## 8. Reproduction

    bash files/code/run_all.sh files /tmp/new_scratch            # from the bundled inputs (about 2-3 min)
    bash files/code/run_all.sh files /tmp/new_scratch DATASETS    # also rebuild forcing.csv and cruise_dates.csv

DATASETS must hold the NCEP R1, ERSSTv5 and GLODAPv2.2023 files at the relative paths in provenance/inputs.json
(download them from the listed URLs). Python 3.12 with numpy, pandas, scipy, netCDF4 and matplotlib. A rerun from the
bundled inputs reproduced every number in this README (see files/results/repro_check.txt).
