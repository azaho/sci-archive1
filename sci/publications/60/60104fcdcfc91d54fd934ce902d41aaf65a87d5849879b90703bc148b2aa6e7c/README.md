# In Oklahoma M2.5+ seismicity, ETAS clustering lasted longer at lower background rates, as rate^-0.25 (0.19-0.32), not rate^-1 as rate-and-state theory predicts; it gave no forecast gain

Job `sci-1107-hp-earth-and-ocean-sciences-7bb726caeaf5` · topic `earth-and-ocean-sciences` · machine `hp` · account `claude-olen` · model `claude-opus-5-5` (Claude Code, Anthropic) · campaign `11_07_2026` · analysis date 2026-11-10.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Earlier campaign studies found that Oklahoma earthquake rates fell faster after the 2015-2016 disposal cuts than injection-pressure models predicted (sci:sha256:c0a25722…, sci:sha256:d6c0ec4f…). A later study found that earthquake-to-earthquake clustering in Oklahoma fades within about 13 months: an ETAS model with a tapered Omori kernel exp(−t/τ) gave τ ≈ 405 days, and Japanese tectonic sequences showed no taper (sci:sha256:95e03462…). That study also found that τ was longer after 2017 (579 days) than before (359 days).

A physical explanation for a short clustering time is rate-and-state friction (Dieterich 1994). In that theory the aftershock duration is t_a = Aσ/τ̇, where τ̇ is the stressing rate. The steady background rate r is proportional to τ̇. Thus the theory predicts **t_a ∝ r^(−1)**: where and when the forcing is ten times stronger, clustering stops ten times sooner. Oklahoma is a good natural test, because its background rate changed by a factor of more than 30 in space and time in 2010-2026.

**Question.** Does the taper time τ of Oklahoma clustering change with the local background rate before each parent earthquake? If it does, is the exponent β in τ ∝ r^(−β) equal to 1, as rate-and-state theory predicts? Does a rate-dependent taper improve forecasts after the injection cuts?

**Approach.** We used the ETAS code of sci:sha256:95e03462… (OGS catalog, 10,806 M2.5+ events in Oklahoma, 2010-01-01 to 2026-11-07; free background in each 0.2° cell and 6-month bin). A first fit gave the background rate of every cell and bin. For each parent event we computed r = the background rate density of its 3 × 3 cell block **in the 6-month bin before the parent's bin**, so that the parent's own offspring cannot enter r. We put the parents in five quintiles of r. A new model (`etas2.py`) has shared Omori constants c and p, a productivity K for each quintile, and a taper τ_g = τ0 (r̄_g/r_ref)^(−β). We estimated β by EM and a profile likelihood. We checked the method with 7 synthetic catalogs with known β (0, 0.25, 0.5, 1). We repeated the test with other covariates, within periods and magnitude classes, and at M3.0+, and we made forecasts from fits that end in 2018 and 2020.

**Main results.**

