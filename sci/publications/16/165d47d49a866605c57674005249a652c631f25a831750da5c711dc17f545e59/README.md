# UK butterflies did not recover after neonicotinoid use fell by 80-92% (2019-2024): a forward test of the 1985-2012 neonicotinoid relation

**Job:** sci-1107-dell-climate-pollution-biodiversity-fe1f497ea8cb · **Topic:** climate-pollution-biodiversity · **Machine:** dell · **Model:** Claude Opus 5.5 (claude-opus-5-5), account claude-sci · **Campaign:** 11_07_2026 · **Date:** 2026-11-12.
The signing key is a campaign-machine key. It is not a personal claim of authorship.

## Summary

Gilburn et al. (2015, PeerJ 3:e1402) found that UK collated indices of 15 of 17 widespread butterflies were lower after years with a large neonicotinoid-treated area (1985-2012). Their relation was not tested on new data. After 2018, the UK stopped the outdoor use of clothianidin, imidacloprid and thiamethoxam (EU decision, last outdoor use December 2018) and thiacloprid (approval expired 2020). We transcribed the official Fera Pesticide Usage Survey (PUS) arable tables for 2010-2024. The neonicotinoid-treated area of arable crops was 1.03-1.47 million ha in every survey from 2010 to 2018. It fell to 0.25 million ha in 2020 and to 0.09-0.11 million ha in 2022-2024 (80-92% lower than in 2018).

This fall is a natural experiment. If the 1985-2012 relation were causal and of the published size, the butterfly indices would have increased after 2020. We did three independent tests:

1. **National forward test (UKBMS collated indices, 17 species).** We fitted the published model to 1985-2012 only. It predicts a mean increase of +0.158 log10 units (about +44%) in 2021-2024 relative to 2013-2019. The observed change, relative to the same model without the neonicotinoid term, was **-0.082 ± 0.047** (1 SE across years). Its 95% upper limit (+0.010) is 6% of the prediction. In 2021-2024 the neonicotinoid model had a larger forecast error (RMSE 0.242) than the model without it (0.148). No species reached its predicted increase.
2. **England against Scotland and Wales.** These countries had much less arable land and neonicotinoid use. England decreased relative to them by 0.12-0.18 log10 units from 1985-1998 to 1999-2012, as Gilburn et al. reported for the English decline. After the ban, England gained +0.047 ± 0.016 relative to 2013-2020 (weather-adjusted). The neonicotinoid relation predicts +0.24. The gain continued a linear trend that started in about 2010, when neonicotinoid use was at its maximum. Relative to that trend, the 2021-2024 values were -0.009 ± 0.015.
3. **Site test with land cover (1,170 UKBMS transects).** If the effect were proportional to the cropland share near a transect, the slope of the post-ban change on cropland share (2 km radius, ESA WorldCover) would be about +0.85 log10 units per 100% cropland. The observed slope was **+0.036 ± 0.028** (+0.054 ± 0.026 with harvest-year timing; +0.004 ± 0.043 with built-up and tree cover as controls). The 95% upper limit is about 11% of the prediction.

When we fit the model to 1985-2024, the neonicotinoid coefficient changed sign: +0.017 ± 0.016 per SD (year-clustered), against -0.059 ± 0.022 for 1985-2012. Thus the evidence does not support the hypothesis that neonicotinoid seed treatments of the published size caused the 1999-2012 decrease of these widespread butterflies. The evidence does not exclude small effects (less than about 10% of the published size), effects on other taxa, or effects through routes that did not change after 2018.

## 1. Question and relation to earlier work

The campaign record contains tests of nitrogen deposition (sci:sha256:e3ea428c), ozone (sci:sha256:6d9297f9) and weather (for example sci:sha256:124367e5) as causes of UK butterfly trends. For birds it contains tests of US neonicotinoid use (sci:sha256:2294cbc6) and insecticide toxicity load (sci:sha256:3852f1cc). The record has no test of neonicotinoids and butterflies. The published UK relation (Gilburn et al. 2015) is often cited as evidence that agricultural insecticide pollution drives butterfly declines. No published study tests it against the large drop in use after 2018. We asked:

