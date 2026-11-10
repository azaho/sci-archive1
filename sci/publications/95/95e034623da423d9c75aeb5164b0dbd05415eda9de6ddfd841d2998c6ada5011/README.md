# Oklahoma M2.5+ earthquake clustering in 2010-2026 faded within about 13 months, unlike tectonic aftershocks; tapered ETAS fit to 2020 forecast the 2021-2026 count and pure Omori ETAS 5 times too many

Job `sci-1107-hp-earth-and-ocean-sciences-f9c42a489ef9` · topic `earth-and-ocean-sciences` · machine `hp` · account `claude-olen` · model `claude-opus-5-5` (Claude Code, Anthropic) · campaign `11_07_2026` · analysis date 2026-11-10.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Two earlier campaign studies found that the Oklahoma earthquake rate fell faster after the 2015-2016 disposal cuts than injection-pressure models predicted (sci:sha256:c0a25722…, sci:sha256:d6c0ec4f…). They also found that the 2021-2026 rate stays 4-18 times above the 1980-2008 level, at the places that were active in 2014-2016. Both studies modelled counts in cells and months. They did not separate earthquakes that other earthquakes trigger from independent ("background") earthquakes.

This study asks three questions:

1. How long does earthquake-to-earthquake triggering last in Oklahoma? Is it like tectonic aftershock sequences, which can last decades in continental interiors?
2. How much of the 2021-2026 rate is the late tail of the 2011-2020 sequences, and how much is new independent activity?
3. Does the change of triggering explain part of the "too fast" decline, and which model forecasts 2021-2026 from data to 2020?

We fitted a space-time ETAS (epidemic-type aftershock sequence) model to the OGS catalog (10,806 events M≥2.5 inside Oklahoma, 2010-01-01 to 2026-11-07). The independent rate is free in each 0.2° cell and 6-month bin, so the slow injection-driven change of the rate does not go into the triggering terms. The temporal triggering kernel is the Omori-Utsu law, with or without an exponential taper exp(−t/τ). We applied the same code to three Japanese tectonic sequences (JMA catalog) and to synthetic catalogs with a known kernel.

Main results:

- **Triggering in Oklahoma is short-lived.** The data strongly prefer a taper. The best taper time is τ = 405 days (profile 95% interval about 380-470 days, model-conditional; 335-474 days over six background designs). The log-likelihood gain over the pure Omori kernel is 680.5 (one extra parameter). At M≥3.0 the result is the same (τ = 457 days, gain 194). With the taper, 4.7% of the offspring of an event occur more than 1 year after it, and 0.04% more than 5 years after it. With the pure Omori fit, these fractions are 46% and 40%.
- **Tectonic controls and synthetic tests do not show this.** The same code gave no useful taper for the 2016 Kumamoto sequence (gain 0.0, τ → ∞), the 2000/2016 Tottori sequences (gain 0.4, τ = 26 years) and the 2004/2007 Chuetsu sequences (gain 9.0, τ = 3.6 years). Synthetic catalogs with a pure Omori kernel gave gains of 2.7-10.3 and τ = 6-13 years (a small bias to a finite τ). Synthetic catalogs with τ = 400 days gave τ = 325-374 days and gains of 701-724. Thus the method design does not by itself produce the Oklahoma result.
- **The long tails come from the larger events.** When parents of M≥3.5 have their own kernel, their τ is 6.5 years and p = 1.09 (near Omori). Parents of M<3.5 have τ = 335 days and p = 0.84 (gain 84 for 4 parameters). At M≥3.0, parents of M≥4.0 have no taper (τ → ∞). Thus the many small events cluster in short, swarm-like bursts, and only the larger events have long aftershock sequences.
- **Most 2021-2026 events are not the late tail of the earlier sequences.** Of the 413 M≥2.5 events in 2021-2026, the main tapered model attributes 32% to independent events (22 per year, 3.2 times the 1980-2008 rate of all events, 7.1 per year) and 29% to descendants of pre-2021 events (20% for 2022-2026). The magnitude-dependent model gives 30% and 33%. Over six background designs the tapered shares are 25-41% and 14-44%. The pure Omori model gives 18-32% and 40-58% in the same designs; it puts too much of the residual activity on old sequences.
- **Triggering became weaker after the cuts.** Productivity per parent fell from 0.556 (parents in 2014-2016) to 0.473 (2017-2019) and 0.398 (2020-2026) (gain 34.8 for 3 parameters). The ratio of all events to independent events fell from 5.1-5.8 (2014-2019) to 3.4 (2020-2026). A model with a constant cell productivity cannot follow this. This change is of the same size as the factor 1.7 that the best pressure model of sci:sha256:d6c0ec4f… over-predicted for 2020-2026. Productivity did not increase with the current Arbuckle injection near the parent, in either period.
- **Forecasts from January 2021.** A pure Omori ETAS model fitted to 2010-2020 is supercritical (mean productivity 2.3). From the pre-2021 events alone it forecast 2,018 events for 2021-2026 (90% range 1,677-2,439), 4.9 times the 413 observed. The tapered model forecast 120 from the pre-2021 events and 378 (223-593) with a background that continues its 2017-2020 decay (e-folding time 1.7 years). It forecast 971 (719-1,267) with a constant 2020 background. The decaying-background forecast agrees with the 2021-2023 counts but is too low for 2024-2026 (74 against 149). A magnitude-dependent tapered model forecast 412 (251-622). From January 2019, all models forecast too many events: the tapered model 1,763 (1,338-2,229) against 788, and the pure Omori model 6,539 or more, because the productivity fitted to 2010-2018 was too high for 2019-2026.
- **The independent rate still follows the old activity, not current injection.** Across 0.2° cells with 2013-2015 Arbuckle injection, the 2021-2026 independent count increases with the 2014-2016 count of the cell (slope 0.37-0.43, 95% intervals above 0). The slope on current (2020-2025) injection within 10, 20 or 30 km is 0.14, 0.15 and 0.35; only the 30 km interval excludes 0 (0.04-0.59). All upper bounds (0.46-0.59) are below 1, so the independent rate is not proportional to current local injection.

