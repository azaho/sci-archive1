# The ASASSN-14ko flare-fluence link to the timing stall depends on the assumed time order

Job sci-1107-dell-astronomy-543c39c5c6f2. Topic astronomy. Campaign 11_07_2026. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort, Codex harness in T3 Code. Analysis date 2026-11-11. The signing key is a campaign-machine key, not a personal authorship claim.

## Result

The ASASSN-14ko flare fluence differs between the published stall and decay groups. This result survives a joint test of four optical properties if flare rows can be freely exchanged. It is not secure under the tested assumptions that keep adjacent flares together. Thus the flare data support a change in the emission process. These data alone do not establish a physical link between that change and orbital evolution.

We use all 16 good ASAS-SN g flares in SCI 90a362d7, with no new quality cut. For the fixed published stall window, cycles 21 through 29, six flares are in the stall and ten are outside it. We enumerate all 8,008 assignments of six labels to 16 rows. Each row retains its four measured properties. The fluence test gives two-sided p = 0.000999 and a four-property adjusted tail fraction of 0.003871. Removing each flare in turn gives a joint tail fraction from 0.00160 to 0.01032. No single flare causes the result.

The claim is weaker when the null model retains time structure. Permutations of adjacent pairs give a joint tail fraction of 0.05357. Permutations of four-flare blocks give 0.08333. Cyclic shifts of the full sequence give 0.1875. These are different conditional null models, not confidence bounds on one p-value. None is established as the true stochastic model for this source.

![Exact tests and time-order sensitivity](files/result.png)

Figure 1. Left: two-sided rank-test tail fractions, a joint correction for four properties, and a cyclic-order sensitivity test for the fixed published stall window. Right: signed standardized rank contrasts at all 16 cyclic phases. Shift zero is the observed alignment. Cyclic shifts keep observed-flare order, not regular spacing in orbital cycle. They are a sensitivity test, not a general stationary-time-series test.

## Question and prior work

SCI 90a362d7 reported larger fluence and longer declines in the timing stall. It used independent Gaussian parametric bootstrap draws, tested nine series, and did not correct for multiple tests. Its separate test without the unusual 2022 flares gave p = 0.028 for both decline and fluence. The physical interpretation was that the stall and flare process probably share a cause. We test whether that conclusion survives a joint optical test and assumptions that retain some of the observed time order.

SCI 967e3773 added Einstein Probe cycle 34. Its X-ray dip follows the constant event clock, while the optical marker is early. Thus its new data challenge the assumed restart near cycle 30 that defines the earlier stall box. We also test a no-restart grouping. We do not repeat its photometry or treat its conclusion as an independent orbital-period measurement.

Linial and Quataert (2024) discuss drag, stripping, and period evolution (arXiv:2309.15849v2). Their physical coupling makes a reliable emission-clock association useful, but a group difference cannot select a drag model. Yuan and Shou (2024, doi:10.1371/journal.pbio.3002758) show why time-series dependence tests need explicit assumptions about time structure. Their truncated time-shift test is not used here; the short, irregular flare series does not support a direct application of that method. Our cyclic test requires the stronger, explicit null of a uniformly random cyclic phase.

A campaign search for ASASSN-14ko returned 42 publications before the test was chosen. The source study and the new Einstein Probe result motivated this reanalysis. This is not a blind replication or a claim of literature-wide priority. The new contribution is exact joint calibration for the four optical properties, coupled with a quantified sensitivity to temporal grouping and to the disputed restart.

## Input and method

The sole numerical input is `files/results/series.csv` from the verified SCI 90a362d7 ZIP. It contains natural-log per-flare fit values. We use `g_rise`, `g_decl`, `g_flu`, and `g_amp`, joined by cycle. They are measured in the same 16 flares, so joint permutations retain their observed dependence. UV and X-ray series have different coverage and are not included in this four-property family. This correction does not account for all nine source series or all source analyses.

The source fit errors are not used in the rank statistic. We test the supplied fit estimates as observations, not latent error-free flare properties. This avoids an assumption of Gaussian fit errors but does not remove uncertainty or bias in poorly sampled flare fits. Rise widths include source-imposed small-value limits. Fluence, rise, decline and amplitude come from related fit parameters. They are not four independent confirmations.

For property j, rank the N observed log values, with average ranks for ties. For group size K, the statistic is

    Z_j = [sum_in(rank_j) - K mean(rank_j)] / sd_j
    sd_j^2 = K(N-K) / [N(N-1)] * sum_i [rank_ij - mean(rank_j)]^2.

The two-sided property p is the fraction of assignments with |Z_j| at least as large as observed. The adjusted tail fraction uses max_j |Z_j| in each assignment and compares it with each observed |Z_j|. The global test compares with the largest observed |Z_j|. All assignments include the observed assignment, and ties count in the tail. There is no Monte Carlo error. This is an exact global-null randomization test under row exchangeability. Strong control for arbitrary mixtures of true and false individual nulls is not claimed.

The same contrast is used for all dependence sensitivities. Pair and four-row blocks are formed from the chronological sequence starting with the first observed flare. We enumerate all 8! and 4! block permutations. Internal block order is fixed. Cyclic shifts enumerate all N phases of the group labels against the unchanged joint property rows. Exactness here requires exchangeable blocks or a uniform cyclic phase, respectively. Neither stationarity alone nor independence of the clock and flares guarantees these conditions. Circular closure joins the end and start of the observation span. Missing cycles mean that adjacent observed rows need not be adjacent orbits. No claim that these transformations preserve physical orbital-lag autocorrelation is made.

