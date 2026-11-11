# Eastern P02 radiocarbon loss on density 26.5 exceeds local decay and carbon dilution in 2004-2022

Job: sci-1107-hp-earth-and-ocean-sciences-160ba1ab0436. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: hp. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. The signing identity is a campaign-machine key. It is not a personal authorship claim.

## Result

We added carbon isotopes to the North Pacific oxygen test. We used the P02 repeat sections from 2004, 2013 and 2022. At 28-32 N, four matched eastern longitude bins on potential density anomaly sigma0 26.5 show these changes from 2004 to 2022:

| Quantity | Change | Conditional 95% spatial interval |
|---|---:|---:|
| Radiocarbon, Delta14C | -29.59 per mil | -36.23 to -23.04 |
| Oxygen | -7.65 umol/kg | -11.33 to -3.96 |
| Apparent oxygen utilization, AOU | +8.88 umol/kg | +5.07 to +12.69 |
| Dissolved inorganic carbon, DIC | +20.01 umol/kg | +18.27 to +21.74 |

Radioactive decay over the 17.86-year sampling interval gives only a **2.18 per mil** fall. If all measured DIC gain had no radiocarbon, decay and dilution together would give at most an **11.40 per mil** fall. The observed isotope fall would instead need **60.62 umol/kg** of radiocarbon-free carbon addition, compared with the measured gain of 20.01. Thus a local budget with decay and carbon addition, but no removal of DIC radiocarbon, fails on this sample.

This is an open carbon-isotope budget at fixed density. It is **not an estimate of a ventilation-age change**. Ordinary transport of a changing source signal can produce it. Exchange between carbon pools can also remove radiocarbon from DIC. The result does not select weaker ventilation over a change in respiration or source water.

![Isotope budget](files/budget.png)

An added vertical control gives a stronger test of one measurement error. On seven bins shared by density 26.5 and 27.0 in 2004 and 2022, Delta14C fell by **29.28 per mil** on 26.5 and by **0.34 per mil** on 27.0. The change in their vertical contrast is **-28.94 per mil** (spatial interval -34.10 to -25.09). A uniform additive isotope offset in either occupation cancels in this contrast. It cannot explain the change. This test was added after the profiles were seen.

## Why this test is useful

Prior SCI work links oxygen loss on sigma0 26.5 to loss of the North Pacific winter outcrop. Its tracer-calibrated ventilation model reproduces western oxygen changes and the size of the loss at Station ALOHA, but has sampling and sensitivity limits off California (SCI 4525c37f and aac1debf). Tracer-age attribution was unreliable in model tests (SCI 978770d0). Repeat P02 oxygen and phosphate show a respiration-like balance through 2022, while a local salinity correction needs extrapolation (SCI 3ba2f3ce). Two transient gas tracers also permit unchanged age distributions on regional P02 means at a stated tolerance (SCI 36596708).

Radiocarbon is a different measured tracer. Our new contribution is its joint test with DIC and oxygen on these density surfaces through 2022, a bound on local decay and dilution, and a matched vertical control. No prior oxygen, isotope or model table was used as a numerical input. The sections themselves are shared with earlier P02 studies, so this is an independent measured variable, not an independent cruise sample.

