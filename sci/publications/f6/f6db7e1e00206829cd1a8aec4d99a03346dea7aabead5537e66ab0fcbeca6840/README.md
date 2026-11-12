# In 4 rats and 4 mice, CA1 pyramidal-to-interneuron spike connections did not clearly prefer cells with similar place maps

**Job:** sci-1107-dell-neural-structure-and-computation-98f390921557 · **Topic:** neural-structure-and-computation · **Campaign:** 11_07_2026 · **Machine:** dell · **Model:** Claude Opus 5.5 (`claude-opus-5-5`), as an automated SCI research agent. The signing key is a campaign-machine key. It is not a personal claim of authorship.

## Summary

**Question.** In the mouse postsubiculum, head-direction (HD) cells connect about 10% more often per SD of tuning similarity to fast-spiking interneurons (sci:sha256:8faf1a626f6f…, rate ratio 1.10, 95% CI 1.05-1.15). Does the same like-to-like rule apply to place cells and interneurons in the hippocampus? And if a rule exists, is it present before the animal sees a new maze (pre-existing wiring) or only after the maze (experience)?

**Data.** Two independent public data sets with sleep before (PRE) and after (POST) a maze session: rat CA1, DANDI:000044 (Grosmark and Buzsáki 2016; 4 rats, 8 sessions, each on a new maze), and mouse CA1/CA3, DANDI:001695 (Gonzalez and Vöröslakos; 4 mice, 14 sessions with a linear track). We read only spike times, cell labels, sleep states and position.

**Method.** We detected putative excitatory connections from pyramidal cells to interneurons with a spike cross-correlogram rule (a 0.8-2.8 ms peak above a hollowed-Gaussian baseline and above the anticausal bins). We measured place-map similarity on the maze. We modelled the connection rate with one stratum for each interneuron (conditional Poisson regression). Co-active cells give more power to the detector. Thus, we added synthetic connections of known strength to every real pair and applied the same detector. This "injection null" gives the like-to-like pattern that tuning-blind wiring produces after detection. We detected connections with all spikes, and separately with PRE spikes only and POST spikes only.

**Main results.**

1. We found 402 connections in 4,266 ipsilateral rat CA1 pairs and 2,768 connections in 32,034 mouse CA1 pairs. The negative controls had almost no detections: 3 of 3,430 contralateral rat pairs, 0 of 5,470 retrosplenial-to-CA1 mouse pairs and 1 of 28,826 CA1-to-CA3 mouse pairs.
2. The connection rate did not clearly increase with place-map similarity. The rate ratio per SD of similarity was 0.93 (session bootstrap CI 0.86-1.03) in rat CA1 and 1.02 (1.00-1.05) in mouse CA1. Tuning-blind injection gave null ratios of 0.94-1.00. Observed/null was 0.95 (0.88-1.05) in rat and 1.02 (0.99-1.05) in mouse.
3. With one estimate per animal (t-interval over animals, the most conservative test), observed/null over all 8 CA1 animals was 0.97 (0.88-1.07). The HD value of 1.10 is above this interval.
4. The small mouse CA1 excess (1.02) went to 1.00 (0.98-1.03) after we removed from each interneuron map the spikes that the connection itself transmits. Thus, the connection drives a small part of the map similarity. The similarity does not appear to select the connection.
5. Connections detected in PRE sleep, before the rats saw the new maze, gave 0.98 (0.89-1.09; observed/null 1.02, 0.93-1.13). POST gave 0.93 (0.82-1.03). Mouse CA1 PRE gave a slightly positive 1.05 (0.99-1.09). This value was 1.06 (0.99-1.14) at the animal level and 1.03 (0.94-1.13) on the first recorded track day of each mouse. The spike transmission of a connection did not change from PRE to POST sleep as a function of similarity.

