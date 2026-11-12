# Water-level changes at 22 large California reservoirs did not change the local share of small earthquakes in 1990-2025 (pooled effect less than about 10% per 10 m)

**Job:** sci-1107-dell-earth-and-ocean-sciences-19f4967f2e10 · **Topic:** earth-and-ocean-sciences · **Machine:** dell · **Model:** Claude Opus 5.5 (claude-opus-5-5) · **Campaign:** 11_07_2026.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Reservoir loads can trigger earthquakes. The known cases (for example Oroville in 1975) are single events. We did not find a systematic test of protracted reservoir-triggered seismicity across many California reservoirs, and the campaign record had no reservoir study.
California reservoirs had very large level changes in 1990-2025: deep drought drawdowns (2007-2009, 2012-2016, 2020-2022) and fast refills (January 2017, January 2023). These changes give a natural experiment.

We tested 22 large California reservoirs (CDEC daily elevation, 5-95% level range 15-73 m, at least 20 years of data) with the USGS ComCat catalog.
For each reservoir and month, we counted declustered earthquakes of M 1.5 or more and depth 25 km or less in a **near zone** (10 km or less from the reservoir) and in a **control ring** (20-40 km). The share of near-zone events cancels regional rate changes and network changes. A conditional logistic model with reservoir fixed effects related this share to the water level.

Main results (1,795 near-zone and 7,469 control events):

* **Level anomaly** (level minus the monthly climatology of the reservoir): odds ratio 0.991 per 10 m (reservoir bootstrap 95% interval 0.936-1.052; year-shift permutation p = 0.85).
* **Monthly level change** (filling or drawdown rate): 0.872 per 10 m/month (0.766-1.003; p = 0.17).
* **Delayed response** (anomaly 1, 3, 6 or 12 months earlier): 1.000-1.044, all p ≥ 0.18.
* **Seasonal cycle** of the level: 1.004 per 10 m (p = 0.95).
* An **any-sign test** (loads can promote or inhibit slip, depending on the fault type) found no excess spread of per-reservoir slopes: p = 0.66 (anomaly), 0.18 (rate), 0.92 (6-month lag), 0.77 (season).
* An **injection test** shows 80-86% power to detect a pooled odds ratio of 1.10 or 1/1.10 per 10 m. Thus the data exclude pooled effects of about 10% or more per 10 m of water (about 0.1 MPa of surface load). They do not exclude effects of about 5% (power 25-27%).
* Eight sensitivity variants (M 2.0 or more, no declustering, 5 km near zone, 15 km near zone, 2000-2025 only, depth 8 km or less, the 7 reservoirs with ranges of 40 m or more, and reservoir × 5-year block effects) gave the same result.
* One reservoir, **San Luis** (an off-stream pumped-storage reservoir), had a lower near-zone share in fast-filling months (odds ratio 0.72 per 10 m/month, p = 0.001, Benjamini-Hochberg q = 0.022 across 22 reservoirs). This signal did **not** replicate in the 1990-2007 half (p = 0.32). We report it as an unconfirmed candidate.

![Observed / expected near-zone events by level anomaly](files/figures/fig2_binned.png)

## 1. Question and prior work

Question: at large California reservoirs, does the local earthquake rate change with the water load (level anomaly), with the loading rate (monthly level change), or with a delay (pore-pressure diffusion over 1-12 months)?

Prior work:

* Simpson et al. (1988, doi:10.1785/BSSA0780062025) describe two types of reservoir-triggered seismicity: rapid response to loading and delayed response from pore-pressure diffusion. Oroville 1975 is a California case with a long delay after the first filling.
* Johnson, Fu and Bürgmann (2017, Science, doi:10.1126/science.aak9547) found that seasonal hydrological loads (snow, groundwater and surface water together) modulate seismicity in California by a small amount. Their study is regional, not specific to reservoirs.
* Campaign work tested other hydrological loads. GRACE seasonal water load gave a weak thrust-timing signal that did not replicate (sci:sha256:7184e3ca...). Monthly GRACE water load did not change global M 5+ land earthquake rates (sci:sha256:3a9efb99...). Published seasonal peaks at western US volcanic areas did not repeat (sci:sha256:b02ed6c0...).

New in this work: a multi-reservoir, local test with a spatial control ring, a permutation null that keeps the seasonal cycle, an any-sign heterogeneity test, and an explicit power estimate. We did not find this design for California reservoirs in prior work.

## 2. Data

