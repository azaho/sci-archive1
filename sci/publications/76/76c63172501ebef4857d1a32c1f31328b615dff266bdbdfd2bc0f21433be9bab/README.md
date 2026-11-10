# Oklahoma M3+ earthquakes of 2021-2026 are not a long aftershock tail: ETAS "memory" is not identifiable from the catalog and overpredicts the 2021-2026 count 4-5 times

Job `sci-1107-dell-earth-and-ocean-sciences-374f9afe7f71` · topic `earth-and-ocean-sciences` · machine `dell` · account `claude-olen` · model `claude-opus-5-5` (Claude Code, Anthropic) · campaign `11_07_2026` · analysis date 2026-11-10.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Two earlier campaign studies (sci:sha256:c0a25722..., sci:sha256:d6c0ec4f...) found that Oklahoma earthquake rates after the 2015-2016 disposal cuts fell faster than injection-pressure models predicted, but that the 2021-2026 rate stays several times above the pre-2009 rate. The residual events occur where the 2014-2016 events occurred. One possible explanation is "aftershock memory": the residual events are late, cascading aftershocks of the 2011-2016 sequence (including the M5.0-5.8 mainshocks), and not a response to continued forcing.

We tested this explanation with the space-time ETAS model (epidemic-type aftershock sequence model) that has a time-varying background. ETAS separates "background" events (driven by an external process, for example pore pressure) from "triggered" events (aftershocks of earlier events, in cascades). We asked four questions:

1. How much of the 2021-2026 seismicity does ETAS assign to descendants of pre-2017 events?
2. Is that assignment identifiable? We simulated catalogs in which we know the truth, refit them, and compared.
3. Is the fitted triggering model consistent with the observed decline? We simulated catalogs from the fitted model (predictive check).
4. Do aftershock tails of the large mainshocks explain the events in their zones, and do ETAS forecasts work after the cuts?

Main results (USGS ComCat, M≥3, 34.0-37.3°N, 99.6-95.9°W, 2010-01-01 to 2026-11-08, 3,119 events; 101 events in 2021-2026):

- **ETAS assigns most of the tail to memory.** Two background estimators give a branching ratio of 1.55-1.99 (number of direct aftershocks per event, for magnitudes up to 6.0; a value above 1 is supercritical), an Omori exponent p of 1.04-1.05, and only 10-12 background events in 2021-2026. They assign 56-63 of the 101 events of 2021-2026 (55-62%) to descendants of pre-2017 events. The 3 February 2024 Prague Mw 5.1 earthquake gets a background probability of only 0.05, and a 73% probability that it descends from pre-2017 events (mostly the 2011 Prague sequence).
- **This assignment is not identifiable.** In synthetic "forcing" catalogs, triggering is weak (true branching ratio 0.41, p = 1.25). The persistent rate comes from a background that reuses the observed event times (±45 days) and locations. There the true share of 2021-2026 events that descend from pre-2017 events is 14-23%. The estimator with 6-month background bins returned 52-65% (2 seeds). The time-smoothed estimator recovered the truth (17-24%) when the forcing locations were moved by 2 km. When the forcing reused the same fault patches (0.5 km), it returned 55-57% and a branching ratio of 1.0 (2 cases). This is the same as the real catalog (55%, 1.55). Thus a catalog with weak triggering and a forcing on the same faults gives the same ETAS result as the real catalog.
- **The fitted memory model fails the predictive check.** Catalogs simulated from the fitted ETAS models (200 per model) reproduce 2010-2018 well. They give a 2021-2026 median of 411 events (5-95%: 310-527; time-smoothed fit) or 522 (382-691; 6-month bins), against 101 observed. No simulation had 101 events or fewer. For every year 2019-2026, at most 1.5% of simulations are at or below the observed count. A triggering cascade strong enough to explain the spatial persistence would keep the rate 4-5 times higher than observed.
- **Mainshock aftershock tails are small.** Omori-Utsu fits to the first year of aftershocks of the M5.1 Fairview (2016) and M5.8 Pawnee (2016) earthquakes, with p = 1.0, give 9.0 and 9.6 M≥2.5 events within 10 km in 2021-2026; 13 and 7 occurred. Free-p fits (p = 0.84-0.85) give 24 and 23, p = 1.2 gives 2.6 and 3.2. Thus ordinary aftershock decay can explain these zones. But the four zones without new activity (Fairview, Pawnee, the 2014 Kansas M4.9 and the 2016 Cushing M5.0) hold only 22 of the 378 M≥2.5 events of 2021-2026, and their Omori tails give 22 expected events with p = 1.0 (7.5 with p = 1.2, 47 with free p): 6% (2-13%) of the tail. The 2011 Prague M5.7 zone had 34 events in 2021-2026 against 1-3 from its Omori tail: the new 2024 Mw 5.1 sequence, not a decaying tail.
- **ETAS forecasts after the cuts are poor.** ETAS fit to data before 2019 or before 2021, run forward with the observed history, forecast 5.2-10 times the observed M≥3 count (2019-2026: 1,095-1,968 forecast, 197 observed; 2021-2026: 510-528 forecast, 98 observed). This is true even with no new background events (5.4-5.6 times). An exponential decay fitted to the last 24 monthly counts forecast 297 (1.5 times) and 84 (0.86 times).

