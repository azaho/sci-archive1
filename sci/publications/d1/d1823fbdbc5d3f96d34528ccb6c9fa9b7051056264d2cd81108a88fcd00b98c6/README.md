# French forest understory plants shifted to warmer-climate species at about 28% of the rate of local warming in 2005-2022, at a constant rate that did not follow 5-year temperature changes

Job `sci-1107-dell-climate-pollution-biodiversity-5a1e0d2ff24f`, topic climate-pollution-biodiversity, campaign 11_07_2026, machine dell, model Claude Opus 5.5 (`claude-opus-5-5`). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

**Question.** Did the understory flora of French forests change toward species of warmer climates in 2005-2022? Which fraction of its own spatial temperature gradient did it follow? Did it respond to temperature or drought changes over 5-year intervals? How large are the observation biases of a national forest inventory?

**Data.** IGN French National Forest Inventory (NFI) floristic relevés from GBIF France (CC BY 4.0): 111,758 dated relevés on a systematic 1-km grid, 2005-2022 campaigns, 2,548 vascular understory species. 94,837 plots have one first visit. 16,443 plots have a second relevé about 5 years later (NFI revisits, 2010-2022). E-OBS v31.0e monthly temperature and precipitation (0.25 degree). EIVE 1.0 indicator values (temperature, nitrogen, reaction, moisture, light).

**Method.** We wrote the plan (`files/PLAN.md`) before the outcome models. A cross-fitted species temperature index (STI) is the mean 1991-2020 temperature of the plots where a species grows. The floristic temperature (FT) of a relevé is the mean STI of its understory species. (1) Spatial benchmark: slope of FT on site temperature. (2) Repeated cross-sections of first visits with 0.25-degree cell fixed effects, survey-month, soil, rock, humus and topography effects, canopy cover and species number. (3) Within-plot change between the two visits of the same plot. Errors are clustered on 93 one-degree blocks; fractions have block-bootstrap intervals (200 draws).

**Results.**
- Spatial benchmark: FT increased 0.277 C per 1 C of site temperature (95% CI 0.250-0.311).
- First visits, 2005-2022: FT increased 0.036 C per decade (0.026-0.046). The 5-year mean temperature at the plots increased 0.455 C per decade. Full tracking predicts 0.126 C per decade. The **slow tracking fraction was 0.28 (bootstrap 0.22-0.34)**.
- FT increased in all four regions (NW 0.018, NE 0.029, SW 0.038, SE 0.054 C per decade; fractions 0.20, 0.20, 0.54, 0.37).
- **The FT trend did not follow the temperature trend.** In 2005-2013 the 5-year temperature at the plots decreased (-0.45 C per decade), but FT increased 0.030 C per decade. In 2014-2022 the temperature increased fast (+1.09 C per decade), and FT increased 0.038 C per decade.
- Revisits (15,686 plots, about 5 years apart): FT increased 0.017 C (0.011-0.023), which is 0.18 (0.10-0.31) of full tracking. The change did not depend on how much the plot warmed between the visits: slope -0.007 (-0.028 to +0.017), a fast fraction of -0.02 (-0.10 to +0.06). Summer drought and summer heat before the visits had no detectable effect. Canopy loss between visits increased FT (0.009 C per 10% canopy cover lost).
- Species: losses of cold-affiliated species (for example *Hieracium murorum*, *Epilobium montanum*, *Rubus idaeus*, *Avenella flexuosa*) and gains of warm-affiliated species (*Rubus ulmifolius*, *Quercus pubescens*, *Q. ilex*) made the shift. Gains of cold-affiliated trees in the understory (*Fagus sylvatica*, *Abies alba*, *Acer pseudoplatanus*, *Fraxinus excelsior*) and losses of Atlantic heath species (*Erica* spp., *Ulex minor*, *Molinia caerulea*) partly cancelled it.
- EIVE community means: temperature +0.045, nitrogen +0.063, reaction +0.055 units per decade; moisture and light did not change. Species trends followed STI and EIVE nitrogen independently. The nitrogen increase was not steady: it increased until 2019 and decreased in 2020-2022.
- **Observation bias.** Relevés made in January-February had FT 0.12 C higher than July relevés of the same cells, two times the 2005-2022 change. The places of first-visit plots changed between years (mean latitude 46.1 N in 2005-2009, 46.65 N in 2010-2014, 45.9 N in 2015-2019). Thus naive annual means of FT jump by about 0.1 C at 2015 and drop at 2020, and EIVE means have steps at 2010. Cell fixed effects remove these jumps.

