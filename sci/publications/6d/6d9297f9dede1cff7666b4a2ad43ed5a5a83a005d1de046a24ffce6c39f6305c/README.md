# Modelled ozone anomalies did not decrease next-year butterfly population growth on 2,844 UK transects in 1990-2023

## Summary

Ground-level ozone damages many plants. Laboratory studies show that insects that eat
ozone-exposed plants can grow more slowly. We tested whether this effect is visible in field
populations of UK butterflies.

We used 360,709 year-to-year changes of butterfly site indices from 2,844 UK Butterfly
Monitoring Scheme (UKBMS) transects and 60 species, 1990-2023. We added modelled April-September
ozone exposure from the EMEP MSC-W model (0.1 degree, rv5.6, one model version for all years).
The models compare each site with itself, and remove all national year effects for each
species. Thus, the ozone slope comes only from spatial differences in the ozone anomaly
of a year. The models also control for temperature, rain, solar radiation, winter temperature,
nitrogen deposition and population density.

Main result (pre-specified primary test): a site-year with AOT40 ozone exposure 1 SD
(1.04 ppm h) above its expected value had next-year growth that was 0.30% lower
(95% CI -1.48% to +0.88%; SE clustered by year; year-permutation p = 0.45, 499 permutations).
Thus, we did not find an ozone effect. Effects larger than about 1.5% lower growth per SD are
improbable in this design.

Other results:

- Legume-feeding species did not have more negative ozone slopes. Legumes are among the most
  ozone-sensitive plant families. Their slope difference from grass feeders was +2.25
  (SE 1.38, x100 log units), the opposite of the prediction.
- A stomatal-flux measure (POD1, semi-natural vegetation) gave a small negative slope
  (-0.70, SE 0.32). This slope became -0.26 (SE 0.38) with an NO2 control and -0.62 (SE 0.39)
  with site-by-species linear trends. We do not consider it robust.
- Mean ozone and monthly maximum ozone gave negative slopes (-1.12 and -0.99). But within-site
  mean-ozone anomalies had a correlation of -0.93 with NO2 anomalies. With an NO2 control, the
  mean-ozone slope changed sign (+1.55, SE 1.13). The two pollutants cannot be separated
  with these data.
- Outside southern England, the AOT40 slope was negative (-3.92, SE 1.15). Exploratory checks
  showed that this is not an ozone timing effect. Ozone from two years after the growth
  interval gave the same slope (-4.65). The slope went to -0.82 with an NO2 control and to +1.57
  with site-by-species trends. It was positive in 1990-2006 (+3.58) and negative in 2007-2023
  (-4.85). The most likely cause is that ozone and butterfly numbers had different long-term
  trends at the same sites (for example, ozone increased where NOx emissions decreased).

Limitations: the ozone values are model output, not measurements at the transects. The design
uses only spatial differences within a year, which are about 13% of the AOT40 variance.
Thus, the test cannot show an effect of the national ozone decrease since 1990. The
Wider Countryside Butterfly Survey replication in the analysis plan was not possible, because
the public site-index file does not include WCBS squares.

## 1. Question

Does high growing-season ozone at a site decrease butterfly population growth to the next
year, after control for weather and nitrogen deposition? If it does, is the effect larger for
species whose larvae eat ozone-sensitive legumes (Fabaceae)?

Earlier campaign work found no robust ozone link to US bird counts
(sci:sha256:2603c41c..., sci:sha256:1476b687...) and found that nitrogen deposition did not
explain UK butterfly trends (sci:sha256:e3ea428c..., sci:sha256:8373d13e...). No campaign
publication had tested ozone and insect populations in the field.

## 2. Data

| Data | Use | Licence |
|---|---|---|
| UKBMS site indices 1976-2024 and site locations (EIDC 2024 release) | response | OGL v3 |
| EMEP MSC-W rv5.6 monthly fields 1990-2024, 2025 reporting, 0.1 deg | ozone, NO2, N deposition | NLOD 2.0 / CC BY 4.0 |
| E-OBS v31.0e daily tg, rr, qq, 0.25 deg | weather controls | ECA&D / Copernicus terms |

Exact URLs, file hashes and attribution are in `files/provenance/PROVENANCE.md` and
`files/NOTICE-external-data.md`. The raw and record-level data are not bundled.

We used only standard UKBMS transects (Survey_type UKBMS). A site index of -2 means
"not enough visits" and we removed it. Each record is a pair of consecutive years for one
site and species, with a valid index in both years and a non-zero index in at least one year.
The 2,844 transects had 360,709 pairs for 60 species and growth years 1990-2023.

## 3. Method

Response: r = log(I(t+1) + 1) - log(I(t) + 1).

Ozone exposure for year t at the nearest EMEP cell:

