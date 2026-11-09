# Butterflies flew later at British sites with more nitrogen deposition, but tree-feeding species also flew later, so this study did not show sward cooling

## Summary

We tested the microclimate-cooling hypothesis for nitrogen (N) deposition
(WallisDeVries and van Swaay 2006). This hypothesis says that N makes the grass
and herb layer denser and taller. Thus the layer where caterpillars and pupae
develop in spring becomes cooler, and adult butterflies emerge later. We wrote the
predictions and the models before we fitted them (`files/code/ANALYSIS_PLAN.md`):

- **P1.** Species whose immature stages develop in the grass or herb layer
  ("sward group") fly later at sites with a higher chronic N load.
- **P2.** Species whose immature stages develop on trees or shrubs ("woody group")
  do not show this delay. This is the placebo test.
- **P3.** At high-N sites, flight dates of sward species move less with spring
  warmth.

Data: UK Butterfly Monitoring Scheme (UKBMS) mean flight dates of 20 univoltine
species (one adult brood per year) on British transects. Exposure: CBED 5 km
grid-average total N deposition, mean of 1986-2012. Controls: 50 km block by year
fixed effects, elevation (Copernicus 90 m DEM), mean annual rainfall and local
temperature (E-OBS 0.25 degree), and in exploratory models, land cover (ESA
WorldCover 2021).

Main results (days per 10 kg N/ha/yr; random-effects mean of species estimates; 95% interval):

| Test | Sward group | Woody group (placebo) |
|---|---|---|
| Primary model, 1986-2012 (60,296 site-species-years, 1,401 sites) | **+1.7 [-0.0, +3.5]**, k = 18 | +9.1 [+1.2, +17.0], k = 2 |
| Primary + 4 land-cover classes (exploratory) | **+2.4 [+0.8, +4.0]** | +6.4 [-2.6, +15.4] |
| Sward minus woody, primary model | -7.4 [-15.5, +0.7] | |
| P3: change in the temperature slope per 10 kg N/ha/yr (1986-2024) | **+0.15 [-0.17, +0.48] days per C** | +0.29 [-1.46, +2.03] |
| Temperature slope (for scale) | -4.25 [-4.54, -3.96] days per C | -3.80 [-6.28, -1.31] |

- **P1, partly supported, small effect.** Sward species flew about 2 days later per
  10 kg N/ha/yr. The point estimate was positive in all three regions and all three
  periods, which includes 2013-2024, outside the exposure years. In the primary model
  the interval touched zero (lower limit -0.01). Thus the pre-set "clear" rule (the
  interval excludes zero and the sign repeats in all regions and periods) was **not
  met**. It was met only in the exploratory land-cover model. The 10th-90th
  percentile range of site N was 10.3-17.1 kg N/ha/yr. Over this range, the delay
  is about 1.2-1.6 days. That is a similar delay to about 0.3-0.4 C of cooler
  spring weather.
- **P2, not supported.** The two woody-host species with sufficient data (Purple
  Hairstreak *Favonius quercus*, White Admiral *Limenitis camilla*) had a larger
  positive N association than the sward species in every model. The sward minus
  woody difference was negative (not the predicted positive). Thus the delay at
  high-N sites is not specific to the layer where the hypothesis puts the
  mechanism. The woody group is small (k = 2-3) and its intervals are wide.
- **P3, not supported.** Flight dates advanced by about 4.2 days per 1 C of local
  temperature in the 60 days before flight. This response did not become clearly
  weaker at high-N sites. The upper 95% limit (+0.48 days per C per 10 kg N/ha/yr)
  is 11% of the mean temperature slope.
- **Confounding structure.** Grid-average N correlated with site elevation
  (r = 0.48) and, within 50 km blocks, with the 5 km tree-cover fraction (r = 0.52).
  CBED grid-average values weight deposition by land cover, and forest captures
  more dry deposition. Without elevation and rainfall controls, the sward estimate
  doubled (+3.6). The largest positive species estimates were for woodland-edge
  or woodland species (Dark Green Fritillary, Silver-washed Fritillary, Large
  Skipper, Purple Hairstreak, White Admiral).

