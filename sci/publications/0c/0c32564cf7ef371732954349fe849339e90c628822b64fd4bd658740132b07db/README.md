# Spike avalanches of 40-80 units in six awake mouse brain divisions did not meet the crackling-noise scaling relation; the gap fell with synchrony and did not need spike timing below 50 ms

Job: sci-1107-dell-neural-structure-and-computation-0441a1847647. Topic: neural-structure-and-computation. Campaign 11_07_2026, machine dell, account claude-andrii. Model: Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Fontenele et al. (2019, Phys. Rev. Lett. 122:208101) recorded spikes in rat visual cortex under urethane. They sorted 10-s windows by the coefficient of variation (CV) of the population spike count. They reported that the avalanche exponents satisfy the crackling-noise scaling relation, gamma = (tau_t − 1)/(tau − 1), only at an intermediate CV. They concluded that cortex is critical between desynchronized and synchronized states.

We applied the same test to awake mice. We used two public Neuropixels data sets (Steinmetz et al. 2019: 39 sessions, 10 mice; IBL brain-wide map: 84 sessions with sufficient units) and six brain divisions (isocortex, hippocampal formation, thalamus, midbrain, striatum, other). Each population had a fixed number of good units (40, or 80 in a second set). For each population we calculated Delta = (tau_t − 1)/(tau − 1) − (fitted slope of log mean size against log duration). Delta = 0 means that the scaling relation is satisfied.

Main results:

1. **The relation was not satisfied in awake mice.** In 204 Steinmetz populations of 40 units, Delta was 0.43 (95% mouse-bootstrap CI 0.40–0.46) in the lowest CV decile and 0.25 (0.23–0.29) in the highest CV decile. Delta was positive in all six divisions. It decreased with CV in 90% of populations (median Spearman rho −0.90). Delta changed sign in only 7.8% (5.4–10.6%) of populations. The smallest |Delta| was usually in the highest-CV decile (113 of 204), not at an intermediate CV. 80-unit populations (97) and IBL spontaneous recordings (122 populations, CV terciles, no sign change) gave the same pattern.
2. **Spike timing below 50 ms did not change the result.** A surrogate moved each spike to a random time inside its own 50-ms bin. This keeps every unit's 50-ms counts and so keeps the CV of every window exactly. The Delta profiles of recorded and jittered data had a median correlation of 0.92 (Steinmetz) and 0.97 (IBL). The recorded-minus-jittered difference in mean |Delta| was 0.006 (−0.011 to 0.025) for 40 units, −0.021 (−0.037 to −0.000) for 80 units and 0.000 (−0.018 to 0.017) for IBL.
3. **High-CV windows were quiet windows.** Over CV deciles, CV had a median Spearman correlation of −0.79 with face motion energy and −0.79 with the fraction of time with wheel movement.
4. **A network with no propagation gave the same pattern.** In a driven branching network (2,000 units, slowly changing common drive), the branching ratio m = 0 gave the data pattern: Delta about 0.3 at low CV, about 0.06 at high CV, and no jitter effect. **But the test also has little power at awake firing rates.** A near-critical network (m = 0.995) satisfied the relation with all 2,000 units (Delta = 0.00) only with weak drive (1.3 Hz per unit, CV 1.3–2.4). Then, 40 sampled units gave Delta 0.24 and the jitter removed it. At rates similar to the recordings (3.7–4.5 Hz per unit), networks with m = 0.98 and m = 0.995 also gave Delta of 0.14–0.22 and no jitter effect.

Conclusion: in awake mice, with 40–80 sampled units, avalanche exponents follow the population rate fluctuations at 50 ms or longer. The data do not show the intermediate-CV critical point that was reported under anesthesia. The scaling-relation test, as applied here, cannot separate near-critical propagation from slow common drive at awake rates and sampling. Thus this null result does not show that the awake brain is not critical. It shows that this signature is not evidence for criticality in these data.

## Figures

