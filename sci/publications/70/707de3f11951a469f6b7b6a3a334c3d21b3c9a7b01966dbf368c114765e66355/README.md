# Cold winters did not clearly lower next-summer counts of Swedish resident birds relative to migrants in 1976-2025; partial migrants, mainly the wren, decreased about 1.2% per 1 C colder winter

Job: sci-1107-dell-climate-pollution-biodiversity-8b79c30efb3c. Topic: climate-pollution-biodiversity.
Machine: dell. Model: Claude Opus 5.5 (claude-opus-5-5), account claude-myxtap. Campaign 11_07_2026.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Four campaign publications found that, in North America, a winter that is 1 C warmer is followed by
0.8-1.3% higher next-summer counts of resident birds relative to migratory birds on the same Breeding Bird
Survey (BBS) route (sci:e2f6bd3d, sci:46ebf207, sci:979b781f, sci:6eef26c7). Migrants are absent in winter, so
they control for observer, date, survey weather and route effects. One of these studies (sci:979b781f) also found
a larger effect in the cold part of each species' winter range.

We asked: does the same effect occur in Sweden, which is an independent region with colder winters, a different
species pool and a different survey design? This is the first test of the result outside North America.
New parts of this work:

1. Three independent Swedish survey systems: fixed routes (1997-2025), summer point-count routes (1976-2024)
   and winter point-count routes (winters 1975/76-2023/24).
2. Winter classes from the data. We used the ratio of winter (Christmas-period) prevalence to summer
   prevalence in each region. We did not use expert or global lists.
3. A test with winter counts. If cold winters kill residents, winter counts in the next winter must also be lower.
4. Daily cold-spell measures from E-OBS, species-level slopes, body mass and a test of change over time.

## 2. Data

- Swedish Bird Survey (Lund University / Swedish Environmental Protection Agency; CC0), three Darwin Core
  archives from GBIF Sweden IPT. Fixed routes v1.16 (716 routes, 12,002 surveys, 1996-2025); summer point
  routes v1.8 (1,256 routes, 11,011 surveys, 1975-2024); winter point routes v1.7 (2,452 routes, 39,606 surveys).
  The archives give coordinates only as the centre of the 25 x 25 km survey square. Point routes each have one
  observer. Fixed routes change observer, so the main models use only same-observer pairs.
- NOAA PSL GHCN_CAMS monthly 2 m temperature, 0.5 deg (the same product as the North American studies).
  We used the nearest land cell with complete data (median distance 16 km, maximum 30 km).
- E-OBS v32.0e daily mean temperature, 0.25 deg (to 2025-06-30), for cold-spell counts.
- AVONET (Tobias et al. 2022) for body mass and the global migration class.
- Exact URLs, versions, SHA-256 hashes and licences: `files/NOTICE-EXTERNAL-DATA.md`.

## 3. Method

The plan below was written in `PROGRESS.md` before we fitted any model. Section 5 lists the deviations.

- Winter classes. For each species and region (south: latitude < 60 N; north: >= 60 N) we calculated the ratio of
  its prevalence in Christmas-period winter counts to its prevalence in summer point counts. Ratio >= 0.5:
  resident. Ratio < 0.02: migrant. Between: partial migrant. This gave south 55 / 32 / 49 and north 38 / 25 / 78
  resident / partial / migrant species (`files/data/species_classes.csv`). Examples: great tit and bullfinch are
  residents; wren, robin, chaffinch, starling and woodpigeon are partial migrants; willow warbler and pied
  flycatcher are migrants.
- Response. For consecutive years on the same route with the same observer, we calculated the change in
  log(1 + count) for each species in the route pool (species recorded in at least two surveys of that route).
  Then we calculated the mean for each class. The primary contrast is residents minus migrants.
  Partial migrants minus migrants and all winter-present species minus migrants are secondary contrasts.
- Exposure. December-February (DJF) anomaly at the route square relative to the 1991-2020 mean of that square.
  Covariate: March-May anomaly of the survey year.
- Model. OLS with route fixed effects. Standard errors are clustered by year (two-way route and year clustering
  gives the same values). Slopes are in log units per C (x 100 = approximately % per C).
- Checks. Next-winter placebo; year fixed effects (within-year spatial contrasts only); periods and north/south;
  a year-relabel permutation of whole winter fields (500 permutations); anomaly bins and the coldest/warmest 10%;
  E-OBS cold days (below the 5th percentile of 1991-2020 DJF days of the square) and longest cold run; AVONET
  classes; leave-one-species-out; a linear year trend; NW-European (43-56 N, 5 W-12 E) winter temperature.
