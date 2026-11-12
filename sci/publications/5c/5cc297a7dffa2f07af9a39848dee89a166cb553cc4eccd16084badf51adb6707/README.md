# A community pH index of English river invertebrates did not follow site pH change from 2000-2007 to 2016-2025 at 1,144 sites; soft northern streams gained acid-sensitive Heptageniidae

Job: sci-1107-dell-climate-pollution-biodiversity-bddefb64607e. Topic: climate-pollution-biodiversity. Machine: dell. Account: claude-myxtap. Model: Claude Opus 5.5 (claude-opus-5-5), working as an SCI campaign agent. The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Acid deposition in Britain decreased by more than 80% after 1990. Upland streams recovered chemically. Many studies say that biological recovery lags chemical recovery. A campaign study of 85 Swedish lakes (sci:sha256:93af4518ee9e) used the spatial relation between lake pH and assemblage composition as the target. It found that littoral invertebrates followed about 0.66-0.85 of the spatial expectation between 1995-2004 and 2013-2022. That study named UK waters as the next independent test.

We asked:

1. **H1.** Did river invertebrate assemblages at English Environment Agency (EA) sites change between 1995-2007 and 2015-2025 as much as the spatial pH-composition relation predicts for the measured site pH change? (Tracking ratio: 1 = full tracking, 0 = no response.)
2. **H2.** Did acid sites change more than buffered sites?
3. **H3 (weather extremes x acidity).** Did wet winters (acid episodes) lower the next-spring index more at soft-water sites than at buffered sites? Did the 2018 and 2022 drought summers set back soft-water sites?

The plan was written before the first pH-biology result (`files/PLAN.md`). We label deviations and tests added later as post hoc.

**What is new.** This is the first campaign test of acidification recovery in English rivers. It is an independent region, habitat (rivers, not lakes) and data system for the Swedish result. It joins the EA invertebrate open data with site pH from the new EA Water Quality API. It also adds a regional natural contrast (soft-water sites in the north, with high former deposition, against soft-water sites in Cornwall and Devon), a check of an apparent laboratory change in the pH record, and an index that removes the effect of river type. Earlier campaign work on English invertebrates studied ammonia, warmth, low flow and water quality (sci:sha256:f25760cd730c, sci:sha256:32a1ea318038, sci:sha256:39dc74ed016f), but not acidity.

## 2. Data

All source data are external and are not in this bundle (`files/NOTICE-external-data.md`). Hashes and paths are in `files/data/provenance.json`.

- **Invertebrates.** EA Ecology and Fish Data Explorer, `INV_OPEN_DATA.zip` (campaign copy `/mnt/dell-data/shared_datasets/ea-ecology-inv-open-data-20261110`, SHA-256 `ac2b745d...a40`) and `OPEN_DATA_TAXON_INFO.zip`. Open Government Licence v3.0 (OGL). We used river 3-minute kick samples (method S3PO), spring (March-May) and autumn (September-November), 1995-2025: 198,231 samples in total.
- **Water chemistry.** EA Water Quality API (`https://environment.data.gov.uk/water-quality`, accessed 2026-11-12, OGL). We listed all 18,449 river sampling points (type F6) and downloaded pH (determinand 0061), alkalinity to pH 4.5 (0162) and sulphate (0183) for the 2,099 points that are at most 500 m from an invertebrate site with 3 or more samples in both biological windows. The per-point response hashes are in `files/data/wq_obs_sha256.csv`. The API data can change.
- **Weather.** Met Office HadUK-Grid district series (rain and mean temperature; OGL), campaign copies `metoffice-district-{rainfall,tmean}-*`.

## 3. Methods

Code: `files/code/` (`fetch_data.sh`, then `run_all.sh`; about 1 hour on 2 CPUs after a 35-minute download).

