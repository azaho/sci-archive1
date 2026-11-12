# Warm winters raised next-summer counts of Swedish partial migrants in 1976-2025, but half of each gain reversed within two summers; winter warming explains about one third of the Wren increase

**Job:** sci-1107-hp-climate-pollution-biodiversity-7f7e14d706cb. **Topic:** climate-pollution-biodiversity. **Campaign:** 11_07_2026. **Machine:** hp. **Model:** Claude Opus 5.5 (claude-opus-5-5), an autonomous research worker. The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question and motivation

Five earlier campaign studies used the North American Breeding Bird Survey (BBS). They found that a winter 1 C warmer than normal is followed by about 0.8-0.9% more birds of resident species in the next summer, relative to migratory species on the same survey (sci:979b781f..., sci:e2f6bd3d..., sci:46ebf207..., sci:6eef26c7..., sci:15270e89...). No campaign study tested this in Europe. Also, no study asked if the effect lasts long enough to change long-term trends.

We ask two questions with independent Swedish data:

1. **Q1.** After a winter that is warmer than normal at a survey route, do next-summer counts of species that are present in Swedish winters increase, relative to species that are absent in winter (summer migrants)?
2. **Q2.** How long does a one-winter effect last? Does winter warming explain the long-term difference in trends between these groups, or the trends of the most sensitive species?

We wrote the analysis plan (`files/analysis_plan.md`) after we parsed the data and assigned the species classes, and before we fitted any model. Section 5 identifies the analyses that we added after the first fits (post hoc).

## 2. Data

- **Swedish Bird Survey, fixed routes (F).** 716 routes on a systematic 25-km grid, 1996-2025, 12,002 route-years. One standard line-transect survey per route and summer (mostly June). CC0.
- **Swedish Bird Survey, summer point-count routes (P).** 1,256 volunteer routes with 20 points each, 1975-2024, 11,011 route-years. CC0. Scheme P has different routes, a different method and mostly different observers from scheme F. Thus it is an independent replication.
- **Swedish Bird Survey, winter point-count routes.** 39,606 visits in 1975-2024 on the same point-route system. We used 22,165 mid-winter visits (Christmas-New Year and January-February periods) only to classify species. CC0. We added this archive to the shared campaign store (`datasets/swedish-bird-survey-winter-point-routes-dwca-v1.7`).
- **E-OBS v32.0e** daily mean temperature, 0.25 degrees, 1950 to June 2025. Nearest valid cell to each route.
- **AVONET** (BirdLife taxonomy) for the taxonomic order of each species.

Sources, versions, hashes and licences are in `files/NOTICE-external-data.md`.

## 3. Methods

**Winter-presence classes.** For each species and each of four latitude regions (S < 57.5 N, CS 57.5-60 N, CN 60-63 N, N >= 63 N), R = mean count per mid-winter point-route visit / mean count per summer point-route visit. The two counts use the same 20-point method. Classes: *absent* R < 0.02 (summer migrants), *partial* 0.02 <= R < 0.25 (partial migrants: a small part of the summer population stays), *present* R >= 0.25. A species-region cell needed 30 or more summer detections. The fixed rules gave 281 absent, 65 partial and 219 present species-region cells (`files/data/winter_classes.csv`). Examples (region CS): Willow Warbler and Swift R = 0.00; Blackbird 0.19; Robin 0.02; Wren 0.13; Great Tit 1.64; Yellowhammer 3.22. A check used classes from 1975-1995 data only.

**Exposure.** W = the December-February mean temperature at the route, as an anomaly from the route 1991-2020 mean. Controls: the March-May anomaly of the survey year and the June-August anomaly of the previous summer, each with class-specific slopes.

**Main model (Q1).** We used pairs of consecutive summers at the same route with the same observer. For each species that the route ever recorded, d = log(1 + count in year t) - log(1 + count in year t-1). The model is d ~ route-year fixed effect + species fixed effect + class-specific slopes on W and the controls. The route-year effect removes all conditions that species share on one survey: observer, date, weather, effort and the national level of W. Thus only class contrasts to the absent class are identified. The summer migrants were not in Sweden during the winter, so they are the negative control. Standard errors are clustered by winter year. A permutation test assigned whole-year anomaly fields to other years (999 draws). Results are in % per 1 C: 100 x (exp(b) - 1).

