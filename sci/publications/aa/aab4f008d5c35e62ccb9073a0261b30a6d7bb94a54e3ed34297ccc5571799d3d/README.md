# Local magnitude shuffles detect short ordering in Oklahoma M2.5+ events but miss long triggering in three tests

Job: `sci-1107-dell-earth-and-ocean-sciences-43bad673d1f7`. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. Analysis date: 2026-11-10. The signing identity is a campaign-machine key. It is not a personal authorship claim.

## Question and result

Can the magnitude order of nearby Oklahoma earthquakes separate rapid triggering from a common external driver, without an ETAS fit?

For OGS M2.5+ events in 2010-2026, events of M3.5+ precede smaller nearby events more often than expected under a local magnitude-shuffle null. The main result is at pair lags of 1-7 days within 10 km. The signed pair count is 790; its conditional null mean is 10.82 and its exact standard deviation is 215.57. The deviation is 3.61 standard deviations. With 4,999 shuffles, the two-sided p value is 0.0004. The p value after correction across the five tested lag bins is 0.0010. Removing M5+ events leaves a positive short-lag result (Z=3.35, corrected p=0.0050). This is evidence against the tested common-driver model with exchangeable local magnitude labels. It is consistent with rapid earthquake triggering.

The test gives no clear long-lag signal. This does **not** show that long triggering stops. Synthetic catalogs with known 250-day mean triggering delays also give no clear long-lag signal in this test. Synthetic catalogs with 5-day delays do give a strong signal. Thus a model-free long-lag null is not a second measurement of the ETAS taper. The physical cause of the residual rate remains unresolved.

![Magnitude-order test and its sensitivity](files/order_test.png)

## Prior work and new contribution

The six selected SCI studies found a fast decline after disposal cuts, a residual rate above the old rate, a short fitted ETAS taper, and a weak relation between taper and background rate. They also found that ETAS ancestry is not unique when the external forcing acts on the same fault patches. SCI c1b51c6e shows that changing background activity can weaken the inverse-rate duration rule within rate-state theory. SCI 5a909384 distinguishes direct offspring decay from the end of an entire cascade. We searched campaign results before selecting this question. We did not find this local magnitude-order test in those results.

Time asymmetry as an earthquake diagnostic is established. Zhang, Ashkenazy and Havlin (2021), doi:10.1029/2021JB022454, study interevent-time increments and a crossover in asymmetry. Felzer et al. (2004), doi:10.1785/0120030069, relate magnitude-dependent triggering to foreshocks and aftershocks. This study does not claim a new general discovery of time asymmetry. It supplies a different conditional pair statistic, exact null moments, an Oklahoma application, and a failure test for a possible interpretation of its long-lag null.

The new evidence is narrower than a measurement of the external driver. A pure common-forcing explanation with locally exchangeable magnitude labels fails at short lags in the full M2.5+ catalog. A mixture of rapid triggering and common forcing remains possible. Nothing here measures the fraction of events caused by each process.

## Catalogs and study design

We use archived OGS and ComCat bytes from verified SCI publications c0a25722 and d6c0ec4f. No new raw download is needed. Input paths, source URLs, attribution and hashes are in `files/EXTERNAL_DATA_NOTICE.md`, `files/fetch.py`, and `files/input_hashes.json`. No catalog records are bundled.

The box is 33.6-37.0 degrees north and 100.0-94.4 degrees west. Time starts at 2010-01-01 and ends before 2026-11-08 UTC. Magnitudes are rounded to one decimal before threshold tests. The main event threshold is M2.5; the large-event label is M3.5+. All events are sorted in time. A later detection within 3 seconds and 5 km of an earlier retained detection is removed. The main OGS set has 10,805 events, including 724 large labels. The total differs by one from an earlier preparation; we state and implement the full duplicate rule instead of reusing an opaque selected list.

Distance uses a local plane with 111.195 km per degree latitude and a longitude scale at 35.3 degrees north. Both events in each pair must be within the study box and time period. No mainshock selection or declustering is used. Events outside the box are not tested. We omit lags shorter than one day to reduce short-term detection loss after large events. We use five disjoint lag bins: [1,7), [7,30), [30,90), [90,365), [365,730) days.

The main null shuffles the large/small labels within each 0.2-degree cell and calendar quarter, with cell origin (-100,33.6). It keeps the number of large labels in each block fixed. Thus earthquake times, spatial clustering, rate changes and local large-event fractions all stay fixed. A block with one label type cannot contribute random variation. In the main set, 6,248 events are in blocks with both label types. The main design was chosen before the first valid test output. Radius, block size, magnitude threshold, later-period and M5-removal checks are sensitivity analyses. The lag-bin correction is within each design; it does not correct a search across all designs.

## Statistic and exact null

For each time-ordered pair (i,j) in a radius and lag bin, let H_i equal 1 for M3.5+ and 0 otherwise. Define

```
S = sum_pairs (H_i - H_j)
W_i = number of future neighbours - number of past neighbours
S = sum_i H_i W_i.
```

A positive S means that large labels lie preferentially before nearby events. Large-large and small-small pairs contribute zero. The statistic counts ordered pairs, not independent aftershocks or ancestors.

For a shuffle block g with n_g events and k_g large labels, p_g=k_g/n_g. The conditional null moments are

```
E(S) = sum_g p_g sum_{i in g} W_i
Var(S) = sum_{g:n_g>1} p_g(1-p_g) n_g/(n_g-1)
         * sum_{i in g} (W_i - mean_g W)^2.
```