- AOT40 for forests, summed April-September (primary, ppb h);
- POD1 for semi-natural vegetation (stomatal ozone flux), summed April-September;
- mean surface ozone and mean monthly maximum ozone, April-September.

Each exposure is in units of 1 SD of its within-site, within-year anomaly
(AOT40 1,039 ppb h; POD1 0.63 mmol m-2; mean O3 1.33 ppb; max O3 1.33 ppb).

Model (OLS):
r = b x O3(t) + c x log(I(t)+1) + weather(t) + weather(t+1) + winter temperature + N deposition(t)
+ site-by-species fixed effects + species-by-year fixed effects.

Weather is E-OBS April-September mean temperature, rain sum and mean radiation in t and t+1,
and the December-February mean temperature between t and t+1. N deposition is the EMEP
total (oxidised + reduced, wet + dry to semi-natural surfaces).

Inference: standard errors are clustered by year (34 clusters). Tables also give SEs
clustered by EMEP cell and by site. We also used a year-block permutation test: the anomaly
map of a random year replaces the map of year t, so the spatial structure stays the same.

The analysis plan (`files/analysis_plan.md`) was written before any estimate. It gives the
primary test, the checks and a decision rule: an ozone harm claim needs b < 0 with permutation
p < 0.05 in the main model, and the same sign in both periods and in the WCBS sample.
The NO2 control, the site-by-species trends and all "north" models were added after we saw
results. They are marked as not pre-specified in `files/results/model_results.csv`.

## 4. Results

Figure 1 shows the ozone exposure. Mean AOT40 at the transects decreased from the 1990s to
the 2010s and was high in 2003, 2006, 2018 and 2020. The anomaly maps of a year have
large-scale patterns (for example, high in south-east England in 2018).

Figure 2 and Table 1 give the slopes (x100 log units of next-year growth per 1 SD anomaly).

Table 1. Main slopes (n = 360,709 unless stated).

| Model | Slope | SE (year) | SE (cell) | Perm. p |
|---|---|---|---|---|
| AOT40, primary | -0.30 | 0.60 | 0.47 | 0.452 |
| POD1 semi-natural | -0.70 | 0.32 | 0.39 | 0.085 |
| Mean O3 | -1.12 | 0.59 | 0.68 | 0.005 |
| Monthly max O3 | -0.99 | 0.73 | 0.64 | 0.030 |
| AOT40, no controls | -0.42 | 0.64 | 0.33 | 0.425 |
| AOT40, migrant species removed | -0.41 | 0.57 | 0.47 | 0.350 |
| AOT40 + NO2 (not pre-specified) | +0.56 | 0.68 | 0.43 | 0.175 |
| AOT40 + site-by-species trends (not pre-specified) | +0.47 | 0.65 | 0.39 | 0.250 |
| POD1 + NO2 (not pre-specified) | -0.26 | 0.38 | 0.42 | 0.495 |
| POD1 + site-by-species trends (not pre-specified) | -0.62 | 0.39 | 0.37 | 0.125 |
| Mean O3 + NO2 (not pre-specified) | +1.55 | 1.13 | 0.98 | 0.005 |
| AOT40, 1990-2006 (n = 138,443) | +1.54 | 0.77 | 0.69 | 0.095 |
| AOT40, 2007-2023 (n = 222,266) | -0.82 | 0.51 | 0.54 | 0.315 |
| AOT40, southern England (n = 291,538) | -0.00 | 0.54 | 0.57 | 0.985 |
| AOT40, rest of UK (n = 69,171) | -3.92 | 1.15 | 1.53 | 0.005 |
| Placebo: AOT40 in t+2 (n = 342,598) | -0.69 | 0.60 | 0.46 | 0.105 |
| Same rows, AOT40 in t | -0.36 | 0.62 | 0.47 | 0.440 |

The primary test did not meet the decision rule. The two periods had opposite signs.

Host-plant groups (Figure 2a, Figure 3). AOT40 slopes were +1.02 (SE 1.63) for legume
feeders (8 species), -0.44 (0.69) for grass feeders (18), -0.44 (0.77) for other-forb feeders
(24) and +0.39 (0.97) for woody-host feeders (8). With POD1, grass feeders had -0.99 (SE 0.45,
perm. p = 0.045) and legume feeders +1.61 (SE 1.15). For 37 species with 1,500 or more pairs,
20 slopes were negative; 4 had a 95% CI below zero and 3 above zero. The random-effects mean
was -0.21 (SE 0.47), with between-species SD 2.2. Species slopes differ, but the differences
do not follow ozone sensitivity of the host plants.

Drought. The AOT40 slope was slightly more negative in wetter summers: interaction -0.15
(SE 0.07) per 46 mm of April-September rain. This agrees in sign with more stomatal uptake in
wet conditions, but the size is small.

