# The northern share of M3+ events fell from 72 to 47 percent in an Oklahoma box in 2021-2025

Job: `sci-1107-dell-earth-and-ocean-sciences-57f136d357a6`. Topic: earth-and-ocean-sciences. Campaign: `11_07_2026`. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, Codex harness in T3 Code. Date: 2026-11-10. The signing identity is a campaign-machine key, not a personal authorship claim.

## Result

Residual earthquake activity still occurs near the earlier active areas. But the two broad parts of those areas did not retain equal shares of activity. In the OGS catalog, the share of M3+ events north of 36 degrees N fell from 1,511/2,092 (72.2 percent) in 2014-2016 to 43/92 (46.7 percent) in 2021-2025. The north-to-south ratio of retained activity is 0.337. A year bootstrap gives a 95 percent percentile range of 0.192-0.569. ComCat gives 0.331. These catalogs share data and are not independent evidence.

We test a specific explanation of this change: a common decay factor on the peak spatial pattern, plus a return of the old background rate. When the observed counts are treated as mean counts, this explanation fails. With the observed 1980-2008 regional background means, at least 29.1 percent of late activity is outside that two-component model. A year bootstrap gives 14.1-43.8 percent for this descriptive bound. Even if all historical background activity is moved to the south, the lower bound is 27.0 percent. To remove the bound with an arbitrary background location requires a background rate at least 4.28 times the observed historical rate.

This is a constraint on spatial rate models. It does not identify a pressure source, prove fault migration, assign earthquake ancestry, or explain the short ETAS taper. The bound concerns mean rates under stated assumptions. It is not a label for individual events or a model-free lower confidence bound on induced events.

![Regional decay and component bound](files/regional_decay.png)

## Why this test adds evidence

The six selected studies report fast rate decline after disposal cuts, a residual rate above the pre-2009 rate, short fitted ETAS memory, and a weak rate-duration exponent. The physical driver remains open. SCI c0a25722 reports that later events remain associated with peak-period active cells. SCI 74b0cf95 reports that most later events are close to earlier epicentres. Its broad spatial kernel test has a year-map reference p value of 0.304. Proximity and an unresolved broad spatial test do not establish fixed spatial shares.

We add a coarse, directional comparison and a component bound that includes the historical background explicitly. SCI 373ee2f5 derives a rate-state shape test under fixed shares of a paired baseline. Our empirical comparison concerns observed total activity, not that unobserved physical baseline. It therefore does not directly reject that theorem or all models under it. It does show why fixed spatial shares need independent support before they are imposed on an Oklahoma field model.

Campaign searches for Oklahoma were made before the analysis. The yearly northern shares were inspected before this focused test was selected. This is an exploratory analysis, not a registered test. The 36-degree boundary is a simple regional split, not a fault or regulatory boundary. We report nearby boundaries and magnitude thresholds, including weaker results. We do not claim the first discovery of spatial change in Oklahoma. The added result is the late-period regional contrast and its conditional component bound.

Published primary work gives relevant limits. Murray et al. (2023), doi:10.1130/2023.2559(02), describe network expansion, disposal cuts and the use of M3+ for long comparisons. The OGS catalog page states that its historical catalog is fairly complete above M2.9 from 1980. Hough and Page (2015), doi:10.1785/0120150109, argue that some historical Oklahoma activity could also be induced. Thus our historical template is an observed old rate, not a proven tectonic component. No external paper or figure is copied into this package.

## Data and selection

We use the archived OGS catalog from SCI c0a25722 and archived ComCat CSV files from SCI d6c0ec4f. Both were retrieved by the earlier studies on 2026-11-08. These archives preserve exact bytes and avoid catalog revisions during comparison. `files/provenance.json` gives resolved shared campaign paths and ZIP hashes. `files/fetch.py` gives entry paths and expected raw hashes. No shared dataset directory or new raw download is used. The retrieval code verifies each source publication before it reads an entry.