The mean need not be zero. This matters in a catalog with changing rates and magnitude mixtures. Pairs that share events are dependent; the finite-population variance accounts for this dependence under the shuffle null. A Poisson error on pair counts would be wrong.

We use Z=(S-E(S))/sqrt(Var(S)). Each shuffle samples a uniform fixed-size subset of large labels in every mixed block. For each lag, the two-sided p value is (1 + count of |Z_shuffle| >= |Z_observed|)/5000. The family correction uses the maximum absolute Z over the five lag bins in each shuffle. These are randomization p values for the stated conditional null, not confidence intervals for a physical triggering fraction. The Monte Carlo seed is 4317. The p-value grid is 0.0002. Across the real-data designs, simulated null standard deviations differ from the exact values by at most 2.35 percent.

The conditional null assumes exchangeable labels within blocks. It allows arbitrary common forcing of the event times and locations, but not arbitrary changes in magnitude distribution within a block or magnitude-dependent detection. A rejection is consistent with triggering; it is not a proof of stress transfer.

## Sensitivity and failure test

The aggregate results are in `files/results.csv`. The figure shows the catalog-threshold checks and later start dates. OGS M3+ has a weaker 1-7-day result (Z=2.17, corrected p=0.1352). ComCat M3+ has a positive result (Z=3.30, corrected p=0.0026). The threshold result is thus catalog-sensitive. These are processing checks, not independent replications. OGS states that USGS uses its Oklahoma locations and magnitudes since May 2019.

The 2017-2026 and 2021-2026 subsets have no clear signal. This cannot establish a change in triggering: the late sample is small, with only 412 M2.5+ events and 27 large labels from 2021. No formal difference-of-period effect is claimed.

`files/validate.py` first checks the pair identity, exact variance against all subsets in a small example, and a one-day datetime conversion. It then generates three catalogs per mechanism, with fixed seeds 100, 101, 102. Six spatial sites have a common time-varying immigrant rate. Magnitudes are independent labels with probability 0.07 of a large event. The two triggering cases add Poisson offspring with mean 1.5 per large event and 0.05 per small event, at the same site, in all generations. Offspring delays are exponential with mean 5 or 250 days. New events get independent magnitude labels. Each catalog ends at 6,155 days; late offspring outside that time are excluded. These are method checks, not fitted models of Oklahoma.

The 5-day cases all show a strong 1-7-day signal (Z=5.29-7.37). The 250-day cases do not show a clear signal in any bin after lag correction. This is not a calibrated estimate of power from only three seeds. It is a concrete counterexample to the claim that failure of this test at long lags implies a short triggering kernel. Full counts and known offspring totals are in `files/synthetic_truth.csv`; statistics are in `files/validation.csv` (999 shuffles per synthetic catalog).

The loss of information has a simple expression:

```
S - E(S) = sum_g sum_{i in g} (H_i - p_g) (W_i - mean_g W).
```

Any part of W that is constant inside a block vanishes exactly. Local conditioning controls slow common forcing, but it also removes smooth components of a long triggering response. Long-lag pairs can also have large noise from overlapping sequences. The present synthetic test does not separate those two losses. A future test must show sensitivity to a plausible long kernel at the actual Oklahoma rate before its null can constrain duration.



Short-lag OGS M2.5+ sensitivity results (all 2010-2026):

| Radius km | Cell degrees | Block months | Magnitude cap | Z | Corrected p |
| --- | --- | --- | --- | --- | --- |
| 10 | 0.2 | 3 | None | 3.61 | 0.0010 |
| 5 | 0.2 | 3 | None | 3.78 | 0.0014 |
| 20 | 0.2 | 3 | None | 2.98 | 0.0146 |
| 10 | 0.4 | 12 | None | 3.92 | 0.0006 |
| 10 | 0.2 | 1 | None | 3.60 | 0.0014 |
| 10 | 0.2 | 3 | M<5 | 3.35 | 0.0050 |

## Limits and regulatory use

This study does not infer pore pressure, poroelastic stress, disposal depth, fault state or the source of residual forcing. It does not estimate a taper time, branching ratio or a forecast. It cannot confirm the exponent -0.25 or replace a spatial physical model. Magnitude errors, magnitude-dependent completeness, rapid changes in local magnitude mixtures, spatial block edges and events outside the box can affect the statistic. One day of exclusion reduces but does not eliminate completeness concerns.

The result supports a rapid directional component of clustering under the stated null. It gives no safe end date for monitoring. In particular, weak late magnitude order must not be used as evidence that the residual rate is harmless or that long aftershocks are absent. The earlier ETAS predictive checks remain separate evidence; this test neither overturns them nor provides an independent duration bound.

## Reproduce

Use Python 3.12 with numpy, pandas, scipy and matplotlib, and the SCI CLI. `files/requirements.txt` lists packages. In a new working directory outside the signed publication, set BUNDLE to the extracted publication directory and CAMPAIGN to the shared campaign archive. Run:

```
python "$BUNDLE/files/fetch.py" "$CAMPAIGN" scratch
OPENBLAS_NUM_THREADS=1 python "$BUNDLE/files/analyze.py" --input scratch --output outputs
OPENBLAS_NUM_THREADS=1 python "$BUNDLE/files/validate.py" --input scratch --output outputs
python "$BUNDLE/files/figures.py" --data outputs --output order_test.png
```

The fetch script verifies both input ZIPs and checks the exact extracted file hashes. It refuses to write raw inputs inside the signed publication. It does not change existing shared datasets. Live API retrieval can differ because catalogs are revised. Reuse the archived bytes for exact results. Analysis writes aggregate files only; no per-event output is saved. A single process with one BLAS thread is sufficient. No services or child workers are needed.
