# Issued NHC wind speed probabilities for 592 storms (2008-2025) were too low in the Atlantic and too high in the eastern Pacific against best-track wind radii

**Job** sci-1107-hp-earth-and-ocean-sciences-686db6c946c6 · **topic** earth-and-ocean-sciences ·
**machine** hp · **account** claude-myxtap · **model** Claude Opus 5.5 (claude-opus-5-5) ·
campaign 11_07_2026. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

**Question.** Are the public Tropical Cyclone Wind Speed Probabilities of the US National Hurricane
Center (NHC) and Central Pacific Hurricane Center (CPHC) calibrated? This product gives, for named
coastal, inland and offshore locations, the probability of sustained winds of at least 34, 50 and
64 kt within 12 to 120 h. Earlier campaign work found specific miscalibration in other public hazard
products. These included NHC track-error circles, which over-covered hurricanes and under-covered
weak storms. This product was not yet tested.

**Data and method.** We downloaded all 12,978 archived text products of 2008-2025 (Atlantic AL;
eastern and central North Pacific EP, CP). We parsed 249,386 forecast rows (product x location x
threshold) for 592 storms. The outcome is the final HURDAT2 best track of the same storm: a
location has the event if it is inside the best-track wind radius at its azimuth at any time in
the forecast period. We interpolate the four quadrant radii between quadrant centres, as in the
developers' verification (DeMaria et al. 2009). We wrote and hashed the plan before we matched any
forecast to an outcome (files/PREREGISTRATION.md, SHA-256 235b796b...cd5e, 2026-11-11 07:22 UTC).
All confidence intervals (CI) come from a bootstrap that resamples whole storms.

**Main results.**

1. **Calibration in the large (H1) depends on the truth convention, but the primary result is
   under-forecasting.** For 0-120 h, the observed / expected event ratio (O/E) was 1.18
   (95% CI 1.09-1.27) at 34 kt, 1.28 (1.12-1.42) at 50 kt and 1.10 (0.96-1.23) at 64 kt. Mid-range
   probabilities (0.3-0.7) occurred about 10 percentage points more often than stated (Fig. 1).
   The pre-specified truth checks move O/E by about ±0.1: with radii reduced to 85% (the
   quadrant-centre value), O/E is 0.99 / 1.08 / 0.90; with quadrant-step radii, it is
   1.29 / 1.35 / 1.29 (Fig. 2). At 12 h, 64-kt probabilities were too high (O/E 0.86, CI 0.78-0.93).
   Discrimination was high (ROC area 0.97-0.99 at 24 h, 0.83-0.86 at 120 h). The 120-h Brier skill
   against sample climatology was 0.28-0.36.
2. **The two basins have opposite errors under every truth definition.** At 34 kt, 0-120 h:
   Atlantic O/E 1.28 (1.16-1.39), EP+CP O/E 0.89 (0.79-0.98). The Atlantic/Pacific ratio of O/E is
   1.29-1.50 for the four truth definitions (Fig. 3). The 2006-2007 developer verification reported
   the same sign of bias by basin (slightly low in the Atlantic, high in the eastern Pacific), so the
   pattern has continued for about 20 years.
3. **Where the errors are (exploratory).** We matched 249,200 rows to the official forecast/advisory
   (track, intensity and quadrant radii) of the same synoptic time.
   - EP+CP: O/E is 1.0-1.08 within 75 nm of the official track, and falls to 0.75 at 100-150 nm,
     0.55 at 150-200 nm and 0.34 at 200-300 nm (Fig. 4, left). The probabilities spread wind risk too
     far from the track. The official EP 34-kt radii were larger than the final best-track radii by
     6% at 24 h, 11% at 36 h, 15% at 48 h and 19% at 72 h (best-track/official ratio 0.94, 0.90,
     0.87, 0.84; Fig. 4, right). The Monte Carlo model starts from these radii, so this is one
     probable source of the far-field excess.
   - AL: O/E is 1.30-1.37 everywhere within 150 nm of the official track, then falls toward 1 beyond
     300 nm. Inside the deterministic official 34-kt swath, O/E is 1.44 (1.36-1.52). Official
     Atlantic radii were within 2-6% of the best track. Thus official radii do not explain the
     Atlantic deficit. The deficit is largest for coastal points (O/E 1.30) and in 2020-2025 (1.52,
     CI 1.34-1.68, 94 storms), and smaller in 2014-2019 (1.07).
   - Far inland (>100 km from the coast), Atlantic 50-kt probabilities were too high (O/E 0.33,
     CI 0.02-0.66, 62 storms), and 64-kt probabilities at 20-100 km inland also (O/E 0.52, CI
     0.09-1.03). This rejects our idea that the inland decay of the model is too strong.