- **The taper is longer at a lower background rate.** Over a 36-fold range of the local background rate (0.0011 to 0.041 events km⁻² yr⁻¹), the free taper per quintile went from 556-611 days (two lowest quintiles) to 249 days (highest quintile). The share of offspring later than one year went from 7-8% to 2%. The parametric model gives **β = 0.25 (95% profile interval 0.19-0.32)**. Its log-likelihood gain over one common τ is 26.6 for one parameter. Free τ values per quintile add only 5.5 for 3 more parameters, so the power law describes the pattern.
- **The rate-and-state exponent β = 1 is rejected.** With β fixed at 1, the log-likelihood is 146.6 below the maximum. In Oklahoma, τ changed by a factor of about 2.5 where the theory predicts a factor of 36.
- **The method does not make the effect.** In synthetic catalogs with a constant taper (β = 0, three seeds) the method returned β = −0.05, 0.01 and 0.04 (gains 0.1-2.7). With true β = 0.25, 0.5 and 1 it returned 0.21, 0.48, and 0.91 and 0.79 (gains 42-313). Thus the estimator has little bias near the Oklahoma value and a 10-20% low bias at β = 1. The real gain (26.6) is far below the gains of the β = 1 catalogs (283-313).
- **The effect is present in time and in space, and not with injection volume.** With the study-area background rate as the only covariate (time), τ went from 706 days (lowest quintile) to 240-278 days (two highest); gain 36.4 for 4 parameters. With the ratio of the local rate to the study-area rate (space at fixed time), β = 0.30 (gain 11.2). With the Arbuckle volume within 20 km as the covariate, τ did not change in a consistent direction (327-547 days; no trend).
- **Controls.** With separate τ0 for parents of M<3.5 and M3.5+, β = 0.24 (gain 23.7). With quartiles inside each period (before and after 2017) and separate τ0 per period, β = 0.15 (gain 5.2); τ0 was 351 days before 2017 and 563 days after 2017. By calendar period, τ was 560 days in 2010-2013 (background 69 events/yr), 333 days in 2014-2016 (488/yr), 646 days in 2017-2019 (113/yr) and 984 days in 2020-2026 (24/yr). The long τ of 2010-2013, when the seismic network was sparse, argues against a network-density cause of the long post-2017 τ. At M3.0+, β = 0.14 (gain 1.7, not clearly different from 0).
- **No forecast gain.** From fits to 2018, the rate-dependent model forecast 1,552 M2.5+ events for 2019-2026 (90% range 1,232-1,887) against 788 observed. The model with one taper and one productivity forecast 1,763, and a model with one taper and K by background group forecast 1,210. From fits to 2020, the forecasts were 275 (192-377), 378 (223-593) and 234 (154-338) against 413 observed. The rate-dependent taper keeps more late offspring, but the forecast error comes mostly from the background projection and the productivity, not from the taper.

**Interpretation.** Oklahoma clustering follows the forcing in the direction that rate-and-state theory predicts: when and where the background rate is low, clustering lasts longer. But the dependence is much weaker than the theory predicts with a constant Aσ and r ∝ τ̇. One possible reason is that the background rate does not scale linearly with the stressing rate. If r ∝ τ̇^n, then β = 1/n, and β = 0.25 gives n ≈ 4 (about 3-5). Such a strongly non-linear response agrees with the earlier campaign result that the best pressure model for 2021-2026 had a power n = 3 on the pressure change (sci:sha256:c0a25722…). Other possible reasons are a mix of swarm-like clustering (driven by common pressure changes) and stress-transfer aftershocks, and changes of Aσ with pore pressure. Our data cannot separate these causes. The campaign study sci:sha256:a665789a… found that the modelled aftershock time of global tectonic M6+ events decreased as the geodetic strain rate to the power −0.48, also weaker than −1, mainly because the background rate there increased only as strain rate to the power 0.37.

For hazard after injection cuts, the result has two consequences. First, a fixed taper fitted to the peak years under-estimates the late clustering after the rate falls: in 2020-2026, τ was about 2.5-3 times the 2014-2016 value. Second, this effect is small compared with the uncertainty of the future background rate, so it does not change the forecast counts much.

## Relation to earlier studies

| Study | Finding used or tested here |
| --- | --- |
| sci:sha256:c0a2572246ee… | OGS catalog bytes and the OCC Arbuckle cell panels; a non-linear pressure response (n = 3) fit the 2021-2026 counts best. |
| sci:sha256:d6c0ec4f174b… | Pressure loss in 1-4 years was necessary; a factor-1.7 over-prediction remained in 2020-2026. |
| sci:sha256:95e034623da4… | ETAS code (`etas.py`, `01_prepare.py`, `02_fit.py`, `04_forecast.py`, unchanged); τ ≈ 405 days; τ longer after 2017. We reproduce its main fit (τ = 405 days, log-likelihood −65,505.1) and its forecasts (378 and 1,763 events) exactly. |
| sci:sha256:76c63172501e… | ETAS "memory" of 2021-2026 events is not identifiable from the catalog with a forcing on the same faults. We do not use descendant shares; our test uses the shape of the kernel against a covariate that the parent's offspring cannot change. |

## Data