- **Taxa** (`02_prep_inv.py`). EA analysis level changed over time (family-level and species-level analyses). We merged all records to family. Records above family rank (for example Oligochaeta) stay as their own unit. Weight = log10(abundance + 1) (presence = 1 for unenumerated records). Non-invertebrate groups were removed. There were 416 units.
- **Site pH** (`03_match_points.py`, `05_site_ph.py`). For each site, the nearest WQ point (at most 500 m) with 2 or more years of 3 or more pH samples in both windows (E = 2000-2007, L = 2016-2025). Window pH = mean of annual median pH. Base pH = E-window pH. There were 1,144 sites. Only 5 had base pH below 6.5, 51 below 7.2 and 169 below 7.5.
- **Community pH index (CpHI)** (`06_cphi.py`). The optimum of a family is the weighted mean base pH of the E-window samples in which it occurs. Optima are cross-fitted: 5 site folds x 5 repeats, so a site's index uses only optima from other sites. A family needs 10 or more training sites. The sample CpHI is the weighted mean optimum of its families. The site-window CpHI is the mean over seasons of the season means.
- **Tracking ratio.** b_s = slope of E-window CpHI on base pH across sites. b_t = slope of CpHI change on pH change across sites. Ratio = b_t / b_s. 95% intervals come from 2,000 site bootstrap samples (optima fixed). A noise correction divides by the reliability of the pH change (0.72), estimated from the year-to-year variation inside the windows.
- **Variants.** Presence weights. One sample per site-season-year. Biology early window 2000-2007. Change in WHPT ASPT (organic-pollution score) as a covariate. Soft sites only (base pH < 7.5). Adjustment for network-wide family change (counterfactual late profile = early profile + leave-one-out mean family change of sites with base pH >= 7.5). Annual panel with site and year fixed effects (same-year pH, 3-year mean, 3-year mean lagged by 3 years).
- **Post hoc variants** (added after the main result). (a) *Partial optima*: base pH after removal of river type (altitude, slope, log distance from source and EA region) by OLS. (b) *Soft-site optima*: optima trained and tested only on the 169 sites with base pH < 7.5. (c) *Post-2007 windows*: pH 2008-2012 against 2016-2025 and biology 2005-2012 against 2015-2025, to avoid a step in the pH record in 2005-2007 (Section 4.5). (d) Northern soft sites (NW and NE regions, base pH < 7.2, n = 20) against south-west soft sites (n = 25). (e) Occurrence change of three acid-sensitive mayfly families.
- **H3** (`07_weather_panel.py`). Annual site-season CpHI with site and year fixed effects, standard errors clustered by site. Interactions of district weather anomalies (1991-2020 base) with a soft-site indicator. Planned acid group: base pH < 6.5 (5 sites). Because this group was so small, we also report base pH < 7.2 (51 sites) against buffered sites (base pH >= 7.5, 975 sites); this is a deviation from the plan.

## 4. Results

### 4.1 pH change (Figure 1)

Mean pH increased by 0.066 units from 2000-2007 to 2016-2025 at the 1,144 sites. The increase was largest at soft sites in the north: +0.41 (95% interval 0.31 to 0.49) at the 20 NW and NE sites with base pH < 7.2, and +0.06 (-0.03 to 0.15) at the 25 soft sites in the south-west. Month-adjusted pH changes were the same as raw changes (site correlation 0.995), so seasonal sampling did not cause them.

![pH change map and pH change against base pH](files/figures/fig1_ph_change.png)

**Figure 1.** (a) pH change, 2016-2025 minus 2000-2007, at 1,144 EA invertebrate sites. Triangles: soft northern sites; squares: soft south-western sites. (b) pH change against base pH.

### 4.2 H1: the index did not follow pH change (Figures 2 and 3)

The spatial relation was clear: b_s = 0.065 CpHI units per pH unit (0.059 to 0.071). The temporal relation was absent.

