# NHC wind speed probabilities (2010-2025, 604 storms) were nearly calibrated only with the model's 0.86 radius factor; in all radius rules they were too low for large and too high for small storms

## Main result

The National Hurricane Center (NHC) publishes 0-120 h probabilities that tropical-storm (34 kt), strong tropical-storm (50 kt) and hurricane (64 kt) winds reach each point (wind speed probabilities, WSP). We matched 7,405 half-degree WSP grids (2010-2025, Atlantic and eastern and central North Pacific, 604 storms, 20.7 million point records) to the best-track wind areas of the storms that had an official forecast at issue time. We also tested 435 grids from 2026 against operational best tracks.

1. **The overall verdict depends on how a quadrant wind radius is converted to an area.** NHC defines each quadrant radius as the *largest* extent of the wind in that quadrant. If we fill each quadrant to that radius (the convention in our plan), observed events were 1.33 (95% storm-bootstrap interval 1.23-1.41), 1.46 (1.33-1.59) and 1.30 (1.16-1.44) times the forecast sums for 34, 50 and 64 kt. Thus, the WSP looks too low. The WSP model (DeMaria et al. 2009) uses 0.85 times each radius at the quadrant centre. The hour-0 WSP fields confirm this: the 50% edge was at 0.86 of the as-issued radius in every year 2010-2025 (34 and 50 kt; 0.85-0.90 for 64 kt). With this product radius rule (0.86), the ratios were 1.04 (0.96-1.12), 1.16 (1.05-1.25) and 1.02 (0.92-1.13). Thus, the product is close to calibrated on its own terms, with a 16% excess at 50 kt. Of the event excess under the plan rule, 65-93% comes from the radius convention, not from forecast error. A user who reads the wind areas with the NHC quadrant-maximum definition finds 30-46% more events than the probabilities state.

2. **The error follows storm size in every convention (pre-registered hypothesis supported).** With the product rule, 34-kt O/E was 0.73 (0.66-0.82) for storms in the smallest third of initial 34-kt size and 1.31 (1.21-1.41) for the largest third (difference 0.58, 0.46-0.69). The pattern holds at 50 and 64 kt, with as-issued sizes, and inside each strength class (initial wind below 64 kt: 0.73 versus 1.13; 64 kt or more: 0.75 versus 1.40). Storms that had no 34-kt winds at the start were also over-forecast (0.79, 0.71-0.88).

3. **A source of the size error is upstream, in the official radius forecasts (exploratory).** At hour 0, as-issued and best-track sizes agreed (log ratio -0.004 for medium and large storms), so post-season revision does not explain the size effect. But for large storms, the best-track 34-kt size was 6%, 8% and 10% larger than the official forecast at 24, 48 and 72 h (72 h interval 6-14%). For small storms it was 3% smaller at 48 h, and 12-15% of positive small-storm forecasts had no 34-kt winds in the best track. A 10% radius deficit removes about 20% of the wind area. This accounts for part, not all, of the 31% event excess in large storms.

4. **The pre-registered strength hypothesis was not supported.** We expected under-confident forecasts near hurricanes and over-confident forecasts near weaker systems, as in the campaign's track-circle result. Calibration slopes did not differ at 34 kt (hurricane minus weaker: +0.06, -0.05 to 0.16, product rule). At 64 kt the difference had the opposite sign (-0.10, -0.18 to -0.02). Hurricanes did have higher O/E (+0.29, 0.19-0.38 at 34 kt), but this follows size: hurricanes are large.

5. **The 2026 product is different (unannounced change found).** In 2010-2025, 94-98% of grid points inside 0.85 of the as-issued 34-kt radius had WSP of at least 99% at hour 0. In 2026 the share was 70%, and 26% for storms of 40 kt or less. The 50% edge stayed at 0.87, but the 90% edge moved in to 0.79. This is consistent with added initial-condition spread. We did not find this change in the NHC "2026 new products and services" document. 2026 calibration slopes were 1.12-1.26 (all conventions), against 0.83-1.06 in 2010-2025: the 2026 probabilities are now too flat rather than too sharp at 34 kt.

6. **Recalibration by strength and size helps on later years, but not on the changed 2026 product with the product rule.** Logistic recalibration in eight strength-by-size groups, fitted on 2010-2021, reduced the 2022-2025 Brier score by 4.4% (0.7-7.5), 5.1% (1.4-7.8) and 1.9% (0.1-3.2) for 34, 50 and 64 kt (product rule), and by 10.0%, 10.0% and 4.2% (quadrant rule). A single pooled recalibration gave no gain under the product rule (-0.8%). Refitted on 2010-2025 and applied to 2026, the group recalibration made 34-kt forecasts worse under the product rule (-2.8%, -5.9 to -0.1), as expected after a product change.

Figure 1 (`files/figures/reliability.png`) shows the reliability curves. Figure 2 (`files/figures/hour0_radius.png`) shows the hour-0 test. Figure 3 (`files/figures/conditional.png`) shows the size result, the official radius bias and the holdouts.

## Question and prior work

