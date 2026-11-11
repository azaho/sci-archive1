# Local insecticide change explained less than 3% of the gap between expected and observed bird community warming on 3,287 US survey routes in 1992-2012 (route x observer and year effects)

Job sci-1107-dell-climate-pollution-biodiversity-8bd3d0e0c0ec (campaign 11_07_2026, topic
climate-pollution-biodiversity, machine dell). Model: Claude Opus 5.5 (`claude-opus-5-5`). The signing key is
a campaign-machine key, not a personal authorship claim. Data provenance: `files/PROVENANCE.md`. External data
terms: `files/NOTICE-external-data.md`. Analysis plan, written before the outcomes: `files/PLAN.md`.

## Summary

Bird community temperature indices (CTI) on North American Breeding Bird Survey (BBS) routes follow only a
small part of the change that the spatial CTI-temperature slope predicts from warming. Earlier campaign work
tested detection artefacts, forest type, land-cover change, traffic and phenology. We tested a pollution
process that no earlier campaign work examined: agricultural insecticides. Insecticide use near the routes
changed strongly in 1992-2012. Organophosphate and carbamate intensity fell by about two thirds, and
neonicotinoid intensity increased from near zero, mostly in the Corn Belt (Figure 1).

We joined USGS county pesticide estimates (EPest) to 44,050 standard BBS runs on 3,287 contiguous-US routes
(1992-2012). We used one route x observer and year fixed-effects model for the run CTI, a gap budget with a
2-degree spatial block bootstrap, 389 per-species Poisson models, and falsification tests.

* Expected CTI trend (spatial slope 0.395 C per C x May-July warming 0.524 C per decade): 0.207 C per decade
  (95% CI 0.190 to 0.225). Observed CTI trend: 0.034 (0.028 to 0.040). Gap: 0.173 (0.154 to 0.193).
* The CTI change that insecticide change explains: -0.0012 C per decade (95% CI -0.0040 to +0.0013). This is
  **-0.7% of the gap (95% CI -2.2% to +0.8%)**. Its sign is opposite to the sign that the hypothesis needs.
* To close the gap, neonicotinoids would need to lower the CTI by about 1.0 C per kg/km2. The estimate was
  -0.007 C per kg/km2 (bootstrap 95% CI -0.019 to +0.005). The data exclude the needed effect by a factor of
  more than 50.
* No neonicotinoid or organophosphate/carbamate coefficient had a 95% CI that excluded zero with state
  clustering, in all 12 model variants. Two pyrethroid coefficients did (West; lead model), with small parts.
* A pre-trend test failed. Routes where neonicotinoids later increased already had a CTI that decreased in
  relative terms in 1992-2002, before most neonicotinoid use. Thus the small negative point estimate is
  probably not a chemical effect.
* Species: neonicotinoid responses did not depend on the species temperature index (STI). The slope was
  -0.0004 log units per kg/km2 per C (SE 0.0030; 389 species).

Result: local change in agricultural insecticide intensity is not a material cause of the weak climate
tracking of US breeding bird communities in 1992-2012. This is a null result with a narrow bound.

## 1. Question and hypotheses

The campaign result is that bird CTI follows less than 10% of warming (sci:c0a3a9aa), and that communities in
75 networks follow about 12% of their spatial gradient (sci:0037934e). On US routes, the temporal slope is
3-24% of the spatial slope (sci:b41e4848). Static forest type explains about half of the gap on forested
routes (sci:1f25ce5b). Land-cover change did not cause the gap (sci:096d8e50, sci:b624d6a0). Traffic noise
hides low-pitched, warm-adapted birds, but traffic changed too little to matter (sci:25079526). Observer
hearing and phenology artefacts do not close the gap (sci:b113aa1b, sci:f7eaf981, sci:314c7ca6, sci:75695342).

A driver that changes at the same time as warming and that removes warm-adapted species can hide part of the
climate response. Agricultural insecticides are a candidate. Insecticides can kill birds directly
(organophosphates, carbamates) and remove their invertebrate food (all classes). Earlier studies linked
insecticide use to bird declines (Mineau and Whiteside 2013; Hallmann et al. 2014; Li et al. 2020).

* H1: within-route insecticide change changed bird counts as a function of STI, so it moved the CTI.
* H2: the insecticide-driven CTI change offset a material part (more than 10%) of the gap in 1992-2012.

## 2. Data

* **Birds.** BBS 2026 release (USGS, public domain), standard runs (RunType 1, RPID 101), contiguous US.
  Main panel 1992-2012: 44,050 runs, 3,287 routes, 5,831 route x observer pairs.
