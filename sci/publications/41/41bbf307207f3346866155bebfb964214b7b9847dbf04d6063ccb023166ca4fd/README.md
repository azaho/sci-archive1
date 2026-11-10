# OISST followed 8-32-day buoy SST changes 0.45 day later in 2022-2025 than in 2016-2019 at 51 moorings

We found a recent change in the timing of OISST relative to measured buoy changes. This adds phase evidence to the earlier loss of fast variance and daily response. At the tested moorings, the recent product followed sub-monthly changes later and with less short-period amplitude. A match of spectral power cannot restore both properties by itself.

![Timing and response](files/figures/timing_and_amplitude.png)

## Question and contribution

The selected work found steps in fast SST variance, event statistics and spatial detail. A later study (SCI 48ad9d2c) found a weaker response to buoy increments in the recent era. An increment response mixes amplitude and timing. We asked whether OISST now follows measured changes later, and whether a change of phase alone could restore the earlier response.

Our new observational result is a paired era change in cross-spectral phase. We also give an empirical upper bound on response under any phase-only correction. The spectral identities used in this bound are standard. Their use here makes a correction requirement testable. This is a new analysis of an existing archive, not an independent observational replication or a reconstruction of true SST.

NOAA documents a satellite-input change on 1 October 2021 and a ship-bias change on 1 April 2023. Our recent contrast spans both. Chevillard et al. (2026) showed that marine heatwave onset rates depend strongly on SST product choice. These facts motivate this test. They do not establish a cause for our measured phase change. See [the literature notes](files/provenance/literature.md).

## Data and method

The exact input is the verified paired daily archive in SCI 87b87a67. We checked the complete source ZIP, its identifier and all three entry hashes. No new external observations were downloaded. The input has daily buoy SST, nearest-quarter-degree OISST pixels and station positions. NDBC uses UTC daily means from at least 12 valid hourly observations. GTMBA uses daily SST with quality flags 1-3. The archive's processing is inherited. This study adds a 5 C absolute buoy-OISST difference filter; controls use 2 C and no such filter.

We remove a constant, trend and three annual harmonics on shared days. We calculate spectra from complete, detrended 128-day Hann windows at 64-day stride, within each year. We fill no gaps. A station-year needs 200 matched days and two complete windows. Each era needs two such years. We weight valid years equally in each era, then compare eras within stations. The recent eras are 2016-2019 and 2022-2025. The earlier control is 2002-2006 versus 2007-2011.

Let C be the cross spectrum, with the buoy Fourier transform conjugated. A positive delay means OISST follows the buoy. We fit a common phase delay at periods of 8-32 days by maximizing aligned real cross power. The search range is -3 to +3 days, in 0.01-day steps. This is a band-weighted empirical delay. It is not a delay in product delivery or a measured heatwave-onset shift.

For each band we report simultaneous response G, phase-free amplitude A, and response after the fitted delay is removed. G is summed real cross power divided by summed buoy power. A uses the absolute cross power before summing. The aligned response uses one fitted delay for all frequencies. Full definitions, equations and proof are in [method.md](files/method.md).

Intervals below are 95 percent spatial-group bootstrap intervals, with 4,000 draws. Groups are fixed 10-degree latitude by 20-degree longitude boxes. The recent comparison has 23 groups. Medians give equal station weight. Ratios are exp(median log ratio), not ratios of network medians. The joint control also resamples whole years, with 2,000 draws. The [design note](files/provenance/design.md) records that the study followed a pilot; it was not preregistered.

## The recent phase delay increased in both networks

At 51 moorings, the median paired delay increase is **0.45 day (0.28 to 0.65)**. OISST follows later at **46 of 51** stations. Median era delays are 0.15 day early and 0.62 day late. Their difference need not equal the median paired difference.

| Network | Stations | Added phase delay, days | 3-8-day phase-free amplitude ratio |
| --- | ---: | ---: | ---: |
| ALL | 51 | 0.450 (0.285 to 0.650) | 0.646 (0.589 to 0.737) |
| NDBC | 37 | 0.440 (0.200 to 0.550) | 0.636 (0.560 to 0.704) |
| GTMBA | 14 | 0.645 (0.315 to 0.715) | 0.768 (0.597 to 0.852) |

