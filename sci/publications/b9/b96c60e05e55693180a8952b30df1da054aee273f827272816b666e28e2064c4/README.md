# Northward tree seedling offsets did not pass to new saplings and predicted adult shifts only on disturbed plots (121,814 remeasured eastern US forest plots, about 2002 to 2022)

Job: sci-1107-dell-climate-pollution-biodiversity-8aeca3d19041. Topic: climate-pollution-biodiversity. Machine: dell. Model: Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Many studies use the position of tree seedlings relative to adult trees as an early sign of climate-driven range shift. Woodall et al. (2009) found that, for many eastern US species, seedlings in one Forest Inventory and Analysis (FIA) survey were more than 20 km north of adult trees. They read this as migration at up to 100 km per century. Zhu, Woodall and Clark (2012) used a larger single survey and did not find general range expansion. Both studies used one survey. They could not see what happened to the seedlings.

FIA now has plots that crews measured two or more times, about 20 years apart. This lets us do a forward test of the indicator:

1. Does the seedling minus adult offset at the first visit predict where the adult distribution of the same species moved by the last visit?
2. Do the new saplings at the last visit grow where the first-visit seedlings were (the cohort that the indicator is about)?
3. Do survey effects (state crews, protocols, or state-level management) change seedling counts, and how much of the offset do they cause?

## 2. Data

- USDA Forest Service FIA DataMart CSV tables (PLOT, COND, SEEDLING, TREE, REF_SPECIES) for 31 eastern states: AL AR CT DE FL GA IL IN IA KY LA ME MD MA MI MN MS MO NH NJ NY NC OH PA RI SC TN VT VA WV WI. Files dated 6-7 November 2026, downloaded 9 November 2026. Public domain. File hashes are in `files/provenance/fia_datamart_SHA256SUMS.txt`.
- NOAA nClimGrid monthly mean temperature (shared campaign copy, SHA-256 b781f5ee...). Public domain. We use it only to give each plot a 1991-2020 mean annual temperature.
- See `files/NOTICE-external-data.md` for sources, terms and citations.

## 3. Method

### 3.1 Fixed plot panel

- We kept annual-design visits (KINDCD 1 or 2), sampled plots (PLOT_STATUS_CD 1 or 2) and base sample intensity.
- For each plot location we used the first visit (t1, not later than 2010) and the last visit (t2). We kept plots with t2 - t1 of 10 years or more.
- Result: 121,814 plots in 2,012 counties. Median t1 is 2002. Median t2 is 2022. The mean gap is 19.8 years.
- Because the plot set is fixed, a change in a species centroid comes from demography (growth, death, recruitment, harvest, land use change). It does not come from a change in where crews sampled.

### 3.2 Stages and centroids

- Seedling: live stem below 1 inch (2.5 cm) diameter, from the SEEDLING table (microplots).
- Sapling: live tree 1.0 to 4.9 inches (2.5 to 12.6 cm) diameter (microplots).
- Adult: live tree 5 inches (12.7 cm) or more (subplots). We also use adult basal area.
- New saplings (recruits): saplings at t2 whose subplot and tree number was not a live tallied tree at t1 on the same plot. They are 76.5% of t2 sapling stems.
- Adult ingrowth: adults at t2, 5 to 11.9 inches, that were not adults at t1.
- For each species, stage and visit we calculate the stem-weighted mean position of the plots: latitude (km), longitude (km), and plot mean annual temperature (C). Plot temperature is fixed in time, so a temperature centroid change shows a move of the species to warmer or cooler plots.
- We kept 104 species with seedlings and adults on 150 or more t1 plots each.

### 3.3 Tests

- Seedling offset at t1: seedling centroid minus adult centroid (the Woodall indicator).
- Forecast tests: across species, we regress a later change on a t1 offset. Examples: adult centroid change (t2 minus t1) on the seedling minus adult offset; new-sapling centroid minus t1 sapling centroid on the seedling minus sapling offset. If seedlings move into the next stage at the same places, the second slope is 1.
- Split-sample design: we split plots at random into two halves. We calculate the predictor in one half and the outcome in the other half, in both directions, and take the mean over 40 random splits. This removes the shared sampling error that causes false negative or positive slopes when the same t1 centroid is in the predictor and the outcome. We also give an instrumental-variable slope (the predictor from the other half is the instrument) that corrects for noise in the predictor, and a rank (Spearman) correlation that is robust to a few high-leverage species.
- Uncertainty: county cluster bootstrap (500 replicates for all plots, 200 for subsets), with a new random split in each replicate. The county bootstrap adds noise to the split-sample statistics and moves their bootstrap distribution down. For this reason we give normal intervals: estimate plus or minus 1.96 bootstrap standard errors (standard error = width of the 2.5 to 97.5 percentile range divided by 3.92). The raw percentiles are in `files/results/forecast_tests_all_subsets.csv`.
- Placebo direction: the same tests in east-west position. A climate-driven northward indicator should work better north-south than east-west.
- Within-state offset: the seedling minus adult difference calculated inside each state, then averaged with adult-abundance weights. This removes differences between states.
- Subsets: all plots; no harvest and no planting or artificial regeneration between t1 and t2 (90,569 plots); fully forested at both visits (41,430 plots); states where at least 90% of large (20 inches or more) t2 trees matched a t1 tree number (48,050 plots); t1 in 2004 or earlier (96,451 plots).
- State border test: we paired each forested plot with its nearest forested plot in another state within 15 km (unique pairs) and compared the log stem density of seedlings, saplings and adults across each state border. Same-state pairs at the same distances give the reference. If there is no state effect, the mean squared z of the border jumps is about 1 (upper 97.5% limit about 1.7 for 23 borders).