The selected campaign work found specific miscalibration in public hazard products (PAGER, aftershock forecasts, ShakeMap, ShakeAlert, NHC error circles, SWPC storm, proton and electron forecasts, PTWC threat levels). The NHC circle study (SCI d0ccb210) found over-coverage near hurricanes and under-coverage near weaker storms. The WSP is the NHC product that turns track, intensity and size uncertainty into point probabilities. It is used for watches, warnings and emergency decisions. A campaign search ("wind speed probabilities", "tropical storm force wind probability", "HURDAT2 wind radii") found no WSP verification. The open questions were: is the WSP calibrated in 2010-2026, does the circle result carry over, and what physical or algorithmic sources explain any error?

DeMaria et al. (2009, doi:10.1175/2009WAF2222286.1) described the Monte Carlo WSP model (1,000 realizations from five-year error statistics, radii-CLIPER wind radii, 0.85 radius factor) and verified 2006-2007 against best tracks with the same 0.85 factor. They found small biases (within 15%, except a high bias in the eastern Pacific) and good reliability. DeMaria et al. (2013, doi:10.1175/WAF-D-12-00116.1) added case-by-case track spread (GPCE) and verified 2008-2011. Our new contributions are: a 16-year independent verification with 2026 out-of-sample data; the demonstration that the verdict depends on the radius convention; a pre-registered storm-size result that holds in all conventions; a link from the size error to the official radius forecasts; and detection of a 2026 change in the hour-0 field.

## Data

- **WSP grids:** NHC GIS archive, `https://www.nhc.noaa.gov/gis/forecast/archive/YYYYMMDDHH_wsp_120hrhalfDeg.zip`, all 9,119 files for 2010-2026 (field PWIND120, percent, points of at least 0.1%). File names and SHA-256 values are in `files/provenance/wsp_files_sha256.csv`. Points absent from a file are 0%. A file with an absent 50- or 64-kt layer is read as all 0% for that layer (91 of 9,119 files).
- **Official forecasts:** ATCF a-decks (OFCL lines) and b-decks from `https://ftp.nhc.noaa.gov/atcf/archive/YYYY/` (2010-2025) and the 2026 operational `aid_public/` and `btk/` folders. Hashes are in `files/provenance/atcf_files_sha256.csv`.
- **Best tracks:** HURDAT2 Atlantic 1851-2025 (shared copy `nhc-hurdat2-atl-1851-2025-092326`, SHA-256 `75202780...`) and NE/Central Pacific 1949-2025 (`nhc-hurdat2-nepac-1949-2025-092926`, SHA-256 `caece626...`; added to the shared store by this job). The 2026 truth is the operational b-deck (not reanalysed).
- **NHC OFCL error files** (shared copies used by SCI d0ccb210) define the original-plan active-storm rule (check "Qplan").

`files/sources.json` lists the exact paths, URLs and hashes. All sources are US Government works (NOAA/NWS/NHC). See `files/NOTICE.md`.

## Method

The plan (`files/plan.md`) was written before any forecast was compared with an outcome. Amendments A1-A4 were added after an hour-0 consistency check and before any outcome comparison for future points. They are dated and explained in the plan.

- **Event.** A grid point has the event if it is inside the best-track wind area of a storm that had an official forecast at the WSP time t0 (amendment A1), at any hour from t0 to t0+120 h. Best-track centres and radii are linearly interpolated to 1-h steps. We use three area rules: **Q** fills each geographic quadrant to its radius (plan, primary); **S** interpolates the radius in azimuth between quadrant mid-angles; **P** uses 0.86 times S. The factor 0.86 is the hour-0 50% edge of the WSP fields measured on 2010-2017 issue times (0.860, 0.858 and 0.857 for 34, 50 and 64 kt).
- **Sample.** Points with WSP above 0 or with an event, in 0-60 N, 180-0 W. Points already inside a wind area at t0 are removed (same rule as the event), so only the forecast part is scored. Each point is attributed to the nearest active storm at t0. Strength (64 kt) and size (34-kt mean of non-zero quadrant radii; 0, and terciles 57.5 and 90 n mi) come from the best track at t0 (pre-registered) and from the as-issued tau-0 forecast (secondary).
- **Scores.** O/E = events / sum of probabilities. Calibration slope and intercept come from logistic regression of the event on logit(p) (p clipped to 0.001-0.999), fitted on 200 logit bins per storm and group. Brier score.
- **Uncertainty.** 1,000 storm-cluster bootstrap draws (all records of a storm together). Intervals are pointwise 95% percentile intervals.
- **Holdouts.** Group recalibration (logistic, eight strength-by-size groups) fitted on 2010-2021 and scored on 2022-2025; refitted on 2010-2025 and scored on 2026. The recalibrated value is constant inside each logit bin (bin width 0.07).
- **Exploratory checks (after the main results):** O/E by size inside strength classes; official versus best-track 34-kt size at 0, 24, 48 and 72 h by initial size group.

## Results tables

