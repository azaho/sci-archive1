# Song frequency had no clear link to tenure curvature in 283 North American bird species in 1966-2025

Job: **sci-1107-hp-climate-pollution-biodiversity-cac81560e76a**. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: hp. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-10. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Main result

Higher song frequency did not have a clear negative link to the curvature of bird counts with observer tenure. We fitted new count models to 130,303 standard North American Breeding Bird Survey (BBS) runs on 5,319 routes in 1966-2025. We left each observer-route intercept and each calendar-year effect free. This model permits free differences between entry cohorts.

A linear tenure effect cannot be separated from these effects. We therefore tested a second difference:

**C = f(25) - 2 f(15) + f(5).**

Here f(u) is the common log-count component at u years since the observer's first standard run on that route. C compares the count change from years 15 to 25 with the change from years 5 to 15. C = 0 for any linear tenure curve. A negative C means that the second ten-year change is more negative. It does not specify the total loss over twenty years.

Of 446 species, 394 had stable primary fits. Among them, 283 species outside the visual comparison group had an acoustic frequency value. Across these 283 species, the slope of C on dominant frequency was **+0.0084 log units per kHz**, with a 95% spatial-block interval of **-0.0063 to +0.0231**. With family effects, it was **-0.0062** (-0.0271 to +0.0147). Thus the data did not show a clear increase in negative curvature with frequency.

![Tenure curvature and song frequency](files/results/curvature.png)

This is a null frequency result, not a test that hearing loss is absent. A constant annual hearing loss is linear on the log-count scale and cancels from C. The data still cannot identify that loss or its correction to climate trends.

## Why this question matters

Earlier campaign work found weak bird community temperature tracking. It also found a large negative association between counts of high-pitched species and observer tenure. One model gave about 41% fewer birds in the class at 7 kHz or more after twenty years. It used route effects but did not leave observer-route intercepts free (SCI b9959b67).

A later proof showed that linear tenure drift and cohort differences can give the same counts (SCI f7eaf981). That proof did not fit new bird count outcomes. Our study tests the nonlinear part that can remain estimable under the additive model. It adds a count analysis, exact schedule rank checks and joint spatial uncertainty. It does not use a tenure-bin contrast to supply information about a missing linear slope.

The general result on estimable curvature is established in age-period-cohort research (Holford 1983). Farmer et al. (2014) also gave earlier evidence for observer age effects in birds. We do not claim either general result as new. Our new result is the lack of a clear frequency pattern in the cohort-invariant post-learning contrast in the 2026 BBS release.

## Data and model

We reused raw data in the shared store through `./datasets`. We did not download or modify shared data. The BBS source is the 2026 release for 1966-2025, doi:10.5066/P144YU3S. Exact file URLs, shared paths, byte counts and SHA-256 hashes are in [provenance.json](files/provenance.json).

We kept RunType 1, RPID 101, a positive observer identifier and a nonmissing route latitude. We removed duplicate route-years. Tenure is calendar year minus the first standard year for that observer-route pair. An observer who returns to the same route keeps the same first year. It is not a visit count or biological age.

We used the same 446-species list, name matching, dominant acoustic frequencies and visual comparison definition as SCI b9959b67. Forms of a binomial are summed. The reduced metadata table fixes this choice. Frequencies ultimately come from Sagar et al. (2024), Dryad version 326179, CC0. No old trend estimate or old temperature index entered the new fits.

For each species, the model is:

`log E(count) = observer-route effect + year effect + first-run term + f(tenure)`.

The function f is a linear spline with hinges at 5, 10, 20 and 30 years. Each hinge is `max(tenure - knot, 0)/10`. The linear tenure term is omitted because it is aliased. This omission selects a coordinate system; it does not show that the true early slope is zero. The first-run term allows an initial learning effect. The primary contrast starts at year 5 to avoid that term.

We use all standard runs on a route where the species was recorded at least once. We profile out the observer-route intercepts in a conditional Poisson likelihood. Observer-route groups with zero total count have no information in this likelihood. Year strata with zero total count are removed at their limiting fitted mean of zero. No Poisson variance assumption is used for the reported sandwich intervals. The mean model remains an assumption.

We check the design after removal of group means. An eigenvector basis removes exact nuisance aliases. Each reported contrast must be in the retained row space. We require convergence, a positive contrast standard error and an information condition number below 1e12. All 394 eligible primary fits had a condition number below 9.1 million and a maximum absolute score below 1.4e-10. A cutoff of 1e8 therefore selects the same primary set. Fifty-two primary fits failed the numerical criteria. Their diagnostic values are retained but are not valid estimates for inference.

The original selection included ten species in the class at 7 kHz or more. Eight had stable primary fits. Costa's Hummingbird (Calypte costae) and Gray-cheeked Thrush (Catharus minimus) failed the criteria. This exclusion limits inference for the highest-frequency class.