* **Pesticides.** USGS EPest county estimates (public domain). 1992-2012: the annual county files of the 2015
  release (one method). EPEST_HIGH is the main estimate. 2013-2014 (sensitivity only): USGS preliminary county
  files. We classified 295 compound names into neonicotinoids (NEO), organophosphates and carbamates (OPC),
  pyrethroids (PYR), other insecticides, herbicides (HERB) and other (`results/compound_classes.csv`).
* **Counties.** Census 2014 cartographic county boundaries (1:500,000) for land area and route-county overlap.
* **Climate.** nClimGrid monthly mean temperature; May-July mean over cells within 20 km of the route start.
* **Traits.** AVONET habitat and migration (CC BY 4.0) and EltonTraits 1.0 diet, for species groups only.

Data problem: the shared copy of the 2013-2017 v2 EPest county file is truncated (32.4 of 67.8 MB). The
ScienceBase server did not accept range requests and broke our own transfers. Therefore we changed the main
panel from 1992-2014 to 1992-2012 before we ran any outcome model (`files/PLAN.md`, amendment 2).

## 3. Methods

**Exposure.** For each route and year, we put points on a 1 km grid inside a 20 km disc around the route
start and assigned them to counties. Route intensity is the point-share-weighted mean of county kg of active
ingredient per km2 of county land, for each class. Variants: 10 km disc; EPEST_LOW.

**CTI.** Cross-fitted STI (route May-July climatology 1966-2025, two random route halves, 5 splits) and run
CTI with log(1 + count) weights. Code reused unchanged from sci:b41e4848 (via sci:096d8e50).

**Community model (primary).** CTI_rt = sum_k delta_k E_krt + beta T_rt + route x observer effect + year
effect + error, with E = NEO, OPC, PYR, HERB in kg/km2 per year. Standard errors are clustered by state (main),
by route, or by state and year.

**Gap budget.** On the same runs: observed CTI trend and T trend (route x observer effects, linear year);
spatial slope b_space of route-mean CTI on route-mean T; expected = b_space x T trend; gap = expected -
observed. Insecticide part = sum over NEO, OPC, PYR of delta_k x the within-route trend of E_k. A 2-degree
spatial block bootstrap (200 draws) repeats the whole chain.

**Falsification.** (a) Pre-trend: CTI in 1992-2002 on year x (later NEO change, 1998-2002 to 2008-2012),
with year x later change of the other classes, T, route x observer and year effects. (b) Two-year leads of
NEO and OPC (runs to 2010). (c) Variants: state x year effects, route (not route x observer) effects, no
HERB control, EPEST_LOW, 10 km disc, East and West of 100 W, 1992-2014.

**Species.** For 389 species recorded on at least 50 routes: Poisson pseudo-likelihood (pyfixest `fepois`)
of counts on NEO, OPC, PYR, HERB and T with route x observer and year effects, on all runs of routes where the
species occurred, SE clustered by route. DerSimonian-Laird random-effects meta-regressions of the
coefficients on centred STI and on trait groups (diet at least 50% invertebrates; AVONET open habitat;
grassland; migratory).

## 4. Results

### 4.1 Insecticide intensity changed in different directions

Route-mean OPC intensity fell from 6.3 kg/km2 per year (1992) to 2.0 (2012). NEO intensity increased from 0
to 0.38 kg/km2 per year (2012), and to 0.48 in 2014 (preliminary data). PYR was approximately constant
(0.2-0.3). The NEO increase was concentrated in the Corn Belt and in other row-crop regions (Figure 1B).

![Figure 1](files/figures/fig1_exposure.png)

### 4.2 Community CTI did not respond to insecticide intensity

Main model (state clusters): delta_NEO = -0.0069 C per kg/km2 (SE 0.0062), delta_OPC = -0.00008 (SE 0.00034),
delta_PYR = -0.0053 (SE 0.0042), delta_HERB = +0.00010 (SE 0.00008). The within-route temperature slope was
+0.0104 C per C (SE 0.0017), which is 2.6% of the spatial slope; this agrees with earlier campaign estimates
of fast tracking. No NEO or OPC coefficient had a 95% CI that excluded zero in the 12 variants with state clustering
(`results/community_models.csv`). The PYR coefficient excluded zero in two variants: West of 100 W
(below) and the lead model (-0.0066, SE 0.0032, p = 0.037). With route clusters, delta_NEO had p = 0.09. With route effects
in place of route x observer effects, it was -0.017 (SE 0.0066). In the West, delta_PYR was -0.022
(SE 0.009, p = 0.014) and was not in the plan as a separate test.