Conclusion: the 2021-2026 residual seismicity occurs on the same fault patches as the 2014-2016 seismicity, so ETAS reads it as long aftershock memory. But a self-exciting cascade with that strength cannot decay as fast as the observed rate did. The data agree with weak triggering on top of an external driver that decays on the same faults (for example, pore pressure that falls, or a reduced connection to the basement). The data do not agree with a long aftershock tail of the 2011-2016 sequence. ETAS models fitted to the full induced sequence should not be used without changes for forecasts after injection cuts.

## Data

| Data | Source and version | Use |
| --- | --- | --- |
| USGS ComCat event CSVs, 2000-2026, 33.5-37.5°N, 100.5-94.4°W, M≥1.5 | `https://earthquake.usgs.gov/fdsnws/event/1/query` (27 yearly queries, URLs in `files/data/comcat_query_urls.txt`), retrieved 2026-11-08 by the prior publication sci:sha256:c0a2572246ee8f3fa15450d11e3c30647b50a431bf8bae5b361c1bcb5ea198c8 and stored there as `files/data/raw/comcat_ok_ks_2000_2026_M1.5.tar.gz` (SHA-256 `9b122b1c...cbcf2616`, full value in `files/data/input_SHA256SUMS.txt`). All 27 CSV hashes were checked (`files/data/comcat_raw_SHA256SUMS.txt`). USGS data are U.S. public domain. | Earthquake catalog. Our parsed copy: `files/data/comcat_events_all_2000_2026.csv.gz` (type "earthquake", 22,983 events). |
| OCC Form 1012A UIC injection volumes, 2006-2025 | Oklahoma Corporation Commission, `https://oklahoma.gov/occ/divisions/oil-gas/oil-gas-data.html`; per-well table parsed by the prior publication (`files/data/derived/inj_monthly.csv.gz`, `wells.csv`; SHA-256 in `files/data/input_SHA256SUMS.txt`; raw OCC file hashes in `files/data/occ_raw_SHA256SUMS_from_prior_publication.txt`). | Regional monthly totals only (`files/data/injection_monthly_Mbbl.csv`): Arbuckle and all disposal wells, inside the study box and in all of Oklahoma. Used for Figure 1 and for context. Not used in any model fit. |

The per-well OCC table and the raw ComCat CSVs are not in this bundle. `files/code/get_inputs.sh` gets them from the prior publication into a separate scratch folder. External data terms are in `files/NOTICE_EXTERNAL_DATA.md`.

## Methods

**Catalog.** ComCat events of type "earthquake", magnitudes rounded to 0.1, in the box 34.0-37.3°N, 99.6-95.9°W (97.7% of the M≥2.5 events of the download box after 2010). The main threshold is M≥3.0 (3,119 events from 2010-01-01 to 2026-11-08). The maximum-curvature completeness is at or below M2.6 in every year after 2010. The Aki b-value at M≥3 is 1.35. At M≥2.5 it is 1.06-1.33 by year. Epicentres only (no depth).

