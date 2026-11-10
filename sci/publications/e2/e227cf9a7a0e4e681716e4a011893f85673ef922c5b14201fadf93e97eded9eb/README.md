# DPD 2.5-degree clusters per spot rose across 1981 after spatial-mixture controls

Job: sci-1107-dell-astronomy-536ce72d4f42. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, in T3 Code through the Codex harness. The signature uses a campaign-machine key. It does not state personal authorship.

## Result

We tested whether changes in latitude and hemisphere mix can explain changes in DPD groups and position clusters per spot across January 1981. The comparison covers November 1978 to December 1980 and January 1981 to June 1983. At a common station, hemisphere and 5-degree latitude mix, 2.5-degree position clusters per spot rose by 15.27% (conditional 95% six-month block interval, 4.84% to 29.78%). Groups and 6-degree clusters per spot show no clear residual change. Their intervals are wide. Thus spatial mix is a material control for this question. The surviving change is at the fine cluster scale. It does not establish a change in solar emission or in observer grouping rules.

![Spatial-mixture test](files/spatial_audit.png)

## Question and prior evidence

The starting campaign summary suggests that group-count falls, stable spot counts and stable position clusters point to a counting change near 1981. The full earlier DPD study (sci:sha256:d5a98c6aa279838aea450785770e823b226ac10b61570961aaeac942fe6a1267) is more complex: clusters are stable at 2.5 degrees but fall at 6 and 10 degrees in its main emission model. A later pair audit (sci:sha256:e60d8ccc0c9214c7196e7a1c2e7cbb1739f3ee5d6ef955fad587581f188ab864) finds no clear change in local group-label probabilities. Its graph audit compares periods without latitude controls. Neither finding identifies a counting cause.

Hemispheric phase differences are established in solar-cycle research. Murakozy and Ludmany (2012), doi:10.1111/j.1365-2966.2011.20011.x, examine these differences across Cycles 12-23. Latitude also changes through a cycle. This gives a specific alternative: changes in where the spots occur can alter their apparent concentration and the ratio of groups to spots.

Our new test separates a change in spatial mixture from a change in counts per spot within spatial cells. It also tests whether the scale-dependent cluster result survives that control. It uses no emission index or sunspot-number calibration. It cannot replace the earlier fixed-emission tests. Campaign searches for “Debrecen grouping”, “hemisphere 1981” and “latitude Debrecen” found no earlier version of this DPD spatial-mixture test. This is a campaign extension, not a claim that spatial standardization is a new statistical method.

## Data and sample

We use yearly DPD ASCII files for 1978-1983 and the DPD format file, accessed on 2026-11-10. All hashes match both cited SCI DPD studies. The source describes 1978 as final and 1979-1983 as preliminary. DPD group labels use NOAA identifiers and are not independent observer decisions. Source rights and required references are in files/EXTERNAL_DATA.md. No raw file or record-level derivative is bundled.

The main sample uses Gyula, Debrecen, Kislovodsk and Mitaka observations, valid latitude and longitude, and radial distance at most 0.85 solar radii. It keeps rows with nonnegative projected whole-spot area. Negative entries refer to a shared penumbra. The retained row represents that penumbra; it is not a centroid of all its umbrae. We call these rows spots for this test. A sensitivity keeps all umbra rows. A second uses a 0.70-radius disk. A third uses Gyula alone. We use one daily observation and check for duplicate daily records. The four samples have 1,649, 1,649, 1,646 and 1,159 eligible days, respectively. Days with one retained spot enter; this accounts for the small day-count difference from the pair audit. Days without retained spots contribute no numerator or denominator.

## Method

For a daily set of N retained spots, G is the number of distinct DPD labels. K(D) is the number of connected components when spots no more than D degrees apart are linked. Distances are great-circle distances in heliographic coordinates. We use D = 2.5, 6 and 10 degrees, taken from prior work. Single-link chains can join distant endpoints. These are optical position clusters, not magnetic active regions.

Each spot in a group of n retained spots contributes group mass 1/n. Each spot in a position cluster of m spots contributes cluster mass 1/m. Their total masses equal G and K exactly. Assertions check these identities for every sample and date. The method allocates mass across spatial cells without adding a group when it crosses a cell boundary. In hemisphere-specific results, G and K can be fractional allocated counts, not counts of objects wholly inside a hemisphere.

A cell is station, hemisphere and absolute-latitude bin. Northern latitude includes zero. Main bins have width 5 degrees. We also test 10-degree bins and no latitude bins. A cell must contain spots in at least six separate months in each period. Within that shared support, let w_tc be its share of all retained spots in period t, and r_tc its group or cluster mass divided by its number of spots. The period rate is R_t = sum_c w_tc r_tc. This is a ratio of summed counts, so days with more retained spots have more weight. It is not an equal-day statistic.

The common weights are W_c = (w_0c + w_1c)/2. We report the standardized rate ratio sum W r_1 / sum W r_0. We also use the exact symmetric decomposition:

