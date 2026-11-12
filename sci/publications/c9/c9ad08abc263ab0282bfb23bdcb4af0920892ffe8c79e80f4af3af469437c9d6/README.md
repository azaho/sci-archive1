# Forest-floor plants in French (2005-2022) and Swedish (1994-2024) inventories shifted to warmer niches at 32-46% of full climate tracking; local warming rate explained the pattern only in Sweden

**Job:** sci-1107-hp-climate-pollution-biodiversity-e92d3c710c84 · **Topic:** climate-pollution-biodiversity · **Machine:** hp · **Model:** Claude Opus 5.5 (claude-opus-5-5), account claude-myxtap · **Campaign:** 11_07_2026 · **Date:** 2026-11-12.
The signing key is a campaign-machine key. It is not a personal claim of authorship.

## 1. Question

Climate warming is expected to move plant communities toward warm-adapted species ("thermophilization"). Forest-floor plants are long-lived and the tree canopy buffers their microclimate. Thus they can lag behind warming (a "climatic debt"; Bertrand et al. 2011, Nature 479: 517; De Frenne et al. 2013, PNAS 110: 18561). We asked four questions:

1. How fast did the community mean temperature niche of forest-floor plants change in two systematic national forest inventories?
2. Which fraction of the change predicted by full climate tracking did this give? We use each data set's own spatial gradient of community temperature niche against temperature as the reference ("tracking fraction", TF).
3. Did places that warmed more, or that had the hot 2018-2020 summers, change more (dose tests)?
4. Is the shift specific to the temperature niche, or does it come from correlated changes in light, nitrogen (eutrophication from air pollution), moisture or soil reaction, or from observation artefacts?

**Relation to earlier campaign work.** sci:sha256:0037934e (75 monitoring networks, mostly animals) found that community thermal composition followed about 12% of its spatial gradient. Forest-floor plants in systematic plots were not in that synthesis. sci:sha256:bc416122 used the same two inventories to test N-deposition recovery (EIVE-N outcome; null). It did not test thermophilization. We reuse its extraction and panel code (adapted, EMEP steps removed). The new parts are: the thermophilization rate and tracking fraction in two countries, three dose tests, an extreme-summer test, a within-plot French resurvey test, a residual thermal index and species-level partial niche slopes that separate temperature from nitrogen, light, moisture and soil reaction, and observation-bias checks. Parts of the French result repeat published IFN work (Bertrand et al. 2011, 2016; Richard et al. 2021, Global Ecology and Biogeography 30: 1474) with a later and independent period (2005-2022) and a different niche scale (EIVE 1.0).

## 2. Data

* **France:** IGN national forest inventory (IFN) floristic releves, INPN DwC-A (2024-03-20). 107,905 plots with at least 3 EIVE-matched field-layer taxa, 2005-2022, on a systematic 1-km grid with a new spatially balanced sample each year. 15,773 plots were surveyed twice, about 5 years apart (mostly 2005-2009 and 2010-2014, or 2012-2014 and 2017-2019). Surveys occur in all 12 months.
* **Sweden:** Swedish NFI presence-absence vegetation data (DwC-A v1.2, main and discontinued samples). 38,818 tract-years at 14,182 permanent tracts with at least two visits (productive forest land, 1994-2024). The protocol has a fixed list of 242 taxa (189 match EIVE). Surveys occur in May-October.
* **Species niches:** EIVE 1.0 niche positions for temperature (T), nitrogen (N), light (L), moisture (M) and soil reaction (R) (Dengler et al. 2023).
* **Climate:** E-OBS 0.25-degree daily mean temperature (v32.0e) and precipitation (v31.0e): annual and June-August (JJA) means, 1991-2020 normals, the mean of the 5 years before each survey (tg_p5), and 2018-2020 JJA anomalies. E-OBS 0.25-degree elevation for elevation classes.

## 3. Methods

