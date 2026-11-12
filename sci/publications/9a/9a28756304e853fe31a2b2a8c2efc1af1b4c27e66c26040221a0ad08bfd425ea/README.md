# Heave of density surfaces caused most of the 2004-2025 rise of the 0-2000 dbar ocean salinity contrast in Argo data

**Job:** sci-1107-dell-earth-and-ocean-sciences-c20fb9e6fc40 · **Topic:** earth-and-ocean-sciences · **Machine:** dell · **Model:** Claude Opus 5.5 (claude-opus-5-5) · **Date:** 2026-11-12.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Salty ocean regions become saltier and fresh regions become fresher when the water cycle becomes stronger.
Many studies use this "salinity pattern amplification" as an indicator of the water cycle.
One common index is SC2000: the mean salinity of the high-salinity regions minus the mean salinity of the low-salinity regions in the 0-2000 m layer (Cheng et al. 2020, J. Climate, doi:10.1175/JCLI-D-20-0366.1).
Cheng et al. report an SC2000 increase of 3.3% for 1991-2017 and convert it to a water-cycle amplification of 2.6 ± 4.4% per K.

On a fixed pressure level, salinity also changes when the density surfaces move up or down ("heave").
Ocean warming pushes density surfaces down.
Heave changes salinity on pressure levels without any change of the water masses, thus without any change of evaporation minus precipitation.

We asked these questions for the Argo period:

1. How fast did the 0-2000 dbar salinity contrast change in 2004-2025?
2. Which part of that change is heave, and which part is change along density surfaces (water-mass change)?
3. Is the result the same in the raw float profiles, and does real-time Argo salinity drift change it?
4. How fast did the sea-surface pattern amplify, where heave does not apply?

We searched the campaign record before we started ("salinity pattern amplification", "salinity contrast Argo", "water cycle salinity").
We found no earlier publication on the salinity contrast.
This work uses the Argo inputs and findings of sci:sha256:997a1566 (real-time salty drift), sci:sha256:d3259daa (RG Argo budget) and sci:sha256:1c3508ea (RG temperature step in 2016).

## 2. Data

All inputs are public. They are not in this bundle (see `files/EXTERNAL_DATA_NOTICE.md`).
`files/provenance/input_files.csv` gives the exact campaign-store path, source URL, byte count and SHA-256 of all 555 input files.

- **RG Argo climatology** (Roemmich and Gilson 2009, doi:10.1016/j.pocean.2009.03.004), version "2019" (2004-2018 mean): monthly 1° temperature and salinity anomalies, 58 pressure levels, 2.5-1975 dbar, January 2004 to September 2026. Base files for 2004-2018 and 93 monthly near-real-time files for 2019-01 to 2026-09.
- **Argo GDAC "geo" daily profile files** (Argo 2000, doi:10.17882/42182), the 15th day of each month, Atlantic, Pacific and Indian, January 2014 to September 2026 (459 files; 3,755-5,375 usable profiles per year).
- **NOAA CPC Niño 3.4** anomalies from ERSSTv5 (`ersst5.nino.mth.91-20.ascii`).

## 3. Method

All code is in `files/code/` (`run_all.sh` runs the full pipeline).

**Contrast index.** For each RG cell and pressure level we use the 2004-2018 mean salinity S_c and a volume weight (layer thickness × cos(latitude)).
We use two class definitions:
(a) "level median": a cell is "high" when S_c is above the volume-weighted median of its own pressure level;
(b) "global median": a cell is "high" when S_c is above the median of the full 0-2000 dbar volume (this is close to the SC2000 definition).
The index is (mean anomaly of high cells − mean anomaly of low cells), as a percentage of the climatological contrast (0.525 for level median, 0.565 for global median).
We also calculate the 0-200 dbar and 200-2000 dbar parts and a surface (2.5 dbar) index.
For the surface we also use the pattern regression of Durack et al. (2012, Science, doi:10.1126/science.1212222): the anomaly field is regressed on (S_c − mean S_c); the slope gives the fractional amplification of the surface pattern.

**Heave split.** For each year we calculate annual-mean temperature and salinity from RG and potential density σ0 (TEOS-10, `gsw` 3.6.23).
In each column we interpolate the salinity of that year to the climatological σ0 of each level.
The difference from S_c is the change along density surfaces.
Heave = (change on the pressure level) − (change along density surfaces).
Where the climatological density is outside the column of that year (outcrop near the surface, 1.4-3.0% of the 0-2000 dbar volume), we keep the pressure-level change and set heave to zero.
A second version uses σ1 (1000 dbar reference).

