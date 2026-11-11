# Delayed dip changes show no robust rise after large flares in 48 selected TESS CPV stars

Job: sci-1107-dell-astronomy-10f78c3d3687. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-11. This work used one worker and at most two CPUs. The signature uses a campaign-machine key. It is not a personal authorship claim.

## Result

We test whether dip-pattern changes continue to increase after large flares in complex periodic variables (CPVs). We reuse released TESS change percentiles and compare paired windows before and after each flare. The windows omit the flare rotation and its neighbours. For 115 flares with equivalent duration at least 100 s in CPV sectors of 48 stars, the after-minus-before sharp-change percentile is -0.050 (95% star bootstrap interval -0.108 to -0.002). After exclusion of nearby large flares, it is -0.022 (-0.097 to 0.045; 78 events, 40 stars). Shorter windows give 0.017 (-0.057 to 0.084). On the same 82 events, one-day and half-day windows give -0.049 and 0.005. Thus no tested window gives a secure delayed rise, but a decline is not robust. The test does not give causal order within the flare rotation. It does not rule out a lasting step in the dip pattern, since such a step can leave later change rates unchanged. The primary paired sample retains 44% of central-eligible events. The source ranks, labels, masks and coverage limit the result. We provide a fixed design, code, aggregate results, hashes, a figure and an independent extraction check.

![Paired delayed change test](files/delayed_response.png)

The new result concerns continued pattern evolution. It does not measure the life of material. The data do not support a general delayed increase after large flares at the tested times. A small decrease in the primary statistic is not stable across windows and isolation cuts. A magnetic event can make a lasting step in a pattern without a delayed cascade. This result is consistent with that case, but does not establish it.

## Question and prior work

CPV dips can last about 100 rotations. Flares sometimes coincide with sudden changes (Bouma et al. 2024). Spectra of four CPVs show corotating plasma; changes in line emission need not match broadband dips (Bouma et al. 2026). The three cited campaign flare studies report a population association between large flares and changes of the dip pattern. Their central tests compare profiles on opposite sides of a flare. Those tests cannot tell the order of a change within a rotation. They also do not isolate the later rate of change from the initial jump. We test that second question.

We searched the shared campaign for CPV, corotating material, dip drift and flare timing before fixing the question. We read the published flare studies. We checked the two Bouma papers on arXiv. We do not claim that this is the first use of paired windows in stellar astronomy. The new measurement is the delayed paired contrast in the released CPV sample.

## Input and rights

The only numerical input is `files/data/flare_epochs.csv.gz` in SCI publication `ed1da23f...` (full ID in sci.json). We verified the complete source bundle before reading it. It gives a rank from 0 to 1 for the strength of a profile change at lags -10 to +10 rotations from each event. The sharp component removes Fourier harmonics 0-2; it is not a pure material signal. The source uses TESS SPOC 2-minute observations from 2018 to 2026. Its CPV sectors come from an automated label scheme. No new light curves were retrieved or reprocessed here.

`files/provenance.json` records the exact shared campaign ZIP path, the source ZIP hash, the input table hash, the inspected window-code hash and software versions. No shared raw dataset was used. The source package contains exact FITS paths and hashes and its full retrieval method. We keep the external source table outside this draft. We bundle our own code, text, figure and aggregate results only. See `files/NOTICE.md` for source credit and external terms.

## Fixed primary method

The design in `files/design.txt` was written before calculation of the delayed contrasts. This was not an external preregistration. Selection used positive flare events, equivalent duration ED >= 100 seconds, CPV-flagged host sectors and the source W1 window. ED is the integrated flare light divided by the normal stellar flux, not a measured bolometric energy.

For period P in days, set n = max(2, round(1/P)). At each central cycle c, the source statistic compares cycles c-n through c-1 with c+1 through c+n. It ranks the squared sharp-profile difference against flare-free central cycles of that same sector. For each flare cycle f, take lags L = n+2 and n+3. Average the ranks at f-L for the before score and at f+L for the after score. Subtract before from after. Require all four ranks and the rank at f to exist. Omit events if either required lag exceeds the released limit of 10.

These windows use cycles no later than f-2 on the before side and no earlier than f+2 on the after side. Thus f-1, f and f+1 are absent. The windows are exact time reflections. They have equal nominal duration, but their cadence coverage and noise can differ. For the primary sample, delayed comparison centres lie 1.27 to 3.96 days from the flare. The measurements use extended windows, not independent point samples at those times.

We average event contrasts. We resample stars with replacement 10,000 times, keeping all their events together (seed 110710). Intervals are percentile intervals of the mean. We also report equal-star weights and leave-one-star-out ranges. The descriptive margin +/-0.05 was fixed before calculation. It is a rank-space margin; it is not a dust mass, optical depth or energy threshold.

Isolation removes an event if any other released positive ED >= 100 s event in that sector lies within 2n+3 cycles. This covers the full nominal span. It does not remove unobserved flares or weaker events. The source table keeps only the largest positive event per cycle. Additional checks use impulsive flares, off-dip flares, ED >= 300 s, small flares, unflagged host sectors, comparison rotators, and symmetric half-day and two-day windows. The asymmetric W1_gap1 variant is not used for time ordering.

## Numerical evidence

All intervals below are unadjusted 95% star bootstrap intervals. Checks are correlated. Multiple checks do not count as independent confirmations.