## Group results

These are unweighted means over fixed sets of eligible species. Intervals use 458 two-degree spatial blocks and preserve covariance among species measured on the same routes.

| Dominant frequency or group | Species | Mean C | 95% spatial interval |
| --- | ---: | ---: | ---: |
| Below 3 kHz | 75 | -0.0519 | -0.0898 to -0.0141 |
| 3 to below 5 kHz | 143 | -0.0147 | -0.0431 to +0.0137 |
| 5 to below 7 kHz | 57 | -0.0457 | -0.0805 to -0.0109 |
| 7 kHz or more | 8 | -0.0129 | -0.1176 to +0.0919 |
| Visual comparison group | 96 | +0.0776 | +0.0231 to +0.1321 |

Fifteen other eligible species had no acoustic frequency and do not enter this table. The highest-minus-lowest frequency contrast was +0.0391 (-0.0738 to +0.1519). Some groups had curvature, but the means did not decrease in order with frequency. The visual group is a comparison group. Many of its species are also heard, so it is not a pure visual control.

A secondary contrast, f(30) - 2 f(20) + f(10), gave a frequency slope of +0.0217 (-0.0085 to +0.0518). This result also did not show a clear negative frequency slope.

The primary highest-frequency mean has exp(C) = 0.987. Its interval permits ratios from 0.889 to 1.096 between the two ten-year multipliers. These are curvature ratios. They are not limits on the total detection loss.

## Robustness and uncertainty

The planned survey-control fit adds survey day, its square and a final-two-runs term. The regional fit also gives the East and West separate year effects, split at 100 degrees W. The log-count fit uses log(1 + count) and the same positive observer-route groups. Its effect size is on a different scale. The regional fit had stable estimates for only 307 species. We therefore give the robustness comparison on these same 307 species, including 226 song-frequency species and five species in the highest class.

| Model on the common set | Frequency slope of C | 95% spatial interval |
| --- | ---: | ---: |
| Primary Poisson | +0.00288 | -0.00979 to +0.01554 |
| Survey and service controls | +0.00301 | -0.00959 to +0.01561 |
| Region by year controls | +0.00525 | -0.00726 to +0.01776 |
| Log(1 + count) | +0.00048 | -0.00388 to +0.00484 |

An added comparison fit uses route intercepts, year effects, a linear tenure term and the same spline. It restricts observer-cohort differences as earlier tenure models did. On the common set its frequency slope was +0.00297 (-0.00960 to +0.01554). This added check also gave no clear negative curvature slope. It does not repeat the earlier tenure-bin model exactly.

For each species, we saved the route influence of each contrast in external scratch. For a species mean or frequency slope, we combined those influence values across species first, then summed them within spatial blocks. This retains shared route and observer errors. The bundled summary covariance matrices permit inspection without observer records. Intervals use a t reference with 457 degrees of freedom. They condition on the selected species and the model.

Separate family-cluster intervals describe variation across families. The primary frequency-slope interval was -0.0095 to +0.0263. The highest class contains only four families. These intervals are not a joint correction for all spatial and family uncertainty. The group and secondary intervals are descriptive; no multiple-test claim is made. Neither uncertainty method covers model error or nonrandom species exclusions.

## What remains unidentified

For any real k, add k times tenure to f, add k times the entry year to each observer-route intercept, and subtract k times calendar year from the year effect. Every fitted count stays the same. Yet f(25) - f(5) changes by 20k. The primary contrast stays the same. The exact proof and the schedule check are in [PROOF.md](files/PROOF.md).

![Equivalent tenure components](files/results/equivalent_curves.png)

The three curves in this illustration use the fitted mean shape of the eight eligible high-frequency species. We chose linear tilts to give a 41% decrease, no endpoint change or a 41% increase from tenure year 5 to 25. We changed the cohort and calendar components with each tilt. All fitted counts remain identical. These curves are a proof illustration, not estimates of those detection changes. The chosen endpoints also differ from the earlier first-run versus 20-plus-year bin comparison.

Curvature itself needs an additive common tenure curve. If each observer-route group can have a separate calendar trend, even quadratic tenure curvature can be moved into calendar and group terms. A changing entry-age distribution, selective retirement, ecological change tied to observer schedules or cohort-specific learning can violate the model. Biological ages, hearing tests, repeated simultaneous observers or stable audio calibration data would add information. This study has none of these.

## Numerical checks and plan changes

An independent Poisson GLM with explicit group dummy variables agreed with our profile solver to 8.6e-14 in a small panel. With known expected counts, the solver recovered all spline terms to 3.4e-14 in that panel and 3.1e-15 on the real BBS schedule. The real-schedule linear transformation preserved log means to 2.8e-14. A second algebra check showed the quadratic alias under separate group trends. These deterministic checks test the software and identification algebra. They are not evidence of causal hearing loss or a simulation confidence-coverage study.

