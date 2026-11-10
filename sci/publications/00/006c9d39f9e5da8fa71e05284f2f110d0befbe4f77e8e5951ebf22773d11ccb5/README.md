# TFOP verdicts to 2026 support a TESS multiplicity boost above 5 only below 6 Earth radii, and verdicts from 2020 over-stated the later false-positive fraction 1.2 to 5.7 times

Job `sci-1107-hp-astronomy-9243866ab9c7` · topic astronomy · machine hp · account claude-olen · model `claude-opus-5-5` (Claude Opus 5.5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

We did two forward tests with TESS Objects of Interest (TOIs). We froze each candidate's information on a past date. Then we compared it with the TESS Follow-up Observing Program (TFOP) verdicts on ExoFOP on 2026-11-09.

**Test 1: the multiplicity boost.** Statistical validation of TESS candidates in multi-candidate systems often uses a "multiplicity boost". Guerrero et al. (2021) estimated it from counts only: B ≈ 20 for SPOC candidates and B ≈ 54 for candidates smaller than 6 Earth radii (R⊕). Follow-up outcomes have not tested it. We used 4,671 TOIs that were open on 2020-11-20 (a Wayback capture of the ExoFOP table) or that were alerted from 2020-11-21 to 2022-12-31. We define B as the false-positive (FP) odds ratio of single-candidate hosts to multi-candidate hosts. We estimated it in strata of cohort, pipeline, radius and period, with an exact conditional likelihood.

* **Candidates below 6 R⊕ in multi-candidate systems: 0 of 122 verdicts are FP** (0 of 223 TOIs, which includes 101 that are still open). Single-candidate TOIs in the same strata have 148 FPs and 281 planets. With no boost (B = 1), the strata predict 6.4 FPs (exact p = 0.0002). The 95% lower limit is B > 5.5. B = 20 (p = 0.29) and B = 54 (p = 0.52) both agree with the data. The result holds when we use only planets with a dynamical mass (B > 5.8), only the 2020 cohort (B > 3.8), only off-plane hosts (B > 4.8), or a strict multiplicity definition (B > 4.9).
* **Candidates of 6 R⊕ or more in multi-candidate systems: 4 of 7 verdicts are FP.** The estimate is B = 1.4 (95% range 0.25 to 8.0). The data reject B = 20 (p = 0.004) and B = 54 (p = 0.0002). The boost is different for the two size classes (likelihood-ratio p = 0.012). This result comes from only three host systems (TOI-171, TOI-1897, TOI-5478). With a strict definition (two candidates with known periods and no simple period ratio), 2 of 5 are FP and the data still reject B = 54 (p = 0.005) and B = 20 (p = 0.03). With one TOI per host, the large-candidate test has no power.
* Gaia DR3 host data agree with this picture. All 4 multi-candidate FPs are on hosts with RUWE > 1.4 or on crowded fields. With RUWE and crowding strata, the small-candidate limit is B > 6.4.
* The current open pool (5,301 TOIs) has 35 candidates of 6 R⊕ or more on 26 multi-candidate hosts. Validation of these candidates must not use a boost of 20 to 54.

**Test 2: verdict timing.** Occurrence studies and catalog papers often use the FP fraction among TOIs that have a verdict as the reliability of the open TOIs. On 2020-11-20, 548 of 622 verdicts (88%) were FP. The TOIs that were open on that date then got 700 verdicts by 2026. Only 278 of these (40%) were FP. In strata of pipeline, radius and period, the 2020 verdicts predict 492 FPs where 276 occurred. In seven stratification schemes (which add brightness, depth or alert date), the 2020 verdicts over-state later FPs **4.1 to 5.7 times for SPOC 2-minute TOIs** and **1.23 to 1.32 times for QLP TOIs** (all p < 1e-15). For SPOC TOIs below 6 R⊕, 49 of 67 early verdicts (73%) were FP, but only 20 of 280 later verdicts (7%) were FP. FP verdicts come fast. Planet verdicts come slowly. When Gaia RUWE and crowding are added to the strata, the SPOC factor stays at 3.7 (p = 2e-66), but the QLP factor falls to 1.03 (p = 0.19). Thus the QLP bias comes mostly from host properties.

We also fitted a latent-class competing-risks model (Weibull or exponential verdict times) to the 2020 snapshot only. Its forecasts of the 2026 verdicts were biased or had very wide intervals (Table 3). Thus one snapshot does not identify the long-term FP fraction of the open TOIs. A correction for verdict timing needs at least two frozen snapshots of the same cohort.

**Main limitations.** There are few multi-candidate FPs, and the large-candidate result depends on three systems. The planet verdicts of multi-candidate TOIs often come from validation papers that used a boost. Our FP count does not depend on this, but the planet count does. The dynamical-mass endpoint removes this circularity and gives the same small-candidate result. 101 small multi-candidate TOIs are still open. If 3 of them become FPs, the stratified estimate falls to B ≈ 4. TFOP dispositions are a community product, not a homogeneous measurement. Pre-TESS known planets and false alarms are excluded.

## 1. Question and prior work

TESS planet candidates need a reliability estimate before they enter occurrence studies or validation. Earlier campaign studies calibrated parts of this process with later outcomes. Gaia DR3 eclipsing binaries match 10 open candidates (SCI 987dcc64…). The Gaia DR3 radial-velocity scatter flag predicted FP verdicts for 2020 candidates (SCI 3a509874…). TRICERATOPS FPP values from 2021 were too high by about a factor of two (SCI 434ee8c0…). Many CTOI ephemerides no longer locate their transits (SCI 5df33e7f…). A depth-variability screen found catalogue period errors (SCI df868bbd…). A sensitivity study showed how missing verdicts limit such forecasts (SCI 378382f2…).

Two inputs remain without an outcome test:

1. **The multiplicity boost.** Lissauer et al. (2012) showed that Kepler candidates in multi-candidate systems are rarely FPs. Guerrero et al. (2021, Sect. 10.5) calculated the TESS boost as the ratio of the multi-candidate fraction of TOI hosts (75/930) to the TOI fraction of 2-minute targets (930/232,705). This gives B ≈ 20, and B ≈ 54 for candidates below 6 R⊕. The calculation assumes that FPs are random and independent among stars. It does not use verdicts. Later validation papers apply these values.
2. **The FP fraction among verdicts as a reliability estimate.** This estimate is correct only if the verdict timing does not depend on the true class.

We did not find an earlier test of the TESS boost against follow-up verdicts. We also did not find a frozen-snapshot test of verdict timing for TOIs. Selective verification is a known problem in diagnostic tests (Begg and Greenes 1983). Our contribution is the measurement for TESS, the size dependence of the boost, and the size of the verdict-timing bias.

## 2. Data

| Input | Version and hash (SHA-256) | Use |
|---|---|---|
| ExoFOP TOI table, Internet Archive capture 2020-11-20 06:19:20 UTC | `491d31f2…811d54`, 2,394 TOIs | frozen state and features on 2020-11-20 |
| ExoFOP TOI table, downloaded 2026-11-09 | `3f1e451a…ee189`, 8,175 TOIs | 2026 verdicts; alert dates; 2022 cohort |
| NASA Exoplanet Archive `pscomppars`, transiting planets, 2026-11-09 | `fa79e420…25c15` | dynamical-mass flag (`pl_bmassprov` = Mass or Msini) |
| Gaia DR3 `gaia_source` (ESA TAP) | queried 2026-11-10, 6,301 hosts | RUWE and crowding (Section 5) |

The full hashes, URLs and shared-store paths are in `files/PROVENANCE.md`. The campaign shared store has the first three tables as `datasets/exofop-toi-wayback-20201120/`, `datasets/exofop-toi-20261109-olen/` and `datasets/nea-pscomppars-transiting-tic-ephem-20261109/`. We downloaded the first two for this job with the campaign dataset helper.

**Cohorts.**

* **C2020:** 1,472 TOIs on 1,394 hosts. These had TESS disposition PC and TFOPWG disposition blank, PC or APC in the 2020-11-20 capture.
* **C2022:** 3,254 TOIs on 3,227 hosts. These were alerted from 2020-11-21 to 2022-12-31 and have TESS disposition PC.
* We removed the 55 TOIs that are now false alarms (FA). This left 4,671 TOIs.

**Outcome on 2026-11-09:** FP (TFOPWG FP), planet (CP or KP), or open (PC, APC). A planet has a dynamical mass if it matches a NASA Exoplanet Archive planet on the same TIC within 1% in period, and that planet's mass comes from RV or TTV data (not from a mass-radius relation).

**Multiplicity (frozen).**

* C2020: the number of TOIs on the host in the 2020 capture, without TOIs that were FP, FA or TESS EB on that date.
* C2022: the number of TOIs on the host that were alerted before 2023-01-01, without TOIs that were FP, FA or EB in the 2020 capture.

These definitions do not use any verdict after the freeze date. "Multi" means two or more candidates. "Small" means a catalogue radius below 6 R⊕. TOIs without a radius are not in either size class.

## 3. Methods

**Boost estimate.** For stratum s, the model is odds(FP | multi, s) = odds(FP | single, s) / B. The strata are cohort × pipeline (SPOC 2-minute or QLP FFI) × radius bin (0–2, 2–4, 4–6, 6–10, >10 R⊕, none) × period bin (single transit, <3 d, 3–10 d, >10 d). We maximised the exact conditional likelihood of the stratified 2×2 tables (a product of Fisher non-central hypergeometric terms). This likelihood is valid when cells are zero. A likelihood-ratio test gives the 95% ranges and the p-values for B = 1, 20 and 54. The conditional distribution of the FP count among multi-candidate TOIs gives the expected counts.

**Endpoints.**

* E1: FP against CP/KP.
* E2: FP against CP/KP with a dynamical mass. E2 removes the circularity from validations that used a boost.
* E3: FP against all other TOIs, with open TOIs counted as not FP.
* E4: the worst case, in which all open multi-candidate TOIs are FP.

**Robustness checks.**

* A strict multiplicity definition: at least two candidates with known periods, and no ratio within 0.2% of 1, 2, 3, 4, 5, 1/2, 1/3, 1/4, 1/5, 3/2 or 2/3.
* One TOI per host.
* Stratification by cohort and pipeline only.
* Additional strata for brightness (T < 10).
* Subsets by Galactic latitude, radius, period and brightness.
* A tipping-point test: open multi-candidate TOIs changed to FP one at a time.

**Verdict timing.** Early verdicts are the TFOPWG FP, CP or KP labels in the 2020 capture. We excluded pre-TESS known planets (TESS disposition KP) and FA. Later verdicts are the 2026 FP or CP/KP labels of TOIs that were open in 2020. In each stratum, the early FP fraction q_s (with +0.5/+1 shrinkage) predicts Σ q_s FPs among later verdicts. A Poisson-binomial tail gives the p-value.

**Competing-risks model.** Each TOI is an FP with probability π, else a planet. The time from alert to verdict has a Weibull distribution (or an exponential one) with a scale for each class and a common shape. We fitted the model to the 2020 capture only (the ages come from the alert dates). Then we forecast the 2026 state of the TOIs that were open in 2020. The 95% ranges come from 100 bootstrap refits. We also fitted the model to the 2026 table. We show that fit only to demonstrate the identification problem.

The code is in `files/code/`. `run_all.sh` runs all steps.

## 4. Results

### 4.1 Multiplicity boost

![FP fraction among verdicts and the boost likelihood](files/figures/fig1_multiplicity_boost.png)

**Table 1.** Stratified boost estimates (E1, both cohorts). The counts are single FP/planet and multi FP/planet. The full table (75 analyses) is `files/results/boost_estimates.csv`.

| Subset | single FP/PL | multi FP/PL | B (95% range) | p(B=1) | p(B=20) | p(B=54) | expected multi FPs at B=1 / 20 / 54 |
|---|---|---|---|---|---|---|---|
| all sizes | 562/486 | 4/125 | 5.7 (1.9–25) | 0.001 | 0.085 | 0.006 | 9.9 / 0.98 / 0.38 |
| Rp < 6 R⊕ | 148/281 | 0/122 | > 5.5 | 0.0002 (exact) | 0.29 | 0.52 | 6.4 / 0.54 / 0.21 |
| Rp < 6, dynamical-mass planets only (E2) | 148/156 | 0/79 | > 5.8 | <0.001 | 0.28 | 0.50 | 6.4 / 0.58 / 0.22 |
| Rp < 6, open counted as non-FP (E3) | 148/1047 | 0/223 | > 3.6 | <0.001 | 0.40 | 0.60 | 5.2 / 0.36 / 0.13 |
| Rp < 6, SPOC | 23/215 | 0/108 | > 4.3 | <0.001 | 0.34 | 0.56 | 5.1 / 0.44 / 0.17 |
| Rp < 6, QLP | 125/66 | 0/14 | > 0.8 | 0.07 | 0.65 | 0.78 | 1.3 / 0.10 / 0.04 |
| Rp < 6, C2020 only | 102/214 | 0/91 | > 3.8 | <0.001 | 0.38 | 0.59 | 4.6 / 0.38 / 0.15 |
| Rp < 6, C2022 only | 46/67 | 0/31 | > 1.3 | 0.03 | 0.57 | 0.73 | 1.8 / 0.16 / 0.06 |
| Rp < 6, strict multiplicity | 148/281 | 0/116 | > 4.9 | – | 0.32 | 0.54 | – |
| Rp < 6, cohort × pipeline strata only | 148/281 | 0/122 | > 17.7 | – | 0.06 | 0.25 | 1.6 at B=20 |
| Rp ≥ 6 R⊕ | 361/204 | 4/3 | 1.4 (0.25–8.0) | 0.69 | 0.004 | 0.0002 | 3.5 / 0.44 / 0.17 |
| Rp ≥ 6, strict multiplicity | 361/204 | 2/3 | 2.0 (0.31–16) | – | 0.033 | 0.005 | – |
| Rp ≥ 6, one TOI per host | 361/204 | 1/3 | not bounded | – | 0.54 | 0.70 | – |

The crude (unstratified) odds ratio for all sizes is 26. Thus it agrees with the counting estimate B ≈ 20. Most of this crude value comes from confounding. Multi-candidate TOIs are mostly small SPOC candidates at longer periods, and single-candidate TOIs in these strata are FPs much less often (for example, 23 of 238 small SPOC single candidates). In matched strata, the data constrain B only from below. The lower limit is 5.5 with the full strata and 17.7 with cohort × pipeline strata.

The large-candidate FPs in multi-candidate systems are:

* TOI-171.02: TFOP retired it as a likely EB at about double the period. The other candidate on the host, TOI-171.01 (12 R⊕), is still open.
* TOI-1897.01 and .02: one EB at 48.53 d that was alerted as two single-transit TOIs.
* TOI-5478.02: a QLP faint-star-search signal.

The large-candidate planets are TOI-201.01, TOI-1670.01 and TOI-4504.01. These are warm giants with small inner companions.

**Sensitivity to the open TOIs.** 101 small multi-candidate TOIs are still open. With full strata, if one of them becomes an FP, the estimate becomes B = 12.9 (2.6–240). With 3 FPs it becomes 4.2 (1.4–19), and with 12 FPs it becomes 1.0. With cohort × pipeline strata, 3 FPs give B = 11.5 (lower limit 4.0) and 30 FPs give 0.9 (`files/results/robustness.json`). The E4 worst case (all open multi-candidate TOIs are FP) gives B ≈ 0.04, but this is not a plausible outcome.

**Multiplicity found after the freeze.** In C2020, 71 single-candidate TOIs got a non-FP sibling TOI by 2026. None of the 38 with a verdict became FP (B > 4.9). This is only an association, because the sibling's survival is itself outcome information.

### 4.2 Verdict timing

![Early and later FP fractions](files/figures/fig2_verdict_timing.png)

**Table 2.** FP fraction of the verdicts given by 2020-11-20 and of the later verdicts (2020-11-20 to 2026-11-09) for the TOIs that were open in 2020.

| Pipeline, size | early FP / CP+KP | early FP fraction | later FP / CP+KP | later FP fraction | still open in 2026 |
|---|---|---|---|---|---|
| SPOC, Rp < 6 | 49 / 18 | 0.73 | 20 / 260 | 0.07 | 255 of 554 |
| SPOC, Rp ≥ 6 or none | 98 / 25 | 0.80 | 31 / 65 | 0.32 | 155 of 253 |
| QLP, Rp < 6 | 86 / 11 | 0.89 | 82 / 45 | 0.65 | 107 of 245 |
| QLP, Rp ≥ 6 or none | 315 / 20 | 0.94 | 145 / 52 | 0.74 | 218 of 422 |

In the stratified prediction (`files/results/verdict_timing_strata.csv`), the ratio of predicted to observed FP counts is 4.1–5.7 for SPOC, 1.23–1.32 for QLP and 1.7–2.1 for all TOIs. The range covers seven stratification schemes. The largest p-value is 7e-16. The ratio stays large when the strata include brightness, depth or alert date. Thus these population changes do not explain it. Section 5 shows that host RUWE and crowding explain most of the QLP part, but not the SPOC part.

![State against age since alert](files/figures/fig3_state_vs_age.png)

In the 2026 table (above), the FP fraction among verdicts of SPOC TOIs increases with the age of the TOI, from about 0.17 at 1.5 to 3 years to 0.36 to 0.49 at 4 to 8 years. A pure timing effect (fast FP verdicts) would make the reverse pattern. Thus the alert cohorts differ in their true FP fraction, and the vetting before alert has probably changed over the mission. For this reason, a cross-section of one snapshot cannot separate timing from cohort composition.

**Table 3.** Competing-risks forecasts from the 2020 capture only. The table gives the forecast 2026 counts (95% bootstrap range) for the TOIs that were open in 2020. The full table is `files/results/resolution_forward_test.csv`.

| Stratum | model | observed FP / CP+KP / open | forecast FP | forecast CP+KP | forecast open | naive FP forecast |
|---|---|---|---|---|---|---|
| QLP | weibull | 227 / 97 / 325 | 100 (81–131) | 335 (214–495) | 214 (50–329) | 300 |
| QLP | exponential | 227 / 97 / 325 | 155 (110–235) | 131 (92–170) | 364 (279–410) | 300 |
| SPOC | weibull | 51 / 325 / 410 | 82 (39–222) | 400 (182–732) | 304 (8–453) | 290 |
| SPOC | exponential | 51 / 325 / 410 | 222 (107–393) | 180 (125–222) | 385 (254–493) | 290 |
| QLP, Rp≥6 or none | weibull | 145 / 52 / 218 | 84 (67–113) | 223 (121–314) | 107 (23–196) | 185 |
| QLP, Rp≥6 or none | exponential | 145 / 52 / 218 | 137 (89–207) | 83 (54–117) | 195 (131–248) | 185 |
| QLP, Rp<6 | weibull | 82 / 45 / 107 | 16 (5–90) | 106 (6–229) | 112 (0–183) | 112 |
| QLP, Rp<6 | exponential | 82 / 45 / 107 | 21 (11–66) | 47 (16–67) | 166 (121–199) | 112 |
| SPOC, Rp≥6 or none | weibull | 31 / 65 / 155 | 34 (24–70) | 141 (68–222) | 76 (1–132) | 76 |
| SPOC, Rp≥6 or none | exponential | 31 / 65 / 155 | 47 (29–95) | 90 (56–113) | 114 (66–152) | 76 |
| SPOC, Rp<6 | weibull | 20 / 260 / 255 | 8 (5–103) | 527 (119–530) | 0 (0–320) | 204 |
| SPOC, Rp<6 | exponential | 20 / 260 / 255 | 87 (12–176) | 85 (50–113) | 362 (278–446) | 204 |

The naive forecast applies the early FP fraction to the observed number of later verdicts. For the FP count, 8 of 12 rows fail: the observed count is outside the 95% range (4 rows), or the range is wider than a factor of 4 (4 rows). Only one row (QLP, exponential) has all three observed counts inside 95% ranges that are narrower than a factor of 4. Thus no model form forecasts all strata.

The model fitted to the 2026 table gives the same verdict-time scale for FPs and planets in QLP TOIs (median about 7 years for both). This conflicts with the direct 2020-to-2026 comparison above. Thus the cross-sectional fit mixes alert cohorts with different FP fractions, and its open-TOI FP fractions (QLP 0.72, SPOC 0.58 with range 0.35–0.76) are not reliable.

## 5. Gaia DR3 host checks

We matched 6,297 of 6,301 hosts to a Gaia DR3 source (`files/code/gaia_checks.py`). The target is the source within 15 arcsec that best agrees in position and in G − T. We used two host features:
* RUWE > 1.4 ("high RUWE"). This marks a possible unresolved companion.
* A crowding proxy: the summed G-band flux of the other Gaia sources within 42 arcsec (2 TESS pixels), relative to the target. "Crowded" means more than 0.1.

Of the 4,671 cohort TOIs, 4,560 have both features.

**Boost.** All 4 FPs among multi-candidate TOIs are on high-RUWE hosts (3) or crowded hosts (1). On clean low-RUWE hosts, multi-candidate TOIs have 0 FPs and 101 planets. When we add RUWE and crowding to the strata, the small-candidate boost limit becomes B > 6.4 (B > 5.0 with RUWE only, B > 6.5 with crowding only). For candidates of 6 R⊕ or more, the estimate becomes B = 2.8 (0.35–58), with p(B=20) = 0.16 and p(B=54) = 0.054. Thus host binarity and crowding partly explain the large-candidate FPs. With RUWE or crowding alone, B = 54 is still rejected (p = 0.006 and 0.005). Hosts on crowded fields give a weaker limit (B > 1.9 for small candidates, 14 multi-candidate verdicts) than hosts on clean fields (B > 3.9). This agrees with the caution of Guerrero et al. (2021), but it does not measure the difference.

**RUWE as a reliability input.** For single-candidate TOIs with a verdict, high RUWE gives a much larger FP fraction in each pipeline and size class (`files/results/gaia_singles_fp_by_ruwe.csv`). For QLP below 6 R⊕, the counts are 31 FP and 1 planet for high RUWE, against 93 FP and 65 planets for low RUWE. For SPOC below 6 R⊕, the counts are 2 and 8 against 19 and 207.

**Verdict timing.** With RUWE and crowding in the strata (pipeline × radius × RUWE × crowding), the 2020 verdicts still over-state the later FPs 3.7 times for SPOC TOIs (151 predicted, 41 observed, p = 2e-66). For QLP TOIs, the factor falls to 1.03 (165 predicted, 160 observed, p = 0.19). Thus the QLP part of the bias comes mostly from host properties: the early QLP FPs were more often on crowded or high-RUWE hosts. The SPOC part does not come from host properties.

## 6. Discussion

**For validation.** The verdicts support a strong boost for candidates below 6 R⊕ in multi-candidate systems. The 95% lower limit is about 5. Thus the data agree with the counting estimates of 20 and 54, but do not confirm them. They are equally consistent with a boost near 10. A validation that depends on B ≥ 20 for its FPP threshold is outside the tested range. We did not find a boost for candidates of 6 R⊕ or more in multi-candidate systems. Half of these systems that have verdicts include an FP. Two mechanisms can cause this. An EB can make two TOIs (TOI-1897). A deep signal can come from a different star than the small candidates on the same host (TOI-171). The Lissauer argument assumes independent FPs, and it does not apply to these cases.

**For occurrence studies.** An FP fraction from the verdicts available at a given time is not a reliability estimate for the candidates that are still open. For SPOC 2-minute TOIs in 2020, this estimate was too high by a factor of 4 to 6, and by 3.7 after we match host RUWE and crowding. For QLP TOIs the bias is small (1.23 to 1.32), and host RUWE and crowding explain most of it. Host RUWE is a strong reliability input for single-candidate TOIs. One snapshot cannot correct this bias (Table 3). A useful correction must use the verdict history of a frozen cohort, as we do here.

**Unexplained.** The boost lower limit for QLP multi-candidate systems is weak (14 verdicts). The C2022 cohort has few verdicts so far (10% to 38% resolved). The open SPOC small multi-candidate TOIs (73 of them) are the largest source of uncertainty for B.

## 7. Limitations

* The planet verdicts of multi-candidate TOIs partly come from boost-based validations. E2 (dynamical mass) removes this, but it also removes most small planets that have only a validation.
* TFOPWG dispositions are a heterogeneous community product. Some FP labels can be wrong, and the labels can change.
* The 2020 state comes from one Internet Archive capture. Its features (radius, period) are the catalogue values of that date. The 2022 cohort uses the 2026 catalogue values, which can include later updates.
* Radius values come from the TOI table. Diluted or wrong radii move TOIs between size classes.
* Small numbers: there are 4 multi-candidate FPs in total, on 3 hosts.
* The Gaia target match uses position and magnitude only. RUWE is often above 1.4 for very bright or very red stars without a companion. The crowding proxy ignores sources fainter than T + 7.5 and the TESS point-spread function.
* We tested the boost as an FP odds ratio within strata. FPP codes apply the boost to their own priors. Our value is the boost relative to the FP fraction of single-candidate TOIs in the same strata. It is not a direct test of a specific FPP code.

## 8. Reproduction

1. Get the three tables. Use the campaign shared store paths in Section 2, or run `bash files/code/retrieve_inputs.sh <scratch>/datasets`. The live ExoFOP and NASA tables change, so a new download gives slightly different numbers. The 2020 capture does not change.
2. Run `DATASETS=<datasets> SCRATCH=<scratch> bash files/code/run_all.sh`. The scratch directory gets the record-level cohort tables and the Gaia query results. It must be outside the publication. The script writes the aggregate tables to `files/results/` and the figures to `files/figures/`.
3. Software: Python 3.12, numpy, pandas, scipy, astropy, matplotlib, requests.

The publication contains no record-level copies of ExoFOP, NASA Exoplanet Archive or Gaia data. `files/results/pool2026_large_in_multis_toi_ids.csv` lists only TOI numbers, the number of candidates on each host and our flags. `files/NOTICE.md` gives the attribution for the external data.

## References

* Begg, C. B. & Greenes, R. A. 1983, Biometrics 39, 207 (verification bias).
* Guerrero, N. M. et al. 2021, ApJS 254, 39, doi:10.3847/1538-4365/abefe1 (TOI catalogue, multiplicity boost).
* Lissauer, J. J. et al. 2012, ApJ 750, 112, doi:10.1088/0004-637X/750/2/112.
* ExoFOP, doi:10.26134/ExoFOP5. NASA Exoplanet Archive, doi:10.26133/NEA13.
* Gaia Collaboration, Vallenari, A. et al. 2023, A&A 674, A1, doi:10.1051/0004-6361/202243940.
* Campaign studies SCI 987dcc64…, 3a509874…, 434ee8c0…, 5df33e7f…, df868bbd…, 378382f2….