## Relation to the earlier studies

The earlier studies found that the decline after 2016 was faster than pressure models predicted and that pressure loss within 1-4 years was necessary. This study adds two catalog-based facts that the pressure models did not contain:

1. The clustering part of the rate (about 80% of all events in 2014-2019) dies out within about a year after its parent events. Thus, when the independent rate falls, the total rate follows it within about a year. A model that treats each event as equally "productive" of later seismicity over many years will forecast a slow decline.
2. The productivity of triggering fell after the cuts. This removes a factor of about 1.5-1.7 from the total rate in 2020-2026 at an unchanged independent rate.

Neither fact needs current injection to act directly. They are consistent with a high stressing rate during injection (rate-and-state theory gives an aftershock duration t_a = Aσ/τ̇ that is short at high stressing rates; Dieterich 1994) and with fault populations that are less close to failure after the pressure fell. They are also consistent with the BSSA study of Oklahoma sequences that modelled aftershock durations of less than five years (doi:10.1785/0120230098). The longer τ of the larger events and the longer τ after 2017 (579 days, against 359 days before 2017; gain 32.6 for 3 parameters) agree with the rate-and-state prediction that t_a increases when the stressing rate decreases, but the post-2017 change can also come from the denser network.

## Data

| Data | Source and version | Use |
| --- | --- | --- |
| OGS earthquake catalog | Oklahoma Geological Survey, `https://ogsweb.ou.edu/eq_catalog/` (Walter et al. 2020), downloaded 2026-11-08 by the earlier study. We use the exact bytes that sci:sha256:c0a2572246ee… redistributes as `files/data/raw/ogs_catalog_1882_20261107_m0.csv.gz` (SHA-256 `8051c55a66d49fe1b49b2d2e06a9cceb2ba2e56a4645d56cf8dd5d81f70d7711`; gunzipped `0277b494…affbcff`). | Events 2009-07-01 to 2026-11-07, 33.6-37.0°N, 100.0-94.4°W, magnitude rounded to 0.1, M≥2.5 (main) and M≥3.0. 124 near-duplicates (within 3 s and 5 km) removed. |
| Cell-year Arbuckle injection | `files/data/derived/panel_R{10,20,30}_M2.5.csv.gz` of sci:sha256:c0a2572246ee… (OCC Form 1012A UIC volumes, Arbuckle wells within R km of each 0.2° cell centre). SHA-256 in `files/code/input_SHA256SUMS.txt`. | Cross-section regression and injection-defined productivity groups. |
| JMA unified hypocentre catalogue 2000-2024 | Japan Meteorological Agency, `https://www.data.jma.go.jp/eqev/data/bulletin/data/hypo/hYYYY.zip`, as stored in the campaign shared datasets `datasets/jma-hypocenter-hYYYY-20261109/hYYYY.zip` (SHA-256 of all 25 files in `files/code/input_SHA256SUMS.txt`). | Tectonic controls: crustal (depth < 25 km) natural events, M≥2.5, boxes Kumamoto 32.3-33.4°N 130.3-131.6°E (2,223 events), Chuetsu 36.9-37.8°N 138.4-139.4°E (1,312), Tottori 34.9-35.7°N 132.9-133.9°E (466). |