Conclusion: a later flight period at high-N British sites is present but small.
The trait-group placebo and the absence of a change in temperature response do
not support sward microclimate cooling as the cause. Residual site coolness or
woodland structure that grid-average N tracks is an equally possible explanation.

## Figures

- `files/figures/fig1_forest_N_flight_date.png`: Group means for all model variants, regions and periods.
- `files/figures/fig2_species_estimates.png`: Species estimates with and without land-cover controls.
- `files/figures/fig3_temperature_by_N.png`: Temperature slopes and their change with N (P3).
- `files/figures/fig4_binned_residuals.png`: Sward-group flight-date residuals by N bin, before and after controls.

## Methods

**Outcome.** UKBMS `MEAN_FLIGHT_DATE`: the count-weighted mean day after 1 April
of all counts of a species at a site in a year. We used only univoltine species, so
that the mean date refers to one brood. We excluded bivoltine, adult-hibernating and
migrant species and the *Thymelicus* aggregate. The species lists are in
`files/code/02_analysis.py` and `ANALYSIS_PLAN.md`. *Erebia aethiops* and three
woody species did not meet the 300-record / 30-site minimum in the primary model.

**Observation-bias controls.** The primary filter kept records with a peak count of
at least 3. It also kept only site-years in which some species was recorded by day 45
(15 May) and some species was recorded on or after day 150 (29 August), which removes
partly walked seasons. Sensitivity runs used peak counts of 1 and 10, no
season-coverage filter, and added log(peak count) and the site-year species count.
Block-by-year fixed effects remove year-specific national and regional weather and
recording changes. Standard errors are clustered by site.

**Exposure.** CBED total N deposition (NOx + NHx) at the 5 km cell that holds the
transect start, as the mean of 1986-2012 (kg N/ha/yr). We did not use annual
values as the main exposure, because wet deposition follows the rainfall of each
year. Also, the Spearman correlation of site N between 1986-1988 and 2010-2012 was
only 0.60. NHx and NOx were also tested separately (NHx: sward +3.0 [+0.6, +5.5];
NOx: +2.4 [-2.2, +7.0]; woody estimates were larger in both).

**Primary model (each species, 1986-2012).**
`MFD ~ N10 + elev/100 + (elev/100)^2 + rain/100 + T_window + FE(50 km block x year)`.
`T_window` is the local E-OBS mean daily temperature over the 60 days that end on
the national median mean flight date of the species. We combined species estimates
with DerSimonian-Laird random effects in each group.

**P3 model (each species, 1986-2024).** Site fixed effects, `T_window`,
`T_window x N` and `T_window` interactions with elevation, rainfall, northing and
easting, and linear year trends for each region.

**Replication.** Three regions (SE England: northing < 300 km and easting >= 400 km;
SW England and Wales: northing < 300 km and easting < 400 km; North: northing >= 300 km)
and three periods (1986-1999, 2000-2012, 2013-2024).

**Exploratory analyses (added after we saw the primary results).**
E1 added the fractions of tree cover, grassland, cropland and built-up land in a
1 km box and in the 5 km CBED cell (ESA WorldCover 2021). E2 split the sward group
into short-sward specialists and tall-grass species (short-sward +0.5 [-2.6, +3.6],
tall-grass +1.2 [-0.9, +3.3] in the primary model). The prediction was a larger delay
in short-sward species, and the result did not show this. E3 removed one species at
a time from the sward group: the mean stayed between +1.2 and +2.1 (primary) and
between +1.9 and +2.8 (land-cover model). Heterogeneity among species was high
(I2 = 0.76 primary, 0.59 land-cover model).

## Sensitivity table (sward group, days per 10 kg N/ha/yr)

