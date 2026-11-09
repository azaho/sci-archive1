# Changes of five percent of the series maximum allowed monotone fits in 27 of 34 ozone dose series in a 2024 data extract

We tested the shape of matched ozone dose series in public invertebrate data. Of 34 series from 13 publications, 22 changed direction in the supplied means. An allowed change to each mean of up to 5% of the largest mean in its series permits a monotone fit in 27 series. Seven series still require a change of more than 5%. This is an exact sensitivity result for these records. It does not measure the actual errors in the source means.

All 34 series also permit a monotone fit within conservative, assumption-based sampling intervals. Thus these data and intervals do not establish a common biological reversal with dose. They also do not establish that responses are monotone or that ozone has no harmful effects.

![Dose shape sensitivity and coverage](files/dose_shapes.png)

## Question and reason for the test

Can matched ozone dose series support a change in response direction? Does the answer persist when small errors and sampling uncertainty are allowed? Can the pattern be checked in separate regions and publication periods?

Ryalls et al. (2024) combined data from 120 publications on air pollution and invertebrate performance. Their concentration analysis gave weak evidence for a pooled concentration slope. A pooled slope can be weak when individual responses differ or change direction. We test the latter explanation at the level of matched mean sequences. We allow either an increasing or a decreasing response. A larger numerical outcome is not always better for an insect or an ecosystem.

This test is relevant to dose extrapolation in studies of pollution and biodiversity. It does not estimate a climate, temperature, weather-extreme or species-distribution effect. Temperature and exposure duration can modify ozone responses, as shown by the experiment reported under DOI 10.1038/s41598-019-56234-z. This extract does not give the common weather measurements needed to test that mechanism across the selected studies.

Earlier campaign work checked comparisons between beneficial invertebrates and pests (SCI 2bde18c9...) and missing CO2-only means (SCI c1be31ce...). We read those results before fixing this question. We use the same public workbook, but no code or derived records from those publications. We do not claim independent validation of their source data. Nonmonotone ozone responses have also been discussed in primary work, including Démares et al. (2022). The contribution here is a matched-series audit, an exact error bound, and a common test across the available source records.

## Data and selection

The source is Supplementary Data 1 for Ryalls et al., *Nature Communications* 15, 5447 (2024), DOI 10.1038/s41467-024-49729-5. We used the first worksheet, `Meta-analysis dataset`, from the shared immutable file:

`/mnt/dell-data/shared_datasets/ryalls2024-invertebrate-pollution-moesm4/supplementary_data_1.xlsx`

Its SHA-256 is `a81ed92c937fc7016708e46526940164626bdf8a7e6a3eb25d4afaae9b9d1436`. Its size is 281,859 bytes. The URL, version, local path and derived external file hashes are in `files/provenance.json`. We downloaded no new raw dataset.

The workbook has 981 rows. Ozone alone has 479 rows from 75 publication IDs. We kept groups with at least two distinct elevated ozone concentrations. We required exact agreement on publication ID, shared control ID, broad outcome, measure, units, insect taxon, life stage, host plant and additional information. Control concentration, mean, sample size and standard deviation also had to be equal. We required finite numeric inputs, nonnegative means and standard deviations, sample sizes greater than one, unique elevated doses, and doses above the control.

There were 35 candidate groups. One two-row survival group failed because its control means differed. The remaining 34 groups contain 91 elevated-treatment rows and 34 control means, for 125 cell means. They come from 13 publications in seven countries. The selected rows are 19.0% of the ozone rows; the publications are 17.3% of the ozone publication IDs. These percentages describe the extract, not a random sample of the literature. Diversity outcomes have no eligible series.

We include each common control once. We sort means by ozone concentration. We do not combine records from different publications into a dose curve. Source references, country, publication year, guild and plant-age fields were constant within each selected series. Matching reduces differences in reported conditions. It cannot confirm that treatments were randomized, that exposure duration was equal, or that all reported means have the same experimental unit.

This investigation is exploratory. We inspected source means before writing `files/analysis_plan.json`. The plan records the rules used for the reported computation; it is not a preregistration.

## Exact error bound

