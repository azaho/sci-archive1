# Species presence, not abundance, made 95% of spatial temperature gradients in 75 community networks; per 1 C, exchange of species in time was 16% of that in space (1948-2025)

Job: sci-1107-dell-climate-pollution-biodiversity-5c413f4a2fba (campaign 11_07_2026, topic
climate-pollution-biodiversity, machine dell, account claude-sci). Model: Claude Opus 5.5
(claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Earlier campaign work found that community temperature indices (CTI) follow only a small part of
warming. In 75 monitoring networks, the CTI trend was about 12% of the network's own spatial
CTI-temperature slope (sci:sha256:0037934e...). A lag fit gave fast adjustment to a small target
(theta about 0.28). Bird studies found the same small fraction (sci:sha256:c0a3a9aa...,
sci:sha256:b41e4848..., sci:sha256:91f371b5...). Forest type explained about half of the gap on
forested bird routes (sci:sha256:1f25ce5b...). Observer, phenology, traffic and insecticide effects
were too small to close it. Which ecological process holds the rest of the gap is open.

A CTI can change in two ways:

1. **Membership**: which taxa are present at a site. This changes by colonisation and local
   extinction. Colonisation needs dispersal and establishment. Extinction of established
   populations can be slow.
2. **Dominance**: the relative abundance of the taxa that are present. This changes by births, deaths
   and local movement of resident populations.

We asked: which of the two makes the spatial CTI gradient, and which of the two follows warming in
time? We used data beyond the Breeding Bird Survey (BBS): 73 BioTIME 2.0 studies, plus the BBS and
the UK Butterfly Monitoring Scheme (UKBMS) as anchor networks.

## 2. Data

The networks, sites and temperatures are the same as in sci:sha256:0037934e. We reused its build
scripts without change.

- BioTIME 2.0 (Zenodo 15222193, 15 April 2025): 73 studies with at least 8 climate grid boxes that
  have at least 5 sampled years, at least 10 sampled years and at least 10 taxa.
- BBS 2026 release (standard runs, 1966-2025) and UKBMS site indices 2024 (1976-2024).
- NOAA GHCN_CAMS 0.5 degree air temperature (land and fresh water); HadISST1 (marine, main) and NOAA
  OISST v2.1 (marine, 1983 and later, sensitivity).
- 75 networks: 32 marine, 26 freshwater, 17 terrestrial; 56 ectotherm, 14 endotherm, 5 plant.
  8,529 sites (climate grid boxes), 183,626 site-years, 1948-2025. All 75 networks have abundance or
  biomass on at least 90% of records.

## 3. Method

### 3.1 Exact decomposition (planned; `files/PLAN.md`, written before outcomes)

Species temperature indices (STI) are cross-fitted as in sci:sha256:0037934e: the STI of a taxon is
its prevalence-weighted mean site climatology in one half of the sites. It is used only at sites in
the other half (10 random splits, stratified by climatology). For each site-year:

- A = abundance-weighted CTI. The weight of a taxon is the mean over the site-year samples of
  log(1 + abundance).
- M = membership CTI: the unweighted mean STI of the taxa present.
- D = A - M: the dominance part.

A = M + D exactly. All slopes are linear in the outcome. Thus the spatial slope b_A = b_M + b_D, and
the temporal slope beta_A = beta_M + beta_D. The spatial slope uses site means on site climatology
(joint 2 degree block bootstrap). The slow slope uses the site's linear temperature trend and the fast
slope uses the annual anomaly, with site fixed effects and two-way (site, year) clustered errors.
The gap b_A - beta_A divides exactly into a membership part and a dominance part.

Synthesis: one random-effects weight per network for all three parts (from the A part), so that the
pooled parts add up exactly. Intervals come from 2,000 network bootstrap resamples. STI-shuffle nulls
(100 permutations per network) test whether each slow slope follows thermal affinity.

Planned hypothesis H1 (membership inertia): communities reweight their resident taxa fast, but
membership changes slowly. Then the dominance fraction beta_D / b_D is larger than the membership
fraction beta_M / b_M. If H1 is true with full reweighting, the total fraction is near the dominance
share of the spatial slope, s_D = b_D / b_A.

Planned robustness variants: richness and sample-number covariates; occurrence-frequency weights;
raw relative-abundance weights; only site-years with the site's modal number of samples; OISST for
marine networks; BioTIME only; networks with b_A interval above 0.

### 3.2 Gains, losses and reweighting (planned split, refined after the first results)

For each site with at least 6 sampled years, we compared the early half and the late half of its
sampled years. P = taxa in both halves, G = gained taxa, L = lost taxa. These splits are exact:

- membership: dM = gain + loss, with gain = q_G (m_G - m_P) and loss = -q_L (m_L - m_P);
  q_G and q_L are the shares of taxa.
- membership, second form: dM = exchange + richness term, with exchange = (q_G + q_L)/2 (m_G - m_L)
  and richness term = (q_G - q_L) ((m_G + m_L)/2 - m_P). The exchange term is the thermal contrast of
  gained against lost taxa. The richness term comes from a change in the number of taxa.
- abundance-weighted: dA = reweighting of persistent taxa + gain + loss, where the gain and loss terms
  use abundance shares Q_G and Q_L.

Each term is corrected by its STI-permutation null (100 permutations), and divided by the pooled
warming between the halves. The plan had gain and loss terms. The exchange/richness split, the
abundance-weighted split and the null correction of the terms were added after the first results.

### 3.3 Space versus time (added after the first results)

For pairs of sites in the same network (up to 6,000 pairs), we compared the early-half taxa lists of
the two sites, with the warmer site in the role of the late window. We fitted (per network) the
exchange term and the gained-minus-lost STI difference on the climatology difference (through the
origin), and turnover on the temperature difference and the distance. We compared these spatial
values with the temporal values from 3.2.

## 4. Results

### 4.1 The spatial gradient is a membership gradient (Figure 1)

| Pooled slope (C per 1 C), 75 networks | A (total) | M (membership) | D (dominance) |
| --- | --- | --- | --- |
| Spatial, b | 0.179 (0.142 to 0.215) | 0.171 (0.136 to 0.206) | 0.008 (0.003 to 0.014) |
| Slow (warming trend), beta | 0.017 (-0.001 to 0.050) | 0.021 (0.004 to 0.051) | -0.004 (-0.012 to 0.007) |
| Fast (annual anomaly) | 0.004 (0.002 to 0.008) | 0.003 (-0.001 to 0.007) | 0.002 (-0.001 to 0.006) |

- The dominance share of the spatial slope was **s_D = 0.046** (0.015 to 0.076); network median 0.044.
  The membership slope had an interval above 0 in 55 networks, the dominance slope in 18.
- BBS: b_M = 0.449, b_D = -0.0001 (-0.0016 to 0.0016). UKBMS: b_M = 0.141, b_D = 0.009 (-0.005 to 0.020).
- s_D was 0.04 to 0.06 in every variant and group except the modal-sample variant (-0.01) and
  freshwater networks (-0.03).

### 4.2 The trend response is membership; reweighting did not follow warming (Figures 1 and 4)

- Membership followed **phi_M = 0.125** (0.025 to 0.285) of its spatial slope (0.165, 0.060 to 0.407,
  in the 54 networks with a clear spatial slope). The membership slow slope was above its STI-shuffle
  null in combination (Stouffer z = 3.35; 7 single networks p < 0.05).
- The dominance slow slope was -0.004 (-0.012 to 0.007), and at its shuffle null (z = 0.04).
  In the two large anchor networks it was clearly negative: BBS -0.026 (SE 0.004; membership +0.090),
  UKBMS -0.024 (SE 0.005; membership +0.053).
- Membership held **93%** of the spatial-temporal gap (g_M = 0.925, 0.868 to 0.995). This follows
  mainly from 4.1: the spatial slope is almost all membership.
- **H1 is not supported.** The dominance fraction was not larger than the membership fraction
  (17 networks with both spatial slopes clearly positive: median difference -0.62, Wilcoxon p = 0.21;
  phi_D larger in 29%). Also, s_D (0.05) is far below theta = 0.28. A fast reweighting toward a
  dominance-only target cannot explain the observed tracking.
- Fast responses: the dominance part was about half of the fast response in terrestrial networks
  (0.006 of 0.013 C per C; share 0.44, 0.11 to 0.84), but not in the trend. Warm-year abundance or
  detection changes do not accumulate into the trend.
- Variants (Figure 4): richness and effort covariates gave phi_M = 0.091 (-0.015 to 0.226); modal
  sample number 0.187 (0.060 to 0.337); occurrence-frequency weights 0.120; raw relative abundance
  0.103. With OISST (marine, 1983 and later), membership did not follow warming (-0.118, -0.397 to
  0.108), as the marine result in sci:sha256:0037934e.

### 4.3 Gains, losses and rare newcomers (Figure 2)

Early half versus late half at 72 networks (pooled warming between halves 0.30 C). Values are per 1 C
of warming, after null correction:

| Term | per 1 C | Stouffer z |
| --- | --- | --- |
| Gains (count) | +0.055 (0.023 to 0.112) | 4.83 |
| Losses (count) | -0.024 (-0.066 to 0.003) | -2.37 |
| Exchange (gained versus lost taxa) | +0.028 (-0.001 to 0.059) | 2.64 |
| Richness-change term | +0.003 (-0.006 to 0.014) | 1.18 |
| Membership total dM | +0.031 (0.002 to 0.064) | 3.27 |
| Reweighting of persistent taxa | +0.000 (-0.017 to 0.023) | 0.05 |
| Gains (abundance-weighted) | +0.007 (-0.003 to 0.022) | 2.49 |
| Abundance-weighted total dA | +0.008 (-0.015 to 0.038) | 1.52 |

- Gained taxa were warm-affinity taxa. Lost taxa were also warmer than persistent taxa, so losses
  moved the CTI slightly the wrong way. The net effect is the exchange term: gained taxa had an STI
  0.065 C (0.002 to 0.13) above lost taxa, after null correction.
- Turnover was large: gained taxa were 22% and lost taxa 19% of the taxa of a half.
- **Newcomers stayed rare.** Gained taxa had 6.1% of the abundance weight, against 21.7% of the taxa.
  Their abundance share was 0.28 (0.23 to 0.34) of their count share. In all 72 networks, the
  abundance share of gained taxa was below their count share. Lost taxa were also rare (ratio 0.29).
  Thus the abundance-weighted CTI follows warming less than the membership CTI. This explains why the
  dominance part of the trend is negative where membership changes most (BBS, UKBMS).

### 4.4 Space versus time: less turnover and less thermal selection (Figure 3)

70 networks with spatial pairs and windows:

| Quantity | Space (site pairs) | Time (early vs late) | Time / space |
| --- | --- | --- | --- |
| Exchange term (C of M per 1 C) | 0.186 (0.155 to 0.219) | 0.030 (0.001 to 0.065) | 0.16 (0.01 to 0.34) |
| Gained-minus-lost STI (C per 1 C) | 0.363 (0.320 to 0.409) | 0.235 (0.025 to 0.476) | 0.65 (0.07 to 1.25) |
| Turnover (share of taxa) | 0.300 at zero distance and zero dT (0.272 to 0.329) | 0.193 (0.168 to 0.222) | 0.64 (0.56 to 0.72) |

- The spatial exchange slope agreed with the membership spatial slope (0.186 against 0.171; rank
  correlation across networks 0.90). It was above its STI-shuffle null in 62 of 70 networks.
- Between real site pairs (median distance 340 km), turnover was 0.42. It increased by about 0.02 per
  100 km and 0.01 per 1 C (network medians).
- In time, turnover between half-series (mean years 5 to 23 apart, median 10) was lower than between two equally warm sites at zero
  distance. Across networks, temporal turnover did not increase with the warming between halves
  (Spearman -0.15, p = 0.23).
- The thermal selectivity of temporal turnover was uncertain (time/space 0.07 to 1.25).

## 5. Interpretation

1. Spatial CTI gradients in these networks are gradients in species lists. Abundance differences
   among the taxa that occur at a site add only about 5%. Range limits and site pools, not abundance
   structure, make the space-for-time benchmark.
2. In time, only membership change followed warming. Resident taxa did not shift their relative
   abundances toward warm-affinity taxa in the trend. Thus the gap is a membership gap: about 93% of
   it is in which taxa are present.
3. The process that limits the trend response is the warming-driven exchange of taxa. Communities do
   turn over (19-22% of taxa per half-series), but this turnover is mostly background turnover: it
   does not increase with warming, and its thermal selection per 1 C is lower and uncertain. The
   exchange per 1 C in time was 16% of the exchange per 1 C between sites.
4. Colonists stay rare for the length of these series. This is consistent with an establishment
   phase: new warm-affinity taxa arrive, but do not become common within about 5 to 23 years. Abundance-weighted
   indices therefore show even less tracking than presence-based indices.
5. These results do not support a fast reweighting of residents toward a small target. They agree
   with sci:sha256:0037934e that the deficit is not a simple long lag, and they move the deficit to
   the colonisation-extinction process.

## 6. Deviations from the plan

- Added after the first results: the null-corrected window terms, the exchange/richness split, the
  abundance-weighted window split (section 3.2), the space-versus-time pair benchmark (3.3), and the
  check of temporal turnover against warming. The first-version window columns (`w_*` in
  `decomp_main.csv`, and the `window_*` entries in `decomp_tests.json`) are superseded by
  `windows_*.csv/json`.
- The planned "exclude BBS/UKBMS" check is the BioTIME-only row.
- The occurrence-frequency variant covers the same 75 networks, because all networks had abundance data.

## 7. Limitations

- Membership change includes detection and effort changes of rare taxa. The STI-permutation null
  removes detection noise that does not depend on STI. It does not remove detection changes that
  correlate with thermal affinity (for example observer hearing in the BBS, sci:sha256:b113aa1b...).
  Richness and effort covariates reduced phi_M from 0.125 to 0.091.
- The dominance part is small in space, so the dominance fraction beta_D / b_D is not stable; we
  compare slopes in C per C instead.
- Window and pair analyses compare taxa lists of half-series. Spatial turnover at zero distance is an
  extrapolation from pairs that are at least one grid box apart. Temporal and spatial turnover both
  include sampling turnover; we compared them at the same window length per site.
- Abundance units differ between studies; we used only within-network contrasts and log weights
  (raw relative-abundance weights gave the same result).
- STIs are network-internal and include non-thermal gradients. Air temperature and SST are proxies
  for freshwater and benthic habitats. Marine results depend on the SST product.
- Two BioTIME studies (166, 172) are CC BY-NC; we publish only aggregate statistics for them.
- We did not test which traits (dispersal, habitat breadth) limit the exchange. This is the next step.

## 8. Files

- `files/PLAN.md`: plan written before the component slopes were computed.
- `files/code/`: `00_convert_rds.py`, `01_build.py`, `01b_external.py` (from sci:sha256:0037934e),
  `02_decomp.py` (decomposition, windows and pairs), `03_decomp_synth.py`, `05_windows_synth.py`,
  `06_pairs_synth.py`, `07_figures.py`, `retrieve_data.sh`, `run_all.sh`.
- `files/results/decomp_<variant>.csv`: per-network spatial, slow and fast slopes of A, M and D
  (variants main, freq, raw, modal, oisst). `decomp_main_annotated.csv` adds realm, taxon group,
  study title and BioTIME permission. `decomp_synthesis.csv`, `decomp_tests.json`: pooled results.
- `files/results/decomp_windows.csv`, `windows_annotated.csv`, `windows_synthesis.csv`,
  `windows_tests.json`: gain, loss, exchange and reweighting terms and their nulls.
- `files/results/decomp_pairs.csv`, `space_time_turnover*.csv/json`: spatial pair benchmark.
- `files/figures/fig1..fig4`: figures. `files/input_sha256.txt`: hashes of all input files.
- `files/NOTICE-external-data.md`: sources, versions, hashes and licences of external data.

## 9. Reproduction

1. `bash files/code/retrieve_data.sh DATA_DIR` (or use the campaign `datasets/` folder; dataset
   folder names are the names in the script). Check hashes against `files/input_sha256.txt`.
2. Python 3.12 with pandas 3.1, numpy 2.5, scipy, xarray, netCDF4, pyreadr 0.5.9, pyproj, matplotlib.
3. `bash files/code/run_all.sh DATA_DIR SCRATCH OUT_RESULTS OUT_FIGURES 12`. SCRATCH receives
   record-level tables; keep it outside the publication. The full run takes about 1 to 1.5 hours with
   12 workers. Random seeds are fixed (network ID for splits, bootstraps and permutations).

External data stay under their own licences (see `files/NOTICE-external-data.md`). The LICENSE of
this bundle covers only our code, text, figures and aggregate tables.
