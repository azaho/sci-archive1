# Australian zooplankton thermal composition followed 35-57% of its spatial temperature slope year to year and 37-93% over 3-year blocks in two IMOS surveys, 2007-2025; the decadal ratio is unresolved

**Job:** sci-1107-dell-climate-pollution-biodiversity-c33b28713b4b · **Topic:** climate-pollution-biodiversity · **Campaign:** 11_07_2026 · **Machine:** dell · **Account:** claude-myxtap · **Model:** Claude Opus 5.5 (claude-opus-5-5), as an autonomous research agent. The signing key is a campaign-machine key. It is not a claim of personal authorship.

## 1. Question

Campaign work found that the community temperature index (CTI) of land and freshwater networks follows only a small part of its own spatial temperature slope in time: about 0.02 for year-to-year change and 0.12 for slow change (75 networks, sci:sha256:0037934e...). Marine plankton on the US Northeast Shelf was the main counter-case: 5-year ratios of 0.78 (zooplankton) and 0.55 (larval fish) (sci:sha256:dd5e171c...). External thermal indices from OBIS made this transfer larger, not smaller (sci:sha256:bec363cb...). California fish larvae gave a short-term ratio near 0.5 (sci:sha256:7069d14a...). All these marine results come from the Northern Hemisphere, and the Northeast Shelf result comes from one survey on one shelf.

We asked: **does near-full space-for-time transfer of plankton thermal composition also occur in independent Southern Hemisphere surveys with different gear and design?** We used two IMOS programmes around Australia:

* the Australian Continuous Plankton Recorder survey (AusCPR, ship-of-opportunity routes, about 7 m depth, 270 um silk), and
* the National Reference Stations (NRS, fixed coastal stations, vertical drop nets, about monthly).

The NRS design removes the route-change bias of the CPR survey: the same stations are sampled every year.

We wrote the plan (`files/PLAN.md`) before we calculated any CTI slope. It states two predictions:

* **H_marine** (transfer is general in plankton): year-to-year ratio of 0.3 or more, and 3-year or trend ratio of 0.5 or more.
* **H_weak** (weak transfer is general): ratios of 0.2 or less, as on land.

## 2. Data

| Source | Version and access | Use | License |
| --- | --- | --- | --- |
| IMOS AusCPR zooplankton abundance, copepods and non-copepods (AODN WFS layers `imos:cpr_zooplankton_abundance_copepods_data`, `imos:cpr_zooplankton_abundance_non_copepods_data`) | Downloaded 2026-11-12. 8,517 CPR segments, 2007-2026 (we used 2007-2025), 324 taxa. | Main survey | CC BY 4.0 |
| IMOS NRS zooplankton abundance (`imos:bgc_zooplankton_abundance_copepods_data`, `..._non_copepods_data`) | Downloaded 2026-11-12. 1,211 samples, 2002-2026. We used 10 stations (DAR, KAI, MAI, NSI, PHB, ROT, YON, ESP, NIN, PH4) and 2002-2025: 1,130 samples. | Second survey | CC BY 4.0 |
| NOAA OISST v2.1 monthly mean, 0.25 degree | PSL `sst.mon.mean.nc`, sha256 f30eaf68...61a, data to 2026-10 | SST at each sample, 1991-2020 monthly climatology | US Government, public domain |
| NOAA World Ocean Atlas 2023, decav annual surface temperature, 1 degree | `woa23_decav_t00_01.nc`, sha256 0bd98d3c...1b5 | External STIs | US Government, public domain |
| OBIS occurrence grid (geohash level 3) | `https://api.obis.org/v3/occurrence/grid/3?scientificname=<taxon>`, queried 2026-11-12 | External STIs (cells outside the survey box only) | Mixed per dataset (CC0, CC BY, CC BY-NC) |

The exact SHA-256 hashes of the IMOS files that we used are in `files/results/input_hashes_sha256.txt`. The IMOS files are also in the campaign dataset store as `imos-aodn-*-20261112`. The WFS output is a live service: a new download can contain more samples and has different feature IDs, so its hash can change.

OISST at the sample matched the satellite SST in the CPR file with r = 0.994, and the CTD surface temperature at NRS with r = 0.990.

## 3. Method

All code is in `files/code/`. Scripts take paths as arguments. `files/code/fetch_data.sh` gives the full order of steps.