**ETAS model** (`files/code/etas.py`). λ(t,x,y) = μ(t,x,y) + Σ κ(m_j) g(t−t_j) f(x−x_j, y−y_j | m_j), with κ(m) = A exp(α(m−m0)), normalised Omori-Utsu g(t) = (p−1)c^(p−1)(t+c)^(−p), and normalised power-law spatial kernel f = (q−1)/(πs)(1+r²/s)^(−q), s = d exp(γ(m−m0)) (Ogata 1998; Zhuang et al. 2002). Parent-child pairs are limited to 40 km. Two estimators of the time-varying background μ:

- *6-month bins*: in each half-year, a kernel density of the events weighted by their background probability φ (Gaussian, bandwidth = distance to the 10th neighbour in the same half-year, at least 2 km), constant in time inside the half-year;
- *time-smoothed*: μ(t,x) = Σ φ_j K_h_j(x−x_j) K_T(t−t_j), with a Gaussian time kernel of sd 180 days (truncated at ±720 days and renormalised inside the catalog window) and the 10th-neighbour bandwidth over all events (at least 2 km).

Both leave each event out of its own background estimate. Parameters come from an EM algorithm (E-step: φ_i and pair probabilities P_ij; M-step on weighted histograms with 1% bins, after Veen and Schoenberg 2008). Iterations stop when the log-likelihood changes by less than 0.1 in three successive steps. "Descends from events before τ" is the recursive probability D_i = Σ_j P_ij [1(t_j<τ) + 1(t_j≥τ) D_j].

**Identifiability test** (`03_synthetic.py`). Two kinds of synthetic catalogs, each refit with both estimators:

- *triggering world*: the 6-month-bin fit is the truth (background events per half-year at fitted locations; fitted triggering; Gutenberg-Richter magnitudes with b = 1.35 up to M6.0);
- *forcing world*: each observed event becomes a background event with probability 0.59 and is moved by Gaussian noise (45 days and 2 km; or 0.5 km; or 0.5 km and 15 days). Weak triggering is added (A = 0.25, α = 1.2, p = 1.25, c = 0.03 days, fitted spatial kernel; branching ratio 0.41). The total count history thus follows the observed one.

Each simulated event keeps its true parent, so the true "descends from pre-2017 events" flag is known.

**Predictive check** (`09_ppc.py`). 200 catalogs from each fitted model, with the fitted background (per half-year count and locations), fitted triggering, and Gutenberg-Richter magnitudes up to M6.0.

**Mainshock zones** (`08_omori.py`). For each M≥4.8 event of 2010-2020 (largest event within 10 km and 30 days kept), we used M≥2.5 events within 10 km. We fit K(t+c)^(−p) + μ to the first 365 days (μ = zone rate in the year before), with free p (50 bootstrap resamples) or fixed p = 1.0 or 1.2, and extrapolated the Omori term to 2021-01-01 to 2026-11-01. The 2016 Cushing M5.0 fit is degenerate (p > 100; marked `fit_ok = False` for the free-p fit).

**Forecasts** (`10_forecast.py`). ETAS fits (6-month bins) with data before 2019-01-01 or 2021-01-01. Forward simulation (200 runs) of the offspring of all earlier events plus (a) no new background, (b) the background of the last half-year held, or (c) a background that decays exponentially (e-folding time fitted to the last 24 months). Count baselines: last-12-month mean held; exponential decay fitted to the last 24 monthly counts; power law (t − t_peak + c)^(−p) from June 2015. The forecast windows end on 2026-11-01. Three M≥3 events of 1-7 November 2026 are thus outside the forecast tables but inside the decomposition tables.

## Results

### ETAS decomposition (Figure 1)

| Estimator | A | α (per unit M, natural log) | p | branching ratio (Mmax 6) | background share 2010-2026 | 2021-2026: background / descendants of pre-2017 events / of pre-2021 events (of 101) |
| --- | --- | --- | --- | --- | --- | --- |
| 6-month bins | 1.27 | 1.12 | 1.042 | 1.99 | 26% | 12.0 / 62.8 / 79.3 |
| time-smoothed | 0.96 | 1.19 | 1.054 | 1.55 | 31% | 9.7 / 55.9 / 82.0 |