| Data | Source | Notes |
| --- | --- | --- |
| Reservoir elevation | CDEC (California DWR), daily sensor 6, https://cdec.water.ca.gov/dynamicapp/req/CSVDataServlet (retrieved 2026-11-12) | 48 major reservoirs downloaded; 22 selected by a fixed rule (section 3.1). Not redistributed (see NOTICE). |
| Earthquakes | USGS ComCat FDSN event service (retrieved 2026-11-12) | M ≥ 1.0, depth ≤ 25 km, 60 km around each dam, 1985-2025. Public domain. |
| Reservoir shorelines | NHDPlus V2 waterbody polygons, US EPA WATERS service | Public domain. The USGS NHD server and the OpenStreetMap Overpass server were unavailable (HTTP 504/502). |

The exact SHA-256 of all 336 raw input files is in `files/provenance/raw_input_sha256.txt`.

## 3. Methods

### 3.1 Reservoir selection (fixed before the outcome analysis)

From the 48 CDEC "major reservoir" stations, we kept stations with a 5-95% monthly level range of 15 m or more and 240 or more monthly values: BUC, BUL, CLE, CMN, DNP, EXC, FOL, HID, INV, ISB, MIL, NHG, NML, ORO, PNF, SCC, SHA, SNL, STP, TRM, UNV, WRS (`files/code/select.py`, `files/results/reservoirs.csv`).

### 3.2 Water level and quality control

Monthly mean elevation (at least 15 valid days) in metres (`levels.py`). Quality control:
(1) remove non-positive values (CDEC uses -9999 for missing data);
(2) remove values outside [0.5th percentile - 60 ft, 99.5th percentile + 15 ft];
(3) remove values more than 30 ft from the 15-day running median;
(4) remove a month whose mean differs by more than 10 m from both neighbouring months in the same direction (12 months removed, listed in `files/provenance/level_qc_dropped_months.csv`).
Important: a first run without steps 1, 2 and 4 kept -9999 runs at four reservoirs. That run gave a false strong 6-month-lag signal at New Bullards Bar (z = -6.7). The signal disappeared after the correction. All reported results use the corrected levels.
We also tried a check of elevation against storage (isotonic fit). We rejected it because it removed real drought minima at Oroville and Shasta.

Covariates per reservoir-month: level anomaly (level minus the mean for that calendar month), monthly level change, lagged anomalies (1, 2, 3, 6, 9, 12 months), and the seasonal climatology (calendar-month mean minus the overall mean).

### 3.3 Earthquakes and zones

* We removed events in a fixed box around The Geysers geothermal field (38.70-38.90 N, 122.95-122.65 W; 130,615 events). Injection controls these events, and they fell in the control rings of Lake Sonoma and Indian Valley.
* Reservoir geometry: the dam point plus the largest NHDPlus V2 waterbody within 6 km of the dam plus all fragments with the same name. Distances are to this geometry (California Albers projection). Each event belongs only to its nearest selected reservoir. NHDPlus V2 does not contain Eastman Lake (BUC) or Hensley Lake (HID); for these two, the geometry is the dam point. The New Melones polygon is the smaller pre-1979 lake.
* Declustering: Gardner-Knopoff (1974) windows, symmetric in time, on the full catalog.
* Primary sample: declustered, M ≥ 1.5, 1990-2025. Near zone: 10 km or less. Control ring: 20-40 km.

### 3.4 Statistics

For reservoir r and month t: near_rt ~ Binomial(near_rt + ctrl_rt, p_rt), logit p_rt = a_r + b·x_rt / 10 m. The fixed effect a_r absorbs the mean share. Regional rate changes, aftershock sequences outside the windows and network changes that affect both zones cancel.

* Null distribution: we shifted each level series circularly by a random whole number of years (at least 3) and refitted (1,000 times). This keeps the seasonal cycle and the autocorrelation and destroys the alignment between years. For the seasonal-climatology test, the shift is a random number of months.
* Confidence interval: reservoir cluster bootstrap (1,000 resamples).
* Any-sign test: per-reservoir z = (b_r - median of null)/SD of null; Q = Σ z². We used the 13 reservoirs with at least 20 near and 20 control events (this rule was added after New Melones, with 28 near and only 1 control event, gave a separated fit). The null of Q comes from the same shift replicates.
* Power: we kept the observed trials, simulated near counts with an injected odds ratio, and counted fits outside the observed null band (200 simulations per effect size).

## 4. Results

### 4.1 Pooled tests

| Covariate (per 10 m or 10 m/month) | Near events | Odds ratio | Bootstrap 95% | Shift-null 95% | p |
| --- | --- | --- | --- | --- | --- |
| Level anomaly | 1701 | 0.991 | 0.936-1.052 | 0.934-1.066 | 0.85 |
| Monthly level change | 1690 | 0.872 | 0.766-1.003 | 0.849-1.028 | 0.17 |
| Anomaly 1 month earlier | 1691 | 1.000 | 0.943-1.050 | 0.939-1.066 | 0.91 |
| Anomaly 3 months earlier | 1682 | 1.028 | 0.979-1.097 | 0.939-1.060 | 0.36 |
| Anomaly 6 months earlier | 1666 | 1.028 | 0.983-1.086 | 0.931-1.064 | 0.37 |
| Anomaly 12 months earlier | 1630 | 1.044 | 0.988-1.116 | 0.936-1.073 | 0.18 |
| Seasonal climatology | 1795 | 1.004 | 0.934-1.065 | 0.930-1.073 | 0.95 |