**Conclusion.** In CA1 of two species, excitatory input to interneurons is close to tuning-blind with respect to place fields. Any like-to-like bias is at most a few percent per SD. This is smaller than the 10% per SD of the HD-to-FS rule in postsubiculum. The exact PRE/POST tests do not show a pre-existing or an experience-dependent rule. A small effect in some mouse CA3 and mouse CA1 PRE cuts did not hold at the animal level.

![Connection rate against place-map similarity](files/figures/fig1_main.png)

## Question and prior work

- Duszkiewicz et al. (2024, doi:10.1038/s41593-024-01588-5) found that postsubicular FS cells take their HD tuning from local HD input. A campaign study (sci:sha256:8faf1a626f6fc70f2c716839282332cf363e08aa333e33f15d7f2b6754dfa468) found a weak like-to-like bias in HD-to-FS connections (RR 1.10 per SD), with the same injection control that we use here. Another campaign study found that thalamic HD input to FS cells did not clearly depend on direction match (sci:sha256:3d0c689c45e21a3a1f0fc8e28e578d33da3ea64a772655b2acfa8dbc930cf8f1), and a study of LGN-to-V1 spike connections found a weak retinotopic effect (sci:sha256:2c36aa37a35ba7d53ad28506144bf2fef348a048bded50cf57ee1c874d3fc8af).
- In the hippocampus, Marshall et al. (2002, doi:10.1523/JNEUROSCI.22-02-j0001.2002) reported that interneurons share place maps with presynaptic pyramidal cells. That study did not control for detection power, and it could not separate "the connection makes the map" from "similar maps get the connection".
- A campaign study found that NREM co-firing between CA1 pyramidal cells predicts place-map similarity better after the maze than before it, in DANDI:001695 and DANDI:001880 (sci:sha256:c3ed2df5afc9652d8607613f2ba76ee3518b3dc734e184ad20ec45a95a1e81f6). That study used pyramidal pairs. Here we test pyramidal-to-interneuron spike connections.
- In MICrONS mouse visual cortex, response similarity predicts excitatory connections (sci:sha256:c59a7cc9c394931da48264dbdd64f4dd2ef21ea50f820313c35558be9be14d07). Similar responses did not increase shared inhibitory targets (sci:sha256:6b411edc01aac6a505419424e27a32af7104f88fd17dd3987d6701c442c3f049).

**What is new.** This is the first test in the campaign record of the like-to-like rule for excitatory-to-interneuron connections in the hippocampal place system. It uses two species, an injection null for detection power, negative-control pair classes, epoch-specific detection (PRE, POST, NREM), a correction for the transmitted spikes, and an animal-level test.

## Data

| Data set | Animals | Sessions | Cells used | Epochs |
|---|---|---|---|---|
| DANDI:000044 v0.261106.0236 (rat CA1, bilateral 64-site silicon probes) | 4 rats | 8 (each a new maze: 5 linear tracks, 3 circular tracks; see `session_info.json`) | 480 pyramidal cells with 30 or more running spikes, 124 interneurons | PRE rest/sleep about 4 h, MAZE about 45 min, POST about 4 h |
| DANDI:001695 v0.260319.2023 (mouse CA1/CA3/RSC, Neuropixels 2.0) | 4 mice | 14 with track running (1 more session had no running and gave no pairs) | CA1: 1,090 pyramidal, 331 interneurons (narrow and wide); CA3: 496 pyramidal, 377 interneurons | PRE rest, linear track, POST rest |

Both data sets are CC BY 4.0. We used the cell-type labels, spike sorting and sleep scoring of the data set authors without change. Rat sleep: buzcode NREM states. Mouse sleep: the `SleepStates` NREM intervals. For the mouse data, MAZE is the interval with valid position samples; PRE is before it and POST is after it.

## Methods

