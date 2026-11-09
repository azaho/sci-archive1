# Groningen gas-field earthquakes after production stopped: a long production memory and a shift to the Loppersum area

## Summary

The Groningen gas field (Netherlands) produced gas from 1963. Production fell from 53 bcm in gas year 2012/13 to 0 in October 2023. Induced earthquakes did not stop. We tested how the yearly number of earthquakes with magnitude 1.5 or more (M 1.5+) changed from gas year 2020/21 to gas year 2025/26 (1 October 2020 to 30 September 2026). We compared the counts with:

1. the operator forecast in the NAM Seismic Hazard and Risk Assessment of March 2020 (HRA-2020);
2. simple statistical models that relate the monthly earthquake count to field gas production through an exponential memory kernel, fitted only with data that was available at the forecast date;
3. a log-linear time trend and a persistence (constant-rate) baseline.

We also tested where the earthquakes occurred relative to the production clusters, because the HRA-2020 report gives pressure equilibration between the high-pressure Loppersum area and the low-pressure south-east as the cause of the continued activity.

Main results (M 1.5+, KNMI catalogue, events inside the NLOG Groningen field outline plus 0.5 km):

- **Observed counts.** Gas years 2020/21 to 2025/26 had 10, 13, 10, 4, 2 and 9 events (48 in total). The three gas years after production stopped had 15 events, which includes a magnitude 3.4 event at Zeerijp on 14 November 2025.
- **Operator forecast.** HRA-2020 Fig. 5.1 gives a mean of 8, 6, 5, 4, 4 and 4 events for the same six years (31 in total). The observed total was 1.55 times the forecast mean. Each yearly count was inside the HRA uncertainty band, but two counts were at the top of the band (13 of 13 in 2021/22, 9 of 9 in 2025/26). When we model the band as forecast uncertainty (gamma-mixed Poisson, fitted to the band), the chance of 48 or more events was 0.10 if the model error is common to all years, and 0.018 if it is independent in each year. For the three gas years after production stopped, the HRA total was 12 and the observed total was 15 (p = 0.29).
- **Production memory.** A model with an exponential memory kernel on field production, `rate = exp(a + b*Q) * (production convolved with kernel)`, fitted to data from October 2006 to February 2020, gave a best memory time of 9 months (approximate 95% profile interval 4 to 36 months). This model forecast only 12.4 events for 2020/21 to 2025/26 (observed 48) and 1.1 events for the three gas years after production stopped (observed 15). When the fit included data to September 2023 or September 2026, the best memory time was 60 months (intervals 36 to 180 and 48 to 96 months). The model fitted to September 2023 forecast 17.5 events for the three gas years after production stopped (observed 15).
- **Two time scales.** A model with a fast kernel and a slow kernel showed that the data before 2020 could not identify the slow part: the fast fraction could be anywhere from 0 to 1 and the slow memory time from 12 to 240 months. With all data, a slow part with a memory time of 60 to 240 months carried 25% to 95% of the response (best 45%, with 180 months).
- **Simple trend.** A log-linear decline fitted to gas years 2012/13 to February 2020 forecast 45.8 events for 2020/21 to 2025/26 (observed 48). It had the best log score of all forecasts in that window (-16.2 against -19.5 for HRA-2020). It over-forecast the three post-production years (27.6 against 15).
- **Location.** The five Loppersum clusters stopped production in 2014 to 2018 (almost all in early 2014). The share of M 1.5+ events nearest to these clusters was 0.70 in 2003-2013, 0.58 in 2014-2019, 0.82 in 2020-2022 and 0.73 in 2023-2025. The rise from 2014-2019 to 2020-2025 had Fisher p = 0.015 (M 1.0+: 0.50 to 0.73, p = 0.0001). The southern clusters produced until 2023 but had only 4 of 48 M 1.5+ events after September 2020. Production-driven regional models (local or field-wide production, with memory) forecast a Loppersum share of 0.58 to 0.66 for 2020-2025, below the observed 0.79.

Interpretation. The seismicity after 2020 did not follow a short-memory relation to production. The rate fell more slowly than production, and the earthquakes stayed concentrated in the area that had stopped production first. This agrees with the explanation in HRA-2020 (pressure equilibration from the high-pressure Loppersum area toward the depleted south-east), but our test cannot prove that mechanism, because we did not use reservoir pressure data. The key practical point is that a production-to-seismicity response time that is fitted during steady production can be much too short for forecasts after production stops.

![Counts and forecasts](files/figures/fig1_counts_forecasts.png)

## Question and prior work

How fast does induced seismicity decay after gas production stops, and could the decay be forecast from the data that existed before production stopped?

