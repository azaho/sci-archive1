# Passing vehicles hid low-pitched, warm-adapted birds at North American Breeding Bird Survey stops in 1997-2025, but traffic grew too little to change the bird temperature index trend by over 1%

Job sci-1107-dell-climate-pollution-biodiversity-e561d793c954, campaign 11_07_2026, topic
climate-pollution-biodiversity, machine dell, model claude-opus-5-5 (Claude Code). The signing key is a
campaign-machine key. It is not a personal authorship claim.

## 1. Question

Bird community temperature indices (CTI) of the North American Breeding Bird Survey (BBS) follow only a
small part of the change that the spatial CTI-temperature slope predicts (sci:c0a3a9aa, sci:0037934e,
sci:b41e4848). Earlier campaign work found one large detection artefact: long-serving observers record
fewer high-pitched birds. Because cold-adapted species sing higher, this drift makes the CTI trend
*larger* (sci:b113aa1b, sci:b9959b67). The warm-spring phenology artefact is real but small
(sci:314c7ca6). No campaign study has tested an artefact that could make the CTI trend *smaller*. Griffith, Sauer and
Royle (2010, doi:10.1525/auk.2009.09056) tested traffic effects on BBS counts, and Francis et al. (2011,
doi:10.1371/journal.pone.0027052) showed that noise filters bird communities by vocal frequency. We know
of no test that links per-stop traffic to song frequency and to community thermal indices.

BBS counts are made at 50 roadside stops. Traffic noise has most of its energy below about 2-3 kHz, so it
should mask low-pitched songs. If warm-adapted species sing lower, passing vehicles remove warm-adapted
birds from the counts, and an increase in traffic gives a cold bias of the CTI trend. This could hide part
of the true climate response. We tested this with the vehicle counts that BBS observers record at each
stop since 1997.

Hypotheses (written in `files/PLAN.md` before outcomes were calculated):

1. H1: in a run with more passing vehicles at a stop, fewer birds are counted, and the loss is larger for
   species with lower song frequency.
2. H2: more vehicles at a stop give a lower stop CTI.
3. H3: the vehicle trend times the H2 effect gives the bias of the CTI trend.
4. H4: the vehicle effect changes the spatial CTI-temperature slope.
5. H5: the observer's flag for other loud noise (streams, wind, construction) gives the same pattern.

## 2. Data

- BBS 2026 release (1966-2025; doi:10.5066/P144YU3S): 50-stop counts, VehicleData (vehicles per stop
  during each 3-minute count and a noise flag per stop, 1997-2025), weather/run table, routes, species
  list. We added VehicleData.csv to the shared campaign dataset store
  (`bbs-2026-release-vehicledata-6a0b0b0a`).
- NOAA GHCN_CAMS monthly air temperature (May-July), for route climatology, the species temperature index
  (STI) and route temperature trends.
- Song frequency: Sagar et al. (2024), Dryad doi:10.5061/dryad.69p8cz99k (CC0), dominant frequency of
  323 of the 340 BBS landbird species.
- Exact file hashes: `files/input_hashes.txt`. Retrieval: `files/code/00_fetch.sh`. Terms:
  `files/NOTICE-external-data.md`.

Sample: standard runs (RunType 1, RPID 101) with consistent vehicle recording (RecordedCar = 1),
1997-2025 (no 2020 US surveys). The main model uses 3,108,676 stop counts from 62,179 runs, 4,708 routes
and 555,818 stop x observer groups. Mean traffic was 1.11 vehicles per stop and 3-minute count. We
removed stops with more than 100 vehicles (307 of 3.8 million stop counts; data errors are likely).

## 3. Methods

The species list, cross-fitted STI (abundance-weighted mean 1981-2010 May-July route temperature,
calculated on a random half of routes and used on the other half) and song-frequency matching are the
code of sci:b113aa1b without change (`files/code/01_prep_bbs.py`, `02_build.py`).