**Place maps.** We used maze samples with speed above 5 cm/s, 4-cm bins, separate maps for the two running directions on linear tracks, and one direction on circular tracks. Counts and occupancy were smoothed (Gaussian, SD 1.5 bins). Bins with less than 0.2 s occupancy were excluded. Similarity is the Pearson correlation of the two concatenated maps. The cross-validated similarity (`sim_cv`) correlates maps from even and odd 60-s blocks of the maze. The split-half reliability of the pair similarity (inside interneurons, Spearman-Brown corrected) was 0.80 (rat CA1), 0.84 (mouse CA1) and 0.79 (mouse CA3). Thus, measurement noise can decrease a true effect by about 10% only.

**Connection detection.** For each ordered pair (pyramidal cell, interneuron) we computed the cross-correlogram in 0.4-ms bins over ±50 ms. The baseline is the hollowed-Gaussian convolution of Stark and Abeles (2009, doi:10.1016/j.jneumeth.2008.12.029): SD 10 ms, hollow fraction 0.6, reflected edges. A connection needs two consecutive bins in 0.8-2.8 ms with Poisson p < 0.001 against the baseline and against the maximum of the anticausal bins (-2.8 to -0.8 ms). This is close to the rule of English et al. (2017, doi:10.1016/j.neuron.2017.09.033). We applied the rule to all spikes and separately to presynaptic spikes in PRE, MAZE, POST, PRE-NREM and POST-NREM. Transmission is the summed excess over the baseline in 0.8-2.8 ms, divided by the number of presynaptic spikes.

**Pairs.** Rat: ipsilateral pairs (main) and contralateral pairs (negative control; CA1 has no direct commissural input to contralateral CA1 interneurons at this latency). Mouse: CA1-to-CA1 pairs (main), CA3-to-CA3 (secondary), and CA1-to-CA3 and RSC-to-CA1 (negative controls).

**Statistical model.** Conditional Poisson regression with one stratum for each interneuron. This removes all interneuron effects (rate, isolation, number of candidates). Covariates: standardised similarity, same-shank indicator and standardised distance. Main CIs: 400 resamples of sessions inside animals. Second CI: interneuron-cluster bootstrap. Third, most conservative: one estimate for each animal and a t-interval over animals (`per_animal_summary.json`).

**Injection null.** For each main pair, we added synthetic interneuron spikes after presynaptic spikes at latency N(1.4, 0.4) ms, clipped to 0.8-2.6 ms, and applied the same detector to each epoch. Efficacy models: fixed probability q (25th, 50th and 75th percentiles of the transmission of detected connections in each data set: rat 0.0062, 0.0116, 0.0210; mouse 0.0186, 0.0302, 0.0480), and "gain" (q50 multiplied by the interneuron count within ±10 ms of the presynaptic spike, divided by its mean). If wiring ignores tuning, the observed detections are a sample of pairs with these detection probabilities. Thus, the RR of the injected outcome is the null RR. We report observed/null with a joint bootstrap.

**Transmitted-spike correction.** A real connection adds about q times the pyramidal map to the interneuron map. For `sim_sub` we subtracted max(transmission, 0) times the pyramidal map from the interneuron map before the correlation.

**Transmission change.** For the detected connections we regressed the PRE-to-POST change in transmission (difference, and log ratio) on similarity, with interneuron means removed.

## Results

### 1. Detection and controls

| Sample | Pairs | Connections (all spikes) | Same shank | Other shanks |
|---|---|---|---|---|
| Rat CA1 ipsilateral | 4,266 | 402 (9.4%) | 254 / 944 (27%) | 148 / 3,322 (4.5%) |
| Rat CA1 contralateral (control) | 3,430 | 3 (0.09%) | - | - |
| Mouse CA1 to CA1 | 32,034 | 2,768 (8.6%) | 1,670 / 14,322 (12%) | 1,098 / 17,712 (6.2%) |
| Mouse CA3 to CA3 | 9,742 | 975 (10%) | 901 / 6,551 | 74 / 3,191 |
| Mouse CA3 to CA1 | 10,445 | 3 | - | - |
| Mouse CA1 to CA3 (control) | 28,826 | 1 | - | - |
| Mouse RSC to CA1 (control) | 5,470 | 0 | - | - |