1. **Parse** (`01_parse.py`). The WFS CSV has one row per sample and a JSON dictionary of taxon abundances (per m3). We kept positive abundances.
2. **SST** (`02_oisst_subset.py`, `03_build_samples.py`). Each sample received the OISST value of its month at the nearest ocean pixel, and the 1991-2020 climatology of that calendar month at that pixel.
3. **Species thermal index (STI)** (`tracklib.py`). For each taxon with 30 or more positive CPR samples (148 taxa) and each calendar quarter (DJF, MAM, JJA, SON), the STI is the log(1 + abundance)-weighted mean climatological SST at the samples where the taxon occurred. A taxon-quarter needs 5 or more positive samples.
4. **CTI** of a sample: the log(1 + abundance)-weighted mean STI of its scored taxa (2 or more scored taxa needed).
5. **Spatial slope b_space**: slope of the 1-degree cell mean CTI on the cell mean climatological SST, over cell-quarters with 10 or more samples, with quarter fixed effects.
6. **Temporal slopes**, all with 1-degree cell x quarter fixed effects and calendar-month fixed effects (weighted alternating projections):
   * *year-to-year*: slope on the region x quarter x year mean SST anomaly, detrended inside region x quarter;
   * *3-year*: slope of 3-year block means (2007-09, 2010-12, ...) of the residual CTI on the residual SST anomaly, region x quarter;
   * *trend*: CTI trend per decade / (b_space x SST trend per decade at the same samples);
   * *local*: slope on the sample SST anomaly inside region x quarter x year.
   The ratio is the temporal slope divided by b_space. A ratio of 1 means full space-for-time equivalence.
7. **Uncertainty**: joint bootstrap of 3-year blocks and 2-degree spatial blocks (300 replicates for the main run, 200 for the other runs). STIs are recalculated in each replicate. Intervals are 2.5-97.5 percentiles. For NRS, the bootstrap resamples 3-year blocks and stations; we also give a year-block-only interval.
8. **Null**: STI values permuted among taxa inside each quarter (200 permutations). This keeps the amount of turnover and removes its link to thermal position. For the pooled domain we added a stricter null that permutes STIs only inside the Southern Ocean taxon group or inside the northern taxon group (a taxon is in the Southern Ocean group if more than half of its records are in the Southern Ocean region).
9. **Variants** (`04_run_cpr.py`, `07_run_config.py`): presence weights; day/night fixed effect (CPR samples at 7 m are affected by diel migration); taxa-per-sample effort covariate; taxa with 100 or more positives; STIs from 2007-2015 only; copepods only; Southern Ocean only and north of the Southern Ocean only, each with region-internal STIs; 2012-2025 only (the first CPR years had fewer taxa per sample); external STIs.
10. **External STIs** (`06_obis_external_sti.py`): mean WOA23 annual surface temperature of the OBIS geohash-3 cells where the taxon occurs, **only outside** the survey box (latitude -67 to -8, longitude 88 to 176 E). This makes the STI independent of the survey samples. 137 of 148 taxa had 20 or more cells outside the box. External and internal STIs had r = 0.90.
11. **NRS** (`05_run_nrs.py`): life-stage labels were merged into species. CTI was calculated (a) with the CPR STIs (an index from a different programme; 128 matched species, 35% of NRS log-abundance) and (b) with NRS-internal STIs. The station is the cell and the region. b_space is the across-station slope (31 station-quarters).

## 4. Results

### 4.1 Main pre-specified test (CPR, all regions)

| Quantity | Estimate (95% CI) | Shuffle null p (one-sided) |
| --- | --- | --- |
| b_space (C CTI per C SST) | 0.835 (0.522-0.889) | |
| Year-to-year ratio | **0.35** (0.01-0.49) | 0.07 (slope) |
| 3-year ratio | **0.55** (0.13-0.81) | 0.04 (slope) |
| Trend ratio | 1.46 (-0.83-6.55) | 0.16 (CTI trend) |
| Local ratio | 0.42 (0.11-0.71) | |
| SST trend at samples (C per decade) | 0.26 (-0.02-0.48) | |

The point values meet the pre-stated H_marine criteria (0.35 >= 0.3 and 0.55 >= 0.5). They are far above the land and freshwater values (0.02 fast, 0.12 slow). But the year-to-year lower bound is near zero, and the trend ratio is not resolved because the SST trend over 2007-2025 at the sampled cells has an interval that includes zero.

The stricter zone null changes the interpretation of this pooled test. When STIs are permuted only inside the Southern Ocean and northern taxon groups, the null year-to-year slope is 0.26 (observed 0.29, p = 0.38) and the null CTI trend is 0.35 (observed 0.32). Only the 3-year slope stays above this null (p = 0.025). Thus, in the pooled domain, most of the year-to-year and trend signal is an exchange between the cold Southern Ocean group and the warm northern group (a movement of the subtropical front boundary). The fine thermal order of taxa inside each group adds little at this scale.

![Transfer ratios by timescale](files/figures/fig1_transfer_ratios.png)