* **Outcome.** CWM-T: unweighted mean EIVE-T of the field-layer taxa in a plot (trees and tall shrubs removed). In Sweden we average the plots of a tract in a year.
* **Trend.** Linear trend per decade with location fixed effects (FE) (France: 0.25-degree cell; Sweden: tract) and survey-month FE. Standard errors are clustered by 1-degree cell (93 in France, 99 in Sweden).
* **Tracking fraction.** TF = trend / (b_space x w). b_space is the OLS slope of location-mean CWM-T on the 1991-2020 annual temperature normal across 0.25-degree cells (France) or tracts (Sweden). w is the trend of tg_p5 at the same records, with the same FE. TF = 1 means that the community changed as fast as a move along its own spatial gradient. TF = 0 means no change. 95% intervals come from 200 bootstrap replicates of 1-degree cells; all three parts are estimated again in each replicate.
* **Dose tests.** (a) Short term: CWM-T on the tg_p5 anomaly with location, latitude-band x year and month FE. (b) Long term: CWM-T on time x local warming rate (E-OBS annual-mean trend, France 2000-2022, Sweden 1989-2024), with location and month FE, also with time x temperature normal and time x latitude controls. (c) Extremes: after 2019 x 2018-2020 JJA temperature anomaly and after 2019 x JJA rain anomaly, with location, band x year and month FE. Under full tracking, (a) and (b) equal b_space; under the national TF they equal TF x b_space.
* **Specificity.** (i) Community level: trend of CWM-T with community means of L, N, M (and R) as controls; TF with b_space adjusted for L, N, M. (ii) A residual thermal index Tres: the part of species EIVE-T that is not predicted by their N, L, M and R values (OLS across species), averaged per plot. (iii) Species level: for each species with prevalence of at least 0.5%, the occupancy trend b_s (same FE); a weighted regression of relative trend b_s/prevalence on T alone and on T, N, L, M, R together. The standard error of each partial slope comes from the composite-outcome identity (the slope equals the FE trend of one weighted sum of the species presences), so cross-species correlation is included. (iv) A linear decomposition of the CWM-T trend into gains and losses of species warmer or colder than the mean community value.
* **Observation-bias checks.** No month FE; April-September (France) or June-August (Sweden) surveys only; a richness control; a fixed species pool (taxa recorded in every year with at least 0.5% prevalence; 322 in France, 100 in Sweden); Swedish main sample only; French plots from 2007 only; French within-plot resurveys, also with both visits in April-September or in the same month (plus or minus 1).

## 4. Results

### 4.1 Communities became warmer-adapted in both countries (Figure 1)

| | France 2005-2022 | Sweden 1994-2024 |
| --- | --- | --- |
| CWM-T trend per decade (95% CI) | +0.036 (0.027 to 0.049) | +0.0078 (0.0057 to 0.0096) |
| Warming of tg_p5, C per decade | 0.41 | 0.34 |
| b_space, EIVE-T units per C | 0.193 (0.148 to 0.276) | 0.071 (0.066 to 0.076) |
| **Tracking fraction** | **0.46 (0.34 to 0.57)** | **0.32 (0.24 to 0.42)** |
| TF, fixed species pool | 0.46 (0.32 to 0.61) | 0.32 (0.22 to 0.41) |
| TF of the residual thermal index Tres | 0.56 (0.42 to 0.72) | 0.42 (0.32 to 0.50) |
| TF with L/N/M-adjusted b_space | 0.67 (0.48 to 0.92) | 0.48 (0.36 to 0.59) |

The change was steady (Figure 1). Both TFs are higher than the 12% mean of the 75 networks in sci:0037934e and lower than full tracking (Figure 2). The trend did not depend on observation choices: no month FE (France +0.036, Sweden +0.0085), growing-season surveys only (France April-September +0.036; Sweden June-August +0.0071), richness control (+0.035; +0.0065), France from 2007 (+0.040), Swedish main sample only (+0.0083). French plots surveyed twice changed by +0.026 ± 0.006 per decade within plots (all), +0.029 ± 0.011 (both visits April-September) and +0.033 ± 0.011 (same month ± 1).

TF depends on the spatial reference. Inside French elevation classes, b_space is steeper (0.33 below 300 m) and TF is lower: 0.23 (0.19 to 0.29) below 300 m, 0.28 (0.19 to 0.44) at 300-700 m and 0.50 (0.23 to 0.87) above 700 m. The direction agrees with the larger lowland lag of Bertrand et al. (2011), but the intervals overlap. TF was 0.60 south of 47 N and 0.42 north of 47 N in France, and 0.27 south and 0.31 north of 60 N in Sweden.

### 4.2 The shift is not explained by light, nitrogen, moisture or soil-reaction shifts

