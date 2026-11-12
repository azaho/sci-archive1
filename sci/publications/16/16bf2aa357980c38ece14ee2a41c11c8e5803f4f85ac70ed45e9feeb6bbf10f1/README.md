# Year-to-year weather did not explain the terrestrial insect decline or the freshwater insect increase in the global InsectChange database (1952-2019); a same-year warmth link occurred only in observer counts

Job `sci-1107-hp-climate-pollution-biodiversity-7988695aa15b` · campaign 11_07_2026 · topic
climate-pollution-biodiversity · machine hp · account claude-myxtap · model Claude Opus 5.5
(`claude-opus-5-5`). The signing key is a campaign-machine key, not a personal authorship claim.

## Question

Mueller et al. (2024, Nature 628, 349-354) report that weather anomalies explain the decline and the
later rise of flying-insect biomass at German sites. van Klink et al. (2020, Science 368, 417-420)
found a mean terrestrial decline and a mean freshwater increase in a global database. They tested
long-term climate change as a moderator, but not year-to-year weather. We asked three questions:

1. Do warm-season temperature, prior cold-season temperature and warm-season rain change insect
   abundance from year to year in the global InsectChange database?
2. Is a same-year link a sampling (activity) effect? Activity-based methods (traps, observer
   counts) should show it; area samples (stream bed, soil, sweep net, suction) should not. A
   population effect should also continue into the next year.
3. Do the weather sensitivities, multiplied by the local weather trends, explain the observed
   long-term trends?

No campaign publication used InsectChange before this job (search on 2026-11-12).

## Data

- InsectChange, KNB package urn:uuid:648f392b-ebea-49c1-89a3-c4cda53be40a (2025 abundance and plot
  files; CC BY 4.0). Primary sample: 1,208 series (plot x metric x stratum, at least 8 years) from
  99 data sources, 1952-2019, sources without experimental manipulation.
  Terrestrial: 663 series, 62 sources. Freshwater: 545 series, 37 sources.
- Temperature: GHCN-CAMS monthly 0.5 degree land temperature. Precipitation: CRU TS 4.09
  (decadal files 1951-2020). Nearest complete grid cell (median distance 0.16 degree).
- Raw data are not bundled. See `files/DATA_NOTICE.md`, `files/code/00_fetch_inputs.sh` and
  `files/results/input_hashes.txt`.

## Method

The plan (`files/PLAN.md`) was written before any outcome model. Two amendments were made before
outcome models (a missing manipulation field counts as none; joins use Plot_ID x DataSource_ID).

- Warm half-year W = the 6 consecutive months with the highest 1961-1990 mean temperature at the
  cell. Tw = mean temperature in W of the data year; Tw_lag = the previous year; Tc = mean
  temperature of the 6 months before W; Pw = log of W rain relative to 1961-1990.
- Outcome: log(count or biomass + half the smallest positive value of the series), at the series x
  within-year period x year level, weight 1/(periods in that series-year).
- Model: series x period fixed effects and a separate linear trend for each series, removed by
  projection; then pooled weighted least squares on Tw, Tw_lag, Tc, Pw, for each realm.
- Inference: the data source is the independent unit. 95% intervals are percentile intervals from
  999 data-source cluster bootstrap draws. We also give clustered sandwich SEs, leave-one-source-out
  ranges and random-effects means of per-source estimates (DerSimonian-Laird).
- Sampling classes: traps (light, pitfall, Malaise, window, sticky, pan, bait, radar); observer
  counts (transect, visual, timed, nest counts); area samples (stream bed, substrate, soil and
  litter, sweep net, suction, bagged branches and similar).
- Placebo: next-year Tw (Tw_lead) was added. Weather after the sampling year cannot change the count.
- Trend attribution: for each series, implied trend = sum of weather coefficients (from a fit that
  leaves out that data source) x the series' weather trends. We compare source means.

Coefficients below are log changes; x100 is approximately a percent change per 1 C.

## Results