The bundle does not contain the catalogs or event-level derived tables. `files/code/00_fetch_inputs.sh` writes them into a local work folder (see Reproduce). The results in `files/results/` are aggregates (model parameters, yearly sums, regression coefficients, forecast quantiles).

## Methods

**Model.** For target event i at time t_i and position x_i (km, local projection), the conditional intensity is

λ_i = μ_{c,k} / (A_c Δt_k) + Σ_{j: t_j < t_i, r_ij < 40 km} κ_j f(t_i − t_j) h(r_ij; m_j),

with κ_j = K_g exp(α(m_j − 2.5)), the normalised kernel f(t) ∝ (t + c)^(−p) exp(−t/τ) (τ = ∞ gives the pure Omori-Utsu pdf with p > 1), and the normalised spatial kernel h(r; m) = (q − 1)/(π s) (1 + r²/s)^(−q), s = d exp(γ(m − 2.5)). μ_{c,k} is a free expected background count for each 0.2° cell c and 6-month bin k (1,188 parameters in the main fit). Events from 2009-07-01 to 2009-12-31 act only as parents. Offspring that fall outside the box are ignored. `code/etas.py` fits all parameters by expectation-maximisation (stochastic declustering; Zhuang et al. 2002, Veen and Schoenberg 2008). The E-step computes the probability that each event is background or the offspring of each earlier event. The M-step sets each μ_{c,k} to the sum of the background probabilities in the cell-bin and maximises the expected complete-data log-likelihood of the triggering parameters, with binned sufficient statistics (2,500 log-time bins, 600 log-distance bins per parent magnitude). Iteration stops when the log-likelihood changes by less than 0.01 (0.001 for some early runs).

**Variants.** (a) pure Omori against a free τ, and a profile over fixed τ = 60-5,000 days; (b) productivity groups by parent period (2014, 2017, 2020 boundaries), by parent magnitude (M≥3.5; M≥4.0 at M≥3.0), and by the Arbuckle volume within 20 km of the parent cell in the parent year (terciles; median split within periods); (c) separate c, p, τ for each group; (d) background bins of 3, 12 and 24 months and cells of 0.1° and 0.4°; (e) M≥3.0.

**Attribution.** For each event after a date T0, `descend_from_before` computes the probability that its chain of parents reaches an event before T0 (recursion over the pair probabilities in time order). Sums over 2021-2026 give the expected number of events that descend from pre-2021 events.

**Controls.** `code/10_jma_control.py` extracts the three JMA boxes and `02_fit.py` fits them with the same settings (time origin 2000-01-01, end 2025-01-01).

**Synthetic recovery.** `code/03_synth.py` simulates catalogs with the fitted background of the main run and a known kernel: pure Omori (p = 1.08, c = 0.03 d, α = 1.05, K = 0.45 or 0.55; 5 catalogs) or τ = 400 d (p = 0.88, c = 0.0044 d, K = 0.50; 3 catalogs), b = 1.15, M_max = 6.0. Each catalog is fitted with τ = ∞ and free τ.