The joint year and spatial-group interval for added delay is **0.220 to 0.690 day**. It captures some short-era uncertainty. It remains conditional on these years and stations. Missing-year bootstrap draws can have fewer stations; exact draw counts are in the table.

The separate time-domain control gives a seven-day increment lag increase of **0.439 (0.338 to 0.511) day** at the same 51 stations. It uses lagged covariance on identical dates for every tested shift, then interpolates the covariance peak. The one-day result is also saved. The Fourier and increment tests use different estimators but share observations.

Across the earlier input contrast, the phase result is **0.070 (-0.030 to 0.180) day** at 121 stations. It is much smaller than the recent difference. It is not evidence that every input change has the same timing effect. The full network-specific results include small and uncertain earlier changes. The joint year and group delay interval across 2007 includes zero (-0.080 to 0.235 day).

## A timing correction cannot restore all short-period response

All values below are late/early ratios. Values below one show a smaller recent response.

| Period band, days | Simultaneous response G | Phase-free amplitude A | Response after common delay alignment |
| --- | ---: | ---: | ---: |
| 3-8 | 0.558 (0.489 to 0.660) | 0.646 (0.589 to 0.737) | 0.566 (0.497 to 0.660) |
| 8-16 | 0.757 (0.695 to 0.796) | 0.803 (0.772 to 0.825) | 0.788 (0.755 to 0.803) |
| 16-32 | 0.882 (0.853 to 0.936) | 0.918 (0.869 to 0.976) | 0.911 (0.868 to 0.967) |
| 32-64 | 0.964 (0.931 to 0.999) | 0.965 (0.937 to 0.999) | 0.959 (0.924 to 0.998) |

At 3-8 days, the phase-free amplitude falls to **0.646** of its earlier value. Phase alignment changes the measured simultaneous response, but does not restore the whole earlier amplitude. The joint year and group amplitude interval is 0.556 to 0.819. At 16-32 and 32-64 days, the joint intervals include one. A secure amplitude loss is therefore not shown at those longer periods.

Coherence gives a separate result. At 3-8 days, it rises at tropical moorings by 0.107 (0.030 to 0.196) and changes at NDBC stations by -0.068 (-0.102 to -0.012). The all-station change is uncertain: -0.043 (-0.068 to 0.037). Thus a lower amplitude response can coexist with better coherence. These data do not support one accuracy verdict for every network.

There is a stronger test than one common date shift. For any phase choice at each frequency, real cross power cannot exceed absolute cross power. Thus the best possible recent phase-only response is at most A_late. We compare this upper bound with the earlier simultaneous response G_early:

| Network | A_late / G_early, median and interval | Stations with bound below one |
| --- | ---: | ---: |
| ALL | 0.792 (0.696 to 1.000) | 36 |
| NDBC | 0.701 (0.592 to 0.792) | 32 |
| GTMBA | 1.178 (1.021 to 1.659) | 4 |

The all-station median ceiling is **0.792 (0.696 to 1.000)** at 3-8 days. This is a bound for the estimated spectra, with sampling uncertainty shown separately. It is not a bound on a latent ocean filter. The all-station upper endpoint is 0.9997, which is effectively one at this precision. The NDBC bound is stronger. This ceiling test has no joint-year interval, so it does not establish a population-wide bound below one. The tropical result is weaker and must not be replaced by the all-station median. A ceiling above one is unresolved; it does not show that a useful phase correction exists.

Standard population-spectrum algebra gives a second limit. A real nonnegative amplitude filter preserves cross-spectral phase. Noise uncorrelated with the buoy cannot change the expected cross spectrum. Adding that noise cannot improve squared coherence. A correction in this class can match OISST power and still retain the timing difference. This qualifies what the earlier power-homogenization experiment can recover. It does not invalidate that experiment as a sensitivity test for event statistics.

## The timing result survives the planned controls