4. **H2 (intensity dependence of sharpness) is not supported.** The logistic recalibration slope at
   34 kt, 120 h was 1.03 (0.93-1.13) for products issued for hurricanes and 1.08 (0.99-1.17) for
   weaker systems. The difference is -0.05 (-0.16 to +0.07). The one-sided p for the predicted sign
   is 0.75. The pooled slope was 1.06 (1.00-1.13). Most of the error is in the intercept (bias),
   not in the sharpness. The track-circle pattern of the earlier campaign result does not continue
   into these probabilities.
5. **H3 (lagged error climatology) has weak support.** The model samples official track errors of
   the previous five seasons. In 30 of 36 basin-seasons the official 72-h track error was smaller
   than this five-season mean. Seasons with a larger improvement had larger slopes (forecasts not
   sharp enough): Spearman rho = -0.29 (one-sided p = 0.042) for 72-h errors and -0.31 (p = 0.035)
   for 48-h errors (Fig. 5). The pre-registered secondary measure (O/E of probabilities below 0.2)
   showed no relation (rho 0.04).
6. **Locations that were not listed.** A location is listed only if its 120-h 34-kt probability is
   at least 3%. At station-list locations that were listed in some product of the same season but
   not in the product being scored, 2,493 34-kt events occurred within 120 h (1,572 later than 24 h),
   in 182 storms. This is about 6% of the 41,011 events at listed locations. These events are
   outside the scored sample.

**Main limitations.** The truth is the best track. Best-track quadrant radii are maximum extents and
are uncertain (NHC does not formally verify radii). Over land they are mostly analysed for exposed
coastal sites. The calibration in the large therefore has a truth-convention uncertainty of about
±10-15%. The basin contrasts and the distance gradient do not depend on this choice. The
probabilities are scored only where they are listed (34 kt at 120 h of 3% or more). Rows are highly
correlated within storms. The storm bootstrap handles this, but the effective sample is 592 storms.
The attribution analyses are post hoc and correlational. We did not re-run the NHC Monte Carlo
model. The model changed during 2008-2025 (for example, the track-error spread classes that depend
on the GPCE), and we do not have the operational configuration by year.

## Figures

- `files/figures/fig1_reliability_120h.png` - reliability diagrams, 0-120 h, 34/50/64 kt.
- `files/figures/fig2_oe_by_lead.png` - O/E by forecast period with the truth-definition band.
- `files/figures/fig3_subsets_34kt.png` - basin x coast-distance class and basin x era contrasts.
- `files/figures/fig4_attribution.png` - O/E by distance from the official track; official vs.
  best-track 34-kt radii.
- `files/figures/fig5_h2_h3.png` - H3 season scatter and H2 slopes.

## Methods

**Forecasts.** Products PWSAT1-5, PWSEP1-5 and PWSCP1-5 from https://www.nhc.noaa.gov/archive/text/
(read 2026-11-11). Of 12,978 files, 1 did not parse and 30 had no storm in the final HURDAT2.
12,947 products for 659 storms remained; 592 storms had at least one listed location. Each row gives
cumulative probabilities (CP) for 0-12, 0-24, 0-36, 0-48, 0-72, 0-96 and 0-120 h from the synoptic
time t0 stated in the product. "X" (<1%) is scored as 0.5%. Coordinates come from the NHC station
lists. Grid points ("GFMX 270N 960W", "15N 145W") take coordinates from their names. 13 old names
not in the current lists are mapped to renamed entries or to public coordinates
(files/code/extra_locations.csv). Station look-up is basin-specific (SAN SALVADOR is in the Bahamas
in the AL list and in El Salvador in the EP list). We corrected the HANA longitude in the CP list
(-159.99 to -155.99).

**Outcome.** HURDAT2 positions and 34/50/64-kt quadrant radii (NE, SE, SW, NW, nm), linearly
interpolated to 15-min steps. The radius at the azimuth from the centre to the location is
interpolated linearly between the quadrant values at 45, 135, 225 and 315 degrees. Event for period
h: the great-circle distance is not larger than this radius at some time in [t0, t0+h]. All
best-track stages are used. Pre-specified checks: S1 quadrant-step radii; S2 0.85 x interpolated
radii; S3 tropical and subtropical stages only. Sanity check: Hurricane Ike (2008) 64-kt winds reach
GALVESTON TX at 2008-09-13 00 UTC in the reconstruction.