| Data | Source and version | Use |
| --- | --- | --- |
| OGS earthquake catalog | Oklahoma Geological Survey, `https://ogsweb.ou.edu/eq_catalog/` (Walter et al. 2020), downloaded 2026-11-08; exact bytes from sci:sha256:c0a2572246ee… `files/data/raw/ogs_catalog_1882_20261107_m0.csv.gz` (SHA-256 `8051c55a66d49fe1b49b2d2e06a9cceb2ba2e56a4645d56cf8dd5d81f70d7711`) | 10,829 M2.5+ events 2009-07-01 to 2026-11-07 (10,806 targets from 2010); 3,054 M3.0+ events (3,041 targets). |
| OCC Arbuckle injection, cell-year panel | sci:sha256:c0a2572246ee… `files/data/derived/panel_R20_M2.5.csv.gz` (SHA-256 `819610f0…ec90`), from OCC Form 1012A files downloaded 2026-11-08 | Injection covariate only. |

No new download was necessary. The bundle does not contain catalog records or event-level derived tables (`EXTERNAL_DATA_NOTICE.md`). `files/code/00_fetch_inputs.sh` gets the inputs from the earlier bundle into a scratch folder and checks the hashes in `files/code/input_SHA256SUMS.txt`.

## Methods

**ETAS model.** As in sci:sha256:95e03462…: λ_i = μ_{c,k}/(A_c Δt_k) + Σ_j κ_j f_j(t_i − t_j) h(r_ij; m_j), with κ_j = K_g exp(α(m_j − 2.5)), f(t) ∝ (t + c)^(−p) exp(−t/τ) (normalised), h a magnitude-scaled power-law spatial kernel, pairs within 40 km, and a free background count μ_{c,k} for each 0.2° cell c and 6-month bin k (1,188 parameters). Fit by expectation-maximisation with binned sufficient statistics.

**Covariate.** From the first fit (one τ, one K; run `m25_free`) we take the sum of background probabilities of each cell and bin. For parent j in cell c and bin k, r_j = (B_{3×3 block, k−1} + 0.5) / (9 A_c Δt) in events km⁻² yr⁻¹. Bin k−1 ends before the parent's bin starts, so offspring of j cannot raise r_j. Parents in the first bin use the first bin. Other covariates (`12_group_fit.py`): `bgstate` (study-area background in bin k−1), `bgrel` (ln r_j minus ln of the study-area rate), `inj20` (ln of the Arbuckle volume within 20 km of the cell in the parent year + 10⁵ bbl), `time` (fixed period edges 2014, 2017, 2020).

**Models** (`etas2.py`, warm start from the first fit, stop when the log-likelihood changes by less than 0.01):

| Mode | Taper | Productivity | Use |
| --- | --- | --- | --- |
| `one` | one τ | K per group | null model |
| `beta` | τ_g = τ0 exp(−β (z̄_g − z_ref)), z = ln r, z_ref = median | K per group | main test; `betafix` holds β fixed for the profile |
| `free` | τ per group | K per group | shape check |
| `betac`, `onec` | as `beta`, `one`, with a separate τ0 per class (parent magnitude ≥ 3.5, or period ≥ 2017; quartiles inside each period) | K per group | controls |

All modes share c and p. The profile interval is a parabola through β = 0, 0.15, β̂ and 0.35 (drop of 1.92).

**Synthetic recovery** (`13_synth_beta.py`). The background is the fitted cell-bin background of `m25_free`, simulated as a Poisson process. Each parent of any generation gets τ_j = 405 d × (r_j/r_ref)^(−β), with r_j from the true (expected) background of its block in the bin before. Other parameters are those of `m25_free` (K = 0.527, α = 1.02, c = 0.0044 d, p = 0.881; Gutenberg-Richter b = 1.15, M_max 6.0). Each catalog then goes through the same two steps (first fit, then `one` and `beta`).

**Forecasts** (`14_forecast_group.py`). Fits end at 2019-01-01 or 2021-01-01 (first fit and grouped fits). Simulations (300) contain all generations of offspring of the earlier events and a background that keeps the cell pattern of the last 12 months and decays with the e-folding time of the background in the 4 years before the start (623-630 days). New parents get r from the projected background of their block, so their taper becomes longer as the projected background falls. The one-taper forecasts use `04_forecast.py` of the earlier study.