### 4.2 Regional and design tests

| Analysis | b_space | Year-to-year ratio | 3-year ratio | Trend ratio | Null p (yy / 3-year slope) |
| --- | --- | --- | --- | --- | --- |
| CPR north of the Southern Ocean (region STIs; 4,349 samples, 120 taxa) | 0.371 (0.312-0.492) | **0.53** (-0.05-0.73) | **0.93** (0.22-1.37) | 2.87 (-5.1-9.6) | 0.020 / 0.005 |
| CPR Southern Ocean only (38 taxa) | 0.688 (0.176-0.746) | 0.19 (-0.92-2.13) | 0.88 (-1.97-4.02) | 1.51 (-10.1-7.6) | 0.34 / 0.23 |
| CPR 2012-2025 only | 0.546 (0.450-0.660) | 0.44 (-0.10-0.69) | 0.67 (0.03-1.01) | 0.97 (-15-7.4) | 0.020 / 0.015 |
| CPR all, external OBIS STIs | 0.872 (0.478-0.924) | 0.36 (-0.04-0.99) | 0.60 (0.25-1.67) | 3.18 (-3.6-21) | 0.37 / 0.10 (zone null) |
| CPR north, external OBIS STIs | 0.354 (0.319-0.441) | 0.37 (-0.45-1.20) | 0.83 (0.03-1.78) | 3.52 (-11-24) | 0.17 / 0.085 |
| NRS stations, CPR STIs | 0.306 (0.217-0.357) | **0.57** (0.05-1.19) | 0.51 (-0.36-1.34) | 1.49 (-11-26) | 0.005 / 0.12 |
| NRS stations, NRS STIs | 0.284 (0.138-0.478) | **0.37** (-0.15-0.61) | 0.37 (-0.26-0.72) | 0.87 (-10-7.7) | 0.005 / 0.015 |

NRS year-block-only intervals (stations fixed): year-to-year 0.27-0.84 (CPR STIs) and 0.12-0.50 (NRS STIs); 3-year 0.12-0.94 and 0.05-0.71.

Main findings:

* **North of the Southern Ocean**, the CPR CTI followed about half of its spatial slope from year to year (0.53) and most of it over 3-year blocks (0.93). Both slopes are above the within-zone shuffle null (p = 0.02 and 0.005). Here, the thermal order of taxa inside one zone carries the signal.
* **At the fixed NRS stations**, which have no route changes, the year-to-year ratio was 0.57 with CPR STIs and 0.37 with NRS STIs. Both slopes are above the shuffle null (p = 0.005). This is a second, independent design with a different net, depth and taxonomic resolution.
* **Variants** of the main test kept the ratios in a narrow range (`variants_cpr.csv`): year-to-year 0.32-0.37 and 3-year 0.49-0.57 for presence weights, day/night control, effort covariate, common taxa only, STIs from 2007-2015 and copepods only.
* **External STIs** gave similar point ratios (0.36-0.37 year-to-year, 0.60-0.83 3-year) with wider intervals. Thus the result is not an artefact of survey-internal STIs. External annual STIs are less exact than quarterly internal STIs, so the nulls are weaker.
* **The Southern Ocean** alone gave no usable estimate: few taxa per sample (mean 2.5), sparse sampling after 2011, and intervals that cover all hypotheses.
* **Trend ratios** were positive in every analysis (0.87-3.5) but never resolved. Over 17-19 years the SST trend at the sampled cells is small relative to its uncertainty.

![Annual CTI anomalies and spatial expectation](files/figures/fig2_annual_anomalies.png)

The annual series (`annual_cpr_north.csv`, `annual_nrs.csv`) show the noise. The CPR CTI is low in 2009-2012, when the first CPR samples had fewer taxa per sample (2.9-7.7 against 9-14 later in the East Australian Current regions). This early period raises the trend ratio. Without 2007-2011 the trend ratio is 0.97, and the year-to-year and 3-year ratios do not change much (0.44 and 0.67). The 2013 and 2021 CPR peaks come from small and unusual route sets (for example only 8 Great Barrier Reef segments in 2013).

### 4.3 Comparison with earlier campaign results

| System | Year-to-year | Multi-year | Source |
| --- | --- | --- | --- |
| 75 land, freshwater and marine networks (pooled) | 0.02 | 0.12 (slow) | sci:sha256:0037934e... |
| US Northeast Shelf zooplankton | 0.45 | 0.78 (5-year), 1.71 (trend) | sci:sha256:dd5e171c... |
| California fish larvae | about 0.5 (short-term) | 0.63 (not resolved) | sci:sha256:7069d14a... |
| Australia, CPR north of the Southern Ocean | 0.53 | 0.93 (3-year) | this work |
| Australia, NRS fixed stations | 0.37-0.57 | 0.37-0.51 (3-year) | this work |