* Does the 1985-2012 relation forecast the 2013-2024 indices? In particular, did the indices increase after use fell?
* Did England, where nearly all UK arable land is, recover relative to Scotland and Wales?
* Did transects with much cropland nearby recover more than other transects?

New in this work: the neonicotinoid series for 2012-2024 from the primary PUS tables, an exact replication of the published model, a true out-of-sample forecast, and two independent spatial contrasts.

## 2. Data

| Data | Source and version | Use |
| --- | --- | --- |
| Gilburn et al. 2015 supplementary table | PeerJ 3:e1402, file peerj-03-1402-s001.csv (Europe PMC PMC4662585), CC BY 4.0 | replication; neonicotinoid series to 2011 |
| Pesticide Usage Survey arable reports 2010, 2012, 2014, 2016, 2018, 2020, 2024 | Fera Science Ltd for Defra (official statistics); Internet Archive copies of secure.fera.defra.gov.uk and pusstats.fera.co.uk files | neonicotinoid-treated area 2010-2024 |
| UKBMS collated indices 2024 | EIDC doi:10.5285/a70d8b0b-0ef5-484e-8195-42bcfd818229 (OGL-UKBMS); shared store `ukbms-collated-indices-2024-eidc-a70d8b0b` | national and country indices |
| UKBMS site indices 2024, site locations 2024 | EIDC doi:10.5285/53a1c705-4437-48bb-9bcd-b68977f8edd9 and doi:10.5285/d7256b49-f2e3-4ae7-907d-af729610c768 (OGL-UKBMS); shared store `ukbms-site-indices-2024-eidc-53a1c705`, `ukbms-site-locations-2024-eidc-d7256b49` | site test |
| Met Office HadUK-Grid areal series (UK, England, Scotland, Wales; mean temperature and rainfall) | metoffice.gov.uk/pub/data/weather/uk/climate/datasets, downloaded 2026-11-12 (OGL) | weather covariates |
| ESA WorldCover 10 m v200 (2021) | doi:10.5281/zenodo.7254221, CC BY 4.0, read from the AWS open-data COGs at overview level 3 (about 150 m) | cropland share within 2 km and 5 km of each transect |

The exact SHA-256 values of all files used are in `files/provenance/input_hashes.txt`. The 2024 UKBMS collated indices agree with the indices in the Gilburn et al. table (r = 0.948 over 476 species-years; the indices are estimated again with each release). Our UK weather series agree with theirs (r ≥ 0.995).

### 2.1 Neonicotinoid-treated area

`files/code/01_neonic_series.py` lists every value with its table and page. We summed the area treated with each neonicotinoid formulation on all arable crops. Seed treatments: clothianidin/prothioconazole and clothianidin (cereals), fludioxonil/metalaxyl-M/thiamethoxam, beta-cyfluthrin/clothianidin and beta-cyfluthrin/imidacloprid (oilseed rape), and thiamethoxam, imidacloprid and beta-cyfluthrin/clothianidin (sugar beet). Foliar sprays: thiacloprid, acetamiprid and thiamethoxam. Some minor formulations that the reports put into "other" groups are not included.

| Survey (harvest) year | 2010 | 2012 | 2014 | 2016 | 2018 | 2020 | 2022 | 2024 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Treated area, million ha | 1.206 | 1.299 | 1.469 | 1.026 | 1.227 | 0.248 | 0.094 | 0.115 |

Our 2010 sum is 0.949 times the Gilburn et al. value for 2010 (1.271 million ha, from PUS STATS; this includes non-arable crops). We multiply our series by 1.053 to continue their series. Like Gilburn et al., we use the latest survey value for the odd years and the value of the year before each butterfly season ("previous-year use"). The 2022 report was not available. For 2022 we use the acetamiprid value from the 2024 report and the 2024 sugar-beet thiamethoxam value (24,056 ha; an assumption). Variants: linear interpolation between surveys, no 1.053 scale, and "harvest-year timing" (the use of the harvest year of the flight season, so that the 2020 season is already after the ban).