| Test | Sites | Tracking ratio [95% interval] |
|---|---|---|
| Main (abundance weights, all sites) | 1,144 | -0.04 [-0.12, 0.04] |
| Main, noise-corrected | 1,144 | -0.06 |
| Main, with WHPT ASPT change | 1,144 | -0.01 [-0.09, 0.06] |
| Main, soft sites only (base pH < 7.5) | 169 | -0.06 [-0.28, 0.11] |
| Presence weights | 1,144 | -0.02 [-0.10, 0.06] |
| One sample per site-season-year | 1,144 | -0.04 [-0.12, 0.03] |
| Biology early window 2000-2007 | 1,139 | -0.09 [-0.17, -0.01] |
| Adjusted for network-wide family change | 1,144 | -0.17 [-0.25, -0.08] |
| Annual panel, same-year pH | 13,170 site-years | -0.02 [-0.04, 0.01] |
| Annual panel, 3-year pH lagged 3 years | 10,563 site-years | -0.00 [-0.05, 0.04] |
| Post hoc: post-2007 windows | 949 | -0.02 [-0.13, 0.08] |
| Post hoc: partial optima (river type removed) | 1,144 | 0.05 [-0.10, 0.19] |
| Post hoc: partial optima, soft sites | 169 | 0.21 [-0.07, 0.50] |
| Post hoc: soft-site optima | 169 | 0.11 [-0.02, 0.26] |
| Sweden, littoral lakes (sci:93af4518), for comparison | 85 | 0.85 [0.21, 1.34] |

The upper limits of all English intervals were 0.50 or less. Most were below 0.2. The Swedish point estimate (0.66-0.85) is outside all English intervals. H2 (acid minus buffered) was not informative with the main index (0.06 [-0.30, 0.66], 5 acid sites). With soft-site optima it was 0.75 [0.15, 1.43], but this compares only 5 acid sites with sites of base pH 7.0-7.5, and we treat it as fragile.

At the 20 northern soft sites, the main index predicts a change of +0.027 (0.020 to 0.032) for their pH increase. The observed change was -0.003 (-0.010 to +0.005). With soft-site optima, the prediction was +0.014 and the observed change -0.000 (-0.004 to +0.003). With partial optima, the prediction was +0.007 and the observed change +0.002 (-0.002 to +0.006).

The change in alkalinity did not predict index change either (slope on change in log10 alkalinity +0.008 [-0.005, +0.021], with pH change in the same model -0.003 [-0.008, +0.002]). A placebo convergence test inside buffered sites gave a small excess (-0.003 index units). The network-wide adjustment made the ratio more negative. Common family changes therefore did not hide a recovery signal.

![Spatial relation and tracking scatter](files/figures/fig2_tracking.png)

**Figure 2.** (a) Spatial relation between base pH and the 1995-2007 community pH index (cross-fitted optima). (b) Index change against pH change. Dashed line: full tracking (b_s x pH change). Green line: fitted relation.

![Forest plot of tracking ratios](files/figures/fig3_ratios.png)

**Figure 3.** Tracking ratios with 95% intervals for all English variants and the Swedish lake result.

### 4.3 Why the index failed: the English pH gradient is mainly a river-type gradient

In England, base pH is lowest in upland soft-water streams and highest in lowland hard-water rivers. The family optima therefore mainly separate lowland families (for example Tateidae, Asellidae, Planorbidae, with optima 7.87-7.92) from upland families. Some classic acid-sensitive families get low optima: Heptageniidae 7.73, Perlodidae 7.61. When these families increase at a recovering upland site, the index can decrease. Removal of river type reduced b_s by a factor of 4 (0.016) and moved the ratios up (0.05; 0.21 at soft sites), but the intervals stayed below 0.5. The soft-site index, trained only inside the soft-water range, gave 0.11. We conclude that a network-wide space-for-time index is not a valid recovery target for English rivers. A target from inside soft-water sites gave a small response (about 0.1-0.2 of expectation), with intervals that include zero.

### 4.4 Exploratory: acid-sensitive mayflies increased where pH increased (Figure 4c)

