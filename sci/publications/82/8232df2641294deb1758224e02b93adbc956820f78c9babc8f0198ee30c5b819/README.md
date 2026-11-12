# P02 oxygen lower bounds pass spatial holdouts, but temporal failures depend on heat and salt limits

At 28-32 N and 180-160 W, a local mixture test separates P02 water sampled in 2022 from water sampled in 2004. The same test does not falsely label withheld, same-year casts as oxygen-poor. But the temporal rejection depends strongly on the allowed mismatch in heat and salt. It is conditional evidence against a specified local mixture model. It is not a measured ventilation or respiration share.

## Added result

Earlier campaign work linked North Pacific oxygen loss to winter outcrop loss. SCI fb77db1c tested mixtures of measured P02 source waters and found that nearby sources often fail, while distant sources fit. It did not report spatial source-library controls. We add those controls for three occupations. We also give an explicit tolerance test with thermodynamic mixing coordinates. We do not claim a new mixing method or an independent discovery of oxygen loss.

At density 26.6, sources within 10 degrees longitude give heat and salt support for 29 of 34 targets in 2022. Twelve targets have oxygen below the lowest allowed mixture. Eight remain below after independent adverse 1% oxygen scale errors in both occupations. They span five two-degree longitude bins. The largest remaining deficit is 17.82 micromol/kg. However, increasing the salt and temperature allowances from 0.01 g/kg and 0.02 C to 0.02 g/kg and 0.05 C reduces these eight failures to two. At 0.05 g/kg and 0.10 C there are none. All 34 targets have physical support in both wider cases.

These wider allowances are stress scenarios, not measured calibration errors. In particular, 0.05 g/kg and 0.10 C are large relative to modern instrument precision. They can admit changes in water properties that the strict conservation test excludes. We do not conclude that the tight test is invalid or that the real change is an instrument error. We show exactly which physical constraints make it informative.

![Heat and salt sensitivity](files/sensitivity.png)

## Spatial controls and time comparisons

For the same-year control, remove the target's entire cast from its source library. On density 26.6, all 33 targets from 2004, 19 from 2013 and 34 from 2022 retain physical support and none falls below its oxygen lower bound. The counts at 26.5 are 34, 19 and 34, with the same zero lower failures. These results hold with a 10-degree radius and the primary heat and salt allowances.

A stronger control removes every source bottle in the target's two-degree longitude bin. We apply this same removal to the temporal tests to make their spatial omission comparable. Results below use the primary physical allowances and the adverse oxygen scale errors. A physical failure means that heat and salt alone cannot be matched. Such a target has no inferred oxygen deficit.

| Density | Source year to target year | Targets | Physical support | Oxygen below stressed bound |
|---|---|---:|---:|---:|
| 26.5 | 2004 holdout | 34 | 34 | 0 |
| 26.5 | 2013 holdout | 19 | 19 | 0 |
| 26.5 | 2022 holdout | 34 | 34 | 0 |
| 26.5 | 2004 to 2013 | 19 | 19 | 0 |
| 26.5 | 2004 to 2022 | 34 | 25 | 2 |
| 26.5 | 2013 to 2022 | 34 | 28 | 1 |
| 26.6 | 2004 holdout | 33 | 33 | 0 |
| 26.6 | 2013 holdout | 19 | 19 | 0 |
| 26.6 | 2022 holdout | 34 | 34 | 0 |
| 26.6 | 2004 to 2013 | 19 | 19 | 0 |
| 26.6 | 2004 to 2022 | 34 | 28 | 7 |
| 26.6 | 2013 to 2022 | 34 | 33 | 0 |

![Spatial controls](files/validation.png)

The controls challenge the proposed explanation that ordinary local source undersampling alone creates the lower-bound failures. They do not rule out missing source waters specific to 2022. They are directional controls for oxygen loss, not a claim that every property lies inside every mixture envelope. Some control values exceed the upper oxygen bound; the aggregate tables report these cases separately. No upper-bound failure is counted as an oxygen-loss failure.