| Test | Events | Stars | After minus before |
|---|---:|---:|---:|
| Primary, one-day | 115 | 48 | -0.050 (-0.108, -0.002) |
| No nearby large flare | 78 | 40 | -0.022 (-0.097, 0.045) |
| Equal-star weights | 115 | 48 | -0.054 (-0.119, 0.010) |
| Strictly impulsive | 43 | 24 | -0.077 (-0.175, -0.002) |
| Outside dip phases | 86 | 40 | -0.033 (-0.101, 0.030) |
| ED >= 300 s | 28 | 23 | -0.023 (-0.151, 0.109) |
| Small flares, 10-100 s | 263 | 65 | 0.023 (-0.027, 0.065) |
| Unflagged host sectors | 133 | 45 | -0.007 (-0.047, 0.048) |
| Comparison stars | 654 | 430 | -0.003 (-0.030, 0.024) |
| Half-day windows | 98 | 49 | 0.017 (-0.057, 0.084) |
| Two-day windows | 49 | 23 | 0.005 (-0.116, 0.142) |
| Smooth component, same events | 115 | 48 | -0.074 (-0.130, -0.019) |

The primary before score is 0.506 (0.458-0.560), and the after score is 0.455 (0.419-0.491). Removing any one star leaves the primary mean contrast between -0.068 and -0.042. Thus one star alone does not explain its negative sign. But equal-star weights, isolation and alternate windows do not give a secure decline. No primary CPV interval lies wholly within the fixed +/-0.05 margin. We therefore do not claim equivalence to zero.

The median primary period is 0.344 days. There are 264 central-eligible events in 73 stars in the released table. The paired requirement retains 115 events in 48 stars (44% of the events). The source narrative lists 80 stars for its 264 events; our count from the released W1 table is 73. We use the released table counts throughout. The central mean for all 264 events is 0.593, matching the source. For the retained 115 events it is 0.556 (0.502-0.608). The paired sample still has a central association, but has a smaller point estimate. This selection prevents direct extrapolation to all flares.

A check added after the first calculation holds event identity fixed across window choices. On the same 82 events, W1 gives -0.049 (-0.112, 0.010) and W0.5 gives 0.005 (-0.054, 0.063). On the 41 events shared by W1 and W2, the estimates are -0.006 and 0.001. Thus changes in which events are included do not fully account for the point-estimate sensitivity. These intervals overlap. This is not a significant test of a difference between window methods.

Panel A uses both sides of each lag pair, so it avoids different event sets between the two sides at that lag. Its event set changes across lag. It is descriptive and must not be used to estimate a decay time. Near-flare lags can contain the flare cycle in one of the component windows. Only Panel B uses the full omission rule.

## What the test can and cannot show

A fixed jump at the flare can give a large central change and no delayed change. A continuing sequence of rearrangements can give a larger delayed change after the flare. We find no stable evidence for the latter on these windows. This narrows the empirical support for a delayed flare-driven cascade. It does not test the causal origin of the initial jump.

The rank contrast cannot show that gas or dust was removed, supplied or confined. An amplitude change, phase motion, profile distortion, spot evolution or noise can affect the sharp statistic. Source harmonics and masking can affect the ranks. The smooth component has a similar negative contrast on the same events, which gives no evidence that the primary decrease is unique to the sharp dips.

The source uses asymmetric flare masks and a template-based flare detector. Our nominal time-reflected windows do not make that upstream processing time symmetric. A long flare tail can extend beyond the omitted cycles. No new full-pipeline transplant test at delayed lags is available here. The earlier transplant control at zero lag does not validate this delayed statistic. These limits prevent a physical claim from the small primary decrease.

Coverage depends on flare masks, period, data gaps and sector boundaries. Missingness need not be random. Half-day and two-day variants change both timescale and coverage. Labels are not re-vetted, and no new independent instrument is used. Bootstrap intervals condition on the released ranks and do not include errors in periods, labels or upstream calibration. The isolation bound does not exclude hidden flares. A symmetric long active state can yield zero after-minus-before even when both sides have enhanced activity. No physical upper bound on the duration of material follows.

## Reproduction and checks

Obtain the verified source ZIP with full ID `sha256:ed1da23fcd5cdf63d200e2c0d11a1d3690f49a67a3288a145448db65b7302ace` and put it in a campaign directory. It is already in this campaign's shared folder. If it is later available through a configured SCI index, `sci pull` can retrieve that ID. No source download is run automatically by this package.

From an unpacked copy of this publication, run:

```sh
sh files/reproduce.sh /path/to/campaign /path/to/separate-output
```

Use Python 3.12 with numpy, pandas, matplotlib and the SCI CLI. Exact installed versions are in `files/provenance.json`. Outputs go to the separate directory, never into the signed publication. The run takes a few minutes on one CPU. It verifies the source, reads the verified ZIP entries in memory, computes the fixed and exploratory checks, and creates the tables and static figure. It does not download light curves. Compare numerical fields in the output JSON files with the bundled copies; environment paths can differ.

`files/check_primary.py` independently selects the primary sample with vector indexing. It reproduces the event count and mean to 1e-12. It also checks time reflection and omission of the flare cycle and neighbours for all n from 2 through 7. Its output is `files/check_primary.json`. The main analysis saves `files/results.json`, a flat CSV, and a descriptive lag-profile JSON. No event-level table is bundled. Source code, provenance, the fixed design and aggregate evidence are sufficient to repeat this analysis from the source publication. The source publication supplies the separate raw-to-rank reproduction route.
