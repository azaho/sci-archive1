# BioTIME v2 marine assemblages did not show larger richness gains with warming in warmer seas

## Summary

Antao et al. (2020, Nature Ecology & Evolution 4:927) used BioTIME v1 temperate assemblages (23.5-60 degrees latitude). They reported that marine species richness increased with local warming, and that this increase was about twice as large in warmer locations. They also reported that warming coincided with abundance loss in the warmest marine locations, and that land assemblages had no systematic response.

BioTIME 2.0 (Zenodo 15222193, 15 April 2025) has 708 studies. The metadata field `DATE_TO_DB` puts 326 studies in 2016-2019 (the v1 era) and 382 studies in 2024. We used the 2024 studies as an independent replication sample. We used the v1-era studies to re-test the original claim with our own pipeline.

We built 22,996 temperate assemblage time series (study x ~11 km cell, at least 5 sampled years) from 374 studies. We rarefied each year to the minimum number of samples in that series. We calculated per-decade OLS slopes of log richness (S) and log total abundance (N). Then we regressed these slopes on the local temperature trend (dT, C/decade) and its interaction with baseline temperature (Tc). Sea temperatures came from NOAA ERSSTv5 and land temperatures from NOAA GHCN_CAMS.

Main results (Marine, richness):

* **There was no overall richness gain with local warming.** At a 15 C baseline, the dT slope was -0.04 +- 0.12 (v1 era, 82 studies, 13,968 assemblages) and +0.15 +- 0.13 (2024 studies, 32 studies, 1,090 assemblages). These values are log-richness change per decade per 1 C/decade of warming, with equal weight per study and study-clustered SE. In the pooled data, the slope was +0.02 +- 0.10 (95% CI -0.18 to +0.22).
* **The warming x baseline interaction had the sign opposite to the published claim.** It was negative in 38 of 42 model specifications and positive with p < 0.05 in none. With inverse-variance random-effects weights (the published weighting), the v1-era estimate was -0.041 +- 0.007 per C (p = 5e-10). This value stayed between -0.043 and -0.032 when we removed any one study. Thus warming was linked to richness gains in cool water (about +8% per decade at 5 C baseline for 0.2 C/decade of warming) and to losses in warm water (about -4% per decade at 20 C). In the 2024 studies, the equal-weight interaction was -0.034 +- 0.023 (not clear). The inverse-variance estimate for the 2024 studies is controlled by a single seabird survey that holds 80% of the weight. Without that survey, the estimate was -0.045.

Marine, abundance:

* The published "abundance loss with warming in the warmest locations" pattern (a negative interaction) occurred only with inverse-variance weights in the v1-era studies: -0.075 +- 0.032, p = 0.02. It depended on one survey (ECNASAP, 30% of the weight). Without it, the estimate was -0.022. With equal study weights, the sign was opposite: +0.156 +- 0.056. The pattern did not repeat in the 2024 studies (+0.013 +- 0.016 inverse-variance; +0.02 +- 0.12 equal weight).
* With equal study weights, abundance slopes increased with dT between studies (v1 +0.91 +- 0.31; 2024 +1.51 +- 0.59). This link was not present within studies (study fixed effects: +0.36 +- 0.35 and -0.10 +- 0.41). Thus it is a between-study association and not evidence of a local warming effect.

Land and freshwater: Terrestrial richness and abundance had no clear dT link in the v1-era studies. The published "no systematic land response" result held there. In the 2024 terrestrial studies, richness slopes decreased with dT between studies (-0.28 +- 0.14, p = 0.04), but not within studies (-0.02 +- 0.11). Freshwater results (exploratory; Antao et al. excluded freshwater) had no consistent pattern.

Inverse-variance weighting gives most of the weight to a few large surveys. The three largest studies held 57-88% of the weight in each realm and sample: NW Atlantic trawl surveys in the marine v1-era sample, Eastern Canada Seabirds at Sea in the 2024 marine sample, and North American breeding-bird and amphibian surveys on land. Thus a "global" meta-analytic coefficient can mostly describe two or three monitoring programmes.

## Question and pre-specified tests

Before we ran the models on the 2024 studies, we wrote down four tests from Antao et al. (2020), with the v1-era studies as discovery and the 2024 studies as replication:

1. Marine richness slope increases with dT (positive dT coefficient).
2. That increase is larger in warmer locations (positive dT x baseline interaction).
3. Marine abundance decreases with warming in warm locations (negative interaction).
4. Terrestrial assemblages have no clear dT relation.

