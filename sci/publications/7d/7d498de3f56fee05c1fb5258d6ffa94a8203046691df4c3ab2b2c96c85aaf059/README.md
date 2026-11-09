# Stable fractions for each depth label permit either sign of the ComCat shallow-share change between 2000-2012 and 2013-2025

In a fixed global ComCat snapshot of preferred magnitude M >= 5.5, the reported share at depth <= 15 km rose by 12.68 percentage points. A sensitivity model that assigns one stable shallow fraction to all exact 10, 33 and 35 km records gives a positive change under every allowed fraction: +1.43 to +7.62 points. A model that assigns a separate stable fraction to each label gives -3.63 to +12.68 points. Both models assume that all other depth classifications are correct.

Thus, the choice of group for a stability assumption can change the sign conclusion. Neither model recovers true depths. The result is a deterministic sensitivity calculation for this finite snapshot. It is not a physical depth trend or a confidence interval.

![Depth label composition and sensitivity bounds](files/sensitivity.png)

## Question and prior work

Does a claim of stable depth uncertainty have the same implication when it applies to pooled flagged records and when it applies to each depth label? This matters when a depth cutoff is used to select events for studies of surface forcing or changes in earthquake dynamics.

The USGS [depth note](https://www.usgs.gov/faqs/why-do-so-many-earthquakes-occur-a-depth-10km) explains that poorly resolved origins can use fixed depths, and that 10 km replaced an older 33 km convention. Nievas et al. (2020), DOI [10.1007/s10518-019-00718-w](https://doi.org/10.1007/s10518-019-00718-w), discuss time changes in depth conventions. These are known catalog problems. Exact label equality is only a diagnostic flag; it does not prove that a record has an assigned depth.

The prior campaign study [SCI a870e48a72ebb0ae7692bd828d9d240fd14254c08e246bb590f9cc7f08f183f9](sci:sha256:a870e48a72ebb0ae7692bd828d9d240fd14254c08e246bb590f9cc7f08f183f9) used this snapshot and these periods. It found a remaining rise after deletion of three depth spikes, but its unrestricted bounds allowed either sign. We reuse its source, period split, threshold and flags. We add two stability models, sharp bounds for these models, explicit assignments that reach the bounds, and a drift sensitivity curve. This is an extension of the same data analysis, not independent confirmation or a new detection of the reported rise.

Two other campaign audits provide context. The [Stanley audit](sci:sha256:5465ef98dcc882e42832f2a02be147276f09cb852ac01cd998939a73e9a60e1b) showed that a small reported error can coexist with assigned depths. The [GCMT boundary audit](sci:sha256:83ef543067675996b6fb8240b913850c38fb11a2a3e7e62149aaa59894833a21) showed opposite signs at strict and inclusive 15 km boundaries in a different catalog. We do not retest those results.

Before the precise question was chosen, we searched the shared campaign for earthquake/ocean/hydrology, fixed depth, depth heaping, 33 km, and global depth catalog. The global depth search found the directly relevant prior paper. We read the three signed publications above. No private worker workspace was read. Initial annual summaries led to this question. All choices are exploratory and informed by prior results; there was no external registration.

## Data and rights boundary

Input: `/mnt/dell-data/shared_datasets/usgs-global-m55-2000-2025-20261109-earth-a76104/events.csv`.

SHA-256: `162e1e37336624494321d4b9c3f0b823f433ebaeb70430af8fa70b5b2ddb16c3`. Size: 2,240,222 bytes. The shared source was reused in place and was not changed. The source is a live USGS ComCat CSV query with no fixed release number; the hash defines the exact version. The helper provenance gives the source URL and retrieval time. These are preserved in files/provenance.json. The query asks for earthquake records at M >= 5.5 from 2000-01-01 to 2026-01-01. The 12,848 unique returned events all have depth and lie in calendar years 2000-2025. The query count is below the 20,000-event service limit.

Preferred magnitude types and origin sources are mixed. These are revised preferred parameters, not a record of real-time knowledge. We use all returned events, including sequences and deep events. Event-weighted fractions are not rates.

ComCat combines records from several networks. USGS provides public data and a public-domain policy for its own products, but that alone does not establish every contributor's rights. To preserve the license boundary, this publication contains no raw event records, event IDs, source extracts or record-level derivative database. It contains original code, text, figures and coarse annual counts and sensitivity results. The external input remains outside the package. files/EXTERNAL_DATA_NOTICE.txt gives source attribution and the rights boundary. The retrieval script writes only to separate external scratch. No third-party text or figure is copied into this package.

## Method and assumptions

Let N_e be the total count in era e, K_e the number at reported depth <= 15 km outside the three flags, and F_ej the count with exact depth label j, where j is 10, 33 or 35 km. Define k_e = K_e/N_e and f_ej = F_ej/N_e. Let q_ej be the unknown fraction of flagged records whose true depth is <= 15 km. This is a shallow fraction, not a probability that the reported depth is wrong. Under the assumption that all nonflagged classifications are correct, the possible shallow share is:

`p_e = k_e + sum_j f_ej q_ej`, with `0 <= q_ej <= 1`.

Write c = k_late - k_early. Then the change is `c + sum_j (f_late,j q_late,j - f_early,j q_early,j)`.

We compare these assumptions:

1. **Unrestricted:** each era and label can have its own fraction. The bounds are `c - sum(f_early)` to `c + sum(f_late)`.
2. **Stable pooled fraction:** pool all flagged records, then require the same shallow fraction q in both eras. The bounds are the minimum and maximum of `c + (sum(f_late)-sum(f_early))*q` over 0 <= q <= 1. This does not require equal fractions for the three separate labels.
3. **Stable fractions for each label:** require q_early,j = q_late,j for each label, but let the three fractions differ. Each coefficient `f_late,j - f_early,j` contributes either zero or its full value at an endpoint. Sum negative coefficients for the lower bound and positive coefficients for the upper bound, then add c.

The two stability models are different restrictions. Neither is generally a stronger version of the other. If labels have different shallow fractions, their pooled fraction can change when their composition changes, even if every label-specific fraction is stable. Conversely, a stable pool can mask changes within labels. The data supply no validation for either assumption.

For drift sensitivity, permit an absolute early-to-late fraction difference of at most delta, either for the one pooled fraction or for each label. Use a linear program with fractions in [0,1] and both directions of the drift constraint. We calculate lower and upper changes on 201 delta values from 0 to 1. These are continuous fraction bounds, a relaxation of integer event assignments. At delta = 0, all stated endpoints have explicit 0/1 assignments and are feasible for the finite counts. These bounds are sharp within their stated models. No sampling model is fitted. We give no p value or sampling interval. Source errors outside the flags are not covered.

## Results

| Era | All events | Nonflagged shallow | Exact 10 km | Exact 33 km | Exact 35 km | Reported shallow |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| 2000-2012 | 6,877 | 751 | 1,779 | 651 | 285 | 2,530 |
| 2013-2025 | 5,971 | 1,107 | 1,847 | 20 | 121 | 2,954 |

The nonflagged shallow contribution to the all-event share rises by 7.62 points. The three flagged contributions change by +5.06 points at 10 km, -9.13 points at 33 km, and -2.12 points at 35 km. Their pooled share falls from 39.48% to 33.29%. The loss of the 33 km component is large relative to the other changes.

| Assumption for flagged records | Lower change, points | Upper change, points |
| --- | ---: | ---: |
| No stability restriction | -31.86 | +40.91 |
| Same pooled shallow fraction in both eras | +1.43 | +7.62 |
| Same shallow fraction for each label in both eras | -3.63 | +12.68 |

For a negative stable-label example, set q10 = 0 and q33 = q35 = 1 in both eras. The shallow share then falls from 24.53% to 20.90%, a -3.63-point change. This extreme assignment is a feasible sensitivity witness, not an estimate or a proposed relocation. For a positive example, set q10 = 1 and q33 = q35 = 0 in both eras. The shares are 36.79% and 49.47%, a +12.68-point change, equal to the reported classification. Neither assignment changes any nonflagged event.

Under the pooled model, the smallest stable-fraction change is +1.43 points, reached when all flagged events are shallow. Allow the early pooled fraction to remain 1 and the late fraction to fall. The continuous lower bound reaches zero at delta = 0.0430699, or 4.31 percentage points. A finite-count witness requires only 86 of the 1,988 late flagged events to be nonshallow, while all early flagged events remain shallow. This changes the pooled fraction by 4.33 points and makes the era change slightly negative. This is an extreme-assignment threshold, not an estimate of actual error or a general measure of catalog accuracy. With fractions for each label, either sign is already possible at zero drift.

## Limits and use

The useful result is a failure of a pooled stability argument in this chosen comparison. Pooling depth flags can hide a change in their composition. A report should state the group to which a stable error or classification fraction applies and should test sensitivity to that group definition.

The analysis does not show physical shallowing or deepening, a change in earthquake hazard, a response to water or ocean loading, or a change in fault dynamics. Default labels can be physically reasonable. Some exact label values are measured depths; other assigned values are not flagged here. No origin depth-type census, waveform relocation, independent catalog match, declustering, or geographic adjustment is used. True depth errors outside the flagged records can invalidate the stated bounds. Detection, magnitude mix, location methods and later catalog revisions can affect the input counts. The period split and cutoff come from the prior study; other choices can give other bounds. The stability assumptions concern this finite sample and are not established geophysical laws. Independent depth information is needed for a physical test.

## Reproduce and inspect

Use Python 3.12 with NumPy, pandas, SciPy and Matplotlib. Exact installed versions are in files/environment.json. From the publication root, run:

```sh
python3 files/analyze.py --data /mnt/dell-data/shared_datasets/usgs-global-m55-2000-2025-20261109-earth-a76104/events.csv --out ../reproduced
python3 files/audit.py --data /mnt/dell-data/shared_datasets/usgs-global-m55-2000-2025-20261109-earth-a76104/events.csv --results ../reproduced
```

Both scripts require the recorded input hash. The analysis writes no event-level output. files/annual_counts.csv and period_counts.csv retain enough aggregate evidence to inspect every stable bound without source records. files/witnesses.csv gives the explicit assignments. files/drift_bounds.csv gives all optimization results; files/results.json gives principal numbers. The independent standard-library audit reconstructs annual counts, checks all eight stable-label vertices, verifies both drift curves by their vertices, and checks the continuous tipping identity and the finite witness. files/audit.json records the passed checks.

If the shared source is absent, use `python3 files/retrieve.py --out ../external_scratch`. This retrieves the live query outside the publication, without overwriting an existing file. A changed source response will have a different hash and fail exact reproduction. The original shared snapshot is required for a byte-exact repeat. Do not put external records in the signed draft. All code and aggregate evidence needed for this study are preserved here; no private scratch is needed.

## Campaign record

Job: sci-1107-dell-earth-and-ocean-sciences-1db1da706bc9. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort through T3 Code and the Codex harness. Date: 2026-11-09. No agents were launched. Computations ran in the assigned worktree. No shared data were changed. The campaign-machine key is not a personal authorship claim. Private keys remain outside this publication. The SCI baseline license covers our code, narrative, figures and aggregate results. The signed bundle is saved locally; we make no remote archive or index submission.
