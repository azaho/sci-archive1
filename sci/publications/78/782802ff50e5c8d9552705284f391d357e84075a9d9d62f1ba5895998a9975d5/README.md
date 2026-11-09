# Bumble bee losses and thermal exposure: a sampling-effort and placebo re-test of Soroye et al. (2020), with a new 2000-2014 to 2015-2024 interval

## Summary

Soroye, Newbold and Kerr (2020, *Science* 367:685) reported that local extirpation of 66 bumble bee (*Bombus*) species in 100-km cells of North America and Europe increased with the change in a thermal exceedance index (TEI) between 1901-1974 and 2000-2014. We repeated their model with their records and exposure rasters. Then we did three tests:

1. **Sampling effort.** We removed or controlled cells where the later period had few or no records.
2. **Species-limit placebo.** We randomly exchanged the thermal limits of species within each continent. This keeps cell warming, records and effort unchanged.
3. **New interval.** We used GBIF records and CRU TS 4.09 temperature for 2000-2014 to 2015-2024. These data are independent of the original model fit.

Main results:

- **We reproduced the published model.** The TEI-change coefficient was +0.26 log-odds per SD (cell-clustered SE 0.08). Its interaction with baseline TEI was +0.47 (SE 0.12).
- **Many original losses are only missing records.** Of the 6,936 loss events in the original table, 2,999 (43%) are in cells with no *Bombus* record in 2000-2014. This is 50% in North America and 31% in Europe. The original model counts all species that had records in 1901-1974 as lost from these cells.
- **The main TEI-change effect did not survive effort control in 1901-1974 to 2000-2014.** It was +0.03 ± 0.10 in cells with at least 10 location-years in both periods, and -0.03 ± 0.09 with equal-record subsampling. With GBIF records for the same periods, it was near zero in all six sample variants (-0.07 to +0.04).
- **The main effect in the original form is a cell-warming effect, not a species-limit effect.** With randomly exchanged species limits, the coefficient was +0.274 (2.5-97.5%: 0.256-0.292). The observed value was +0.288. The coefficient also changed from +0.29 to +0.15 when we used CRU TS 4.09 in place of CRU TS 3.24.01. The two versions give different 1901-1974 to 2000-2014 warming patterns (r = 0.76 across 0.5-degree land grid cells).
- **Between cells, the interaction of baseline TEI and TEI change is larger than the placebo in all three data sets.** This interaction means that warming increases losses more where a species is near the hot side of its range. In the new interval it was +0.40 ± 0.18 (at least 10 location-years in both periods; placebo mean +0.09, one-sided placebo p = 0.045) and +0.38 ± 0.16 (equal-record subsample, 10 draws; for draw 0, +0.37 against placebo +0.17, p = 0.015). With all cells it was small (+0.08 ± 0.12), but it was still above the placebo (-0.09, p = 0.02).
- **In the new interval, losses were higher in cells that warmed more, also on the cold side of species ranges.** With equal-record subsampling, the TEI-change coefficient was +0.51 ± 0.10. However, randomly exchanged limits gave +0.42 (0.38-0.45), against +0.50 for the same subsample draw. The slope per +0.01 TEI was positive on the cold side of ranges (+0.54 ± 0.16) as well as the hot side (+0.88 ± 0.16). A thermal-limit mechanism predicts a cold-side slope of zero or less. Thus most of this signal is a cell-level association with warming. It is not specific to the thermal limits of each species.
- **Within-cell tests gave weaker support.** With cell and species fixed effects (a linear probability model), all cell-level effort, observer and data-source differences are removed. In the authors' records, neither the TEI-change coefficient nor the interaction was above the placebo (interaction -0.001 ± 0.028 probability of loss per SD^2, placebo p = 0.42). In GBIF 1901-1974 to 2000-2014, both were above the placebo in cells with at least 10 location-years in both periods (change +0.17 ± 0.08, p < 0.01; interaction +0.095 ± 0.035, p = 0.01). In the new interval, only the interaction was above the placebo (all cells +0.056 ± 0.022, p = 0.02; at least 10 location-years +0.043 ± 0.023, p = 0.05). The TEI-change main effect was not above the placebo (+0.06 ± 0.05, p = 0.20). A conditional logit grouped by cell gave a TEI-change coefficient near zero in all data sets, and a positive but uncertain new-interval interaction (+0.39 ± 0.30 log-odds). In all three data sets, within the same cell, species with a higher baseline TEI were lost more often (placebo p ≤ 0.02). This stayed true after control for the local record count of the species.
- **Data composition did not explain the new-interval cell signal.** The shift to human-observation records (mostly community-science photographs) between 2000-2014 and 2015-2024 had no correlation with cell warming (r = -0.02). Adding this shift as a control did not change the TEI-change coefficient.