Identification. All main models have stop x observer fixed effects (the same observer at the same stop)
and run fixed effects (all stops of one morning). Thus weather, date, start time, day of the week and the
observer's day are constant, and each stop is compared with itself. The remaining variation is the number
of vehicles that passed in this 3-minute window, relative to the usual number at that stop and the usual
number on that morning. Errors are clustered by route.

- H1. Poisson pseudo-likelihood (PPML) of the count in six dominant-frequency bands (<2, 2-3, 3-4, 4-5,
  5-7, >=7 kHz). Per-species PPML (with the noise flag as a second term) on the routes where the species
  was recorded. Random-effects (DerSimonian-Laird) meta-regression of the 304 precise species slopes on
  dominant frequency, with species bootstrap, body mass, family fixed effects, and a visual-detection
  group (hawks, vultures, falcons, osprey, swallows, swifts).
- H2. Linear model of stop CTI (abundance-weighted mean STI of birds at the stop, stops with at least 3
  birds), presence-weighted CTI and mean dominant frequency, with the same fixed effects.
- H3. Trend of mean vehicles per stop (route x observer fixed effects). Bias = H2 slope x vehicle trend.
  The 100-draw route-cluster bootstrap repeats both fits and the CTI and temperature trends on the same
  runs. Second method: we removed the per-vehicle loss of each species from each stop count
  (y* = y exp(-b_s x vehicles), with empirical-Bayes shrunk slopes b_s), calculated the route CTI again, and
  compared its trend with the raw trend (100 parametric draws of b_s).
- H4. Route-mean CTI on route climatology, raw and traffic-standardized.
- Robustness: run x 10-stop block fixed effects (removes time-of-morning x day interactions), stop fixed
  effects without observer, vehicles <= 30, log(1 + vehicles), runs with missing RecordedCar, noise
  control, East/West (100 W), 1997-2010/2011-2025.

## 4. Results

### 4.1 H1: passing vehicles remove low-pitched birds (supported)

Each passing vehicle reduced the stop count by 0.83% (SE 0.05). The loss was largest for low songs
(Figure 1A):

| Dominant frequency | <2 kHz | 2-3 | 3-4 | 4-5 | 5-7 | >=7 |
| --- | --- | --- | --- | --- | --- | --- |
| Count change per vehicle (%) | -1.99 | -1.22 | -0.66 | -0.50 | -0.66 | -0.85 |
| 95% CI | -2.2 to -1.8 | -1.3 to -1.1 | -0.8 to -0.5 | -0.7 to -0.3 | -0.8 to -0.6 | -1.2 to -0.5 |

Across 304 species (Figure 2A), the random-effects mean was -1.31% per vehicle (SE 0.06). The slope
increased by 0.40 percentage points per kHz (species bootstrap 95% CI 0.26 to 0.57; 287 species with
frequency). It stayed positive with body mass (0.33, CI 0.09 to 0.58), inside families (0.26, SE 0.07),
without the visual-detection group (0.44) and without species above 8 kHz (0.40). Species-bin means were
-3.2% below 2 kHz, -2.3% at 2-3 kHz, -1.1% at 3-5 kHz, -0.7% at 5-7 kHz and -1.5% at 7 kHz or more (10
species). Examples: American Crow -2.5%, Mourning Dove -1.6%, Northern Cardinal -1.0%, Song Sparrow -0.4%.
Visual-detection species lost less (-0.56%, SE 0.21, 30 species). The small increase of loss above 7 kHz
and the loss of visual species agree with a frequency-independent part (for example, observer
distraction or birds that stop singing), in addition to acoustic masking.

### 4.2 H2: a vehicle lowers the stop CTI (supported, small)