| Variant | Estimate [95% interval] |
|---|---|
| Year fixed effects only | +1.75 [+0.54, +2.95] |
| No elevation or rainfall control | +3.58 [+2.15, +5.01] |
| Primary | +1.73 [-0.01, +3.48] |
| Peak count >= 1 | +1.78 [+0.17, +3.38] |
| Peak count >= 10 | +1.74 [-0.28, +3.76] |
| No season-coverage filter | +2.16 [+0.44, +3.87] |
| + log(peak count) + species count | +1.72 [+0.11, +3.33] |
| 25 km blocks | +1.47 [-0.23, +3.18] |
| 1 km mean elevation | +1.01 [-0.88, +2.91] |
| SE England / SW England+Wales / North | +1.09 / +3.19 / +2.20 |
| 1986-1999 / 2000-2012 / 2013-2024 | +1.10 / +2.02 / +2.45 |
| + 4 land-cover classes | +2.37 [+0.78, +3.97] |

All values, intervals, species counts and I2 are in `files/results/meta_summary_*.csv`.
Species-level coefficients are in `files/results/species_coefficients_*.csv`.

## Limitations

- This is an observational, cross-sectional contrast. N load is not randomly
  assigned. Elevation, rainfall, woodland cover and other site properties that
  covary with N can bias the result. The estimate moved between +1.0 and +3.6 days
  with the choice of controls.
- The CBED grid average is a 5 km land-cover-weighted value. It is not the
  deposition on the transect habitat. The exposure stops in 2012. For 2013-2024 we
  assumed that the 1986-2012 site ranking stayed the same.
- E-OBS temperature (about 25 km) does not show microclimate. We did not measure
  sward height or ground temperature, so we cannot test the mechanism directly.
- The woody placebo group has only 2-3 species with sufficient data. It cannot
  separate a general N effect on all habitats from site confounding.
- Mean flight date depends on weekly visit completeness. The public table does not
  give visit counts, so we used a season-coverage proxy.
- Site selection in UKBMS is not random. Transects are more frequent in southern
  England and in protected or semi-natural sites.
- Species groups use published life-history knowledge and the trait table of Cook
  et al. (2025). Other group definitions can give different results.

## Reproduction

Shared raw data were read in place from the campaign dataset store (paths and hashes
in `files/provenance/input_files.json`). To reproduce the analysis from public sources:

```bash
bash files/code/00_retrieve_data.sh /tmp/nbf_data            # external data -> local scratch
python3 files/code/01_build_inputs.py --datasets /tmp/nbf_data --scratch /tmp/nbf_scratch
python3 files/code/03_landcover.py --scratch /tmp/nbf_scratch  # ESA WorldCover windows (about 25 min)
python3 files/code/02_analysis.py --scratch /tmp/nbf_scratch --out /tmp/nbf_out/results
python3 files/code/04_figures.py --res /tmp/nbf_out/results --out /tmp/nbf_out/figures
```

`01_build_inputs.py` also downloads Copernicus GLO-90 DEM tiles. The tile URLs and
their SHA-256 values are in `files/provenance/copernicus_dem_tiles.json`. Software
versions are in `files/provenance/software_versions.txt` (Python 3.12, pandas,
numpy, scipy, xarray, rasterio, pyproj, matplotlib). The full run takes about 35
minutes on 8 cores. Most of the time is for the remote land-cover reads.

This bundle has no record-level third-party data. It has only our code, our
figures and our aggregate model results. See `files/NOTICE.md` for the external data,
licences and the required attribution.

## Provenance

- Job: sci-1107-hp-climate-pollution-biodiversity-4004474f5df9; campaign 11_07_2026;
  topic climate-pollution-biodiversity; machine hp; account claude-andrii.
- Model: Claude Opus 5.5 (claude-opus-5-5), in the Claude Code harness. The signing key is a
  campaign-machine key, not a personal authorship claim.
- Analysis date: 2026-11-09.
- Related campaign work: earlier campaign publications tested N deposition with
  butterfly abundance, trends and warmth slopes of abundance. They found no
  repeated N contrast after geographic controls. A search of the campaign
  catalogue on 2026-11-09 found no earlier publication that tested N with flight timing.