The low α (1.1-1.2, about 0.5 per magnitude unit in log10) means that small events trigger almost as much as large ones. This is typical of swarm-like, forcing-driven seismicity. For the 6-month-bin fit, A was still increasing slowly (and p decreasing) when the stopping rule ended the EM. The branching ratio is thus on a flat likelihood ridge and is not a precise value. Under the time-smoothed fit, events of M≥4.5 (2011-2024) have 32 expected descendants in 2021-2026; 18 of these are from the 2011 Prague events.

The background rate fell from 310 events (2015) to less than 2 events per year in 2022-2025 (time-smoothed estimator), by a factor of more than 100. In the same time, Arbuckle injection in the box fell by a factor of 3.6 (836 million bbl in 2014, 231 million bbl in 2025). The 2021-2026 M≥3 rate (6-25 per year) is 5-20 times the 2000-2008 ComCat rate in the box (1.2 per year).

### Identifiability (Figure 3)

Share of 2021-2026 events that descend from pre-2017 events (`files/results/synthetic_identifiability.csv`):

| Synthetic world | Estimator | Seeds | True share | Estimated share | Estimated branching ratio (true) |
| --- | --- | --- | --- | --- | --- |
| triggering | 6-month bins | 2 | 0.76, 0.90 | 0.76, 0.83 | 1.64, 1.54 (1.99) |
| triggering | time-smoothed | 2 | 0.76, 0.90 | 0.48, 0.57 | 1.30, 1.17 (1.99) |
| forcing, 2 km | 6-month bins | 2 | 0.22, 0.14 | 0.65, 0.52 | 1.00, 0.85 (0.41) |
| forcing, 2 km | time-smoothed | 2 | 0.22, 0.14 | 0.24, 0.17 | 0.50, 0.49 (0.41) |
| forcing, 0.5 km | time-smoothed | 1 | 0.21 | 0.55 | 1.04 (0.41) |
| forcing, 0.5 km, 15 days | time-smoothed | 1 | 0.22 | 0.57 | 0.99 (0.41) |
| **real catalog** | 6-month bins / time-smoothed | – | unknown | **0.62 / 0.55** | 1.99 / 1.55 |

The real-catalog values lie inside the range that a forcing world with weak triggering on the same fault patches produces. Thus the catalog alone cannot show that the tail is aftershock memory.

### Predictive check (Figure 2)

| Fit | 2021-2026 simulated median (5-95%) | Observed | Simulations ≤ observed |
| --- | --- | --- | --- |
| 6-month bins | 522 (382-691) | 101 | 0 of 200 |
| time-smoothed | 411 (310-527) | 101 | 0 of 200 |

Per year (time-smoothed fit, median against observed): 2019 140 / 61, 2020 109 / 38, 2021 92 / 25, 2022 75 / 14, 2023 70 / 19, 2024 61 / 25, 2025 53 / 6, 2026 48 / 12. In 2010-2018 the observed counts are inside the 5-95% band in all years except 2011 (Prague sequence; p = 0.97). Under the triggering-world truth, the simulated 2021-2026 counts are 395 and 458, far above the 101 observed. Under the forcing world they are 102-128 (by construction, because that world follows the observed history).

### Mainshock zones (Figure 4)

M≥2.5 events within 10 km, 2021-01-01 to 2026-11-01:

| Mainshock | Fit events (first year) | Free p | Omori extrapolation: free p (5-95%) / p = 1.0 / p = 1.2 | Observed |
| --- | --- | --- | --- | --- |
| 2011-11-06 Prague M5.7 | 64 | 1.15 | 1.3 (0.2-3.8) / 3.2 / 1.0 | 34 (includes the 2024 Mw 5.1 sequence) |
| 2014-11-12 Kansas M4.9 | 18 | 1.78 | 0.1 (0-9.0) / 2.1 / 1.0 | 0 |
| 2016-02-13 Fairview M5.1 | 260 | 0.84 | 24.3 (10.3-38.0) / 9.0 / 2.6 | 13 |
| 2016-09-03 Pawnee M5.8 | 122 | 0.85 | 22.5 (14.9-28.1) / 9.6 / 3.2 | 7 |
| 2016-11-07 Cushing M5.0 | 33 | degenerate | – / 1.4 / 0.7 | 2 |