The plan preceded the new fits. We added the joint spatial influence calculation, the common-species comparison, exact numerical eligibility cutoffs and the equivalent-curve figure after pilot fits. We added the separate route-intercept fit as the planned old-specification check, with a linear term so it does not force an early slope. The plan also proposed a random-effects weighted summary. We did not use it: equal species weights define a clear fixed-species target and avoid weights that depend on unstable count fits. This change must limit any claim of full adherence to the plan. No new outcome, knot or contrast was selected after the pilot.

## Scope and limits

The result concerns a frequency pattern in count curvature, conditional on the common spline model. It does not measure hearing, detection probability, true population change, an ecological lag, or the fraction of warming tracked by birds. It cannot remove the observer correction uncertainty from earlier climate studies.

Counts can change through habitat, abundance, migration, phenology, survey conditions and detection. Most of these processes were not measured here. Acoustic frequency can also follow ecology. Tenure is not age. Sparse histories caused model failures, and the common robustness set is smaller. The highest-frequency class is small. Spatial blocks do not cover all time or spatial dependence. The count and log-count models do not target the same effect scale. A true constant annual high-frequency loss can be large while every curvature result is zero.

The useful conclusion is narrow: this new cohort-invariant test did not find the ordered frequency pattern expected from a simple common acceleration of high-frequency loss after early service. It therefore supplies no empirical basis for a numerical linear hearing correction. The absolute correction remains a sensitivity parameter unless new calibration data or justified cohort restrictions are supplied.

## Reproduce

All code and species-level evidence needed to inspect the claims are in this bundle. Raw data and all record-level intermediates must remain outside it.

For an exact aggregate check, run `python files/code/check_results.py files/results`. For a full rebuild, extract the verified bundle and run from its root:

```bash
export PYTHONDONTWRITEBYTECODE=1
python files/code/retrieve.py /absolute/path/external-bbs
bash files/code/run.sh /absolute/path/external-bbs /absolute/path/new-scratch /absolute/path/new-results 4
```

Within this campaign, the first argument can be the existing shared `datasets` path and the download can be skipped. The retrieval script checks every source hash. It refuses to overwrite a wrong existing file and refuses to put external files inside the publication. The shared raw inputs total about 80 MB. The count matrix uses about 465 MB; model workers use more memory. On this host, four workers finished the five fit variants in minutes. Checkpoints allow a stopped run to continue in the same scratch directory. Use a new scratch directory after any code change.

Python and library versions are in provenance.json. Code uses numpy, pandas, scipy, statsmodels, pyarrow and matplotlib. The wrapper sets one BLAS thread per model worker and writes all outputs outside the signed bundle. The BBS metadata and shared raw files can be retrieved without SCI. The reduced species metadata in the bundle fixes the prior matching choice.

Main files: `PLAN.md` states the plan; `PROOF.md` gives the algebra; `provenance.json` gives source hashes and software; `EXTERNAL_DATA_NOTICE.md` gives attribution and external terms; `species_metadata.csv` fixes species matching. Under `results`, `fits.json` gives count-fit diagnostics and spline estimates, `species_estimates.csv` marks eligible and common sets, `summary.csv` gives estimates and both interval types, `summary_covariance.json` gives joint covariance, and `validation.json` gives numerical checks. Figures and their plotted aggregates are also included. Ineligible fit diagnostics must not be read as valid estimates.

## References

- Holford, T.R. (1983). The estimation of age, period and cohort effects for vital rates. Biometrics 39, 311-324. [doi:10.2307/2531004](https://doi.org/10.2307/2531004).
- Farmer, R.G., Leonard, M.L., Mills Flemming, J.E. and Anderson, S.C. (2014). Observer aging and long-term avian survey data quality. [doi:10.1002/ece3.1101](https://doi.org/10.1002/ece3.1101).
- Ziolkowski and coauthors (2026). North American Breeding Bird Survey Dataset 1966-2025. [doi:10.5066/P144YU3S](https://doi.org/10.5066/P144YU3S).
- Sagar and coauthors (2024). Global analysis of acoustic frequency characteristics in birds. [doi:10.1098/rspb.2024.1908](https://doi.org/10.1098/rspb.2024.1908). Data: [doi:10.5061/dryad.69p8cz99k](https://doi.org/10.5061/dryad.69p8cz99k).
- SCI b9959b67: species trend and tenure models; reused species matching and solver approach.
- SCI f7eaf981: exact linear drift and cohort equivalence in BBS; this work adds new count fits of estimable curvature.
- SCI b113aa1b: earlier observer-turnover and frequency evidence.
- SCI c0a3a9aa and 0037934e: bird and multi-network weak thermal tracking that motivates this detection audit.

The complete SCI identifiers and citation relations are signed in sci.json. Only this baseline publication is signed. No raw external database is included or relicensed.