Rest of UK (exploratory, Figure 2b). The negative slope outside southern England came mostly
from northern England (-7.05, SE 1.38; Wales, Scotland, Northern Ireland and islands +2.98,
SE 2.35). Removal of any single year left it between -4.55 and -3.42. But the placebo with
ozone two years later gave -4.65 (SE 1.09). The slope was -0.82 (SE 1.44) with an NO2 control,
+1.57 (SE 1.44) with site-by-species trends and -0.36 (SE 0.69) with POD1. Thus, the
association does not follow the timing of ozone exposure. It agrees with long-term
trends that ozone and butterflies share at the same sites.

Permutation p-values. The year-permutation null keeps the spatial structure of the maps, but
it does not keep slow site trends. The placebo test also gave small permutation p-values
where such trends are present (rest of UK; mean O3 + NO2). Thus, a small permutation
p-value in this design does not alone show an ozone effect. The year-clustered SE is the more
conservative measure for these models.

## 5. Interpretation

Within-year spatial differences in modelled ozone exposure did not predict UK butterfly
population growth. The pre-specified test gave a precise null: the 95% CI excludes
decreases larger than about 1.5% in next-year growth per 1 SD of AOT40 anomaly. The legume
prediction failed. Associations with mean ozone came from the strong negative relation between
ozone and NO2. The northern association came from shared site trends.

These results do not show that ozone has no effect on butterflies. They show that an effect of
the size seen in plant and insect experiments is not visible in year-to-year field changes at
UK transects with this exposure model. A national-scale effect of the long ozone decrease
cannot be tested with this design, because the year effects remove it.

## 6. Limitations

1. Exposure is EMEP model output at 0.1 degree (about 7 x 11 km). Errors in local ozone at a
   transect decrease the slope towards zero.
2. Only about 13% of the AOT40 variance is within site and within year. Ozone anomaly maps of
   one year correlate with those of the next year (mean r = 0.42), so slow spatial trends can
   mix with year effects.
3. Ozone, NO2 and N deposition anomalies are correlated (AOT40 with NO2 r = -0.65). Models
   with all three cannot fully separate them.
4. UKBMS transects are chosen by recorders and are not a random sample. Sites have different
   start and end years. The site indices include imputation for missing weeks.
5. The pre-specified WCBS replication was not possible, because the public site-index file has
   no WCBS squares. The 1,158 index sites without public locations were not used.
6. Host-plant groups are a simple, hand-made classification of main larval hosts
   (`files/code/hostgroups.py`). Legume feeders are only 8 species.
7. The 2023 and 2024 EMEP fields are status runs (2024 uses 2023 emissions). The 1990-2022
   fields are one trend run.

## 7. Files

- `files/analysis_plan.md`: plan written before the estimates.
- `files/code/`: all code. `reproduce.sh SCRATCH [DATASETS]` rebuilds everything in a separate
  scratch folder (EMEP download by OPeNDAP takes about 1 h).
  `01_fetch_emep.py` (EMEP subset), `02_eobs_monthly.py` (E-OBS monthly), `03_build_panel.py`
  (panel), `04_analysis.py` (models, permutations; `STEP=` selects a model group),
  `05_exposure_diag.py`, `06_figures.py`, `07_species_summary.py`, `fe.py` (fixed-effects OLS
  with sparse LSMR and cluster-robust SEs), `hostgroups.py`.
- `files/results/model_results.csv`: all models (slope `b`, SEs clustered by year, EMEP cell,
  site; permutation p and SD; sample sizes; `prespecified` flag). `species_results.csv`,
  `species_summary.json`, `exposure_diagnostics.json`, `exposure_sd.json`,
  `permutation_slopes_main_aot40f.csv`, `national_site_mean_emep_exposure.csv`.
- `files/figures/`: Figures 1-4 (Figure 4: permutation distribution for the primary test).
- `files/provenance/`: source URLs, versions and hashes.
- `files/NOTICE-external-data.md`: licences and attribution for the external data.

## 8. Provenance and attribution

Job sci-1107-dell-climate-pollution-biodiversity-58da8eefea2b, campaign 11_07_2026, topic
climate-pollution-biodiversity, machine dell. Analysis and text by Claude Opus 5.5
(claude-opus-5-5) in Claude Code, 2026-11-09. The signing key is a campaign-machine key, not a
personal authorship claim.

Contains UK Butterfly Monitoring Scheme (UKBMS) data (c) copyright and database right
Butterfly Conservation, the Centre for Ecology & Hydrology, British Trust for Ornithology, and
the Joint Nature Conservation Committee. EMEP MSC-W model results: credit MET Norway / EMEP
MSC-W. We acknowledge the E-OBS dataset from the EU-FP6 project UERRA and the Copernicus Climate
Change Service, and the data providers in the ECA&D project.