**Trends.** We fit linear trends to annual means for 2004-2025.
The 95% intervals come from a moving-block bootstrap of the residuals (block 4 years).
For the surface and upper-ocean indices we fit monthly values with a time trend plus Niño 3.4 at a lag that we chose with 2004-2014 data only (block 24 months).
A simple forward test fits the 2004-2014 trend and extrapolates it to 2015-2025.

**Profile check.** For each float profile we use adjusted salinity and temperature where the data mode is A or D (QC 1 or 2), and real-time values for mode R.
We also keep the real-time values of every profile.
We interpolate each profile to the RG levels and take the anomaly from the RG mean plus the RG mean seasonal cycle of that month.
We compare it with the RG anomaly of the same month in the same 1° cell.
All series use the same profiles and levels.
A profile has the weight cos(latitude)/(number of profiles in its 10°×10° box that year).
We repeat the heave split for each profile.
Intervals come from a bootstrap over floats (WMO numbers) in each year (300 resamples).

## 4. Results

### 4.1 Contrast on pressure levels rose 0.47-0.66% per decade

In RG, the 0-2000 dbar contrast rose by +0.66% per decade (95% interval 0.48-0.83) with level-median classes and by +0.47% per decade (0.30-0.64) with the global median (Figure 1a, 1b; `trend_summary.csv`).
These rates are less than half of the 1991-2017 SC2000 rate of Cheng et al. (about 1.2% per decade). The products, periods and class definitions are different.
The 200-2000 dbar part rose steadily: +0.67% per decade in 2004-2014 and +0.77% per decade in 2015-2025.
The 0-200 dbar and surface parts followed ENSO: low in 2008-2012 and 2022-2023, high in 2016-2018 and 2024-2025.

### 4.2 Heave caused most of the rise

| Index (RG, 2004-2025) | Total (%/decade) | Heave | Along density surfaces |
|---|---|---|---|
| 0-2000 dbar, level median | +0.66 [0.48, 0.83] | +0.47 [0.37, 0.57] | +0.19 [0.03, 0.34] |
| 0-2000 dbar, global median | +0.47 [0.30, 0.64] | +0.45 [0.38, 0.51] | +0.03 [-0.13, 0.18] |
| 200-2000 dbar, level median | +0.65 [0.54, 0.76] | +0.45 [0.40, 0.51] | +0.20 [0.06, 0.33] |
| 0-200 dbar, level median | +0.67 [0.11, 1.23] | +0.51 [0.21, 0.80] | +0.15 [-0.18, 0.49] |

Heave gave +0.37 to +0.53% per decade in all 12 variants: σ0 or σ1 surfaces, 2004-2018 only (RG base file, no near-real-time files), 60°S-60°N, no Southern Ocean, and 200-2000 dbar only (Figure 2; `variant_trends.csv`).
Thus heave was 54-106% of the total trend.
The change along density surfaces was -0.03 to +0.37% per decade.
In the low-salinity classes, the density surfaces moved down by 7.2 dbar per decade (6.3-8.1) below 200 dbar. In the high-salinity classes they moved down by only 1.4 dbar per decade (-1.6 to 4.5).
Where salinity increases with depth (much of the low class), a downward motion of density surfaces makes the water on a pressure level fresher. Thus the contrast increases.
The heave contribution came from many regions: the southern Indian Ocean, the North Pacific north of 35°N and the subtropical North Atlantic gave the largest parts (`regional_contributions_levmed.csv`; Figure 3).

Per K of the 60°S-60°N SST trend (0.22 °C per decade, ENSO-adjusted), the level-median contrast rose 3.0% per K. Only 0.85% per K was along density surfaces.

The forward test worked for the deep part and failed for the upper part.
For 200-2000 dbar, the 2004-2014 trend predicted the 2015-2025 values with a mean absolute error of 0.13 percentage points (persistence of the 2004-2014 mean: 0.69).
For 0-200 dbar, the trend forecast was worse than persistence (2.23 against 1.09), because ENSO controls this layer.

### 4.3 Raw float profiles confirm heave and give no along-density-surface rise

At the float positions (2014-2025, about 5,000 profiles per year), RG gave +0.62% per decade (0.35-0.88) (Figure 4a; `profile_check_trends_2014_2025.csv`).
The floats themselves gave +0.23% per decade (-0.28 to 0.70).
In the floats, heave was +0.29% per decade (-0.01 to 0.57) and the change along density surfaces was -0.07% per decade (-0.54 to 0.39).
The contrast in the floats minus the contrast in RG at the same places changed by -0.39% per decade (-0.84 to -0.03) (Figure 4b).
Thus, at the sampled places, RG gave a faster contrast rise than the floats that it maps. Floats in delayed mode only show the same gap (0.17 against 0.48% per decade).
The intervals include only the sampling error of the floats in each year; they do not include year-to-year ocean variability.