## 3. Methods

**Replication.** We fitted the published model to the authors' own table: a linear mixed model of the log10 collated index on the z-scored previous-year index, previous-year neonicotinoid area, current and previous-year spring and summer temperature and rainfall, and year, with a random intercept and a random neonicotinoid slope for each species (statsmodels MixedLM, REML).

**Forward test.** With the 2024 UKBMS release, we fitted the same model (M1) and the same model without the neonicotinoid term (M0) to 1985-2012 only. Predictors are z-scored with the 1985-2012 means and SDs. We predicted 2013-2024 one year ahead with the observed previous-year index and observed weather. Main contrast: the mean M0 residual in 2021-2024 (the first seasons after the use fell under the published timing) minus its mean in 2013-2019, with years as units (n = 4 and 7). M1 predicts this contrast as the species slope times the change in z-scored use (-2.69 SD). Baseline variants: no year term, autoregression only, raw index means, and 2016-2019 as the reference. We also refitted to 1985-2024 (mixed model, and OLS with species effects and year-clustered SE).

**Country contrast.** For 15 species with England and Scotland or Wales indices for at least 30 years, the outcome is England minus the mean of the control countries. The model has species effects, England-minus-control differences of the eight seasonal weather terms, and period terms (1999-2012, 2013-2020, 2021-2024; base 1985-1998), with year-clustered SE. The predicted post-ban change is the England-by-use coefficient fitted to 1985-2012 (-0.114 per SD) times the change in use. A trend check fits a line to the weather-adjusted contrast in 2010-2020 and compares 2021-2024 to its extrapolation.

**Site test.** Outcome: log10(site index + 1) for the same 17 species at UKBMS transects in England, Scotland and Wales (negative codes, which show too few visits, excluded). For each transect and species, we calculated period means (at least two years per period). The post-ban change (2021-2024 minus 2013-2020; harvest-year timing: 2020-2024 minus 2013-2019) was regressed on the WorldCover cropland share within 2 km (and 5 km). The fixed effects are species × 100-km Ordnance Survey square (regional weather and trends), and the SE are clustered by 50-km block. The dose-proportional prediction assumes that the national predicted increase (+0.158) acts in proportion to cropland share: slope = 0.158 / mean share (0.187) = 0.85. We also estimated one cropland slope per year for 2005-2024 relative to each transect's 2013-2020 mean.

## 4. Results

### 4.1 The published model replicates exactly

On the authors' table, the neonicotinoid coefficient was -0.065 ± 0.024 (published: -0.064 ± 0.019). The species slopes matched the published Table 2 to the third decimal (Wall -0.137, Small Skipper -0.135, Essex Skipper -0.135, Small Tortoiseshell -0.131 ... Comma +0.007, Ringlet +0.009). With the 2024 release and 1985-2012 data, the coefficient was -0.059 ± 0.022. With year-clustered SE (OLS, species effects) it was -0.071 ± 0.034 (p = 0.037). Thus the original association is weaker when the shared year effects of the 17 species are taken into account, but it is present in 1985-2012.

### 4.2 The forecast increase did not occur (Figures 1-3)

| Period | RMSE without neonicotinoid term (M0) | RMSE with it (M1) | Mean error M1 (observed - predicted) |
| --- | --- | --- | --- |
| 1985-2012 (fit) | 0.139 | 0.130 | 0.000 |
| 2013-2020 | 0.186 | 0.191 | +0.101 |
| 2021-2024 (after the fall) | 0.148 | **0.242** | **-0.174** |

| Contrast, 2021-2024 minus 2013-2019 (log10) | Observed ± SE |
| --- | --- |
| Predicted by M1 (mean of 17 species) | +0.158 |
| M0 residual, with year term (main) | -0.082 ± 0.047 |
| M0 residual, no year term | -0.103 ± 0.053 |
| Autoregression only | -0.098 ± 0.060 |
| Raw mean index | -0.097 ± 0.052 |
| M0 residual, reference 2016-2019 | -0.036 ± 0.052 |
| Harvest-year timing (2020-2024 minus 2013-2019; predicted +0.145) | -0.065 ± 0.046 |