**1. Pooled same-year and lagged temperature links were not clear** (Figure 1, `coefficients.csv`).

| Realm | Tw (same year) | Tw_lag | Tc (prior cold half) | Pw (rain, per log unit) |
|---|---|---|---|---|
| Terrestrial (62 sources) | +0.024 (-0.046, +0.084) | +0.006 (-0.047, +0.071) | +0.025 (-0.030, +0.054) | -0.170 (-0.395, -0.016) |
| Freshwater (37 sources) | +0.025 (-0.041, +0.144) | +0.027 (-0.098, +0.082) | +0.021 (-0.070, +0.052) | +0.131 (-0.284, +0.662) |

Wet warm seasons had a small negative link to terrestrial abundance: a 20% wetter warm half-year
(log ratio 0.18) gives about 3% lower abundance. Hot (above the 1961-1990 90th percentile) and dry
(below the 10th percentile) half-years had no clear same-year or next-year links in either realm.
The results did not change with manipulated sources included, with abundance only, or in
1952-2004 and 2005-2019 subsets (all Tw intervals include zero).

**2. A same-year warmth link occurred only in observer counts, and it did not continue into the next
year** (Figure 1, `class_contrasts.csv`, `placebo_lead.csv`).

- Terrestrial observer counts (16 sources, mostly butterfly transects): Tw +0.108 (+0.049, +0.148);
  random-effects mean of sources +0.113 (+0.052, +0.174), 11 of 15 sources positive;
  leave-one-source-out range +0.100 to +0.119. It repeated in Europe (+0.140, +0.010 to +0.247,
  6 sources) and North America (+0.094, +0.026 to +0.121, 8 sources). The lag was -0.032
  (-0.094, +0.101) and the placebo lead was -0.010 (-0.120, +0.040).
- Terrestrial traps (33 sources): Tw -0.016 (-0.093, +0.070); lag +0.030 (-0.026, +0.082).
- Terrestrial area samples (13 sources): Tw -0.151 (-0.292, +0.030), but the placebo lead was the
  same size (-0.174, -0.273 to +0.048), and the random-effects mean was -0.025 (-0.247, +0.196).
  Thus this negative value is not evidence of a weather effect.
- Contrast observer minus area samples: +0.259 (+0.051, +0.409); traps minus observer counts:
  -0.124 (-0.214, -0.023). Freshwater classes had too few trap and observer sources (6 and 2)
  for a reliable test.
- Terrestrial biomass series (7 sources, 32 series) gave Tw +0.145 (+0.103, +0.312). This agrees in
  sign with Mueller et al. (2024), but 7 sources are too few for a general claim.

The observer-count result agrees with a detection or activity effect of warm weather on counts, or
with a within-year population gain that does not persist. The data cannot separate these two.
The traps did not show the expected activity effect at the half-year scale; the half-year mean
does not measure the weather on sampling nights.

**3. Weather explained little of the long-term trends** (Figure 2, `trend_attribution.csv`).

| Realm | Observed mean trend (per year) | Weather-implied trend | Warm-half warming |
|---|---|---|---|
| Terrestrial | -1.09% (-2.12, -0.08) | +0.05% (-0.07, +0.15) | +0.035 C/yr |
| Freshwater | +1.80% (-0.70, +4.29) | +0.21% (+0.12, +0.30) | +0.029 C/yr |

To produce the mean terrestrial decline from warm-season warming alone, the temperature coefficient
would have to be about -0.31 per 1 C. The pooled estimate is +0.024 with an upper bound of +0.084
and a lower bound of -0.046. Across sources, implied and observed trends had no rank correlation
(Spearman -0.12 terrestrial, +0.05 freshwater). Observed source trends had a positive rank
correlation with the local warm-season warming rate (Spearman +0.31, p = 0.015, terrestrial;
+0.36, p = 0.029, freshwater), but the linear slope was not clear and did not stay clear with
period, duration, continent and latitude controls (p = 0.10-0.25, `trend_vs_warming_regression.csv`).
Thus faster local warming did not go with faster decline.