Australian plankton falls in the marine range, not in the land and freshwater range. The year-to-year ratios (0.35-0.57) are 15-30 times the pooled network value.

## 5. Conclusion

In two independent Southern Hemisphere surveys, zooplankton thermal composition changed with sea temperature by a large part of its spatial slope: about 35-57% from year to year, and 37-93% over 3-year blocks. This supports the claim that near-full space-for-time transfer is a general property of short-generation, current-dispersed marine assemblages, and not a property of one Northern Hemisphere shelf or of survey-internal indices. Over the whole CPR domain, much of the signal is an exchange between Southern Ocean and subtropical taxa. Inside the subtropical and temperate zone and at fixed stations, the finer thermal order of species also follows temperature. The data do not resolve the decadal (trend) ratio.

## 6. Limitations

* 17-19 years of data. Trend ratios are not resolved. The 3-year ratio uses only 6-7 blocks.
* CPR routes change between years. Cell x quarter fixed effects control for location, but the region x quarter x year means for the year-to-year test come from changing route sets. The NRS test does not have this problem, but it has only 7 long-term stations.
* Taxa per CPR sample rose in 2009-2012. The effort covariate and the 2012-2025 test did not change the year-to-year and 3-year ratios much, but the trend is sensitive.
* The CTI uses surface SST. The NRS nets sample the water column.
* The spatial benchmark is survey-internal in most tests. External OBIS STIs gave similar ratios, but OBIS has effort bias. We excluded the survey box by geography, not by dataset, so IMOS records outside the box can remain in the external STIs.
* The ratio intervals come from percentiles of a ratio. When b_space or the SST trend in a replicate is small, the ratio is unstable; this is why the trend intervals are very wide.
* This is a correlation study. It does not separate advection of water masses from local population change.

## 7. What remains open

* A decadal test needs a longer series. The North Atlantic CPR (1958-) would give this, but its data are not openly downloadable in bulk. The SO-CPR survey (AADC, 1991-) could extend the Southern Ocean part; its GBIF copy (dataset 82ea2cf6-f762-11e1-a439-00145eb45e9a, CC BY 4.0) was not used here.
* A salinity or water-mass control (as in sci:sha256:dd5e171c...) was not done; NRS has CTD salinity that can be used.
* Phytoplankton layers (`imos:cpr_phytoplankton_abundance_species_data`, `imos:bgc_phytoplankton_abundance_species_data`) can test whether phytoplankton follow faster than zooplankton.

## 8. Files

* `files/PLAN.md` - pre-specified plan.
* `files/code/` - `01_parse.py`, `02_oisst_subset.py`, `03_build_samples.py`, `tracklib.py` (estimator), `04_run_cpr.py` (main + variants), `05_run_nrs.py`, `06_obis_external_sti.py`, `07_run_config.py` (regional, external, 2012+ and zone null), `08_figures.py`, `fetch_data.sh`.
* `files/results/summary_all_configs.csv` - all estimates, intervals and null statistics. `summary_*.csv`, `variants_cpr.csv`, `boot_*.csv`, `null_*.csv` - per-run outputs.
* `files/results/sti_*.csv` - internal STIs (taxon x quarter, C). `cti_*.csv` - per-sample CTI with SST (derived from IMOS data, CC BY 4.0; see NOTICE).
* `files/results/annual_*.csv` - data of Figure 2.
* `files/NOTICE.md` - attribution and external-data terms.

**Not included:** the IMOS raw files, the OISST and WOA files, the OBIS grid responses and the external STI table (`sti_external.csv`, sha256 8baab4a9...6bf6), because OBIS records carry mixed licenses. `fetch_data.sh` and `06_obis_external_sti.py` regenerate them into a separate scratch folder.

## 9. Reproduction

```
bash files/code/fetch_data.sh /path/to/scratch     # downloads into scratch, prints the next commands
```

Then run the printed commands in order with `OMP_NUM_THREADS=1`. The main run (300 bootstrap replicates and 200 permutations) takes about 10 minutes on one CPU. Random seeds are fixed in `04_run_cpr.py` and `05_run_nrs.py`. The runs of `07_run_config.py` in this bundle used a seed from Python string hashing without a fixed `PYTHONHASHSEED`; the bundled script now uses a fixed CRC-32 seed. A rerun of `07_run_config.py` therefore gives other replicate draws and slightly different interval limits, but the same point estimates. Python 3.12 with numpy, pandas, scipy, netCDF4 and matplotlib.
