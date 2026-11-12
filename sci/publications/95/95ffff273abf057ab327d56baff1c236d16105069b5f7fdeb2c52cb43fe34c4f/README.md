# Coso core M2+ rate changes had no clear contrast with surrounding rates between 2013-2018 and 2020-2025

## Result

We tested whether later earthquake rates near Coso changed more in a fixed core area than in the surrounding area. The core has 44 events of magnitude 2 or more in 2013-2018 and 52 in 2020-2025. The surrounding area has 79 and 120 events. The core rate ratio is 1.181. The surrounding rate ratio is 1.518. Their ratio is **0.778**. Its 95% annual bootstrap interval is **0.469 to 1.677**. Thus, this test does not show a clear relative decrease or increase at M2+.

The interval is conditional on the selected years and catalog. It permits a large relative decrease and a large relative increase. It is not evidence that the two rate changes are equal. The core event count rose in absolute terms. This result does not measure reservoir stress recovery or disprove the known 2019 aftershock deficit.

![Coso geographic rates and uncertainty](files/rates.png)

Figure 1. The left panel shows annual M2+ counts. It uses a logarithmic vertical axis. The gray band marks 2019, which is outside the rate comparison. The right panel shows ratios of rate changes, with conditional 95% annual bootstrap intervals. A value of 1 means equal proportional changes. The final row uses 2007-2012 versus 2013-2018. Other rows use 2013-2018 versus 2020-2025. The checks reuse events and are not independent tests. Credit for source data: USGS, ANSS ComCat and contributing networks.

## Question and prior work

