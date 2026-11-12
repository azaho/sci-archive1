# With range-wide GBIF niche indices, North American bird communities followed 4-7% of their spatial temperature gradient in 1970-2025 but 25-30% in 1997-2025; Swedish birds followed 28-53% in 1996-2019

Job: sci-1107-hp-climate-pollution-biodiversity-b42b87d90397 (campaign 11_07_2026, topic
climate-pollution-biodiversity, machine hp, account claude-olen). Model: Claude Opus 5.5
(claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Campaign work found that community temperature indices (CTI) follow only a small part of warming.
North American Breeding Bird Survey (BBS) CTI followed less than 10% of warming (sci:sha256:c0a3a9aa...).
75 monitoring networks followed about 12% of their own spatial gradient (sci:sha256:0037934e...). A lag
fit gave fast adjustment to a small target (theta about 0.28). For British butterflies, a recent result
(sci:sha256:814f6d39...) showed that the species temperature index (STI) source changes the answer:
STIs taken from the network's own sites gave 62% tracking, but STIs from the European range gave 14%.
The part of the internal STI that the range-wide niche did not explain carried non-climatic declines.

All bird results so far used internal STIs (from BBS routes, or from the network's own sites). That
publication listed the same test for birds as open. We asked:

1. Does bird CTI tracking change when the STI comes from the species' breeding range outside the survey
   (GBIF June occurrences) in place of the survey's own routes?
2. Which part of the internal STI carries the CTI trend and the spatial CTI gradient?
3. Is the result the same on a second continent (Swedish Bird Survey fixed routes, from BioTIME)?
4. Is the result the same in the early (1970-1996) and late (1997-2025) parts of the BBS record?

Questions 1-3 and the STI rules were fixed before we calculated any full-data tracking result. We added
these items after a first look at a partial download (138 of 539 species): the year-fixed-effect
estimator, the late-period internal STI, the period split, and the presence-only CTI. Section 6 gives
the details.

## 2. Data

- **BBS 2026 release** (USGS, public domain): States.zip (SpeciesTotal, 1966-2025), Weather.csv,
  Routes.csv, SpeciesList.csv. Standard runs (RunType 1, RPID 101), 1970-2025. Forms merged to Genus +
  species. Unidentified and hybrid entries removed.
- **BBS core trends 1966-2025** (USGS, public domain): survey-wide (SU1) species trends, only for diagnostics.
- **Swedish Bird Survey, fixed routes** (BioTIME 2.0 study 634, 1996-2019, PDDL; BioTIME Zenodo 15222193,
  15 April 2025). Species-level records only. Site = route.
- **GHCN_CAMS** monthly land air temperature, 0.5 degree (NOAA PSL; snapshot of 2026-11-05).
  May-July (MJJ) mean of each year. Climatology = MJJ mean of 1971-2000.
- **GBIF occurrence maps** (api.gbif.org v2 adhoc map tiles, fetched 2026-11-11): June records,
  years 1990-2025, 0.176-degree squares, zoom-2 tiles. North America: longitude -180 to -45, latitude
  0 to 90 (6 tiles per taxon). Europe and Asia: longitude -45 to 180 (10 tiles per taxon). We also
  fetched all birds (taxonKey 212) as an effort layer. The data come from many GBIF datasets, mostly
  eBird. We do not redistribute any GBIF record or tile.
- **AVONET** (Tobias et al. 2022, CC BY 4.0), eBird taxonomy sheet: habitat, migration and trophic niche,
  only for diagnostics.

The exact files, URLs and SHA-256 hashes are in `files/provenance.json`. `files/NOTICE-external-data.md`
gives the external licences.

## 3. Method

**CTI.** CTI(run) = sum(w x STI) / sum(w), with w = log(1 + count). A run needs at least 10 species
with all STI versions. We used the same species set for all STI versions, so differences come only
from the STI values (BBS: 413 species; Sweden: 161 species).

**Internal STI** (as in sci:sha256:c0a3a9aa...): the log(1 + count)-weighted mean route climatology of
the runs where the species occurred. BBS uses 1970-1989 runs (main) or 2006-2025 runs ("late").
Sweden uses all years (main), 1996-2007 or 2008-2019. We cross-fitted the STI between two random
halves of the routes (seed 20261111). A route's CTI uses the STI from the other half. A species needs
at least 10 routes in each half.

**External STI** (rules fixed before the tracking results; `04_sti_external.py`):

- Squares go into 0.5-degree CAMS cells. A cell is surveyed if all birds have 100 or more June records.
  A species is present in a surveyed cell if it has 2 or more records. We used only cells at or above
  10 degrees N.
- Main STI = equal-weight mean MJJ climatology of the present cells. A species needs 10 or more present cells.
- Variants: "rate-weighted" (weights = species records / all-bird records); "survey box only" (cells in
  24-62 N, 170-52 W for North America, or 55-69.5 N, 4-25 E for Sweden); "1% rate cut" (cells with a
  reporting rate below 1% of the species maximum are removed).
- Four BBS names use the AOS 2025 genera (Anarhynchus, Botaurus exilis). We matched them to their GBIF
  backbone names (Charadrius, Ixobrychus exilis).

**Spatial slope** b_space: OLS of route-mean CTI on route climatology (routes with 5 or more runs).

**Temporal slopes.** All with route x observer fixed effects for BBS, and route fixed effects for Sweden:

- Trend ratio R = (CTI ~ year) / (T ~ year) on the same runs. Tracking fraction phi_trend = R / b_space.
  A value of 1 means that the CTI changed as much as the spatial gradient predicts for the warming that occurred.
- Period trends: the same, within 1970-1996 and 1997-2025 (fixed effects within route x observer x period).
- Slow and fast parts (as in sci:sha256:0037934e...): CTI ~ beta_slow x tau + beta_fast x anomaly, where
  tau is the route's linear MJJ trend and anomaly = T - tau. phi = beta / b_space.
- Year-fixed-effect version: the same model with year effects added. Then only differences in warming
  between routes, not the common trend, identify beta_slow.

**Exact decomposition.** We fitted the internal STI (all-route version) on the external STI across
species: STI_int = a + b x STI_ext + residual. CTI is linear in STI, so
CTI_int = a + b x CTI_ext + CTI_res for every run. Thus the trend and the spatial slope split exactly
into a range-wide-niche part and a residual part.

**Uncertainty.** 400 bootstrap draws of 2-degree blocks of routes (1-degree blocks in Sweden). Each draw
keeps all runs of a route. We give percentile 95% intervals.

**Species contributions** (BBS): (within-route-observer trend of w per decade) x (STI - mean CTI) / mean
sum(w), as in sci:sha256:c0a3a9aa.... The contributions add to 0.019 against the exact fixed-effect trend
of 0.016 C per decade (linear approximation).

## 4. Results

### 4.1 Internal and external STIs agree in rank but not in detail

BBS: r = 0.95 between the internal and external STI, fit slope 1.01, residual SD 1.48 C (Figure 1).
Sweden: r = 0.72, slope 0.62, residual SD 1.43 C. The Swedish survey covers only a small, cold part of
most breeding ranges, so its internal STIs are compressed.

### 4.2 BBS 1970-2025: external STIs give one quarter to one half of the internal tracking

| STI version (413 species) | CTI trend, C per decade | phi_trend (95% CI) |
| --- | --- | --- |
| Internal, 1970-1989 routes (main) | 0.016 (0.010, 0.022) | 0.141 (0.089, 0.189) |
| Internal, 2006-2025 routes | 0.018 (0.012, 0.023) | 0.147 (0.100, 0.194) |
| Internal, presence only | 0.018 (0.012, 0.023) | 0.158 (0.105, 0.210) |
| External, GBIF June (main) | 0.004 (-0.001, 0.009) | 0.039 (-0.011, 0.093) |
| External, rate-weighted | 0.008 (0.000, 0.015) | 0.054 (-0.001, 0.112) |
| External, survey box only | 0.006 (0.002, 0.011) | 0.066 (0.016, 0.121) |
| External, 1% rate cut | 0.006 (0.000, 0.013) | 0.054 (0.002, 0.111) |
| External, presence only | 0.008 (0.003, 0.013) | 0.079 (0.029, 0.133) |

MJJ temperature on the same runs rose 0.267 C per decade (0.252 to 0.283). The spatial slope was 0.42
(internal) and 0.38 (external). 126,811 runs, 5,308 routes, 19,842 route-observer pairs.

- The internal result agrees with the earlier campaign value (raw ratio 0.060 here, 0.061 before).
- The STI period does not explain the difference. Internal STIs from 2006-2025 routes give the same
  fraction as those from 1970-1989 routes (0.147 against 0.141). Range shifts between periods
  thus do not cause the gap.
- **The residual part carries 75% of the internal CTI trend (0.0118 of 0.0158 C per decade), but only 9%
  of the spatial slope** (Figure 4). The range-wide-niche part carries the other 25% of the trend and 91%
  of the spatial gradient.
- The external variants range from 0.039 to 0.079. Even the variant that removes the tropical and Arctic
  parts of the range (survey box only) gives less than half of the internal value.

### 4.3 The two BBS periods: counter-climatic fall, then about 30% tracking with all STIs

| Period | MJJ trend, C per decade | phi_trend internal | phi_trend external | Residual-part CTI trend |
| --- | --- | --- | --- | --- |
| 1970-1996 | 0.129 (0.097, 0.163) | -0.60 (-0.81, -0.43) | -0.74 (-1.00, -0.54) | +0.004 (0.001, 0.007) |
| 1997-2025 | 0.372 (0.347, 0.398) | 0.33 (0.29, 0.38) | 0.27 (0.23, 0.32) | +0.012 (0.009, 0.016) |

In 1997-2025, all nine STI versions gave 0.25 to 0.33 (Figure 3). In 1970-1996, all versions gave a CTI
that fell while temperature rose (as found in sci:sha256:c0a3a9aa...). The residual part rose
steadily in both periods, independently of the climatic part (Figure 2). Over 1970-2025 the
fall and the rise of the range-wide-niche CTI cancel. The steady residual rise then makes most of
the internal long-term trend. Thus the low long-term value (about 0.04-0.14) mixes a counter-climatic
1970-1996 fall with a later response of about 0.3 of the spatial gradient.

### 4.4 Responses identified from temperature variation do not depend on the STI

| BBS estimator | Internal | External |
| --- | --- | --- |
| phi_fast (year-to-year anomalies) | 0.025 (0.021, 0.030) | 0.019 (0.015, 0.023) |
| phi_fast, with year effects | 0.023 (0.019, 0.027) | 0.017 (0.013, 0.021) |
| phi_slow, with year effects (differences in warming between routes) | 0.090 (-0.019, 0.178) | 0.068 (-0.025, 0.149) |
| phi_slow, without year effects | 0.143 (0.089, 0.193) | 0.053 (-0.001, 0.107) |

When the estimator uses only temperature variation (anomalies, or differences in warming between routes
with year effects), the two STIs give similar values. They differ only in the common continent-wide trend.
Climate does not identify that common trend.

### 4.5 What the BBS residual encodes

- The residual did not predict survey-wide species trends (Spearman -0.009, p = 0.86, 383 species). It
  also did not predict the within-route trend of w (Spearman -0.056, p = 0.26). The external STI had a
  weak positive link to the within-route trend (Spearman 0.14, p = 0.004). Thus the butterfly mechanism
  (residual = national decline geography) is not general. In BBS, the residual trend comes from a few
  species with large residuals and large changes.
- Positive residuals (birds on warmer BBS routes than their range-wide niche) were typical of grassland
  (+0.66 C, 38 species), human-modified habitat (+0.70 C, 16) and vertebrate-eating species (+0.98 C, 20).
  Forest species had -0.14 C (141).
- The largest residual contributors were increases of Canada Goose (residual +2.4 C), Turkey Vulture
  (+2.2 C) and Pileated Woodpecker (+3.4 C), and declines of Yellow Warbler (-5.7 C) and Eastern
  Meadowlark (-0.7 C). The external STIs of Yellow Warbler and Eastern Meadowlark include tropical resident
  populations that GBIF keeps in the same species. The "survey box only" variant removes this effect
  (phi 0.066). Declines of Savannah Sparrow, Horned Lark, Northern Flicker and Common Grackle (positive
  residuals) pulled the residual trend down.
- Many of the positive-residual increasers have known non-climatic causes (goose and turkey management,
  less persecution of raptors and vultures, forest regrowth). We did not test these causes.

### 4.6 Sweden 1996-2019: the opposite direction

| STI version (161 species) | phi_trend (95% CI) |
| --- | --- |
| Internal, all years (main) | 0.30 (0.19, 0.49) |
| Internal, 1996-2007 / 2008-2019 | 0.30 (0.18, 0.49) / 0.31 (0.20, 0.49) |
| Internal, presence only | 0.28 (0.17, 0.48) |
| External, GBIF June (main) | 0.53 (0.39, 0.75) |
| External, rate-weighted | 0.46 (0.34, 0.68) |
| External, survey box only | 0.28 (0.15, 0.48) |
| External, 1% rate cut | 0.52 (0.39, 0.75) |
| External, presence only | 0.36 (0.22, 0.57) |

9,318 route-years, 707 routes. MJJ temperature rose 0.31 C per decade (0.24 to 0.36). The CTI rose 0.034
(internal) and 0.051 C per decade (external). In Sweden the residual part carried only 8% of the
trend but 48% of the spatial slope. Thus the internal STI inflates the denominator (spatial gradient)
here, and not the numerator (trend) as in BBS. The year-effect estimators gave negative slow slopes
(internal -0.36, external -0.21). With 24 years and small differences in warming between routes, we
consider them not identified.

## 5. Interpretation

1. **The STI source matters for birds, but not in one fixed direction.** In BBS 1970-2025, range-wide
   STIs cut the tracking fraction from 0.14 to 0.04-0.08. In Sweden 1996-2019 they raised it from
   0.30 to 0.36-0.53 (0.28 for the box variant). In each network, the part of the internal STI that the
   range-wide niche does not explain carries a non-climatic geographic signal. It can inflate the
   trend (BBS, British butterflies) or the spatial gradient (Sweden). A tracking fraction that uses
   internal STIs is not a reliable measure of climate tracking unless an external-STI test agrees.
2. **The long-term "less than 10%" bird value is an average of two different periods.** With every STI,
   BBS CTI fell in 1970-1996 while temperature rose, and rose at 0.25-0.33 of the spatial gradient in
   1997-2025. Sweden gave 0.28-0.53 in 1996-2019. These recent values are close to the equilibrium
   fraction theta = 0.28 of the 75-network lag fit (sci:sha256:0037934e...). The very low long-term value
   comes from a counter-climatic early period (farmland and grassland losses, sci:sha256:c0a3a9aa...) and
   a residual drift, not from a uniformly weak response.
3. **Responses tied to temperature variation are small and robust.** Year-to-year anomalies move CTI by
   only 0.02 of the spatial gradient with either STI. Between-route warming differences give 0.07-0.09
   (intervals include 0). Thus the recent common rise of about 0.3 is not yet shown to follow local
   warming. A part of it can be a continent-wide non-climatic change. This limits point 2.
4. **For the open question of which processes set the gap:** the gap between space and time is
   partly a measurement problem (STI source; period mixing) and partly real. A real part remains
   with external STIs: about 0.3 of the gradient in recent decades, and only 0.02 of it for single
   warm or cold years.

## 6. Limitations and deviations from the plan

- Added after a partial-data look (138 species): year-effect estimators, late-period internal STI,
  period split, presence-only CTI. We ran the main estimators and STI rules as fixed before that.
- GBIF occurrences have strong effort bias (mostly eBird, towns and roads, US and Europe). The effort layer
  and the 100-record threshold reduce but do not remove it. The external STIs use 1990-2025 records,
  mostly after 2005.
- GBIF species concepts can include tropical or distinct populations (Yellow Warbler, Eastern Meadowlark).
  The box variant addresses this only for the North American range.
- 178 of 599 BBS taxa were too rare for the cross-fitted internal STIs. Of the other 421, 8 got no
  external STI (for example Cooper's Hawk, American Goshawk, Mountain Plover, Least Bittern: no species-level
  GBIF match or fewer than 10 present cells). Results apply to the 413 common species.
- The Swedish series is short (24 years). BioTIME holds 1996-2019 only. We did not use observer identity.
- Period-split fractions use the spatial slope of the whole period. The 1997 split point comes from the
  earlier campaign result (sci:sha256:c0a3a9aa...), not from these data.
- GHCN_CAMS is a coarse (0.5 degree) grid. Route climate uses the route start point.
- We did not test causes of individual species trends.

## 7. Files

- `files/code/`: all code. `run_all.sh` runs the full pipeline. `retrieve_data.sh` gets the inputs into
  local scratch. `mvt.py` decodes GBIF vector tiles.
- `files/results/bbs_tracking.csv`, `sbs_tracking.csv`: all estimates with bootstrap intervals (columns
  sti, stat, est, lo, hi, se). The STI codes are: int, intL, intE, ext, rr, dom, cut, res, intall, pint, pext.
- `files/results/bbs_sti.csv`, `sbs_sti.csv`: species STIs (internal halves, external variants, GBIF match).
- `files/results/*_decomposition.json`: exact residual decomposition.
- `files/results/species_diag_bbs.csv`, `species_diag_sbs.csv`, `species_diag.json`: residuals, AVONET
  traits, BBS trends and species contributions.
- `files/results/*_annual_cti.csv`: raw annual means (not fixed-effect adjusted).
- `files/figures/`: four PNG figures.

## 8. Reproduction

From the worktree root, with shared datasets under `./datasets` (or after `retrieve_data.sh` and path
edits): `sh work/result/files/code/run_all.sh`. Requirements: Python 3.12, numpy 2.5.4, pandas 3.1.1,
scipy 1.18.1, xarray 2026.9.0, matplotlib 3.11.2. A separate venv with pyreadr 0.5.9 reads the BioTIME RDS.
The GBIF fetch (about 4,700 tile requests) took about 30 minutes with 4 threads. The BBS bootstrap took
about 35 minutes on 1 CPU. GBIF counts change daily, so a new fetch gives slightly different external STIs.
The STIs we used are in `files/results/`.
