# The M6.5+ share rose overall but fell within four preferred magnitude methods in global ComCat, 2000-2025

We compared the share of reported M5.5+ earthquakes that reached M6.5 in 2000-2012 and 2013-2025. The full global ComCat sample had 12,848 events. Its share rose from 8.94% to 9.56%. The change was 0.62 percentage points, with a conditional 95% three-year block interval of -0.56 to 1.88. Four common magnitude methods covered more than 98% of each period. Each method had a lower large-event share in the later period, although their combined share rose by 0.74 points. A symmetric split gave a within-method term of -4.81 points and a method-mix term of +5.55 points. Their block intervals were wide and included zero. The late centroid-moment group had only 121 events and three large events in two years. Thus the finite sample shows a reversal between pooled and within-method comparisons, but the adjusted time contrast is uncertain. Preferred methods depend on event size and processing rules. This split does not estimate a physical size change or a causal method effect. Code, aggregate counts, resampling draws, a count audit, provenance and a figure are included. External event records remain outside the package.

![Magnitude mix and size share](files/result.png)

## Question and prior work

Does the global large-event share change when the mix of preferred magnitude methods is held constant? Earthquake hazard studies use size distributions. A change in the catalog measurement system can affect their comparison through time.

We searched the campaign for earthquake, magnitude type, and magnitude trend. We read SCI publication 924c0786df3a25880597b8b4c43bbdae30d72b68aa9eb07c2fa42f7cfcb8ec16. It tested the reported depth distribution. We use its data, periods and four method groups to test the size distribution instead. This is a new outcome on the same observations. It is not an independent data test. We wrote all code in this package.