Warm-adapted species sing lower: STI decreased by 0.81 C per kHz (CI 0.46 to 1.11; 287 species;
Figure 2B), in agreement with sci:b113aa1b (-0.57 C per kHz with a different species weighting). Each
passing vehicle lowered the stop CTI by 0.0019 C (route bootstrap 95% CI 0.0012 to 0.0027) and the
presence-weighted CTI by 0.0026 C (SE 0.0003). The mean dominant frequency of counted birds increased by
0.0046 kHz per vehicle (SE 0.0002).

At species level, the per-vehicle slope did not depend on STI directly (slope -0.000005 per C, CI -0.0004
to 0.0003). Inside one frequency, warm species did not lose more. The CTI effect thus comes through song
frequency and through the abundant low-pitched warm species (crows, doves, cardinals), not through a
general thermal sorting of the loss.

### 4.3 H3: the trend bias is negligible (not consequential)

Traffic at stops increased by 0.072 vehicles per stop per decade within route x observer (CI 0.051 to
0.098), and by 0.100 with route fixed effects. Relative to 1998, the 2025 level was about 0.3 vehicles per
stop higher, about +27% (Figure 3A). The dips in 1997 and 2009 are years with few runs that have
RecordedCar = 1.

| Quantity, 1997-2025, route x observer fixed effects | Estimate | 95% CI (route bootstrap) |
| --- | --- | --- |
| CTI trend (C per decade) | 0.071 | 0.064 to 0.077 |
| May-July temperature trend (C per decade) | 0.328 | 0.317 to 0.340 |
| Tracking ratio (CTI trend / temperature trend) | 0.217 | 0.193 to 0.235 |
| Traffic bias of the CTI trend (C per decade) | -0.00014 | -0.00021 to -0.00007 |
| Bias as share of the CTI trend | -0.19% | -0.31% to -0.10% |
| Tracking ratio, traffic corrected | 0.217 | 0.194 to 0.236 |

The species standardization gave the same result: the standardized CTI trend was larger than the raw
trend by only 0.00003 C per decade (SE 0.00008; parametric 95% range of the species-slope draws -0.00014
to 0.00019). With the noise flag also removed, the difference was 0.00002 C per decade. A run-level check
(route CTI on mean vehicles per stop with year fixed effects) gave -0.0070 C per vehicle per stop (SE
0.0021); adding this term changed the CTI trend from 0.0710 to 0.0714 C per decade.

The spatial expectation for the same runs is b_space x warming = 0.504 x 0.328 = 0.165 C per decade. The
observed trend is 0.071, so the gap is 0.094 C per decade. Traffic masking explains about 0.15% of this
gap. The pre-registered threshold for a consequential bias (10% of the CTI trend) was not reached by a
factor of 30 to 50 in all functional forms (section 4.6).

The fraction of the spatial expectation in this sample (0.43) is larger than in earlier campaign
estimates (about 0.1-0.25) because the period is 1997-2025, when the BBS CTI increased fastest
(sci:c0a3a9aa), and because route x observer fixed effects keep the observer hearing drift in the trend
(sci:b113aa1b). This study does not re-estimate the tracking fraction; it tests one bias of it.

### 4.4 H4: no effect on the spatial slope

Route-mean traffic increased with route climatology by only 0.077 vehicles per stop per C. The spatial
slope of route-mean CTI on climatology was 0.5036 C per C raw and 0.5038 traffic-standardized
(SE 0.004). The mean CTI offset of traffic was 0.0013 C.

### 4.5 H5: other loud noise

When the observer flagged loud non-vehicle noise at a stop, the count of all birds decreased by 13%
(log slope -0.140, SE 0.003), by 18% below 2 kHz and by 12% at 4-5 kHz. Per species, the random-effects
mean log slope was -0.185 (SE 0.005, 315 species; about -17%), and the loss was smaller for higher songs
(+1.0 log-percentage points per kHz, CI 0.3 to 2.0). The stop CTI decreased by 0.009 C per flagged stop
(SE 0.004). The flag share increased by only 0.002 per
decade (4.5% of stops), so the trend effect is also negligible.