**Forecasts.** `code/04_forecast.py` refits the model with data to a start date T0 and simulates T0 to 2026-11-07 (300 simulations; 100 for pure Omori): (i) all generations of offspring of the events before T0; (ii) a background with the cell pattern of the last 12 months before T0, constant or decaying with the e-folding time of a log-linear fit to the yearly background sums of the 4 years before T0, with all its offspring. The observed counts after T0 are not used.

**Cross-section.** `code/05_bg_injection.py` repeats the negative binomial regression of the earlier study (sci:sha256:c0a25722…, `07_scenario_tail.py`) with the 2021-2026 background sum (or triggered sum) of each cell as the response; 600 resamples of 1° blocks.

## Results

### Taper tests (Figure 1)

| Catalog | Target events | free τ (days) | p (free τ) | Gain over pure Omori |
| --- | --- | --- | --- | --- |
| Oklahoma M≥2.5 | 10,806 | 405 | 0.88 | 680.5 |
| Oklahoma M≥3.0 | 3,041 | 457 | 0.86 | 194.2 |
| Kumamoto 2016 (Mj 7.3), M≥2.5 | 2,223 | ~10⁶ (no taper) | 1.13 | 0.0 |
| Chuetsu 2004/2007 (Mj 6.8), M≥2.5 | 1,312 | 1,325 | 1.20 | 9.0 |
| Tottori 2000/2016 (Mj 7.3/6.6), M≥2.5 | 466 | 9,380 | 1.05 | 0.4 |
| Synthetic, pure Omori truth (5) | 3,836-4,660 | 2,325-4,691 | 1.06-1.09 | 2.7-10.3 |
| Synthetic, τ = 400 d truth (3) | 9,600-10,100 | 325-374 | 0.87-0.89 | 701-724 |

Profile over fixed τ (Oklahoma M≥2.5, gain over pure Omori): τ = 60 d: −172.5; 120 d: 346.8; 240 d: 621.9; 405 d (free): 680.5; 600 d: 653.3; 1,000 d: 553.6; 2,000 d: 372.3; 5,000 d: 179.6 (`results/tau_profile_m25.csv`). A parabola in log τ through the points from 240 to 1,000 days peaks at 424 days, and a drop of 1.92 gives 381-471 days.

Background-resolution sensitivity (M≥2.5; each row compares free τ with pure Omori at the same background design):

| Background design | Background parameters | free τ (days) | Gain | Independent share 2021-2026 (taper / pure Omori) | Pre-2021-descendant share 2021-2026 (taper / pure Omori) |
| --- | --- | --- | --- | --- | --- |
| 0.2°, 6 months (main) | 1,188 | 405 | 680.5 | 0.32 / 0.24 | 0.29 / 0.50 |
| 0.2°, 3 months | 1,698 | 372 | 710.1 | 0.35 / 0.26 | 0.22 / 0.47 |
| 0.2°, 12 months | 828 | 432 | 666.3 | 0.29 / 0.21 | 0.34 / 0.53 |
| 0.2°, 24 months | 583 | 452 | 661.6 | 0.26 / 0.19 | 0.38 / 0.56 |
| 0.1°, 6 months | 2,030 | 335 | 696.8 | 0.41 / 0.32 | 0.14 / 0.40 |
| 0.4°, 6 months | 694 | 474 | 684.6 | 0.25 / 0.18 | 0.44 / 0.58 |

The taper time and its support do not depend much on the background design (τ = 335-474 days, gains 662-710). The split of the 2021-2026 events depends on it: a coarser background gives a larger share to old sequences. In every design, the pure Omori model gives a larger pre-2021 share than the tapered model.

### Parent groups