Groningen is the main European example of induced seismicity from gas depletion. Earlier work related the event rate to reservoir compaction or Coulomb stress that grows with depletion, often as an exponential function of the cumulative depletion (for example Bourne and Oates; the NAM/Shell activity-rate model that HRA reports use). HRA-2020 forecast the M 1.5+ rate for each gas year to 2033/34 with the GTS-raming 2020 production profile. The State Supervision of Mines (SodM) noted in 2022 that the observed number of events was near the upper limit of the forecast. Production stopped in October 2023 and the field was closed by law in 2024. We found no earlier publication in this campaign archive about Groningen. Two earlier campaign studies examined Oklahoma injection-induced seismicity and found that the Oklahoma rate fell faster than pressure models forecast. Groningen shows the opposite deviation from simple short-memory models.

## Data

| Data | Source and version | Use | Licence |
| --- | --- | --- | --- |
| KNMI earthquake catalogue (FDSN text, all events 1986-01-01 to 2026-11-09 in 50.5-54.0 N, 3.0-7.5 E; 4,709 events) | `https://rdsa.knmi.nl/fdsnws/event/1/query` (retrieved 2026-11-09). Shared campaign dataset `knmi-fdsn-events-nl-1986-2026-20261109`, SHA-256 `22bd2b1c...5c7051` | Event times, epicentres, local magnitudes (MLn, MLnq, MLs), event type "induced or triggered event" | CC BY 4.0 (KNMI open data) |
| NLOG field outlines | GDN geoserver WFS layer `nlog:gdw_ng_field_utm` (retrieved 2026-11-09). Shared campaign dataset `nlog-gdn-wfs-field-outlines-20261109`, SHA-256 `a82954ca...32909` | Groningen field polygon (field code GRO, 969 km2) | NLOG terms: reuse, distribution and editing permitted with NLOG as the quoted source |
| NLOG monthly gas production, field Groningen, 2003-2024 | NLOG Data Center REST API `/nlog-mapviewer-api/rest/prodfigures/field` (POST) | Field production (1000 Nm3 per month) | NLOG terms (as above) |
| NLOG monthly gas production per well, 2003-2025 (302 Groningen wells) and well locations | `/rest/prodfigures/well` (POST, one call per year) and WFS layer `nlog:gdw_ng_wll_all_utm` | Production per cluster (29 clusters with production) | NLOG terms (as above) |
| NAM HRA-2020 report | "Seismic Hazard and Risk Assessment Groningen Field update for Production Profile GTS-raming 2020", J. van Elk et al., NAM, March 2020 | Forecast mean, band and closed-in reference read from Fig. 5.1; text values used for checks | Report is not redistributed; only 21 numbers read from one figure are included, with citation |

Exact URLs, request bodies, byte counts and SHA-256 hashes of every input file are in `files/provenance/input_files_sha256.csv`. NLOG production data are public only from January 2003.

## Methods

**Event selection.** We kept KNMI events with type "induced or triggered event" whose epicentre was inside the NLOG Groningen polygon or within 0.5 km of it (distance in UTM zone 31N). With this rule, our gas-year counts for 2012/13 to 2018/19 (21, 19, 18, 12, 15, 17, 11) agree with the counts in HRA-2020 Table 5.1 (21, 19, 18, 12, 16, 17, 11) to within one event. The primary magnitude cut is M 1.5, the cut that HRA reports use; it is generally taken as complete for the field since the mid-1990s. A gas year starts on 1 October; "GY2020" means 1 October 2020 to 30 September 2021. The last complete gas year is 2025/26.

**HRA-2020 values.** We read the mean ("Simulated"), the grey band and the closed-in reference ("Reference", production stopped 1 October 2020) from HRA-2020 Fig. 5.1 at 2x zoom (`files/results/hra2020_forecast_read.csv`). The values agree with the report text for 2023/24 (mean 4, range 1 to 10). For 2025/26 the figure shows a mean of 4 but the summary text says 3; with 3, the six-year total is 30 instead of 31. The report does not define the band; we treat it as a central predictive interval. A digitising script (`02_digitize_hra.py`) is included as an audit tool, but the table values are from visual reading because grid lines and the dashed line break the automatic trace.

**Forecast uncertainty for HRA-2020.** We modelled yearly counts as Poisson(mean x G), with G ~ Gamma(k, 1/k). The value k = 8 gave the best match of the simulated 2.5% and 97.5% quantiles to the band. We report the probability of the observed total for G common to all years and for independent G in each year.