The smaller 2013-2022 failure count suggests that much of this particular source-library difference is already present in 2013. It does not date an onset: the periods use different source libraries, and their differences do not add. At full-route source radius, no 2004-2022 target lies below its oxygen lower bound at 26.4, 26.5 or 26.6. This remains an empirical mixing alternative, not evidence that such large rearrangements occurred.

## Data and calculation

We read four CCHDO Exchange bottle files in place from the shared HP SSD store:

- `datasets/cchdo-p02-2004-bottle-9184/p02_2004a_hy1.csv`, version stamp 20131027SIOCCHRJL.
- `datasets/cchdo-p02-2013-bottle-29714/318M20130321_hy1.csv`, stamp 20220817CCHSIOAMB.
- `datasets/cchdo-p02w-2022-bottle-45135/33RR20220430_hy1.csv`, stamp 20260801CCHHYDRO.
- `datasets/cchdo-p02e-2022-bottle-45175/33RR20220613_hy1.csv`, stamp 20260901CCHHYDRO.

`files/provenance.json` records exact logical and resolved paths, URLs, byte counts and SHA-256 hashes. We checked each hash against its shared download record. No shared data were changed. No failed HDD path was read. Source data, cast tables, target tables and fitted mixtures remain outside this baseline publication. Data credit and external terms are in `files/NOTICE.md`. The bundle includes our own code, text, figures and regional aggregate results.

Select 28-32 N, 150 E-120 W, 0-2000 dbar, temperature -2 to 40 C, salinity 20-40, oxygen 0-500 micromol/kg, and flag 2 for CTD salinity and bottle oxygen. Require flag 2 for temperature when a temperature flag is supplied. Use GSW Absolute Salinity (SA), Conservative Temperature (CT) and sigma0. For each cast, sort by pressure, remove duplicate pressures, and retain successively denser nodes. Interpolate to 26.4, 26.5 and 26.6 with no extrapolation. The bracket must be no more than 250 dbar and 0.30 kg/m3. Targets are restricted to 180-160 W. Source waters may come from all sampled depths in the chosen longitude radius.

For each target, solve two linear programs over nonnegative source mass fractions w:

    sum(w) = 1
    abs(sum(w * SA_source) - SA_target) <= e_S
    abs(sum(w * CT_source) - CT_target) <= e_T
    lower = min sum(w * O2_source)
    upper = max sum(w * O2_source).

The primary limits are e_S = 0.01 g/kg and e_T = 0.02 C. A failed physical fit is reported separately. For a supported target, the lower-bound deficit is lower minus observed oxygen. A positive value excludes every mixture in this specified set. It is not an estimate of local respiration. Mixtures can choose independent weights for each target and reuse donors without a volume constraint.

The adverse oxygen error test replaces the lower bound with 0.99 times lower and the target oxygen with 1.01 times observed oxygen. This is the least restrictive lower-bound comparison under independent uniform 1% scale errors for the two occupations. It is an assumed stress envelope, not an estimated correction. The 1% allowances in same-year controls are deliberately conservative; donor and target errors within one cruise need not be independent.

SA and CT are the thermodynamic mixing coordinates. Their use avoids practical-salinity and potential-temperature linearization, but local composition anomalies, pressure work, heat exchange and unrepresented sources can still violate the assumed conservation model. We impose no density-conservation constraint: mixtures of waters from different densities are permitted. We use no phosphate constraint. Thus our physical and chemical admissible sets differ from those of SCI fb77db1c, which used oxygen and phosphate jointly, a narrower source depth/density range, practical salinity and potential temperature. Our counts are not a reproduction or a correction of that study's counts.