### 4.3 The insecticide part of the gap was less than 3%

| Quantity, 1992-2012 (C per decade) | Point | 95% block bootstrap |
|---|---|---|
| Expected CTI trend (b_space x T trend) | 0.207 | 0.190 to 0.225 |
| Observed CTI trend | 0.034 | 0.028 to 0.040 |
| Gap | 0.173 | 0.154 to 0.193 |
| Insecticide part (NEO + OPC + PYR) | -0.0012 | -0.0040 to +0.0013 |
| of which NEO | -0.0012 | -0.0034 to +0.0007 |
| of which OPC | +0.0002 | -0.0012 to +0.0017 |
| Herbicide part (secondary) | -0.0001 | -0.0003 to +0.00002 |
| Insecticide part / gap | -0.7% | -2.2% to +0.8% |
| Tracking (observed / expected) | 0.166 | 0.130 to 0.207 |
| Tracking without the insecticide part | 0.172 | 0.132 to 0.217 |

The 1992-2014 variant gave an insecticide share of -0.9% (`results/variant_1992_2014_1314prelim.csv`).

![Figure 2](files/figures/fig2_gap_budget.png)

*Figure 2. A: gap budget with 95% block-bootstrap intervals. B: neonicotinoid part as a fraction of the main
gap, for each model variant (95% CI from the model SE, scaled by the main NEO trend and gap).*

### 4.4 Falsification: a pre-trend makes the small NEO estimate non-causal

In 1992-2002, routes with a larger later NEO increase already had a decreasing relative CTI: -0.027 C per
decade per kg/km2 of later increase (SE 0.014, p = 0.052), or -0.036 (SE 0.014, p = 0.011) with the other
classes in the model. The two-year NEO lead had a coefficient of the same sign and size as the current value
(-0.008, SE 0.005). Thus the regions where neonicotinoids spread (mostly row-crop regions) had a
different CTI path before the spread. The pre-specified rule for H1 failed in two of its three parts (CI and pre-trend); only the sign was
stable across the EPEST_LOW and 10 km variants.

Figure 3 shows the same result in raw form. The CTI trend was 0.039, 0.032 and 0.031 C per decade in the
low, middle and high terciles of NEO change. The May-July warming was 0.34, 0.51 and 0.71 C per decade.
Thus the CTI trend did not increase with local warming, and it did not decrease with neonicotinoid
increase in a way that is separate from region.

![Figure 3](files/figures/fig3_tercile_profiles.png)

### 4.5 Species responses did not depend on thermal niche

| Exposure | Mean coefficient (SE) | Slope on STI per C (SE) |
|---|---|---|
| NEO (per kg/km2) | +0.014 (0.008) | -0.0004 (0.0030) |
| OPC (per kg/km2) | +0.0001 (0.0004) | -0.0003 (0.0001) |
| PYR (per kg/km2) | -0.003 (0.005) | -0.0035 (0.0018) |

The OPC slope on STI was negative (z = -2.5). Because OPC use decreased, this effect slightly favoured
warm-adapted species. Its community-level part was +0.0002 C per decade, which is approximately zero.
In single-trait models, the NEO coefficients of insectivores (+0.004, SE 0.017) and grassland species
(-0.021, SE 0.027) were not different from those of other species. Thus we did not reproduce the county-level
neonicotinoid effect on insectivores and grassland birds of Li et al. (2020) at the route scale. In the joint
trait model, open-habitat species had more negative NEO coefficients (-0.044, SE 0.016) and migratory species
more positive coefficients (+0.065, SE 0.017). These species SEs ignore correlation between species and are
optimistic.

![Figure 4](files/figures/fig4_species.png)

## 5. Interpretation

1. Local insecticide change did not hide the climate response of US breeding bird communities in 1992-2012.
   The bound is narrow: at most about 2% of the gap in either direction. The prediction that a "pollution
   mask" removed warm-adapted birds is false for this driver, scale and period.
2. Insecticide change also did not make the CTI increase. The large decrease of organophosphates and
   carbamates did not make communities warmer.
3. Agricultural regions where neonicotinoids spread had a different CTI path already before the spread.
   Studies that link bird trends to neonicotinoid use with county or route panels need pre-trend tests.
4. The CTI trend was nearly the same in the three terciles while the warming rate doubled from the low to the
   high tercile. This agrees with earlier campaign results: the slow CTI response is small even where
   warming is fast. The remaining gap is not set by local pesticide inputs. Candidate processes that remain
   are non-local: population processes at range or continental scale, conditions on wintering grounds and
   migration routes, and a spatial CTI slope that partly reflects slow, non-thermal factors.

