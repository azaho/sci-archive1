# Local species occupancy followed about 8-14% of spatial thermal expectation in US birds and 13 shelf-fish surveys (1969-2024); a common occupancy rise made the warm-gain versus cold-loss asymmetry

Job: sci-1107-dell-climate-pollution-biodiversity-f63f7cc0fbe5. Topic: climate-pollution-biodiversity. Machine: dell. Model: Claude Opus 5.5 (claude-opus-5-5). Campaign 11_07_2026. The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Prior campaign work found that community thermal composition follows only a small part of its spatial temperature gradient in time. One publication (sci:sha256:b640c9c8) split this gap into a warm side and a cold side. It concluded that warm-affinity taxa arrive at about 45% of the spatial expectation, but cold-affinity taxa do not leave. In US birds it gave a warm side of 0.95 and a cold side of -0.53. This "persistence" result is now a main candidate process for the gap. Marine shelf communities were the main counter-case, because Northeast US Shelf assemblages followed most of their spatial gradient (sci:sha256:bec363cb).

We asked three questions:

1. At the species level, what fraction of the occupancy change that each network's own spatial occupancy-temperature curves expect actually occurs, separately for expected gains and expected losses?
2. Is the gain-loss asymmetry a real ecological asymmetry, or does a change that is common to all species cause it?
3. Do marine shelf fish differ from birds, and does the marine community-index (CTI) counter-case hold at the species level?

## 2. Data

- Birds: North American Breeding Bird Survey (BBS), 2026 release. Contiguous US routes, primary observer protocol (RPID 101), runs with RunType 1, landbird taxa (AOU 2880 and higher, no hybrids, no unidentified taxa, no owls or nightjars). East and West of 100 W. Early window 1969-1978, late window 2015-2024. Variant: 1982-1991 and 2010-2019. Temperature: NOAA nClimGrid annual mean at the route start.
- Marine fish, North America: OceanAdapt filtered survey table (12 surveys with at least 25 years from 1982: Aleutian Islands, Eastern Bering Sea, Gulf of Alaska, Gulf of Mexico, Gulf of St. Lawrence North and South, Scotian Shelf summer, Northeast US spring and fall, Southeast US spring, summer and fall). Fish taxa only (OBIS class), binomial names, hauls at 200 m depth or less. Early window = first 10 years from 1982; late window = last 10 years.
- Marine fish, Europe: ICES DATRAS North Sea IBTS quarter 1 (GOV gear, valid hauls, 15-65 min, all species recorded, depth 200 m or less). Windows 1985-1994 and 2015-2024.
- Sea temperature: annual mean SST. The site climatology comes from NOAA OISST v2.1 (0.25 degree, 1982-2025 mean over each 1-degree cell). The change in time comes from NOAA ERSSTv5. We did not use OISST for change in the main analysis, because OISST has a false drop of about 1 C in 2008 in near-shore Southeast US cells, which ERSSTv5 does not show. Variants use OISST alone and ERSSTv5 alone.
- External species temperature index (STI) for marine taxa: the mean World Ocean Atlas 2023 surface temperature over the OBIS geohash-3 cells where the taxon occurs (all oceans, at least 5 cells).

## 3. Method

Site = 1-degree cell (marine) or route (BBS), with at least 3 sampling events (hauls or runs) in each window. For each species i and site s, k_E and k_L are the numbers of events with the species present, and n_E and n_L the numbers of events.

1. Spatial niche curve. For each species, a binomial logistic regression of early occupancy on site temperature (linear and quadratic terms, small ridge penalty). We cross-fit it by spatial blocks (3 x 3 degrees, 5 folds), so a site never contributes to its own curve.
2. Expected change x = g(T_L) - g(T_E). Observed change y = k_L/n_L - k_E/n_E. Expected gains are the species-sites with x > 0. Expected losses are those with x < 0.
3. Raw side ratio = sum(y)/sum(x) on each side (the type of split in sci:sha256:b640c9c8).
4. Corrected side transfer: least squares y = c * g_E(1 - g_E) + B_gain * x+ + B_loss * x-. The first term is a common logit shift c of occupancy for all species (for example observer skill, gear, vessel or richness change). B_all is the same fit with one slope.
5. Calibration. A narrow within-network temperature range makes the fitted curves noisy, and this attenuates B. For each network we simulated data with its own sites, event counts, temperatures and fitted curves as truth. Under full tracking every species-site moves on the logit scale by the change of its curve. lambda = the mean estimate of B under this full tracking (10-20 replicates). Calibrated transfer = B / lambda. Under simulated no tracking the estimator gave values within 0.02 of zero in all networks. We pooled only networks with lambda of 0.3 or more (pre-set rule; this excludes the three Southeast US surveys).
6. Uncertainty: 300 spatial-block bootstrap replicates (3 x 3 degree blocks; 100 for variants), with the niche curves refitted in each replicate. Random-effects pooling (DerSimonian-Laird) over networks.
7. CTI. Occupancy-weighted CTI of each site (mean STI of a detection), spatial slope b_space of early CTI on early temperature, and the CTI ratio = mean CTI change / (b_space x mean warming). We recomputed the CTI ratio with only the species-wide part of y (the species mean over sites) or only the local part (site deviations), and with y = x (full local space-for-time tracking).

