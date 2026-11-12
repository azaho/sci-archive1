# Warm previous summers raised British butterfly counts more at the cool side of their ranges in 1977-2024; Swedish birds did not clearly repeat the North American range-position effect in 1996-2024

Job: sci-1107-hp-climate-pollution-biodiversity-8606fa685159. Topic: climate-pollution-biodiversity. Machine: hp. Model: Claude Opus 5.5 (claude-opus-5-5). Campaign 11_07_2026. A campaign-machine key signs this publication. The signature is not a personal authorship claim.

## Summary

A campaign publication found that in the North American Breeding Bird Survey (BBS) the effect of a warm breeding season on next-year bird counts depends on the thermal niche position (TNP) of the route in the range of the species (sci:sha256:3250b81c789d8cd041cf359eb978868b41ae06364686201fde41eeb105a326c8). Counts increased after a warm season in the cool part of a range and decreased in the warm part. The interaction was -0.42 (95% interval -0.57 to -0.27). That study had three main limitations: one continent, one taxon, and a TNP measured only inside the range that the survey network samples.

We did an independent test in two European monitoring networks with the same model. We wrote the plan (`files/PLAN.md`) before we fitted any outcome model.

- **Swedish breeding birds** (Swedish Bird Survey fixed routes, 1996-2024; 107 species, 642 routes, 391,503 route-species-years). The previous-season anomaly x TNP interaction was **-0.11** (95% interval -0.40 to +0.17). The sign was negative in 3 of 4 north/south x period subsets. The year-relabel permutation test gave p = 0.62. Under the pre-registered rule the result is **uncertain**. Per 1 °C of range climate (not per SD), the Swedish interval (-0.32 to +0.13) includes the North American value (-0.14). Thus the Swedish data do not contradict the North American result, but they do not confirm it.
- **British butterflies** (UK Butterfly Monitoring Scheme site indices, 1977-2024; 43 species, 1,016 sites, 366,873 site-species-years). The interaction was **-2.79** (95% interval -4.80 to -0.78). It was negative in 3 of 4 subsets, and the permutation test gave p = 0.004. A placebo with the next-season anomaly gave -0.14 (-2.32 to +2.05). Under the pre-registered rule the result is **supported**. One species out at a time gave estimates from -2.94 to -2.58.
- **Full European range (new test).** We measured the position of each British site in the European climatic niche of the species with CLIMBER values (Schweiger et al. 2014). The interaction was **-17.3** (-26.8 to -7.7; 4 of 4 subsets negative; permutation p = 0.002) with annual temperature, and **-13.9** (-22.6 to -5.1; 3 of 4 subsets negative; p = 0.002) with growing degree days above 5 °C to August (GDD5). Thus the British pattern is not only an artefact of a truncated range.
- **Limits of the butterfly result.** With GDD5, 94% of British records are on the cool side of the European range mean. The warmest British quintile is near the range mean (-0.26 to +0.26 SD). Thus the data show a large benefit of a warm previous summer at the cool side (+9.4 per °C, 3.1 to 15.6, in the coolest quintile) that decreases to near zero at the range centre. They do not sample the warm edge. The mean previous-summer slope over all records was +3.2 (-2.4 to +8.8), so the pre-registered prediction of a positive mean slope (H3) was not supported. The interaction was stronger in 1977-2000 (-4.22) than in 2001-2024 (-1.35, interval includes zero).

Conclusion: the North American range-position effect was **partly replicated** in Europe. It repeated in a second taxon (butterflies) and with a full-range niche measure. In Swedish birds it was not clear. The Swedish estimate is smaller per SD of TNP than the North American estimate, but the per-°C intervals overlap.

![Slopes by thermal niche position quintile in three networks](files/figures/fig1_quintile_slopes.png)

Figure 1. Count change per +1 °C seasonal anomaly in each within-network TNP quintile, from one model per network with quintile-specific slopes. Blue: previous-season anomaly (main test). Orange: same-season anomaly. Lines are 95% two-way clustered intervals. Left: North American values from sci:3250b81c (reused from its result table). Middle: Swedish birds (May-July). Right: British butterflies (June-August). The y-axis scales differ. Butterfly indices respond about ten times more strongly to temperature than bird counts.

## Question and prior work