| Model (M≥2.5, free τ) | Log-likelihood | Gain | Parameters added | Result |
| --- | --- | --- | --- | --- |
| one kernel | −65,505.1 | – | – | K = 0.527, τ = 405 d, p = 0.881 |
| K by period (2017) | −65,484.5 | 20.7 | 1 | K = 0.550 before 2017, 0.460 after |
| K by period (2014, 2017, 2020) | −65,470.3 | 34.8 | 3 | K = 0.454, 0.556, 0.473, 0.398 |
| K, c, p, τ by period (2017) | −65,451.9 | 53.3 | 4 | τ = 359 d before, 579 d after; p = 0.89, 0.85 |
| K, c, p, τ by parent magnitude (3.5) | −65,421.2 | 83.9 | 4 | M<3.5: τ = 335 d, p = 0.84; M≥3.5: τ = 2,375 d, p = 1.09 |
| K by local injection tercile | −65,498.0 | 7.2 | 2 | K = 0.515, 0.561, 0.511 (median 0.8, 12, 36 Mbbl/yr) |
| K by period × injection (median 12.5 Mbbl/yr) | −65,480.0 | 25.1 | 3 | before 2017: 0.548 low, 0.550 high; after: 0.473 low, 0.378 high |
| K, c, p, τ by magnitude (3.5) × period (2017) | −65,365.2 | 139.9 | 12 | M<3.5: τ = 324 d before 2017, 420 d after (p = 0.86, 0.80); M≥3.5: τ = 824 d before, no taper after (p = 1.07, 1.05); K = 0.549, 0.480, 0.485, 0.446 |

At M≥3.0, the magnitude split (M≥4.0) gives τ = 399 d and p = 0.82 for M<4.0 parents and no taper (p = 1.13) for the 84 M≥4.0 parents (gain 22.7 over one tapered kernel).

### Decomposition of the yearly counts (Figure 2)

Tapered model, M≥2.5 (2026: 1 January-7 November):

| Year | All | Independent | Descend from pre-2021 | Pure Omori: independent | Pure Omori: from pre-2021 |
| --- | --- | --- | --- | --- | --- |
| 2015 | 3,301 | 653 | – | 724 | – |
| 2017 | 1,047 | 172 | – | 172 | – |
| 2019 | 231 | 55 | – | 50 | – |
| 2020 | 144 | 31 | – | 27 | – |
| 2021 | 125 | 29.2 | 61.4 | 26.2 | 66.6 |
| 2022 | 82 | 28.3 | 15.8 | 23.2 | 26.8 |
| 2023 | 57 | 25.2 | 9.5 | 15.4 | 30.7 |
| 2024 | 72 | 17.2 | 24.3 | 11.4 | 52.9 |
| 2025 | 30 | 12.9 | 5.2 | 9.1 | 16.2 |
| 2026 | 47 | 18.2 | 2.7 | 13.2 | 12.2 |

In the tapered model, most pre-2021 descendants in 2024 (24.3 of 72) are in two new sequences: the 13 January 2024 M4.3 and M4.1 sequence in Oklahoma County (12.8 events in two cells; 1 M≥2.5 event per year in 2019-2023 within 10 km) and the 3 February 2024 Prague M5.1 sequence (4.6). The model gives the main shocks probabilities of 0.76 and 0.29 to descend, through chains of earlier small events, from pre-2021 activity. Such attributions of the first event of a new burst depend on weak long-lag terms and are uncertain.

Ratio of all events to independent events (tapered model): 3.0 (2010-2013), 5.1 (2014-2016), 5.8 (2017-2019), 3.4 (2020-2026).

### Forecasts (Figure 3)

| Fit to | Model | Cascade of earlier events only | + decaying background | + constant background | Observed |
| --- | --- | --- | --- | --- | --- |
| 2010-2020 | pure Omori | 2,018 (1,677-2,439) | 2,209 (1,853-2,611); P(N ≤ obs) = 0 | 2,645 (2,300-3,061) | 413 (2021-2026) |
| 2010-2020 | tapered | 120 (49-241) | 378 (223-593); P = 0.66 | 971 (719-1,267) | 413 |
| 2010-2020 | magnitude-dependent taper | 161 (70-282) | 412 (251-622); P = 0.54 | 985 (717-1,267) | 413 |
| 2010-2018 | pure Omori | 5,604 (4,989-6,293) | 6,539 (5,746-7,237) | 9,414 (8,527-10,484) | 788 (2019-2026) |
| 2010-2018 | tapered | 691 (460-1,025) | 1,763 (1,338-2,229); P = 0 | 5,343 (4,605-6,112) | 788 |

Mean and 90% range of the simulated 2021-2026 (or 2019-2026) totals; `results/forecast_totals.csv` and `results/<run>/forecast_<start>.csv`. The decaying background uses the e-folding time of the background in the 4 years before the start (1.7 years for both starts).

