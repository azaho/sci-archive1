# Remeasured US forest plots: small, mortality-driven tree community warming in the West and the East, 2001-2025

Job: sci-1107-dell-climate-pollution-biodiversity-4e943ba5eb01 (campaign 11_07_2026). Topic: climate-pollution-biodiversity. Machine: dell. Model: Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Rosenblad, Baer and Ackerly (2023, PNAS, doi:10.1073/pnas.2301754120) found that tree communities on remeasured Forest Inventory and Analysis (FIA) plots in 10 western US states became composed of warmer-climate species ("thermophilization") between 2000-2008 and 2010-2018. They reported these claims:

1. The community temperature index (CTI) increased by about 0.039 C per decade.
2. This was about one tenth of the local warming.
3. Differential tree mortality was the strongest demographic driver, not growth or recruitment.
4. Thermophilization was about 3 times faster where insect damage was recorded.
5. Each 1 C of warming was associated with 0.112 C of thermophilization.
6. Thermophilization was faster on north-facing slopes.

We tested these claims again with the full FIA DataMart (downloaded 2026-11-09) in four samples: the same western states and era, the same western states in a new period (second survey 2019-2025), and 37 eastern states (an independent region) in two periods. We added a test that the original study did not have: a permutation of the species thermal index (STI) among species. This test asks if the measured CTI change is larger than the change that a random species trait would show with the same tree demography.

Main results (CTI change in C per decade, mean of plots, 95% intervals from a 2-degree spatial block bootstrap):

| Sample | Plot pairs | Net CTI change | Mortality part | Growth part | Recruitment part | Harvest part | Air warming trend | Ratio |
|---|---|---|---|---|---|---|---|---|
| West, T1 2000-08, T2 2010-18 | 18,020 | 0.018 [0.008, 0.029] | 0.017 [0.010, 0.025] | -0.000 [-0.003, 0.002] | 0.000 [-0.002, 0.003] | 0.003 [0.001, 0.005] | 0.16 [0.13, 0.20] | 0.11 |
| West, T2 2019-25 | 14,358 | 0.015 [0.004, 0.025] | 0.016 [0.009, 0.022] | 0.000 [-0.002, 0.003] | -0.000 [-0.002, 0.002] | 0.002 [0.000, 0.004] | 0.28 [0.25, 0.31] | 0.05 |
| East, T2 2001-18 | 107,691 | 0.016 [0.002, 0.029] | 0.025 [0.019, 0.031] | 0.002 [-0.002, 0.004] | -0.004 [-0.010, 0.002] | -0.004 [-0.014, 0.006] | 0.24 [0.22, 0.27] | 0.07 |
| East, T2 2019-25 | 55,139 | 0.014 [0.003, 0.025] | 0.028 [0.022, 0.034] | 0.004 [0.001, 0.006] | -0.005 [-0.010, 0.000] | -0.007 [-0.013, -0.001] | 0.37 [0.32, 0.43] | 0.04 |

What repeated:

- A small positive CTI change occurred in all four samples (0.014-0.018 C per decade). It was 4-11% of the local air warming trend (claim 2 repeated, with an even larger lag after 2019).
- Natural mortality gave the largest positive part in all four samples (claim 3 repeated). In the East, recruitment and harvest moved the CTI in the opposite direction and removed about half of the mortality part.
- In the West, plots with recorded insect disturbance changed 7-9 times faster than other plots in both periods (0.081 vs 0.011 and 0.077 vs 0.009 C per decade; claim 4 repeated and was stronger). In the East, insect disturbance gave no clear difference (difference -0.000 [-0.047, 0.045] and 0.018 [-0.009, 0.043]).

What did not repeat:

- The western net rate was about half of the published 0.039 C per decade. Our interval [0.008, 0.029] does not include 0.039. Method differences (STI source, tree weights) can explain part of this difference (see Limitations).
- The slope of CTI change on local warming was 0.037 [0.001, 0.073] per C in the original western era (smaller than 0.112), -0.010 [-0.050, 0.031] in the new western period, 0.051 [0.030, 0.073] in the early East and -0.050 [-0.075, -0.025] in the late East. The sign was not stable, so claim 5 did not repeat.
- North-facing slopes did not show clearly faster change in the West (0.009 [-0.007, 0.025] and 0.007 [-0.014, 0.027] C per decade per unit northness; claim 6 did not repeat). The early East sample had a positive northness slope (0.025 [0.001, 0.048]); the late East sample did not (-0.001 [-0.026, 0.024]).
- Fire was linked to faster change only in the original western era (difference 0.066 [0.021, 0.114]), not in the new western period (-0.002 [-0.055, 0.060]).