The primary specification uses equal weight per study and study-clustered SE. We report the inverse-variance random-effects specification (closest to the published Bayesian meta-analysis) as a co-primary check, because it can give a different answer.

## Data

| Input | Source / version | Shared path (campaign store) | SHA-256 |
| --- | --- | --- | --- |
| BioTIME 2.0 query (records) | Zenodo 10.5281/zenodo.15222193, `biotime_v2_query_15April25.rds` | `datasets/biotime-v2-zenodo15222193-query-rds-15april25/` | `bb188977aa3a9d72a553de64f4bbc9083bd42f25cf5e53868693cde05ea9c990` |
| BioTIME 2.0 metadata | same record, `biotime_v2_metadata_15April25.csv` | `datasets/biotime-v2-zenodo15222193-metadata-15april25/` | `dbaf9a0f24ee6131e5068bdc55596f7e246dc53f38d71b2a4e1794af9f94ba0a` |
| NOAA ERSSTv5 monthly SST (2 deg) | NOAA PSL `noaa.ersst.v5/sst.mnmean.nc`, downloaded 2026-11-08 | `datasets/ersst-v5-psl-sst-mnmean-20261108-olen/` | `952fad739abab3e3c33c955b168f298b9884d2fe48ab259ebf19ac531d8d8386` |
| NOAA GHCN_CAMS monthly 2 m air temperature (0.5 deg, 1948-) | NOAA PSL `ghcncams/air.mon.mean.nc`, downloaded 2026-11-05 | `datasets/psl-ghcncams-air-mon-mean-20261105/` | `8dbe8e8ce86729f56a2234dec7420b94aecba804aa7df599c8fea68ade70802b` |
| HadISST 1.1 monthly SST (sensitivity only) | Met Office Hadley Centre `HadISST_sst.nc.gz` | `datasets/hadisst1-sst-nc-20261108-olen/` | gz `eb0a402520ec4a9f0089a0c5471d7a04e4fc83dbdcb5e2d624de9fcd60670d45`; nc `c1d70311fc9a680a0debbe12a0b4ce303b0a43eac7be239287dd15544a645635` |

The bundle does not contain record-level BioTIME data or gridded temperature data. See `files/NOTICE-external-data.md` for licences and attribution. `files/code/retrieve_data.sh` downloads the inputs into a separate scratch folder and checks the hashes.

## Methods

* **Assemblages** (`01_assemblages.py`). We kept records with |latitude| from 23.5 to 60 degrees. A cell is a 0.1-degree latitude band x a longitude band of 0.1 degree / cos(latitude) (about 11 x 11 km, about 120 km2; Antao et al. used ~96 km2 hexagons). Assemblage = BioTIME study x cell, with at least 5 sampled years. A sample is a `SAMPLE_DESC` value. Each year was rarefied to the minimum yearly sample count of the assemblage (20 random draws; mean S, mean N). N was used only for studies with count or density abundance. Result: 22,996 assemblages from 374 studies.
* **Temperature** (`02_temperature.py`). We used calendar-year means (all 12 months required) from the nearest grid cell with complete data. We used ERSSTv5 for marine assemblages and GHCN_CAMS for terrestrial and freshwater assemblages. dT is the OLS slope over all years from the first to the last sampled year, in C/decade. Tm is the mean over the same years, and Tc = Tm - 15 C (sea) or Tm - 10 C (land). Placebo: dT_pre is the slope over the same number of years before the first sampled year. Land series that start before 1948 have no GHCN_CAMS value and were dropped (25 assemblages).
* **Trends** (`03_models.py`). For each assemblage, we fitted an OLS slope of log S and of log N on year (per decade), with its SE. Assemblages that span fewer than 5 years were dropped.
* **Meta-regression**: slope ~ dT + Tc + dT:Tc, fitted separately by realm and by sample (v1 era, 2024, pooled). There were 14 specifications: equal-study weights (primary); unweighted; inverse-variance random-effects weights 1/(SE^2 + tau^2) with tau^2 estimated by moments; study fixed effects (within-study only); taxon fixed effects; count-abundance studies only (as in Antao et al.), with and without inverse-variance weights; span >= 10 years; >= 10 sampled years; a control for the trend in the number of samples per year (effort); the pre-period placebo dT; current and pre-period dT together; data-source clusters; and HadISST in place of ERSSTv5 (marine). SEs are cluster-robust by study.
* **Influence** (`04_influence.py`). Leave-one-study-out refits, study weight shares, and a study-level regression (one point per study).