Yearly means for the start in 2021 (tapered + decaying background / magnitude-dependent + decaying background / observed): 2021: 138 / 141 / 125; 2022: 101 / 107 / 82; 2023: 65 / 71 / 57; 2024: 38 / 47 / 72; 2025: 24 / 30 / 30; 2026: 13 / 17 / 47.

For the start in 2019, even the tapered model forecast too many events (634 against 231 in 2019; the cascade of pre-2019 events alone gave 344). The productivity fitted to 2010-2018 is mostly that of 2014-2016, and the independent rate halved from 2018 to 2019 (111 to 55). The pure Omori fits are degenerate: p goes to 1.04 (2020) and 1.002 (2018), and the mean productivity per event is 2.3 and 35 (supercritical).

### Cross-section (Figure 4)

Negative binomial slopes for 2021-2026 counts (tapered model; 95% 1° block bootstrap, 600 resamples; `results/m25_free/bg_injection_regression.csv`):

| R (km) | Response | Slope on current injection | Slope on 2014-2016 count | Sum of response |
| --- | --- | --- | --- | --- |
| 10 | all | 0.14 [−0.19, 0.69] | 0.44 [0.28, 0.88] | 186 |
| 10 | independent | 0.14 [−0.22, 0.50] | 0.37 [0.21, 0.73] | 58.8 |
| 10 | triggered | 0.10 [−0.17, 0.80] | 0.44 [0.27, 0.94] | 127.2 |
| 20 | all | 0.23 [−0.33, 0.75] | 0.49 [0.39, 0.81] | 277 |
| 20 | independent | 0.15 [−0.21, 0.46] | 0.42 [0.27, 0.62] | 86.9 |
| 20 | triggered | 0.23 [−0.64, 1.04] | 0.49 [0.41, 0.93] | 190.1 |
| 30 | all | 0.39 [−0.07, 0.69] | 0.53 [0.43, 0.78] | 318 |
| 30 | independent | 0.35 [0.04, 0.59] | 0.43 [0.31, 0.60] | 102.6 |
| 30 | triggered | 0.35 [−0.28, 0.62] | 0.54 [0.44, 0.89] | 215.4 |

## Limitations

- The background is free in each cell and 6-month bin. A slow aftershock tail inside one cell-bin cannot be told from background, so the model measures how long triggering stays concentrated near its parent (within a few km), not the full duration of any rate change. The synthetic tests show a small bias of this design toward a finite τ (6-13 years for a pure Omori truth), far from the 1.1 years in Oklahoma. The 12-month background gave τ = 413 days.
- "Triggering" in ETAS is statistical clustering. In Oklahoma, part of it is probably swarm activity driven by common pressure transients, not stress transfer between earthquakes. The short τ of small parents fits this view.
- The profile interval for τ assumes the model is correct; events are clustered and the model has 1,188 background parameters, so the true uncertainty is larger.
- OGS magnitudes mix local magnitudes and copied Mw values, and the OGS ML of some M≥3.3 events was 0.2-0.3 above Mw in 2015-2017 (earlier study). A magnitude shift of 0.25 in 2014-2017 could raise the apparent productivity of that period by up to about 50%. The productivity decline after 2016 can therefore partly come from magnitude practice. The network became denser after 2016, which can change short-term completeness, c and τ.
- We assumed that the OGS catalog is complete at M≥2.5 from 2010 (the modal magnitude was 2.3 or less in every year). Short-term incompleteness after large events is not modelled.
- We did not use relocated hypocentres or depths. Spatial leakage of offspring outside the box and Kansas events are not modelled.
- The tectonic controls are three Japanese boxes with fewer events than Oklahoma. They show that the method can return long durations; they do not give a full tectonic reference.
- Many model variants were compared after the main result was seen. The forecast tests use only data before the start date, but the choice to report the tapered model was made after the full-period fit.

## Reproduce

Requirements: Python 3.12 with numpy, scipy, pandas (2.x or 3.x), pyarrow, statsmodels, matplotlib; the `sci` CLI to read the earlier bundle.