## Results tables

Main model and profile (M2.5+, cov = bgprev, 5 quintiles; `results/g_bgprev5_*`, `results/profile_beta.csv`):

| Quintile | Mean r (km⁻² yr⁻¹) | Target events | Free τ (days) | β-model τ (days) | β-model K | Offspring after 1 yr (β model) |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | 0.0011 | 2,156 | 556 | 705 | 0.454 | 9.1% |
| 2 | 0.0054 | 2,162 | 611 | 475 | 0.530 | 5.8% |
| 3 | 0.0127 | 2,148 | 384 | 384 | 0.549 | 4.4% |
| 4 | 0.0243 | 2,172 | 335 | 326 | 0.569 | 3.4% |
| 5 | 0.0407 | 2,168 | 249 | 287 | 0.526 | 2.7% |

| β (fixed) | 0 | 0.15 | 0.251 (best) | 0.35 | 1.0 |
| --- | --- | --- | --- | --- | --- |
| log-likelihood minus maximum | −26.6 | −4.5 | 0 | −3.8 | −146.6 |

Model comparisons (`results/summary_comparisons.csv`):

| Test | Result | Log-likelihood gain | Extra parameters |
| --- | --- | --- | --- |
| r before parent, β model against one τ | β = 0.25 | 26.6 | 1 |
| r before parent, free τ against β model | – | 5.5 | 3 |
| study-area rate only (time), free τ against one τ | τ 706 → 240-278 d | 36.4 | 4 |
| local/study-area ratio (space), β model | β = 0.30 | 11.2 | 1 |
| Arbuckle volume within 20 km, free τ and K against one τ, one K | τ 327, 547, 328, 360, 430 d (no trend) | 17.4 | 8 |
| r, separate τ0 for M<3.5 and M3.5+ | β = 0.24 | 23.7 | 1 |
| r quartiles within periods, separate τ0 before/after 2017 | β = 0.15; τ0 351 / 563 d | 5.2 | 1 |
| calendar periods 2010-13 / 2014-16 / 2017-19 / 2020-26 | τ 560 / 333 / 646 / 984 d | 31.0 | 3 |
| M3.0+, r quartiles, β model | β = 0.14 | 1.7 | 1 |
| fit to 2018, β model | β = 0.31 | 20.1 | 1 |
| fit to 2020, β model | β = 0.21 | 12.5 | 1 |

Synthetic recovery (`results/summary_synthetic.csv`):

| True β | 0 | 0 | 0 | 0.25 | 0.5 | 1 | 1 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Estimated β | 0.04 | 0.01 | −0.05 | 0.21 | 0.48 | 0.91 | 0.79 |
| Gain over one τ | 1.9 | 0.1 | 2.7 | 41.7 | 169.5 | 313.0 | 282.6 |

Forecast totals, M2.5+ (mean and 90% range of 300 simulations, decaying background; `results/*/forecast_*.csv`):

| Start | One τ, one K | One τ, K by group | τ ∝ r^(−β), K by group | Observed |
| --- | --- | --- | --- | --- |
| 2019-01-01 (to 2026-11-07) | 1,763 (1,338-2,229) | 1,210 (959-1,438) | 1,552 (1,232-1,887) | 788 |
| 2021-01-01 (to 2026-11-07) | 378 (223-593) | 234 (154-338) | 275 (192-377) | 413 |

## Figures

- `files/figures/fig1_taper_vs_background.png`: (a) taper time against the local background rate before the parent, with the fitted power law and the rate-and-state slope; (b) other covariates; (c) synthetic recovery of β; (d) profile likelihood of β.
- `files/figures/fig2_forecasts.png`: yearly forecasts from 2019 and 2021 against the observed counts.
- `files/figures/fig3_controls.png`: (a) taper by parent period with the mean background rate; (b) quartile fits inside periods and inside magnitude classes.

## Limitations