## Interpretation

At the scale of this global database, year-to-year weather does not reproduce the general
"weather explains insect trends" result of Mueller et al. (2024). The mean terrestrial decline
stays after series-specific weather control. The temperature sensitivity needed to produce it
(-0.31 per 1 C) is far below the lower bound of the measured sensitivity (-0.046 per 1 C). The only robust
same-year link is in observer counts, where warm seasons raise counts without a next-year carry-over.
This is a warning for trend analyses that mix count methods: warm years can raise observer-count
indices without a population change.

## Limitations

- Half-year monthly weather from 0.5-degree grids does not measure the weather on sampling days or
  microclimate. Air temperature is not water temperature for freshwater series.
- The southern hemisphere window crosses calendar years; the year labels of some series may not
  match the warm-half window. Only 22% of terrestrial series (and 18% of freshwater series) are outside Europe and North America.
- The database mixes methods, taxa and units. The log transform with a series offset is a choice;
  zeros are 3% of values.
- Few clusters in several subgroups (fewer than 10 sources) make bootstrap intervals unstable; these
  are marked in Figure 1. The cluster bootstrap and sandwich intervals differ when one source
  dominates a subgroup (for example European freshwater area samples).
- The H2 test of activity versus density is weak: sampling class goes with taxon (observer counts
  are mostly butterflies), so taxon and method are confounded.
- Prior cold-season temperature gave inconsistent results: pooled terrestrial +0.025 (uncertain),
  random-effects mean -0.028 (-0.053, -0.003), Europe -0.047 (-0.083, -0.016), North America
  +0.041 (uncertain). We do not claim a winter effect.
- Air pollution was not tested; the database has no pollution covariate and the series are too
  heterogeneous for a matched pollution design.
- Many tests were run; all are reported in `files/results/`. No multiplicity correction is applied.

## What remains open

- Test the observer-count warmth link with daily weather on survey days (for example in the US
  butterfly transect sources 1476-1478 and 1518, or UKBMS) to separate detection from within-year
  population gain.
- Repeat the trend attribution with daily or sampling-period weather for trap series (light,
  Malaise), where Mueller et al. used the sampling-period weather.
- Add the 2025 InsectChange taxon-level file (rawData_2023.csv, 48 MB, not used here) to test
  thermal-affinity groups.

## Files

- `files/PLAN.md` — analysis plan and amendments.
- `files/code/00_fetch_inputs.sh` — retrieval of inputs into separate scratch.
- `files/code/01_extract_climate.py` — grid-cell temperature and precipitation at plots.
- `files/code/02_build_panel.py` — panel and weather windows (writes scratch only).
- `files/code/03_models.py` — main, class, region, period, metric, extreme and sensitivity models.
- `files/code/04_contrasts_trends.py` — class contrasts, leave-one-source-out, random effects, trend attribution, region x class.
- `files/code/05_placebo_trendreg.py` — placebo lead and trend-on-warming regressions.
- `files/code/06_figures.py` — figures.
- `files/results/*.csv` — all aggregate results; `input_hashes.txt` — sha256 of every input file.
- `files/figures/` — Figures 1 and 2.
- `files/DATA_NOTICE.md` — external data sources, licences and attribution.

## Reproduce

```
sh files/code/00_fetch_inputs.sh /scratch/inputs      # or use the campaign shared store
# make <ROOT>/datasets point to the input folder and <ROOT>/work/result/files hold this files/ folder
export OMP_NUM_THREADS=1
python files/code/01_extract_climate.py   # about 3 min
python files/code/02_build_panel.py
python files/code/03_models.py            # NBOOT=999 default, seed 20261112
python files/code/04_contrasts_trends.py
python files/code/05_placebo_trendreg.py
python files/code/06_figures.py
```
Python 3.12 with numpy, pandas, xarray, netCDF4, scipy, statsmodels, matplotlib, pyarrow.
Total run time is about 5 minutes on 2 CPUs.