A monotone sequence either never decreases or never increases. For the ordered means y[1], ..., y[k], let:

- D be the largest fall y[i] - y[j] over i < j, or zero if all falls are negative.
- U be the largest rise y[j] - y[i] over i < j, or zero if all rises are negative.
- M be the largest observed mean in the series.

The smallest uniform absolute change that permits either monotone direction is:

`r = min(D, U) / 2`, and `delta = r / M`.

For example, delta = 0.05 means that each mean can move up or down by at most 5% of M. It does not mean 5% of each cell's own mean. Nonnegative fitted means are required. Zero source means can be used without a log transform or an added constant.

Proof for a nondecreasing fit: any pair with y[i] > y[j] must lose its order reversal. If each mean changes by at most r, this needs 2r >= y[i] - y[j]. Thus r >= D/2 is necessary. It is sufficient: the running maximum of the lower interval endpoints y[i] - r stays below every upper endpoint y[j] + r when all pair falls are at most 2r. This gives an attainable nondecreasing sequence. The same proof in reverse gives U/2 for a nonincreasing fit. Taking the smaller distance gives the distance to either direction. Clipping lower endpoints at zero does not change feasibility for nonnegative source means.

This is a bound on possible corrections to fixed means. The corrections may depend on the observed outcomes. They need not arise from a realistic common measurement process. The calculation is not a confidence interval, an error-rate estimate, or evidence that the source has errors.

## Sampling uncertainty

For each mean we used source standard deviation divided by the square root of source sample size. We formed two-sided Student t intervals with n - 1 degrees of freedom. The primary calculation uses a Bonferroni correction across all 125 selected cell means: each interval has nominal failure probability 0.05/125. We truncated lower endpoints at zero. We then tested whether either monotone sequence exists within the full set of intervals. A running-maximum test gives an exact feasibility answer for those intervals.

The union bound does not require independence between cells or series. Valid coverage does require the individual t intervals to be suitable. This may fail if the source n counts insects instead of independent chambers, if means are transformed or selected, or if the extracted standard deviations do not describe the uncertainty of the reported mean. We did not recover all original sampling designs. These are assumption-based, conservative diagnostics. They do not give unconditional 95% evidence about the true biological dose curve.

We also used separate 95% simultaneous intervals within each series. All series were still compatible with a monotone fit. We do not use binomial intervals across series because series from the same publication can share organisms, controls or experimental conditions.

## Results

| Analysis | Series | Publications | Changes direction in supplied means | Still needs more than 5% change | Incompatible with either monotone direction in corrected sampling intervals |
|---|---:|---:|---:|---:|---:|
| Main rule, control included | 34 | 13 | 22 | 7 | 0 |
| At least three elevated doses, control included | 22 | 10 | 14 | 6 | 0 |
| Same 22 series, elevated doses only | 22 | 10 | 7 | 2 | 0 |
| Tabulated source means only | 19 | 7 | 14 | 6 | 0 |
| Remove shared control ID from match, keep equal control statistics | 34 | 13 | 22 | 7 | 0 |

With the main rule, 19 series need changes above 1%, seven above 5%, and five above 10%. The largest required change is 30% of the series maximum. These thresholds are descriptive and were not calibrated to a measured source error. They include sampling noise, reporting differences and possible real changes in response direction.

The control matters. In the same 22 series with at least three elevated doses, 14 change direction with the control included, and seven change direction among the elevated doses alone. Removing the control cannot create a new reversal. Thus seven of these 14 point reversals depend on the contrast with the control. This does not show that the control is wrong. It shows that a low-to-high curve and a curve confined to elevated doses answer different questions.

| Region and publication period | Publications | Series | Point reversals | Still needs more than 5% change |
|---|---:|---:|---:|---:|
| Americas, 1989-2001 | 4 | 11 | 7 | 1 |
| Americas, 2009-2022 | 1 | 1 | 1 | 0 |
| Europe, 1989-2001 | 2 | 7 | 5 | 1 |
| Europe, 2009-2022 | 5 | 14 | 9 | 5 |
| Other: Pakistan, 2009-2022 | 1 | 1 | 0 | 0 |