**Conclusion.** The published link between TEI *change* and bumble bee extirpation is not robust in 1901-1974 to 2000-2014. It depends on cells without later records, on the climate data version, and on the data source. A smaller, species-specific pattern repeats in all three data sets and in the new 2000-2024 interval: warming is more strongly linked to loss where a species is near the hot side of its range. However, the uncertainty is large, and the pattern is weaker within cells. These are presence-only records with changing observers. Thus all "losses" are non-detections, not confirmed extinctions.

## Data

| Source | Use | Version / retrieval | Licence |
|---|---|---|---|
| Soroye et al. 2020 data and code repository, figshare [10.6084/m9.figshare.9956471](https://doi.org/10.6084/m9.figshare.9956471) (`Bumblebee_repo.zip`, 1,131,332,971 bytes, SHA-256 `f6b51f83...4ac3`) | Bumble bee records 1901-2014 (66 species), R code, exposure-index rasters (TEI/PEI baseline and change, per species), CRU TS 3.24.01 grids | Downloaded 2026-11-09. Campaign path `datasets/soroye2020-bumblebee-repo-figshare9956471` | CC BY 4.0. The repository asks users to contact the original data providers for novel uses. We use the records only to repeat and test the published analysis, and we do not redistribute them. |
| CRU TS 4.09 monthly Tmax, 0.5 degree (Harris et al. 2020, doi:10.1038/s41597-020-0453-3) | New-period and alternative-version TEI | `cru_ts4.09.1901.2024.tmx.dat.nc.gz`, 187,840,417 bytes, SHA-256 `78df1a40cc0b522664a6874a014bc42982e6b9632194ddc249a62ce27b049e78`. Campaign path `datasets/cru-ts-4.09-tmx-1901-2024` | Open Government Licence v3 (CRU/NCAS). We redistribute no grids. |
| GBIF occurrence density map API (`https://api.gbif.org/v2/map/occurrence/density/1/{x}/0.mvt`, EPSG:4326, 8-px squares = 0.1758 degree) | Bombus records per species, cell and period (1901-1974, 2000-2014, 2015-2024, 2015-2025); genus effort per year; genus records by basisOfRecord | Retrieved 2026-11-09. The SHA-256 of each tile file is in `files/provenance/gbif_tile_files_sha256.json` | Records come from many publishers under CC0, CC BY and CC BY-NC. The bundle has no record-level or cell-level GBIF tables, only model coefficients and continent totals. |
| GBIF backbone taxonomy (species/match API) | Name-to-key matching for the 66 species and the synonyms that the original study merged | 2026-11-09, `files/data/gbif_species_keys.json` | GBIF backbone (CC BY 4.0) |

The bundle does not include third-party records, cell-level tables or climate grids. `files/code/run_all.sh` downloads them again into a separate scratch folder and repeats all steps.

## Methods

### Rebuild of the original table
`03_build_original.py` follows the original R scripts `1_Cleandata_and_makeMCPs.R`, `2_CalcSpeciesPr_Rich.R`, `3_CalcSamplingEffort_Cont.R` and `5_binomialGLMM4Presence.R`. It applies the same species list, synonym merges, erroneous-record exclusions, periods (1901-1974 = P0, 2000-2014 = P3) and 100-km cylindrical equal-area grid. Absence is inferred in every cell where any *Bombus* record exists in either period. This is the same as in the original. "Extirpation" = the species has records in the cell in the earlier period and no record in the later period. The original "sampling" covariate is the sum over both periods. It does not show a decrease in effort between the periods.

### Exposure indices
Script `calib_tei.py` and `06_climate.py` show that the original species TEI rasters are exactly an affine function of the 1901-1974 mean of the annual-mean monthly Tmax (CRU TS 3.24.01). For each species, R^2 = 1.000000, so TEI = k_s * Tmax + c_s. PEI is the same function of annual-mean monthly precipitation (R^2 = 1.0000000). We recovered k_s and c_s for each species by least squares. We applied them to CRU TS 4.09 period means: baseline TEI = k_s * T(2000-2014) + c_s, and TEI change = k_s * (T(2015-2024) - T(2000-2014)). The rebuilt CRU TS 3.24 TEI change agrees with the authors' change raster at r^2 = 0.99. We read the RDS rasters without R, with the `rdata` Python parser (`rds_raster.py`). The new-interval models use the temperature-only form, because the precipitation terms changed the TEI coefficients only a little in the original data (+0.26 vs +0.30; interaction +0.47 vs +0.45; `spec_checks.txt`).

### Models
- **Original form (between cells).** Logistic regression of extirpation on continent, the original sampling covariate, baseline TEI, its square, TEI change, and baseline x change, with species fixed effects. The original paper used species random effects with a phylogenetic covariance in MCMCglmm. We use species fixed effects and cell-clustered standard errors. The original model did not cluster by cell. Naive standard errors make the original TEI-change effect look much stronger (p = 6e-11 naive vs p = 0.001 clustered).
- **Effort variants.** (A) all cells; (B) cells with at least one later record; (E5, E10, E20) cells with at least 5, 10 or 20 location-years in both periods, plus log(later/earlier location-years). For the authors' records, a location-year is a distinct LYID. For GBIF, it is a distinct 0.1758-degree square x year with a *Bombus* record. (R) Equal-record subsampling: in each cell with at least 20 records in both periods, we drew the same number of records from each period without replacement (multivariate hypergeometric over species counts). We repeated this 10 times and pooled the results with Rubin's rules.
- **Species-limit placebo.** We exchanged (k_s, c_s) at random among species of the same continent. Then we recomputed TEI and refitted the model, 200 times per variant. A coefficient that comes from cell warming or cell temperature (not from species limits) stays the same under this placebo.
- **Within-cell design.** We used a linear probability model with cell and species fixed effects and cell-clustered SE. TEI change is then identified only by k_s x cell warming, and baseline TEI only by differences among species in the same cell. The placebo was the same as above (100 draws). As a check, we fitted a conditional logit grouped by cell. We also did a local-rarity check: we added the log of the earlier-period record count of the species in the cell.
- **Composition check.** We calculated the change in the share of human-observation records per cell from GBIF basisOfRecord tiles. We correlated it with cell warming and added it as a control.

Effect units: "per SD" = per standard deviation of the index across all species x study cells of that data set. "Per +0.01 TEI" is a raw index unit. For a typical species, k_s is about 0.016 per degree C, so +0.01 TEI is about +0.6 degree C of mean Tmax.

## Results tables (files/results)

Original-form (between-cell) logistic models, temperature-only form, species fixed effects, cell-clustered SE. Coefficients are log-odds per SD of the index (`between_summary.csv`). The placebo is the 200-draw species-limit permutation (`perm_between.csv`). For the "equal records" variant, the placebo uses draw 0 of the subsampling.

| Data set | Sample | n (cells) | Loss rate | TEI change | Placebo mean (2.5-97.5%) | Baseline x change | Placebo mean (2.5-97.5%) |
|---|---|---|---|---|---|---|---|
| Authors 1901-74 to 2000-14 | all cells | 11,583 (1,642) | 0.60 | +0.29 ± 0.08 | +0.27 (0.26, 0.29) | +0.43 ± 0.11 | +0.29 (0.22, 0.37) |
| | >=10 loc-yr both | 3,985 (266) | 0.26 | +0.03 ± 0.10 | +0.02 (-0.01, 0.04) | +0.48 ± 0.19 | +0.16 (0.00, 0.31) |
| | equal records | 4,636 (394) | 0.31 | -0.03 ± 0.09 | -0.04 (-0.07, -0.02) | +0.27 ± 0.17 | -0.04 (-0.23, 0.16) |
| GBIF 1901-74 to 2000-14 | all cells | 11,272 (1,678) | 0.48 | -0.00 ± 0.06 | +0.02 (-0.00, 0.04) | +0.37 ± 0.09 | +0.09 (0.02, 0.18) |
| | >=10 loc-yr both | 5,453 (404) | 0.28 | -0.02 ± 0.08 | -0.04 (-0.07, -0.01) | +0.52 ± 0.12 | +0.24 (0.10, 0.36) |
| | equal records | 5,860 (559) | 0.35 | -0.05 ± 0.09 | -0.04 (-0.07, -0.01) | +0.73 ± 0.13 | +0.39 (0.26, 0.51) |
| GBIF 2000-14 to 2015-24 (new) | all cells | 9,790 (1,567) | 0.13 | +0.18 ± 0.08 | +0.08 (0.02, 0.12) | +0.08 ± 0.12 | -0.09 (-0.27, 0.06) |
| | >=10 loc-yr both | 6,459 (554) | 0.08 | +0.29 ± 0.15 | +0.17 (0.11, 0.22) | +0.40 ± 0.18 | +0.09 (-0.21, 0.41) |
| | equal records | 7,171 (724) | 0.20 | +0.51 ± 0.10 | +0.42 (0.38, 0.45) | +0.38 ± 0.16 | +0.17 (-0.03, 0.33) |

Other files:
- `between_summary.csv`: all six sample variants, with the slopes per +0.01 TEI on the cold side (25th percentile) and hot side (75th percentile).
- `perm_between.csv`, `within_lpm_obs.csv`, `within_lpm_perm.csv`, `within_lpm_rarity_obs.csv`: placebo draws and within-cell fits.
- `orig_models_fullform.csv`, `spec_checks.txt/.csv`: the full original form (with PEI), and the effects of the CRU version and the rebuilt indices.
- `gbif_T_models.csv`, `gbif_T_*_rarefied_pooled.csv`: the first GBIF runs (the same models; the pooled subsampling uses the full original form without PEI).
- `composition_P3P4.txt/.csv`: the data-composition check.
- `describe.csv`: sample sizes, record totals and the share of losses in unsampled cells, by continent.
- `within_conditional_logit.csv`: conditional logit (cell-grouped) check.

## Figures

- `files/figures/fig1_effort_artifact.png`: (a) share of loss events in cells with no later record; (b) the original-form TEI-change coefficient under the effort variants, for the three data sets.
- `files/figures/fig2_interaction_placebo.png`: the baseline TEI x TEI change interaction compared with the species-limit placebo band (gray, 2.5-97.5%), (a) between cells and (b) within cells.
- `files/figures/fig3_cold_hot_slopes.png`: the loss slope per +0.01 TEI change on the cold side (25th percentile of baseline TEI) and the hot side (75th percentile) of ranges.

## Limitations

- All "extirpations" are non-detections in presence-only records. Equal-record subsampling and effort thresholds reduce detection bias, but they cannot remove it. Effort restriction also keeps mostly well-studied cells (western Europe, eastern North America).
- GBIF 2015-2024 records are mostly community-science photographs. Identification of cryptic species (for example *B. terrestris*/*lucorum*, *B. cryptarum*) is uncertain. Name matching follows the GBIF backbone. Records of synonyms that GBIF accepts as separate species were added to the merged species, as in the original study.
- The new interval is short (about 12.5 years between period midpoints, against about 70 years originally). The TEI changes are smaller, so the power is lower.
- The GBIF 1901-1974 and 2000-2014 records partly overlap the authors' database. Thus the GBIF test of the original interval is not fully independent. The 2015-2024 records are new.
- We used species fixed effects, not the original phylogenetic random effects. We used temperature-only models for the new interval. The shared CRU TS 4.09 precipitation file in the campaign data store is truncated (see below), so the new-interval PEI terms were not tested.
- The placebo p-values compare the observed coefficient with the placebo distribution only. They do not include the sampling uncertainty of the observed coefficient (its SE is given separately).
- Many sample variants were tested. We report all of them and do not select one.

## Reproduction

1. `bash files/code/run_all.sh /path/to/scratch` downloads the sources again (the Soroye repository, CRU TS 4.09 Tmax and the GBIF tiles). Then it runs scripts 01-18 in order. It writes only in the scratch folder. The scripts need Python 3.12 with numpy, pandas, pyarrow, scipy, statsmodels, xarray, netCDF4, pyproj, requests, mapbox-vector-tile, rdata and matplotlib. Set OMP_NUM_THREADS=1.
2. GBIF content changes over time. New retrievals will give slightly different counts. The tile hashes of our retrieval are in `files/provenance/`.
3. Equal-record subsampling and the placebos use fixed random seeds.

## Campaign data-store note

The shared dataset `cru-ts-4.09-pre-1901-2024` (SHA-256 `1fd0601d...013d`) has 248,093,335 bytes, but the source file has 692,801,358 bytes. It fails `gzip -t`, although the dataset helper reported "created". We did not use or change it. An operator should examine it.

## Provenance

- Job `sci-1107-dell-climate-pollution-biodiversity-d87909267258`, campaign 11_07_2026, topic climate-pollution-biodiversity, machine dell, account claude-andrii. Model: Claude Opus 5.5 (`claude-opus-5-5`). The signing key is a campaign-machine key. It is not a personal authorship claim.
- `files/provenance/soroye_repo_members_used_sha256.json`: SHA-256 of each member of the repository archive that we used.
- `files/provenance/gbif_tile_files_sha256.json`: SHA-256 of each decoded GBIF tile file (JSON, gzip) of our retrieval.

## Licence and attribution

The LICENSE file applies to our own text, figures, aggregate result tables and code. The third-party sources above keep their own licences (see `files/NOTICE_external_data.md`). We did not include their records or grids in this bundle.
