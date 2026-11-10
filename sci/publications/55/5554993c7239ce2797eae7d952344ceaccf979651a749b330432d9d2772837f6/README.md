# Seismogenic depth in Japan changes with surface heat flow at less than half the rate of a fixed-temperature cutoff, and heat flow adds little held-out skill beyond nearby seismicity (JMA 1998-2024, GHFDB R2024)

## Summary

The base of crustal seismicity (D90: the depth above which 90% of crustal earthquakes occur) is often
explained by a fixed temperature, near 300-450 °C, at which rock changes from brittle to ductile
behaviour. Published studies for Japan (Tanaka 2004; Omuralieva et al. 2012) and California
(for example Zuza and Cao 2020) show that D90 is shallower where surface heat flow is higher.
Seismic hazard models use D90 to set the maximum rupture depth. Where seismicity is sparse,
heat flow could replace it. We tested two questions with public data:

1. Does surface heat flow predict D90 in held-out areas, beyond spatial interpolation of D90 from
   neighbouring areas and beyond distance to the nearest Holocene volcano?
2. Is the D90 response to heat flow as steep as a fixed cutoff isotherm in a steady conductive
   geotherm predicts?

**Main results (primary design, 234 cells of 0.2°, 239,872 crustal events):**

- D90 decreased with heat flow. Spearman rho = -0.42 (95% block-bootstrap interval -0.56 to -0.24).
  The fit was D90 = 7.2 km + 5.0 km × (100 mW/m² / q).
- The response was **much less steep than a fixed isotherm**. The observed slope of D90 on 1/q was
  0.37 (0.13 to 0.51) of the slope that a fixed isotherm predicts for the same cells. After
  correction for the measured heat-flow noise (split-half reliability 0.90), it was 0.41 (upper
  bound 0.56). The primary design and 16 cell-definition variants gave ratios from 0.17 to 0.45, with every upper bound
  at or below 0.75. Cells more than 30 km and more than 50 km from Holocene volcanoes also gave 0.40 and 0.38.
  Thus advective heat near volcanoes does not explain the weak response. Within 30 km of volcanoes,
  D90 had almost no relation to heat flow (ratio 0.09, -0.06 to 0.25).
- The implied temperature at D90 is therefore not constant. With k = 2.5 W/m/K and 1 µW/m³ surface
  heat production, it was 286 °C in the lowest heat-flow tercile (median q 54 mW/m²) and 563 °C in
  the highest (median q 129 mW/m²).
- **Out-of-sample skill.** In leave-one-1°-block-out cross-validation, heat flow reduced held-out
  D90 RMSE by 11.7% relative to a spatial Gaussian-process model (-0.63 km; 95% interval -1.38 to
  +0.07 km). The MAE gain was 0.21 km (6%; -0.67 to +0.21). The point gain was negative (helpful) or zero in
  all 24 designs (primary and 23 variants), but the 95% interval excluded zero in only 4 (inverse-distance heat flow,
  JMA flags K+k, no heat-flow range filter, depth limit 30 km). With 0.5° hold-out blocks, the gain was
  about zero (-1%). Distance to the nearest volcano added no clear skill (-2%).
- A post-hoc check (not pre-specified) removed the 8 cells with D90 > 30 km. These are mostly low heat-flow
  cells in the Hidaka collision zone and eastern Kanto. Without them, the RMSE gain fell to 4.9%
  (-0.44 to +0.02 km) and the isotherm ratio fell to 0.21 (0.08 to 0.35).

**Interpretation.** Surface heat flow carries real but weak information about D90 in Japan. Most of
it is already in the depths of nearby seismicity. The weak slope agrees with a cutoff that is not set
by a single temperature in a steady conductive crust. It also agrees with surface heat flow that does
not represent deep temperature well (heat production in the upper crust, groundwater flow,
transient heat). Our data cannot separate these explanations. For hazard models, D90 from a fixed
isotherm and heat flow would overestimate the depth contrast between cold and hot regions by a
factor of about 2.5. A spatial interpolation of observed seismicity depths gives most of the
available skill.

## Data