Simulation check (Figure 4, `results/sim.csv`): in a 12 C wide design the corrected estimator recovered gain-only, loss-only, half and full tracking within about 0.1, also with a common logit shift of +/-0.3. The raw side ratios were biased by about +/-1 under the same shift. With a 2.5 C range and 100 sites, full tracking gave only 0.47. This is the reason for step 5.

## 4. Results

Main values (95% intervals; Figure 1, Figure 2, `results/main_network_table.csv`, `results/pooled_summary_table.csv`).

| Group | Raw gain ratio | Raw loss ratio | Common shift c (logit) | Calibrated B_all | Calibrated gain | Calibrated loss |
| --- | --- | --- | --- | --- | --- | --- |
| BBS birds, 1969-78 to 2015-24 (2 regions, 1,184 routes) | 0.91 (0.72, 1.09) | -0.44 (-0.75, -0.13) | 0.18 (0.12, 0.24) | 0.14 (0.09, 0.19) | 0.17 (0.07, 0.26) | 0.13 (0.03, 0.23) |
| BBS birds, 1982-91 to 2010-19 | 0.73 (0.53, 0.92) | -0.21 (-0.38, -0.03) | 0.06 (0.03, 0.09) | 0.13 (0.04, 0.21) | 0.11 (0.00, 0.22) | 0.13 (0.05, 0.22) |
| Shelf fish, 10 surveys with lambda of 0.3 or more | 0.27 (0.10, 0.44) | -0.25 (-0.41, -0.08) | 0.12 (-0.01, 0.25) | 0.08 (0.02, 0.14) | 0.05 (-0.03, 0.14) | 0.10 (0.03, 0.16) |
| North Sea IBTS Q1 alone | 0.26 (0.12, 0.41) | -0.37 (-0.52, -0.22) | 0.32 (0.16, 0.48) | 0.05 (0.01, 0.10) | 0.03 (-0.06, 0.11) | 0.07 (-0.01, 0.13) |

Finding 1. The raw split reproduces the published asymmetry: in birds the warm side follows almost fully (0.91) and the cold side moves the wrong way (-0.44). Shelf fish show the same sign pattern (0.27 and -0.25).

Finding 2. A common rise of occupancy for all species causes this asymmetry. In the BBS the common shift was +0.18 logit (mean species per run rose from 45.8 in 1965-69 to 48.6 in 2025). When we removed it, both sides became small and equal: gains 0.17, losses 0.13, difference -0.04 (-0.17, 0.10). The 1982-2019 variant gave the same result. A common shift adds to every expected gain and subtracts from every expected loss. Thus it makes "full warm-side tracking" and "cold-side persistence" from a change that has no relation to temperature. Earlier conclusions that the gap is mainly absent cold-side losses (persistence, extinction debt) do not hold for birds at the species-site level.

Finding 3. Local species occupancy followed only a small part of the spatial expectation in both realms: about 14% in birds and about 8% in shelf fish (calibrated). Uncalibrated within-species slopes (species-wide trends removed) were 0.06 in birds and 0.01 in fish. In shelf fish, the loss side was equal to or larger than the gain side in most variants (difference 0.11, -0.01 to 0.24 in the main analysis; 0.15-0.20 with all depths or OISST; -0.05 with ERSSTv5 windows from the 1970s). Thus there is no evidence that marine communities track better through cold-side losses.