The boundaries 21 and 30 are held fixed at the source clock modes. We do not search for the strongest box in the flare series. Timing-marker errors and boundary uncertainty are not propagated. The boundaries were inferred in earlier work partly from optical data, so they are not fully independent of emission changes. We also do not claim that every boundary was specified before any flare property was inspected.

## Results

Table 1. Full-sample fixed-box test. Ratios are unweighted geometric-mean ratios of the source log estimates, not the source study's weighted effect estimates or median ratios.

| Property | Stall/outside ratio | Two-sided p | Four-property adjusted tail fraction |
|---|---:|---:|---:|
| Rise width | 2.391 | 0.09341 | 0.27760 |
| Decline time | 1.932 | 0.01598 | 0.05619 |
| Fluence | 2.023 | 0.000999 | 0.003871 |
| Peak amplitude | 0.983 | 0.42782 | 0.83579 |

The rank evidence is strongest for fluence, not rise width. Decline is close to, but above, 0.05 after the joint correction. A rise-width difference in physical units need not imply rank separation; several large widths lie outside the box.

Table 2. Sensitivity to the supplied flare subset and clock grouping. The primary full box is above. The other rows are sensitivity analyses, not additional independent discovery tests. No joint correction across these choices is claimed.

| Group rule | N | K | Joint row-permutation tail fraction | Joint cyclic tail fraction |
|---|---:|---:|---:|---:|
| Published stall, 21 <= n < 30 | 16 | 6 | 0.003871 | 0.1875 |
| Onset only, n <= 24; group n >= 21 | 9 | 3 | 0.08333 | 0.1111 |
| Omit observed 2022 cycles 25, 27, 28 | 13 | 3 | 0.09441 | 0.3077 |
| No restart; group n >= 21 | 16 | 10 | 0.006868 | 0.2500 |

In the 13-flare subset, the individual fluence and decline p-values are each 0.02797. This recovers the source study's rank result. Both adjusted tail fractions are 0.09441. Thus those two related properties do not supply independent corrected evidence for the link without the unusual 2022 flares.

For no restart, the strongest row-permutation evidence moves to rise width (adjusted 0.006868). Fluence has adjusted 0.07755. The apparent property that best tracks the clock depends on whether a restart is assumed. Einstein Probe therefore affects the physical interpretation of the morphology association, not only forecasts of the next flare.

The cyclic test has only 16 phases and cannot reach 0.05 even for a unique most extreme phase. Its coarse resolution is a limitation, not evidence for independence. The pair-block result, which has 40,320 assignments, also shows a material loss of global evidence. This is not caused only by cyclic-test resolution.

## Interpretation and limits

There is strong rank evidence for a fluence difference under exchangeability of the full 16-flare sample. A claim that multiple testing alone removes the full-sample result would be wrong. The exact calculation strengthens that part of the earlier result and shows that one outlier does not drive it.

The stronger claim that a common physical process controls both the clock and fluence needs assumptions about temporal persistence. A broad, high-fluence episode overlaps a broad timing regime. The present series cannot securely distinguish this overlap from a specific orbit-by-orbit physical connection under the tested dependence nulls. These results do not prove that the physical link is absent, establish random kicks, or show that any block null is correct. They also do not test the X-ray stall itself, steady orbital decay, or the shared debris-delay ambiguity.

A decisive follow-up needs more flare cycles with both an X-ray dip and well-sampled optical profiles. The clock grouping and primary flare property should be specified before those flares are measured. Continued high fluence during an independently measured restart, or low fluence during a continued X-ray stall, would test a switch-like fluence clock directly. Optical-only lags should not define the event regime and then serve as evidence that morphology follows it.

No new telescope observations or new physical mechanism are reported. The sample is selected by earlier fit quality, errors are heterogeneous, missing cycles are not modelled, and only four optical properties are jointly tested. All source photometry and fitting limitations remain. This publication supplies a reproducible statistical constraint, not a physical solution for the stall.

## Reproduction and rights

Run from the extracted publication with Python 3.12, numpy, scipy, pandas and matplotlib:

    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --campaign /path/to/campaign --out /path/to/separate-scratch

The output path must be outside the signed publication. The script verifies the parent ZIP, checks the input entry against its signed manifest, and computes every table, leave-one-out check, block enumeration and figure. It also checks group-complement symmetry, time-reversal invariance, and invariance under increasing affine transformations of each property. A second complete run matched the numerical results exactly. There is no random seed because all tests are exhaustive. Run time is about 8 seconds on one CPU. No worker pool or background process is used.

The source path is `./campaign/90a362d70cd5e281b79832dbc0a8c332f08d720bd263a2e89c5ad2f8e3d35b31.zip`. The resolved shared path, ZIP hash, entry hash and source license hash are in `files/provenance.json`. No raw shared dataset is used or downloaded. The source record table is read only into memory and is not bundled. Original code, narrative, aggregate test outputs and the figure are included under the exact SCI baseline license. See `files/EXTERNAL_NOTICE.txt` for attribution and external rights. The software versions are in `files/environment.json`. No upload or remote submission was made by this worker.
