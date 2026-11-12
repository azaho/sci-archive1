# Southern African bird communities followed about 28% of their spatial temperature gradient in 2008-2024 but only 2-5% of their rainfall gradient; waterbirds followed about one third

Job: sci-1107-dell-climate-pollution-biodiversity-b4d4097de6ef (campaign 11_07_2026, topic
climate-pollution-biodiversity, machine dell, account claude-sci). Model: Claude Opus 5.5
(claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Campaign work found that community thermal composition follows only a small part of its own spatial
temperature gradient in time: 12% for the multi-year trend and 2% for year-to-year anomalies in 75
monitoring networks (sci:sha256:0037934e...), 24-47% in Swedish birds (sci:sha256:3adef8e9...),
14% in British butterflies with European niches (sci:sha256:814f6d39...). All these networks are in
the Northern Hemisphere and all of them test temperature only.

We asked:

1. Does a Southern Hemisphere bird community, with a new atlas protocol and a new observer pool,
   give the same small temperature fraction?
2. In a semi-arid region, do communities follow rainfall instead? Rainfall in southern Africa
   changes much from year to year (the 2015-2016 and 2019 droughts, the 2021-2022 wet years).
   If birds track water more than heat, a community precipitation index (CPI) should follow a
   large part of its spatial rainfall gradient.

## 2. Data

- **SABAP2** (Southern African Bird Atlas Project 2, GBIF dataset 906e6978..., CC BY 4.0,
  25.7 million records). Each record is one species on one atlas card (a pentad of 5' x 5', at least
  2 hours of observation, at most 5 days). We used the GBIF occurrence-search API with facets: the
  number of records of each species in each 1-degree cell, calendar year (2008-2024) and half-year
  (H1 January-June, H2 July-December), with facets for month, pentad latitude/longitude and observer.
  We did not download individual records.
- **SABAP1** (1987-1992 atlas, GBIF dataset 282d0ccb..., CC BY 4.0): the same facets for 1986-1992
  pooled, per 1-degree cell and half-year.
- **Species niches**: SABAP2 2008-2025 pooled, per 0.5-degree cell, over southern Africa
  (35-8 S, 11-41 E): 846 cells with at least 20 cards (proxy), 990 species.
- **Climate**: CRU TS 4.09 monthly mean temperature and precipitation, 0.5 degree (decadal files from
  the campaign store; the shared 1901-2024 tmp/pre copies and one 2021-2024 pre copy are truncated
  gzips and were not used; see `files/data/cru_provenance.json`).

Study panel: 113 one-degree cells in South Africa, Lesotho and Eswatini (35-22 S, 16-33 E) with at
least 20,000 SABAP2 records; 3,534 cell-year-halves with a card proxy of at least 10 (median 61);
21.2 million records. SABAP1: 98 of these cells (196 cell-halves, 4.1 million records).

## 3. Method

The estimator follows sci:sha256:0037934e... so that the numbers compare directly.

- **Species indices.** For each species, the species temperature index (STI) and species
  precipitation index (SPI) are the means of the 1991-2020 annual mean temperature and log10 annual
  precipitation over the 0.5-degree cells, weighted by the relative reporting rate
  r = n(species, cell) / max over species n(cell). The card count of a cell cancels in r up to a
  constant. 891 species had indices from at least 3 cells.
- **Cross-fitting.** We split the 1-degree cells into two halves, stratified by climate (10 random
  splits). A cell's community index uses only species indices from the other half.
- **Community indices.** CTI and CPI of a cell-year-half are record-weighted means of STI and SPI.
  This is the reporting-rate-weighted mean; the number of cards cancels. We also used a
  presence-only (unweighted) variant.
- **Observation-bias controls.**
  (a) Month mix: we subtracted the shift that the month composition of the cards gives, from a
  regional month profile of CTI and CPI (migrants arrive in October-March).
  (b) Effort and observers: covariates log card proxy, mean pentad latitude and longitude, number of
  distinct observers and the share of records from the top observer. Effort grew fast (card proxy
  +0.42 log units and +21 observers per decade per cell).
  (c) Year effects: a variant with year-half fixed effects removes all region-wide changes,
  including protocol and observer drift, and uses only differences between cells.
  (d) Species-shuffle null: 100 permutations of STI/SPI among species.
- **Climate per cell-year-half.** 12-month window ending in June (H1) or December (H2), mean of the
  0.5-degree boxes; also a 24-month and a lagged 12-month rainfall window.
- **Spatial slope b.** Cell-mean index on 1991-2020 cell climatology, bivariate in temperature and
  log10 precipitation.
- **Temporal slopes.** For each cell-half, temperature and log precipitation were split into a
  linear 2008-2024 trend (tau) and an anomaly (a). Index = cell-half effect + beta_slow,T tau_T +
  beta_fast,T a_T + beta_slow,P tau_P + beta_fast,P a_P + controls; two-way (cell, year)
  cluster-robust errors.
- **Fractions.** phi = beta / b. A value of 1 means full space-for-time equivalence.
  95% intervals: 500 (main) or 400 (second set) bootstrap samples of 2-degree blocks of cells.
- **Groups.** Waterbirds = 27 wetland families (Anatidae, Ardeidae, Rallidae, Scolopacidae,
  Charadriidae, Podicipedidae, Phalacrocoracidae, Alcedinidae and others; 222 species). Land birds =
  all other species.
- **Long term.** SABAP1 (1986-1992) to SABAP2 (2008-2024) change across cells, regressed on the
  change in temperature and log precipitation, with an intercept that absorbs a common protocol
  offset.
- **Species level.** For each of 636 species with at least 500 records: within-cell-half regression of
  log record share on the 24-month rainfall anomaly and the temperature anomaly.

## 4. Results

Spatial gradients were strong (`files/figures/fig1_spatial.png`): CTI rose 0.33 C per 1 C of cell
climatology, and CPI rose 0.32 log units per log unit of cell rainfall (both far outside the
species-shuffle null, p < 0.01).

| Response (all birds unless stated) | Fraction phi | 95% CI |
| --- | --- | --- |
| CTI on temperature trend (main, with controls) | 0.28 | 0.06 to 0.51 |
| CTI on temperature trend, no effort/observer controls | 0.40 | - |
| CTI on temperature trend, year effects (between-cell warming only) | 0.12 | -0.41 to 0.51 |
| CTI on temperature trend, land birds | 0.38 | 0.15 to 0.63 |
| CTI on temperature trend, presence-only CTI | 0.29 | - |
| CTI on year-to-year temperature anomaly | -0.01 | -0.04 to 0.02 |
| CPI on 12-month rainfall anomaly | 0.027 | -0.001 to 0.047 |
| CPI on 24-month rainfall anomaly | 0.053 | 0.008 to 0.092 |
| CPI on 24-month rainfall anomaly, land birds | 0.021 | -0.016 to 0.052 |
| CPI on 12-month rainfall anomaly, waterbirds | 0.18 | 0.05 to 0.36 |
| CPI on 24-month rainfall anomaly, waterbirds | 0.34 | 0.18 to 0.66 |
| CPI on 24-month rainfall anomaly, waterbirds, year effects | 0.30 | 0.11 to 0.61 |
| CPI on rainfall trend | 0.04 | -0.09 to 0.27 |
| SABAP1 to SABAP2, CTI on cell warming (mean +0.57 C) | -0.33 | -1.26 to 0.84 |
| SABAP1 to SABAP2, CPI on cell rainfall change | 0.13 | -0.09 to 0.28 |

`files/figures/fig2_fractions.png` shows these fractions.

**Temperature.** Cells warmed 0.27 C per decade in 2008-2024. CTI rose 0.039 C per decade
(0.095 C per 1 C of cell trend with controls; species-shuffle null mean -0.012, SD 0.026,
p < 0.01). This is 28% of the spatial expectation, in the range of the Swedish birds and above the
75-network trend value of 0.12. Year-to-year temperature anomalies (SD 0.35 C) gave no CTI response.
The regional CTI rose steadily, also in the cool 2021-2022 La Nina years (`fig3_timeseries.png`).
Thus the trend fraction is not separable from other slow changes in the atlas. With year effects,
which remove all region-wide change, the fraction was 0.12 with a wide interval that includes 0.
The cells with slow and fast effort growth gave 0.22 (-0.05 to 0.49) and 0.31 (0.04 to 0.65).
More effort lowered CTI (-0.021 C per log unit; -0.035 to -0.007). The effort, observer and location
controls lowered the fraction from 0.40 to 0.28. The fraction was larger in H2 (0.39) than H1 (0.19).
The SABAP1 to SABAP2 comparison could not test temperature: the 1986-1992 to 2008-2024 warming was
nearly uniform across cells (`fig4_longterm.png`).

**Rainfall.** Rainfall anomalies were large (24-month SD 0.065 log10 units, about +/-16%), and the
regional CPI went up and down with rainfall (`fig3_timeseries.png`), but with a small amplitude.
All birds followed 3-5% of the spatial rainfall gradient. Land birds followed 2% (interval includes 0).
Waterbirds followed 18% within 12 months and 34% over 24 months, also with year effects
(`files/figures/fig5_rain_response.png`). Lagged (previous 12-month) rainfall added a positive term
of the same size as the current term for waterbirds and all birds, so the response builds up over two
years. In dry cell-years (12-month rainfall below 79% of the cell mean; 359 cell-year-halves) waterbird CPI was 0.0025 log
units below the cell mean; in wet years (above 126%; 348) 0.0033 above (SD 0.011).

**Why CPI hardly moves.** Rainfall changed the composition a lot: 143 of 636 species had a
record-share response with |z| > 3 (for example Hamerkop, Black-winged Kite, Zitting Cisticola,
Little Grebe and herons increased after wet periods; Cape Turtle Dove, Laughing Dove, Lark-like
Bunting and Namaqua Sandgrouse decreased). But the response was not related to the species'
spatial rainfall niche: across species, r = 0.04 between the rainfall response and SPI
(record-weighted r = -0.02); for land species r = 0.02, for the 141 waterbird species r = 0.14. Waterbirds as a group
increased in wet periods, and this gives most of the CPI response. Rainfall-driven turnover is real,
but it does not move land communities along their spatial rainfall gradient.

**Long-term rainfall.** The SABAP1 to SABAP2 cross-cell CPI slope gave 0.13 (-0.09 to 0.28). The CTI
of cells that became wetter rose (fraction of the CTI-rainfall spatial slope 0.92, 0.55 to 1.52;
waterbirds 1.52). We do not interpret this term strongly: rainfall change is spatially structured
(east-west), the protocols differ, and 98 cells give one comparison.

## 5. Conclusions

1. The first Southern Hemisphere test of the campaign estimator gives a temperature trend fraction
   (0.28, 0.06-0.51) near the Swedish bird value and above the 75-network value, and a year-to-year
   fraction of zero, as in all earlier networks. The trend fraction depends on the region-wide trend
   and is not separable from slow changes in the atlas (effort doubled); the between-cell estimate is
   uncertain (0.12, -0.41 to 0.51).
2. The hypothesis that birds in a semi-arid region track water instead of heat is not supported for
   the community as a whole: rainfall fractions are 2-5%, smaller than the temperature trend fraction.
   Rainfall drives strong species turnover, but the turnover is almost orthogonal to the spatial
   rainfall niche of the species.
3. Waterbirds are the exception. They follow about one third of their spatial rainfall gradient within
   two years.

## 6. Limitations

- Atlas records are detection/non-detection on cards of variable length (2 hours to 5 days). Record
  weights are reporting rates, not abundance. Detectability may change with rainfall (for example,
  observers visit full wetlands), so the waterbird response can include detection.
- We could not separate ad hoc lists from full-protocol cards through the API facets; ad hoc lists are a
  small part of SABAP2.
- The card count is a proxy (the record count of the most-reported species).
- Observer identity changes were controlled only with summary covariates; no observer fixed effects.
- 1-degree cells mix habitats; the pentad location mix was controlled only with mean latitude and
  longitude.
- Species niches come from the same atlas (2008-2025) and include non-climatic gradients (land cover,
  the fynbos/karoo/savanna biomes). Cross-fitting removes same-cell circularity only.
- Temperature and rainfall windows are fixed (12 and 24 months); CRU TS station density in southern
  Africa decreased after 2000.
- SABAP1 versus SABAP2 compares two different protocols (quarter-degree month lists versus pentad
  cards); the cross-cell design removes only a common offset.
- We fixed the waterbird family list, the 24-month window and the effort split after the first main
  fits; treat them as exploratory.

## 7. Open items for the next worker

- Pentad-level analysis with full-protocol cards only (SABAP2 API `api.birdmap.africa`), with observer
  fixed effects; this would test whether the 0.28 trend fraction is an atlas artefact.
- Species niches from an independent source (for example GBIF density across Africa or BirdLife range
  maps) instead of the atlas itself.
- Waterbird response with a surface-water product (for example JRC Global Surface Water) instead of
  rainfall, to separate wetland filling from detection.
- Other Southern Hemisphere atlases (Kenya, Nigeria and Zambia atlases on GBIF; the Australian atlas).

## 8. Files

- `files/code/` - all code. `run_all.sh` lists the order. `gbif_facets.py` fetches the facet counts
  (resumable); `make_queries.py` builds the query lists; `prepare.py` builds the cross-fitted panel;
  `analysis.py`, `extra.py`, `boot2.py`, `long_term.py`, `species_rain.py` give the results;
  `figures.py` draws the figures.
- `files/data/` - the exact query lists (`q_*.jsonl`), the 1-degree prescan counts, aggregated
  species counts per cell (`s2_counts`, `s1_counts`, `sti_counts`, `month_counts`), card/effort
  metadata without observer names (`*_meta`), the analysis panels (`panel_model`, `panel_extra`,
  `s1_cells`), species indices and names, and all result JSON/CSV files (`results.json`,
  `boot2.json`, `extra.json`, `longterm.json`, `null_shuffle.csv`, `boot.csv`, `species_rain.csv`).
- `files/figures/` - five PNG figures.
- `files/NOTICE.md` - sources, licenses and attribution of the external data.

Reproduce: copy `files/code` and the query lists to an empty scratch folder and run `run_all.sh`
(instructions in the script). GBIF facet counts change slightly as SABAP2 receives new and reviewed
cards; we fetched on 2026-11-11/12 (SABAP2 version 1.87).