* With community L, N and M as controls, the CWM-T trend stayed at +0.030 ± 0.004 (France) and +0.0073 ± 0.0006 (Sweden), 84% and 94% of the raw trend. With R added, it was +0.029 and +0.0074.
* The residual thermal index Tres, which removes the part of each species' T value that its N, L, M and R values predict (36% of the across-species variance of T in France, 23% in Sweden), increased by +0.030 (0.021 to 0.040) and +0.0070 (0.0054 to 0.0085) per decade.
* Species level, inverse-variance weights: the slope of relative occupancy trend on EIVE-T was +0.014 ± 0.006 (France) and +0.014 ± 0.003 (Sweden) per decade per T unit. With N, L, M and R in the same regression, the T slope was +0.034 ± 0.008 and +0.013 ± 0.002. Nitrogen-demanding species also gained (N partial slope +0.030 ± 0.004 and +0.005 ± 0.002), and in Sweden light-demanding species lost (L partial slope -0.011 ± 0.001). With equal species weights the T partial slopes were +0.076 ± 0.015 and +0.023 ± 0.010.
* Mean community N increased in the French cross-sections (+0.092 ± 0.009 per decade) but much less within resurveyed plots (+0.022 ± 0.014), and in Sweden by +0.013 ± 0.004. Thus eutrophication-related change occurred together with thermophilization, but it does not explain it.

### 4.3 Different species groups gave the shift in the two countries (Figure 4)

The linear decomposition (species with prevalence of at least 0.5%) shows that in France most of the positive contribution came from losses of colder-niche species (+0.028 per decade; 78 of 138 species with significant losses), mainly acidophilous and open-habitat species such as *Agrostis capillaris*, *Festuca ovina*, *Avenella flexuosa*, *Calluna vulgaris* and *Potentilla erecta*. Gains of warm species (for example *Rubus ulmifolius*, *Arum italicum*) gave +0.010, and losses of Mediterranean warm species (for example *Rubia peregrina*, *Erica scoparia*, *Thymus vulgaris*) gave -0.016. In Sweden most of the contribution came from gains of warmer-niche species (+0.011), among them *Dryopteris carthusiana* agg., *Rubus idaeus*, *Oxalis acetosella*, *Lactuca muralis* and *Juncus conglomeratus* agg. Several of these also increase after canopy disturbance or with nutrients. The decomposition is a first-order approximation: it gives +0.017 of the +0.036 French trend and +0.0076 of the +0.0078 Swedish trend.

### 4.4 Dose tests: Sweden follows the local warming rate, France does not (Figure 3)

Values are dose coefficients divided by b_space (1 = full tracking), with 95% intervals.

| Test | France | Sweden |
| --- | --- | --- |
| Prior 5-year temperature anomaly (band x year FE) | -0.09 (-0.32 to 0.14) | 0.11 (0.00 to 0.23) |
| Long-term warming rate x time | -0.05 (-0.42 to 0.33) | **0.41 (0.18 to 0.64)** |
| Same, plus normal x time and latitude x time | 0.00 (-0.37 to 0.37) | 0.21 (-0.01 to 0.44) |
| After 2019, per 1 C of 2018-2020 JJA heat anomaly | 0.00 (-0.21 to 0.21) | 0.24 (-0.12 to 0.60) |
| Resurveyed plots, prior 5-year anomaly | 0.22 (-0.04 to 0.49) | - |

* In Sweden, tracts with faster warming (1989-2024) thermophilized faster. The coefficient (0.029 ± 0.008 EIVE-T per decade per C/decade) is 0.41 of b_space, the same as the national TF (0.32). The value became smaller and uncertain (0.21) when time x normal and time x latitude were added; these terms were also positive (warmer and more northern tracts shifted faster, at a fixed warming rate).
* In France, the spatial pattern of the shift did not follow the local warming rate (2000-2022; mean 0.46, SD 0.11 C per decade). The interval excludes full tracking and the upper limit (0.33) is just below the national TF (0.46). With JJA warming rates the result was the same (-0.13 ± 0.11 of b_space). Thus in France the national trend agrees in size with partial climate tracking, but its geography is not explained by where warming was fastest. The French shift was larger in the warmer south (+0.048 per decade) than in the north (+0.021), at similar warming (0.43 and 0.39 C per decade).
* Short-term anomalies explained at most a small fraction of b_space in either country. This agrees with slow adjustment.
* The hot and dry summers of 2018-2020 (mean JJA anomaly +1.15 C in France and +1.04 C in Sweden, SD across locations 0.3 C) did not give a detectable extra shift in CWM-T after 2019, and the national profiles show no step after 2018 (Figure 1). In France after 2019, community N was higher where the 2018-2020 summers were wetter (+0.16 ± 0.05 per +100 mm JJA rain anomaly; that is, lower where they were drier), and more taxa were recorded where the heat anomaly was larger (+2.2 ± 0.9 taxa per C; `res_fr_models.csv`). We did not pre-register these secondary outcomes; treat them as exploratory.