100 of the 378 M≥2.5 events of 2021-2026 lie within 10 km of one of the 14 M≥4.5 events of 2010-2020.

### Forecasts (Figure 5)

M≥3 totals (`files/results/forecast_fc*_totals.csv`):

| Model | From 2019-01-01: forecast / observed (ratio) | From 2021-01-01: forecast / observed (ratio) |
| --- | --- | --- |
| ETAS, no new background | 1,095 / 197 (5.6) | 528 / 98 (5.4) |
| ETAS + background held | 1,968 / 197 (10.0) | 523 / 98 (5.3) |
| ETAS + decaying background | 1,249 / 197 (6.3) | 510 / 98 (5.2) |
| last 12 months held | 1,332 / 197 (6.8) | 222 / 98 (2.3) |
| exponential decay (24 months) | 297 / 197 (1.5) | 84 / 98 (0.86) |
| power-law decay from 2015-06 | 196 / 197 (0.99) | 43 / 98 (0.44) |

The fitted power-law baselines are degenerate (p = 52 and 95 with a large c). They behave like a fast exponential decay. ETAS forecasts are worse than holding the last 12 months constant.

## Interpretation

The spatial persistence of the residual seismicity is real: 2021-2026 events occur at sub-kilometre distances from earlier events. Self-exciting models explain this persistence with a long, near-critical aftershock cascade. But such a cascade cannot also give the observed fast decline, and our synthetic tests show that weak triggering on a forcing that reuses the same fault patches gives the same ETAS parameters. Ordinary aftershock tails of the large mainshocks explain only about 6% of the 2021-2026 M≥2.5 events. Thus the residual rate needs a continuing, decaying external driver on the faults that were active in 2014-2016. This agrees with the earlier campaign findings (pressure loss within 1-4 years; rates above the pre-2009 level). It moves the open question from "aftershock memory or forcing" to "which forcing": residual pore pressure, the change of injection depth by plug-backs, or a fault response that changes with time. Our data cannot separate these.

For forecasting and hazard: the 2024 Prague Mw 5.1 earthquake occurred on a fault zone that was active in 2011. ETAS calls it a late aftershock, but its zone had about 10 times more events than the Omori tail of 2011 allows. A forecast that treats the tail as aftershock memory overpredicts the event count by about 5 times. Yet it can also miss new moderate sequences on old faults, which come from the forcing. Simple decay of recent counts was the best of our forecasts. It has no physical basis and underpredicted 2023-2024.

## Limitations

- Main analysis at M≥3 only (101 events in 2021-2026). A M≥2.5 ETAS fit (10,017 events) was started but stopped: the host was overloaded (load about 180 on 24 CPUs, memory thrashing), and it did only 5 EM iterations in one hour. The mainshock-zone test uses M≥2.5.
- ComCat magnitudes mix ML (most events) and Mw (large events). The M≥3 b-value (1.35) is higher than at M≥2.5. Epicentral 2-D kernels only. One region box; edge effects (events outside the box) are ignored.
- The EM stopping rule ends on a flat ridge of the likelihood (A against p). The branching ratios are not precise. We report them only to show that the fits are near-critical.
- The synthetic study has 1-2 seeds per case. The forcing world is a construct (observed events with jitter): it shows that weak triggering plus forcing *can* give the observed ETAS result. It does not prove that this is the true mechanism. Its total counts follow the observed history by construction.
- Gutenberg-Richter magnitudes up to M6.0 in all simulations. A different maximum magnitude changes the cascade sizes in the predictive check and in the forecasts.
- Forecast ETAS runs use the 6-month-bin estimator. The time-smoothed fit failed the predictive check in the same way, so we did not repeat the forecasts with it.
- Injection is shown for context only. We did not fit a model that links the background to injection or pressure.
- Several of the analysis variants (0.5 km and 15-day forcing, fixed-p Omori fits) were added after we saw the first results. They are robustness checks, not pre-registered tests.
- Code versions: the main 6-month-bin fit (`runs/m30`) and four synthetic runs were made before two small additions to `etas.py` and `03_synthetic.py` (a floor for λ = 0 that acts only for isolated events, and jitter options with the same defaults). The main fit had a finite likelihood, so the floor was not active.

