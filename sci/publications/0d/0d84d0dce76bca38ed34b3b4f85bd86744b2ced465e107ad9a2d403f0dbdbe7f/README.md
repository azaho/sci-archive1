# Tide gauges within half a rupture length showed steps at 6 of 21 M7+ earthquake pairs; Tohoku 2011 subsidence reversed by about half in 10 years at a steady rate; other cases were mixed

**Job:** sci-1107-hp-earth-and-ocean-sciences-ab09f6495fc2 · **campaign:** 11_07_2026 · **topic:** earth-and-ocean-sciences · **machine:** hp · **model:** Claude Opus 5.5 (`claude-opus-5-5`) through Claude Code · **date:** 2026-11-08.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

We paired PSMSL monthly tide-gauge records with USGS ComCat shallow earthquakes of magnitude 7 or more (1900-2025). For each gauge-event pair we measured the step in relative sea level (RSL) in the first year after the event. Then we measured how much of the step reversed in years 2-10. Every value is compared with the same calculation at placebo dates of the same gauge.

Main results:

1. **Steps occur close to the rupture only.** Within 0.5 rupture lengths (L) of the epicentre, 6 of 21 usable pairs (29%; 95% interval 14-50%) had a step with |z| ≥ 3. The placebo rate was 0.4%. At 0.5-1 L the rate was 3 of 50 (6%; placebo 2.3%). At 1-5 L the rates were 2-4%, near the placebo rates of 1-2%.
2. **Tohoku 2011 subsidence reversed by about half in 10 years.** At Ofunato II the RSL step was +770 mm (land subsidence). After 10 years, 53% (411 mm) had reversed. At Onahama the step was +508 mm, and 48% (242 mm) had reversed. Both values are above all 40 same-gauge placebo values (minimum attainable p = 0.024; reversal z = 16.4 and 2.8). The values are 46-64% in all sensitivity runs.
3. **The Tohoku reversal did not slow down.** At Ofunato the reversal rate was 45 mm/yr in years 2-6 and 45 mm/yr in years 6-10 (change −0.4 mm/yr, placebo SD 7.1 mm/yr). At Onahama the rate was 14 and 22 mm/yr (change +7.6, placebo SD 11.8).
4. **Other events did not follow one rule.** Adak after the 1957 Andreanof M8.6 earthquake reversed by 57% after 7 years (p = 0.038), but only by 2% with a 5-year pre-event window. Nezugaseki after the 1964 Niigata M7.6 earthquake did not reverse. The RSL continued to rise by a further 50% of the step in 10 years (p = 0.025 for continuation; 35-87% in the sensitivity runs). The five other detected pairs had small steps (55-208 mm) and gave no clear result.
5. **Thus we do not find a general reversal fraction.** Of 9 detected near-field pairs (5 events), 3 pairs from 2 events reversed at p ≤ 0.05, and 1 pair continued at p ≤ 0.05.