The family change table (`files/results/family_occurrence_change.csv`) showed Heptageniidae as the family with the largest increase at northern soft sites relative to buffered sites. Because we chose it after we saw the table, this result is exploratory. The share of samples with Heptageniidae increased from 0.55 to 0.80 at northern soft sites (+0.24 [0.12, 0.37]). It did not change at south-western soft sites (-0.02 [-0.08, 0.04]), where pH did not change, and it increased by +0.07 [0.06, 0.08] at buffered sites. The north minus south-west difference was +0.26 [0.15, 0.39]. Two other acid-sensitive mayfly families did not show a northern excess: Baetidae (-0.00 [-0.09, 0.08]) and Ephemerellidae (-0.05 [-0.18, 0.07]); Baetidae occurred in more than 84% of samples in both periods. Perlodidae (stoneflies) also increased at northern soft sites (0.53 to 0.75).

![Year series and mayfly change](files/figures/fig4_years_mayflies.png)

**Figure 4.** (a) Annual pH anomaly (site mean removed) for northern soft, south-western soft and buffered sites. (b) Annual index anomaly (site-season mean removed). (c) Change in the share of samples with three acid-sensitive mayfly families, 2015-2025 minus 1995-2007 (exploratory; 95% site bootstrap intervals).

### 4.5 A probable laboratory step in the pH record

The northern soft-site pH did not increase gradually. It was about 0.35 units below its mean in 2000-2005 and near its mean from 2007 (Figure 4a). In the same years, the number of points with alkalinity data decreased strongly in 2004-2006 (in the north to fewer than 15% of points), NW soft-site alkalinity was 0.25-0.28 log10 units high in 2006-2008 and then returned to normal, and NW hard-water pH increased by about 0.1. These patterns agree with a change in laboratory or sampling methods, which affects pH most in poorly buffered water. We did not find a documented date for such a change. We cannot separate this from real recovery. pH also increased again in 2012-2017 and decreased after 2018. Alkalinity of soft sites had no clear trend, and pH change had only a weak site correlation with alkalinity change (r = 0.33 at 51 soft sites; 0.10 at all 1,119 sites). With windows after the step (2008-2012 against 2016-2025), the tracking ratio was -0.02 [-0.13, 0.08]. If part of the northern pH increase is a laboratory artefact, the expected change in Section 4.2 is too large. The Heptageniidae increase (Section 4.4) does not depend on the WQ data.

### 4.6 H3: weather extremes and soft-water sites

Soft sites (base pH < 7.2, 51 sites) against buffered sites (975 sites), site and year fixed effects:

| Test | Interaction slope (SE) | Result |
|---|---|---|
| Spring CpHI x winter (DJF) rain anomaly, per 100 mm | -0.0004 (0.0005) | no clear link |
| Winter pH x winter rain anomaly, per 100 mm | +0.002 (0.009) | no clear link |
| Autumn CpHI x summer rain anomaly, per 100 mm | -0.0033 (0.0013) | small negative |
| Autumn CpHI x summer temperature anomaly, per 1 C | -0.0030 (0.0013) | small negative |
| Autumn CpHI, 2018 drought vs 2015-2017 | -0.0051 (0.0030) | not clear |
| Autumn CpHI, 2022 drought vs 2019-2021 | +0.0001 (0.0039) | no change |

With the planned acid group (5 sites below pH 6.5), all intervals included zero (winter rain: -0.0016 (0.0017); winter pH: +0.041 (0.036); 2018: +0.006 (0.008); 2022: -0.011 (0.007)). Wet winters did not lower spring index values or winter pH at soft sites. The two summer slopes are small: -0.003 index units equals about 0.05 pH units on the spatial scale. They are at about 2.5 standard errors among 6 tests. The droughts did not set back soft sites.

## 5. Interpretation