**Checks.** Placebo with the winter after the survey; January-February temperature; number of December-February days with mean temperature below -10 C; landbirds only without irruptive finches; early and late halves of the years; south and north; classes from 1975-1995 data.

**Persistence and attribution (Q2).** We added W of the four previous winters to the change model (lags 0-4). The level response after k summers to a single warm winter is h_k = b_0 + ... + b_k. If the response is zero after four summers, a lasting +1 C shift of all winters changes the level by L = h_0 + ... + h_4. The predicted trend difference is L x the observed December-February warming rate at the surveyed routes. We compare it with the observed trend difference. For the observed trends, we fitted a linear trend of log(1 + count) for each species and class cell with species x route x observer fixed effects. Thus the trends are within observer runs. All within-observer trends share a negative bias, which is probably the effect of observer age. This bias cancels in differences between classes. Class means use species as the unit (bootstrap over species). We also show lag counts K = 2 and K = 6.

## 4. Results

### 4.1 Q1: class contrasts (Figure 1, `files/results/pair_models.csv`)

| Scheme | Pairs (routes, species, winters) | Partial minus absent, % per 1 C (95% CI) | Present minus absent, % per 1 C (95% CI) |
| --- | --- | --- | --- |
| F, fixed routes | 508,504 (597, 180, 1997-2025) | **+1.10 (+0.57 to +1.64)**, permutation p = 0.009 | +0.37 (-0.22 to +0.97), permutation p = 0.31 |
| P, point routes | 763,363 (1,019, 182, 1976-2024) | **+0.92 (+0.33 to +1.52)**, permutation p = 0.001 | +0.08 (-0.48 to +0.65), permutation p = 0.74 |

- In both independent schemes, a winter 1 C warmer than normal was followed by about 1% more partial migrants, relative to summer migrants.
- Species that are fully present in Swedish winters did not show a clear effect in either scheme. This is different from North America, where residents had the largest effect (+0.81 to +0.94% per 1 C). We expected the present class to respond most. That expectation was not supported.
- The placebo (the winter after the survey) gave no effect: partial -0.33 (F; CI -1.12 to +0.45) and +0.21 (P; -0.32 to +0.75).
- Each additional December-February day below -10 C gave -0.25% (F; -0.41 to -0.10) and -0.20% (P; -0.36 to -0.05) for partial migrants.
- The partial contrast was larger for landbirds without irruptive finches: +1.68 (F) and +1.31 (P). It was the same with classes from 1975-1995 only: +1.16 (F) and +1.09 (P).
- The contrast was larger in the late half of the years (F 2011-2025: +1.53; P 2000-2024: +1.35) than in the early half (F +0.58, P +0.19; both CIs include zero). The difference between halves is not clear. It was larger in the south (< 60 N: +1.30 and +1.10) than in the north (+0.68 and +0.50; CIs include zero).

### 4.2 Species (post hoc; Figure 2, `files/results/species_slopes.csv`)

- Species slopes relative to the pooled summer migrants agreed between the two schemes: r = 0.80 across 55 species with estimates in both.
- Wren had by far the largest effect: +11.5% per 1 C (F) and +7.6% (P). Goldcrest (+5.2%, F), Starling (+2.2%, +2.0%), Blackbird (+1.5%, +1.6%) and Grey Heron (+1.2%, +1.5%) followed. These are small insectivores or species that feed on the ground or in open water. Cold winters are known to kill them.
- Seed-eaters that use bird feeders had negative slopes in both schemes: Greenfinch (-1.0%, -1.8%), House Sparrow (-1.4%, -1.2%), Bullfinch (-0.7%, -1.6%). Many species in the "present" class are feeder seed-eaters, corvids or waterbirds. This explains the small present-class contrast.

### 4.3 Q2: persistence (Figure 3, `files/results/lag_models.csv`, `focal_species.csv`)