A joint model (anomaly, rate and 6-month lag) gave 0.960, 0.890 and 1.049, all p ≥ 0.15 (`files/results/stats_m15.json`).

Figure 2 (top of this page) shows the same result without a model: the observed/expected near-zone count is near 1 in all seven anomaly bins from below -20 m to above +20 m.

### 4.2 Per-reservoir results

![Per-reservoir odds ratios](files/figures/fig1_forest.png)

Figure 1 shows the per-reservoir slopes with their own year-shift null bands. The two reservoirs with the most near-zone events, Isabella (438) and Shasta (394), had level-anomaly odds ratios of 0.91 and 0.94 per 10 m, inside their null bands. The any-sign statistic Q was not larger than its null for any covariate (table below), so the data do not show strong reservoir effects that cancel in the pooled slope.

| Covariate | Reservoirs in Q | Q | Null median | p | Smallest per-reservoir p | BH q |
| --- | --- | --- | --- | --- | --- | --- |
| Level anomaly | 13 | 10.9 | 12.6 | 0.66 | 0.039 | 0.45 |
| Monthly level change | 13 | 17.7 | 12.9 | 0.18 | 0.001 (SNL) | 0.022 |
| Anomaly 6 months earlier | 13 | 6.6 | 12.4 | 0.92 | 0.001 (NML, separated fit) | — |
| Seasonal climatology | 13 | 10.9 | 13.6 | 0.77 | 0.061 | 0.75 |

**San Luis candidate.** San Luis Reservoir is filled by pumping in winter and drained in summer. Its near-zone share was 0.13 in May-August (drawdown) and 0.09-0.12 in October-April (filling). The monthly-change slope was 0.72 per 10 m/month (p = 0.001). In the split-half check (`files/results/snl_check.json`), 2008-2025 gave 0.86 against a null band of 1.05-1.28 (p = 0.001), but 1990-2007 gave 0.68, inside its null band of 0.61-0.93 (p = 0.32). The seasonal pumping cycle moves the null band away from 1, so the evidence for a non-seasonal effect is weak. This is one of about 90 per-reservoir tests. We do not claim a reservoir effect at San Luis.

### 4.3 Power

| Injected odds ratio per 10 m (level anomaly) | 1.03 | 1.05 | 1.10 | 1.20 | 1/1.05 | 1/1.10 | 1/1.20 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Power | 0.17 | 0.25 | 0.86 | 1.00 | 0.27 | 0.81 | 1.00 |

The binomial simulation has no extra-binomial noise. Real power can be a little lower.

### 4.4 Sensitivity

![Sensitivity of pooled odds ratios](files/figures/fig4_sensitivity.png)

| Variant | Level anomaly OR (p) | Monthly change OR (p) | 6-month lag OR (p) |
| --- | --- | --- | --- |
| Primary (M ≥ 1.5, near 10 km, declustered) | 0.991 (0.85) | 0.872 (0.17) | 1.028 (0.37) |
| M ≥ 2.0 (622 near events) | 0.997 (0.94) | 0.871 (0.47) | 1.008 (0.81) |
| No declustering | 1.017 (0.66) | 0.692 (0.13) | 1.056 (0.48) |
| Near 5 km | 0.958 (0.46) | 0.877 (0.11) | 1.017 (0.77) |
| Near 15 km, control 25-45 km | 0.979 (0.52) | 0.950 (0.89) | 0.990 (0.73) |
| 2000-2025 only | 0.996 (0.99) | 0.888 (0.29) | 1.032 (0.38) |
| Depth 8 km or less | 0.982 (0.85) | 0.777 (0.014) | 1.015 (0.67) |
| 7 reservoirs with range ≥ 40 m | 0.998 (0.92) | 0.870 (0.09) | 1.037 (0.23) |
| Reservoir × 5-year block effects (500 replicates; run stopped after 5 of 8 models) | 0.954 (0.22) | 0.900 (0.38) | 1.001 (0.92) |

The monthly-change slope is below 1 in all variants (0.69-0.95), and it is nominally significant only for shallow events (p = 0.014). The null bands for this covariate are also below 1, because the seasonal cycle of filling and drawdown is kept by the null. With about 40 variant tests, one p of 0.014 is not strong evidence. A real but small decrease of the near-zone share during fast filling (or increase during drawdown) remains possible, and San Luis contributes most to it.

### 4.5 Example series