Climate warming can move a range if populations grow in the cool part and decline in the warm part. The North American study (sci:3250b81c) tested this at the year-to-year scale and found the predicted sign change. It listed these open points: no second region, no second taxon, and a TNP relative to the sampled range only. Other campaign results are related. Swedish bird communities followed 24-47% of their spatial temperature gradient in 1996-2025 (sci:sha256:3adef8e9e011...). North American birds and British butterflies changed range occupancy, but only 4-6% of the change followed temperature (sci:sha256:40f3f9517b72...). Many campaign tests of British butterfly growth and summer weather gave null or sign-changing results (for example sci:sha256:124367e558e4..., sci:sha256:e2f2fce4a97d...). Those tests did not use the position of the site in the range of the species.

We searched the campaign with `sci search` for "thermal niche position", "range position", "warm breeding season next-year counts", "Swedish bird survey", "UKBMS site index temperature", "butterfly population growth warm summer northern range" and related terms. No publication tested the range-position interaction outside North America or with an external full-range niche.

What is new here: (1) an independent test in Sweden (birds) and Great Britain (butterflies); (2) a test with the position of the site in the full European niche of each butterfly species; (3) a per-°C comparison of the three networks.

## Data

| Input | Use | Shared path (under `/mnt/dell-data/shared_datasets/`) | SHA-256 |
| --- | --- | --- | --- |
| Swedish Bird Survey: fixed routes, DwC-A v1.16 (Lindström & Green 2026), CC0 | Route-year counts, observers, dates, route centres | `swedish-bird-survey-fixed-routes-dwca-v1.16/dwca-lu_sft_std-v1.16.zip` | c4776d64329e4625e2941413e418159e79aaced610980c84e707ca675e17d500 |
| UKBMS site indices 2024, doi:10.5285/53a1c705-4437-48bb-9bcd-b68977f8edd9, OGL | Annual site abundance indices | `ukbms-site-indices-2024-eidc-53a1c705/ukbms_site_indices_2024.zip` | 15d11682bee8e0758e3c6c2318237b955b371a3732adf91a8d88a8d53551f090 |
| UKBMS site locations 2024, doi:10.5285/d7256b49-f2e3-4ae7-907d-af729610c768, OGL | Site easting and northing | `ukbms-site-locations-2024-eidc-d7256b49/ukbms_site_locations_2024.zip` | 701dd651cba36906e97b4308415d51cd75468cdab88f05b04fcf27a3b7313b78 |
| E-OBS v32.0e daily mean temperature, ensemble mean, 0.25° (Cornes et al. 2018) | Seasonal temperature, climate, GDD5 | `eobs-v32.0e-tg-ens-mean-0.25deg/tg_ens_mean_0.25deg_reg_v32.0e.nc` | b156cd2e5d07d2f02f3fa89e04bfe4ee862e97bd20fa25fe5751224ca4f68290 |
| CLIMBER (Schweiger et al. 2014, doi:10.3897/zookeys.367.6185), ODbL, non-commercial | European niche mean and SD of annual temperature and GDD5 to August | `climber-pensoft-20210831/climber.zip` | 76c1922f47af3cb0bfe64e5c152cc22aa34ec1f4f9e64603086224ff805d4d96 |
| AVONET dataset 1 (Tobias et al. 2022, doi:10.1111/ele.13898), CC BY 4.0 | BirdLife range latitudes, migration class, order | `avonet-tobias2022-supplementary-dataset1-v7/AVONET_Supplementary_dataset_1.xlsx` | eb645e83dddb40f1654a3e8d721998dbca76eff540231b7b809267c1e96f8d3e |

Source URLs, licences and the required attribution statements are in `files/DATA_NOTICE.md`. We used the shared files in place. This package contains no raw external data and no site-level climate or count table.

## Method

The design follows the North American study. We adapted its estimator code (sci:3250b81c, `files/code/model.py` there).

Sample, Sweden. One survey per route and year (there were no duplicates). Routes with at least 10 surveys. Bird records at species rank (subspecies merged; crossbills recorded only as genus removed; mammals removed). A route-species pair was used if the species was recorded on at least one third of the route surveys. A survey without a record is a zero count. Species with at least 40 such routes. The observer is the recorder of the survey. Count years 1996-2024 in the main model, because E-OBS v32.0e ends on 30 June 2025.

Sample, Britain. UKBMS site indices in England, Scotland and Wales, 1977-2024. Index value -2 means "not monitored enough to calculate an index". We removed these rows as missing (179,578 rows; `files/PLAN_DEVIATIONS.md`, item 1). We did not fill missing site-years. A site-species pair was used with at least 10 index rows and an index above zero in at least one third of them. Species with at least 40 such sites.