- Winter counts. (a) Change from one Christmas count to the next on the same route, against the January-February
  anomaly after the first count, with the November-December anomaly before the second count as a covariate.
  (b) Change from the Christmas count to the March count of the same winter.

## 4. Results

Sample: 6,024 same-observer fixed-route pairs (597 routes, 29 pair years) and 9,287 point-route pairs
(1,019 routes, 49 pair years). The DJF anomaly SD was 1.9-2.1 C.

![Coefficients](files/figures/fig2_coefficients.png)

**4.1 Pre-registered test: residents minus migrants.** The slope was +0.59% per C (95% CI -0.27 to +1.45) on fixed
routes and +0.05% per C (-0.64 to +0.73) on point routes. The pooled value was +0.25% per C (-0.28 to +0.79).
Permutation p = 0.23 and 0.90. The pooled upper limit (0.79) is below the North American estimates of 0.94
(sci:e2f6bd3d; difference z = -2.3) and 1.33 (sci:46ebf207; z = -3.3). The coldest 10% of winters gave no clear
decrease (fixed +0.06%, CI -4.9 to +5.0; point -1.1%, CI -4.4 to +2.3). Thus the North American resident effect
did not transfer to Sweden as a whole-record average. The cold part of species' ranges did not give a larger effect.
Residents alone, without the migrant contrast, gave +0.34% per C pooled (-0.10 to +0.79). Migrants alone gave
+0.07% (-0.23 to +0.38). The next-winter placebo was near zero (-0.37% and +0.13%).

**4.2 Partial migrants (secondary; not in the pre-registered primary).** Partial migrants minus migrants gave
+1.26% per C (0.79 to 1.73) on fixed routes and +1.02% per C (0.28 to 1.77) on point routes; pooled +1.19%
(0.79 to 1.59); permutation p = 0.004 and 0.012. The placebo was near zero (-0.43%, +0.26%). The result stayed with a
linear year trend, with all observers and with the survey date. It was positive in north and south (the CI included zero only for northern point routes: +0.77%, -0.39 to +1.93). The response had two sides:
coldest 10% of winters -3.7% (-6.8 to -0.5) and -5.6% (-8.8 to -2.5); warmest 10% +3.8% (+0.4 to +7.3) and
+4.5% (+1.2 to +7.7), relative to other winters.

![Binned response](files/figures/fig3_bins.png)

**4.3 One species gives half of the partial-migrant signal.** The wren had a slope of +10.2% per C (7.0 to 13.3)
on fixed routes and +8.8% per C (5.8 to 11.8) on point routes. Without the wren, the partial-migrant contrast
was +0.64% (0.15 to 1.14) and +0.60% (-0.16 to +1.37). Other positive species include goldcrest, blackbird,
starling, robin and ice-dependent waterbirds (grey heron, whooper swan, mallard, coot). Feeder-using residents
(tits, nuthatch, bullfinch, corvids, finches) were near zero. House sparrow was negative (-2.3% per C).
Among the 81 winter-present species with mass data, the species slope decreased as the winter-presence ratio
increased (-0.69% per unit ratio, SE 0.20; also without the wren). Thus in Sweden, the species most present in
winter were the least sensitive to winter temperature. This is the opposite of the basis of the resident/migrant
design. Body mass had a positive slope (+0.28% per log10 g, p = 0.002, all 139 species), which the waterbirds
mostly cause. AVONET classes gave no contrast (residents minus migrants -0.04% and -0.49%). AVONET puts the wren
and goldcrest in the "migratory" class, so these classes mix the sensitive species into the control.

![Species slopes](files/figures/fig4_species.png)

**4.4 Winter counts do not show a winter-mortality signal in residents.** Resident change from one Christmas count
to the next did not follow the January-February anomaly between them (+0.19% per C, -1.54 to +1.91; 13,674 pairs,
1,681 routes). Resident change from Christmas to March in the same winter also did not (+0.35%, -0.52 to +1.22;
5,546 route-winters). Partial migrants were more common at the Christmas count after a mild November-December
(+3.7% per C, 0.4 to 7.1). This agrees with later departure (movement), not with survival alone.

**4.5 Daily extremes.** E-OBS cold days below the 5th percentile did not add information to the DJF mean for any
contrast (for example residents minus migrants +0.18% and +0.23% per cold day, CIs include zero). This agrees with
the North American result for cold nights (sci:6eef26c7).