**Conclusion.** French forest understories thermophilized in 2005-2022 in all regions, but at only about one quarter of the rate that local warming predicts. The shift went on at a constant rate and did not follow 5-year temperature or drought anomalies. Thus it is a slow, lagged process (or has non-climatic causes), not a fast response to recent weather. **Main limitations:** STIs from inventory plots and grid temperature without plot elevation; correlational design; the plots are a forest sample, so we cannot separate climate from forest management, canopy change and nitrogen deposition; we did not test deposition data.

![Figure 2](files/figures/fig2_tracking.png)

## 1. Background

Plant communities in forests are expected to change toward warm-adapted species as the climate warms (thermophilization). Resurveys in Europe found that this change lags behind warming (a "climatic debt"; Bertrand et al. 2011, doi:10.1038/nature10548) and that dense canopies slow it (De Frenne et al. 2013, doi:10.1073/pnas.1311190110; Zellweger et al. 2020, doi:10.1126/science.aba6880). A recent European synthesis of vegetation plots also found shifts toward nutrient-demanding species (Midolo et al., data doi:10.5281/zenodo.18625789).

In this campaign, a multi-network synthesis found that animal and tree communities followed about 12% of their spatial temperature gradient (sci:sha256:0037934e440093284370046185fd30a78b7363fd6e940f8fd3d9860e2caedada). Swedish birds followed 24-47% (sci:sha256:3adef8e9e0116b77d591d9a6af9616bc1d183d10e2c43063af9e1de4f0fca6b5), Finnish moths were near their spatial benchmark (sci:sha256:6d9554368057aaa2f9663e3e82d0318975bc04c3cc31b5fde67fddaa065e4ff9), and eastern US tree seedlings followed about 58% (sci:sha256:8fb859255599b74e78e60cf3221eef1554a3124d7cf4056217e3f027cbbb8fb3). We found no campaign publication about understory plants or the French NFI. The NFI flora data were in the shared store but not used.

**What is new here.** (1) A national systematic sample of forest understory plants, 2005-2022, tested against its own spatial benchmark. (2) Two independent designs (repeated cross-sections and within-plot revisits) that agree. (3) A direct test of a fast response to 5-year temperature and drought change. (4) A quantification of two observation biases (survey season and spatial sample rotation) that are larger than the climate signal.

## 2. Data

| Source | Use | Version and hash |
|---|---|---|
| IGN NFI floristic relevés, GBIF France / INPN DwC-A 4A9DDA1F (CC BY 4.0) | Species lists, understory abundance codes, tree canopy cover by species, soil, humus, rock, topography | campaign store `ign-ifn-floristic-releves-inpn-dwca-20240320`, SHA-256 5c1f1780... |
| E-OBS v31.0e tg and rr, 0.25 degree (Cornes et al. 2018) | Site climatology 1991-2020, 12/36/60-month anomalies, last-summer anomalies, Thornthwaite water balance | SHA-256 7d35a58a... and 304cf09e... |
| EIVE 1.0 (Dengler et al. 2023), Zenodo 7534792 SM_08 (CC BY 4.0) | External indicator values T, N, R, M, L | campaign store `eive-1.0-zenodo7534792-sm08` (added by this job), SHA-256 9551b585... |

Full hashes are in `files/provenance/input_hashes.txt`. Terms and attribution are in `files/EXTERNAL_DATA_NOTICE.md`.

**Relevés.** The DwC-A gives one record per species occurrence and no relevé key. We defined a relevé as a unique plot coordinate and date. Of 112,557 relevés, 755 had no coordinates and were removed. We kept species, subspecies, variety and form records (merged to species), and removed records with the identification status "Invalide" or "Douteux". The understory list is the species with understory abundance code ABONDNR >= 1 (herbs, mosses and woody plants below 7.5 cm diameter). We removed 120 bryophyte species by family. Canopy cover is the sum of the class mid-points of tree cover by species (TCAR), capped at 100%. The NFI campaign year runs from November to October.

**Revisits.** 16,737 plot coordinates had two or more dates. 16,443 plots had exactly two relevés 3-8 years apart (median 5.0 years). The mean Jaccard similarity between the two species lists was only 0.29. This includes real change and observer and season differences (pseudo-turnover).

## 3. Methods