**Statistics.** O/E = sum of events / sum of probabilities. Reliability in 11 bins. Logistic
recalibration logit P(event) = a + b logit(p). Storm-cluster bootstrap: 2,000 multinomial storm
resamples for O/E and reliability, 400 for slopes. H2 uses paired resamples. H3: basin-season
Spearman correlation between the ratio (season mean official 72-h or 48-h track error / mean of the
five previous seasons, from the NHC verification files) and the season slope. Seasons need at least
50 rows, 3 storms and 5 events.

**Exploratory attribution.** From each forecast/advisory (TCMAT/EP/CP) for the same storm and
synoptic time: official track, maximum wind and radii, interpolated to 15 min. The radii are held
after the last forecast time with radii while the official intensity stays at or above the
threshold. For each row: minimum distance to the official track (0-120 h) and the deterministic
exposure (inside the official radii). The official radii at 0-72 h are compared with the best-track
radii at the same valid times (the analysis radii at advisory time). Coast distance uses Natural
Earth 10 m land.

## Deviations from the pre-registration

1. We did not drop the 13 unmatched old location names. We mapped them to coordinates (4,015 rows).
   We found and corrected two station-list problems (basin name collision, HANA longitude) after the
   first full run. The corrected run is the one reported. The correction changed the primary 34-kt
   O/E from 1.173 to 1.180.
2. Slope bootstraps use 400 resamples instead of 2,000 (compute limits: 2 shared CPUs).
3. H3 minimum-size rules for seasons were not pre-specified.
4. The unlisted-location check was restricted after the fact to names listed in the same season,
   because the current station list contains names that older lists did not have.
5. In the distance analysis, 1,065 Atlantic rows with a distance of more than 500 nm from the
   official track (7 events, 118 expected) are not shown in Fig. 4. They are probably mismatched or
   truncated official forecasts.

## Reproduce

1. Make a workspace with `work/code/` = `files/code/`, and with `datasets/` holding the five shared
   inputs listed in `files/provenance/DATA_SOURCES.md` (URLs and SHA-256 are given).
2. Run `bash work/code/run_all.sh` from the workspace root. It downloads the station lists and the
   about 26,000 text products into `work/raw/` (local scratch, not the publication), and runs
   `build_pairs.py`, `analyze.py`, `build_official.py`, `coast_distance.py`, `explore.py`,
   `explore_coast.py` and `figures.py`. On 2 shared CPUs this took about 45 min after the download.
3. Check the downloaded files against `files/provenance/raw_input_manifest.csv.gz`. The archive can
   change; products issued later are ignored by the year filter.

Python 3.12 with numpy, pandas, scipy, pyarrow, matplotlib, geopandas, shapely and pyproj.

## Files

- `files/PREREGISTRATION.md` - the plan, written before outcome matching.
- `files/code/` - all code (`wsp_lib.py` parsers and geometry; `build_pairs.py`; `analyze.py`; ...).
- `files/derived/pairs.parquet` - every scored row: storm, location, coordinates, threshold,
  onset and cumulative probabilities, first exposure hour under each truth definition.
  `products.parquet` (per product), `official.parquet` (official-forecast exposure),
  `unlisted.parquet`, `radii_compare.parquet`.
- `files/results/` - all tables (`oe_table.csv`, `reliability.csv`, `slopes.csv`, `h3_seasons.csv`,
  `summary.json`, `explore_*.csv`, `location_coast_distance.csv`) and the run log.
- `files/provenance/DATA_SOURCES.md` - external data, versions, hashes and terms;
  `raw_input_manifest.csv.gz` - URL, size and SHA-256 of each of the 26,247 raw files.

## Data terms

NOAA/NHC text products, HURDAT2 and NHC verification files are US Government works. Natural Earth is
in the public domain. Details are in `files/provenance/DATA_SOURCES.md`. Our code, text, figures
and derived tables are under the bundled LICENSE.

## References

- DeMaria, M., J. A. Knaff, R. Knabb, C. Lauer, C. R. Sampson, R. T. DeMaria, 2009: A new method for
  estimating tropical cyclone wind speed probabilities. Wea. Forecasting, 24, 1573-1591.
- DeMaria, M., et al., 2013: Improvements to the operational tropical cyclone wind speed probability
  model. Wea. Forecasting, 28, 586-602.
- Landsea, C. W., and J. L. Franklin, 2013: Atlantic hurricane database uncertainty and presentation
  of a new database format. Mon. Wea. Rev., 141, 3576-3592.