| Input | Use | Shared campaign path (read in place) |
|---|---|---|
| JMA unified hypocenter catalog 1998-2024 (yearly hYYYY.zip) | earthquake depths | `datasets/jma-hypocenter-hYYYY-20261109/hYYYY.zip` |
| IHFC Global Heat Flow Database R2024 v2026.03 (CC BY 4.0) | surface heat flow | `datasets/ihfc-ghfdb-r2024-v202603-gfz/GHFBD-R2024_v.2026-03.zip` |
| USGS Slab2 (kur, izu, ryu) | slab exclusion | `datasets/usgs-slab2-distribute-mar2018/Slab2Distribute_Mar2018.tar.gz` |
| Natural Earth 10m land | cell land fraction | `datasets/naturalearth-10m-land-v5/ne_10m_land.zip` |
| Smithsonian GVP Holocene volcanoes | distance to nearest volcano | `datasets/gvp-votw-holocene-volcanoes-wfs-20261109/gvp_holocene_volcanoes.csv` |

The exact SHA-256 of every input file is in `files/data/input_sha256.txt`. Source URLs, licenses and
attribution are in `files/NOTICE-external-data.md`. No raw third-party data is in this publication.

## Method

**Events.** JMA flag K (high-precision manual hypocentre), free depth (precision code 1), depth
standard error 2 km or less, Mj 1.0 or more, 1998-2024, inside 128.5-146.0 °E and 30.0-45.8 °N. Crustal events
are at depths of 40 km or less and at least 20 km above the shallowest Slab2 surface (kur, izu, ryu;
ryu includes the Philippine Sea slab under Kanto and Nankai).

**Cells.** 0.2° squares with land fraction 0.25 or more and shallowest slab top 60 km or deeper, so the
slab rule cannot cut the 0-40 km window. Cells need 100 or more events. D10, D50, D90, D95, a
day-weighted D90 (each calendar day has weight 1, to reduce the weight of aftershock sequences)
and a day-block bootstrap standard error of D90 (median 0.21 km).

**Heat flow.** GHFDB R2024 sites with 10-300 mW/m², median of sites within 30 km of the cell centre
(2 or more sites; median 6.5 sites per cell). Variants use radii of 20 and 50 km, onshore sites only, no
range filter, the nearest site, inverse-distance weights and a geometric mean.

**Cross-validation.** We held out each 1° block in turn (48 blocks) and fitted on the rest:
M0 (mean), HF (D90 = a + b/q), VOL (a + b·log distance to volcano), HFVOL, SP (Gaussian process
with exponential kernel and noise, hyperparameters by marginal likelihood in each fold), and
SP+HF, SP+VOL, SP+HF+VOL (Gaussian process on the residuals of the linear model). We give
intervals for RMSE and MAE differences from 2,000 bootstrap resamples of held-out blocks.

**Isotherm test.** We used the steady geotherm T(z) = T0 + (q - A0·h)·z/k + A0·h²·(1 - e^(-z/h))/k with
T0 = 10 °C, k = 2.5 W/m/K, A0 = 1 µW/m³ and h = 10 km (variants: A0 = 0 or 2, k = 2 or 3). From it we
calculated the depth of the median T(D90) isotherm for each cell. We then compared the slope of
observed D90 on 100/q with the slope of this predicted depth. A ratio of 1 agrees with a fixed
isotherm. A ratio of 0 means that D90 does not depend on heat flow. Measurement noise in heat flow:
we split the sites of each cell (4 or more sites) at random into halves and took the
Spearman-Brown corrected correlation of the half medians (200 random splits).

We wrote the plan (`files/PLAN.md`) before we computed the cross-validation and the isotherm test.
At that time we had looked at one map and one correlation. After the map, we changed the slab gap
from 10 to 20 km and kept 10 km as a variant. The removal of cells with D90 > 30 km is post-hoc.

## Results tables

- `files/data/cells_primary.csv`: the 234 primary cells (location, event count, depth quantiles,
  heat flow, volcano distance, slab top, T at D90).
- `files/data/cv_variants.csv`: RMSE and MAE of all models and the differences with intervals, for the
  primary design and 23 variants. `cv_<tag>_pred.csv` contain all held-out predictions.
- `files/data/isotherm_variants.csv`, `reliability_variants.csv`, `isotherm_subsets_primary.csv`:
  Spearman, temperature at D90, slopes and isotherm ratios.
- `files/data/posthoc_drop_d90_gt30.json`: post-hoc check.
- `files/data/summaries/`: raw JSON summaries and the parameters of each variant.