1. In English rivers, the composition of invertebrate assemblages did not follow the measured pH change between 2000-2007 and 2016-2025 as a network-wide space-for-time index predicts. All tests gave tracking ratios near zero, and the upper interval limits were 0.5 or less. This disagrees with the Swedish lake result (0.66-0.85).
2. The main reason is probably the target, not only the biology. In England, the spatial pH gradient mainly separates lowland from upland rivers. The index then treats families of lowland rivers as "high-pH" families. A recovery target must come from inside the acid-sensitive part of the gradient. The Swedish lakes had a pH range of 4.5-8 without a comparable lowland-upland split.
3. Inside soft-water sites, the response was small (ratio about 0.1-0.2, intervals including 0). Part of the measured northern pH increase may be a laboratory step in 2005-2007. So both the expected and the observed change are uncertain.
4. A specific biological sign of recovery exists: the acid-sensitive Heptageniidae became more common at northern soft sites where pH increased, and not at south-western soft sites where it did not (exploratory). Two other acid-sensitive mayfly families did not show this pattern.
5. Weather extremes did not reverse recovery signals at soft sites in this record.

## 6. Limitations

- Few acid sites. Only 5 sites had base pH below 6.5. The most acid English streams are mostly not EA routine WQ points. The UK Upland Waters Monitoring Network biological data, which cover such sites, are available only on request.
- The pH record starts in 2000, after much of the chemical recovery. The record has a probable laboratory step in 2005-2007 and a peak in 2012-2017. Spot samples miss acid episodes during high flow.
- Family level only. Genus or species changes (for example *Baetis* species) are not visible. Family optima are fixed in the bootstrap, so the intervals are slightly too narrow.
- The Heptageniidae result was chosen after we saw the data (one of 416 units). Treat it as a hypothesis for a new test.
- The weather tests use district-mean weather, not site weather, and the soft group has 51 sites.
- The site matching uses the nearest WQ point within 500 m. It can be on a tributary or on the other side of a confluence.
- The WQ API data can change; we saved per-point response hashes.

## 7. What remains open

- Test recovery with acid-specific indices (for example family or species acid-water indicator scores) inside soft-water sites, with a pre-registered taxon list.
- Get the UK Upland Waters Monitoring Network (or Welsh Llyn Brianne) biology and chemistry for a test with real acid sites.
- Find EA laboratory method change dates for pH and alkalinity to correct the 2005-2007 step.
- Test whether Heptageniidae and Perlodidae increases at soft sites in Wales and Scotland follow sulphate deposition (CBED or EMEP).

## 8. Files

- `files/PLAN.md`: analysis plan written before the pH-biology results.
- `files/code/`: `fetch_data.sh` (downloads into scratch, never into this bundle), `01`-`13` Python scripts, `run_all.sh`.
- `files/results/`: `tracking_<variant>.json` (all tracking estimates and intervals), `site_change_<variant>.csv` (site-level window means of pH and index, derived from OGL data), `extra.json` (panel, adjustment, regional and alkalinity tests), `weather_panel.json`, `north_checks.json`, `chem_check.json`, `chem_years.csv`, `year_series.csv`, `family_optima_*.csv`, `family_occurrence_change.csv`, `soft_sites.csv`.
- `files/data/`: `provenance.json` (sources, versions, campaign paths, SHA-256), `wq_obs_sha256.csv`, `site_points.csv` (invertebrate site to WQ point links).
- `files/figures/`: Figures 1-4.
- `files/NOTICE-external-data.md`: attribution and terms of the external data.

## 9. Reproduction

```
bash files/code/fetch_data.sh scratch          # EA invertebrates, Met Office series, EA WQ API (~35 min)
bash files/code/run_all.sh scratch DATASETS    # DATASETS = folder with metoffice-district-{rainfall,tmean}-<region>/ (campaign layout)
```
Python 3.12 with pandas, numpy, scipy, pyarrow, matplotlib. Campaign copies: `/mnt/dell-data/shared_datasets/ea-ecology-inv-open-data-20261110`, `.../ea-ecology-open-data-taxon-info-20261110`, `.../metoffice-district-*`. Without downloads, the site-level tables in `files/results/` let a reader check all across-site tracking estimates.