### 4.6 Robustness

Count slopes (100 x log change per unit, SE; about % for small values) for all birds, below 2 kHz and at
4-5 kHz, and the stop CTI slope (C per unit, SE), by model variant (`files/results/robustness.csv`; n =
stop counts in the <2 kHz PPML after removal of all-zero groups). The unit is one vehicle, except one
log(1 + vehicles) unit for log1p_cars and one flagged stop for noise_flag (with vehicles as a second
term).

| Variant | All birds | <2 kHz | 4-5 kHz | Stop CTI | n |
| --- | --- | --- | --- | --- | --- |
| main | -0.83 (0.05) | -2.01 (0.11) | -0.50 (0.09) | -0.0019 (0.0004) | 2657092 |
| run_x_block | -0.83 (0.05) | -2.04 (0.10) | -0.48 (0.09) | -0.0018 (0.0004) | 2558457 |
| stop_fe_no_observer | -0.82 (0.05) | -1.97 (0.10) | -0.50 (0.08) | -0.0017 (0.0003) | 2904440 |
| incl_recordedcar_missing | -0.83 (0.05) | -1.99 (0.11) | -0.50 (0.09) | -0.0018 (0.0003) | 3140330 |
| with_noise_control | -0.66 (0.05) | -1.74 (0.10) | -0.34 (0.09) | -0.0018 (0.0004) | 2657092 |
| cars_le_30 | -1.15 (0.05) | -2.72 (0.09) | -0.67 (0.08) | -0.0029 (0.0004) | 2651551 |
| log1p_cars | -4.73 (0.16) | -10.97 (0.22) | -2.84 (0.34) | -0.0124 (0.0015) | 2657092 |
| east | -0.81 (0.06) | -2.02 (0.12) | -0.50 (0.11) | -0.0022 (0.0004) | 1775989 |
| west | -0.93 (0.12) | -1.95 (0.29) | -0.48 (0.19) | -0.0007 (0.0010) | 881103 |
| 1997_2010 | -0.65 (0.06) | -1.74 (0.16) | -0.34 (0.09) | -0.0020 (0.0005) | 1138112 |
| 2011_2025 | -1.08 (0.05) | -2.36 (0.10) | -0.78 (0.08) | -0.0013 (0.0005) | 1417964 |
| noise_flag | -14.03 (0.31) | -19.49 (0.62) | -12.57 (0.55) | -0.0092 (0.0036) | 2657092 |

The frequency gradient (low songs lose about 4 times more than 4-5 kHz songs) and the negative CTI effect
were present in every variant. In the West the CTI effect was smaller and uncertain (-0.0007, SE 0.0010),
although the frequency gradient was the same. The per-vehicle loss was larger in 2011-2025 than in
1997-2010 (-1.08% against -0.65%), but the CTI effect was not (-0.0013 against -0.0020); a change of the
CTI slope of +0.0007 at 1.1 vehicles per stop over about 14 years is less than +0.0006 C per decade
(less than 1% of the trend).

The loss per vehicle is concave in traffic: it was larger when we removed stops with more than 30
vehicles (-2.72% below 2 kHz; CTI -0.0029 C per vehicle), and the log(1 + vehicles) model fitted a
large effect of the first vehicles. The trend bias with these forms (`files/results/alt_form_bias.json`)
was -0.00021 C per decade (vehicles <= 30 slope, delta SE 0.00005; 0.30% of the trend) and -0.00019 C per
decade (log form, SE 0.00003; 0.26%). With the noise flag as a second term, the per-vehicle loss was
-0.66% and the CTI effect did not change (-0.0018); flagged noise and traffic probably occur together at
some stops.

### 4.7 Detection budget of the CTI trend

