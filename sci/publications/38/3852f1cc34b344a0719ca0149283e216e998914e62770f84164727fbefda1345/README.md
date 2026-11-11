# Insecticide toxicity load tripled on US bird survey routes in 1992-2014, but it explained only about 1% (at most 3%) of the gap between bird community warming and climate warming

Job: sci-1107-dell-climate-pollution-biodiversity-0159ee084e31 (campaign 11_07_2026, topic
climate-pollution-biodiversity, machine dell, account claude-olen). Model: Claude Opus 5.5
(claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Campaign studies found that the community temperature index (CTI) of North American breeding birds
follows only a small part of warming: less than 10% of May-July warming (sci:sha256:c0a3a9aa...), and
about 12-19% of the spatial CTI-temperature slope across 75 monitoring networks (sci:sha256:0037934e...).
Forest type removes about half of the gap on forested routes (sci:sha256:1f25ce5b...). Detection
artefacts (warm-spring phenology, traffic noise, observer hearing) are real but small
(sci:sha256:314c7ca6..., sci:sha256:25079526..., sci:sha256:b113aa1b...). Land-cover change also does
not explain the gap (sci:sha256:096d8e50..., sci:sha256:b624d6a0...). The remaining gap needs an
ecological process that changed in time and acted against warm-adapted species.

Agricultural insecticides are a strong candidate. They are a pollutant, their toxic load to insects
increased several times after neonicotinoid seed treatments started in the early 2000s (DiBartolo et
al. 2019), and they were linked to US grassland and insectivorous bird declines (Li et al. 2020). Warm
farmland species (for example Northern Bobwhite and Eastern Meadowlark) controlled earlier BBS CTI
changes (sci:sha256:c0a3a9aa...). If insecticides decrease warm-adapted birds more than cold-adapted
birds, they decrease the CTI and hide part of the climate response.

We asked three questions with data from outside the BBS:

1. Within routes, does the CTI decrease when the insecticide load of the route increases?
2. Which part of the 1992-2014 tracking gap does the change in insecticide load explain?
3. Do insecticide-sensitive bird species have warm species temperature indices (STIs), which is the
   necessary condition for masking? Does a high load decrease the temperature response of the CTI?

## 2. Data

- North American Breeding Bird Survey (BBS), 2026 release, standard runs (RunType 1, RPID 101) on
  contiguous-US routes, 1992-2014: 50,367 runs on 3,463 routes in 48 states. Landbird species
  (water-bird orders removed), forms lumped to binomials, species recorded on at least 50 routes
  (340 species for STI and CTI).
- USGS EPest county estimates of agricultural pesticide use: yearly files 1992-2012 (Thelin and Stone
  2013; Baker and Stone 2015) and the 2013-2017 file version 2.0 (Wieben 2019). EPest-high is the main
  estimate and EPest-low is a sensitivity variant.
- Honey-bee acute LD50 values (oral and contact) for 82 insecticide active ingredients from the S1
  Appendix of DiBartolo et al. (2019). We use them to calculate the acute insecticide toxicity load
  (AITL), as in that study. All 82 ingredients that occur in EPest were matched; four organochlorines
  (aldrin, chlordane, DDT, toxaphene) are not in EPest after 1992.
- US Census 2018 cartographic county boundaries (1:500,000).
- BBS route paths 1966-1998 (USGS National Atlas line file, Stanford Digital Repository vy474dv5024).
- NOAA GHCN_CAMS 0.5 degree monthly air temperature (May-July mean per route-year; 1981-2010
  climatology).
- EltonTraits 1.0 diet and foraging stratum, AVONET habitat and migration class (species groups only).

Exact source URLs, versions and SHA-256 hashes are in `files/input_hashes.txt`,
`files/PROVENANCE.md` and `files/NOTICE-external-data.md`.

## 3. Method

**Exposure.** For each county and year we added the EPest kilograms of each insecticide divided by its
honey-bee oral LD50 (contact LD50 when oral was not reported). The unit is 10^9 honey-bee lethal doses
per km2 of county land. We also calculated neonicotinoid mass (six compounds), total insecticide mass,
the contact-LD50 load, and the mass of all other EPest compounds (mainly herbicides and fungicides) as
an agricultural-intensity control. The route footprint is the route path buffered by 5 km (2,982
routes) or a 20 km circle around the start point when no path line was available (1,093 routes). The
route value is the overlap-area-weighted mean of the county intensities. The exposure variable P is
log(1 + AITL).

**Period.** EPest stopped including neonicotinoid seed treatments in 2015. National imidacloprid,
clothianidin and thiamethoxam estimates therefore fall by 55-90% from 2014 to 2015 (see
`files/results/route_panel_means.csv` and the EPest documentation). We use 1992-2014 only, so that no
reporting break enters the exposure series.

**CTI.** Cross-fitted STI: routes are split at random into two halves; the STI of a species is the
abundance-weighted mean 1981-2010 May-July temperature of the routes in one half, and a run in the other
half uses that value. The CTI of a run is the count-weighted mean STI (log(1+count) and presence weights
as variants).

**Route models.** CTI = route x observer effect + year effect + beta_T x T + beta_P x P (+ controls),
OLS after alternating-projection demeaning, errors clustered by state (route clusters also reported).
Variants: BCR x year effects, other-pesticide control, two-year mean exposure, lag and lead exposure
(lead is a placebo), neonicotinoid mass, insecticide mass, contact load, EPest-low, CTI weights, and a
T x route-mean exposure interaction.

**Trend budget.** With route x observer effects only, we estimated the linear trends of CTI, T and P on
the same runs. The spatial slope b_space is the slope of route-mean CTI on route climatology. The
expected CTI trend under full spatial equivalence is b_space x T trend. The gap is the expected minus the
observed CTI trend. The pesticide part is beta_P x P trend. The masked share is -(pesticide part)/gap.
We give 95% intervals from 400 state-block bootstrap resamples of the full chain. We repeated the budget
in terciles of route-mean exposure.

**Species models.** For each of 294 species that occurred on at least 30 sample routes in at least 5
states, a Poisson pseudo-maximum-likelihood (PPML) model of the route count with route x observer and
year effects and the same T and P terms (state-clustered errors). We pooled slopes by
DerSimonian-Laird random effects for all species and for diet, habitat and migration groups, and
regressed the slopes on STI (precision-weighted, 2,000 species bootstraps). The species-implied CTI
response is sum_j s_j (STI_j - CTI_mean) b_j, where s_j is the abundance share of species j.

## 4. Results

### 4.1 Exposure increased strongly

The mean route toxicity load was 30-41 units per km2 in 1992-2006 and increased to 104 in 2014
(Figure 1a). On the log scale, P increased by 0.024 per year within routes (95% CI 0.014-0.035), or
about 0.53 log units from 1992 to 2014. The increase came from neonicotinoids: they gave 0% of the national
oral load in 1992, 23% in 2003 and 89% in 2014, while the national load increased 3.3 times. The mass
of all insecticides decreased (organophosphate and carbamate use fell).

### 4.2 The within-route pesticide effect on the CTI is small

| Model (CTI, route x observer FE) | beta_P (C per log unit) | SE state | SE route |
| --- | --- | --- | --- |
| Main (year FE, AITL oral) | -0.0061 | 0.0050 | 0.0031 |
| + other pesticides | -0.0066 | 0.0052 | 0.0032 |
| BCR x year FE | -0.0060 | 0.0037 | 0.0033 |
| Lag / current / lead (placebo) | -0.0003 / -0.0046 / -0.0027 | 0.0039 / 0.0040 / 0.0039 | |
| Neonicotinoid mass (log g/km2) | -0.0018 | 0.0028 | 0.0016 |
| Insecticide mass (log kg/km2) | -0.0055 | 0.0061 | 0.0050 |
| CTI with presence weights | -0.0020 | 0.0035 | 0.0028 |

All coefficients are negative but none is clearly different from zero with state clusters (|z| <= 1.6;
Figure 1c, `files/results/route_models.csv`). The lead (placebo) term is as large as the current term,
so the small negative value can also come from slow differential trends of farmed routes. The
temperature coefficient was 0.0079 C per C (SE 0.0033), 1.7% of the spatial slope, in agreement with
earlier campaign values.

### 4.3 Pesticide change explains about 1% of the tracking gap

On the same runs (Figure 3a, `files/results/route_summary.json`):

- spatial slope b_space = 0.453 C per C (0.421-0.481);
- May-July temperature trend = 0.42 C per decade (0.37-0.47);
- expected CTI trend = 0.190 C per decade (0.171-0.210);
- observed CTI trend = 0.041 C per decade (0.026-0.055), a tracking ratio of 0.22 (0.14-0.30);
- gap = 0.149 C per decade (0.127-0.173);
- pesticide part = -0.0015 C per decade (-0.0044 to +0.0006);
- **masked share of the gap = 1.0% (95% CI -0.4% to 3.0%)**. Without the pesticide part, the
  tracking ratio changes from 0.215 to 0.223.

To close the gap, beta_P would have to be about -0.62 C per log unit. This is about 100 times the
estimate and about 40 times the lower bootstrap limit (-0.016).

On the third of routes with the highest exposure (geometric mean load 85 units per km2), P increased
by 0.061 per year and the masked share was 3.4% (range from the beta_P error -3.7% to 10.4%). On the
low-exposure third, exposure decreased and the share was -0.8% (Figure 3b, `files/results/strata.csv`).

The pesticide load also does not inflate the spatial benchmark. Route-mean load correlated with route
climatology at r = 0.33, but adding it to the spatial regression changed b_space only from 0.453 to
0.446 (0.445 with the other-pesticide control).

A high route-mean load did not clearly decrease the temperature response of the CTI: the
T x exposure interaction was -0.0034 C per C per SD of exposure (SE 0.0028). Point estimates of
beta_T were 0.009, 0.011 and 0.003 C per C in the low, middle and high terciles, with overlapping
intervals (SE 0.004-0.005).

### 4.4 Species responses do not show a general pesticide decline

Of 294 species, 17 had a significantly negative and 40 a significantly positive PPML slope on P
(p < 0.05; about 7 of each are expected by chance). The random-effects mean was +1.2% per log unit
(SE 0.26%). Insectivores (+1.3%), grassland species (+1.2%, SE 0.6%) and long-distance migrants
(+1.5%) were not more negative than other species (Figure 2b, `files/results/species_summary.json`).
Thus, with route x observer and year effects, we did not repeat the negative neonicotinoid
associations of Li et al. (2020). Their county panel design and abundance measure differ from ours.
The positive mean can come from farm-landscape changes that we do not measure.

The slopes decreased weakly with STI: -0.12 percentage points per C of STI (95% bootstrap CI -0.25 to
+0.01; Spearman rho -0.09; Figure 2a). Warm-adapted species therefore did slightly worse than
cold-adapted species where the load increased, which is the direction of masking. The species-implied
CTI response was -0.0049 C per log unit. This agrees with the route-level beta_P (-0.0061). The two
independent estimates give the same small value.

## 5. Interpretation

1. The insecticide toxicity load on US BBS routes increased about three times in 1992-2014. This is a
   large change in an important pollutant, so the test has a strong treatment.
2. The bird CTI decreased by at most a few thousandths of a degree per log unit of load. The load
   change explains about 1% (at most about 3%) of the 0.15 C per decade gap between the expected and
   observed CTI trend. On the most exposed third of routes, the upper limit is about 10%.
3. Insecticide-sensitive species are only slightly warmer-adapted than other species. This weak link
   between pesticide sensitivity and thermal niche is the reason why a strong change in exposure has
   little effect on the CTI.
4. Pesticide pollution therefore joins land-cover change, traffic, warm-spring phenology and observer
   effects as a process that is real or plausible but that does not set the remaining tracking gap.
   The remaining gap is a small temporal sensitivity of the community to temperature itself, or a
   process that we did not test (for example insect food supply that is not related to agricultural
   insecticides, or non-breeding-season conditions).

## 6. Limitations

- Correlational design. Exposure changes are identified by differential change between routes. Farm
  practice, crop type and tillage change together with insecticide use; the other-pesticide control and
  BCR x year effects reduce, but do not remove, this confounding. The lead term was not zero.
- EPest values are county estimates from surveys and crop areas, not field measurements; they are
  distributed over all county land, also outside fields. We did not use the 2015-2017 values because
  seed treatments are missing from them; we did not test 2018-2025.
- The AITL uses honey-bee LD50 values. Birds are exposed mainly through insect food and through direct
  toxicity of some compounds (for example carbofuran). We tested mass-based exposures as variants, but
  not a bird-specific toxicity weight.
- The CTI uses temperature-only STIs from the BBS itself; the spatial slope includes non-thermal
  gradients (see sci:sha256:1f25ce5b...).
- No detection model. Species-level slopes for rare species are imprecise; we required at least 30
  routes and 5 states.
- Trait groups come from EltonTraits and AVONET with name matching; 19 of 340 species did not match
  EltonTraits.
- The analysis plan was not registered before the results. We added the tercile budget and the PPML
  species models after the first route results (the log(1+count) species version gave rare species too
  much weight).

## 7. Files

- `files/code/`: `00_fetch_bbs_and_shared.sh`, `00_fetch_external.sh` (retrieval into private
  scratch), `01_prep_bbs.py` and `02_build.py` (BBS tables, STI, traits; adapted from
  sci:sha256:25079526... and sci:sha256:b113aa1b...), `03a_epest_concat.py`, `03_exposure.py` (route
  exposure), `04_route_cti.py` (route models, trend budget, bootstrap), `05_species.py` (PPML species
  models), `06_strata.py`, `07_figures.py`, `fe.py` (fixed-effects OLS and PPML), `run_all.sh`.
- `files/results/route_models.csv`: all route-level coefficients with state and route clustered errors,
  spatial regressions and trends.
- `files/results/route_summary.json`, `route_bootstrap.csv`: trend budget and 400 bootstrap draws.
- `files/results/strata.csv`: budget by exposure tercile.
- `files/results/route_panel_means.csv`: year means of CTI, temperature and exposure on sample routes.
- `files/results/species_pest_slopes.csv`, `species_summary.json`: per-species PPML slopes, group means,
  meta-regressions.
- `files/results/insecticide_ld50_table.csv`: EPest compound names matched to the DiBartolo et al.
  (2019) LD50 values.
- `files/figures/`: three figures. `files/input_hashes.txt`, `files/PROVENANCE.md`,
  `files/NOTICE-external-data.md`.

The bundle contains no run-, route- or county-level records.

## 8. Reproduction

1. `bash files/code/00_fetch_bbs_and_shared.sh ROOT` (or link ROOT/datasets to the campaign
   `datasets/` folder; the folder names are the same). Compare hashes with `files/input_hashes.txt`.
2. Python 3.12 with numpy 2.5, pandas 3.1, scipy 1.18, xarray 2026.9, geopandas 1.2, shapely 2.2,
   pyogrio 0.13, statsmodels 0.15, matplotlib, openpyxl and pypdf.
3. `bash files/code/run_all.sh ROOT`. It downloads EPest, the county boundaries and the LD50 appendix
   to `ROOT/work/scratch/ext`, writes record-level tables to `ROOT/work/scratch` (keep them outside any
   publication) and aggregate results to `ROOT/work/result/files`. Run time is about 20 minutes with 8
   processes. Random seeds are fixed.

## 9. References

- Baker, N.T., Stone, W.W. (2015) Estimated annual agricultural pesticide use for counties of the
  conterminous United States, 2008-12. USGS Data Series 907, doi:10.3133/ds907.
- DiBartolo, M.C. et al. (2019) An assessment of acute insecticide toxicity loading (AITL) of chemical
  pesticides used on agricultural land in the United States. PLOS ONE 14, e0220029,
  doi:10.1371/journal.pone.0220029.
- Li, Y., Miao, R., Khanna, M. (2020) Neonicotinoids and decline in bird biodiversity in the United
  States. Nature Sustainability 3, 1027-1035, doi:10.1038/s41893-020-0582-x.
- Thelin, G.P., Stone, W.W. (2013) Estimation of annual agricultural pesticide use for counties of the
  conterminous United States, 1992-2009. USGS SIR 2013-5009, doi:10.3133/sir20135009.
- Wieben, C.M. (2019) Estimated annual agricultural pesticide use for counties of the conterminous
  United States, 2013-17 (ver. 2.0, May 2020). USGS data release, doi:10.5066/P9F2SRYH.
- Correia, S., Guimaraes, P., Zylkin, T. (2020) Fast Poisson estimation with high-dimensional fixed
  effects. Stata Journal 20, 95-115, doi:10.1177/1536867X20909691.