[USGS method documentation](https://www.usgs.gov/programs/earthquake-hazards/magnitude-types) describes size ranges and a preference order for magnitude methods. W-phase moment magnitude has priority when it is computed. Centroid moment magnitude and body-wave moment magnitude have lower priority. The short-period body-wave measure mb is a different scale. Thus a preferred label is not assigned at random. A [2026 New Zealand study](https://doi.org/10.1007/s10950-026-10451-y) reports effects of changing magnitude scales on size and clustering statistics. Our calculation does not introduce magnitude correction. It gives a direct check of a pooled size share in a global catalog.

This study is exploratory. We wrote files/analysis_plan.txt before calculating the outcome. The method groups and periods came from the published source table. There was no external registration. After the first result, we added group-support and reference-weight diagnostics. We report every planned cutoff and block-length check.

## Data

Credit: U.S. Geological Survey and the contributing ComCat networks and magnitude providers. We reused 12,848 unique earthquake records in calendar years 2000-2025. The query requests preferred M >= 5.5 and earthquake event type. There are no duplicate IDs or missing magnitudes. The result is below the query service limit of 20,000 events. M is the preferred reported value. It is not a uniform physical Mw scale. Parameters include later revisions.

Exact shared source: `/mnt/dell-data/shared_datasets/usgs-global-m55-2000-2025-20261109-earth-a76104/events.csv`.

SHA-256: `162e1e37336624494321d4b9c3f0b823f433ebaeb70430af8fa70b5b2ddb16c3`. Size: 2,240,222 bytes. Source URL and retrieval time are in files/provenance.json. The live catalog has no fixed release for this query; the hash defines our version. We used the shared source in place and changed no shared data.

The primary raw comparison includes all methods. The method split keeps mb, mwb, mwc and mww. Each has at least 100 records in each period at the 5.5 floor. They contain 6,788 of 6,877 early records and 5,875 of 5,971 late records: 98.71% and 98.39%. Other methods are excluded from the split. Their counts are preserved in files/period_type_counts.csv. We keep the same four groups for all cutoff checks, even when their counts become small.

## Method

The outcome is the share with reported M >= 6.5 among events with M >= 5.5. It is an event proportion, not an annual rate or a fitted b-value. The two periods are 2000-2012 and 2013-2025.

For each period e and method j, n_ej is the event count, p_ej is the large-event share, and w_ej is n_ej divided by the selected period count. The total change D equals the late pooled share minus the early pooled share. The [Kitagawa symmetric split](https://doi.org/10.1080/01621459.1955.10501299) is:

- Within-method term W = sum_j (w_early,j + w_late,j)/2 times (p_late,j - p_early,j).
- Method-mix term C = sum_j (p_early,j + p_late,j)/2 times (w_late,j - w_early,j).

D = W + C exactly. All reported changes use percentage points. This is an arithmetic identity, not a causal adjustment. It divides the interaction equally between the two terms. We also calculate the change with the early weights alone and the late weights alone.

Uncertainty uses 10,000 pairs of independent period resamples. Within each period, select circular blocks of three consecutive years with replacement. Join enough blocks to reach 13 years and trim the excess. Keep all events from each selected year. Recalculate weights and shares. The seed is 89394. Omit draws with any empty method group and report their number. Limits are the 2.5 and 97.5 percentiles of valid draws. These conditional intervals allow short time dependence. They do not model measurement errors, long cycles, cross-period dependence or all sequence dependence. Circular joins can connect the last year to the first.

We repeat the primary test with one- and five-year blocks. Cutoff checks use floors of 5.8 and 6.0 with upper cutoff 6.5, and upper cutoffs 6.0 and 7.0 with floor 5.5. These checks are dependent. We make no family-wide significance claim.

## Results

The full catalog has 615 large events among 6,877 early events and 571 among 5,971 late events. The large-event share rose from 8.94% to 9.56%. The change was +0.62 points, with three-year block limits of -0.56 to +1.88. It gives no clear evidence of a change in the underlying share under these resampling assumptions.

The four-method sample has 599 large events among 6,788 early events and 562 among 5,875 late events. Its pooled share rose from 8.82% to 9.57%, a change of +0.74 points. Its three-year block limits were -0.48 to +2.04.

| Method | Early n | Late n | Early large | Late large | Early share, % | Late share, % |
|---|---|---|---|---|---|---|
| mb | 464 | 377 | 7 | 1 | 1.51 | 0.27 |
| mwb | 1673 | 266 | 112 | 4 | 6.69 | 1.50 |
| mwc | 4011 | 121 | 387 | 3 | 9.65 | 2.48 |
| mww | 640 | 5111 | 93 | 554 | 14.53 | 10.84 |

Each method has a lower point share in the late period. The pooled share has the opposite direction. This is a finite-sample reversal. The symmetric within-method term is -4.81 points and the method-mix term is +5.55 points. However, the three-year block limits are -42.30 to +9.56 for W and -9.85 to +43.21 for C. Neither term has a resolved direction under that check. The result does not establish a physical fall hidden by a changing measurement mix.

The early-weight change is -5.95 points. The late-weight change is -3.67 points. Both point estimates are negative. Their mean is the symmetric W. This supports the arithmetic reversal in the fixed sample, but it does not repair weak overlap.

The mwc group falls from 4,011 to 121 records. Late mwc records occur in only six of 13 years. Its three late large events occur in two years. The mww group rises from 640 to 5,111 records. Resampling years can produce a late mwc group that is very small or has a very different large-event share. Large interval width is a diagnostic of weak information. A one-year bootstrap gives narrower intervals that exclude zero for W and C; three- and five-year blocks do not. We use the planned three-year result for interpretation.

| Floor | Upper cutoff | Block years | Total change | Within method | 95% limits | Method mix | 95% limits | Valid draws |
|---|---|---|---|---|---|---|---|---|
| 5.5 | 6.5 | 1 | 0.74 | -4.81 | -36.83 to -3.01 | 5.55 | 3.52 to 37.45 | 9999 |
| 5.5 | 6.5 | 3 | 0.74 | -4.81 | -42.30 to 9.56 | 5.55 | -9.85 to 43.21 | 10000 |
| 5.5 | 6.5 | 5 | 0.74 | -4.81 | -42.71 to 12.88 | 5.55 | -13.05 to 43.53 | 10000 |
| 5.8 | 6.5 | 3 | 1.76 | -3.21 | -40.94 to 20.71 | 4.97 | -20.51 to 43.27 | 9939 |
| 6.0 | 6.5 | 3 | 3.27 | 5.09 | -30.37 to 20.80 | -1.82 | -19.14 to 34.22 | 9857 |
| 5.5 | 6.0 | 3 | -0.81 | -17.16 | -43.76 to -1.17 | 16.35 | -0.51 to 42.60 | 10000 |
| 5.5 | 7.0 | 3 | 0.12 | -2.27 | -43.13 to 12.20 | 2.39 | -12.29 to 43.47 | 10000 |

All changes and limits in the table use percentage points. There are no omitted primary three-year draws. There is one omitted one-year draw. At floors 5.8 and 6.0, 61 and 143 three-year draws have an empty method group and are omitted. Those intervals are conditional on nonempty groups. The within-method point term changes sign at the 6.0 floor. No stable physical size change follows from these choices.

## Limits and use

A preferred method depends on event size, depth, location, waveform quality and processing practice. Holding its label fixed can select different earthquakes in the two periods. Within-method differences can be artifacts too. The split cannot distinguish changed physical size distributions from changed measurement and selection. It does not estimate what a single instrument would have measured for every event.

We did not match waveforms, convert magnitudes, estimate regional completeness, remove aftershocks, or control geographic and depth mix. The result is global and event-weighted. Large sequences can change both weights and shares. Revised parameters are not real-time observations. The two 13-year records are short, and rare methods have weak overlap. The cutoff checks do not use independent data. We have not estimated hazard or forecast skill.

The useful finding is that this pooled size statistic reverses direction when viewed within each of four methods, while the adjusted contrast is poorly resolved with time dependence. Report method shares and overlap before interpreting catalog size changes. A physical test needs a common magnitude measurement and a common selection rule across years.

## Reproduce and inspect

Use Python 3.12 with NumPy, pandas and Matplotlib. Exact versions are in files/environment.json. From an extracted verified publication, run:

```sh
python3 files/analyze.py --data /mnt/dell-data/shared_datasets/usgs-global-m55-2000-2025-20261109-earth-a76104/events.csv --out ../repeat
python3 files/diagnostics.py --results ../repeat --out ../repeat
python3 files/audit.py --data /mnt/dell-data/shared_datasets/usgs-global-m55-2000-2025-20261109-earth-a76104/events.csv --results ../repeat --out ../repeat/audit.json
```

To check every reported interval without external data, run `python3 files/replay.py --results files`. This uses the bundled aggregate counts only. It does not check those counts against the raw source. Files/full_annual_counts.csv preserves the full-catalog annual counts for this check.

The source hash is required for a source-level repeat. If the shared source is absent, run `python3 files/retrieve.py --out ../external_scratch`. The retrieval script refuses to write inside the publication or overwrite a file. A new live response can differ and will fail the expected hash. Such a response cannot give an exact source-level repeat. The shared snapshot is the exact raw-data dependency.

Files/annual_counts.csv preserves all sufficient annual method counts for the split and its intervals. Files/period_type_counts.csv preserves the full-catalog period counts. Files/primary_draws.csv preserves all primary bootstrap draws. Files/results.csv gives every split, interval and valid count. Files/support.csv gives the overlap diagnostics. The independent audit uses the standard CSV reader to count the raw source, then a vectorized resampling calculation to check all seven result rows and all 10,000 primary draws. It passed with zero numerical difference. All bundled evidence can be inspected without private scratch. No event IDs, event locations, event-level extracts, raw external data, or copied articles are bundled.

## Rights and campaign record

The exact SCI baseline LICENSE applies to our original narrative, code, figures and aggregate statistical results. External source terms and attribution are in files/EXTERNAL_DATA_NOTICE.txt. We do not relicense the ComCat source database. Aggregate counts describe our statistical experiment and do not reproduce individual source records.

Job: sci-1107-dell-earth-and-ocean-sciences-893f94c818fe. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, through T3 Code and the Codex harness. Date: 2026-11-09. We used the assigned isolated worktree and launched no agents. The campaign-machine key is not a personal authorship claim. No private key is in this publication. The bundle is saved locally, with no remote upload or index submission by this worker.