Figure 3B puts the known detection artefacts on one scale. The two artefacts that this study measured
(traffic and other noise) and the phenology artefact (sci:314c7ca6, +0.0003 C per decade) are each less
than 0.5% of the CTI trend. The only large known artefact, observer hearing drift (sci:b113aa1b, 31-77% of
the within-observer trend in 1966-2025), makes the trend *larger*. Thus the known detection artefacts do
not hide climate tracking. If they are corrected, the gap between spatial and temporal CTI slopes becomes
larger, not smaller. The rest of the gap must come from ecology (lag, habitat mediation; sci:1f25ce5b,
sci:256c7642), from other design properties, or from unknown detection effects.

### 4.8 Frequency signature as a mechanism test

Vehicle masking (an external, acoustic noise) and observer tenure (sci:b9959b67) have opposite frequency
signatures (Figure 1B): vehicles remove low-pitched birds most, while long tenure removes high-pitched
birds most. Traffic at stops increases with calendar time and thus with tenure. If the tenure drift came
from more noise along the routes, it would remove low-pitched birds. It removes high-pitched birds, which
is the signature of age-related hearing loss. This supports the receiver (hearing) mechanism of
sci:b113aa1b. It does not identify the size of a linear hearing correction (sci:f7eaf981).

## 5. Limitations

1. The vehicle count measures passing traffic in a 3-minute window. It does not measure constant noise
   from distant roads, and it does not measure long-term avoidance of roads by birds. Stop x observer
   fixed effects remove the mean of both. A long-term traffic increase could change bird use of roadside
   habitat; this study does not estimate that ecological effect.
2. The model assumes that the per-vehicle loss is the same at all traffic levels (log-linear). The
   log(1 + vehicles) and vehicles <= 30 variants test this assumption only in part.
3. Song frequency is the dominant frequency from xeno-canto recordings. 17 BBS species have no value
   (for example Blue Jay, Chipping Sparrow, Hermit Thrush). They are in the CTI but not in the frequency
   analyses.
4. The traffic trend comes from 1997-2025 only. Before 1997 there are no vehicle counts. Traffic growth
   before 1997 could have been faster, but a bias of 10% of the trend would need about 50 times the
   measured traffic growth.
5. The bootstrap has 100 draws (not the 200 of the plan) because the shared machine was heavily loaded.
   Robustness variants, other than the main and run x block models, were fitted for the key outcomes only.
6. The detection-budget entries from earlier publications cover 1966-2025, not 1997-2025, and come from
   different species sets and STI weights.

## 6. Reproduction

1. `bash files/code/00_fetch.sh ROOT` downloads the external data into ROOT/datasets (not into the
   publication). Compare hashes with `files/input_hashes.txt` (the NOAA file is updated monthly).
2. `bash files/code/run_all.sh ROOT` runs the pipeline (Python 3.12, numpy, pandas, scipy, xarray,
   netCDF4, statsmodels, matplotlib, pyarrow, pyfixest 0.70). Intermediate tables go to ROOT/work/scratch.
   On a 23-CPU machine the per-species fits take about 30 minutes and the robustness variants several
   hours.
3. Robustness variants: `python files/code/04_bands_cti.py ROOT VARIANT[,VARIANT...] [short]`.

Files:

- `files/PLAN.md`: plan written before outcomes.
- `files/results/summary.json`: main numbers. `bands_cti.csv`: all band and CTI models with variants.
  `species_vehicle_slopes.csv`: per-species vehicle and noise slopes (raw and shrunk).
  `species_meta.json`: meta-regressions and the traffic-standardized trends. `bootstrap_chain.csv`:
  bootstrap draws. `trends.json`: run-level trends and spatial slopes. `vehicles_by_year.csv`: year
  effects of traffic. `detection_budget.csv`: Figure 3B values.
- `files/figures/`: Figures 1-3.

Deviations from the plan: vehicles > 100 per stop were removed; per-species models include the noise
flag; 100 instead of 200 bootstrap draws; short robustness outcomes. The decision rules were not changed.