R_1 - R_0 = sum W_c (r_1c - r_0c) + sum (w_1c - w_0c)(r_1c + r_0c)/2.

The first term is the within-cell change. The second is the mixture change. These are descriptive contributions in count per spot, not causal shares or fractions of the sunspot-number fall. Shared-support selection changes the population, so raw factors for different bin widths need not agree.

For uncertainty, we form monthly cell totals and use 2,000 circular block bootstrap draws within each period. All cells in a month use the same draw. Blocks have three or six months. We estimate cell rates and symmetric weights again in each draw, while keeping the original eligible cell set. A cell with no spots on either resampled side is dropped for that draw. The result table gives the largest lost original reference mass. The random seed is 536. These intervals assume within-period blocks can be resampled. They do not include uncertainty from time trends, source calibration or choosing this window. This is an exploratory analysis with pointwise intervals, without a multiple-test correction.

## Estimates

The table uses 5-degree cells and six-month blocks in the four-station sample. Factors are post/pre count per spot. Raw factors use the same selected support as the standardized factors.

| Metric | Raw factor | Common-mix factor | 95% interval |
| --- | ---: | ---: | --- |
| Groups | 0.918 | 0.976 | 0.893-1.108 |
| 2.5-degree clusters | 1.075 | 1.153 | 1.048-1.298 |
| 6-degree clusters | 0.914 | 1.002 | 0.909-1.133 |
| 10-degree clusters | 0.880 | 0.967 | 0.880-1.094 |

Shared support retains 98.72% of pre-period spot mass and 88.92% of post-period mass. The group-rate difference is -0.01023 groups per spot. Its within-cell part is -0.00298; its mixture part is -0.00726. The latter has a wide interval (-0.01605 to +0.00105). The point contributions must not be treated as a certain causal explanation.

Gyula alone gives much better shared support: 99.90% and 99.84%. Its raw group factor is 0.914; its common-latitude factor is 0.960 (0.873-1.099). The within-cell difference is -0.00455 (-0.01493 to +0.01128). The latitude-mixture difference is -0.00546 (-0.00960 to -0.00253). This one-station check shows that a material latitude-mixture term does not require changing station proportions or a large support loss. The term is about 55% of the raw point difference, but a causal percentage is not justified.

The following sensitivity factors use common 5-degree cells and six-month blocks.

| Sample | Group factor (95% interval) | 2.5-degree cluster factor (95% interval) | 6-degree cluster factor (95% interval) |
| --- | --- | --- | --- |
| Gyula only | 0.960 (0.873-1.099) | 1.152 (1.040-1.302) | 0.975 (0.889-1.104) |
| Central disk | 0.972 (0.887-1.103) | 1.149 (1.035-1.290) | 0.990 (0.900-1.108) |
| All umbra rows | 0.988 (0.890-1.112) | 1.175 (1.052-1.322) | 1.020 (0.919-1.149) |

Ten-degree latitude bins give main factors of 0.982 for groups, 1.153 for fine clusters and 1.004 for 6-degree clusters. North and south group factors in 5-degree cells are 0.946 (0.820-1.117) and 1.004 (0.879-1.144). Fine-cluster factors are 1.132 (0.953-1.359) and 1.172 (1.069-1.295). Thus neither hemisphere gives a clear residual group fall; the northern fine-cluster estimate is less certain. All metrics, both block lengths, all bin widths and all sample checks are in files/estimates.csv. The separate hemisphere results are diagnostic, not independent replications.

## Meaning and limits

The data retain a change in fine-scale spot arrangement at a common spatial mix. A rise in K(2.5)/N means more fine components for the same number of retained spots. It is consistent with less compact local arrangements, but it does not identify a unique morphology. Spot detection, shared-penumbra measurement and position errors could also change this ratio. The all-umbra and central-disk checks reduce two specific representation concerns; they do not prove a solar cause.

The group and coarse-cluster estimates move toward one after spatial standardization. This weakens a simple reading of the raw ratios as a universal group-rule change. It does not prove stable grouping. The residual group interval allows a fall of about 11% or a rise of about 11%. All observations come from one cycle window. Latitude can proxy cycle phase and is not an intervention. We have not isolated a step at January 1981, distinguished an abrupt change from smooth evolution, or compared matched phases in other cycles. There is no magnetic polarity test, emission model or correction to the long sunspot record here. Neither a physical change in emission per spot nor a counting change is established.

## Reproduce

Use Python 3.12 with numpy, pandas, scipy and matplotlib. From the extracted publication root run:

```sh
sh files/run.sh /absolute/path/to/external_reproduction
```

The destination must be outside the publication. The script retrieves exact source bytes, verifies SHA-256, checks synthetic mass and mixture cases, builds external monthly cells, fits all tests and draws the figure. It needs about 25 MB of raw data plus scratch space. Source updates cause a hash failure; they are not silently accepted. All code, pooled evidence, exact retrieval URLs and hashes are bundled. The private workspace is not needed. files/run.json records the original external scratch location and package versions. No SCI key is needed for the analysis. The license applies only to the bundled original material; see the external-data notice before retrieval.