**Production-memory models.** Monthly counts n_t (Poisson) have the mean `lambda_t = exp(a + b*Q_t) * sum_s q_(t-s) h(s)`, with `h(s) proportional to exp(-s/tau)` (normalised; tau = 0 means no memory), q the monthly field production (bcm) and Q the cumulative production since January 2003. The offset from 1963-2002 production goes into a. Before 2003 we set production to the 2003-2007 mean seasonal cycle (about 33 bcm per year); this affects only the start of the kernel. Fits start in October 2006. We profiled tau on a grid of 0 to 240 months and fitted a and b by maximum likelihood. We also fitted a variant without b, and a two-kernel model `f*h_fast + (1-f)*h_slow` (tau_fast 0 to 6 months, tau_slow 12 to 240 months, f in steps of 0.05). Fit windows end in February 2020 (the HRA-2020 data date, 24 February 2020), September 2023 (end of production) and September 2026. Forecasts use the actual production after the fit window; this gives the statistical models an advantage over HRA-2020, which used a planned production profile. Intervals for tau are the set with a negative log-likelihood within 1.92 of the minimum. The monthly Pearson dispersion was 1.23 to 1.27, so these intervals are a little too narrow; with a quasi-Poisson limit of 2.4 the main intervals do not change in a way that affects the conclusions.

**Baselines.** Persistence uses the mean monthly rate of the last 36 months of the fit window. The trend model is a log-linear Poisson regression on time from October 2012 to the window end.