The main caution: in all four samples, the observed net CTI change was inside the distribution produced by random permutation of STI values among species (two-sided permutation p = 0.63-0.74; permutation SD 0.026-0.041 C per decade). The demographic changes of a small number of abundant species (for example Douglas-fir and lodgepole pine mortality in the West; loblolly pine recruitment, red maple and balsam fir mortality in the East) control the CTI. A random species trait gives a shift as large as the thermal shift in about two thirds of the permutations. Thus the positive CTI change is real for the thermal index, but these data do not show that thermal niche, rather than species-specific causes such as insect outbreaks, pathogens and stand development, selected the species that died or recruited.

In the West, the CTI change came almost fully from disturbed plots: plots without any recorded disturbance or treatment had 0.005 [-0.002, 0.012] and 0.005 [-0.001, 0.011] C per decade. In the East, undisturbed plots had a larger change (0.023 [0.013, 0.033] and 0.024 [0.014, 0.033]), and harvest lowered the CTI (plots with cutting: -0.032 and -0.071 C per decade, vs 0.023 and 0.025 without cutting).

## Figures

- `files/figures/fig1_components.png`: net CTI change and the parts from mortality, growth, recruitment and harvest for the four samples, and CTI change next to the local air warming trend.
- `files/figures/fig2_disturbance.png`: differences in CTI change between plots with recorded insect, fire or harvest disturbance and other plots.
- `files/figures/fig3_map.png`: map of 1-degree cell mean CTI change for the two periods.
- `files/figures/fig4_placebo.png`: observed net CTI change compared with 500 random permutations of STI among species.

## Data

- FIA DataMart state CSV tables PLOT, COND, SUBPLOT and TREE for the 48 conterminous states, and REF_SPECIES.csv, from `https://apps.fs.usda.gov/fia/datamart/CSV/<ST>_<TABLE>.zip`, downloaded 2026-11-09 (192 files, 3.09 GB). SHA-256 values of every file used: `files/provenance/fia_datamart_sha256.txt`. These are US Government (USDA Forest Service) public data. Public plot coordinates are perturbed by the FIA program (up to about 1.6 km, with swapping of some private plots).
- NOAA NCEI nClimGrid monthly mean temperature and precipitation (5 km grid, 1895-2026-09), shared campaign dataset copies `datasets/noaa-nclimgrid-monthly-tavg-20261006/nclimgrid_tavg.nc` (sha256 b781f5ee586c1b9de5334a65453bb6e6888da43c959ba8d306f2d1e7f59d83c7) and `datasets/noaa-nclimgrid-monthly-prcp-20261006/nclimgrid_prcp.nc` (sha256 1d9f6cb28dd8ed203ed512ad9083f5a5252dedd85ac58cf155a33582b36459fb), source `https://www.ncei.noaa.gov/data/nclimgrid-monthly/access/`. Provenance records: `files/provenance/`.

The raw FIA and nClimGrid files are not bundled because of their size. `files/DATA_NOTICE.md` gives sources, terms and attribution.

## Methods

Plot pairs. A pair is an annual-inventory plot measurement (KINDCD 2) and its previous annual measurement (KINDCD 1 or 2, linked by PREV_PLT_CN). Both measurements must have PLOT_STATUS_CD 1, QA_STATUS 1 (or missing), and all sampled conditions in accessible forest (COND_STATUS_CD 1), as in the original study, which excluded partly forested plots. Only subplots 1-4 with SUBP_STATUS_CD 1 at both times are used.

Trees. Live trees with diameter 12.7 cm (5.0 in) or more at T1 are followed to T2 through PREV_TRE_CN. The fate is survivor (STATUSCD 1), natural death (STATUSCD 2 with a cause other than silvicultural), or harvest (STATUSCD 3, or STATUSCD 2 with AGENTCD 80, which is how annual inventories code most cut trees). Trees without a T2 status are removed from both times. Recruits are T2 live trees of 12.7 cm or more that were saplings at T1 or have RECONCILECD 1 or 2 (ingrowth or through-growth). Each tree has the weight basal area x TPA_UNADJ (m2 per ha), so subplot and macroplot trees are combined with their design weights. The original study used trees within 7.32 m of the subplot centre; the public TREE table does not contain the distance field now, so this exact rule is not possible.

Species thermal index. STI is the mean 1981-2010 nClimGrid annual mean temperature over all FIA forest plots where the species occurred (live, 12.7 cm or more) at the first annual measurement of the plot, over the 48 states. We used the 285 species with 20 or more occurrence plots (they hold 99.97% of the basal area). Sensitivity versions: basal-area-weighted mean, median, and region-specific (West or East) means. The original study used modelled niche means from CHELSA climate over the western range.

CTI and its parts. Subplot CTI is the weighted mean STI. The net change uses T1 trees and T2 survivors plus recruits. The parts follow the original study: mortality (dead trees removed, sizes at T1, no recruits), growth (survivor sizes at T2, dead and cut trees at T1 size, no recruits), recruitment (all T1 trees at T1 size plus recruits), and harvest (cut trees removed). The change is divided by the remeasurement interval and given per decade. Plot values are subplot means.