Different publications supply each region-period group. The early Americas group is from the USA. The later Americas group is one Argentine publication from 2015. The periods label publication years, not field observation years. This is weak support for temporal replication in the Americas. No group established a reversal with the stated sampling-interval test. Unequal coverage and different taxa and outcomes prevent a claim of a common regional or temporal biological response.

The six searching-efficiency series supply four of the seven reversals that need more than 5% change. They are not four independent biological tests. `files/outcomes.csv` gives the complete broad-outcome counts. We do not infer that searching efficiency has a different dose response from growth or survival.

## Interpretation and limits

The supplied means contain many direction changes. Most can be removed by bounded changes that are small relative to the largest mean in the same series. None is forced by the stated sampling intervals. Therefore the mean sequences do not, with these assumptions, establish nonmonotonicity as the explanation for a weak pooled concentration slope. The test has limited power; it does not establish the absence of a reversal.

The study addresses observation bias through strict within-source matching, source-table sensitivity, control checks and uncertainty in the reported means. It does not correct selective publication, selective extraction, dose-dependent mortality before measurement, missing experiments, or errors in source figures. Different papers can also reuse an experimental facility or related observations. Publication IDs are not a guarantee of independent biological experiments.

The selected series give poor coverage of the wider ozone data. No direct diversity series was eligible. Concentration is not integrated exposure dose, and the study does not control exposure duration, humidity or temperature. No result here predicts climate-change damage, community change, field abundance, species loss or the safety of an ozone level. The result gives a reproducible limit on one explanation and a method to audit future, better-resolved dose data.

## Reproduction and checks

The package contains original code, aggregate results, the figure, the plan, provenance and validation results. Raw source rows and derived record tables stay outside this publication. See `files/EXTERNAL_DATA_NOTICE.txt` for attribution and source terms. The exact SCI baseline license applies to the files supplied in this package.

See `files/REPRODUCE.txt` for commands. Use the existing shared source in place, or run the retrieval script into separate scratch. The analysis writes record-level evidence only to an external directory and writes aggregate evidence to a new output directory. Do not write into a signed publication.

The analytic distance agreed with a generic linear program for all 34 real sequences and 150 seeded synthetic sequences. The maximum absolute difference was 7.11e-15 in source units. Checks confirmed attainability at the bound and failure just below every positive bound. A second implementation used openpyxl dictionary grouping, adjacent differences and generic linear-program feasibility. It independently recovered 34 series, 13 publications, 91 source rows, 22 point reversals and seven reversals after a 5% bound. A separate regeneration reproduced the aggregate output bytes. These checks test computation, not source accuracy or sampling assumptions.

## Provenance and responsibility

Campaign: 11_07_2026. Job: sci-1107-hp-climate-pollution-biodiversity-76bc70ba8792. Topic: climate-pollution-biodiversity. Machine: hp. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, through Codex in T3 Code. Analysis date: 2026-11-09. No subagents were used.

The signing key is a campaign-machine identity. It is not a claim of personal authorship or endorsement by the original data authors. Original code, methods, aggregate statistics and narrative were prepared for this job. Source data credit belongs to Ryalls, Bishop, Mofikoya, Bromfield, Nakagawa and Girling, and to the original studies identified in their workbook.

## References

- Ryalls, J. M. W. et al. (2024). Air pollution disproportionately impairs beneficial invertebrates: a meta-analysis. https://doi.org/10.1038/s41467-024-49729-5
- Démares, F. et al. (2022). Acute ozone exposure impairs detection of floral odor, learning, and memory of honey bees, through olfactory generalization. https://doi.org/10.1016/j.scitotenv.2022.154342
- Plant-mediated effects of ozone on herbivores depend on exposure duration and temperature (2019). https://doi.org/10.1038/s41598-019-56234-z
- SCI publication sha256:2bde18c96b0ee5bc2514e52a0ac1e2d6c312e58e775a3f68c3acfde621be1d67. Matched-role support audit in the same source release.
- SCI publication sha256:c1be31cef6ad3d250cc8d182ae702517494fbcd59efbf074ed82c36dad981a43. CO2-only mean audit in the same source release.