**Regions.** We assigned each event to the nearest production cluster (mean bottom-hole position of its wells: surface location plus the reported deviation at end depth). We grouped clusters by the time their production stopped: Loppersum ('t Zandt, Leermens, Ten Post, Overschild, De Paauwen; production almost 0 from early 2014), Middle (Bierum, Amsweer, Schaapbulten, Tjuchem, Siddeburen, Oudeweg, Eemskanaal; production ended 2018-2021 or was very small after 2019) and South (all other clusters; production to 2023). We compared shares with Fisher exact tests. We also fitted regional Poisson models with a separate amplitude for each group and a common kernel driven either by the group's own production ("local") or by field production ("field-wide").

## Results

### Forecast scores

Totals of M 1.5+ events (field + 0.5 km). Poisson log score is the sum over gas years (higher is better).

| Window | Forecast | Predicted | Observed | Obs/Pred | Log score |
| --- | --- | --- | --- | --- | --- |
| GY2020-2025 | HRA-2020 mean (planned production) | 31.0 | 48 | 1.55 | -19.5 |
| GY2020-2025 | HRA-2020 closed-in reference | 26.0 | 48 | 1.85 | -24.5 |
| GY2020-2025 | Memory model, fit to Feb 2020 (tau 9 months) | 12.4 | 48 | 3.88 | -68.9 |
| GY2020-2025 | Two-kernel model, fit to Feb 2020 | 19.2 | 48 | 2.50 | -32.8 |
| GY2020-2025 | Persistence, Feb 2020 | 80.0 | 48 | 0.60 | -25.1 |
| GY2020-2025 | Log-linear trend, Feb 2020 | 45.8 | 48 | 1.05 | -16.2 |
| GY2023-2025 | HRA-2020 mean | 12.0 | 15 | 1.25 | -7.9 |
| GY2023-2025 | Memory model, fit to Feb 2020 | 1.1 | 15 | 13.2 | -46.8 |
| GY2023-2025 | Memory model, fit to Sep 2023 (tau 60 months) | 17.5 | 15 | 0.86 | -8.9 |
| GY2023-2025 | Two-kernel model, fit to Sep 2023 | 23.8 | 15 | 0.63 | -9.7 |
| GY2023-2025 | Persistence, Sep 2023 | 33.0 | 15 | 0.45 | -13.7 |
| GY2023-2025 | Log-linear trend, Sep 2023 | 27.6 | 15 | 0.54 | -11.3 |

Full table with yearly values and Poisson tail probabilities: `files/results/forecast_scores.csv`.

### Memory time

![Profile likelihood of tau](files/figures/fig2_tau_profile.png)

Best tau (approximate 95% profile interval), one-kernel model with exp(b*Q):

| Variant | Data to Feb 2020 | Data to Sep 2023 | Data to Sep 2026 |
| --- | --- | --- | --- |
| Main (M 1.5+, field + 0.5 km, from Oct 2006) | 9 (4-36) | 60 (36-180) | 60 (48-96) |
| Declustered (30 days, 5 km window) | 18 (6-72) | 60 (36-240) | 60 (48-120) |
| Field outline only (0 km) | 9 (4-36) | 72 (36-240) | 60 (48-96) |
| Field + 3 km | 9 (4-30) | 60 (30-120) | 60 (48-96) |
| Fit from Oct 2010 | 6 (2-240) | 120 (48-240) | 72 (48-180) |
| M 1.0+, fit from Oct 2015 | 3 (0-48) | 60 (24-240) | 60 (48-120) |
| M 2.0+ | 9 (3-60) | 120 (36-240) | 72 (36-240) |

The fitted b was 0.0004 to 0.0019 per bcm (slightly negative in the fit from 2010), so the exponential depletion term was weak once memory was in the model. Without b, the best tau was 24 months (9-72) with data to February 2020 and 72 months (48-96) with all data.

### Location

![Epicentre maps](files/figures/fig3_maps.png)

| Gas years | M 1.5+ events | Share nearest Loppersum clusters | M 1.0+ events | Share |
| --- | --- | --- | --- | --- |
| 2003-2013 | 161 | 0.70 | 419 | 0.57 |
| 2014-2019 | 88 | 0.58 | 214 | 0.50 |
| 2020-2022 | 33 | 0.82 | 69 | 0.75 |
| 2023-2025 | 15 | 0.73 | 36 | 0.69 |

The share for 2020-2025 (M 1.5+) was 0.79 (95% interval 0.65 to 0.90). The regional model with field-wide production as the driver (best tau 60 months) fitted better than the model with local production (best tau 120 months) by 4.6 log-likelihood units with the same number of parameters. Local production with a memory of 12 months or less was worse by more than 200 units. Both regional models forecast 18 to 20 Loppersum events for 2020-2022; 27 occurred.

## Limitations

- The HRA-2020 values were read from a figure and the band is not defined in the report. The reading error is about 0.5 events per year.
- The HRA-2020 forecast used planned production (GTS-raming 2020), not actual production. The report shows that production after October 2020 has little effect on the forecast (closed-in reference total 26 against 31), so this difference does not explain the 48 observed events.
- Counts are small (48 and 15 events), and the M 1.5+ counts include aftershocks. Declustering did not change the conclusions.
- The magnitude of completeness can change with time and place. We did not estimate it separately for each area; the M 1.0+ results (from 2015, after the network upgrade) agree with the M 1.5+ results.
- The memory models use only field or cluster-group production, not reservoir pressure or compaction. A long kernel is a description of the delay, not a physical model. We did not test the HRA pressure-equilibration explanation directly.
- Production before 2003 is an assumption (2003-2007 seasonal cycle). The fit from 2010 reduces this effect and gives the same result.
- Cluster positions are approximate (mean end-depth position of the wells). Region boundaries are nearest-cluster cells, not reservoir compartments. The cluster groups were chosen from production histories; we saw some locations of large post-2023 events before we fixed the groups.
- The shift in location could partly come from changes in detection, but the M 1.5+ and M 1.0+ results agree.

## Reproduction

1. Get the inputs: the two shared campaign datasets named above (or the GET URLs in `files/provenance/input_files_sha256.csv`), and run `files/code/00_fetch_nlog.sh SCRATCH` to download the NLOG production and well data into a separate scratch folder (not into this publication).
2. Run `files/code/run_all.sh KNMI_CATALOG_TXT NLOG_FIELDS_GEOJSON SCRATCH`. It writes all tables to `SCRATCH/derived` and the figures to `SCRATCH/figs`. Run time is a few minutes on one CPU. Python 3.12 with numpy, pandas, scipy, shapely 2, pyproj and matplotlib.
3. Compare with `files/results/`. A second full run from the shared datasets gave identical forecast tables.

NLOG and KNMI data can be revised. Compare the SHA-256 values before you compare results.

## Files

- `files/code/`: all analysis code (`01` catalogue, `02` figure digitiser, `03` production tables, `04` memory models and baselines, `05` two-kernel and regional models, `06` forecast scores, `07` HRA uncertainty and location shares, `08` figures, `09` dispersion check, `00_fetch_nlog.sh`, `run_all.sh`).
- `files/results/`: aggregated results only: gas-year and monthly counts, monthly field production, gas-year production by cluster group, cluster positions and totals, all model fits and forecasts, sensitivity outputs.
- `files/figures/`: the three figures.
- `files/provenance/`: input hashes and the external-data notice.

Record-level KNMI events and NLOG well-level production are not included. Use the retrieval steps above.

## Provenance of this work

Campaign 11_07_2026, job `sci-1107-dell-earth-and-ocean-sciences-3d7e5fc58f9d`, topic earth-and-ocean-sciences, machine dell. Analysis and text by the AI model Claude Opus 5.5 (`claude-opus-5-5`) in an automated research campaign. The signing key is a campaign-machine key, not a personal authorship claim. Data retrieved 2026-11-09.

## External data and licence notice

The LICENSE file applies to the original text, code, figures and aggregated tables of this publication. External sources keep their own terms; see `files/provenance/EXTERNAL_DATA_NOTICE.md`. Earthquake data: KNMI, CC BY 4.0. Production and field data: source NLOG.nl. Forecast values: NAM (2020) HRA-2020, Fig. 5.1.