- `files/figures/fig2_delta_by_class.png`: Delta against CV decile (Steinmetz, 40 units) and CV tercile (IBL) in six divisions. Recorded data in blue, jittered data in orange. Bands are 95% bootstrap intervals over mice (Steinmetz) or sessions (IBL).
- `files/figures/fig4_branching_control.png`: the same test in a driven branching network at six combinations of branching ratio m and drive.
- `files/figures/fig3_recorded_vs_jitter.png`: per-population mean |Delta| and Delta-vs-CV slope, recorded against jittered; and the (tau, tau_t) pairs of all deciles.
- `files/figures/fig1_example.png`: one 40-unit VISp population. Size and duration distributions in the lowest and highest CV deciles, and both sides of the scaling relation against CV. (This example population is one of the few that crossed zero.)

## Data

All inputs are shared campaign datasets. Raw spike data are not copied into this bundle. SHA-256 hashes of every input file that the code read are in `files/provenance/`.

- Steinmetz et al. 2019, Nature 576:266 (doi:10.1038/s41586-019-1787-x), figshare doi:10.6084/m9.figshare.9598406.v2, CC BY 4.0. Shared path `datasets/steinmetz_2019/v5_good_unit_spike_times_2026-10-30/` (whole-session spike times of 33,997 phy-good units; `alf/` files `face.motionEnergy.npy`, `face.timestamps.npy`, `wheelMoves.intervals.npy`, `trials.intervals.npy`, `spontaneous.intervals.npy`). Area = released `allen_ontology` label of the peak channel.
- IBL brain-wide map (IBL et al. 2025, Nature, doi:10.1038/s41586-025-09235-0), CC BY 4.0, release 2023_12_bwm_release, spike sorting 2024-05-06. Shared path `datasets/ibl_bwm_spont_allspikes/2026-10-30/sessions/` (passive spontaneous epoch, about 300 s, 111 sessions; units with `label == 1`). Brain division from `channels.brainLocationIds_ccf_2017` with the Allen CCF 2017 structure graph `datasets/allen_ccf_2017/annotation_25_v2017/structure_graph_1.json`.

## Methods

Populations. Steinmetz: each session x released area label with at least N good units with a mean rate of 0.5 Hz or more (labels such as `root` excluded; coarse labels TH, MB and CA kept in their division). N = 40 with 3 random unit subsets (204 populations, 61 areas, 39 sessions, 10 mice), and N = 80 with 1 subset (97 populations). IBL: each probe x division with at least 40 good units of 0.5 Hz or more, 3 subsets (122 populations, 84 sessions). Results are averaged over subsets before statistics.

Cortical state. We merged the spikes of the N units. We divided the recording into consecutive 10-s windows. CV = SD / mean of the population count in 50-ms bins in the window. Steinmetz windows (whole session: task, passive stimuli and spontaneous periods) were put in CV deciles per population (median 32 windows per decile). IBL windows (about 30 per population) were put in CV terciles.

Avalanches. For each CV group, the time bin was the mean inter-spike interval of the merged population in that group (median 6.8 ms). An avalanche is a run of non-empty bins between empty bins. Avalanches that touch a window edge were not used. Size S = number of spikes; duration T = number of bins. Median 10,059 avalanches per Steinmetz decile.

Exponents. tau and tau_t: maximum-likelihood fits of a discrete power law truncated to [2, 99.5th percentile] (median upper limits S = 35, T = 16). gamma_fit: least-squares slope of log mean S against log T for T in [2, 99.5th percentile of T], with at least 5 avalanches per T. Delta = gamma_pred − gamma_fit, with gamma_pred = (tau_t − 1)/(tau − 1). Per population we calculated Delta in the lowest and highest CV group, the linear slope of Delta against CV, sign change (minimum and maximum Delta of opposite sign), the CV group with the smallest |Delta|, and a quadratic U-shape test (positive curvature, vertex inside the CV range).

Jitter surrogate. Each spike was moved to a uniform random time inside its own 50-ms bin. The grid had the same origin as the CV windows. This keeps each unit's 50-ms counts, all correlations at 50 ms and longer, and the CV of every window. It removes structure inside 50 ms, which is the scale of the avalanche bins (about 5–15 ms).

Statistics. Means with 95% cluster-bootstrap intervals (2,000 resamples of mice for Steinmetz, sessions for IBL).

Sensitivity runs (Steinmetz, 40 units, 1 subset): fixed 4-ms avalanche bin; fit ranges from 1; fit ranges from 3 to the 99th percentile.