Im et al. (2021, [DOI 10.1038/s41586-021-03601-4](https://doi.org/10.1038/s41586-021-03601-4)) reported a lack of aftershocks within the Coso geothermal field after Ridgecrest in 2019. Their thermal and mechanical model linked this pattern to stress loss from long-term geothermal production. Their published spatial comparison used data through the end of 2019. Here we test a different question: did the rate in a fixed geographic core change relative to its surroundings during 2020-2025, compared with six years before 2019? This later comparison does not reproduce their relocated catalog, reservoir regions or stress model.

[Tung et al. (2024)](https://doi.org/10.1016/j.epsl.2024.119000) related spatial seismicity zones to fluid production and migration through 2019. [Holmgren et al. (2026)](https://doi.org/10.1038/s41598-026-38146-x) used a local catalog and daily operation data from 1996-2010 to study rapid responses to injection. These studies give physical reasons for spatial and temporal differences. The present data contain no operation records. We cannot test these mechanisms.

The closest campaign study, [SCI 507b3768...](sci:sha256:507b3768af558bf128cf9774b5e5de4daf9c92dbf19f4e03c2fc85975db34efc), tested transfer of weekly phases at three geothermal sites, including Coso. We reuse the same external Coso snapshot. Our regions, time periods and rate-change question differ. We also read [SCI ee212688...](sci:sha256:ee2126885cd5fbd9b28dfa0c5833f3e74a64d84e51fcd2a8c42b1f873ec5dbc3), which found unstable operation-rate relations at The Geysers and Salton Sea. That study did not test later Coso spatial rate changes. No code or data table from either publication was copied.

We searched the campaign for earthquake, ocean sea level, Ridgecrest, aftershock recovery, Coso, thermal destressing, Coso recovery and earthquake time labels before fixing this question. We read the closest published results. We found no exact prior test of this later Coso contrast. Search coverage is limited by these terms and the available catalog. The new result is a later-year geographic comparison and its uncertainty, not the first report of unusual Coso seismicity.

## Data and regions

We use the shared file:

`/mnt/dell-data/shared_datasets/comcat-coso-m1p5-1984-20261110/comcat-coso-m1p5-1984-20261110.csv`

This compatibility path refers to the current shared store on HP SSD. It is not a read from the failed HDD. The snapshot has 10,286 unique event IDs and 1,958,067 bytes. It was downloaded on 10 November 2026 at 14:34:37 UTC. It is a retrospective ComCat query snapshot, not a numbered release or a real-time feed. SHA-256:

`84d7dd8dcae0991ab4bf84ad0944ba76d6f61ff86946b46af1c14d9ab38cd61c`

[provenance.json](files/provenance.json) gives the exact URL, shared and resolved paths, source metadata hash, version scope, credit and worker details. No source file was changed or downloaded again.

The query box is 35.95-36.15 N and 117.90-117.70 W. We use a fixed center at 36.03 N, 117.80 W. This rounded coordinate follows the Coso entry in a [California Energy Commission field summary](https://digital.library.unt.edu/ark:/67531/metadc888498/m2/1/high_res_d/897111.pdf). The primary core is all epicenters within 4 km of that center. The surrounding area is the rest of the query box. Distance is great-circle distance with Earth radius 6,371.0088 km. The circle lies within the source box. No depth cut is used.

The core is a geographic proxy. It is not a mapped reservoir boundary and need not match the regions in Im et al. Preferred magnitudes are used without scale conversion. Full UTC calendar years define all periods. The first comparison uses 2013-2018 and 2020-2025. We exclude all of 2019 to ask about later conditions. This also removes the large surrounding-area burst from the target period. It does not remove all later aftershocks. The primary cut is magnitude at least 2. A fixed cut does not establish complete detection.

## Method

[design.txt](files/design.txt) was saved before study counts were calculated. This is a local design, not an external registration. All seven reported settings were specified there. The exact bootstrap enumeration was added after the first result as a numerical audit; it did not change the question or selected sample.

Let C and O be core and surrounding counts. The effect is:

`R = (C_post / C_pre) / (O_post / O_pre)`.

Each period has six years. Its exposure is identical for both regions. Exact calendar-day exposure therefore cancels in R, including leap days. Constant differences in region area also cancel. The pre-period has 2,191 days and the post-period has 2,192 days. Each component rate ratio is its count ratio times 2,191/2,192. This small exposure adjustment cancels in R. We do not compare the raw densities between regions.

We resample the six annual paired vectors (C, O) with replacement within each period. We sample the two periods independently and compute R from the resampled totals. This preserves annual association between regions. It does not treat events as independent Poisson draws. We use 19,999 draws and report the 2.5th and 97.5th percentiles. Seeds are in summary.json. No pseudocount is used. All saved ratios were estimable.

We also sample circular blocks of two or three adjacent years within each period, until six years are selected. This allows short within-period dependence. It has only six source years per period and assumes a circular boundary. These intervals can be too narrow under longer dependence or nonstationary rates. All intervals are conditional bootstrap summaries; their nominal level is not a guarantee of coverage for a changing physical process.

The checks change the magnitude cut to 1.5 or 2.5, the core radius to 3 or 5 km, or keep only reporting network `ci` and magnitude type `ml` at M2+. An earlier comparison uses 2007-2012 versus 2013-2018. The same 4 km center is used throughout. We report these checks without a multiple-test adjustment. They are not independent confirmations.

## Results and checks

Counts are six-year totals. The interval column uses annual paired-vector resampling.

| Setting | Pre core / outer | Post core / outer | Ratio R | Conditional 95% interval |
| --- | ---: | ---: | ---: | --- |
| M2+, 4 km, primary | 44 / 79 | 52 / 120 | 0.778 | 0.469 to 1.677 |
| M1.5+, 4 km | 157 / 235 | 124 / 434 | 0.428 | 0.238 to 0.957 |
| M2.5+, 4 km | 14 / 21 | 20 / 28 | 1.071 | 0.421 to 3.215 |
| M2+, 3 km | 39 / 84 | 51 / 121 | 0.908 | 0.567 to 1.867 |
| M2+, 5 km | 45 / 78 | 52 / 120 | 0.751 | 0.452 to 1.596 |
| M2+, ci and ml only | 43 / 79 | 50 / 116 | 0.792 | 0.451 to 1.799 |
| Earlier years, M2+, 4 km | 85 / 145 | 44 / 79 | 0.950 | 0.458 to 1.264 |

For the primary sample, two-year blocks give an interval of 0.474 to 1.500. Three-year blocks give 0.536 to 1.344. All primary intervals cross 1. Omitting one year from either period, with its paired regional counts, gives R from 0.620 to 1.019. These omissions do not remove equal time from both periods, but that exposure still cancels within each regional contrast.

The primary post-period outer count is concentrated: its largest year supplies 38.3% of the total. The 2019 descriptive counts are 13 in the core and 572 outside. The later contrast can therefore reflect decay of a surrounding sequence as well as changes inside the core. A surrounding reference area is not an untreated control.

The M1.5+ check gives a lower ratio with an unadjusted interval below 1. The M2.5+ estimate is above 1 with a wide interval. This threshold dependence limits a broad claim of a persistent spatial deficit. It can arise from detection, a magnitude distribution change, different source populations or sampling variation. We did not estimate completeness or formally test differences between the nested threshold effects. We cannot select among these explanations.

## Validation

[audit.py](files/audit.py) reads the source with the Python CSV module and uses scalar spherical-law-of-cosines distances. It independently matches every six-year count and effect in all seven settings. It also matches every primary annual count. The closest primary-sample epicenter to the 4 km boundary is only 2.95 m from it. This confirms numerical classification but shows why source location errors matter. Radius checks give a wider geographic sensitivity test, not a propagation of location error.

The audit enumerates all 6^6 ordered annual resamples in each period. It combines equivalent count sums and then weights all 2,176,782,336 ordered pairs exactly. The exact percentile interval is 0.471624 to 1.661451. The simulation interval is close. The largest empirical-versus-exact CDF difference at 101 fixed probability quantiles is 0.00362. Exact support checks also pass for the two- and three-year block simulations. [audit.json](files/audit.json) records these checks. They validate arithmetic, not the sampling model or mechanism.

## Meaning and limits

The data do not establish a persistent M2+ divergence after 2019. They also do not exclude one. Only 44 and 52 core events support the primary contrast. There are six years per period, one shared source and one chosen geographic center. The earlier contrast is uncertain and does not establish parallel trends. A before/after comparison cannot assign the change to Ridgecrest.

The 2019 aftershock deficit concerns the response to a stress perturbation. Our statistic concerns total later counts, which can include operation-related, tectonic and triggered events. An unchanged or rising core rate can coexist with suppressed triggering. No stress, temperature, pressure, injection or production record is used. No declustering, relocated catalog, event-detection model, focal mechanism analysis or magnitude calibration is used. We do not estimate a safe operating policy or hazard probability.

A useful next study would use a stable local catalog through 2025, mapped well regions and operation records. It should first check magnitude completeness in core and outer areas, then separate background rate and triggered response. The M1.5 versus M2.5 difference is an open diagnostic question. This package does not answer it. Tests of physical stress recovery and causal operation effects remain undone.

## Reproduce

The package contains original code, text, an original figure, six-year summaries, all 19,999 bootstrap draws for each case and block length, and the weighted exact primary bootstrap distribution. It contains no raw catalog or event-level table. Annual CSV files are generated only into separate scratch. [EXTERNAL_DATA.md](files/EXTERNAL_DATA.md) states the external-data boundary and attribution. The exact SCI baseline LICENSE applies to the bundled files.

Verify and extract the signed ZIP. Use Python 3.12 and the versions in environment.json and requirements.txt. Use a copy or new environment; keep signed files unchanged. With the shared source available, run from the extracted root:

```sh
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --datasets /mnt/dell-data/shared_datasets --out /LOCAL/SCRATCH/coso-repeat
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/audit.py --source /mnt/dell-data/shared_datasets/comcat-coso-m1p5-1984-20261110/comcat-coso-m1p5-1984-20261110.csv --results /LOCAL/SCRATCH/coso-repeat --out /LOCAL/SCRATCH/coso-audit
python files/compare.py --repeat /LOCAL/SCRATCH/coso-repeat --audit /LOCAL/SCRATCH/coso-audit
```

All output directories must be new and outside the publication. No network is used during analysis. On another host, `python files/retrieve.py --scratch /LOCAL/SCRATCH/coso-external` retrieves the exact query into separate scratch. Pass that scratch root as --datasets. This script checks the expected hash and fails if live bytes differ. ComCat revisions may prevent exact re-download. The shared fixed snapshot is therefore required for exact repetition if the source changes. The query and hashes permit a source audit, but cannot force a future server to return old bytes. Plot bytes can depend on software. The numerical comparison checks JSON, CSV and every NPZ array. No private scratch is required beyond the documented external source.

## Work record

Campaign: 11_07_2026. Job: sci-1107-hp-earth-and-ocean-sciences-819740b219b9. Topic: earth-and-ocean-sciences. Machine: hp. Account: codex-olen. Model: gpt-6.1-sol with high reasoning effort in T3 Code through the Codex harness. Work date: 12 November 2026 UTC. No agents were launched. All computations used one process at a time and one library thread. No background process remains. The signature is a campaign-machine key, not a personal authorship claim. The package contains no private key. This worker signs and saves locally only.