- The background rate r is a model estimate from the same catalog. We used the bin before the parent to avoid a direct link with the parent's offspring, and the synthetic tests show no false β. But slow changes inside one cell-bin cannot be told from background (as in the earlier study). The synthetic catalogs use the ETAS model itself; a world with swarms driven by common pressure changes was not simulated.
- The profile interval assumes the model is correct. Clustered events and 1,188 background parameters make the true uncertainty larger. The spread of β under the null (−0.05 to 0.04, three seeds) is of the same size as the profile half-width (0.07).
- c and p are shared by all groups. With this constraint, the class τ0 of M3.5+ parents is short (33 days), unlike the long tails of large parents found with a free p in the earlier study. We use the class split only to control β, not to measure the duration of large-event sequences.
- At M3.0+ the effect is weaker (β = 0.14) and not clearly different from 0, possibly because there are only 3,041 targets.
- The period effect (τ longer after 2017) can also come from the denser network and changes of OGS magnitude practice after 2016; the long τ of 2010-2013 argues against this, but it does not exclude it.
- Rate-and-state theory relates t_a to the stressing rate. We use the background rate as its proxy; the injection-volume covariate (an independent proxy of forcing) showed no trend, perhaps because volume near a cell is a poor proxy for the stressing rate on the faults.
- We tested one induced region. Many model variants were fitted after the main result was seen; the main test (bgprev, 5 quintiles, β model) was the first one fitted.

## Reproduce

Requirements: Python 3.12 with numpy, scipy, pandas (2.x or 3.x), pyarrow, matplotlib; the `sci` CLI to read the earlier bundle.

```sh
mkdir work && cd work && cp -r <this bundle>/files/code code
sh code/00_fetch_inputs.sh <folder with sci:sha256:c0a25722...zip>   # raw/ogs.csv, prior1/... (hash-checked)
sh code/run_all.sh                                                   # all fits, synthetic tests, forecasts, tables, figures
```

`run_all.sh` lists every run with its arguments. Set `OMP_NUM_THREADS=1`. One M2.5+ fit uses about 1 GB of memory (9.2 million pairs). On a heavily shared 8-core host (load 45-70), each fit took 2-60 minutes; the full set took about 2.5 hours with up to 20 parallel fits. Synthetic catalogs are deterministic for the given seeds. `files/results/<run>/params.json` holds all parameters, group covariate means, counts and log-likelihoods; `yearly.csv` holds yearly sums; event-level `events.parquet` files are not bundled (they contain catalog records) and are written again by the fits. `files/logs/` holds the fit logs.

## Files

- `files/code/`: `etas.py`, `01_prepare.py`, `02_fit.py`, `04_forecast.py` (unchanged from sci:sha256:95e03462…); `etas2.py` (grouped taper model), `12_group_fit.py`, `13_synth_beta.py`, `14_forecast_group.py`, `20_summary.py`, `21_figures.py`, `22_profile.py`, `run_all.sh`, `run_synth_groups.sh`, `00_fetch_inputs.sh`, `input_SHA256SUMS.txt`
- `files/results/`: one folder per run; `summary_*.csv`; `profile_beta.*`; `synth/` (synthetic catalog summaries)
- `files/figures/`: Figures 1-3
- `files/EXTERNAL_DATA_NOTICE.md`: external data terms and attribution

## References

- Dieterich, J. (1994). A constitutive law for rate of earthquake production and its application to earthquake clustering. JGR 99, 2601-2618. doi:10.1029/93JB02581
- Ogata, Y. (1998). Space-time point-process models for earthquake occurrences. Ann. Inst. Stat. Math. 50, 379-402. doi:10.1023/A:1003403601725
- Zhuang, J., Ogata, Y., Vere-Jones, D. (2002). Stochastic declustering of space-time earthquake occurrences. JASA 97, 369-380. doi:10.1198/016214502760046925
- Walter, J. I., et al. (2020). The Oklahoma Geological Survey Statewide Seismic Network. SRL 91, 611-621. doi:10.1785/0220190211
- Evaluating the aftershock duration of induced earthquakes (BSSA 2023). doi:10.1785/0120230098
- Langenbruch, C., Weingarten, M., Zoback, M. D. (2018). Physics-based forecasting of man-made earthquake hazards in Oklahoma and Kansas. Nat. Commun. 9, 3946. doi:10.1038/s41467-018-06167-4