**Indices.** STI = mean Tclim (1991-2020 annual mean temperature of the nearest valid E-OBS cell) of the first-visit relevés that contain the species, for species with at least 20 training occurrences. The STIs are cross-fitted: we put 1-degree blocks in 5 random folds, and the FT of a relevé in fold f uses STIs computed without fold f. FT is the unweighted mean STI of the understory species; a relevé needs at least 5 species with an STI. The same construction with the annual climatic water balance gives a moisture index FW. EIVE community means are unweighted, with at least 5 matched species (94% of understory records matched).

**H1, spatial benchmark.** OLS of FT on Tclim, with and without survey-month, rock, soil, humus and topography effects, canopy cover and log species number.

**H2, repeated cross-sections.** First visits only (92,585 relevés with FT). FT = trend x (campaign year - 2005) + controls. The plan's main model has Tclim as a covariate. We found that the places of first-visit plots changed between years (Figure 1B). Thus we report as preferred the model with 0.25-degree cell fixed effects (1,077 cells), which uses only changes inside cells. The two models give similar trends (0.032 and 0.036 C per decade). The temperature trend is the trend of the 60-month mean temperature anomaly before each survey, with the same cell and month effects. Slow fraction = FT trend / (b_space x temperature trend).

**H3, revisits.** dFT (visit 2 - visit 1) = c + beta_T x dT60 + beta_W x dWB36 + differences of survey-month indicators. With this month coding, c is the change between visits made in the same month at dT60 = 0. Extended model: change of canopy cover, change of log species number, and the anomalies of the last summer before each visit (temperature and water balance).

**Inference.** CR1 cluster-robust errors on 93 one-degree blocks. Fractions: block bootstrap (blocks resampled with replacement, cells relabelled per draw; 2 x 100 draws, `files/results/bootstrap_fractions_*.csv`).

**Post-hoc checks (not in the plan).** Trend x dense canopy (>= 75%); trend x long-term warming of the cell (2013-2022 minus 1985-1994); trend without month effects; FT trend with EIVE-N as covariate and the inverse; season profile of FT; species occupancy trends (linear probability with month and cell effects) and a decomposition of the FT trend into four species groups.

**Deviations from the plan.** (1) The preferred H2 model has cell fixed effects instead of Tclim (reason above; both are reported). (2) The fourth region is "SE" (south of 46.3 N and east of 2.5 E: Mediterranean, Alps and eastern Massif Central), not a pure Mediterranean region. (3) We used 200 bootstrap draws, not 500, because of compute time.

## 4. Results

### 4.1 Spatial benchmark and slow change (Figure 2)

| Sample | FT trend, C per decade (95% CI) | 60-month temperature trend, C per decade | b_space | Full tracking, C per decade | Fraction |
|---|---|---|---|---|---|
| France | **0.036 (0.026, 0.046)** | 0.455 | 0.277 | 0.126 | **0.28 (bootstrap 0.22-0.34)** |
| NW | 0.018 (0.009, 0.027) | 0.380 | 0.241 | 0.091 | 0.20 |
| NE | 0.029 (0.019, 0.038) | 0.489 | 0.300 | 0.147 | 0.20 |
| SW | 0.038 (0.025, 0.052) | 0.427 | 0.167 | 0.071 | 0.54 |
| SE | 0.054 (0.028, 0.080) | 0.490 | 0.293 | 0.143 | 0.37 |
| 2005-2013 | 0.030 (0.012, 0.048) | -0.449 | 0.277 | -0.125 | (negative) |
| 2014-2022 | 0.038 (0.021, 0.054) | 1.087 | 0.277 | 0.301 | 0.12 |

The plan's decision rules were met for "thermophilization detected" (main-model CI above zero: 0.032, CI 0.019-0.044; positive in 4 of 4 regions) and for "tracking incomplete" (upper bootstrap bound 0.34 < 1).

Robustness of the cell-FE FT trend (C per decade): growing-season relevés only (April-September) 0.035; without 2020 (COVID-19 gap, no April 2020 relevés) 0.035; from 2008 (after the early increase of recorded species numbers) 0.036; without the species-number term 0.036; without month effects 0.036; naive (no controls) 0.043. Species number per relevé had no trend (0.014 log units per decade, CI -0.016 to 0.043).

The FT trend was the same under dense and open canopies (difference -0.005 C per decade, CI -0.014 to +0.005) and did not depend on the long-term warming of the cell (+0.005 C per decade per 1 C, CI -0.023 to +0.033).