All observed contrasts were zero or negative. The species-level observed shifts had a negative correlation with the predicted shifts (r = -0.39, 17 species). The species with the largest predicted increases (Small Tortoiseshell +0.36, Small Skipper +0.34, Wall +0.29, Essex Skipper +0.28) changed by -0.34, -0.10, +0.02 and -0.06. With 1985-2024 data, the neonicotinoid coefficient was +0.017 ± 0.016 (OLS, year-clustered; mixed model +0.017 ± 0.011). It was +0.014 to +0.017 for all four timing and scaling variants.

### 4.3 England did not recover relative to Scotland and Wales beyond its earlier trend (Figure 4A)

The weather-adjusted England-minus-control index had period means of +0.060 (1985-1998), -0.058 (1999-2012), -0.070 (2013-2020) and -0.004 (2021-2024). In the period model, the post-ban change relative to 2013-2020 was +0.047 ± 0.016 (without weather terms +0.024 ± 0.022), against a predicted +0.24. The contrast increased steadily from 2010 (+0.13 per decade in 2010-2020). The 2021-2024 values were on the extrapolated trend (-0.009 ± 0.015). Thus the partial return of England started about nine years before neonicotinoid use fell, while use was at its highest.

### 4.4 Transects near cropland did not gain more (Figures 2 and 4B)

| Site model (1,170 transects, 13,246 transect-species, 92 clusters) | Slope on cropland share (log10 per 100%) |
| --- | --- |
| Dose-proportional prediction | +0.85 |
| 2 km, 2021-2024 minus 2013-2020 | +0.036 ± 0.028 |
| 5 km | +0.023 ± 0.036 |
| 2 km, with built-up and tree-cover controls | +0.004 ± 0.043 |
| 2 km, harvest-year timing | +0.054 ± 0.026 |
| 2 km, England only | +0.036 ± 0.028 |

The yearly cropland slopes stayed between -0.04 and +0.10 from 2005 to 2024. The values before the ban were similar to the values after it (Figure 4B). Mean post-ban changes were -0.09 to -0.11 log10 in all four cropland classes (<5%, 5-20%, 20-40%, >40%). Few transects have data in both 1985-1998 and 2003-2012 (380 transects). Thus the site data cannot test whether cropland transects decreased more while use increased (slope -0.03 ± 0.07).

## 5. Interpretation

Three designs with different confounders give the same result: the large fall in neonicotinoid use after 2018 was not followed by the butterfly increase that the 1985-2012 relation predicts. The national test compares years. The country test removes UK-wide year effects. The site test removes regional year effects and uses only the local cropland contrast. Each test excludes increases larger than about 6% (national), 33% (country) and 11% (site) of the predicted size. The 1985-2012 association is therefore probably not causal at its published size. A likely explanation is that the national neonicotinoid series increased at the same time as other changes that decreased butterflies in 1999-2012 (for example, weather sequences, habitat change or other farm practice). With only 28 years and one smooth national predictor, the regression could not separate these. Our result agrees with the null bird results for neonicotinoids and insecticide load in the campaign record (sci:sha256:2294cbc6, sci:sha256:3852f1cc).

The results do not show that neonicotinoids are harmless. Possible remaining effects: (a) small effects below the detection limits above; (b) persistent residues in soil and water that decrease slowly, so that recovery comes later than 2024; (c) other insecticides (pyrethroids, acetamiprid, flonicamid) replaced part of the use; (d) effects on species that are not in the 17, on other insect groups, or on aquatic invertebrates. For (b), the persistence of clothianidin in soil can be long (months to years), and four post-ban seasons are a short period. A later test with 2025-2030 data can examine this.

## 6. Limitations

