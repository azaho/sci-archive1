# Community thermal composition in 75 monitoring networks followed about 12% of its own spatial temperature gradient in time; a lag fit gives fast adjustment to a small target (1948-2025)

Job: sci-1107-hp-climate-pollution-biodiversity-665642101897 (campaign 11_07_2026, topic
climate-pollution-biodiversity, machine hp, account claude-andrii). Model: Claude Opus 5.5
(claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Earlier campaign publications measured "tracking ratios" one system at a time. North American breeding
birds had a community temperature index (CTI) trend of 0.06 C per 1 C of warming (sci:sha256:c0a3a9aa...).
Bird centroids moved at 14% of the isotherm shift (sci:sha256:7714830c...). A campaign proof
(sci:sha256:0bc2a582...) showed that a raw CTI ratio is not a fraction of climate tracking: if all
species follow their niches, a frozen CTI changes only by the spatial CTI-temperature slope (0.33-0.44
for birds). Other systems used other methods, so the numbers do not compare directly.

We asked three questions with one estimator for many networks across realms and taxa:

1. Which fraction of its own spatial CTI-temperature gradient does a network follow in time
   (a) for year-to-year temperature anomalies ("fast") and (b) for the multi-year warming trend ("slow")?
2. Is the fraction larger for marine networks or ectotherms than for land networks or endotherms?
3. Is the weak trend response a lag? A lag model (partial adjustment) with one rate k predicts the
   slow response from the fast response. We test this prediction.

We wrote the plan (`files/PLAN.md`) before we calculated any network slope. Section 6 lists the
analyses that we added after the first results.

## 2. Data

- BioTIME 2.0 (Zenodo 15222193, 15 April 2025): all studies that had at least 8 climate grid boxes
  with at least 5 sampled years each, at least 10 sampled years and at least 10 taxa.
- Two external anchor networks with the same code: the North American Breeding Bird Survey (BBS,
  2026 release, standard runs, 1966-2025) and the UK Butterfly Monitoring Scheme (UKBMS site indices,
  1973-2024).
- Temperature: NOAA GHCN_CAMS 0.5 degree land air temperature for land and freshwater networks;
  HadISST1 1 degree SST for marine networks (main); NOAA OISST v2.1 0.25 degree SST (1983+, sensitivity).

After the screen, 76 networks remained. One network (study 68, a copepod survey) had a constant
presence composition at each site, so its slopes were zero with zero error. We removed it. The
analysis has 75 networks: 32 marine, 26 freshwater and 17 terrestrial; 56 ectotherm, 14 endotherm and
5 plant networks. They have 8,529 sites, 183,626 site-years and about 1.0 million samples, 1948-2025.
Median length is 24 sampled years. Median warming is 0.18 C per decade.

## 3. Method

- Site = climate grid box (0.5 degree on land and in fresh water, 1 degree at sea).
- T(site, year) = mean temperature of the 12 months that end in the study's median sampling month.
  Site climatology = mean T over the study years.
- Species temperature index (STI), cross-fitted: we split the sites into two halves, stratified by
  climatology. The STI of a taxon from half A is the prevalence-weighted mean climatology of the half-A
  sites. The CTI of a sample in half B is the mean STI (from half A) of the taxa in the sample. We used
  10 random splits and averaged the CTI. The STI never uses the site where the CTI is measured.
- Site-year CTI = mean of sample CTIs (presence weights).
- Spatial slope b_space: regression of site-mean CTI on site climatology, with a 2 degree block bootstrap.
- Temporal slopes: we divided each site's T into a linear site trend (tau) and an anomaly (a).
  CTI = site effect + beta_slow * tau + beta_fast * a, with two-way (site and year) cluster-robust errors.
- Fractions: phi_fast = beta_fast / b_space and phi_slow = beta_slow / b_space. A value of 1 means that
  the CTI changed in time as much as the spatial gradient predicts.
- Synthesis: DerSimonian-Laird random-effects means of b_space, beta_fast and beta_slow. The pooled
  fraction is the ratio of the random-effects means. Intervals come from 1,000 network bootstraps.
- Species-shuffle null: we permuted the STI values among taxa 200 times in each network. This null
  keeps the amount of species turnover but removes the link to thermal affinity.
- Lag emulator: for each network and 40 values of k (0.003 to 1 per year), we ran
  C_t = (1-k) C_(t-1) + k T_t on each site's full temperature record (from 1949 on land, 1900 at sea),
  and fitted the same panel model on the observed site-years. This gives the fast and slow fractions
  that a pure lag with full spatial equivalence produces.

## 4. Results

### 4.1 All networks follow a small fraction of their spatial gradient

The mean spatial slope was 0.18 C of CTI per 1 C of climatology (random-effects mean). The pooled fast
fraction was **0.020** (95% CI 0.005 to 0.039). The pooled slow fraction was **0.12** (0.02 to 0.28)
(Figure 1). In the 54 networks with a clearly positive spatial slope, the fractions were 0.034
(0.016 to 0.075) and 0.17 (0.05 to 0.43). The network medians were 0.046 and 0.13. Of these 54
networks, 76% had a slow fraction below 0.5 and 83% below 1.

| Variant | n | phi_fast (95% CI) | phi_slow (95% CI) |
| --- | --- | --- | --- |
| Main | 75 | 0.020 (0.005, 0.039) | 0.12 (0.02, 0.28) |
| Climatology SD >= 0.5 C | 67 | 0.025 (0.004, 0.057) | 0.19 (0.05, 0.42) |
| Spatial slope CI > 0 | 54 | 0.034 (0.016, 0.075) | 0.17 (0.05, 0.43) |
| log(1+abundance) weights | 75 | 0.021 (0.005, 0.040) | 0.12 (0.01, 0.27) |
| One STI split | 74 | 0.027 (0.011, 0.049) | 0.09 (0.00, 0.20) |
| OISST at sea, 1983+ | 71 | 0.020 (0.004, 0.035) | 0.02 (-0.08, 0.13) |
| Previous 12-month window | 70 | 0.017 (0.005, 0.029) | 0.09 (0.00, 0.22) |
| Richness and effort covariates | 75 | 0.022 (0.005, 0.044) | 0.09 (-0.01, 0.19) |

In all variants, the slow fraction was at most 0.19 and its upper limit was below 0.45.
The slow fraction did not change with the warming rate (Spearman rho = -0.06, p = 0.65) or with the
series length (rho = -0.03, p = 0.82). The fast and slow fractions had a weak positive rank
correlation (rho = 0.29, p = 0.03).

Anchor networks (fast / slow fraction): BBS 1966-2025, 3,146 boxes: b_space 0.449, phi_fast 0.044,
phi_slow 0.19. Swedish fixed-route birds: 0.036 / 0.19. UKBMS butterflies: -0.03 / 0.21. Northeast US
bottom trawl (NEFSC, 1948-2008): 0.43 / 1.4. East Coast North America trawl (ECNASAP, 1970-1995):
0.26 / 0.94. The BBS raw ratio (beta_slow = 0.087 C per C) is close to the earlier 0.061 (1970-2024). On the
spatial scale it is a fraction of about 0.19.

### 4.2 Groups

Terrestrial networks had a slow fraction of 0.18 (0.04 to 0.35). Freshwater networks had -0.06
(-0.20 to 0.05), and their fast fraction was 0.02 (-0.01 to 0.05). Marine networks had 0.37 (0.07 to
1.10) with HadISST, but -0.07 (-0.28 to 0.09) with OISST for 1983 and later. Thus the marine result
is not robust. A few US East Coast surveys (NEFSC, ECNASAP, EMAP) carry it. Endotherms (0.20, 0.02 to
0.43) and ectotherms (0.13, 0.01 to 0.32) did not differ clearly. The network medians differed
(ectotherm 0.20, endotherm -0.10, Mann-Whitney p = 0.04), but the random-effects ratio did not. We do
not give a robust difference between ectotherms and endotherms. Figure 3 shows all groups.

### 4.3 The weak trend response is not a long lag

- **Pure-lag test (planned).** For each network, we chose k so that the emulator gave the observed
  fast fraction. With this k, a pure lag predicted a median slow fraction of 0.54. The observed median
  was 0.15. The observed value was below the prediction in 65% of networks (Wilcoxon p = 0.013;
  Figure 2A). Warming started decades before most series. Thus a lag with the fast-response rate would
  have caught up with most of the trend.
- **Persistence.** With the previous-year anomaly in the model, the lag-1 coefficient was 0.61 of the
  lag-0 coefficient (networks with positive spatial slope; 0.81 for all networks). A partial adjustment
  gives a ratio of about 1 - k. This agrees with k of about 0.2 to 0.4 per year.
- **Two-parameter fit (added after first results).** We fitted one rate k and one equilibrium fraction
  theta to all 54 networks: C_t = (1-k) C_(t-1) + k theta b_space T_t. The best fit was **k = 0.26 per
  year** (95% network bootstrap 0.17 to 0.41; half-life 2.3 years) and **theta = 0.28** (0.12 to 0.54).
  When we removed one network at a time, theta was 0.18 to 0.31. The best pure-lag model (theta = 1)
  needed k = 0.011 per year and fitted worse (weighted squared error 325.6 against 287.4; Figure 2B).
  Group fits: terrestrial theta 0.16 (0.05 to 0.37), ectotherm 0.33 (0.09 to 0.67). The marine,
  freshwater and endotherm intervals were very wide.

Conclusion: in these data, communities adjust within a few years. But they adjust toward a target that
is only about one sixth to one third of the change that the spatial gradient predicts. The tracking
deficit is mainly a small temporal sensitivity, not a slow approach to the spatial equilibrium.

### 4.4 Thermal signal in the turnover is weak

When we permuted STI values among taxa, the observed slopes were above the null in combination
(Stouffer z = 2.66 for fast and 2.52 for slow slopes). But only 4 networks (fast) and 3 networks (slow)
had p < 0.05 alone (Figure 4). Thus most networks had species turnover. But in most single networks,
the turnover did not select warm-affinity taxa more than random taxa. This agrees with earlier campaign
results for trees (sci:sha256:adb306e0...) and winter birds (sci:sha256:26c7bb1f...).

## 5. Interpretation

1. The weak tracking that campaign studies found for birds, river fish, trees and butterflies is
   general. Across 75 networks, the trend response was about 0.1 to 0.2 of the spatial gradient.
2. Space-for-time substitution overestimates the temporal response of community composition by a
   factor of about 3 to 8 in these networks (1/theta = 3.6; 1/phi_slow = 8). Climate-debt estimates that compare raw CTI change with
   warming, or with the spatial gradient, measure this gap, not only a lag.
3. A long lag does not explain the gap. Year-to-year responses persist for only a few years, and
   long series have no larger fractions.
4. Possible causes of a small equilibrium response: the spatial gradient includes habitat, land use
   and dispersal history that co-vary with temperature; communities respond to other factors that
   changed at the same time (land use, fishing, water quality); and the fast response can include
   detection or activity changes in warm years. These data cannot separate these causes.

## 6. Deviations from the plan

- Added after the first results: the two-parameter (k, theta) fit (`03b_two_param.py`), the
  richness and effort covariate summary (`03c_richness.py`), and the exclusion of the degenerate study 68.
- The planned "drop small spatial range" check is the "Climatology SD >= 0.5 C" row.
- The emulator ran only for the main variant.

## 7. Limitations

- Surface air temperature and SST are proxies for benthic, freshwater and soil habitats. The
  freshwater null result can come from this proxy.
- BioTIME studies differ in methods. We use only within-network contrasts, but the pooled means
  weight networks by precision, and a few large networks (BBS, NEFSC) have large weights.
- The STI comes from the spatial distribution inside each network. It is cut at the network edge
  and includes non-thermal gradients. b_space is therefore not a pure thermal niche gradient.
- beta_slow is the CTI trend divided by the temperature trend on the same site-years. Any CTI trend
  from other causes (land use, effort, taxonomy changes) enters it. Where warming is small, beta_slow is
  imprecise. The random-effects weights reduce, but do not remove, this noise.
- Per-network fractions are ratios with noisy denominators. We give pooled ratios of means for inference.
- The block bootstrap of b_space does not re-estimate STI values. Year-clustered errors use 10 to 59 years.
- The lag model has one rate for all networks and no stochastic term. Detection changes in warm years
  can make the fast response too large.
- The marine result depends on the SST product and period. Only aggregate statistics are published.

## 8. Files

- `files/PLAN.md`: plan written before the slopes were computed.
- `files/code/`: `00_convert_rds.py`, `01_build.py`, `01b_external.py`, `02_networks.py`,
  `03_synthesis.py`, `03b_two_param.py`, `03c_richness.py`, `04_figures.py`, `retrieve_data.sh`, `run_all.sh`.
- `files/results/networks_<variant>.csv`: per-network slopes, errors, counts and shuffle-null statistics.
- `files/results/networks_main_annotated.csv`: main results with realm, taxa, group, lag-test values,
  study title and BioTIME permission.
- `files/results/emulator_main.csv`: emulator fast and slow fractions for each network and k.
- `files/results/synthesis_groups.csv`, `synthesis_tests.json`, `two_param_fit.json`,
  `two_param_profile.csv`, `two_param_bootstrap.csv`, `two_param_loo.csv`, `richness_control.json`.
- `files/figures/fig1..fig4`: figures.
- `files/NOTICE-external-data.md`: sources, versions, hashes and licences of external data.

## 9. Reproduction

1. `bash files/code/retrieve_data.sh DATA_DIR` (or use the campaign `datasets/` folder; dataset names
   are the folder names in the script).
2. Make a Python 3.12 environment with pandas, numpy, scipy, xarray, netCDF4, pyreadr 0.5.9, pyproj and
   matplotlib (we used pandas 3.1, numpy 2.5, scipy 1.18, xarray 2026.9).
3. `bash files/code/run_all.sh DATA_DIR SCRATCH OUT_RESULTS OUT_FIGURES`. SCRATCH receives record-level
   tables. Keep it outside the publication. The main variant takes about 30 minutes on 8 cores.
   Random seeds are fixed (network ID for splits and permutations).

External data stay under their own licences (see `files/NOTICE-external-data.md`). The LICENSE of
this bundle covers only our code, text, figures and aggregate tables.