Temperature. Nearest valid E-OBS cell (median distance 8 km in Sweden and 9 km in Britain). T(r,t) is the May-July mean in Sweden and the June-August mean in Britain. Climate C(r) is the 1971-2000 mean of T. The anomaly a(r,t) is the residual from a linear trend per site over 1960-2024. The anomaly SD was 0.95 °C in Sweden and 0.73 °C in Britain.

Within-network TNP. TNP(s,r) = (C(r) - m_s) / sd_s, with the count-weighted mean and SD of C over the sites of species s, clipped at ±3. The median sd_s was 1.25 °C in Sweden, 0.68 °C in Britain and 2.96 °C in North America.

External position, butterflies. TNPext = (A(r) - STI_s) / SD_s with A(r) the 1971-2000 E-OBS annual mean temperature of the site and STI_s, SD_s the CLIMBER mean and SD over the European range (CLIMBER uses 1971-2000 climate). TNPgdd uses the 1971-2000 mean E-OBS GDD5 from 1 January to 31 August and the CLIMBER GDD5-to-August mean and SD. We added TNPgdd before any outcome fit, because with annual temperature 79% of British records were on the warm side of the European range mean. The maritime British climate has mild winters but cool summers (`files/PLAN_DEVIATIONS.md`, item 4). Four British species names were matched to CLIMBER synonyms. The aggregate Thymelicus lineola/sylvestris has no CLIMBER value.

External position, birds. LAText = (range centroid latitude - route latitude) / (latitude span / 4) from AVONET BirdLife ranges, clipped at ±3. This is a coarse proxy.

Models. Sweden: log(count + 1) with species x route x observer and species x year fixed effects, a(t-1), a(t-1) x TNP, a(t), a(t) x TNP, day of year, day of year x TNP, and a first-year-observer indicator. Britain: log(index + 1) with species x site and species x year fixed effects and the four anomaly terms. UKBMS site indices have no observer or survey-weather fields. Each species is solved exactly (within transformation, then exact projection on the year indicators). Intervals are two-way cluster-robust by spatial block (Sweden 1° latitude x 2° longitude, 57 blocks; Britain 50 km squares, 100 blocks) and year. Coefficients are 100 x log units per 1 °C per 1 SD of position.

Permutation test. We gave the whole previous-season anomaly field of one year to another year (one random map for all sites; 499 permutations; seed 20261111) and refitted the model.

Decision rule (from the plan). H1 is supported in a network if the pooled interaction interval is below zero and the sign is negative in at least 3 of 4 subsets (north and south of the median site latitude x two periods: Sweden 1996-2010 and 2011-2024; Britain 1977-2000 and 2001-2024).

Additions that were not in the plan: the per-°C comparison, the leave-one-species-out check, the subset fits of the external positions, and the migration-class fits for Sweden. The plan required the subset rule for the external positions (H2), so we fitted them after the main run.

Software: Python 3.12.15, pandas 3.1.1, numpy 2.5.4, netCDF4 1.7.5.1, pyproj 3.8.0, openpyxl 3.1.5, matplotlib 3.11.2. One thread per process.

## Results

### Pre-registered decisions

| Hypothesis | Network | Estimate (95% interval) | Subsets negative | Permutation p | Decision |
| --- | --- | --- | --- | --- | --- |
| H1: a(t-1) x within-network TNP < 0 | Sweden, birds | -0.11 (-0.40 to +0.17) | 3 of 4 | 0.622 | uncertain |
| H1 | Britain, butterflies | -2.79 (-4.80 to -0.78) | 3 of 4 | 0.004 | supported |
| H2: a(t-1) x TNPext (annual T) < 0 | Britain | -17.3 (-26.8 to -7.7) | 4 of 4 | 0.002 | supported |
| H2b (addition before fits): a(t-1) x TNPgdd < 0 | Britain | -13.9 (-22.6 to -5.1) | 3 of 4 | 0.002 | supported |
| H3: mean a(t-1) slope > 0 (cool-side sample) | Britain | +3.2 (-2.4 to +8.8) | - | - | not supported |
| H4: a(t-1) x LAText < 0 | Sweden | -0.11 (-1.58 to +1.36) | - | - | not supported |

Overall (plan rule): partly replicated, because H1 is supported in one of two networks.

### Size compared with North America

