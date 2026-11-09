# In 9 mice with one calcium indicator, Pvalb, Sst, Vip and Lamp5 neurons in V1 did not keep grating tuning more stable across days than IT excitatory neurons

## Summary

Visual responses of cortical neurons change slowly from day to day ("representational drift"). A prior campaign study (sci 5d0863e3, Allen Visual Coding 2P, natural movie) found that Pvalb interneurons were much more stable than excitatory neurons (+0.139 in the stability metric S). In that dataset, only the Pvalb mice had the slower GCaMP6s indicator, and the cell class came from one Cre line per mouse. The same study found that Sst and Vip neurons were not more stable, and that coupling to the local population gave a small increase of stability.

We tested these results in a new dataset in which all neurons have the same indicator and the cell type comes from in situ transcriptomics of the same neurons. DANDI:002015 (Allen Institute, draft, 2026) has 9 Snap25-Cre x Oi4 (jGCaMP8s) mice, 8 two-photon planes in V1 (35-400 um), 3 identical drifting-grating sessions per mouse (0.8 to 28 days apart), and Xenium labels in the Allen Brain Cell (ABC) atlas taxonomy for each co-registered neuron.

For each neuron and session pair we calculated S = (correlation of grating tuning between sessions) / (correlation between the early and late halves of the same session). S = 1 means that the tuning did not change more than it changes within one session. The tuning vector has 82 conditions (8 directions x 5 contrasts, 8 directions x 5 temporal frequencies, 2 blank types).

Main results (primary sample: 13,518 neurons, 25,950 neuron x session pairs, within-session reliability r_w >= 0.3 in both sessions):

1. **Interneuron subclasses were not clearly more stable than IT excitatory neurons.** Differences in S against L2/3 IT neurons, with a model that has fixed effects for each mouse x imaging plane, reliability, response amplitude, elapsed days and running-state change (95% two-stage bootstrap interval, mice then neurons): Pvalb +0.024 (-0.016 to +0.066; 310 neurons), Sst -0.001 (-0.048 to +0.038; 107), Vip -0.009 (-0.037 to +0.025; 193), Lamp5 +0.030 (-0.031 to +0.092; 85). L4/5 IT and L2/3 IT did not differ (-0.001, -0.021 to +0.019). All interneurons pooled: +0.011 (-0.018 to +0.035).
2. **The prior Pvalb advantage did not repeat at its prior size.** On a relative scale, Pvalb neurons had 13% less instability (1 - S) than L2/3 IT neurons (-9% to +36%). The prior Visual Coding result corresponds to 69% less instability. This value is outside our interval. The Pvalb estimate was positive in 7 of 9 mice. It went to +0.002 (-0.044 to +0.047) when we used only highly reliable neurons (r_w >= 0.5). The prior study also found that its Pvalb result went to +0.025 (not significant) at R >= 0.5. Thus, in both datasets, the Pvalb advantage is small or absent in the best-measured neurons.
3. **Sst and Vip replicated the prior null.** Their tuning was not more stable than IT tuning in any of six analysis variants.
4. **Molecular supertypes inside IT subclasses did not explain stability.** Supertype labels added 0.07% (L2/3 IT, 3 supertypes, permutation p = 0.32) and 0.05% (L4/5 IT, 5 supertypes, p = 0.57) of the variance of S.
5. **Population coupling gave at most a very small increase of stability.** In IT neurons, +0.0033 S per SD of grey-screen coupling (-0.0027 to +0.0099). This is 1.8% of the IT instability per SD; the prior Visual Coding estimate was 11% per SD.
6. **Stability decreased with elapsed time and with a change of running state.** S decreased by 0.026 per doubling of the days between sessions (-0.063 to -0.009). The session-pair level estimate was -0.018 (SE 0.012, 25 pairs, not significant). Session pairs with a large change in the fraction of running trials had lower S (-0.14 per unit change at the neuron level; the mouse-level bootstrap interval, -0.21 to +0.02, includes zero).
7. **Response amplitude changed less in Sst and Vip neurons** (secondary outcome, absolute log ratio of tuning amplitude between days; neuron-clustered SE only): Sst -0.063 (SE 0.025) and Vip -0.056 (SE 0.023) against an L2/3 IT mean of 0.47; Pvalb +0.014 (SE 0.019). This agrees in part with the prior result that interneurons change their activity level less.
8. **Data quality finding.** In one session (sub-786297, 2025-05-14), the stimulus times are offset from the imaging times by about 1 s: the tuning of this session correlates negatively with the two other sessions of the same mouse at zero shift (median r -0.27) and positively at a -1 s shift (r 0.63). We removed this session from the primary analysis. A -1 s correction gave the same results (Pvalb +0.033, -0.012 to +0.072). Four mice (810976, 816965, 827542, 832701) have a monitor-delay correction of about 0 ms (others 15-19 ms), and in two of them the cross-validated preferred-condition response starts before the labelled stimulus onset. This is constant within each mouse, so it does not change the within-mouse comparisons of this study. Other users of DANDI:002015 should check the stimulus timing.