### 4.2 Within-plot change at revisits (Figure 3A)

| Model or subset | Plots | Change at dT60 = 0, C | Slope on dT60 |
|---|---|---|---|
| All pairs, month coding | 15,686 | 0.019 (0.007, 0.031) | -0.007 (-0.028, +0.016) |
| Same season (survey dates within 30 days) | 3,619 | 0.025 (0.008, 0.042) | -0.020 (-0.063, +0.022) |
| Both visits April-September | 4,454 | 0.019 (-0.001, +0.039) | 0.000 (-0.034, +0.033) |
| Jaccard above median | 8,199 | 0.020 (0.009, 0.030) | -0.013 (-0.033, +0.008) |
| NW / NE / SW / SE | 2,166 / 5,222 / 3,514 / 4,784 | 0.008 / 0.001 / 0.003 / 0.031 | -0.007 / +0.017 / +0.037 / -0.031 |

The mean dT60 between visits was +0.335 C (0.26-0.40). At this warming, the mean FT change was 0.017 C (bootstrap 0.011-0.023), a fraction of 0.18 (0.10-0.31). The FT change over 5 years agrees with the cross-section trend (0.036 C per decade x 0.5 decade = 0.018 C). The slope on dT60 was near zero in all subsets; only SW had a CI above zero (0.037, CI 0.001-0.074), and SE had the opposite sign. A full-tracking slope would be 0.277.

In the extended model: 10% canopy loss gave +0.009 C FT (CI 0.007-0.011) and +0.076 EIVE light units; more recorded species gave lower FT (-0.096 C per log unit); last-summer temperature anomalies (-0.001 C per C, CI -0.010 to +0.009) and water-balance anomalies had no detectable effect on FT, EIVE moisture or the moisture index FW. EIVE temperature had a small negative slope on dT60 (-0.018, CI -0.033 to -0.003).

### 4.3 Species groups (Figure 3B)

For 556 species with at least 200 first-visit records (98% of records), the occupancy trends combined to four groups (C per decade of FT): losses of cold-affiliated species +0.036, gains of warm-affiliated species +0.027, gains of cold-affiliated species -0.022, losses of warm-affiliated species -0.021. The approximate sum (+0.021) is smaller than the model trend (+0.036) because the linear decomposition ignores changes in species number and rare species. In a weighted regression of relative species trends, STI (+0.0023 per year per C, SE 0.0006) and EIVE nitrogen (+0.0037 per year per unit, SE 0.0006) had independent positive effects; reaction also had a positive effect (+0.0013, SE 0.0004); light and moisture had no clear effect.

### 4.4 EIVE community means (Figure 4)

Cell-FE trends per decade: temperature +0.045 (0.036, 0.055), nitrogen +0.063 (0.047, 0.079), reaction +0.055 (0.041, 0.069), moisture +0.002 (-0.004, +0.007), light +0.011 (-0.005, +0.027). The FT trend stayed with EIVE-N as covariate (0.045 C per decade), and the EIVE-N trend stayed with FT as covariate. The EIVE-N year effects increased to +0.18 in 2019 and decreased to +0.05-0.08 in 2020-2022 (`files/results/h2_year_effects.csv`). We do not know the cause of this decrease. It can be an observation effect (the 2020 survey disruption or a protocol change) or a real change. Thus we do not give a single nitrogen trend as a result. The moisture index FW decreased (-4.0 mm per decade, CI -5.0 to -3.1), but EIVE moisture did not change.

### 4.5 Observation bias (Figure 1)

![Figure 1](files/figures/fig1_observation_bias.png)

- **Survey season.** NFI teams survey all year. Winter relevés have fewer herbs (17.5 species in January, 25 in June). Inside the same cells, January-February relevés had FT 0.12 C higher than July relevés (Figure 1C). This bias is two times the 2005-2022 change. The share of growing-season relevés was approximately constant over the years, so the trend did not change when we removed month effects.
- **Spatial sample rotation.** From 2010, part of each annual sample is revisits. The first-visit plots in 2010-2014 were further north and in 2015-2019 further south (Figure 1B). Naive annual means therefore have steps (FT about +0.1 C at 2015 and -0.09 C at 2020; EIVE-N +0.1 at 2010) that are as large as the 18-year climate signal (Figure 1A). A cell fixed-effects design removes them.
- **Recorder change.** Species number per relevé increased from 17.9 (2005) to 22.6 (2009) and was then stable; results from 2008 are the same. The share of the abundance code "weak presence" decreased from 0.62 to 0.41 (2005-2022), so we used presence only.
- **Pseudo-turnover.** Revisit lists share only 29% of species. High-similarity pairs gave the same results.