Climate change at plots. Local warming trend: least-squares slope of annual mean temperature from T1-10 to T2 (to 2025). Window change as in the original study: mean of T1-4 to T1+10 (truncated at 2025) minus mean of T1-19 to T1-5.

Disturbance. Condition disturbance codes recorded at T2 (DSTRBCD 10-12 insect, 20-22 disease, 30-32 fire, 50-54 weather) and treatment code TRTCD 10 (cutting).

Samples. West = AZ, CA, CO, ID, MT, NV, NM, OR, UT, WA (the original 10 states). Sample West A: T1 2000-2008 and T2 2010-2018 (the original design). West B: T2 2019-2025. East = the 37 states of the FIA Northern and Southern regions. East A: T2 2001-2018; East B: T2 2019-2025. Eastern plots are remeasured every 5-7 years, so one plot can give more than one pair in a sample.

Statistics. Means of plot values with 2000 bootstrap draws of 2 x 2 degree spatial blocks. Regressions of plot CTI change on disturbance flags, window warming, and baseline climate, and of subplot change on northness (cos(aspect) x sin(slope)), use cluster-robust standard errors by 2-degree block. Placebo: 500 random permutations of STI among the species that occur in each sample, with the full net change computed again each time. Species parts use the exact identity that subplot CTI change equals the sum over species of (share at T2 minus share at T1) x (STI minus CTI at T1).

## Files

- `files/results/main/summary.csv`: all sample estimates (rates, parts, warming, disturbance contrasts with intervals).
- `files/results/main/regressions.csv`: disturbance, warming and northness regressions.
- `files/results/main/placebo_sti_permutation.csv` and `perm_*.npy`: permutation test.
- `files/results/main/plot_rates.csv.gz`: one row per plot pair (FIA plot CNs, years, perturbed public coordinates, climate, CTI change parts, disturbance flags). This table holds all values behind the main estimates.
- `files/results/species_thermal_index.csv`: STI per species (all versions) with occurrence counts.
- `files/results/contrib/species_contributions.csv`: species parts of the CTI change by sample and process.
- `files/results/sti_*` and `files/results/var_*`: sensitivity versions (BA-weighted STI, median STI, regional STI, no cut plots, no disturbed or treated plots, no woodland species).
- `files/code/`: all code. `files/provenance/`: input hashes.

## Reproduction

1. `bash files/code/00_get_fia.sh SCRATCH/fia/raw` (downloads 192 zips, about 3.1 GB, into local scratch; compare with `files/provenance/fia_datamart_sha256.txt`; FIA updates its tables, so new downloads can differ). Download `https://apps.fs.usda.gov/fia/datamart/CSV/REF_SPECIES.csv` into `SCRATCH/fia/`.
2. Get nClimGrid `nclimgrid_tavg.nc` and `nclimgrid_prcp.nc` from NOAA NCEI into `DATASETS/noaa-nclimgrid-monthly-{tavg,prcp}-20261006/`.
3. `bash files/code/run_states.sh WORKDIR` (extracts columns and builds plot pairs per state; WORKDIR contains `scratch/` and `code/`).
4. `bash files/code/run_all.sh WORKDIR DATASETS` (climate grids, STI, analysis, sensitivity versions, species parts, figures). Python 3.12 with numpy, pandas, pyarrow, xarray, netCDF4, statsmodels and matplotlib. The full run took about 25 minutes on a shared 24-core host. Random seed 20261109.

## Limitations

- The STI is a simple niche mean from FIA plots in the conterminous US. Ranges that continue into Canada or Mexico are cut, so northern species have STI values that are too warm and southern species values that are too cool. The eastern result depended on the STI version: with basal-area-weighted or median STI, the eastern net change was 0.008-0.010 C per decade and its intervals included zero. The western result stayed positive with all versions.
- We could not apply the 7.32 m tree-distance rule of the original study. We used design weights for subplot and macroplot trees instead. This and the STI source can explain part of the lower western rate.
- Disturbance codes are coarse condition-level flags and their recording changed over time (for example the insect share in the East went from 2% to 9% of plots between the two samples).
- Eastern samples contain repeated intervals of the same plots, and remeasurement intervals differ between regions (about 10 years in the West, 5-7 years in the East). Rates per decade from short intervals have more noise.
- The permutation test shows that the CTI change is small compared with species turnover. It does not show that climate has no part; it shows that these data cannot separate a thermal cause from species-specific causes.
- Plot coordinates are perturbed, so plot climate values have small errors.

## Related campaign work

Campaign studies of bird communities found similar lags behind warming: Breeding Bird Survey species centroids moved at about 14% of the isotherm shift (sci:sha256:7714830c552415458e0fbece8fb93ae05d88d18000b801144071d2993a034a3e), and winter feeder-bird CTI rose without a clear link to local winter temperature (sci:sha256:c94acf78273342e4059d41fb6b8494821e7960ffeaf617f2c1e88631488fe9f2).