Finding 4. The marine CTI counter-case is real at the community level but does not come from local space-for-time sorting. The CTI ratio was 1.06 and 1.25 in the Northeast US fall and spring surveys and 1.13 in the North Sea (North Sea interval undefined, because the spatial CTI slope is close to zero in some bootstrap samples). But calibrated species-level transfer was 0.55 (-0.11, 1.00), 0.39 (-0.20, 1.08) and 0.05 (0.01, 0.10). In the North Sea, CTI change from species-wide occupancy trends alone gave a ratio of 1.17, and from local deviations alone 0.49 (Figure 5). Species occupancy trends had almost no rank correlation with external STI (Spearman 0.11 North Sea, -0.20 and 0.00 Northeast US) or with their own expected change (0.10, 0.22, 0.25). Over all marine surveys the pooled CTI ratio was 0.37 (-0.03, 0.77) with large heterogeneity (tau 0.45). A few high-occupancy taxa make a large part of CTI change (top five taxa: 23-34% in the Northeast US and North Sea).

Finding 5. The Northeast US common shift (+0.51 and +0.38 logit) is mostly the 2009 change of survey vessel. Before 2009 (1982-1991 to 1999-2008) the shift was +0.14 and -0.06, and CTI still rose more than the spatial expectation, but with only 0.18-0.19 C of ERSSTv5 warming and very wide intervals.

## 5. Interpretation

Two different questions give two different answers. "Do warm-affinity taxa become more common in a warming network?" can give a CTI ratio near 1 (Northeast US, North Sea). "Does each species change at each site as its own spatial temperature curve predicts?" gives about 10% in birds and fish. The second question is the direct test of space-for-time transfer. Its answer is small and similar for gains and losses. Thus the remaining gap is not specific to one side. It is a general weak link between local occupancy change and local thermal expectation. Species-wide changes that the local thermal expectation does not predict (fishing, vessel and observer change, broad population trends) move CTI. Such changes can make CTI ratios large or negative without local thermal sorting. Persistence of cold-affinity species is therefore not a sufficient explanation of the gap. Any gain-loss split must remove the common occupancy shift first.

## 6. Limitations

- Occupancy is presence per event. Abundance changes inside occupied sites are not in the species-level test.
- The sea temperature is surface temperature. For demersal fish, bottom temperature can change differently (for example the Bering Sea cold pool). The ERSSTv5 grid (2 degree) is coarse for small regions.
- The common shift is one value per network on the logit scale. Gear or detection changes that differ among species are not removed. The Northeast US vessel change is such a case.
- The calibration uses the fitted curves as truth. If true curves are steeper or flatter, lambda changes. lambda was below 0.5 in 8 of 13 marine surveys, so their intervals are wide.
- Fishing changed many demersal stocks. We did not model it. It enters the species-wide part of change.
- The North Sea within-network temperature range is only 2.6 C. Annual mean SST is a weak niche axis there, because depth and season structure the community.
- External STIs from OBIS have effort bias and use surface temperature for all taxa.
- BBS: no observer effects. The common shift includes observer change.

## 7. Files

- `files/figures/fig1_network_side_transfer.png`: calibrated gain and loss transfer by network.
- `files/figures/fig2_raw_vs_corrected_pooled.png`: pooled raw and corrected side transfer.
- `files/figures/fig3_binned_obs_vs_exp.png`: observed against expected occupancy change in 20 quantile bins, raw and with the common shift removed.
- `files/figures/fig4_simulation_check.png`: estimator check on simulated communities.
- `files/figures/fig5_cti_parts.png`: CTI ratio and its species-wide and local parts.
- `files/results/`: per-network estimates with bootstrap intervals (`*_summary.csv`, `network_estimates.csv`), calibration replicates (`*_calibration.csv`), pooled values (`pooled_estimates.csv`, `pooled_summary_table.csv`), CTI parts (`cti_parts.csv`), species-level mean occupancy change and CTI contributions (`*_species_contrib.csv`), external STIs (`sti_external_obis_woa23.csv`), simulation (`sim.csv`). Family codes: bbs (main birds), bbs82 (1982-2019 birds), oa (main North American fish), oa_oisst, oa_ersst (ERSSTv5 only, windows from 1965), oa_all (all depths), oa_pre2009 (Northeast US before the vessel change), datras (North Sea).
- `files/code/`: all code. `run_all.sh` gives the order. Retrieval scripts write to local scratch.
- `files/provenance/`: shared-store paths, source URLs and SHA-256 values; hashes of the retrieved DATRAS and OBIS files.
- `files/EXTERNAL_DATA_NOTICE.md`: third-party data terms and attribution.

## 8. Reproduce

From a campaign worktree root with the `datasets/` link: `sh files/code/run_all.sh` (copy `files/code` to a local folder first). It needs internet access for OBIS and ICES DATRAS. Runtime is about 2-3 hours on 2 CPUs. Bootstrap and simulation use fixed seeds; OBIS and DATRAS content can change after 2026-11-11.
