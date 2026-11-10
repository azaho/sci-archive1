# Night light did not delay autumn leaf colour in US phenology records (2009-2025); earlier spring leaf-out at bright sites followed regional light, not local light

## Summary

Meng et al. (2022, PNAS Nexus) used USA National Phenology Network (USA-NPN) records from 2011-2016. They reported that artificial light at night (ALAN) made "breaking leaf buds" 8.9 days earlier and "colored leaves" 6.0 days later at bright sites. Their model controlled for gridded temperature, species and year. It did not control for location within the country, built-up land, the observer, or the time between visits.

We tested these claims again with the same USA-NPN programme. We used up to 61,490 spring and 55,383 autumn onset records of deciduous broadleaf plants at 9,543 sites in the conterminous US, 2009-2025. We used two independent periods (2011-2016, the period of Meng et al.; and 2017-2025, which is after their data) and two regions (East and West of 100 W). We added the controls above in steps.

Main results:

1. **Autumn.** The Meng model gave a delay of colored leaves at bright sites in both periods (+1.7 and +1.9 days per 1 ln unit of light). Control for built-up land removed the delay (2009-2025: -0.01 days, SE 0.74). With all controls, colored leaves came earlier at bright sites (-2.0 days, SE 0.8). Local light (the site pixel minus the 9 km mean) had no relation to colouring (+0.2 days, SE 0.8). We found no support for a light-driven autumn delay.
2. **Spring.** Bright sites had earlier leaf buds in the East in both periods. All controls together reduced the slope by about two thirds (East 2009-2025: from -2.2 to -0.74 days per ln unit, SE 0.30). In the West, the sign was opposite (later at bright sites; +3.6 days, SE 1.3). In the East, light averaged over about 9 km predicted the spring advance (-0.93, SE 0.40). Local light above that regional mean did not (-0.36, SE 0.26). American beech, the genus that is most sensitive to day length, had no spring light slope (-0.4, SE 0.6).
3. **Meng's headline contrast.** With the method of Meng et al. (top-quartile light sites against other sites in 1 C temperature bins), the raw spring difference in 2011-2016 was -1.5 days (95% site bootstrap -4.3 to +1.5), not -8.9 days. The raw autumn difference was +8.5 days (0.6 to 15.1), near the published +6.0 days. But after we removed species-by-year and 2-degree cell means, the autumn difference was +1.1 days (-5.7 to +7.2), and in 2017-2025 it was -0.5 days (-4.2 to +3.8).
4. **Observation and confounding.** The brightest fifth of sites had about 0.22 built-up fraction (dark sites 0.002) and about 41-47 observers per site (other quintiles 12-21). Gridded Daymet temperature increased by 0.38 C per ln unit of light within the same 2-degree cell and year, so the gridded data includes part of the urban warmth signal, but probably not all of it. The remaining eastern spring slope (-0.74 days per ln unit) is the size of a 0.2 C warming at the observed temperature sensitivity (-3.4 days per C).

Interpretation: the evidence agrees with a city-scale climate (urban heat) or urban planting effect on spring leaf-out in the East. It does not support a direct light effect on the plants at km scale. The data cannot resolve street-lamp-scale exposure of individual trees.

## Question

Does brighter night light make leaf-out earlier and leaf colouring later in US deciduous plants after control for location, built-up land, observer and visit timing? Is the published relation repeated in an independent later period and in two regions?

## Data