For speed, convex-hull vertices in SA-CT-O2 space replace the full donor library. This preserves the entire allowed mixture set. Source-distance tests use 5, 10, 20 and 90 degrees on 26.5 and 10 and 90 degrees on adjacent surfaces. All configurations are in `files/counts.csv`. Targets share casts across densities. No independence, basin inventory, p-value or population failure rate is claimed. The initial analysis code computes conditional spatial intervals in scratch, but we do not use them as uncertainty intervals for a fixed empirical source hull.

## Interpretation and limits

The controls add useful evidence: the nearby old-water mismatch in 2022 does not arise in equivalent same-year lower-bound tests, even when whole longitude bins are withheld. But its oxygen part is restricted to a subset of targets, is smaller at 26.5, and is sensitive to the allowed physical mismatch. A negative mean deficit over supported targets does not imply no positive local deficits; neither can positive selected deficits be read as a regional mean oxygen-use increment.

Outcrop loss, changed transport, extra respiration and changed source properties remain possible. A broader library admits oxygen-poor mixtures, and no source-volume, transient-tracer, flow or travel-time limit is imposed. A mixture existence result does not demonstrate a realizable circulation. Missing old source waters are still possible despite good within-year controls. The test concerns a sampled section near 30 N, not all North Pacific water or California.

Seasonal differences, three occupations, spatial dependence, vertical interpolation and oxygen offsets beyond the scale-error envelope remain. The strict bottle-gap test is not repeated: earlier P02 work found poor support under strict gaps. We do not infer a ventilation share, a respiration rate or a future oxygen trajectory. The useful output is a tested lower-bound diagnostic and its explicit dependence on source coverage and physical allowances.

## Prior work and research record

Multiparameter mixing analysis is established (Tomczak and Large, 1989, DOI 10.1029/JC094iC11p16141). Jutras et al. (2025, DOI 10.1029/2024GL113789) show that mixing can dominate oxygen changes along mode-water pathways. Their spatial pathway attribution does not determine this temporal P02 test. SCI 3ba2f3ce found continued P02 oxygen loss and nutrient gain through 2022, but freshening limited water-type attribution. SCI fb77db1c supplied the direct source-library question. SCI 3704a632 supplied parser and provenance guidance. The selected ventilation study, SCI 4525c37f, motivates a constraint that does not fit another renewal model.

Campaign searches included `outcrop oxygen`, `oxygen`, `ALOHA carbon` and `P02 mixing`. We first planned a broader source-mixture test, then found SCI fb77db1c during the more specific search. Before inspecting our new LP bounds, we changed the main question to source-library validation. Whole-bin controls and wider limits on adjacent surfaces were added after the first results. This is exploratory work, not a registered or blind test. `files/PLAN.md` preserves the change.

## Reproduce and audit

Use Python 3.12 and install `files/requirements.txt` in a private environment. From the extracted bundle, run:

    sh files/reproduce.sh /absolute/path/to/datasets /absolute/path/to/local_scratch

To retrieve missing exact raw versions, first run:

    python files/retrieve.py /absolute/path/to/external_datasets

The retrieval code checks all hashes and refuses changed versions. Outputs must be outside the publication. Record-level evidence stays in scratch. The wrapper regenerates main bounds, whole-bin controls, solver checks, aggregate tables and figures. Only regional aggregate files should be copied into a publication. The computation uses one numerical thread per process and at most two CPU cores. A full run takes a few minutes on this host.

`files/audit.json` checks primal constraints and dual objectives on the observed-data LPs. `files/solver_check.json` compares 40 small random cases with independent vertex enumeration and checks hull reduction. A second run reproduced all 1,742 shared target/configuration rows, including each finite oxygen lower bound exactly. `files/reproduction_check.json` records this check. These tests establish numerical consistency, not the physical assumptions. Exact external file hashes and package versions make the input and computation inspectable without any private campaign workspace.

Job sci-1107-dell-earth-and-ocean-sciences-dd78b2cd3cbf. Topic earth-and-ocean-sciences. Campaign 11_07_2026. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. The campaign-machine key is not a personal authorship claim. No agents were launched, and no remote publication or index submission was made.