## 4. Results

All values are means across species with 95% normal bootstrap intervals, all plots, unless the text gives a subset. `files/results/key_numbers_table.csv` has all values for all subsets.

### 4.1 The Woodall offset is present but it decreased and it is mostly between states

- At t1, seedling centroids were 27 km [20, 34] north of adult centroids, and 57% [52, 62] of species had seedlings north of adults. This agrees with Woodall et al. (2009).
- At t2, on the same plots, the offset was 14 km [7, 20], and 50% [45, 55] of species had seedlings north of adults.
- Inside states the offset was only 3.0 km [1.2, 4.8]. Thus about 90% of the offset comes from differences between states.
- Seedlings were on plots 0.18 C [0.12, 0.24] cooler than adults at t1 and 0.10 C [0.04, 0.15] cooler at t2.
- The offset of a species is persistent: the split-sample rank correlation of the t1 and t2 offsets is 0.64 [0.57, 0.71], and the slope is 0.65 [0.47, 0.83].

### 4.2 New saplings did not grow where the seedlings were (Figure 2)

- Across species, the seedling minus sapling offset at t1 did not predict the position of the new saplings at t2: slope 0.08 [-0.01, 0.17], rank correlation 0.04 [-0.06, 0.15]. The expected slope for full transfer is 1.
- The result is the same in the four other subsets (slopes -0.06 to 0.07; rank correlations -0.02 to 0.04). It is the same for plot temperature (slope 0.07 [-0.02, 0.17]).
- On average, new saplings were 29 km [22, 35] south of the t1 seedlings, and only 3.9 km [-1.6, 9.4] from the t1 saplings. The new saplings grew where saplings already were.
- In the east-west placebo direction, seedling offsets did partly transfer to new saplings (slope 0.34 [0.16, 0.52], rank correlation 0.16 [0.06, 0.26]). Thus the seedling layer carries real east-west information, but its north-south offset did not pass to the next stage.
- In contrast, sapling positions did pass to adult ingrowth: the sapling minus adult offset predicted the position of new adults, slope 0.60 [0.41, 0.79], rank correlation 0.52 [0.44, 0.61]. The rank correlation was 0.45 to 0.52 in all subsets.

### 4.3 Adult shifts followed seedling offsets only on disturbed plots (Figure 1, Figure 3)

- On all plots, species with more northern seedlings had more northern adult shifts: slope 0.38 [0.23, 0.52]. But the rank correlation was only 0.18 [0.10, 0.27], and two taxa with very large offsets (willow spp. and American hornbeam) had high leverage.
- On plots with no harvest and no planting, the slope was 0.05 [0.01, 0.09]. On plots fully forested at both visits, it was 0.01 [-0.03, 0.05]. With basal area weights, these slopes were 0.03 [-0.02, 0.07] and 0.00 [-0.04, 0.05].
- A joint model with both the sapling minus adult offset and the seedling minus sapling offset showed that the seedling layer added nothing on undisturbed plots (no harvest: -0.03 [-0.07, 0.02]; fully forested: -0.06 [-0.10, -0.02]). On all plots it added 0.31 [0.14, 0.49].
- The weak positive rank correlation in undisturbed plots (0.13 [0.04, 0.22] fully forested) was not specific to north-south position. The east-west rank correlation was similar (0.21 [0.12, 0.30]).
- Northern and southern range limits (90th and 10th percentile latitudes) gave slopes near zero on fully forested plots (-0.02 [-0.10, 0.06] and 0.07 [-0.02, 0.16]).

### 4.4 Adults moved north on average, but less than the climate warmed

- Adult centroids moved 14 km [11, 17] north between t1 and t2 on the fixed plots (6.8 km [4.0, 9.6] on fully forested plots). 60% [55, 64] of species moved north.
- Adults moved to plots 0.13 C [0.10, 0.15] cooler (0.06 C [0.04, 0.08] on fully forested plots). The panel plots warmed 0.94 C between the 1971-1990 and 2005-2024 means, about 0.55 C per 20 years. Thus the demographic move of adults compensated about one quarter or less of the warming.
- The pooled adult stems of all study species did not move clearly (2 km [-8, 13]; 0.01 C), so the species mean shift is not a simple result of a regional change in total stem density. But this baseline changed when we removed harvested plots (28 km [14, 41]), so the mean northward shift is sensitive to the plot set.

### 4.5 Seedling counts change at state borders (Figure 4)