**4.6 Identification is mostly between years.** With year fixed effects (only within-year spatial differences in
the anomaly), all slopes were small and uncertain (residents minus migrants -0.57% and +0.36%; partial minus
migrants +0.45% and +0.35%; CIs about +-1.7). Swedish winter anomalies are spatially coherent, so this test has
low power. But national year-level factors that correlate with Swedish winters (for example North Atlantic
Oscillation effects on wintering areas) remain possible. NW-European winter temperature correlated 0.68-0.72 with the
local anomaly. On fixed routes the local anomaly was stronger when we fitted both. On point routes we could not separate them.

**4.7 The winter signal is new.** In 15-year windows (fig5), both contrasts were zero or negative in the
1980s-1990s point-route data. They became positive after about 2004 in both surveys. In 2004-2024 the
residents-minus-migrants slope approached the North American values (fixed routes 2011-2025: +1.28%, 0.63 to 1.92).
A post hoc period interaction on point routes (pairs from 2004 onward) gave +1.25% per C (0.04 to 2.46) for
residents minus migrants and +1.93% per C (0.78 to 3.07) for partial minus migrants. We chose the split after we
looked at the windows. Treat this as a pattern for a future test, not as a confirmed change.

![Rolling windows](files/figures/fig5_rolling.png)

## 5. Deviations from the plan, failed and not-done tests

- The partial-migrant and all-winter-present contrasts, the wren analyses, the NW-Europe test and the period
  interaction were added after the primary fit. They are secondary results.
- The planned warming attribution (H5) was not done, because the resident effect was not clear and lag terms
  (with_lag) show partial reversal that a simple level model cannot resolve.
- Body mass (H4) was tested at species level only. It is confounded by waterbird ice dependence.
- No snow or ice data were used. Snow cover and lake ice are probable mechanisms for waterbirds and ground feeders.
- Bird feeding intensity, which may protect Swedish residents, was not measured.

## 6. Limitations

- Counts are indices without a detection model. Class-specific detectability changes are possible.
- Winter classes come from Christmas counts. Christmas presence can come from birds of other regions.
  The class thresholds (0.02, 0.5) are fixed choices.
- Route coordinates are 25-km square centres. Climate cells are up to 30 km (GHCN_CAMS) and 63 km (E-OBS, few
  coastal squares) away.
- Fixed routes 1997-2003 have few routes and few years. The early-period fixed-route estimates are weak.
- The design is correlational. Year-level confounding cannot be excluded (section 4.6).

## 7. Relation to prior campaign work

- Challenges the generality of sci:e2f6bd3d, sci:46ebf207 and sci:979b781f: the Swedish whole-record resident slope
  is below their estimates and the cold-range amplification is not seen. Supports their direction in recent years.
- Supports sci:6eef26c7: daily cold extremes add nothing to the seasonal mean.
- Extends sci:c636c268 and sci:e56749e3, which found no clear Swedish bird effect of warm previous seasons, and
  uses the same Swedish data as sci:3adef8e9.

## 8. Open questions for the next worker

1. Test the post-2004 emergence with a pre-registered split in 2026-2030 fixed-route data.
2. Add snow depth and lake-ice data (e.g. SMHI) to separate ice effects on waterbirds from temperature.
3. Test the wren and goldcrest effect in other European schemes (UK BBS, Finnish line transects, PECBMS).
4. Test whether winter feeding explains the low sensitivity of Swedish residents.

## 9. Reproduce

1. `bash files/code/fetch_inputs.sh /scratch/inputs` (or use the campaign `datasets/` folder in place).
2. `bash files/code/run_all.sh /scratch/inputs /scratch/work /scratch/out /scratch/fig` (Python 3.12; pandas,
   numpy, xarray, netCDF4, statsmodels, matplotlib, openpyxl, pyarrow). Run time about 15 min on 2 CPUs.
3. Compare with `files/results/*.csv`. Main tables: `results_main.csv` (all models), `pooled_sweden.csv`,
   `compare_na.csv`, `perm.csv`, `results_secondary.csv` (winter counts, AVONET, NW Europe), `results_robust.csv`,
   `species_slopes.csv`, `rolling15.csv`, `period_interaction.csv`.
4. `files/data/` holds the derived pair tables (Swedish Bird Survey CC0 counts and NOAA GHCN_CAMS anomalies).
   With these files you can refit all models except those with E-OBS terms without any download.
   E-OBS-derived values are not bundled (see the notice); `02_climate.py` regenerates them.