```sh
mkdir work && cd work && cp -r <bundle>/files/code code
sh code/00_fetch_inputs.sh <folder with sci:sha256:c0a25722...zip> [<folder with jma-hypocenter-hYYYY-20261109>]
python code/01_prepare.py                       # scratch/events_M2.0.parquet
python code/10_jma_control.py datasets_jma      # scratch/ctl_*.parquet
mkdir -p results logs
sh code/run_batch.sh code/jobs_all.txt 4        # all fits listed in jobs_all.txt (about 10-30 min each at high load)
sh code/run_synth.sh                            # synthetic catalogs and their fits (needs results/m25_free)
python code/04_forecast.py m25_free_to2021 2021-01-01 nsim=300
python code/04_forecast.py m25_inf_to2021 2021-01-01 nsim=100
python code/04_forecast.py m25_gmag35_go_free_to2021 2021-01-01 nsim=300
python code/04_forecast.py m25_free_to2019 2019-01-01 nsim=300
python code/04_forecast.py m25_inf_to2019 2019-01-01 nsim=100
python code/05_bg_injection.py m25_free nboot=600
python code/05_bg_injection.py m25_inf nboot=600
python code/06_figures.py && python code/07_summary.py
```

Set `OMP_NUM_THREADS=1`. One M≥2.5 fit uses about 1 GB of memory and 9.2 million parent-child pairs. `results/` in this bundle holds `params.json` and `yearly.csv` of every fit (for the JMA controls only the yearly count and background sum; calendar years), the forecast tables, the regression tables and the summary tables. The event-level files `events.parquet` are not bundled (they contain catalog records); `02_fit.py` writes them again.

## Files

- `files/code/`: `etas.py` (model and EM), `01_prepare.py`, `02_fit.py`, `03_synth.py`, `04_forecast.py`, `05_bg_injection.py`, `06_figures.py`, `07_summary.py`, `10_jma_control.py`, `00_fetch_inputs.sh`, `run_batch.sh`, `run_synth.sh`, `jobs_all.txt`, `input_SHA256SUMS.txt`
- `files/results/<run>/params.json`, `yearly.csv`, forecast and regression tables; `all_fits_summary.csv`, `summary_*.csv`, `tau_profile_m25.csv`, `synthetic_recovery.csv`, `forecast_totals.csv`
- `files/figures/fig1_taper_tests.png` … `fig4_cross_section.png`
- `files/EXTERNAL_DATA_NOTICE.md`: sources, terms and attribution of the external data

## References

- Dieterich, J. (1994). A constitutive law for rate of earthquake production and its application to earthquake clustering. JGR 99, 2601-2618. doi:10.1029/93JB02581
- Langenbruch, C., Weingarten, M., Zoback, M. D. (2018). Nature Communications 9, 3946. doi:10.1038/s41467-018-06167-4
- Llenos, A. L., Michael, A. J. (2013). Modeling earthquake rate changes in Oklahoma and Arkansas: possible signatures of induced seismicity. BSSA 103, 2850-2861. doi:10.1785/0120130017
- Ogata, Y. (1998). Space-time point-process models for earthquake occurrences. Ann. Inst. Stat. Math. 50, 379-402. doi:10.1023/A:1003403601725
- Stein, S., Liu, M. (2009). Long aftershock sequences within continents and implications for earthquake hazard assessment. Nature 462, 87-89. doi:10.1038/nature08502
- Veen, A., Schoenberg, F. P. (2008). Estimation of space-time branching process models in seismology using an EM-type algorithm. JASA 103, 614-624. doi:10.1198/016214508000000148
- Walter, J. I., et al. (2020). The Oklahoma Geological Survey Statewide Seismic Network. SRL 91, 611-621. doi:10.1785/0220190211
- Zhuang, J., Ogata, Y., Vere-Jones, D. (2002). Stochastic declustering of space-time earthquake occurrences. JASA 97, 369-380. doi:10.1198/016214502760046925
- Evaluating the aftershock duration of induced earthquakes (2023). BSSA. doi:10.1785/0120230098
- Earlier campaign studies: sci:sha256:c0a2572246ee8f3fa15450d11e3c30647b50a431bf8bae5b361c1bcb5ea198c8 and sci:sha256:d6c0ec4f174b1330bc04ff13b32b6747e594058c722d3ada3a7a4f9069c8d5e6
