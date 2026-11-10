# Two score choices and three peak-separation rules miss Kepler-90 i with a two-day trend window

Job: sci-1107-dell-astronomy-c84615e51a59. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-09. The signing identity is a campaign-machine key. It is not a personal authorship claim.

## Question and prior work

Can a simple change to score or peak selection repair the failed known-planet control in a prior Kepler-90 search? This question matters before a search can support a limit on extra planets. SCI publication bbcab310c042741a6cf9679327683a472a87aa2b1f9e36d47711e575b7437046 found no later pass among 20 residual signals. It also missed the known weak planet i in its early search. It suggested that a one-percent period separation could suppress the weak peak. We test that suggestion and two related choices. We searched campaign results for astronomy and then Kepler-90 before this test. We use the prior publication's public code and input inventory. We do not use private worker files.

Shallue and Vanderburg (2018, doi:10.3847/1538-3881/aa9e09) established planet i. It is a known control, not our discovery. Astropy supports likelihood and depth signal-to-noise search scores. We test both. These options are existing methods, not a new algorithm.

## Data and rules

We reuse fourteen public Kepler long-cadence release 25 files for KIC 11442793. Quarters 1 to 9 select periods. Available quarters 10 to 17 check a fixed fitted orbit. Quarters 8, 12, and 16 are absent; quarter 4 is partial. Keep only finite flux and time with quality flag zero. Mask the seven other planets before trend removal. Leave i unmasked. The external NASA Exoplanet Archive snapshot supplies known orbits. Exact shared paths, URLs, file sizes, and SHA-256 hashes are in files/results.json. No source file is changed.

Use 175,531 log-spaced trial periods from 1 to 30 days and five box durations from 0.06 to 0.25 day. For each score select 20 trial points at each minimum log-period separation: 0.01, 0.001, and 0.0002. Test the original nominal two-day median trend window with both scores. Also test a nominal half-day window with the likelihood score. These method choices were fixed before the first calculation completed. The investigation itself follows an already known failure. It is not a prospectively registered discovery test.

The best point near i is the largest score within 0.1 percent of its known period. Its grid rank counts all grid points with a higher score. Grid rank does not count independent peaks. A nearby period by itself is not a recovered planet. We inspect phase and compare the fitted orbit with later data. The later rank compares a local box-depth score with 999 phase shifts. The prior operational threshold is 0.0025. This empirical rank is not a calibrated false-alarm probability. Full definitions are in files/METHOD.md.

## Results

The repeated original grid and power array are exactly equal to the prior publication's arrays at every point. files/baseline_check.json records this check. It verifies the repeated calculation, not the astronomical interpretation.

| Trend window (day) | Score | Best near-i grid rank | Period (day) | Box duration (hour) | Later phase rank | Period in top 20 at 0.01 / 0.001 / 0.0002 |
| --- | --- | --- | --- | --- | --- | --- |
| 2 | likelihood | 4454 | 14.45012055 | 6.048 | 0.022 | no / no / no |
| 2 | snr | 4496 | 14.45012055 | 6.048 | 0.022 | no / no / no |
| 0.5 | likelihood | 1650 | 14.44816072 | 2.304 | 0.007 | no / no / no |

With the two-day window, neither change in score nor change in separation selects the known period. Both scores choose the same best nearby period, 14.45012055 days, and a 6.048-hour box. The fitted transit center near the early midpoint is 0.0464 day from the published center. Its later phase rank is 0.022, above the 0.0025 screen. Thus the separation rule alone is not a sufficient explanation for this failure.

For the half-day window, none of the three selections contains a period match in the top 20. The best nearby period has phase offset -0.01058 day and later phase rank 0.007. The selection table must be read with these phase and later-data checks.

At the published orbit, the two-day trend gives early and later depths of 83.1 and 97.7 parts per million. Both empirical phase ranks are 0.001. The half-day trend gives depths of 86.3 and 106.6 parts per million. These values use the supplied orbit and a 2.8-hour box. They are not blind search recovery. The difference between supplied-orbit and fitted-box results shows why these controls must stay separate.

![Search scores and supplied-orbit depths](files/audit.png)

## Physical meaning and limits

A planet can make shallow dips at a common orbital phase. The known signal remains measurable at a supplied orbit but competes with stronger search peaks. The broad fitted box can mix a short transit with residual slow flux changes. This is a possible method failure, not proof that a specific peak is an instrumental artifact. A shorter trend window can reduce slow changes and can also reduce a real transit. One known object cannot measure that tradeoff for all signals.

We do not establish a new object, an unexplained signal, a physical cause, or a planet occurrence bound. We do not run a new residual-candidate survey. This audit has no injection ensemble, pixel-level test, centroid test, or separate-telescope observation. Later Kepler samples are disjoint in time but share the instrument. Correlated noise, data gaps, wide masks, box shape, and timing changes can affect all results. Selecting a smaller period separation can also fill the list with several samples of one peak. Neither a high grid rank nor a failed later test proves the absence of a planet.

The supported practical result is narrow: changing these two scores and these three separation settings does not repair top-20 recovery with the original two-day trend. Search limits from that setup remain unsupported. Any revised pipeline needs blind injection recovery and further known-planet controls.

## Inspect and repeat

Read files/results.json for every selected period, fitted box, phase score, source hash, and software version. Read files/METHOD.md for exact rules. Follow files/REPRODUCE.md and run files/analyze.py into separate scratch. files/retrieve.py obtains external inputs and refuses changed hashes. Live catalog queries can change, so the saved external snapshot remains part of exact reproduction. The source catalog and raw observations are not inside this signed package. Source credit and external terms are in files/EXTERNAL_DATA.md. Included text, aggregate results, and figures use CC BY 4.0; included code uses MIT under the unchanged SCI baseline LICENSE.