`files/figures/fig3_timeseries.png` shows the monthly level and the annual near-zone share for Shasta, Isabella and San Luis. The 2014-2015 and 2021-2022 drawdowns (Shasta 50 m below full) did not change the annual near-zone share beyond the binomial scatter.

## 5. Interpretation

Ten metres of water applies about 0.1 MPa at the surface. Below a reservoir of 1-3 km width, the stress change at 3-10 km depth is a fraction of this value. The result shows that, in 1990-2025, these interannual loads, loading rates and delayed loads did not change the local small-earthquake share at 22 California reservoirs by 10% or more per 10 m on average, and that no single reservoir with sufficient data had a clear, replicated effect. This agrees with the small size of regional hydrological modulation in California (Johnson et al. 2017) and with the null campaign results for GRACE loads. It does not apply to first filling: all 22 reservoirs were filled before 1990.

## 6. Limitations

* The data are sparse: most reservoirs have fewer than 100 near-zone events. Only Isabella, Shasta, San Luis, Lake Sonoma, Indian Valley and Oroville have more than 80.
* Magnitude completeness in the Sierra foothills is about M 1.5-2.2 and changes with time. The near/control share removes common changes, but not changes that affect only one zone.
* The reservoir geometry is approximate (NHDPlus V2 medium resolution; Eastman and Hensley as dam points; New Melones as the old lake). Errors of a few kilometres move events between the near zone and the 10-20 km gap but not into the control ring.
* We did not use focal mechanisms or compute Coulomb stress. A model with one sign for all reservoirs can miss effects of opposite sign; the any-sign Q test reduces but does not remove this limit.
* CDEC data are provisional real-time data. Our QC removed clear errors; small errors can remain.
* Gardner-Knopoff windows (Gardner and Knopoff 1974, doi:10.1785/BSSA0640051363) are simple. The test without declustering gave the same result.
* We did not test Lake Mead, Lake Powell, or reservoirs outside California.

## 7. What remains open

* A Coulomb-stress version with reservoir footprints and regional focal mechanisms, so that each event has an expected sign.
* An independent test of the San Luis fill-rate candidate with a relocated catalog (for example the NCEDC double-difference catalog) and daily pumping data.
* Lake Mead (about 50 m of unloading in 2000-2022) and Lake Powell with the Nevada and Utah networks.
* Reservoirs with first filling after 1990 (for example Diamond Valley Lake, 1999-2003).

## 8. Reproduce

All code is in `files/code/`. It writes only to a scratch directory that you give.

```bash
S=scratch; mkdir -p $S
bash files/code/fetch_cdec.sh $S/cdec                       # CDEC daily elevation + storage (98 small CSV)
python files/code/levels.py $S/cdec $S/levels_monthly.csv   # QC + monthly means (+ _qc.csv log)
# station metadata: files/provenance/cdec_station_metadata.json (copy to $S/res_meta.json)
python files/code/select.py $S/levels_monthly.csv $S/res_meta.json $S/selected.json
python -u files/code/fetch_comcat.py $S/comcat $S/selected.json          # ComCat, 60 km, 5-year chunks
python -u files/code/fetch_comcat_yearly.py $S/comcat $S/selected.json INV:2000 INV:2005 INV:2010 WRS:2000 WRS:2005 WRS:2010
bash files/code/fetch_nhd.sh $S/selected.json $S/nhd; bash files/code/fetch_nhd_names.sh $S/nhdname
python files/code/build_events.py $S/comcat $S/nhd $S/selected.json $S/out   # distances, Geysers mask, declustering
bash files/code/run_all.sh $S/out $S/levels_monthly.csv         # primary, per-reservoir, power
bash files/code/run_sensitivity.sh $S/out $S/levels_monthly.csv # sensitivity variants
bash files/code/run_extra.sh $S/out $S/levels_monthly.csv       # shallow and large-range variants
python files/code/snl_check.py $S/out/monthly_m15.csv $S/out/snl_check.json 1000
python files/code/figures.py $S/out $S/figures
```

Python 3.12 with numpy, pandas, scipy, shapely 2.2, pyproj 3.8 and matplotlib. The Python downloads force IPv4 because IPv6 routes hung on the campaign host. A new retrieval can differ slightly because ComCat and CDEC revise records; compare with `files/provenance/raw_input_sha256.txt`.

Bundled outputs (`files/results/`): all statistics JSON files, per-reservoir table, heterogeneity and power tables, the San Luis check, monthly near/control counts (`monthly_counts_m15.csv`, counts only), and the ComCat events within 45 km of a selected reservoir with distances and cluster labels (`comcat_events_within45km.csv.gz`, USGS public domain). The CDEC level series are not bundled; see `files/NOTICE_external_data.md`.

Data credit: U.S. Geological Survey ANSS ComCat and the contributing networks (NCSN, BK, SCSN, NN); California Department of Water Resources CDEC; US EPA / USGS NHDPlus V2.