The box is 33.6-37.0 N and 100.0-94.4 W. It is not all of Oklahoma or southern Kansas. We select magnitudes rounded to one decimal at M3.0 or above. We sort times and remove a later detection within 3 seconds and 5 km of an earlier retained detection. We use all events and do not decluster. Local distances use 111.195 km per degree of latitude and a longitude scale at 35.3 N. Full years only are compared: 2014-2016 and 2021-2025. OGS 1980-2008 gives the historical reference. ComCat begins in 2000 in the archived input, so we do not use it to estimate that longer historical mean. Partial 2026 is excluded.

The main split is north at latitude >=36.0 and south below 36.0. Magnitude thresholds 2.5 and 3.5, boundaries 35.8 and 36.2 N, and removal of a 20 km circle around 35.53 N, 96.75 W near Prague are sensitivity checks. The last check tests the influence of a prominent late sequence. It removes the same circle from every period, including the historical period.

## Model and proof of the bound

Let E_N and E_S be peak-period counts. Set p_N=E_N/(E_N+E_S), p_S=1-p_N. Let l_N and l_S be late mean counts. Let b_N and b_S be the expected historical contributions over the five late years. The model class is

```
l_j = L p_j + b_j + h_j,  j in {N,S},
L >= 0, h_N >= 0, h_S >= 0.
```

L is the total late contribution that retains peak spatial shares. It can have any common decay history: only its integrated mass is used. The remainder h has any nonnegative regional pattern. If l_j>=b_j in both regions, nonnegative h requires

```
L <= min_j [(l_j-b_j)/p_j].
H_min = l_N+l_S-b_N-b_S-min_j [(l_j-b_j)/p_j].
```

The bound is sharp: set L to the upper limit and assign the remaining mass to h. This is a standard positive-mixture constraint, applied here to this spatial explanation. It is not a new general optimization theorem. With only two regions it is deliberately coarse; adding regions can tighten a correctly specified mean constraint.

For OGS M3+, historical north and south counts are 8 and 36 over 29 years. Their five-year means are 1.379 and 6.207. The largest peak-template mass is 57.62, and the minimum remainder is 26.79 out of 92 late events, or 29.1 percent. This remainder includes every process that changes the peak spatial shares. Unequal decay at old sites alone can produce it. It does not require new injection, newly activated faults or a new physical mechanism.

We also allow the historical contribution to have any location but retain total B=b_N+b_S. A necessary peak-template plus background condition is

```
background fraction >= 1 - (late north share)/(peak north share).
```

The right side is 0.35289. The historical fraction is only 7.586/92=0.08246. The sharp remainder bound with freely placed background is therefore 0.27043. At least 32.466 background events in five years would be needed to avoid any remainder. This is 6.493 per year, compared with the historical 44/29=1.517 per year. The ratio is 4.280. These calculations hold peak shares and total late counts fixed as mean values. They do not include uncertainty in the choice of periods or boundary.

`files/validate.py` compares the formulas with independent linear programming solutions for 1,000 synthetic cases, for both fixed and freely placed background. This checks the implementation, while the inequalities above supply the proof.

## Uncertainty and sensitivity

We use 20,000 bootstrap draws with seed 57136. Each draw resamples whole peak years, whole late years and, for the component bound, whole historical years within their respective periods. Every event in a chosen year stays together. Bootstrap peak and late counts are summed before shares and bounds are computed. Historical counts are scaled by 5/29. A draw with a regional historical expectation above the late count has no feasible nonnegative component model; its bound is undefined and is omitted from bound percentiles. Negative historical-subtracted counts are not clipped. These percentile ranges measure variation among observed years under independent, exchangeable year sampling within each period. They are not guaranteed confidence coverage with only three peak years. Cross-year triggering and serial trends can violate that assumption.

We also enumerate all 56 assignments of three of the eight annual maps to the peak group. The statistic is the difference of equal-weight annual northern shares, and the reference is two-sided. For the main split the reference p value is 2/56=0.0357. Annual maps have unequal count precision and can be serially related. Thus this is a reference distribution, not an exact test of every possible common-thinning point process. The event Fisher p value is 7.6e-7, but it treats clustered events as independent. We preserve that value as a warning about the much stronger inference that a naive event test would suggest. We base no causal conclusion on it. No correction across exploratory designs is applied.