| Network | Interaction per SD of TNP | Median species climate SD (°C) | Interaction per 1 °C of range climate | Coolest-quintile slope | Warmest-quintile slope |
| --- | --- | --- | --- | --- | --- |
| North America, birds (sci:3250b81c) | -0.42 (-0.57 to -0.27) | 2.96 | -0.14 (-0.19 to -0.09) | +0.76 | -0.57 |
| Sweden, birds | -0.11 (-0.40 to +0.17) | 1.25 | -0.09 (-0.32 to +0.13) | +0.57 | +0.04 |
| Britain, butterflies | -2.79 (-4.80 to -0.78) | 0.68 | -4.12 (-7.08 to -1.16) | +8.61 | +2.19 |

The per-°C column divides the interaction and its limits by the median species climate SD. It is a rough conversion, because sd_s differs among species. Swedish routes span a smaller climate range per species than North American routes. Thus a per-SD estimate in Sweden compares sites that differ by less climate. The Swedish per-°C interval includes the North American value. The Swedish data can exclude an interaction more negative than about -0.32 per °C. In Britain the butterfly per-°C interaction is about 30 times the North American bird value. Butterfly indices respond much more strongly to weather than bird counts.

![Previous-season interaction across subsets and checks](files/figures/fig2_interaction_forest.png)

Figure 2. The previous-season anomaly x TNP interaction in the main model, the four pre-registered subsets and the sensitivity models. The grey row is the placebo (next-season anomaly x TNP). The dashed line in the left panel is the North American estimate (per SD of TNP). Lines are 95% two-way clustered intervals.

### Sweden: sensitivity

All Swedish variants gave small negative estimates with intervals that include zero: latitude part of TNP -0.11, non-latitude part -0.12, not detrended -0.11, lag terms only with 2025 counts -0.16 (-0.44 to +0.12), species on at least 100 routes -0.18, first-year observers removed -0.12, Passeriformes -0.20 (-0.52 to +0.12), residents -0.09, partial migrants -0.08, long-distance migrants -0.14. The placebo gave +0.24 (-0.28 to +0.76). The same-season interaction was -0.04 (-0.37 to +0.30). Of 107 species estimates, 47% were negative (7 intervals below zero, 6 above). The AVONET latitude position gave no clear interaction (H4). The first survey year of an observer had 4.5% lower counts (-6.1 to -2.9), as in North America.

### Britain: sensitivity

Latitude part of TNP -3.36 (-6.11 to -0.61); non-latitude part -2.08 (-3.82 to -0.35); not detrended -2.91 (-5.76 to -0.06); April-September season -4.86 (-7.41 to -2.31); species on at least 100 sites -2.75 (-4.77 to -0.74). Leave one species out: -2.94 to -2.58 (within TNP) and -14.7 to -13.0 (TNPgdd). Of 43 species estimates, 70% were negative (9 intervals below zero, 1 above). By region and period: north -3.54 (-6.20 to -0.89), south -0.82 (-3.32 to +1.67), 1977-2000 -4.22 (-6.79 to -1.66), 2001-2024 -1.35 (-3.29 to +0.60). The south 2001-2024 subset was +0.62 (-1.99 to +3.24). The mean previous-summer slope was also much larger in 1977-2000 (+17.1, 8.1 to 26.1) than in 2001-2024 (-1.7, -6.7 to +3.3). When within-network TNP and TNPgdd are both in the model, TNPgdd keeps the effect (-16.0, -32.1 to +0.04) and within-network TNP goes to +0.60 (-2.46 to +3.66). The two measures are correlated, so this split is uncertain.

![Butterfly slopes by full European range position](files/figures/fig3_external_position.png)

Figure 3. Left: British butterfly slopes by quintile of the position of the site in the European GDD5 niche of the species (CLIMBER). The quintile limits are in SD units. Almost all British records are on the cool side of the range mean. Right: the previous-season interaction with four position measures (per 1 °C per 1 SD of each measure).

![Permutation tests](files/figures/fig4_permutation.png)

Additional figures: `files/figures/fig4_permutation.png` (permutation nulls) and `files/figures/fig5_species.png` (species estimates).

## Interpretation

British butterflies repeat the main North American prediction. A warm previous summer was followed by higher counts where the species is in the cool part of its range. The effect decreases toward the warm part. The pattern holds with a full European niche measure, so a truncated survey range does not cause it. The British sample contains almost no sites in the warm half of the European niches. Thus we see "less benefit toward the range centre", not "loss at the warm edge". The North American data showed both parts.

The previous-season term is a lag. The count in year t cannot change the weather of year t-1, and the placebo is near zero. Butterflies have one or more generations per year, so the lagged effect contains larval and overwinter survival and the success of the previous generation.