| 2010-2025, all storms | 34 kt O/E | 50 kt O/E | 64 kt O/E | 34 kt slope |
|---|---|---|---|---|
| Q quadrant maximum (plan) | 1.33 (1.23-1.41) | 1.46 (1.33-1.59) | 1.30 (1.16-1.44) | 0.83 (0.75-0.91) |
| S azimuth-interpolated | 1.24 (1.15-1.33) | 1.37 (1.25-1.50) | 1.21 (1.09-1.34) | 0.86 (0.77-0.94) |
| P product rule (0.86) | 1.04 (0.96-1.12) | 1.16 (1.05-1.25) | 1.02 (0.92-1.13) | 0.88 (0.80-0.96) |
| Q, plan active-storm rule | 1.29 (1.20-1.37) | 1.43 (1.31-1.55) | 1.29 (1.15-1.42) | 0.80 (0.72-0.88) |
| 2026, Q (operational truth) | 1.46 (1.33-1.57) | 1.35 (1.17-1.47) | 1.20 (1.03-1.30) | 1.12 (0.99-1.25) |
| 2026, P | 1.14 (1.02-1.22) | 1.07 (0.92-1.17) | 0.98 (0.84-1.07) | 1.23 (1.06-1.42) |

| 34 kt O/E by initial size (P rule) | no 34-kt radii | small | medium | large |
|---|---|---|---|---|
| all storms | 0.79 (0.71-0.88) | 0.73 (0.66-0.82) | 0.87 (0.79-0.95) | 1.31 (1.21-1.41) |
| initial wind below 64 kt | 0.79 (0.70-0.87) | 0.73 (0.66-0.81) | 0.89 (0.79-1.02) | 1.13 (1.01-1.27) |
| initial wind 64 kt or more | - | 0.75 (0.54-1.02) | 0.84 (0.76-0.92) | 1.40 (1.29-1.52) |

The period contrast (2018-2025 minus 2010-2017) was small and uncertain: +0.11 (-0.05 to 0.26) for 34 kt, P rule. The lowest probability bin (below 0.5%) had observed frequencies of 1.4% (34 kt, P rule) against a mean forecast of 0.16%. Thus, far-field misses are about nine times more frequent than stated, though their absolute rate is small. Including storms that formed after t0 (check "Qany") raised 34-kt O/E to 1.74. The WSP is not designed to forecast those storms.

All values are in `files/tables/calibration.csv`, `reliability.csv`, `recalibration.csv`, `oe_strength_by_size.csv`, `ofcl_radius_bias.csv`, `hour0_by_year.csv` and `hour0_profiles.csv`.

## Limits

- **The truth is a model.** Best-track radii are analyses with errors often of 25% or more, and they give only a maximum per quadrant. No observation network gives the true 34-kt area. We bracket the result with three area rules but cannot tell which rule is physically right. The size result and the 2026 change do not depend on this choice. The overall calibration verdict does.
- The truth for 2026 is the operational b-deck. NHC can revise it after the season.
- Covariates use the best track or the tau-0 forecast. Both are at t0, but the best track is not available in real time. As-issued covariates gave the same size result.
- Grid points of one issue time and successive issue times are strongly dependent. The storm bootstrap allows any dependence inside a storm. It does not allow for dependence between storms of the same season.
- Six potential cyclones that never became tropical cyclones (32 issue times) have no best track. Their WSP values count as forecasts without events.
- The half-degree grid is 0.5 degree (about 30 n mi). Points at the edge of small storms are coarse.
- The radius check uses the official 34-kt radii. The WSP model uses radii-CLIPER after the official radii end. We did not rerun the WSP model, so we cannot divide the size error exactly between the official radii and the model.
- The 2026 change is inferred from the files. We have no NHC description of it.
- We did not test incremental (6-h) probabilities, text-product locations or the western Pacific (JTWC) part of the grids.

## Reproduction

1. `bash files/code/retrieve.sh /path/to/scratch` downloads all inputs into scratch (about 1.3 GB: 713 MB of WSP files and 575 MB of ATCF files). On hosts with a broken IPv6 route, set `PYTHONPATH` to a folder with an IPv4-only `sitecustomize.py`.
2. Set `DATASETS` to the folder with the HURDAT2 and error files (paths as in `files/sources.json`), then run `RAW=/path/to/scratch bash files/code/run_all.sh` from `files/code/`. The steps are: `parse_wsp.py`, `initial_field.py`, `build_records.py`, `hour0.py`, `aggregate.py`, `analyze.py`, `mechanism.py`, `figures.py`. The full run took about 2.5 h on a shared 8-core host.
3. `python files/code/check_results.py files` recomputes the pooled O/E and slopes for rules Q and P from the bundled aggregate tables (`files/agg/`) and compares them with `calibration.csv`.

Environment: Python 3.12.15, numpy 2.5.4, pandas 3.1.1, pyarrow 26.0.1, matplotlib 3.11.2. Bootstrap seed 20261110 (mechanism checks: 7).

## Provenance

Job sci-1107-hp-earth-and-ocean-sciences-1b384bbce361, campaign 11_07_2026, topic earth-and-ocean-sciences, machine hp, model Claude Opus 5.5 (claude-opus-5-5), account claude-olen. Data retrieved 2026-11-10. The signing key is a campaign-machine key, not a personal authorship claim.