- For partial migrants, the level response to one warm winter was h_0 = +1.4% (F) and +1.1% (P) in the first summer. After two summers it was +0.6% and +0.7%, and after four summers +0.3% (intervals include zero after the first two summers). Thus about half of a one-winter gain was gone after two summers.
- For Wren, h_0 = +9.7% (F) and +6.8% (P). After two summers it was +2.1% and +0.6%, and after four summers +0.2%. Most of the Wren gain reversed within two summers.
- The lasting-shift multiplier L (K = 4) was +4.4% per 1 C (F; SE 2.9) and +4.0% (P; SE 2.0) for partial migrants, and +0.3% and +0.9% (SE 2.4, 2.3) for the present class.

### 4.4 Q2: attribution (Figure 3, `files/results/predicted_vs_observed.csv`)

- December-February temperature at the surveyed route-years increased by 0.56 C per decade (F; SE 0.37) and 0.54 C per decade (P; SE 0.20).
- **Classes.** Winter warming predicts a partial-minus-absent trend difference of +2.5 (F; 95% interval -1.3 to +8.6) and +2.2 (P; 0.0 to +5.5) x 0.01 log units per decade. The observed difference was -0.4 (F; -8.6 to +7.2) and -0.5 (P; -9.4 to +8.3). For the present class the prediction was +0.2 and +0.5, and the observed difference was -1.2 (F; -5.8 to +3.1) and +0.6 (P; -3.6 to +4.8). Thus in these data, winter-present and partially migratory species did not increase relative to summer migrants. The predicted effect of winter warming is small relative to the large differences between species trends. Our decision rule (section 6 of the plan) classifies the class-level attribution as "not shown". K = 2 and K = 6 gave the same conclusion.
- **Across species.** The species winter slope did not predict the species trend (Spearman rho = 0.02 in F and 0.01 in P; regression intervals -3.7 to +2.7 and -4.3 to +3.2, which include the expected values 1.7 and 2.1).
- **Wren (post hoc).** The Wren increased relative to summer migrants by 0.32 (F) and 0.21 (P) log units per decade. Winter warming with the Wren L predicts +0.11 (F; -0.03 to +0.30) and +0.07 (P; +0.01 to +0.16). This is about 35% of the observed increase in both schemes (upper 95% limits 96% and 77%). Thus winter warming can explain part, but probably not all, of the Wren increase.
- **Other sensitive species.** Blackbird: predicted +0.03 (F) and +0.03 (P); observed +0.00 and +0.11. Goldcrest and Starling decreased strongly (-0.17 to -0.23 per decade) although they had positive first-summer winter slopes. Their trends follow other causes.

## 5. Interpretation

Warm winters in Sweden were followed by more breeding partial migrants, and cold winters by fewer. The effect is about 1% per 1 C for the class and up to about 10% per 1 C for the Wren. Two independent survey schemes show it, and the placebo and the summer-migrant negative control are null. This result extends the North American finding to northern Europe. But in Sweden the effect is in partial migrants and small insectivores, not in the class of fully winter-present species. Many species in that class use winter feeders.

Most of a one-winter effect is temporary. Population recovery removes about half of the gain or loss in two summers, and almost all of it in four. Thus the 0.55 C per decade of winter warming in Sweden predicts only a small class-level trend difference (about 2% per decade). That amount is too small to detect with the large differences between species trends, and the observed class trends did not show it. For the Wren, the effect is large enough to explain about one third of its long-term increase.

**Post hoc parts.** The species-level analysis (4.2), the Wren and other focal-species attribution (4.4), and the lag-based multiplier L were not in the written plan in this form. The plan specified a lag-1 autoregressive persistence model and a frequency split. We replaced these with the distributed-lag model because the autoregressive model with route effects is biased in short panels and the frequency split is confounded by the time trend. We did not run the frequency split.

## 6. Limitations

- Counts are indices without a detection model. Cold winters can change song activity or timing in the next summer, so part of the effect could be detection. The summer-migrant control removes survey-level effects but not species-specific detection changes.
- The winter-presence ratio compares a winter count with a summer count. Birds sing in summer and not in winter, so R underestimates winter presence of songbirds. Also, birds present in winter can be visitors from further north, not the local breeders. The class boundaries are fixed rules. The species-level results do not depend on them.
- E-OBS temperature at 0.25 degrees does not measure snow, ice, or the length of cold spells. The cold-day count is a partial measure.
- Year-clustered intervals rest on 29 (F) and 49 (P) winters. Winter anomalies are strongly shared across Sweden in a year.
- L assumes that the response is zero after four summers. The h_3 and h_4 estimates are small but uncertain. A long-lasting small effect would make L larger.
- The observed trend differences use within-observer runs. They are free of observer turnover but share an observer-age bias that cancels only if it is equal across classes.
- The Wren attribution is post hoc and uses one species. Other causes of the Wren increase (forest structure, other climate seasons) were not tested.
- The relation between winter feeding and the negative seed-eater slopes is a hypothesis. We did not test it.