- **USA-NPN individual phenometrics** (Nature's Notebook and integrated data sets), API `getSummarizedData`, downloaded 2026-11-09 for 2009-2025. Phenophases 371 and 373 ("Breaking leaf buds") and 498 ("Colored leaves"). The API adds Daymet seasonal climate fields for each site and year. Licence: CC BY 4.0. Exact request URLs are in `files/code/01_get_npn.sh`. The SHA-256 of each of the 51 downloaded JSON files is in `files/provenance/npn_download_sha256.tsv`. The USA-NPN database changes when observers add or edit records, so a later download can give slightly different files.
- **Harmonized night-time light** (Li, Zhou, Zhao and Zhao 2020, Scientific Data; figshare 9828827 v10), annual 30 arc-second DN (0-63). 2009-2013 are calibrated DMSP; 2014-2024 are VIIRS data converted to the DMSP scale ("simVIIRS"). Licence CC BY 4.0. Shared campaign copies with SHA-256 are listed in `files/provenance/shared_datasets_used.json`. Records from 2025 use the 2024 light value.
- **GHSL built-up surface** GHS-BUILT-S R2023A, epochs 2010 and 2020, 30 arc-second, WGS84 (European Commission JRC). Licence CC BY 4.0. Shared copies: `ghsl-built-s-e2010-r2023a-4326-30ss-v1` (SHA-256 0124f198...) and `ghsl-built-s-e2020-r2023a-4326-30ss-v1` (SHA-256 3dda6099...); full hashes in `files/provenance/shared_datasets_used.json`. We convert built-up area to a fraction of the cell area. We use epoch 2010 for 2009-2015 and epoch 2020 for 2016-2025.

## Methods

Records (`files/code/02_build_records.py`): we kept deciduous broadleaf plants in the conterminous US. For spring we used onset day of year (DOY) of "Breaking leaf buds" at DOY 183 or earlier. For autumn we used "Colored leaves" at DOY 182 or later (the same cut-offs as Meng et al.). For each plant, year and season we kept the first onset. "Bracket" is the number of days since the last "no" record before the first "yes". As in Meng et al., we kept species with at least 80 (spring) or 40 (autumn) records.

Light and built-up land (`03_site_covariates.py`): at each site we read light at the pixel (about 0.9 km), as a 3 x 3 pixel mean (about 2.5 km, the main measure), and as an 11 x 11 pixel mean (about 9 km). The light variable is L = ln(1 + DN). We read built-up fraction at the pixel and as a 5 x 5 mean.

Models (`04_models.py`): linear fixed-effects regressions (pyfixest 0.70.0) of onset DOY on temperature T (Daymet spring mean for leaf buds; summer mean for colored leaves, as in Meng et al.), L, and T x L. Standard errors are clustered by site. The specifications add controls in steps:

- A: species and year effects (the Meng model, with fixed effects in place of random intercepts).
- B: species-by-year and 2 x 2 degree cell effects (location).
- C: B plus built-up fraction (pixel and 5 x 5).
- D: C plus observer effects.
- E: D with records that have a "no" record 7 days or less before the first "yes" (also with the bracket midpoint as the outcome).
- F: E with species-by-cell effects in place of cell effects.

Each model was fitted for 2011-2016, 2017-2025 and 2009-2025, for all sites, East (longitude > -100) and West.

Other tests:

- `05_meng_bins.py`: the Meng top-quartile contrast in 1 C bins on site-species-year means, raw and after removal of species-by-year and cell means, with a 300-replicate site bootstrap.
- `06_diagnostics.py`: observation process by light quintile; bracket length and Daymet temperature against light; light radius (pixel, 2.5 km, 9 km); a within-plant test (plant and species-by-year effects, 2014-2025 simVIIRS years only); species slopes in the East.
- `07_local_vs_regional.py`: one model with local excess light (pixel minus 9 km mean) and regional light (9 km mean), with all F controls.

## Results

### Coefficients of light (days per 1 ln unit of light; site-clustered SE)

| Season | Period | Region | A: Meng model | C: + location, built-up | F: all controls |
|---|---|---|---|---|---|
| Leaf buds | 2011-2016 | all | -0.48 (0.28) | -0.18 (0.43) | -0.45 (0.70) |
| Leaf buds | 2011-2016 | East | -0.86 (0.23) | -0.67 (0.41) | -1.33 (0.67) |
| Leaf buds | 2017-2025 | all | -2.19 (0.34) | -1.87 (0.34) | -0.52 (0.35) |
| Leaf buds | 2017-2025 | East | -2.76 (0.36) | -2.36 (0.35) | -0.76 (0.35) |
| Leaf buds | 2009-2025 | West | +0.29 (0.50) | +1.50 (0.75) | +3.58 (1.26) |
| Colored leaves | 2011-2016 | all | +1.66 (0.63) | +1.51 (0.86) | +0.96 (1.27) |
| Colored leaves | 2017-2025 | all | +1.95 (0.68) | -0.87 (0.90) | -2.30 (0.92) |
| Colored leaves | 2009-2025 | all | +1.99 (0.60) | -0.01 (0.74) | -2.05 (0.81) |
| Colored leaves | 2009-2025 | West | +5.28 (0.89) | +2.47 (1.13) | -4.50 (2.84) |

The full table (144 fits) is `files/results/model_table.csv`. Figure 1 shows all steps. For comparison, Meng et al. reported -1.43 (leaf buds) and +2.60 (colored leaves) days per ln unit of VIIRS radiance. The light units are different (DN against radiance), so only signs and relative changes can be compared directly.

### Local and regional light (2009-2025, all controls, 7-day bracket)

| Season | Region | Local excess | Regional (9 km) |
|---|---|---|---|
| Leaf buds | all | -0.09 (0.28) | -0.73 (0.40) |
| Leaf buds | East | -0.36 (0.26) | -0.93 (0.40) |
| Leaf buds | West | +3.18 (1.32) | +2.72 (1.70) |
| Colored leaves | all | +0.18 (0.80) | -2.71 (1.20) |
| Colored leaves | East | +0.34 (0.83) | -2.29 (1.24) |

A direct effect of light on the plant predicts a larger slope for local light than for regional light. We found the opposite for leaf buds in the East. The within-plant test (light change at the same plant in 2014-2025) gave +0.35 (0.60) for leaf buds and -0.54 (1.25) for colored leaves. The within-site light change is small (SD 0.29 ln units), so this test has low power.

### Species (East, leaf buds, 2009-2025)

All 15 species had a negative point estimate, and 5 had a 95% interval below zero. Red maple had -3.4 (0.6), flowering dogwood -2.8 (0.9), and quaking aspen -8.1 (2.9). American beech had -0.4 (0.6), common lilac -0.4 (0.9), and eastern redbud -0.4 (0.9) (`files/results/species_slopes_east.csv`; Figure 2). If light acts through day length, beech is expected to have one of the strongest responses. It did not.

### Observation process

`files/results/observation_by_light_quintile.csv` and `files/figures/fig4_observation_by_light.png` show that the brightest quintile has much more built-up land and many more observers per site (large multi-observer sites such as campuses and arboreta). The share of records from partner groups is lowest in the fourth quintile. The bracket length did not change clearly with light (leaf buds +0.21 days per ln unit, SE 0.15). The observer effects and the species-by-cell effects were the steps that most reduced the 2017-2025 spring slope (Figure 1).

## Limitations

- **Light measure.** We did not use the NASA Black Marble radiance product of Meng et al. (it needs a login). The harmonized DN saturates at 63; 21% of records are at DN 62 or more. Thus we cannot separate the brightest urban sites from each other, and slopes are not in the same units as Meng et al.
- **Spatial scale.** A 30 arc-second pixel (about 0.9 km) is the smallest scale. A street lamp near one tree is not visible in these data. Our "local" light is km-scale.
- **Urban heat.** We had no direct urban-heat measurement (for example MODIS land surface temperature). Built-up fraction and Daymet temperature are only proxies. Thus the remaining eastern spring slope can be urban heat, urban planting or site type, or light; our tests (regional against local light, beech) favour the non-light explanations but do not prove them.
- **Observers.** USA-NPN is a volunteer programme. Observer effects remove differences between observers, but bright and dark sites can also differ in the type of plant (planted, irrigated, cultivars).
- **West.** The West has fewer records (about 16%), and the positive spring slope there is not explained.
- **Multiple tests.** We report many specifications. We based the conclusions on the pattern across periods, regions and controls, not on single p-values.

## Reproduction

Use a scratch directory outside the publication folder:

```
bash files/code/run_all.sh <path-to>/files/code /mnt/dell-data/shared_datasets
```

The script downloads the USA-NPN records (51 API requests), builds the records, extracts covariates from the shared light and GHSL copies (or from the source URLs in `files/provenance/shared_datasets_used.json`), fits all models, and makes the figures. It needs Python 3.12 with numpy, pandas, scipy, rasterio, pyarrow, matplotlib and pyfixest 0.70.0. The record-level tables are not in this bundle because they contain third-party record-level data with observer identifiers. Their SHA-256 values from our run are: `records.parquet` cdc38a1e..., `site_covariates.parquet` f12277f1..., `analysis_records.parquet` b0241273... (full values in `files/provenance/derived_tables_sha256.txt`).

## Provenance and attribution

- Job: sci-1107-dell-climate-pollution-biodiversity-05c2b96ad7ba; campaign 11_07_2026; topic climate-pollution-biodiversity; machine dell; model Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key, not a personal authorship claim.
- Data were provided by the USA National Phenology Network and the many participants who contribute to its Nature's Notebook program. USA National Phenology Network. 2026. Plant and Animal Phenology Data. Data type: Individual Phenometrics. 01/01/2009-12/31/2025 for Region: conterminous US. USA-NPN, Tucson, Arizona, USA. Data set accessed 2026-11-09 at http://doi.org/10.5066/F78S4N1V.
- See `files/NOTICE-external-data.md` for all external data terms.
- Related campaign work: a night-light test of North American bird counts (sci:sha256:52e8e53c...) and a smoke bias test of PhenoCam greenness (sci:sha256:b0549936...).