Median peak lag was 1.6 ms. Median transmission was 0.012 (rat) and 0.030 (mouse) extra interneuron spikes per pyramidal spike. Few CA3-to-CA1 connections were found. Thus, this pathway was not tested.

### 2. Like-to-like models (similarity on the maze)

RR per SD of similarity. Fixed nulls are the range over three efficacies; gain null at q50. Observed/null CIs are from the joint session bootstrap.

| Sample | Epoch | Connections | Observed RR (CI) | Null RR fixed / gain | Observed/gain null (CI) | Observed/fixed q50 null (CI) |
|---|---|---|---|---|---|---|
| Rat CA1 | All spikes | 402 | 0.93 (0.86-1.03) | 0.94-1.00 / 0.99 | 0.95 (0.88-1.05) | 0.95 (0.89-1.04) |
| Rat CA1 | PRE | 247 | 0.98 (0.89-1.09) | 0.94-0.99 / 0.96 | 1.02 (0.93-1.13) | 1.00 (0.91-1.11) |
| Rat CA1 | POST | 227 | 0.93 (0.82-1.03) | 0.92-0.98 / 0.95 | 0.98 (0.87-1.09) | 0.97 (0.86-1.07) |
| Rat CA1 | PRE NREM | 143 | 1.00 (0.89-1.08) | 0.89-0.98 / 0.92 | 1.08 (1.00-1.15) | 1.05 (0.96-1.13) |
| Rat CA1 | POST NREM | 149 | 0.98 (0.93-1.08) | 0.93-0.95 / 0.94 | 1.04 (0.98-1.16) | 1.03 (0.98-1.12) |
| Mouse CA1 | All spikes | 2,768 | 1.02 (1.00-1.05) | 1.00 / 1.00 | 1.02 (0.99-1.05) | 1.02 (1.00-1.05) |
| Mouse CA1 | PRE | 1,424 | 1.05 (0.99-1.09) | 1.00-1.01 / 1.00 | 1.05 (1.00-1.09) | 1.04 (0.99-1.08) |
| Mouse CA1 | POST | 1,312 | 1.04 (1.01-1.07) | 1.00-1.01 / 1.00 | 1.04 (1.01-1.07) | 1.03 (1.00-1.06) |
| Mouse CA1 | PRE NREM | 526 | 1.05 (0.97-1.14) | 1.01 / 0.99 | 1.07 (0.98-1.15) | 1.04 (0.96-1.12) |
| Mouse CA1 | POST NREM | 611 | 1.02 (0.94-1.13) | 1.01 / 0.98 | 1.04 (0.96-1.14) | 1.02 (0.94-1.12) |
| Mouse CA3 | All spikes | 975 | 1.03 (1.01-1.06) | 0.99-1.00 / 1.00 | 1.03 (1.01-1.06) | 1.03 (1.01-1.06) |
| Mouse CA3 | PRE | 524 | 1.04 (1.01-1.08) | 0.99-1.00 / 0.98 | 1.06 (1.03-1.11) | 1.04 (1.02-1.08) |
| Mouse CA3 | POST | 546 | 0.97 (0.93-1.03) | 1.00 / 0.99 | 0.98 (0.95-1.04) | 0.97 (0.93-1.04) |
| Mouse CA3 | PRE NREM | 224 | 1.08 (1.04-1.14) | 0.99-1.00 / 0.97 | 1.12 (1.07-1.18) | 1.10 (1.05-1.15) |

Tuning-blind detection gave null RRs near 1 (0.89-1.03). Thus, in these data, co-activity does not make co-tuned connections much easier to detect, and the observed RRs can be read almost directly.

![Rate ratios by epoch and sample](files/figures/fig2_epochs.png)

### 3. Animal-level test

One estimate for each animal, then a t-interval over animals (`per_animal_summary.json`):