Model control (`files/code/sim_control.py`). 2,000 binary units, 10 random targets each, 2-ms steps, 2,400 s. An active unit activates each target in the next step with probability m/10, with one-step refractoriness. Each unit also fires from an external drive h(t) = h0 exp(x(t)), where x is an Ornstein–Uhlenbeck process (time constant 2 s, SD 0.5). h0 = R0 (1 − m). We used m = 0, 0.9, 0.98, 0.995 with R0 = 5 Hz, and m = 0.98 with R0 = 10 Hz and m = 0.995 with R0 = 20 Hz to approach the recorded rates. Spike times were placed at random inside their step. Three sets of 40 units went through the same pipeline. The full population of 2,000 units gave the reference exponents.

## Results in detail

Values: estimate (95% bootstrap interval). Full tables: `files/results/summary.json`, `*_units.csv` (one row per population), `*_by_class.csv`, `*_decile_rows.csv.gz` (one row per population, subset and CV group).

| Set | Populations (clusters) | Delta, low CV | Delta, high CV | Sign change | Mean abs Delta, recorded minus jittered | CV range (median) |
| --- | --- | --- | --- | --- | --- | --- |
| Steinmetz, N = 40 | 204 (10 mice) | 0.43 (0.40–0.46) | 0.25 (0.23–0.29) | 7.8% (5.4–10.6%) | 0.006 (−0.011 to 0.025) | 0.43–0.73 |
| Steinmetz, N = 80 | 97 (9 mice) | 0.45 (0.40–0.51) | 0.20 (0.15–0.26) | 9.3% (4.3–14.3%) | −0.021 (−0.037 to −0.000) | 0.33–0.58 |
| IBL, N = 40 (terciles) | 122 (84 sessions) | 0.50 (0.46–0.54) | 0.38 (0.35–0.42) | 0% | 0.000 (−0.018 to 0.017) | 0.33–0.42 |

Mean exponents (Steinmetz, N = 40): tau 1.71, tau_t 2.04, gamma_fit 1.15, gamma_pred 1.48. Over all deciles, tau_t = 0.85 tau + 0.59 (r = 0.81) for recorded data and tau_t = 0.87 tau + 0.56 (r = 0.88) for jittered data. The two clouds overlap (Fig. 3).

Divisions (Steinmetz, N = 40). Delta was positive and decreased with CV in all six divisions. The slopes of Delta against CV were from −0.42 (isocortex) to −1.77 (midbrain) per CV unit, all with intervals below zero. Recorded-minus-jittered mean |Delta| was near zero in most divisions. The largest difference was in the hippocampal formation: 0.09 (0.03–0.15, 32 populations). With 80 units this difference had the opposite sign, −0.07 (−0.10 to −0.03, 6 populations), and in IBL it was 0.03 (−0.01 to 0.07). Thus we do not find a consistent division-specific effect of fast timing.

Sensitivity. All three variants kept Delta > 0 at low CV and a decrease with CV (median Delta from low to high CV: 0.33 to 0.11 with a 4-ms bin, 0.76 to 0.30 with fits from 1, 0.38 to 0.26 with fits from 3 to the 99th percentile; Delta decreased with CV in 97%, 97% and 76% of populations). Sign changes increased to 28% with the fixed 4-ms bin. The median recorded-minus-jittered difference in mean |Delta| was −0.045 to −0.011. With fits from 1 and with the 4-ms bin, some low-rate groups had tau near 1, which made gamma_pred very large. Thus the means of these two variants are unstable and we give medians.

Model control (`files/results/sim_summary.csv`):

| m | Rate per unit (Hz) | CV range | Delta, all 2,000 units | Mean Delta, 40 units | Mean Delta, 40 units jittered |
| --- | --- | --- | --- | --- | --- |
| 0 | 5.1 | 0.39–0.71 | 0.19 | 0.19 | 0.20 |
| 0.9 | 4.1 | 0.47–0.76 | 0.19 | 0.25 | 0.23 |
| 0.98 | 2.7 | 0.74–1.27 | 0.11 | 0.21 | 0.13 |
| 0.98 | 4.5 | 0.53–0.91 | 0.18 | 0.22 | 0.22 |
| 0.995 | 1.3 | 1.25–2.44 | 0.00 | 0.24 | 0.00 |
| 0.995 | 3.7 | 0.68–1.16 | 0.14 | 0.16 | 0.15 |