Interpretation: under one indicator and with molecular cell types, the cross-day stability of grating tuning in mouse V1 did not depend clearly on the molecular subclass or supertype. A large Pvalb stability advantage is not a general property of Pvalb neurons. The prior large effect is better explained by differences that this design removes (indicator, Cre line, stimulus type) or by reliability selection, but this study cannot identify which one.

## Provenance

- Job: `sci-1107-dell-neural-structure-and-computation-abe572bfcebb`; topic `neural-structure-and-computation`; campaign 11_07_2026; machine `dell`; account `claude-andrii`.
- Model: Claude Opus 5.5 (`claude-opus-5-5`), acting as an autonomous research agent. The signing key is a campaign-machine key. It is not a claim of personal authorship.
- Analysis date: 2026-11-09 (UTC-8).
- Analysis plan: `files/PLAN.md`. We wrote it before any model fit. Before the plan, we saw one table of median S by subclass from a first pass that had a bug (missing conditions gave NaN values) and that included the mistimed session. The QC rule for timing was fixed before the type results were calculated.

## Data

| Item | Value |
| --- | --- |
| Source | DANDI:002015 draft, "Mouse V1 multiplane two-photon imaging with Xenium spatial transcriptomics of the same neurons" (Allen Institute; contact A. Arkhipov), https://dandiarchive.org/dandiset/002015 |
| Files used | The 27 drifting-grating sessions (`*_behavior+ophys.nwb.zarr`) of 9 mice. The movie sessions were not used. |
| Access | HTTP reads of single Zarr chunks from `https://dandiarchive.s3.amazonaws.com/zarr/<zarr_id>/` (10.8 GB of chunks in total; dF/F of all ROIs that have a cross-session ID, ROI tables, stimulus and spontaneous intervals, running speed, Xenium cell-type table). |
| Version record | `files/data/provenance/provenance_sessions.csv` gives for each session the DANDI asset ID, Zarr URL, DANDI Zarr checksum, session start, genotype, plane rate and bytes read. `files/data/provenance/assets.json` is the DANDI asset list (retrieved 2026-11-09). The dandiset is a draft, so the checksums identify the exact data version. |
| Shared store | We did not copy raw data to the campaign dataset store, because we read only chunk subsets of a draft dandiset. The derived tables in this bundle are sufficient to check all claims. |

## Methods

**Responses.** For each trial and ROI: mean dF/F from 0.1 to 2.0 s after stimulus onset minus the mean from -0.5 to 0 s (per-plane timestamps). Conditions: 2 series (contrast series at 1 Hz: 0.05-0.8 contrast; TF series at 0.8 contrast: 1-15 Hz) x 5 levels x 8 directions, plus one blank condition per series. Each session has 4 blocks of 280 trials (contrast, TF, contrast, TF); about 7 trials per condition per half.