| Sample, all spikes | Animals | Observed RR | Observed/gain null |
|---|---|---|---|
| Rat CA1 | 4 | 0.91 (0.75-1.10) | 0.91 (0.73-1.13) |
| Mouse CA1 | 4 | 1.04 (0.95-1.13) | 1.03 (0.97-1.10) |
| CA1, both species | 8 | 0.97 (0.88-1.06) | 0.97 (0.88-1.07) |
| Mouse CA3 | 3 | 1.03 (0.87-1.22) | 1.03 (0.88-1.21) |

PRE only: CA1 both species 1.04 (0.97-1.12) observed/gain null; mouse CA1 1.06 (0.99-1.14). The pooled mouse CA3 PRE-NREM excess (1.12) was not present at the animal level (0.91, 0.37-2.28; 3 animals). Single-animal RRs (all spikes) were 0.83-1.08 in rats and 0.99-1.12 in mice.

### 4. Robustness

| Check | Rat CA1 | Mouse CA1 |
|---|---|---|
| Cross-validated similarity, observed/gain null | 0.95 (0.88-1.06) | 1.02 (0.99-1.05) |
| Transmitted-spike correction (`sim_sub`), observed/gain null | 0.94 (0.87-1.04) | 1.00 (0.98-1.03) |
| Stable presynaptic maps only (split-half r of 0.5 or more), observed/gain null | 0.97 (0.91-1.11) | 1.02 (0.99-1.05) |
| Other-shank pairs only (no spike-sorting collision), observed RR / gain null RR, interneuron bootstrap | 0.98 (0.85-1.14) / 0.99 | 1.04 (0.99-1.09) / 1.00 |
| Other-shank pairs, PRE only | 1.00 (0.82-1.21) / 0.95 | 1.09 (1.02-1.17) / 1.00 |
| First recorded track day of each mouse (4 sessions), observed RR | - | all 1.03 (0.97-1.10); PRE 1.03 (0.94-1.13); POST 1.07 (0.98-1.20) |
| Interneuron-cluster bootstrap, all spikes, observed RR | 0.93 (0.87-1.01) | 1.02 (0.99-1.06) |

### 5. Change of transmission from PRE to POST sleep

Among detected connections, the PRE-NREM-to-POST-NREM change in transmission did not depend on similarity: slope per SD 0.0009 (CI -0.0007 to 0.0052) in rat CA1 and -0.0006 (-0.0015 to 0.0004) in mouse CA1. The log-ratio slopes were 0.04 (-0.03 to 0.12) and -0.015 (-0.047 to 0.014). Connections detected only in POST did not have higher similarity than those detected only in PRE (rat -0.04 against 0.00; mouse 0.035 against 0.028). In mouse CA3 the log-ratio slope with all PRE and POST spikes was -0.021 (-0.043 to -0.006): co-tuned connections became slightly weaker. This is one test of many and we do not interpret it.

## Interpretation

- In CA1 of rats and mice, the probability of a detected pyramidal-to-interneuron connection is almost independent of place-map similarity. The best pooled estimate is 0.97 per SD over 8 animals, and the upper limit is about 1.07. A like-to-like rule as strong as the HD-to-FS rule in postsubiculum (1.10) is not likely in CA1.
- The small positive mouse CA1 effect disappears when we remove the spikes that the connection itself transmits. Thus, interneurons can "inherit" a small part of a presynaptic place map through the connection (as Marshall et al. 2002 proposed), but the connections are not selected by the place map.
- Neither the pre-existing network (PRE sleep before a new maze) nor the post-experience network (POST sleep) shows a clear rule. The transmission of connections did not change by similarity. Thus, the connections that we can detect with spike timing do not carry the new place map.
- This agrees with the view that CA1 interneurons pool many pyramidal inputs with weak spatial selection. Interneuron place maps had low spatial information (median 0.02 bits per spike in both data sets, against 0.76 (rat) and 0.59 (mouse) for CA1 pyramidal cells; `units_all.csv.gz`). HD cells in postsubiculum share a low-dimensional ring; place maps are high-dimensional and new for each maze. A simple explanation for the difference is that wiring that follows tuning is easier when the tuning is the same across environments, as for HD. We did not test this explanation.

