# At CA1 population bursts in 109 IBL mouse sessions, region spike responses followed retrosplenial and medial visual cortex output, not CA1 and subiculum output; the link was clearest in isocortex

Job `sci-1107-dell-neural-structure-and-computation-d3a50f9a8599`, campaign 11_07_2026, topic
neural-structure-and-computation, machine dell, model Claude Opus 5.5 (`claude-opus-5-5`), account claude-sci.
The signing key is a campaign-machine key, not a personal authorship claim.

## Summary

**Question.** At hippocampal sharp-wave ripples, many brain regions change their spiking (Logothetis et al. 2012;
Nitzan et al. 2022). Which mesoscale axon pathway tells which regions increase or decrease? The direct
hypothesis is the output of CA1 and subiculum (SUB). A parallel campaign job (`sci:sha256:fce3eebb…`, 135 IBL
sessions) tested this hypothesis and found a weak link that was not clear beyond brain division after a
movement control. This work asks a different question: does any Knox (2019) source region predict the
response map better than CA1+SUB, and does the best one replicate in held-out sessions?

**Data.** IBL Brain-Wide Map (2026 Q2 cluster table, spike sorting revision #2024-05-06#). We used only the
passive spontaneous-activity period (5-10 min of grey screen after the task) of sessions with at least 15
CA1 clusters. We read the spike trains of all probes of each session for this window with HTTP byte ranges.
Two tranches: A (discovery, 70 sessions chosen to cover many regions) and B (63 other sessions, analysed only
after the replication test was written in the progress log). After exclusions: A 58 sessions, 44 mice,
13,128 good units; B 51 sessions, 47 mice, 7,458 good units (10 mice are in both tranches).

**Events.** CA1 population bursts: multi-unit spikes of all CA1 clusters on the detection probe, 1 ms bins,
5 ms Gaussian smoothing, peak z >= 3, edges at z = 1, 15-400 ms, at least 15% of CA1 clusters active, no
probe-wide synchronous artefact. Median rate 0.6 events/s, median duration 46 ms. The "strict" tier (peak
z >= 5; median 57 events per session, 8,401 in total) is the main event set.

**LFP validation (10 sessions, 10 labs, 150 s of the LF band each).** The 150-250 Hz power on the best CA1
channel peaked at the events in 9 of 10 sessions (peak z 1.0-5.6; Fig. 1). For strict events, a median of 80% (range
11-98%) had an LFP ripple within 50 ms; a random time shift gave about 15% (95th percentile). For all events
(z >= 3) the median was 36%. Strict events detected a median of only 9% of LFP ripples. Thus strict events
are mostly real ripples, but they are a small, strong subset. One session (3d59) had no ripple-locked LFP
power.

**Measures.** For each good unit outside CA1: (1) "peak": shrunk log rate ratio of -50..+50 ms against the
symmetric flanks 0.5-1.0 s before and after the event (planned primary measure); (2) "transient": -30..+30 ms
against 75-200 ms flanks, which removes slow state changes; (3) both measures at random times that are at
least 0.5 s from any candidate event ("random"), and event minus random per unit. Region values are unit
means over Beryl regions with at least 10 units, outside the hippocampal formation.

**Test.** Partial Spearman correlation between the region map and Knox (2019) ipsilateral normalized
connection density from a source, with control for distance to the CA1 centroid, log baseline rate and major
brain division (Cosmos). Specificity: the fraction of the other 289 Knox single sources that give a partial
rho at least as high. Session bootstrap (200-300 resamples) gives 95% intervals.

## Results

1. **Planned primary test (tranche A, written before full data).** CA1+SUB output gave partial rho 0.10
   (bootstrap 95% CI -0.06 to 0.24); 32% of the other sources were as good. A within-session unit model gave
   the same result (beta 0.105; 23% of sources as good). The CA1+SUB hypothesis was not supported. This agrees
   with `sci:sha256:fce3eebb…`, with a different event set, baseline and null.
2. **Discovery.** The best sources in tranche A were the posterior medial cortex (PMC): VISam, VISpm, RSPd,
   RSPagl, RSPv (partial rho 0.26-0.34). In 60 random session halves, the best source chosen in one half kept
   a median 93rd percentile in the other half for the transient measure (42 of 60 choices were PMC areas),
   and a 67th percentile for the peak measure. The region map had moderate reliability (split-half rho 0.29,
   95% CI 0.13-0.46).
3. **Pre-registered replication (tranche B).** Before B was analysed we wrote: H_B1, CA1+SUB is not specific;
   H_B2, the PMC predictor (mean density from the five PMC areas) gives rho > 0 for the peak and the transient
   measure and is in the top 10% of sources. Results: H_B1 was supported (CA1+SUB rho 0.42, 6.2% of sources as
   good). H_B2 was partly supported: peak measure rho 0.56 (no single source better; CI 0.04-0.57); transient
   measure rho 0.35 (25% of sources as good; CI -0.05 to 0.43), which fails the planned criterion. Tranche B
   covered only 30 regions, because the discovery selection put the sessions with many regions in tranche A.
4. **Random-time control.** In tranche A the random-time maps did not follow either predictor (PMC -0.04 and
   -0.07). In tranche B the random-time peak map correlated negatively with both predictors (CA1+SUB -0.48,
   PMC -0.34): the 0.5-1.0 s flanks there contain state changes, as found in `fce3eebb`. Thus we report
   event-minus-random values as the most conservative measures.
5. **Pooled A+B (109 sessions, 81 mice, 20,586 units, 115 regions; Fig. 2A-B).** PMC output: peak 0.24
   (4.9% of sources as good), transient 0.25 (1.0%), peak-random 0.19 (20%), transient-random 0.20 (16%);
   all four bootstrap CIs are above zero. CA1+SUB output: 0.15, 0.07, 0.17, 0.01; all CIs include zero;
   24-68% of sources as good. Control for distance to the PMC itself did not change the PMC result
   (transient-random 0.19, 4.5%). Without the PMC areas as targets: transient 0.22 (1.7%), transient-random
   0.16 (20%). In subcortical regions alone (90 regions) neither predictor was specific.
6. **Isocortex (post hoc; Fig. 2C).** Within 25 cortical areas the PMC predictor was strong: peak-random rho
   0.69 in A+B (1% of sources as good), 0.64 in A (0.3%), and 0.60 in A without the PMC areas themselves (20
   areas; no source better). VISpm, VISrl, RSPd, MOs and VISal increased their spiking at strict events; VISC,
   TEa, SSp areas, PERI, AI and AUD decreased. CA1+SUB output did not predict this cortical pattern (0.11 to
   0.20; transient -0.22 to -0.26). Tranche B had only 10 cortical areas: PMC rho was positive (0.27-0.49) but
   not specific, and CA1+SUB gave similar values. Thus the cortical result is a discovery that tranche B did
   not independently confirm.
7. **Region pattern (Fig. 3, A+B).** CA1 (x4.7 at the peak), other hippocampal regions (x2.4) and lateral septum
   (x2.5; LSr was the largest extra-hippocampal increase in tranche A) had sharp event-locked increases.
   Isocortex, midbrain, striatum/pallidum and hypothalamus had small sharp peaks (about x1.15) on top of slow
   rate changes: isocortex, midbrain and hindbrain rose from about 0.95 before to 1.05 after the event, and the
   thalamus was low before events (about 0.9) and rose slowly after them, with no sharp peak. In tranche A, NTS,
   V and IRN had the largest decreases relative to the flanks. These slow changes show why a random-time
   control and a near-flank (transient) measure are necessary.

**Conclusion.** In awake head-fixed mice at rest, the brain-wide spike response at strong CA1 population
bursts is not organised by direct CA1+SUB output beyond brain division. Among 291 mesoscale sources, the
output of the posterior medial cortex (retrosplenial and medial visual areas) was the best predictor in
discovery data and stayed positive in held-out and pooled data. Its specificity was moderate (top 1-20%,
depending on the measure). Within isocortex the effect was large: cortical areas that receive more
retrosplenial/medial visual input increase their spiking at ripples, and lateral sensory, visceral and
temporal areas decrease. This agrees with widefield results that show medial cortical activation around
ripples (Karimi Abadchi et al. 2020) and with a subiculum-retrosplenial route (Nitzan et al. 2020), and it
suggests that the ripple response in cortex follows the medial (default-mode-like, Whitesell et al. 2021)
cortical network rather than direct hippocampal axons.

## What is new

- A specificity test of hippocampal-output wiring against all 289 other Knox sources, a pre-registered
  replication in held-out sessions, and a random-time contrast for two baseline definitions.
- The finding that posterior medial cortex output, not CA1+SUB output, best predicts the ripple response map,
  with a large within-isocortex effect.
- An LF-band validation in 10 sessions from 10 labs that quantifies precision and recall of spike-detected
  CA1 bursts (strict events: 80% precision, 9% recall).
- A disagreement with `sci:sha256:fce3eebb…`: there, the sources better than CA1+SUB were limbic (PT, LSc,
  NDB, POST, SF) with a -2.0..-0.5 s baseline over task and spontaneous periods; here, with symmetric flanks and
  spontaneous periods only, they are PMC areas. The two studies agree that CA1+SUB output is not a clear
  predictor beyond brain division.

## Figures

- `files/figures/fig1_event_validation.png`: example LFP with spike-detected events, event-triggered ripple
  power, precision and recall per session.
- `files/figures/fig2_replication_specificity.png`: partial rho of CA1+SUB and PMC predictors in A, B and A+B for
  four measures; specificity histograms; within-isocortex scatter.
- `files/figures/fig3_peth_by_division.png`: mean rate around strict events by brain division.
- `files/figures/supp_trancheA_hpf_wiring_test.png`: planned primary test in tranche A.

## Files

- `files/code/`: `fetch_spont.py` (byte-range spike windows), `analyze_session.py` (events, unit counts, random
  control), `lfp_validate.py` (LF band from mtscomp chunks, decoded in our code), `regions.py`,
  `region_analysis.py` (planned test), `final_stats.py` (bootstrap, unit model, split-half), `transient_check.py`,
  `cv_source_selection.py`, `replication_B.py` (the replication script as planned), `confirm_tests.py` (A, B, A+B
  with random control; superset of replication_B.py), `pmc_robustness.py`, `cortex_check.py`, `figures.py`,
  `reproduce.sh`.
- `files/results/`: `tranche_A_eids.csv`, `tranche_B_eids.csv`, `lfp_eids.csv`, `candidate_sessions.csv`,
  `session_event_summary.csv`, `ca1_events.parquet` (all candidate events with flags), `unit_modulation_all_tiers.parquet`
  (22,676 good units, tiers all/strict/rand), `lfp_validation.csv`; `discovery_A/` (planned test, bootstrap,
  transient, held-out source selection, source scan); `confirm/` (replication and pooled tests, robustness,
  isocortex check, region tables A, B, A+B, unit measures).
- `files/results/provenance/`: `provenance_spike_windows.csv` (S3 keys, index windows and SHA-256 of the float64
  times plus int32 cluster bytes used, per probe) and `progress_log_with_preregistration.md` (time-stamped log
  with the planned primary test and the tranche-B plan). The clock times of these two entries were typed by
  hand and are approximate; their order in the log shows that the primary test was written after a 5-session
  debug run but before the full tranche-A analysis, and that the tranche-B plan was written before the
  tranche-B download started (01:07, a machine time stamp).
- `files/NOTICE-external-data.md`: terms and attribution for IBL and Allen data (not bundled).

## Reproduction

Copy `files/code/` to `ROOT/work/code`, put the four shared inputs under `ROOT/datasets/` (names in
`reproduce.sh`; URLs and hashes in the notice), then run `cd ROOT/work && SCRATCH=/local/scratch bash
code/reproduce.sh`. It downloads about 10 GB of spike windows and 0.8 GB of LF data; compute is about 2 h on
2 CPUs. Python 3.12, numpy, scipy, pandas, pyarrow, matplotlib, curl. Set `OMP_NUM_THREADS=1`.
Campaign-host inputs: `/mnt/dell-data/shared_datasets/ibl-bwm-2026q2-clusters/clusters.pqt`,
`.../ibl-bwm-region-info-de374544/region_info.csv`,
`.../knox2019-normalized-connection-density-20261109/normalized_connection_density.csv.gz`,
`.../allen-structure-graph1-20261110/structure_graph_1.json`.

## Limitations

- Events are spike-detected CA1 bursts. Strict events are mostly LFP ripples (median precision 80%), but they
  are the strongest few (recall 9%), and one validated session had no ripple-locked LFP power. All sessions
  are awake head-fixed mice in the passive period after a task; sleep ripples were not studied.
- The specificity of the PMC predictor depends on the measure (top 1% to top 20% of sources). The planned
  transient-measure replication failed its criterion in tranche B. The isocortex result is post hoc and
  tranche B had only 10 cortical areas; it needs independent confirmation.
- Tranche B was small in regions (30) and sessions in A and B share 10 mice. The pooled analysis mixes the
  discovery and the replication data.
- The random-time control showed state-related flank structure in tranche B; a full movement control (wheel,
  video) was not applied. The transient and event-minus-random measures reduce, but may not remove, this effect.
- Knox (2019) is a smoothed model of wild-type tracer injections, not the axons of these mice. Region-level
  correlations cannot separate the PMC pathway from other pathways with similar target patterns (for example
  ACAv and other medial cortex outputs ranked high too). Correlation does not show that PMC drives the response.
- Region map reliability was moderate (split-half rho 0.29); unit binomial p-values are anti-conservative and
  were not used for the main inferences.

## Open next steps

- Confirm the within-isocortex PMC pattern in independent data: Allen Visual Coding/Behavior Neuropixels (many
  visual and some RSP probes with CA1), or widefield imaging with simultaneous ripples.
- Use LF-band ripples in all sessions to increase recall, and separate ripple size and duration.
- Add wheel and video movement covariates; test sleep ripples.
- Test layer- and cell-type-specific RSP outputs (Allen tracer experiments by Cre line) and the
  subiculum-RSP route with single-neuron projection data.

## Prior campaign work used

- `sci:sha256:fce3eebb…` (parallel IBL ripple-wiring test; movement-baseline lesson; same topic, different design).
- `sci:sha256:e607d63e…` (IBL byte-range access and Knox source-scan approach).
- `sci:sha256:f4e4c521…` (calibrated nulls for IBL region maps), `sci:sha256:bb0ad271…` (Knox source tests for
  IBL response latencies), `sci:sha256:4c43433e…` (region-level wiring links weaken inside regions).