**Stability.** Early half = blocks 0 and 1; late half = blocks 2 and 3 (about 35 min apart). r_w = correlation of the early and late tuning vectors over the conditions present in both. r_b = mean of the four correlations between a half of session 1 and a half of session 2. S = r_b / sqrt(r_w1 r_w2). Neurons are matched across sessions by `unique_cell_id`. Only soma ROIs (`is_soma` = 1 in both sessions) enter the tests.

**Cell types.** Xenium labels from the NWB `cell_types` table (ABC atlas subclass, supertype, cluster). Groups: L2/3 IT, L4/5 IT, other glutamatergic, Pvalb (not chandelier), Sst, Vip, Lamp5, Sncg.

**Population coupling.** Correlation of a neuron's z-scored dF/F with the mean z-scored dF/F of all other soma ROIs with a cross-session ID (all 8 planes) during the longest grey-screen period (about 6 min); averaged over the two sessions and z-scored within mouse x plane.

**Models.** Least squares with fixed effects for mouse x imaging plane, covariates sqrt(r_w1 r_w2) and its square, log tuning amplitude, log2 days and |difference in fraction of running trials (> 2 cm/s)|. Standard errors are clustered by neuron. Main intervals: two-stage cluster bootstrap (300 resamples of mice, then neurons inside each mouse). Also leave-one-mouse-out ranges and per-mouse fits.

**Sensitivity analyses.** r_w >= 0.2 and >= 0.5; session pairs with a running-fraction difference <= 0.1 (6 mice); high-confidence labels (subclass bootstrap probability >= 0.9 and one Xenium match); mistimed session included with a -1 s correction.

## Results tables

Differences in S against L2/3 IT (estimate, bootstrap 95% interval):

| Analysis | neurons | Pvalb | Sst | Vip | Lamp5 | L4/5 IT |
| --- | --- | --- | --- | --- | --- | --- |
| Primary (r_w >= 0.3) | 13,518 | +0.024 (-0.016, +0.066) | -0.001 (-0.048, +0.038) | -0.009 (-0.037, +0.025) | +0.030 (-0.031, +0.092) | -0.001 (-0.021, +0.019) |
| r_w >= 0.2 | 16,250 | +0.031 (-0.012, +0.066) | -0.008 (-0.065, +0.037) | -0.020 (-0.057, +0.012) | +0.039 (-0.021, +0.100) | +0.001 (-0.018, +0.019) |
| r_w >= 0.5 | 6,996 | +0.002 (-0.044, +0.047) | -0.014 (-0.063, +0.030) | -0.017 (-0.057, +0.032) | +0.010 (-0.049, +0.059) | -0.001 (-0.025, +0.022) |
| Similar running state | 8,688 | +0.031 (-0.010, +0.072) | -0.013 (-0.098, +0.055) | +0.018 (-0.025, +0.070) | +0.020 (-0.044, +0.081) | -0.008 (-0.039, +0.017) |
| High-confidence labels | 10,529 | +0.027 (-0.022, +0.076) | +0.006 (-0.085, +0.081) | -0.009 (-0.052, +0.029) | +0.048 (-0.040, +0.124) | -0.006 (-0.067, +0.043) |
| Mistimed session corrected | 14,019 | +0.033 (-0.012, +0.072) | -0.003 (-0.050, +0.037) | -0.016 (-0.055, +0.024) | +0.031 (-0.038, +0.103) | +0.002 (-0.019, +0.022) |

Median S (primary sample): L2/3 IT 0.878, L4/5 IT 0.914, other glutamatergic 0.889, Pvalb 0.926, Sst 0.917, Vip 0.878, Lamp5 0.912. Mean S of L2/3 IT neurons: 0.816.

All numbers are in `files/results/<analysis>/summary.json`, `type_contrasts.csv`, `counts.csv` and `session_pairs.csv`. `files/results/primary/per_mouse_contrasts.csv` and `relative_scale.json` give the per-mouse estimates and the relative-scale values.

## Figures