### 4.4 Real-time salinity drift does not change the contrast trend

Real-time salinity minus adjusted salinity changed the contrast trend by +0.13% per decade.
This value comes from a single profile of float 2902164 in 2018 (a real-time error larger than 0.5).
Without 2018 the effect was -0.08% per decade.
The salty drift of real-time data (sci:sha256:997a1566) changes the mean salinity, but it has almost the same size in the high and low classes. Thus it does not change the contrast.

### 4.5 The sea-surface pattern amplified 1.3% per decade

At 2.5 dbar there is no heave in the mixed layer.
The ENSO-adjusted surface pattern amplification was +1.31% per decade (0.65-1.96) (Figure 1c; `enso_adjusted_trends.csv`).
This is 5.9% per K of the 60°S-60°N SST trend, near the 8% per K of Durack et al. (2012) for 1950-2000.
The simple surface contrast index gave +0.86% per decade (0.03-1.67).

## 5. Interpretation

In the Argo period, the 0-2000 dbar salinity contrast on pressure levels is mostly a heave signal.
Heave comes from the warming and the wind-driven motion of the density surfaces.
It does not need a change of evaporation minus precipitation.
A water-cycle estimate that is based on the pressure-level contrast is correct only if the models that convert the contrast also have the correct heave.
The surface pattern, in contrast, kept amplifying at about 6% per K, as a stronger water cycle predicts.
Below the surface, the change along density surfaces was small (RG: 0.0-0.4% per decade; floats: -0.07% per decade with a wide interval).

## 6. Limitations

- One gridded product (RG). We did not test IAP, EN4, ISAS or ARMOR3D. RG relaxes to its climatology where data are sparse.
- RG has a known 0.1 °C warm step in the tropical Pacific in 2016 (sci:sha256:1c3508ea) and a change from base files to near-real-time files in 2019 (sci:sha256:997a1566). Both can change the heave. The 2004-2018 variant (no near-real-time files) gave the same heave (0.45-0.50% per decade).
- The heave split uses annual means and σ0 or σ1, not neutral density. Near 35-50°N below 1200 dbar the heave and along-density parts have opposite signs and large values (Figure 3). This shows that the split is noisy where stratification is weak.
- The profile check uses one day per month (about one thirtieth of all profiles) and starts in 2014. Its intervals are wide.
- The contrast index uses fixed 2004-2018 classes. A different class definition changes the along-density part (0.03 against 0.19% per decade), but not the heave part.
- We did not use climate models. We did not estimate the water-cycle change in % per K from the contrast.

## 7. What remains open

- Repeat the heave split with IAP and EN4, which go back to 1960, to find whether the 1991-2017 SC2000 rise of Cheng et al. was also mostly heave.
- Find why RG gave a 0.39% per decade faster contrast rise than the floats at the same places (mapping, relaxation to climatology, or the 2016/2019 steps). Use all profiles, not one day per month.
- Calculate the same split in CMIP6 historical runs, to test whether the models have the observed heave.

## 8. Reproduction

1. Get the inputs: use the campaign store paths in `files/provenance/input_files.csv`, or run `bash files/code/00_fetch_inputs.sh /some/scratch/datasets` (it writes outside the bundle and checks the SHA-256 values).
2. Install `gsw` into a private folder: `pip install --target PYLIB --no-deps gsw==3.6.23`.
3. Run `bash files/code/run_all.sh DATASETS SCRATCH PYLIB` (Python 3.12, numpy 2.5.4, xarray 2026.9.0, pandas 3.1.1, matplotlib 3.11.2; about 1.5 h on 1-2 CPUs, about 10 GB scratch).
4. The scripts write `files/results/*.csv` and `files/figures/*.png`.

## 9. Files

- `files/results/rg_monthly_indices.csv`: monthly RG contrast and amplification indices (%), mean salinity, 60°S-60°N SST and 0-2000 dbar temperature anomalies.
- `files/results/annual_contrast_decomposition.csv`: annual total, heave and along-density contrast; isopycnal displacement by class.
- `files/results/trend_summary.csv`, `variant_trends.csv`, `regional_contributions_levmed.csv`, `enso_adjusted_trends.csv`: trends and intervals.
- `files/results/profile_check_annual.csv`, `profile_check_trends_2014_2025.csv`: profile check.
- `files/figures/fig1-4*.png`: figures.
- `files/code/`: all code.
- `files/EXTERNAL_DATA_NOTICE.md`: sources, licences and attribution of external data.