## Limitations

- Subsampling. We used 40 or 80 units per population. Fontenele et al. used multi-electrode arrays with their own unit counts. CV values depend on the number of units and on rates, so our CV values cannot be compared directly with theirs. The awake CV range (about 0.3–0.9) was narrower than the range that the anesthetized data are reported to cover.
- Short fit ranges. The avalanche sizes extend only to about 35 spikes at the 99.5th percentile (about 1.5 decades). The exponents depend on the fit range (sensitivity runs). We did not do a goodness-of-fit test against other distributions.
- Mixed behaviour. Steinmetz windows include task trials, passive stimuli and spontaneous periods. IBL windows are spontaneous only, but each population has only about 30 windows.
- No anesthesia or sleep. We did not test whether the relation holds under anesthesia in the same animals, so we cannot say if the difference from Fontenele et al. comes from state, species, recording method or analysis details.
- Literature access. We could not get the full text of Fontenele et al. (2019) during this work (publisher and preprint servers did not respond). We compare with the claims in its abstract and with the description of its method in arXiv:2002.08813. Our parameter choices (50-ms CV bins, 10-s windows, mean-ISI avalanche bin) follow the usual method of that group, but they can differ in detail.
- Power. The model shows that the jitter test detects fast propagation only when the drive is weak. Thus the absence of a jitter effect is not evidence against near-critical propagation at awake rates.
- The model is a simple random branching network, not a model of any specific brain circuit.

## Reproduce

Python 3.12.16, numpy 2.5.4, scipy 1.18.1, pandas 3.1.1, matplotlib 3.11.2 (the campaign's prepared environment). From a folder `work/` beside `datasets/` (the shared dataset store), with the code in `work/code/`:

```
OMP_NUM_THREADS=1 python code/run_steinmetz.py out/stein_N40 40 3 5     # about 10 min with 5 processes
OMP_NUM_THREADS=1 python code/run_steinmetz.py out/stein_N80 80 1 3
OMP_NUM_THREADS=1 python code/run_ibl.py out/ibl_N40 40 3 4
AV_DT=0.004 python code/run_steinmetz.py out/sens_dt4ms 40 1 2
AV_SMIN=1 AV_TMIN=1 python code/run_steinmetz.py out/sens_min1 40 1 2
AV_Q=0.99 AV_SMIN=3 AV_TMIN=3 python code/run_steinmetz.py out/sens_q99min3 40 1 2
python code/sim_control.py out/sim 0.0 0.9 0.98 0.995                   # about 15 min per value of m
SIM_R0=10 SIM_TAG=_r10 python code/sim_control.py out/sim 0.98
SIM_R0=20 SIM_TAG=_r20 python code/sim_control.py out/sim 0.995
python code/analyze.py results
python code/figures.py results figs
```

Unit subsets and jitter use seeds derived from session names (CRC-32), so reruns give the same numbers. Bootstrap intervals use a fixed seed. `files/results/sim/` holds the simulation outputs as CSV.

## Files

- `files/code/`: `aval.py` (avalanche, CV, jitter and exponent functions), `run_steinmetz.py`, `run_ibl.py`, `sim_control.py`, `analyze.py`, `figures.py`.
- `files/results/`: all tables described above.
- `files/figures/`: four figures.
- `files/provenance/`: SHA-256 of every shared input file used (`sha256_steinmetz_inputs.txt`, `sha256_ibl_inputs.txt`, `sha256_other_inputs.txt`).

## References

- Fontenele AJ et al. (2019) Criticality between cortical states. Phys Rev Lett 122:208101. doi:10.1103/PhysRevLett.122.208101.
- Steinmetz NA, Zatka-Haas P, Carandini M, Harris KD (2019) Nature 576:266–273. doi:10.1038/s41586-019-1787-x.
- International Brain Laboratory et al. (2025) A brain-wide map of neural activity during complex behaviour. Nature. doi:10.1038/s41586-025-09235-0.
- Destexhe A, Touboul JD (2020) Is there sufficient evidence for criticality in cortical systems? arXiv:2002.08813.
- Sethna JP, Dahmen KA, Myers CR (2001) Crackling noise. Nature 410:242–250. doi:10.1038/35065675.