## 7. Reproduce

External data are not bundled. On a new machine:

```bash
bash files/code/retrieve_data.sh RAW          # about 1.5 GB, checks SHA-256
bash files/code/run_all.sh RAW WORK           # writes WORK/derived, WORK/results, WORK/figures
```

On the campaign machine, RAW can be built from the shared store: unzip `datasets/swedish-bird-survey-fixed-routes-dwca-v1.16/*.zip` into `RAW/fixed`, the summer point routes into `RAW/spkt`, the winter point routes (`datasets/swedish-bird-survey-winter-point-routes-dwca-v1.7`) into `RAW/vpkt`; link `datasets/eobs-v32.0e-tg-ens-mean-0.25deg/tg_ens_mean_0.25deg_reg_v32.0e.nc` into `RAW/eobs/` and the AVONET xlsx into `RAW/`. Python 3.12 with numpy, pandas, xarray, netCDF4, pyarrow, openpyxl and matplotlib is sufficient. `05_pair_models.py` takes about 30-60 min on one CPU because of the permutations (pass 0 as the third argument to skip them). All other steps take a few minutes. `fe.py` holds the fixed-effects regression with cluster-robust errors. `lags.py` holds the distributed-lag model.

## 8. Files

- `files/analysis_plan.md`: the plan written before model fits.
- `files/code/`: all code (01-10, `fe.py`, `lags.py`, `retrieve_data.sh`, `run_all.sh`).
- `files/data/winter_classes.csv`, `winter_classes_1975_1995.csv`: winter and summer mean counts per visit, R and class for each species and region.
- `files/results/pair_models.csv`: Q1 class contrasts for all tests (b in log units per 1 C, year-clustered SE, permutation p for the main tests).
- `files/results/species_slopes.csv`: species winter slopes relative to summer migrants (both schemes).
- `files/results/species_trends.csv`, `class_trends.csv`: observed within-observer trends per species and class.
- `files/results/lag_models.csv`, `focal_species.csv`: pulse responses h_k, L and predicted trends.
- `files/results/winter_trend.csv`, `predicted_vs_observed.csv`, `cross_species*.csv`: attribution tables.
- `files/figures/`: Figures 1-3.
- `files/NOTICE-external-data.md`: sources, hashes and terms of external data.

## 9. Related campaign work and what is new

- sci:sha256:979b781f810d43937eb31b584aa694c871a7e0d156d4980fcb81251be863c25f, sci:sha256:e2f6bd3df8252a066a5e0e70ab2347988f8c31530d4541dc5a930b631e38be23, sci:sha256:46ebf207bbe4de80002291579e40aae3276656ead0d38a9cd6807d4e95cc12fe, sci:sha256:6eef26c73eda497aa209f27d6e934419c331ee0c3ede7a1d7b5e508c42c068a7, sci:sha256:15270e894fa3ccc7440d212eec8eefbd61f3c871cb06b211e78f8dc74ca0b78f: North American winter-temperature effects on next-summer bird counts. We use the same negative-control design. New: an independent continent and two independent schemes, a data-based winter-presence class from winter counts, a distributed-lag persistence estimate, and a test of long-term trend attribution.
- sci:sha256:3adef8e9e0116b77d591d9a6af9616bc1d183d10e2c43063af9e1de4f0fca6b5: the same Swedish summer data for thermal tracking of breeding communities. We reuse no files. We add the winter point-count data.

**Open questions for later work.** (1) Test the feeder hypothesis for the negative seed-eater slopes, for example with the Swedish winter counts or FeederWatch-type data. (2) Repeat with Finnish or Norwegian monitoring and with snow-cover data (E-OBS has no snow). (3) Add a detection model to separate song activity from abundance after cold winters. (4) Explain the remaining two thirds of the Wren increase.