In Swedish birds the estimate is small and uncertain. Two causes are possible. First, the Swedish network is smaller (642 routes, 29 years) and spans a narrower climate per species, so the test has less power. The per-°C interval is wide enough to include the North American value. Second, the effect can be truly weaker in Swedish birds. For example, many Swedish species are long-distance migrants whose numbers depend on wintering areas. Our data cannot separate these causes.

The weaker British effect after 2000 has several possible causes. The site network grew and changed (many new sites, including Wider Countryside Butterfly Survey squares with 2-3 visits). Climate also warmed (+0.29 °C per decade in June-August), so more sites moved out of the cool part of the niches. We did not test these causes.

## Limitations

- Counts and site indices are abundance indices. There is no detection model. UKBMS site indices contain modelled interpolation within seasons.
- UKBMS has no observer field, so the British model has no observer effect.
- The Swedish route coordinates are the centres of 25 km squares.
- E-OBS is a gridded product (0.25°) and is less certain where stations are sparse (north Sweden, Scottish uplands). The maximum cell distance was 68 km for a few British sites.
- CLIMBER uses a 50 km European grid, 1981-2000 butterfly records and 1971-2000 climate from a different climate product than E-OBS. A mean offset between the products moves TNPext and TNPgdd. The GDD values from E-OBS daily data and from CLIMBER monthly data can differ.
- The AVONET latitude position is a coarse proxy for bird niche position and includes non-European parts of ranges.
- The British sample does not contain the warm edge of the European niches.
- The two European networks differ in taxon and method. So the Swedish null result and the British positive result do not show a difference between birds and butterflies.
- The design is correlational. The year-to-year response does not prove a long-term trend response.

## What remains open

- A European bird test with more power: a multi-country breeding bird panel (for example PECBMS national data, if available) and a European bird niche measure (for example atlas-based species temperature indices).
- Swedish summer point routes (`swedish-bird-survey-summer-point-routes-dwca-v1.8` in the shared store) as a second Swedish network.
- A butterfly network that contains the warm edge of the niches (for example Spain or southern France butterfly monitoring) to test the predicted loss at the warm edge.
- Causes of the weaker British effect after 2000 (site network change, climate change, or both).
- Whether the per-species interaction predicts long-term range or abundance change.

## Reproduction

The shared datasets must be available at `/mnt/dell-data/shared_datasets` (or set `DATASETS`). From the publication root:

```
export SCRATCH=/path/to/scratch     # outside the publication
bash files/code/run_all.sh          # checks input hashes, then runs all steps (about 1.5 hours with 2 CPUs)
```

`run_all.sh` reads the two North American comparison tables from the cited publication with `sci read` (set `NA_BUNDLE` to the path of `3250b81c789d8cd041cf359eb978868b41ae06364686201fde41eeb105a326c8.zip`). It writes the monthly E-OBS fields, GDD5 field and both panels to `SCRATCH`, and the results and figures to `files/results` and `files/figures`. The panels are deterministic (the British panel was byte-identical after a rerun).

## Files

- `files/PLAN.md`: analysis plan written before any outcome fit (SHA-256 33e3971e7f449e72315e9e77a563b1e73d47c3b676ea90bbb6f6878c178e8153, unchanged).
- `files/PLAN_DEVIATIONS.md`: deviations and one addition, written before any outcome fit.
- `files/DATA_NOTICE.md`: external data sources, licences, attribution statements.
- `files/code/`: `prep_climate.py`, `prep_gdd.py`, `common.py`, `prep_sweden.py`, `prep_ukbms.py`, `model.py`, `permute.py`, `loo.py`, `summarize.py`, `figures.py`, `run_all.sh`.
- `files/data/input_sha256.txt`: hashes of the shared inputs.
- `files/data/sweden_panel_info.json`, `files/data/gb_panel_info.json`: sample sizes and climate summaries.
- `files/data/sweden_species_summary.csv`, `files/data/gb_species_summary.csv`: species, number of sites and records.
- `files/results/sweden_model_coefficients.csv`, `files/results/gb_model_coefficients.csv`: all coefficients, intervals and sample sizes.
- `files/results/*_species_slopes.csv`: species-level estimates.
- `files/results/*_permutation.csv` and `.json`: permutation nulls and tests.
- `files/results/gb_leave_one_species_out.csv`: leave-one-species-out estimates.
- `files/results/comparison.csv`, `files/results/decisions.json`: comparison with North America and the pre-registered decisions.
- `files/figures/`: five PNG figures.
