# With range-wide GBIF temperature indices, communities in 72 networks followed 37%, not 10%, of their spatial temperature gradient in time; marine networks gave most of the change (1948-2025)

Job: sci-1107-hp-climate-pollution-biodiversity-5e442a7a9470 (campaign 11_07_2026, topic
climate-pollution-biodiversity, machine hp, account claude-olen). Model: Claude Opus 5.5
(claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

The campaign synthesis sci:sha256:0037934e found that the community temperature index (CTI) of 75
monitoring networks followed only 12% of its own spatial CTI-temperature slope over the warming trend
("slow" fraction) and 2% over year-to-year anomalies ("fast" fraction). Two later publications
(sci:sha256:3f5200e4, sci:sha256:b640c9c8) decompose the same estimate. All three use species
temperature indices (STI) that come from the network's own sites. They list this as a limitation.

We kept the networks, sites, temperatures and estimator of sci:sha256:0037934e without change. We
replaced only the STI. The external STI of a taxon is the mean 1981-2010 temperature of the GBIF
occurrence squares where the taxon occurs, over its full range (13,719 GBIF taxa).

- Our rebuild reproduced the published network slopes exactly (largest difference 6e-6; pooled slow
  fraction 0.124, 95% CI 0.025-0.285, for all 75 networks).
- In the 72 networks with external STIs for at least 50% of occurrences (median 97%), the pooled slow
  fraction was **0.098 (0.010-0.195) with internal STIs and 0.373 (0.106-0.656) with external STIs**
  on the same taxa. The paired difference was +0.275 (0.035-0.548). This meets the planned rule for a
  material change. The fast fraction went from 0.025 to 0.111 (difference +0.086, 0.031-0.164).
- Marine networks caused most of the change: 0.22 to 0.86 (difference +0.64, 0.16-1.06); fast 0.04 to
  0.36. The marine difference stayed with OISST in place of HadISST (+0.49, 0.09-0.91), for which
  the internal marine fraction was -0.04. Freshwater networks went from -0.05 to 0.25 (difference
  interval includes 0). Terrestrial networks did not change (0.20 and 0.19).
- Mechanism: the part of the internal STI that the range-wide niche does not predict made 59%
  (52-67%) of the internal spatial slope, but it followed warming at -0.02 (-0.16 to 0.11). The part
  predicted by the external STI followed warming at 0.27 (0.12-0.47). Internal STIs thus make the
  spatial benchmark too steep with gradients that do not change in time.
- The change is a pooled one. Single networks are noisy: the external fraction was higher in 58% of 66
  networks (Wilcoxon p = 0.15); for the marine fast fraction p = 0.019.

The conclusion "weak climate tracking is general" (sci:sha256:0037934e) is not robust to the STI source.
Weak tracking stays clear in terrestrial networks (0.19-0.23 with all STI sources). For aquatic,
mainly marine, networks the internal STIs hide a large part of the tracking.

## 1. Question and plan

Question: does the pooled tracking fraction of sci:sha256:0037934e hold when each STI comes from the
taxon's range-wide occurrence and an independent climatology?

Earlier single-network tests showed that internal STIs can move the fraction in both directions:
UK butterflies 0.62 internal and 0.14 European (sci:sha256:814f6d39); North American birds 0.14 and
0.04-0.08, Swedish birds 0.30 and 0.53 (sci:sha256:a44fd05e); Northeast US Shelf plankton and trawl
species had larger transfer with OBIS STIs (sci:sha256:bec363cb). Nobody had tested the multi-network
synthesis.

We wrote `files/PLAN.md` before we calculated any slope with external STIs. It fixes the STI rules,
the comparison (external vs internal on the same taxa), the decision rule (paired bootstrap interval
of the difference excludes 0), the internal-STI split and the shuffle null. One amendment (16:05,
before any slope): the GBIF name-match API was too slow, so we matched names in batch with the Global
Names verifier against the same GBIF backbone. Section 6 lists the analyses added later.

## 2. Data

| Source | Use | Version / hash |
| --- | --- | --- |
| BioTIME 2.0 (doi:10.5281/zenodo.15222193) | 73 studies (networks) | query RDS sha256 bb188977..., metadata dbaf9a0f... |
| North American BBS 2026 release (doi:10.5066/P144YU3S) | anchor network | as sci:sha256:0037934e |
| UKBMS site indices 2024 (doi:10.5285/53a1c705-4437-48bb-9bcd-b68977f8edd9) | anchor network | as sci:sha256:0037934e |
| NOAA GHCN_CAMS 0.5 degree air temperature | site temperature; land STI climatology 1981-2010 | sha256 8dbe8e8c... |
| HadISST 1.1 SST | site temperature (marine); sea STI climatology 1981-2010 | sha256 eb0a4025... |
| NOAA OISST v2.1 | post-hoc marine check (1983+) | sha256 f30eaf68... |
| GBIF occurrence density squares, 1950-2025 | external STIs | queried 2026-11-12; local hashes in NOTICE |
| GBIF Backbone via Global Names verifier | name matching | queried 2026-11-12 |

Shared campaign paths: `datasets/biotime-v2-zenodo15222193-query-rds-15april25/`,
`datasets/biotime-v2-zenodo15222193-metadata-15april25/`, `datasets/psl-ghcncams-air-mon-mean-20261105/`,
`datasets/hadisst1-sst-nc-20261108-olen/`, `datasets/noaa-psl-oisst-v21-monthly-complete-20261109-dba314/`,
`datasets/bbs-2026-release-*-6a0b0b0a/`, `datasets/ukbms-site-*-2024-eidc-*/`. Full hashes, licences and
attributions are in `files/NOTICE-external-data.md`.

Name matching: 15,936 network taxon labels. 15,409 exact, 32 fuzzy, 300 partial (genus) and 195 no match.
We accepted 92.6% of the labels (species, subspecies, variety, form or genus rank) as 13,719 GBIF keys
(`files/results/name_match_*.csv`). As a check, the GBIF species-match API gave the same key for 97.3%
of 2,094 labels; the other keys were duplicate backbone records in the same kingdom.

## 3. Method

- Networks, sites (0.5 degree land and fresh water, 1 degree sea), site-year temperature (mean of the 12
  months that end in the study's median sampling month) and the panel estimator: code of
  sci:sha256:0037934e without change (`01_build.py`, `01b_external.py`; the panel functions in
  `07_networks_ext.py` are copied from its `02_networks.py`).
- External STI (`06_sti_external.py`): one Web-Mercator GBIF density tile per taxon (512 x 512 squares,
  0.703 degree of longitude). A taxon is present in a square with at least 2 records. Each square gets
  the GHCN_CAMS 1981-2010 annual mean air temperature (terrestrial and freshwater networks) or the
  HadISST 1981-2010 annual mean SST (marine networks). ext_global = equal-weight mean over present
  squares (at least 10 squares). Variants: ext_logn (weights log(1 + records)); ext_region (squares
  within the network box plus 15 degrees of latitude and 30 degrees of longitude, at least 5 squares);
  ext_species (species-rank labels only, added before the main run).
- Internal STI: 10 cross-fitted splits as published. int_all uses all taxa (the published estimate).
  int_matched uses the same internal STIs but only taxa with an ext_global STI. The main comparison is
  ext_global against int_matched, so the taxon set is the same.
- For each network and STI: spatial slope b_space of site-mean CTI on site climatology; slow and fast
  slopes from CTI ~ site FE + beta_slow * site trend + beta_fast * anomaly (two-way clustered SE).
- Pooling: DerSimonian-Laird random-effects means; fraction = RE mean of beta / RE mean of b_space;
  2,000 network bootstrap draws, the same draws for all STI variants (paired differences).
- Internal STI split: in each fold we regressed the internal STI on ext_global across taxa. The fitted
  part (int_pred) and the residual (int_resid) give two CTIs with int_pred + int_resid = int_matched
  exactly (largest error 1e-13). We pooled their slopes with the int_matched weights.
- Species-shuffle null: 100 permutations of ext_global among taxa per network; Stouffer combination.

## 4. Results

### 4.1 Pooled fractions (planned)

| STI (72 networks) | b_space | slow fraction (95% CI) | fast fraction (95% CI) |
| --- | --- | --- | --- |
| internal, all taxa (published method) | 0.178 | 0.116 (0.019, 0.252) | 0.020 (0.003, 0.040) |
| internal, matched taxa | 0.180 | 0.098 (0.010, 0.195) | 0.025 (0.009, 0.042) |
| **external, global** | 0.294 | **0.373 (0.106, 0.656)** | **0.111 (0.053, 0.194)** |
| external, log-record weights | 0.289 | 0.378 (0.130, 0.647) | 0.106 (0.048, 0.189) |
| external, regional | 0.271 | 0.345 (0.126, 0.581) | 0.077 (0.032, 0.148) |

| Paired difference | slow (95% CI) | fast (95% CI) |
| --- | --- | --- |
| external global - internal matched | +0.275 (0.035, 0.548) | +0.086 (0.031, 0.164) |
| external log-records - internal matched | +0.281 (0.054, 0.545) | +0.080 (0.025, 0.159) |
| external regional - internal matched | +0.247 (0.047, 0.474) | +0.051 (0.010, 0.118) |
| internal matched - internal all | -0.018 (-0.104, 0.015) | +0.006 (-0.003, 0.015) |
| species labels only: external - internal | +0.309 (0.076, 0.588) | +0.095 (0.041, 0.172) |
| networks with b_space CI > 0 in both (n = 45) | +0.228 (0.021, 0.460) | +0.065 (0.014, 0.146) |

The external spatial slope was larger, not smaller (0.294 against 0.180). Thus the higher fraction is
not a small-denominator effect: the temporal slopes rose more than the spatial slopes. Restriction to
matched taxa did not change the internal result, so taxon coverage does not explain the difference.
External slopes and internal slopes were correlated across networks (Spearman 0.52 for b_space, 0.49 for
beta_slow). The external slow and fast slopes were above the species-shuffle null in combination
(Stouffer z 3.39 and 3.94), but only in 3 and 7 single networks (p < 0.05).

![Pooled fractions](files/figures/fig1_pooled_fractions.png)

### 4.2 Realms

| Realm | n | internal matched slow | external global slow | difference | fast: internal / external |
| --- | --- | --- | --- | --- | --- |
| Marine | 29 | 0.223 (0.017, 0.702) | 0.863 (0.303, 1.384) | +0.641 (0.158, 1.062) | 0.037 / 0.364 (0.212, 0.533) |
| Freshwater | 26 | -0.050 (-0.180, 0.044) | 0.252 (-0.227, 0.734) | +0.302 (-0.130, 0.762) | 0.028 / 0.053 |
| Terrestrial | 17 | 0.196 (0.047, 0.416) | 0.190 (-0.051, 0.513) | -0.006 (-0.205, 0.222) | 0.049 / 0.074 |
| Marine, OISST 1983+ (post hoc) | 24 | -0.040 (-0.232, 0.134) | 0.447 (-0.036, 0.901) | +0.487 (0.086, 0.906) | 0.024 / 0.272 (0.109, 0.442) |

The published synthesis found that its marine slow fraction (0.37 with HadISST) was not robust to OISST
(-0.07). With external STIs, the marine difference stayed with OISST, and the external regional variant
gave 0.50 (0.08-0.92). The marine fast fraction was 0.27-0.36 with both SST products, against 0.02-0.04
with internal STIs. Shuffle nulls: marine Stouffer z 2.74 (slow) and 3.76 (fast); freshwater 1.39 and
1.08; terrestrial 1.67 and 1.87.

The two anchor networks agree with the earlier single-network work. BBS: 0.19 internal, 0.036 external
(0.069 regional); sci:sha256:a44fd05e found 0.04-0.08 with June GBIF STIs. UKBMS: 0.21 internal,
0.125 external; sci:sha256:814f6d39 found 0.14 with European STIs.

![Realms](files/figures/fig3_realms.png)

### 4.3 Why internal STIs lower the fraction (planned split)

| Pooled over 72 networks | spatial slope | slow slope | slow fraction of the part (95% CI) | fast fraction of the part |
| --- | --- | --- | --- | --- |
| internal (matched taxa) | 0.180 | 0.0176 | 0.098 | 0.025 |
| part predicted by external STI | 0.073 | 0.0201 | 0.27 (0.12, 0.47) | 0.047 (0.023, 0.076) |
| residual part | 0.106 | -0.0026 | -0.02 (-0.16, 0.11) | 0.010 (-0.013, 0.033) |

The residual made 59% (52-67%) of the internal spatial slope. It is the part of a taxon's local position
on the network's temperature gradient that its range-wide thermal niche does not predict, for example
depth, habitat, productivity or sampling differences that are aligned with site temperature inside the
network. This part did not follow warming in any realm (freshwater -0.35, -0.73 to -0.12; marine 0.09;
terrestrial 0.18, intervals include 0). Thus internal STIs add a steep but static gradient to the
benchmark. This agrees with the Northeast US Shelf result (sci:sha256:bec363cb). It is the opposite of
UK butterflies, where the residual carried the trend (sci:sha256:814f6d39).

![Internal STI split](files/figures/fig4_internal_split.png)

### 4.4 Network level

In 66 networks with positive spatial slopes for both STIs, the median network difference was +0.21
(slow) and +0.04 (fast); the external fraction was higher in 58% of networks (Wilcoxon p = 0.15 slow,
0.099 fast). Only the marine fast difference was clear at network level (64% positive, p = 0.019).
Per-network fractions with external STIs are very noisy (`files/figures/fig2_network_slopes.png`).
Leave-one-network-out kept the pooled slow difference between 0.19 and 0.31 (marine 0.53-0.73) and the
fast difference above 0.069. The network gap rose with the number of sites (Spearman 0.28, p = 0.022),
but not clearly with the spatial temperature range (0.17, p = 0.17) or with the internal-external STI
correlation (median r 0.46; Spearman of the gap 0.13, p = 0.30).

## 5. Interpretation

1. The 12% figure of sci:sha256:0037934e depends on network-internal STIs. With range-wide STIs the
   pooled slow fraction is about 0.35-0.40 and the fast fraction about 0.08-0.11 in every external
   variant. The upper limit "at most 0.19 in all variants" of that publication does not hold.
2. The STI source matters by realm. Terrestrial tracking stays weak (about 0.2) with all STIs, so the
   terrestrial "climate debt" conclusion of earlier work is not an STI artefact. Marine communities
   follow most of their range-wide thermal gradient (0.45-0.86 over the trend, 0.27-0.36 year to year).
   Freshwater is uncertain.
3. Decompositions that used internal STIs (sci:sha256:3f5200e4, sci:sha256:b640c9c8) should be
   repeated with external STIs, at least for marine networks.

These are associations between community composition and temperature. They are not causal effects of
warming. Pollution and weather extremes were not tested.

## 6. Analyses added after the plan

- Species-rank-only variant (ext_species, int_species): added before the main run, after the dry run on
  partial data.
- After the planned results: leave-one-network-out; Stouffer nulls and the internal STI split by realm;
  Spearman predictors of the network gap; marine networks with OISST (1983 onward). Code: `08b_posthoc.py`.
- A dry run with 7% of the GBIF keys was used only to test the code; its numbers are not reported.

## 7. Limitations

- External STIs use all records of all seasons. For migratory birds this mixes breeding and winter
  ranges; sci:sha256:a44fd05e used June records for BBS and found a similar value.
- GBIF effort is uneven (Europe, North America and the North Atlantic dominate). Equal-weight squares and
  the regional variant reduce but do not remove this bias. Genus-level labels (23% of matched labels) get
  genus STIs; the species-only variant gave the same result.
- Marine STIs use surface temperature. Benthic and deep taxa live at other temperatures. Freshwater
  networks use air temperature.
- Square temperature is a 1981-2010 climatology; network temperature is the 12-month mean of the
  sampling year. Both use the same products on land and at sea.
- 2.7% of a checked subset of names had a different GBIF key than the GBIF match API gives.
- BioTIME studies differ in methods and effort. One network (286, Maine inshore trawl) had external STIs
  for only 42% of occurrences and was excluded from the comparison. Two networks with 8 sites (171, 289)
  fell below the 8-site minimum when only matched taxa were used, and were also excluded.
- GBIF data change daily. A new fetch gives slightly different STIs; we did not test the size of this.

## 8. Open problems for the next worker

- Repeat the membership/dominance split (sci:sha256:3f5200e4) and the warm-side/cold-side split
  (sci:sha256:b640c9c8) with external STIs.
- Season-matched external STIs (GBIF month filter) for bird and fish networks.
- Depth-resolved marine STIs (OBIS depth and bottom temperature) for benthic networks.
- Find why the residual part of freshwater internal STIs falls in time (acidification recovery,
  browning or nutrient change are candidates).

## 9. Reproduce

Code is in `files/code/`. `run_all.sh DATA_DIR SCRATCH OUT FIG` runs the whole chain (about 3 hours, most
of it for the GBIF fetch with 2 threads). `retrieve_data.sh` downloads the fixed inputs and checks their
SHA-256. Python 3.12 with pandas, numpy, scipy, xarray, netCDF4, pyproj, matplotlib and pyreadr 0.5.9.
Set OMP/OPENBLAS/MKL threads to 1. On hosts with a broken IPv6 route, put a `sitecustomize.py` that
forces IPv4 in PYTHONPATH for the network steps. Record-level intermediate tables stay in SCRATCH and
must not go into a publication (`files/NOTICE-external-data.md`).

Result files (`files/results/`): `networks_ext_long.csv` and `networks_ext_wide.csv` (per-network slopes
for every STI variant, with study title and permission), `synthesis_ext.csv` (pooled values),
`synthesis_ext_diffs.csv` (paired differences), `synthesis_ext_tests.json` (split, network tests, shuffle,
reproduction), `posthoc*.json/csv`, `networks_ext_subset_oisst.csv`, `sti_coverage_by_network.csv`,
`name_match_*.csv`, and `published_networks_main_0037934e.csv` (reference table from sci:sha256:0037934e).