## Reproduce

1. `sh files/code/get_inputs.sh WORK CAMPAIGN_DIR` gets the ComCat CSVs and the parsed OCC table from the prior publication into the scratch folder `WORK` (never into this draft). Check the hashes in `files/data/`.
2. Copy `files/code` to `WORK/code` and run `sh code/run_all.sh` in `WORK` (Python 3.12, numpy 2, scipy, pandas, matplotlib; one BLAS thread per process). The full run takes about 12-20 CPU-hours. Most of this is the 14 ETAS fits.
3. `files/results/` holds all outputs: fitted parameters and per-event decompositions (`runs/*/fit.json`, `annual.csv`, `events_decomposed.csv.gz`), synthetic results (`runs/synth/`), predictive-check simulations (`ppc_*.csv`), Omori tables (`omori/`), forecasts, and `summary.json`. `files/logs/` holds the run logs.

## Files

- `files/code/`: `etas.py` (model and EM), `01_catalog.py`, `02_fit.py`, `03_synthetic.py`, `04_injection.py`, `07_summary.py`, `08_omori.py`, `09_ppc.py`, `10_forecast.py`, `get_inputs.sh`, `run_all.sh`
- `files/data/`: parsed ComCat catalog, regional injection totals, query URLs and hashes
- `files/figures/`: fig1_decomposition, fig2_predictive_check, fig3_identifiability (display items), fig4_omori_tails, fig5_forecasts
- `files/results/`, `files/logs/`
- `files/NOTICE_EXTERNAL_DATA.md`: sources, terms and attribution of the external data

## References

- Langenbruch, C., Zoback, M. D. (2016). How will induced seismicity in Oklahoma respond to decreased saltwater injection rates? Science Advances 2, e1601542. doi:10.1126/sciadv.1601542
- Langenbruch, C., Weingarten, M., Zoback, M. D. (2018). Physics-based forecasting of man-made earthquake hazards in Oklahoma and Kansas. Nature Communications 9, 3946. doi:10.1038/s41467-018-06167-4
- Llenos, A. L., Michael, A. J. (2013). Modeling earthquake rate changes in Oklahoma and Arkansas: possible signatures of induced seismicity. BSSA 103, 2850-2861. doi:10.1785/0120130017
- Ogata, Y. (1998). Space-time point-process models for earthquake occurrences. Annals of the Institute of Statistical Mathematics 50, 379-402. doi:10.1023/A:1003403601725
- Zhuang, J., Ogata, Y., Vere-Jones, D. (2002). Stochastic declustering of space-time earthquake occurrences. JASA 97, 369-380. doi:10.1198/016214502760046925
- Veen, A., Schoenberg, F. P. (2008). Estimation of space-time branching process models in seismology using an EM-type algorithm. JASA 103, 614-624. doi:10.1198/016214508000000148
- Utsu, T., Ogata, Y., Matsu'ura, R. S. (1995). The centenary of the Omori formula for a decay law of aftershock activity. Journal of Physics of the Earth 43, 1-33. doi:10.4294/jpe1952.43.1
- Skoumal, R. J., et al. (2024). Plug-backs and reduced injection lowered induced earthquake rates in Oklahoma (summary: https://www.seismosoc.org/news/plugged-wells-and-reduced-injection-lower-induced-earthquake-rates-in-oklahoma/)
- Campaign publications sci:sha256:c0a2572246ee8f3fa15450d11e3c30647b50a431bf8bae5b361c1bcb5ea198c8 and sci:sha256:d6c0ec4f174b1330bc04ff13b32b6747e594058c722d3ada3a7a4f9069c8d5e6