- Across 23 state borders at t1, seedling density jumps had a mean squared z of 4.7, and 30% of borders had |z| > 2. For adults the values were 1.4 and 13%; for saplings 1.5 and 9%. Same-state reference pairs gave 0.9 to 1.0.
- At t2 the seedling value decreased to 2.7 (adults 1.2, saplings 1.8).
- Thus state-level effects on seedling counts are strong. They can come from crews, from protocol differences, or from real state-level causes (for example deer management). They explain why most of the Woodall offset is between states.

## 5. Interpretation

The seedling minus adult offset is a stable property of each species, but it is not a reliable leading indicator of where the next cohort will be. In 20 years the north-south part of the seedling offset did not pass to new saplings, and adult shifts followed the seedling offset only where harvest, planting or land use change occurred. Most of the offset comes from differences between states, and seedling counts jump at state borders more than adult counts. We conclude that the single-survey seedling offset in FIA should not be read as climate-driven migration without (a) a within-state comparison, (b) a fixed plot set, and (c) a check of the next stage.

Adult tree distributions did move north and to cooler plots on fixed plots in 2002-2022. That move was small relative to the warming of the same plots. It came from adult demography and disturbance, not from a seedling front.

## 6. Limitations

- FIA public coordinates are perturbed by up to about 1.6 km, and some private plots are swapped within a county. This adds noise to plot temperature and to the border test, but it is small relative to centroid offsets of tens of km.
- Tree-number matching is not perfect: 88.8% of t2 trees 20 inches or more matched a t1 tree number (69% to 100% by state). Unmatched survivors make new-sapling and ingrowth centroids more similar to the old ones. The subset with good matching gave the same new-sapling result.
- New saplings at t2 include stems that germinated after t1. The test asks whether the t1 seedling geography passes to the next stage, not whether each t1 seedling survived.
- The 104 species include genus-level codes (for example willow spp.). These and a few rare species have large, noisy offsets. Rank correlations reduce their effect.
- The temperature centroid uses 1991-2020 normals at fixed plots. It does not use microclimate, elevation detail or soil.
- The border test cannot separate crew or protocol effects from real state-level ecological causes such as deer density or forest policy.
- We did not model species traits, browsing or seed dispersal. We did not test western US forests.

## 7. Reproduction

- `files/code/run_all.sh SCRATCH NCLIMGRID_TAVG_NC` runs everything from the raw downloads (about 2.2 GB of FIA zips; about 1 hour on 24 cores). Use a scratch folder outside this bundle.
- `files/code/run_all.sh SCRATCH "" 1` starts from the bundled panel tables `files/data/panel_plots.parquet` and `files/data/panel_stage.parquet` (steps 04-07, about 15 minutes).
- Steps: `00_get_fia.sh` (download), `01_extract.py` (compact tables per state), `02_climate_grids.py` (nClimGrid normals), `03_panel.py` (fixed plot panel, recruits, disturbance flags), `04_analysis.py` (centroids, split-sample tests, county bootstrap), `05_border_test.py` (state border test), `06_figures_tables.py` (figures and tables), `07_report_numbers.py` (normal intervals).
- Software: Python 3.12.16, pandas 3.1.1, numpy 2.5.4, scipy 1.18.1, matplotlib 3.11.2, xarray 2026.9.0. Random seed 20261109.
- Hashes of the bundled derived files: `files/provenance/derived_SHA256SUMS.txt`. Panel build log: `files/provenance/03_panel.log`.

## 8. Files

- `files/figures/fig1_adult_shift_vs_seedling_offset.png`, `fig2_recruit_transfer.png`, `fig3_slopes_by_subset.png`, `fig4_state_border_test.png`.
- `files/results/key_numbers_table.csv` and `key_numbers_normal_intervals.csv`: main numbers with normal intervals.
- `files/results/forecast_tests_all_subsets.csv`: all split-sample tests (OLS, IV, Pearson, Spearman; bootstrap percentiles).
- `files/results/species_mean_stats_all_subsets.csv`: means across species and fractions of positive values.
- `files/results/species_table_<subset>.csv`: per-species centroids, offsets, shifts and bootstrap standard errors.
- `files/results/border_summary.csv`, `border_jumps.csv`: state border test.
- `files/data/`: derived fixed plot panel (public domain inputs).

## References

- Woodall, C. W., et al. (2009). An indicator of tree migration in forests of the eastern United States. Forest Ecology and Management 257, 1434-1444. doi:10.1016/j.foreco.2008.12.013
- Zhu, K., Woodall, C. W., Clark, J. S. (2012). Failure to migrate: lack of tree range expansion in response to climate change. Global Change Biology 18, 1042-1052. doi:10.1111/j.1365-2486.2011.02571.x
- Fei, S., et al. (2017). Divergence of species responses to climate change. Science Advances 3, e1603055. doi:10.1126/sciadv.1603055
- Vose, R. S., et al. (2014). Improved historical temperature and precipitation time series for U.S. climate divisions. Journal of Applied Meteorology and Climatology 53, 1232-1251. doi:10.1175/JAMC-D-13-0248.1