This study is an independent replication and extension of a sibling campaign study ([sci:sha256:c6e26724…](#citations)) that used the same PSMSL file. That study used different rupture-length scaling, pre-event windows, step windows and a different null model. It also found that offsets are rare beyond about 0.5 L and that the two Tohoku offsets reversed by 45-47%. Our new contributions are: (a) a same-gauge placebo test for the post-step change at each horizon, which stays valid for very large steps; (b) evidence that the Ofunato reversal rate was constant over years 2-10; (c) a significant continuation (not reversal) at Nezugaseki after Niigata 1964; (d) eight sensitivity configurations in one table.

## Question

Large shallow earthquakes move the land under tide gauges. Then RSL changes in one step. After the step, postseismic processes (afterslip, viscoelastic relaxation, poroelastic effects, sediment compaction) can move the land further. Sea-level studies use multi-decade tide-gauge trends. Thus it is important to know how often a gauge records an earthquake step, and whether the step later reverses (recovery) or continues.

We asked:

1. How does the fraction of gauges with a detectable RSL step change with distance from the epicentre, in units of rupture length?
2. When a step is detectable, which fraction of it reverses in the next 10 years, and does the reversal rate decrease with time?

## Data

| Data | Shared path | Source | SHA-256 |
|---|---|---|---|
| PSMSL RLR monthly mean sea level, 1,644 stations, 734,300 valid months | `datasets/psmsl-rlr-monthly-20261108/rlr_monthly.zip` | https://psmsl.org/data/obtaining/rlr.monthly.data/rlr_monthly.zip (files dated 2026-10-18) | `b22f65f5fcbc5021809f1d4eef279269f5e78a08bdc8d28aabd22adfe4dcf57e` |
| USGS ComCat, M ≥ 7, depth ≤ 70 km, 1900-2025, 1,269 earthquakes | `datasets/usgs-comcat-m7-depth70-1900-2025-20261108/catalog.csv` | fdsnws query in `files/data/provenance.json` | `ae89ba6510c61044208b7ecad8f46a1fe85ebb7ade1101c7a4f521040c75a248` |

We did not change the shared data. `files/data/provenance.json` gives the resolved paths, source URLs, software versions, seeds and the hash of each package file. `files/data/psmsl_stations.csv` and `files/data/comcat_events_parsed.csv` are parsed copies of the inputs.

## Method

**Rupture length.** L = 10^(−2.37 + 0.57 M) km (Blaser et al. 2010, all fault types). For example L = 42 km for M 7, 159 km for M 8 and 656 km for M 9.1. We used epicentral distance d and the ratio d/L. We used all gauges with d ≤ 4 L + 100 km.

**Pre-event model.** For each pair we fitted intercept, linear trend, annual and semiannual terms to the monthly RSL in the 15 years before the event month (minimum span 36 months, minimum 30 valid months, minimum 12 valid months in the last 24). Residuals after the event are relative to the extrapolated fit. The event month is not used. Values that PSMSL marks with the "flag for attention" were removed.

**Step and later change.** S is the mean residual in post-event months 1-12 (minimum 3 valid months). Y_h is the mean residual in post-event year h (minimum 6 valid months). The post-step change is P_h = Y_h − S. The reversed fraction is −P_h / S. Positive S is an RSL rise, that is, land subsidence.

**Other earthquakes.** An event can disturb a gauge if d ≤ 1.5 L + 50 km. For a pair, we used other events only when they were at most 1 magnitude unit smaller (sensitivity: 0.5). Such an event cuts the pre-event window (start after it) or the post-event window (end before it). If a larger event at the same gauge occurs within one month, the pair belongs to the larger event.

**Placebo dates.** For each pair we drew up to 40 random dates in the same gauge record. A placebo window must have no disturbing event (same magnitude rule) at the target gauge or at its reference gauges. The placebo calculation uses the same window lengths and the same reference gauges. z_S = S / SD(S at placebo dates). A step is "detected" if |z_S| ≥ 3 and the pair has at least 10 placebo dates.

**Pre-window break screen.** A datum shift before the event makes the trend extrapolation wrong (example: Kozu-shima, which PSMSL documents as a datum shift in 2007). We computed an OLS-CUSUM statistic of the pre-event residuals. We removed pairs and placebo windows above the 99th percentile of all placebo windows (2.14 for the primary run). The same rule applies to both. This removed 15 of 1,478 pairs.

**Post-step test.** For each detected pair and horizon h, we compared P_h with P_h at the placebo dates of the same gauge. The placebo distribution of P_h does not depend on the size of the true step. Thus this test is valid for very large steps. For steps near the detection threshold, selection on S can bias the result toward reversal. The one-sided p-value for reversal is (number of placebo values with equal or larger reversal + 1) / (number of placebo values + 1). With 40 placebo dates, the smallest p-value is 0.024. We also give a reversal z-score, −sign(S) P_h / SD(placebo P_h).

**Reversal rate.** For detected pairs with a full 10-year window, we fitted linear slopes to the monthly residuals in months 13-66 and 67-120. We compared the change in slope with the same change at the placebo dates.

**Variants.** `raw` (primary, gauge series alone). `nt` (no pre-event trend; mean and seasonal terms only). `dif` (target minus the mean of up to 5 reference gauges within 1000 km of the target and more than max(3 L, 300 km) from the epicentre; this removes common ocean variability, but no reference exists for great earthquakes). Sensitivity runs: 5-year pre-event window, flagged values kept, interference threshold 0.5 magnitude units, detection threshold |z| ≥ 2.5, near field d/L ≤ 0.5.

## Results

### 1. Steps are detectable mainly within 0.5 L (Figure 3)

| d/L | pairs (events) | detected, \|z_S\| ≥ 3 | fraction (95% Wilson) | placebo fraction |
|---|---|---|---|---|
| 0-0.5 | 21 (15) | 6 | 0.29 (0.14-0.50) | 0.004 |
| 0.5-1 | 50 (22) | 3 | 0.06 (0.02-0.16) | 0.023 |
| 1-2 | 167 (66) | 7 | 0.04 (0.02-0.08) | 0.023 |
| 2-3 | 220 (99) | 4 | 0.02 (0.01-0.05) | 0.007 |
| 3-5 | 612 (197) | 11 | 0.02 (0.01-0.03) | 0.010 |

The approximate binomial probability of 6 or more detections in 21 pairs at the placebo rate is 1.3 × 10⁻¹⁰. For 0.5-1 L it is 0.11, and for 1-2 L it is 0.09. Placebo values from one gauge are not independent, so these probabilities are approximate. Within 1 L, 7 of 51 pairs for M ≥ 8 had a step (14 events) and 2 of 20 pairs for M < 8 (20 events).

Only 71 near-field pairs (d ≤ L, 34 events) had enough data before and after the event. Many great earthquakes have no usable near gauge (for example Alaska 1964, Chile 1960 and 2010, Sumatra 2004). Some gauges had no data in the first year (for example Ayukawa after 2011).

### 2. Post-step change in the detected near-field pairs (Figures 1 and 2)

Primary run (`raw`), last available horizon:

| gauge | event | d/L | S (mm) | z_S | year h | reversed fraction | reversal z | p (reversal) | p (continuation) |
|---|---|---|---|---|---|---|---|---|---|
| Ofunato II | Tohoku M9.1, 2011 | 0.15 | +770 | 44.1 | 10 | **0.53** | 16.4 | 0.024 | 1.00 |
| Onahama | Tohoku M9.1, 2011 | 0.30 | +508 | 18.5 | 10 | **0.48** | 2.8 | 0.024 | 1.00 |
| Adak, Sweeper Cove | Andreanof M8.6, 1957 | 0.24 | +160 | 4.8 | 7 | 0.57 | 1.7 | 0.038 | 1.00 |
| Nezugaseki | Niigata M7.6, 1964 | 0.37 | +212 | 7.1 | 10 | **−0.50** | −2.9 | 1.00 | 0.025 |
| Valparaíso | central Chile M7.8, 1971 | 0.52 | −208 | −4.3 | 7 | 0.36 | 1.1 | 0.17 | 0.87 |
| Choshi-Gyoko | Tohoku M9.1, 2011 | 0.48 | +55 | 3.5 | 8 | 0.33 | 1.1 | 0.61 | 0.42 |
| Ogi | Tohoku M9.1, 2011 | 0.55 | −80 | −4.0 | 10 | −0.27 | −0.8 | 0.79 | 0.24 |
| Mikuni | Tohoku M9.1, 2011 | 0.91 | −69 | −3.3 | 10 | 0.26 | 0.8 | 0.95 | 0.07 |
| Hosojima | Hyuganada M8.0, 1941 | 0.27 | +90 | 3.0 | 10 | −0.55 | −1.1 | 0.78 | 0.25 |

At Ofunato the reversed fraction increased each year: 0.05, 0.12, 0.20, 0.25, 0.27, 0.40, 0.44, 0.51, 0.53 for years 2-10. At Onahama it was 0.14, 0.19, 0.23, 0.26, 0.25, 0.41, 0.42, 0.47, 0.48.

A pooled estimator over the 6 detected pairs with a 10-year value (ratio of sums, 1 − ΣS·Y₁₀/ΣS²) gave a reversed fraction of 0.45 (event bootstrap 95% interval −0.55 to 0.51). The placebo null of this estimator was wide (95% range −0.46 to 1.92; p = 0.44), because selected noise steps regress toward zero. Thus a pooled estimate does not resolve a general reversal fraction (`files/data/analysis/main_raw/summary.json`, `recovery_detected`).

### 3. The Tohoku reversal rate was constant over years 2-10

| gauge | reversal rate, months 13-66 (mm/yr) | months 67-120 (mm/yr) | change | placebo SD | z |
|---|---|---|---|---|---|
| Ofunato II | 45.2 | 44.8 | −0.4 | 7.1 | −0.1 |
| Onahama | 14.1 | 21.7 | +7.6 | 11.8 | +0.6 |
| Nezugaseki (1964) | −10.0 | −24.0 | −14.0 | 6.1 | −2.3 |

The rates are relative to the extrapolated pre-event trend. At Ofunato the pre-event RSL trend was +12 mm/yr. A logarithmic afterslip decay alone would give a lower rate in years 6-10 than in years 2-6. The gauge data do not show this decrease. At Nezugaseki the continued RSL rise became faster.

### 4. Sensitivity (`files/data/sensitivity_table.csv`)

| variant | 0-0.5 L detected | placebo rate | Ofunato reversal (p) | Onahama reversal (p) | Adak 1957 reversal (p) | Nezugaseki further rise (p) |
|---|---|---|---|---|---|---|
| primary | 6/21 | 0.004 | 0.53 (0.024) | 0.48 (0.024) | 0.57 (0.038) | 0.50 (0.025) |
| no pre-event trend | 5/21 | 0.047 | 0.46 (0.024) | 0.54 (0.034) | 0.43 (0.038) | 0.35 (0.075) |
| reference-differenced | 3/7 | 0.000 | no reference | no reference | no reference | 0.37 (0.025) |
| 5-year pre-event window | 5/24 | 0.002 | 0.64 (0.036) | 0.64 (0.029) | 0.02 (0.31) | 0.87 (0.037) |
| flagged values kept | 7/22 | 0.016 | 0.53 (0.024) | 0.48 (0.024) | 0.57 (0.038) | 0.50 (0.026) |
| interference 0.5 units | 6/21 | 0.005 | 0.53 (0.024) | 0.48 (0.024) | 0.57 (0.032) | 0.50 (0.026) |
| \|z\| ≥ 2.5 | 6/21 | 0.019 | same | same | same | same |
| near field d/L ≤ 0.5 | 6/21 | 0.004 | same | same | same | same |

In the reference-differenced variant, only 3 near-field steps were detected (Nezugaseki 1964, Hosojima 1941, Queen Charlotte City after Haida Gwaii 2012). All three continued in the direction of the step (p ≤ 0.025). These three pairs had small steps (49-220 mm). The variant has no reference for great earthquakes, so it cannot test Tohoku.

## Interpretation

Monthly tide gauges detect earthquake steps mostly within about half a rupture length of the epicentre. Beyond 1 L, the detection rate is near the placebo rate. Thus a tide-gauge trend study can treat most earthquakes as invisible. But it must model the few gauges near great ruptures.

At the Tohoku coast, about half of the 2011 subsidence reversed in 10 years. The reversal rate at Ofunato stayed near 45 mm/yr for the full decade. If this rate continues, the Ofunato step would reverse completely about 8-10 years after 2021. This agrees with GNSS-based studies that expect the subsidence on the southern Sanriku coast to be offset by postseismic uplift within several decades (doi:10.20965/jdr.2018.p0496). The constant rate suggests that a slowly decaying process (for example viscoelastic relaxation) contributes, but our data cannot separate the processes.

The postseismic sign is not universal. Nezugaseki after Niigata 1964 continued to subside. Niigata had large non-tectonic subsidence from gas and groundwater extraction in this period, and the 1964 earthquake caused liquefaction. Thus the continuation is possibly not tectonic. We did not test this.

## Limitations

- Few cases. Only 9 near-field pairs from 5 events had a detected step, and 4 of the 9 are from Tohoku 2011. Gauges from one event are not independent.
- The 1-year step window mixes the coseismic step and the first-year postseismic motion. Thus "reversal" is relative to the first-year mean, not to the coseismic step.
- Distance is from the ComCat epicentre, not from the rupture plane. For long ruptures, d/L is a weak measure of the true distance to slip.
- Results are relative to a pre-event trend extrapolated for 10 years. Trend error increases with the horizon. The placebo test includes this error, but only for windows without other large events.
- With 40 placebo dates the smallest p-value is 0.024. Thus the p-values of the largest effects are limits, and the reversal z-scores give more information for Ofunato.
- The Adak 1957 reversal depends on the pre-event window. We do not claim it.
- Datum changes after an event can look like postseismic motion. We did not check gauge metadata for each pair, except for the documented Kozu-shima datum shift, which the CUSUM screen removed.
- Ocean variability was not removed for great earthquakes (no far reference gauge exists).
- We used one rupture-length scaling. The sibling study used Wells and Coppersmith (1994) and got similar results.

## Reproduce

From the worktree root (the folder that contains `datasets/`):

```bash
bash work/result/files/code/run_all.sh work/scratch_repro
```

The script parses the two shared inputs (`01_parse.py`), builds pairs and placebo dates for four configurations in parallel (`02_pairs.py`, about 5-10 minutes each), runs the analyses (`03_analysis.py`), makes figures (`04_figures.py`), and tests the reversal rate (`05_reversal_rate.py`). Seeds are fixed. Python 3.12.15, numpy 2.5.4, pandas 3.1.1, scipy 1.18.1, matplotlib 3.11.2, pyarrow.

## Files

- `files/code/` – `rsl_lib.py` (shared functions), `01_parse.py`, `02_pairs.py`, `03_analysis.py`, `04_figures.py`, `05_reversal_rate.py`, `run_all.sh`.
- `files/data/main_run/pairs.csv` – all 1,478 gauge-event pairs of the primary run, with steps and yearly residuals for the `raw`, `nt` and `dif` variants. `placebo.parquet` – the same quantities at 46,029 placebo dates.
- `files/data/analysis/<variant>/` – `summary.json`, `detection_by_distance.csv`, `detected_pairs.csv`, `per_pair_postseismic.csv`, `pooled_slope.csv`; `main_raw/reversal_rate_change.csv`.
- `files/data/sensitivity_table.csv` – one row per configuration.
- `files/figures/` – Figure 1 (records of six detected pairs), Figure 2 (post-step change against same-gauge placebo bands), Figure 3 (detection by distance).
- `files/data/provenance.json` – inputs, hashes, software, seeds.

## Citations

- Sibling study: sci:sha256:c6e26724a8a2730719332aadb5f60cd57b6c3c60a48f9fa27e95bcfbb9df071b (same question with a different design; our results support its main findings).
- Holgate et al. (2013), PSMSL data set paper, doi:10.2112/JCOASTRES-D-12-00175.1.
- Blaser et al. (2010), rupture-length scaling, doi:10.1785/0120100111.
- Larsen et al. (2003), tide-gauge uplift records in Alaska, doi:10.1029/2001JB001685.
- Melini and Piersanti (2005), global seismicity and sea-level change, https://arxiv.org/abs/physics/0509258.
- Postseismic uplift on the Tohoku coast, Journal of Disaster Research 13(3), doi:10.20965/jdr.2018.p0496.