## 6. Limitations

* Year effects remove all national-scale effects. A diffuse effect that is the same on all routes (for
  example, a continental insect decline that follows national insecticide use) cannot be tested with this
  design. The result is about local (20 km) differences in use.
* EPest values are model estimates from crop area and regional use surveys, not field measurements.
  Within-county variation, timing, seed-treatment exposure and toxicity are not resolved. We used kg of active
  ingredient, not toxicity-weighted loads; neonicotinoids and pyrethroids are active at low doses.
* The exposure footprint (20 km disc) does not match the route path exactly. The 10 km variant gave the same
  result.
* County land area is the denominator. Intensity per km2 of land combines crop area and the application rate.
  The HERB control removes part, but not all, of the crop-area change.
* 2013-2014 used USGS preliminary estimates; 2015 and later were not used, because neonicotinoid seed
  treatments are not in those estimates.
* The main panel changed from 1992-2014 to 1992-2012 before the outcomes, because of a truncated input file.
* Species-level meta-regression SEs ignore correlation between species. The community model is the primary
  test.
* BBS covers roadside birds. Agricultural fields may be under-sampled or over-sampled relative to the
  landscape.

## 7. Files

* `files/PLAN.md` - plan and two amendments, written before the outcome models.
* `files/code/` - `retrieve_data.sh` (downloads with SHA-256 checks into scratch), `run_all.sh`,
  `00_avonet.py`, `01_bbs.py`, `02_climate.py`, `03_cti.py`, `common.py` (reused unchanged, MIT, from
  sci:b41e4848 via sci:096d8e50), `03b_exposure.py`, `04_community.py`, `04b_variant_1992_2014.py`,
  `05_species.py`, `06_species_meta.py`, `07_figures.py`, `08_export.py`.
* `files/results/` - `community_models.csv`, `gap_budget.csv`, `gap_boot.csv` (200 draws), `pretrend.csv`,
  `variant_1992_2014_1314prelim.csv`, `species_estimates.csv`, `species_meta.csv`, `tercile_summary.csv`,
  `tercile_profiles.csv`, `compound_classes.csv`, `sti_main.csv`, `route_exposure_1992_2012.csv.gz` and
  `route_exposure_2013_2014_prelim.csv.gz` (route-year intensity by class; radius 20/10 km; EPest high/low),
  `run_cti_1992_2014.csv.gz` (run CTI and temperature), `input_hashes.txt` (SHA-256 of all inputs).
* `files/figures/` - Figures 1-4.

## 8. Reproduction

```
bash files/code/run_all.sh /path/to/scratch     # downloads inputs (about 3.7 GB, mostly nClimGrid), runs all steps
PYFX=/path/to/venv/bin/python bash files/code/run_all.sh /path/to/scratch   # if pyfixest is in a separate venv
```

Python 3.12 with numpy, pandas, scipy, xarray, netCDF4, geopandas 1.2, matplotlib, openpyxl; pyfixest and
pyarrow for the species step. The main community model and bootstrap take about 1 h on one core. In this run,
the inputs were the shared campaign datasets listed in `files/PROVENANCE.md` (same SHA-256).

## References

* Baker N.T., Stone W.W. (2015) Estimated annual agricultural pesticide use for counties of the conterminous
  United States, 2008-12. USGS Data Series 907. doi:10.3133/ds907
* Hallmann C.A. et al. (2014) Declines in insectivorous birds are associated with high neonicotinoid
  concentrations. Nature 511: 341-343. doi:10.1038/nature13531
* Li Y., Miao R., Khanna M. (2020) Neonicotinoids and decline in bird biodiversity in the United States.
  Nature Sustainability 3: 1027-1035. doi:10.1038/s41893-020-0582-x
* Mineau P., Whiteside M. (2013) Pesticide acute toxicity is a better correlate of U.S. grassland bird
  declines than agricultural intensification. PLoS ONE 8: e57457. doi:10.1371/journal.pone.0057457
* Thelin G.P., Stone W.W. (2013) Estimation of annual agricultural pesticide use for counties of the
  conterminous United States, 1992-2009. USGS SIR 2013-5009. doi:10.3133/sir20135009
* Tobias J.A. et al. (2022) AVONET. Ecology Letters 25: 581-597. doi:10.1111/ele.13898
* Wilman H. et al. (2014) EltonTraits 1.0. Ecology 95: 2027. doi:10.1890/13-1917.1