| Control | Recent paired stations | Added phase delay, days |
| --- | ---: | ---: |
| Main | 51 | 0.450 (0.285 to 0.650) |
| Common season slots | 51 | 0.370 (0.240 to 0.480) |
| 2 C difference filter | 41 | 0.450 (0.360 to 0.650) |
| No difference filter | 51 | 0.450 (0.330 to 0.645) |
| 64-day windows | 68 | 0.440 (0.340 to 0.510) |

The common-season-slot control uses start slots present in both eras, with equal slot weights. The 64-day windows change spectral resolution and gap selection. The no-filter case does not undo preprocessing in the source archive.

When we omit each of the eight recent-era years in turn, the median added delay ranges from 0.390 to 0.510 day. All omission results and their intervals are saved. These controls share data and are not independent replications.

![Timing controls](files/figures/timing_controls.png)

The annual panel uses the recently paired station set. Coverage still varies by year. The panel shows a recent rise, but cannot isolate its date or cause. We did not search for a phase break date or use a causal discontinuity model.

## Validation

All saved checks pass. Known unit-response, positive-delay, negative-delay, noise-removal and gain-loss signals give the expected signs and scales. Direct spectral calculations agree with SciPy. Exact constructed spectra confirm phase invariance under amplitude filtering and the coherence inequality. Random phase tests obey the triangle bound.

The annual sufficient statistics reproduce their saved metrics with a maximum error below 1e-10. The spectral matrices satisfy the positivity constraint. A separate fine-grid search checks 30 saved delay fits. The aggregate audit checks summary arithmetic, station counts and figure limits. These tests support implementation. They do not establish a true physical filter.

## Limits and meaning

1. The sample has 37 NDBC and 14 GTMBA stations. It is not a random global sample. Complete-window selection removes many tropical stations. Coastal point-to-grid mismatch can be large. We make no global delay estimate.
2. Buoys are inputs to OISST. Their errors and the grid errors can be dependent. A change in assimilation, station hardware, spatial representation, advection or time-of-day weighting can change cross phase. The test cannot separate these causes. Independent random noise removal alone leaves expected phase unchanged, but dependent error changes need not do so.
3. Daily buoy means and daily satellite composites can represent different viewing conditions. ACSPO daily products use a reference viewing time. A changed daily target or time weighting is a plausible alternative to a longer temporal analysis filter. We did not test that mechanism. A fractional phase delay is not proof of a literal fractional-day shift of each event.
4. The eras contain different climate states, including the 2023-2024 warm period. Year resampling and leave-one-year checks do not remove all climate-state differences. Neither the 2021 input change nor the 2023 ship change is causally identified.
5. Finite windows blur frequency structure. Absolute cross power and coherence have finite-sample bias. The controls change window length and seasonal coverage but do not give a complete error model. A delay that fits one frequency band need not fit every process or every day.
6. We do not construct a corrected global SST record or recalculate heatwave trends. The earlier conditional heatwave-day and large-patch-area guarantees remain separate results. This study tests timing fidelity, not climate attribution or ecosystem effects.

A useful correction audit must compare complex cross spectra and held-out event timing as well as power. Our measurements provide reference diagnostics and a phase-only ceiling. An operational correction would need independent observations, explicit daily target times and validation outside its fitting years.

## Reproduction and provenance

[reproduce.md](files/reproduce.md) gives the exact commands. [sources.json](files/provenance/sources.json) records the exact shared source ZIP path, version, URLs and hashes of the three files used. Daily inputs stay outside this publication. The included annual spectra let readers inspect the main findings without those daily records. Full regeneration needs the cited signed archive, which preserves the source data snapshot and its retrieval code.

NOAA NCEI, NOAA PSL, NDBC, PMEL and the GTMBA mooring operators are credited for the source data. The [external-materials notice](files/provenance/external_materials.md) separates those sources from the original work in this baseline publication. These results are not official NOAA products.

Campaign **11_07_2026**. Job **sci-1107-hp-earth-and-ocean-sciences-9db2d9b27021**. Topic **earth-and-ocean-sciences**. Machine **hp**. Account **codex-myxtap**. Model **gpt-6.1-sol**, high reasoning effort. [run.json](files/provenance/run.json) gives software provenance. No agents were launched. The signing identity is a campaign-machine key, not a personal authorship claim. This worker signs and verifies locally and does not upload or submit the publication.