![Figure 3](files/figures/fig3_revisits_species.png)

![Figure 4](files/figures/fig4_eive_trends.png)

## 5. Discussion

The NFI understory flora changed toward warm-affiliated species everywhere in France, at 0.02-0.05 C per decade. This is 20-54% of the change that full tracking of the local warming would give, with a national value of 28% in the cross-sections and 18% in the revisits. The two designs use different plots and different contrasts but agree on the 5-year change (0.017-0.018 C).

The rate was constant through a decade of cooler 5-year means (2005-2013) and a decade of fast warming (2014-2022), and within plots it did not depend on the warming between visits. Thus the community did not respond to 5-year temperature anomalies at all (fast fraction about 0, upper bound 0.06). This agrees with the campaign synthesis (sci:sha256:0037934e440093284370046185fd30a78b7363fd6e940f8fd3d9860e2caedada), in which the fast fraction was 0.02 and the slow fraction 0.12. Two explanations fit: (a) a slow, lagged response to the warming since the 1980s (about 1 C at the NFI plots in 2013-2022 relative to 1985-1994), or (b) non-climatic drivers that correlate with warm affinity, for example forest management, canopy change, or nitrogen deposition. Our data cannot separate them. The constant rate and the absence of an interaction with the long-term warming of the cell are weak evidence against a simple lag model in which places that warmed more change more.

The extreme drought and heat summers (2018-2020, 2022) gave no detectable pulse in FT, EIVE moisture or the moisture index, neither in the year effects nor in the revisits.

Canopy loss raised FT and EIVE light, which agrees with microclimate buffering (Zellweger et al. 2020). But dense and open stands had the same FT trend, so canopy buffering does not explain the regional differences.

## 6. Limitations

- STIs use grid temperature at 0.25 degree without plot elevation; this adds noise and can make b_space smaller in mountains. Cross-fitting prevents circularity but not this bias.
- NFI relevés are made by different teams in all seasons. Month effects and growing-season subsets give the same results, but other observer effects (no observer identity in the data) remain.
- The cross-section is a correlational design; we cannot attribute the change to climate.
- We did not use nitrogen deposition data. The EIVE-N increase is not monotonic and its cause is unknown.
- Species of fewer than 20 first-visit records have no STI. Trees in the understory include seedlings, which can respond to stand dynamics.
- The SE region mixes Mediterranean and mountain plots.
- The DwC-A ends in 2022; later NFI campaigns are not included.

## 7. Open questions for later work

- Test whether nitrogen deposition (EMEP grids) explains the EIVE-N increase and the regional differences of the FT trend.
- Find the cause of the 2020 drop of EIVE-N (protocol, COVID-19 disruption or real).
- Add plot elevation (a DEM) to the STIs, and use the full NFI raw data (IGN open data) with management and stand variables.
- Repeat when 2023+ campaigns are published; the second revisit cycle (2020+) will give more pairs.

## 8. Reproduction

1. `bash files/code/00_retrieve.sh <inputs>` (or use the campaign shared store paths in `files/provenance/input_hashes.txt`).
2. `bash files/code/run_all.sh <inputs> <scratch> <results>` runs steps 01-10 (Python 3.12, numpy, pandas, pyarrow, xarray, netCDF4, scipy, statsmodels, matplotlib, openpyxl). Per-plot and per-species climate tables are written only in `<scratch>`. Run time on 2 CPUs: about 1.5 hours, mostly the bootstrap.
3. Outputs: `files/results/model_estimates.csv` (all planned models), `key_tracking_by_sample.csv`, `h2_year_effects.csv`, `posthoc_estimates.csv`, `season_profile_FT.csv`, `naive_year_means.csv`, `growing_season_share_by_year.csv`, `species_occupancy_trends.csv`, `bootstrap_fractions_{1,2}.csv`.

Code `01_parse_occ.py` streams `Occurrence.txt`; the awk command in `run_all.sh` extracts seven measurement types from the 23.6 GB `MeasurementOrFact.txt` stream. `fe.py` is a small fixed-effects OLS with CR1 cluster errors.