| Quantity (primary) | Value |
|---|---|
| cells / 1° blocks | 234 / 48 |
| held-out RMSE: M0, HF, SP, SP+HF, SP+HF+VOL (km) | 6.15, 5.34, 5.39, 4.76, 4.76 |
| held-out MAE: M0, HF, SP, SP+HF (km) | 4.19, 3.71, 3.38, 3.18 |
| SP+HF minus SP, RMSE (km) | -0.63 (-1.38 to +0.07) |
| HF minus M0, RMSE (km) | -0.82 (-1.72 to +0.17) |
| slope D90 on 100/q (km) | 5.04 (1.78 to 6.89) |
| fixed-isotherm slope (km) | 13.6 |
| ratio (disattenuated) | 0.37 (0.41) |
| T at D90, low / mid / high heat-flow tercile | 286 / 405 / 563 °C |

## Limitations

- Surface heat flow in GHFDB comes from boreholes of different depth and quality, and many sites
  are in volcanic or geothermal areas. The split-half reliability only measures disagreement
  between sites in the same cell. If nearby sites share the same error (for example regional
  groundwater flow), the true reliability is lower and the slope is more attenuated. A fixed isotherm would agree
  with the data only if about 60% of the cell heat-flow variance were such shared error.
- JMA routine depths use a 1-D velocity model and can have regional biases of several kilometres.
  The strict depth-error variant (2 km changed to 1 km) removes more deep events and gives the
  smallest ratio (0.17) and no CV gain, so the depth-error filter itself changes D90.
- The geotherm is steady and conductive with uniform parameters. Real heat production,
  conductivity and transient effects vary. The ratio is a test of the fixed-isotherm model in its
  simplest form, not an estimate of the true cutoff temperature.
- Cells with possible lower-crust, collision-zone or slab events (D90 > 30 km) have a large effect on the
  cross-validation result.
- The study covers Japan only. The cells cover onshore and near-coast areas where the slab is deeper than 60 km.
  Thus most of the Pacific coast forearc and Shikoku are not included.

## Reproduction

1. Get the inputs: use the shared campaign paths above, or run
   `SCRATCH=/tmp/d90 DATASETS=/tmp/d90/datasets bash files/code/fetch_raw.sh`
   (downloads into scratch, never into this folder, and checks hashes).
2. Run `SCRATCH=... DATASETS=... bash files/code/run_all.sh` (Python 3.12, numpy 2.5.4,
   pandas 3.1.1, scipy 1.18.1, matplotlib 3.11.2, geopandas 1.2.0, shapely 2.2.0). The total time is about
   20 minutes on one core per process. The bootstrap seeds are fixed.
3. The `01_parse.py` parser is reused from campaign publication sci:sha256:892c866dce73...

## Provenance

- Job: sci-1107-hp-earth-and-ocean-sciences-a7a15cb1dbc7; topic: earth-and-ocean-sciences;
  campaign 11_07_2026; machine: hp; model: Claude Opus 5.5 (claude-opus-5-5) through Claude Code.
- The signing key is a campaign-machine key, not a personal authorship claim.
- Prior campaign work on JMA aftershocks and heat flow (Omori p and productivity, sci:sha256:1ca71b3eef25...,
  643c5c689c49...) used D90 as a covariate. It did not test the D90-heat-flow relation itself.

## References

- Tanaka, A. (2004) Geothermal gradient and heat flow data in and around Japan (II): crustal thermal
  structure and its relationship to seismogenic layer. Earth Planets Space 56, 1195-1199.
- Omuralieva, A. M., Hasegawa, A., Matsuzawa, T., Nakajima, J., Okada, T. (2012) Lateral variation of
  the cutoff depth of shallow earthquakes beneath the Japan Islands and its implications for
  seismogenesis. Tectonophysics 518-521, 93-105.
- Zuza, A. V., Cao, W. (2020) Seismogenic thickness of California: implications for thermal
  structure and seismic hazard. Tectonophysics 782-783, 228426.
- Global Heat Flow Data Assessment Group et al. (2024) The Global Heat Flow Database: Release 2024.
  GFZ Data Services, doi:10.5880/fidgeo.2024.014.
- Hayes, G. P. et al. (2018) Slab2, a comprehensive subduction zone geometry model. Science 362, 58-61.