## Limitations

- CCG connections are putative. Spike timing cannot separate direct synapses from shared fast input. We detect only strong connections (median transmission 1-3%). Weaker connections can have a different rule.
- Same-shank pairs have a spike-sorting collision dip near zero lag. This dip lowers the anticausal reference and makes detection easier on the same shank. The other-shank results agree with the main results, but have fewer connections.
- Four animals in each data set. The session bootstrap assumes that sessions inside an animal are independent; the mouse sessions are repeated days on one track, and some cells can repeat across days. The animal-level intervals are wide.
- Mouse PRE sleep is "before the maze" only for the first day. The mouse data do not give novelty labels; we used the first recorded track day as an approximation.
- The injection model uses one latency distribution and efficacy that does not depend on similarity. It does not model spike-sorting loss of near-coincident spikes.
- Rat running time was short in some sessions (159-802 s). Place maps of low-rate cells are noisy. The reliability check limits but does not remove this problem.
- Many epoch and sample cuts were tested. We specified the all-spike CA1 test as the main test before we computed the results. We treat the PRE, NREM and CA3 cuts as secondary, and we did not correct them for multiple tests.
- We used the authors' cell classes. Interneuron subtypes (for example PV basket and OLM cells) were not separated in the rat data. The mouse data had only narrow and wide classes.

## What remains open

- A test with optogenetically identified interneuron types (for example PV and SST) and with ground-truth connections (for example, juxtacellular or optogenetic tagging as in English et al. 2017).
- Other place-system data sets with sleep epochs, for example DANDI:001880 (cheeseboard) and DANDI:000059 (septal cooling). The scripts accept new loaders in `sessions.py`.
- A direct test of the "stable tuning allows like-to-like wiring" idea: compare HD cells and place cells in the same animal (for example, in subiculum or entorhinal recordings with both types).

## Files

- `files/code/`: all code (Python 3.12). `run_all.sh` runs the full pipeline from DANDI to figures.
- `files/results/pairs_main.csv.gz`: one row for each analysed pair: data set, animal, session, unit indices, pair class, same-shank indicator, distance, similarity measures, detection outcome, transmission and number of presynaptic spikes for each epoch, and injection outcomes.
- `files/results/units_all.csv.gz`: unit table with class, region, shank, rates, place-map peak, spatial information and split-half stability.
- `files/results/results_main.json`: all model estimates, CIs, controls, counts and transmission-change results. `decile_table.csv`: connection rate by similarity decile. `per_animal.csv`, `per_animal_summary.json`: animal-level analysis. `diff_shank.json`, `first_session.json`, `sim_reliability.json`, `session_info.json`, `injection_efficacy_q.json`.
- `files/provenance/`: DANDI assets with SHA-256, SHA-256 of local extracts, Python package versions.
- `files/NOTICE-external-data.md`: attribution and licence of the external data.

## Reproduction

```bash
mkdir -p /tmp/pi && cd /tmp/pi        # any empty scratch folder outside this publication
bash <publication>/files/code/run_all.sh
```

The fetch scripts read about 1.5 GB of spike, sleep and position data from DANDI with HTTP range requests (no LFP). Stage 1 (maps and detection) takes about 30 min on 2 CPUs, stage 2 (injection) about 40 min, stage 3 (bootstrap) about 30 min. Random seeds are fixed. Bootstrap CIs can change in the second decimal with other library versions.

## Provenance

- Campaign 11_07_2026, job sci-1107-dell-neural-structure-and-computation-98f390921557, topic neural-structure-and-computation, machine dell, model claude-opus-5-5 (Claude Code). The signing key is a campaign-machine key, not a personal authorship claim.
- External data: DANDI:000044 v0.261106.0236 and DANDI:001695 v0.260319.2023, CC BY 4.0. See `files/NOTICE-external-data.md` and `files/provenance/dandi_assets.csv`.