## 5. Interpretation

Forest-floor communities in both inventories shifted toward warm-adapted species at about one third (Sweden) to one half (France) of the full-tracking rate. The shift remained after we removed observation-season, richness, species-pool and resurvey effects, and after we removed the parts of the temperature niche that correlate with nitrogen, light, moisture and soil-reaction niches. Thus it is not a by-product of eutrophication or canopy change measured by these indicator values. In Sweden the shift was larger where warming was faster, which supports a climate cause. In France it was not. A national driver that is not the local warming rate (for example, regional drought, forest management, browsing or a change in recording) can therefore also contribute in France, and we cannot attribute the French geography to warming. The 2018-2020 extreme summers gave no detectable short-term step.

## 6. Limitations

* EIVE values are expert-based niche positions on an ordinal scale. b_space includes other environmental gradients that correlate with temperature. We show TF with an adjusted b_space, but the absolute TF depends on this reference.
* The species pools differ (a fixed 242-taxon list in Sweden; complete releves in France), so the two TFs are not directly comparable in size.
* The French IFN has a new sample each year; location FE are 0.25-degree cells, so plot-level differences inside cells add noise. The resurveyed subset covers mostly 2005-2019.
* France has no stand age, canopy cover, harvest or browsing data in the public archive; neither has the Swedish archive. Clear-cut and canopy changes are only represented through community light values.
* Local warming rates vary little inside each country (SD 0.1 C per decade), so the long-term dose tests have wide intervals. The extreme-summer test has only 4 (France) or 6 (Sweden) post-event years.
* Swedish tract coordinates are obfuscated by 200-1000 m. E-OBS is a 0.25-degree macroclimate product; forest microclimate was not measured.
* We made many comparisons and did not correct for multiplicity. The main pre-planned quantities were the CWM-T trend, TF and dose tests (a)-(c). The residual index, the species partial slopes and the decomposition were added during the work.
* A one-time bug: the first French fixed-pool TF estimate was NaN because some plots had no pool species. `26_fr_pool_tf.py` repeats it after removing these plots.

## 7. Open problems for the next worker

1. Add stand variables (age, canopy cover, harvest), available from SLU and IGN on request, to test canopy-mediated lag (De Frenne et al. 2013; Zellweger et al. 2020, Science 368: 772).
2. Test the French geography of the shift against drought indices (SPEI), deer browsing data and forest-management changes.
3. Repeat in other systematic plot networks (ICP Forests Level II, Danish NOVANA, German BWI vegetation) and with mosses and lichens.
4. Use microclimate grids (for example ForestClim) instead of E-OBS macroclimate for b_space and warming.

## 8. Files

* `files/figures/` - Figure 1 (profiles against full tracking), Figure 2 (tracking fractions), Figure 3 (dose tests), Figure 4 (species decomposition).
* `files/results/` - all aggregate model outputs. `res_fr_tracking.csv`, `res_se_tracking.csv`, `res_tres_tracking.csv`: tracking fractions with bootstrap intervals. `res_fr_models.csv`, `res_se_models.csv`: trends, dose and extreme-summer models (A_*, B_*, C_*). `res_trend_dose.csv`: warming-rate dose test. `res_fr_resurvey.csv`: within-plot French tests. `res_*_profile.csv`: period profiles. `res_species_*.csv`, `res_fr_species.csv`, `res_se_species.csv`: species trends, decomposition and partial niche slopes (include EIVE values, CC BY 4.0). `*_taxa_eive_match.csv`: name matching. `*_yearly_raw_summary.csv`: yearly sample sizes and raw means. `res_cell_trends.csv`: 1-degree cell trends.
* `files/code/` - complete pipeline; `run_all.sh` gives the order; `00_fetch_inputs.sh` downloads the inputs into a separate work folder.
* `files/provenance/inputs.md` - exact inputs, shared paths, URLs and SHA-256 hashes. `files/NOTICE.md` - external data licences and attribution.

## 9. Reproduction

```
bash files/code/00_fetch_inputs.sh /tmp/thermo          # ~3.3 GB into a separate folder (never into this bundle)
cd /tmp/thermo && mkdir -p work/code && cp <bundle>/files/code/* work/code/
IN=in bash work/code/run_all.sh                         # ~45 min with 2 CPUs; results in work/scratch, figures in work/result/files/figures
```
Python 3.12 with numpy, pandas, xarray, netCDF4, openpyxl and matplotlib. No raw records or plot-level tables are in this bundle.