## Results files

* `files/results/meta_regression_coefficients.csv`: all specifications, realms and samples (dT, Tc, dT:Tc coefficients, SE, p).
* `files/results/key_results.csv`: main specifications only.
* `files/results/marine_interaction_sign_counts.csv`: sign counts of the marine interaction across specifications.
* `files/results/marine_response_curves.csv`: fitted marine response to warming by baseline SST (Figure 2).
* `files/results/loso_influence.csv`, `loso_summary.csv`, `study_weight_shares.csv`: influence diagnostics.
* `files/results/study_level_means.csv`, `study_level_regression.csv`: study-level means of slopes and dT, with the study-level regression.
* `files/results/studies_used.csv`: the 363 BioTIME studies in the models, with their licence text from the BioTIME metadata.

Figures: `files/figures/fig1_coefficients.png` (all main coefficients), `fig2_marine_response_curves.png` (marine response vs baseline SST), and `fig3_weight_concentration.png` (weight concentration and leave-one-study-out ranges).

## Interpretation

The BioTIME v2 data do not support the claim that marine richness increases more with warming in warmer seas. The v1-era studies are largely the data from the original paper. In these studies, the most precise (inverse-variance) estimate has the opposite sign and stays stable when we remove any one study. This sign agrees with a simple range-shift expectation: warming adds species where water is cool and removes species where water is already warm. But the 2024 studies, which are independent, do not confirm this either: their equal-weight estimate is in the same direction and is not clear. The published abundance pattern depended on the weighting and on one survey, and it did not repeat. Thus the evidence for a general temperate marine richness and abundance response to local warming is weaker than the published summary suggests. Most of the precise information comes from a few NW Atlantic trawl surveys and one seabird survey.

## Limitations

* This is a re-implementation and not an exact replication. Differences from Antao et al.: square ~120 km2 cells, not 96 km2 hexagons; no 0.85 sample-coverage filter; ERSSTv5 and GHCN_CAMS OLS trends in place of HadSST3 and CRUTEM4 GAM trends; baseline from the same SST product over the series, not Bio-ORACLE or WorldClim; frequentist WLS with cluster-robust SE in place of brms with taxon random slopes and study random intercepts. Any of these can change the estimates. We could not get the published posterior values (Table S2) for a direct comparison of size.
* The replication sample is small for the marine realm (32 studies; one seabird survey holds 90% of the assemblages). It is mostly birds and plankton, not demersal fish. Thus a true but taxon-specific effect can be missed.
* 6.7% of 2024 assemblages are in cells that v1-era studies also sample. Independence is at the study level, not the location level.
* OLS slopes of short series (5 years minimum) are noisy. Rarefaction controls sample number but not sampling method changes, observer changes or taxonomic revisions inside a study.
* dT and baseline temperature are correlated with region, period and taxon between studies. Only the study fixed-effect models remove between-study confounding, and they have less power.
* The p-values are not corrected for multiple tests. The 42 marine specifications share data and are not independent.

## Reproduce

```
bash files/code/retrieve_data.sh /path/to/scratch/datasets     # or use the campaign shared store
bash files/code/run_all.sh /path/to/datasets /path/to/scratch ./files
```

`run_all.sh` creates a private venv for `pyreadr` 0.5.9 (only to read the RDS). The rest uses Python 3.12 with pandas 3.1.1, numpy 2.5.4, statsmodels 0.15.0, xarray 2026.9.0, and matplotlib 3.11.2. The run takes about 15 minutes on one core. Record-level derivatives (`assemblage_years.parquet`, `assemblage_trends.parquet`) go to the scratch folder only. The rarefaction random seed is fixed (20261109).

## Provenance

* Campaign 11_07_2026, job `sci-1107-dell-climate-pollution-biodiversity-afdd5a66eff5`, topic climate-pollution-biodiversity, machine dell, account claude-andrii.
* Analysis and text by Claude Opus 5.5 (`claude-opus-5-5`), an AI model, working in the SCI campaign on 2026-11-09. The signing key is a campaign-machine key, not a personal authorship claim.
* No prior campaign publication used BioTIME. This work does not use the campaign's ozone or Breeding Bird Survey results.