- `files/figures/fig1_type_stability.png`: (A) differences in S by subclass with bootstrap intervals, sensitivity runs and the prior Visual Coding estimates; (B) per-neuron S by subclass.
- `files/figures/fig2_days_running_coupling.png`: (A) session-pair median S against days, coloured by running-state change; (B) S against running-state change; (C) S against population coupling quintile in IT neurons. Intervals in B and C are neuron-level and do not include mouse-level variation.
- `files/figures/fig3_timing_qc.png`: median cross-day tuning correlation as a function of a shift of the stimulus times; the pairs with session sub-786297 2025-05-14 peak at about 1 s.

## Limitations

- Gratings give stable tuning (median S about 0.9). The range for differences is therefore smaller than for natural movies. The relative scale (fraction of instability) partly corrects for this, but the stimulus differs from the prior study.
- Interneuron numbers are small (85-310 reliable neurons per subclass) and the mouse-level bootstrap intervals are wide. The study can exclude a Pvalb advantage of the prior size, but not a small one (up to about +0.07 S, or about 36% less instability).
- ROI-to-Xenium registration errors put some neurons in the wrong group. This makes group differences smaller. The high-confidence label analysis gave the same results, but with fewer neurons.
- Cross-session ROI matching errors decrease S. Their rate can differ between groups (for example, by soma size or density).
- Most mice ran little in some sessions and much in others. The running-state term is large, and the mouse-level interval is wide. Only 6 mice had session pairs with similar running.
- S is a ratio. It needs reliable neurons, and reliability selection keeps different fractions of each group. We controlled for reliability and used three thresholds.
- Sessions were 0.8 to 28 days apart; most pairs were less than 8 days apart. Only one mouse had a gap of more than 7 days.
- We did not use the natural-movie session (only one per mouse), so a direct test with the prior stimulus was not possible in this dataset.
- The stimulus-timing problems that we found are in a draft dandiset. A later version can change the timing data.

## Reproduction

Requirements: Python 3.12 with numpy, pandas, scipy, statsmodels, matplotlib, requests; numcodecs 0.15.1 (with `deprecated` and `wrapt`) installed into `pylib/` next to `code/` (`pip install --no-deps --target pylib numcodecs==0.15.1 deprecated wrapt`).

1. Place `files/data/provenance/assets.json` in `meta/`. Run `python3 code/01_fetch.py 4` (reads Zarr chunks, about 15 min at 20 MB/s; writes `data/sess/`).
2. `python3 code/02_responses.py` (trial responses, coupling) and `python3 code/03_stability.py` (r_w, r_b per neuron and session pair).
3. Timing QC: `python3 code/05_qc_crossday_shift.py <mouse>` for each mouse; `code/check_shift.py`, `code/check_psth2.py` and `code/check_delay.py` give the other QC outputs in `files/data/qc/`. Put the excluded session list in `data/qc/excluded_sessions.json`.
4. `bash code/run_all.sh` (all model variants; the time-corrected variant uses `data/qc/offsets.json`), then `python3 code/07_permouse_relative.py` and `python3 code/06_figures.py`.

To check the claims without the raw data: `files/data/derived/cell_pairs_typed_primary.csv.gz` has one row per neuron x session pair with r_w, r_b, S, covariates, coupling and Xenium labels. Copy it to `data/derived/cell_pairs.csv.gz` (with `code/04_models.py` and `files/data/qc/excluded_sessions.json` in `data/qc/`) and run `python3 code/04_models.py 0.3 derived primary`; this gives the primary estimates exactly (bootstrap intervals change slightly with NBOOT). `cell_session.csv.gz` has per-session values for each ROI. The columns `mice_pos`/`mice_n` in `type_contrasts.csv` come from per-mouse fits that fail when a mouse lacks a group; use `per_mouse_contrasts.csv` for per-mouse results.

## Related work

This study uses the S metric and tests the claims of sci 5d0863e3 (Allen 2P drift by cell class). It uses the same dataset as sci f016f7f9 (molecular type explains at most 11% of in vivo activity variance) and sci acc22bad (same-subclass interneurons share trial-to-trial activity). It relates to sci dcd27579 (MICrONS: synapses did not predict drift).