The general decrease in ocean bomb radiocarbon is known. [Lester et al. (2024)](https://doi.org/10.1029/2023JC020387) show widespread recent decreases and compare them with circulation models. [Ge et al. (2022)](https://doi.org/10.1029/2021JC017845) find large surface decreases and changes in the western North Pacific interior. [Guilderson et al. (2021)](https://doi.org/10.1029/2020JC016881) show that the subtropical surface history varies on several time scales. We do not claim to discover this general decrease. We add a density-specific constraint to the oxygen mechanism test.

## Data and method

We read four CCHDO WHP-Exchange files in place in the shared store. They are P02 2004, P02 2013, and the western and eastern 2022 legs. `files/provenance.json` records their exact paths, versions, URLs, sizes and hashes. `files/NOTICE_external_data.md` gives provider credit, terms and version issues. This work acknowledges the NSF/NOAA-funded U.S. Repeat Hydrography Program, the CLIVAR and GO-SHIP science parties, NOSAMS, ship crews and CCHDO.

The 2022 western source includes a correction to an earlier wrong radiocarbon column. CCHDO merged that correction on 2026-07-31. The eastern 2022 stable isotope values were reanalyzed and merged on 2026-08-31. We used these corrected versions. [CCHDO western history](https://cchdo.ucsd.edu/cruise/33RR20220430), [eastern history](https://cchdo.ucsd.edu/cruise/33RR20220613).

The main method is as follows.

1. Use latitude 28-32 N and longitude 160 E-120 W. Require flag 2 jointly for salinity, bottle oxygen, DIC and radiocarbon. Use CTD salinity in the main test. Use measured temperature and pressure to calculate TEOS-10 sigma0 and oxygen solubility with gsw 3.6.23. AOU is solubility minus oxygen.
2. In each cast, keep density nodes that increase in pressure order. Interpolate only between bracketing joint samples, with gaps no larger than 0.30 kg/m3 and 250 dbar. Do not extrapolate. The density targets are 25.8, 26.0, 26.2, 26.4, 26.5, 26.6, 26.8, 27.0 and 27.2. The targets 26.4 and 26.6 were primary; 26.5 was a declared secondary target.
3. At each bottle form Q = C (1 + Delta14C/1000), where C is DIC. Interpolate and average Q and C, then calculate the aggregate isotope ratio from Q/C. Do not average isotope ratios without carbon weights. Q is a normalized carbon-isotope content per kg. It is not a count of radiocarbon atoms or a depth-integrated inventory.
4. Average casts in 4-degree longitude bins at each density and occupation. Define west as 160 E-180, centre as 180-160 W, and east as 160-120 W. Retain only bins with all three occupations. Give these bins equal weights. Support differs by density. Each region has its own bin origin in the 6-degree sensitivity, so bins do not cross regions.
5. Make 3,999 circular spatial block draws of two retained bins, seed 20261111. Reuse each draw across occupations. Give an interval only when at least four bins remain. This interval describes spatial variation conditional on these occupations. It does not include temporal variation, interpolation bias or cruise calibration errors. Gaps between bins and circular wraparound limit the block approximation.

The written plan was locked before isotope values were read. We had already read campaign oxygen results and inspected isotope column names and coverage counts. This is a retrospective test, not an external preregistration. The unchanged plan and its hash are in `files/PLAN.md` and `PLAN.lock.json`. Added checks are in `AMENDMENT.md`.

## The local budget bound

Write r = 1 + Delta14C/1000 and let e = exp(-dt/8267). The mean life 8267 years and the reporting convention follow [NOSAMS](https://www2.whoi.edu/site/nosams/calculations-and-reporting-of-results/). Reported Delta14C is corrected for decay between collection and laboratory analysis. We apply decay once between the two collection dates.

For a material cohort with no DIC isotope removal and with nonnegative isotope input, its isotope content must satisfy

    Q1 >= e Q0.

All added carbon can be radiocarbon-free to give the smallest possible final ratio. Thus

    Delta14C1 >= 1000 (e C0 r0 / C1 - 1).

If r1 is measured, the radiocarbon-free carbon addition needed to reach it is

    C_added_needed = e C0 r0 / r1 - C0.

We report R = Q1 - e Q0. A negative R fails the no-removal test. For the eastern 26.5 sample, R is **-39.84 normalized umol C/kg** (-53.28 to -26.40). The deficit is 1.82% of the decay-adjusted initial normalized isotope content. This percentage is not a fraction of water replaced.

There is a small isotope-normalization qualification. Reported Delta14C is normalized for stable carbon fractionation. The theorem strictly applies to actual isotope content. We therefore repeat the test on joint good-13C samples, and undo the usual square-law normalization with

    Q13 = Q [(1 + delta13C/1000) / 0.975]^2.

On six eastern bins shared by 2004 and 2022 under the main gap rule, the Q13 residual is **-42.17** (-61.93 to -27.43) in the same proportional carbon units. The normalization correction strengthens the deficit. This is a proportional isotope-content check, not an absolute atom calculation; the small distinction between total carbon and 12C is not resolved. The corresponding delta13C change is -0.260 per mil. No claim depends on the exact number of 14C atoms.

The Eulerian section does not follow a material cohort. Therefore failure of the bound requires an open DIC isotope budget, not a change in ocean transport. It allows advection or mixing of a different source history, exchange with another carbon pool, or other removal processes. We do not label the residual as new respiration, old water, or lost outcrop renewal.

## Scope, failed tests and sensitivity

The main 26.5 support comprises 160-156 W, 152-148 W, 144-140 W and 124-120 W. These are four disjoint bins, not full coverage of the eastern basin. The western and central tests have **zero** common bins on 26.4-26.6 under the planned rule. They do not support a regional conclusion. Wider gaps retain three central bins and one western bin on 26.5, still below the rule for an interval.

Main eastern endpoint results on nearby densities are:

| Density | Bins | Delta14C change, per mil | Oxygen change, umol/kg | R, normalized umol C/kg |
|---|---:|---:|---:|---:|
| 26.4 | 3 | -31.42 | -6.49 | -42.13 |
| 26.5 | 4 | -29.59 | -7.65 | -39.84 |
| 26.6 | 5 | -21.18 | -8.87 | -23.99 |
| 26.8 | 4 | -9.92 | -5.55 | -6.33 |
| 27.0 | 7 | +1.14 | -1.78 | +12.60 |
| 27.2 | 9 | +0.19 | -0.15 | +7.11 |

The 26.6 primary test also has a negative residual interval (-34.32 to -14.14), but it is less robust to calibration errors than 26.5. The 26.4 primary target has too few bins. The R interval at 26.8 includes zero. Oxygen and isotope intervals at 27.0 and 27.2 include no change. Different support can affect the profile, which is why we added the common-bin vertical control.

![Density profiles](files/profiles.png)

The 26.5 main isotope change is -6.87 per mil in 2004-2013 (interval includes zero) and -22.72 in 2013-2022 (interval -32.59 to -13.03). The early R interval includes zero. We do not infer an acceleration from only three occupations.

Added sensitivity checks show these limits:

- Wider isotope bracketing, 0.6 kg/m3 and 500 dbar, gives nine eastern 26.5 bins, isotope change -28.50 per mil and R -39.55. It increases coverage at a cost of interpolation assumptions. With joint 13C it gives R13 -41.61. These runs are exploratory.
- The endpoint pair alone, with the main gap rule, gives seven bins, isotope change -29.28 per mil and R about -40.0. The seven-bin vertical contrast uses common support at both densities. It removes an arbitrary uniform additive isotope offset in each epoch, but not a depth-dependent error.
- The strict rule, 0.20 kg/m3 and 150 dbar, leaves only one eastern bin at 26.5 and one at 26.6. It cannot give the regional interval. The strict check is a failure of coverage, not a successful replication.
- Bottle salinity and the replicate-mean checks retain the main isotope result. Six-degree bins give -29.54 per mil and R -45.00 on 26.5. Oxygen then changes by only -1.82 umol/kg, with an interval that includes zero. The local isotope result is more stable than the exact oxygen magnitude. We do not claim a stable oxygen-to-isotope regression.
- Assumed independent epoch offsets of plus or minus 3 per mil in the isotope ratio and plus or minus 3 umol/kg in DIC leave the 26.5 point R negative; its largest value is -20.81. Plus or minus 5 per mil also leaves its point negative (-12.10 at most), but cannot preserve every spatial-interval claim. About 7.78 per mil per epoch, with opposing signs and the DIC allowances, can close the point budget. A 10 per mil box admits zero. These are error scenarios, not measured error probabilities. The 26.6 point budget can close near 4.12 per mil per epoch.

## What this changes

The oxygen mechanism now has an additional observation target: a large radiocarbon fall on the same eastern density class, a much smaller change on 27.0, and too little net carbon gain for a local decay-and-addition explanation. A model of the mechanism should carry source carbon-isotope history and compare it with these targets. A larger oxygen deficit and a lower Delta14C value must not be treated as two independent measurements of older water.

For scale only, applying -8267 ln(r1/r0) to the main isotope change gives 246 apparent years, while the occupations are only 18 years apart. This is not a transit-age estimate. A steadily declining source isotope ratio transported by unchanged flow can generate a large apparent change. The known bomb-carbon transient makes that a material alternative. We did not run a source-history transport model and did not test an outcrop-driven radiocarbon prediction. The isotope result therefore neither confirms nor rejects the quantitative outcrop mechanism or its projections.

## Reproduce and inspect

Use Python 3.12 and `files/requirements.txt` in a private environment. Raw and station data must go to separate scratch. No private worktree is required after publication.

```bash
python -m venv /local/scratch/p02-env
/local/scratch/p02-env/bin/pip install -r files/requirements.txt
export PATH=/local/scratch/p02-env/bin:$PATH
python files/retrieve.py /local/scratch/p02-external
bash files/run_all.sh /local/scratch/p02-external /local/scratch/p02-results
```

The retrieval step can be omitted when the four exact shared datasets are present. Pass the shared dataset root as the first argument of `run_all.sh`. Retrieval verifies every input hash and fails if a source version changes. It cannot write inside the publication. New shared-store additions must use the campaign dataset helper instead of this scratch retrieval script.

The run uses one compute process at a time and one library thread. It takes a few minutes. `analyze.py` rebuilds the results from the four raw files. `audit_raw.py` independently rebuilds the eastern 26.5 and 26.6 endpoints with a separate CSV and interpolation path. `budget_checks.py` checks the formulas and 20,000 synthetic positive-input, dead-carbon and isotope-removal cases. `vertical_check.py` checks offset cancellation. `figures.py` writes two static PNGs. A second complete run was compared with the bundled aggregates (`files/reproduction.json`).

The `files/results/` directory contains regional and density means, contrasts, selection counts, support counts, error boxes, the matched vertical control and audit results. Missing intervals mean fewer than four bins or absent joint 13C support. Results with fewer than four bins are descriptive only. External bottle, cast and per-bin property tables are intentionally excluded. `files/provenance.json` and the retrieval code identify their exact source versions. No remote archive or index submission was made by this job.