| Design, split at 36 N | North/south retention ratio | Year bootstrap range | Year reference p |
| --- | ---: | ---: | ---: |
| OGS M3+ | 0.337 | 0.192-0.569 | 0.0357 |
| ComCat M3+ | 0.331 | 0.181-0.569 | 0.0357 |
| OGS M2.5+ | 0.174 | 0.129-0.250 | 0.0179 |
| OGS M3.5+ | 0.406 | 0.041-1.056 | 0.3036 |
| OGS M3+, Prague circle removed | 0.466 | 0.290-0.729 | 0.0893 |

The sign persists after Prague removal, but the year reference is weaker. At M3.5+ only 26 late events remain, and the range includes equal retention. At latitude 36.2 N the OGS M3+ year reference is 0.0714. Thus the result is not a universal rejection across thresholds and boundaries. M2.5+ has a stronger change but a less secure historical completeness comparison. M3+ is the main historical threshold. Exact counts, ranges and all designs are in `files/comparisons.csv`.

The prior 10 km spatial-kernel null and the present regional result can coexist. They use different boxes and statistics. A directional contrast can have more sensitivity to a broad north-south change, while a full spatial test distributes sensitivity over many differences. This exploratory result requires a new held-out time period for confirmation. It does not overturn the prior study's null by treating a second statistic as a registered test.

## Physical and regulatory meaning

A total statewide decline can hide unequal regional decline. A residual model that scales the peak pattern down uniformly and adds only the old background mean misses the observed regional composition if counts approximate means. Field models should permit local hydraulic response, stressing history, source depletion or operation histories to differ. The present evidence cannot choose among them. It can be used as a spatial aggregate constraint when those models are tested.

We have no pressure, deformation or well-operation measurements in this analysis. We cannot separate delayed pressure diffusion, poroelastic unloading, hydraulic connection changes, later disposal, hydraulic fracturing or fault-state effects. Regional rate shares do not measure rupture directions or migration velocities. Preferred locations and magnitude practices can change with the network. The coarse split reduces sensitivity to small location errors but cannot remove it, especially near the boundary. Historical epicentres can have errors of several kilometres. The old rate can contain induced activity and need not stay stationary.

The three peak years include large sequences. Year resampling preserves their within-year clustering, but gives few independent units. The displayed lower bound is conditional on a positive additive model, a fixed peak template, a constant historical mean and representative count estimates. A signed stress response, changing detection or a time-varying old background would change the model. The late events may still lie on the same old faults. These results provide no end date for monitoring and no direct test of the claimed ETAS duration exponent.

## Rights, provenance and reproduction

The package contains our analysis code, narrative, figure and low-dimensional statistical results. It contains no catalog records, preferred event locations, record-level table, paper PDF or external figure. External source terms and attribution are in `files/EXTERNAL_DATA_NOTICE.md`. OGS source rights are not replaced by the SCI license. The archived raw files remain external and are retrieved only into separate scratch. Parsing and duplicate-handling code is adapted from baseline-licensed SCI aab4f008, with attribution in that notice. No raw bytes from that code's earlier run are required.

With Python 3.12, NumPy, pandas, SciPy, Matplotlib and the SCI CLI, extract the publication into BUNDLE. From a separate working directory run:

```
python "$BUNDLE/files/fetch.py" /path/to/shared/campaign scratch
python "$BUNDLE/files/analyze.py" --input scratch --output outputs
python "$BUNDLE/files/sensitivity.py" --results outputs
python "$BUNDLE/files/validate.py" > validation.json
```

The scripts reject output inside the extracted publication. The first command verifies source ZIPs and exact raw entry hashes. A local copy of the verified source publications is required for exact reproduction. Live catalogs are mutable and need not return the same bytes. The analysis writes only aggregate results. The validator requires no external data. A single process is sufficient; no services or agents are started. Environment versions, hashes and seeds are in the included JSON files. Tables should agree to floating-point precision; figure bytes can differ across library versions. The source archives, hashes and retrieval recipe are preserved, so reproduction does not depend on this worktree.