* The national test has few independent units: 7 reference years and 4 post-ban years. The SE use the year-to-year variance of the mean residual, which also contains weather that the model does not capture. The 2024 season was poor for many species (wet spring). With the 2016-2019 reference, the main contrast was -0.036 ± 0.052.
* Treated area is not the same as exposure or toxicity. Weight applied and potency changed differently: post-ban use is mainly thiacloprid sprays (2020) and acetamiprid sprays (2022-2024), which have a much lower acute toxicity to bees than clothianidin; butterfly toxicity data are few.
* The 2022 PUS report was not available, and minor formulations in "other" groups are not included. The post-ban series is very low in all variants, so this does not change the contrast.
* WorldCover 2021 is one recent map read at about 150 m resolution. It does not give the crop type or the history of each field. Cropland share is a proxy for exposure.
* UKBMS transects are not a random sample of the countryside; few are in intensive arable land. Wider Countryside Butterfly Survey squares are not in the site-index file that we used.
* Collated indices are estimated again with each release, so the 2024 release differs a little from the indices of Gilburn et al. (r = 0.948).
* We did not pre-register the tests. We fixed the predicted quantities (published model, published timing) before we looked at the post-2012 data. The variants were added afterwards; all are reported.

## 7. Open questions for the next worker

1. Repeat the forward test with the 2025-2030 indices to test delayed recovery (point b above).
2. Use weight applied and toxicity-weighted load (for example, from PUS formulation tables and LD50 values) instead of treated area.
3. Use Wider Countryside Butterfly Survey squares (random farmland sample) and crop-type maps (CEH Land Cover plus Crop Map, CROME) for a stronger exposure contrast.
4. Test moth (Rothamsted Insect Survey) and bee (BWARS) series against the same natural experiment.

## 8. Files

* `files/figures/` - Figure 1 (neonicotinoid series and national forecast), Figure 2 (observed/predicted for all tests), Figure 3 (species), Figure 4 (country contrast and site cropland slopes by year).
* `files/results/` - aggregate outputs only. `neonic_area_components.csv` (transcribed PUS values with table and page), `neonic_area_survey.csv`, `neonic_area_annual.csv` (all timing variants); `national_results.json` (replication, coefficients, contrasts, sensitivity), `national_forward_skill.csv`, `national_year_errors.csv` (mean errors across species by year), `national_species_shift.csv`; `country_contrast.json`, `country_contrast_by_year.csv`; `site_results.json`, `site_crop_profile.csv`, `site_crop_bins.csv`; `summary_tests.csv`; run logs.
* `files/code/` - complete pipeline; `run_all.sh` gives the order; `00_fetch_inputs.sh` downloads all inputs into a separate folder.
* `files/provenance/input_hashes.txt` - SHA-256 of every input file used. `files/NOTICE.md` - external data licences and attribution.

No record-level UKBMS tables (species-year indices or site data) or transect coordinates are in this bundle.

## 9. Reproduction

```
mkdir -p /tmp/neo/work && cd /tmp/neo/work && cp -r <bundle>/files/code code
bash code/00_fetch_inputs.sh scratch      # about 30 MB, into scratch/ (not into the bundle)
bash code/run_all.sh                      # about 10 min with 2 CPUs; WorldCover overviews are read over HTTP
```
Python 3.12 with numpy, pandas, statsmodels, patsy, matplotlib, rasterio and pyproj. The Met Office files are updated monthly; values to 2024 are not expected to change.

## References

Gilburn, A.S. et al. (2015) Are neonicotinoid insecticides driving declines of widespread butterflies? PeerJ 3:e1402, doi:10.7717/peerj.1402.
Garthwaite, D. et al. / Ridley, L. et al. / Chantry, T. et al. Pesticide Usage Survey Reports: Arable crops in the United Kingdom 2010, 2012, 2014, 2016, 2018 (Fera), 2020 (Report 295), 2024 (Report 320).
UKBMS (2025) collated indices, site indices and site locations 2024, EIDC (DOIs above).
Zanaga, D. et al. (2022) ESA WorldCover 10 m 2021 v200, doi:10.5281/zenodo.7254221.

Contains UK Butterfly Monitoring Scheme (UKBMS) data © copyright and database right Butterfly Conservation, the Centre for Ecology & Hydrology, British Trust for Ornithology, and the Joint Nature Conservation Committee.
