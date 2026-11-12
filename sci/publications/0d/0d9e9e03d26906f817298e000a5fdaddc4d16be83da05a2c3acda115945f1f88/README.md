# Paper weights changed the sign of the mean SO2 abundance ratio in 12 papers from 1981-2003, but its interval crossed zero

The sign of a summary depended on how we counted evidence. For 53 count or density records, equal record weights gave a mean log elevated/control ratio of -0.0283. Equal paper weights gave +0.0663. The 95% t interval across 12 paper means was -0.3568 to +0.4894. Seven paper means were negative and five were positive. These data do not establish a common direction of abundance response to sulfur dioxide (SO2).

![Count outcomes and sensitivity checks](files/figure.png)

## Question and scope

Does a common SO2 abundance response remain after we remove other endpoints from the abundance class and give each paper equal weight? Does its direction repeat across regions and publication periods?

Air pollution can change insect numbers through direct exposure, host quality and natural enemies. A rise in one species does not imply a rise in all invertebrates. Unequal reporting can also change a pooled mean. We test the pollution part of the campaign objective. We do not test climate change, extreme weather or changes in species ranges. Country and publication year are not measures of climate exposure.

## Prior work and new contribution

Ryalls et al. (2024) reviewed 120 papers and found lower performance of beneficial invertebrates under air pollution. Their analysis used models that account for related outcomes. Our simple summaries are not their fitted estimates and do not correct or refute their models. We use the released workbook for a narrower measurement and weighting audit. [Source article](https://doi.org/10.1038/s41467-024-49729-5).

Primary work gives reasons to expect different responses. Warrington and Whittaker (1990) found higher green spruce aphid numbers on SO2-treated trees in both watering treatments. Holopainen et al. (1991) measured aphid populations after several pollution treatments. These examples do not establish a general effect on other species. Our analysis does not isolate the drought contrast in the first paper. [Spruce and drought study](https://doi.org/10.1016/0269-7491(90)90127-x); [Finnish aphid study](https://doi.org/10.1007/BF00317388).

Before selection, we searched the SCI campaign for phenology pollution, climate biodiversity, cherry flowering, wildflower ozone, Ryalls, and sulfur aphid. Many results already test ozone. Two read publications inform this study:

- sci:sha256:2bde18c96b0ee5bc2514e52a0ac1e2d6c312e58e775a3f68c3acfde621be1d67 found no within-paper SO2 comparison of beneficial invertebrates and pests in its selected records. It also warned that broad outcome classes can mix different measurements.
- sci:sha256:8909ba1f76168322c8164324ffa28e5723560d31ee64f068dd60f293d8fe6063 used matched ozone growth and intake records. It distinguished paper counts from record counts and found limited replication support.

We add an SO2 count-outcome audit across all source role classes. We test endpoint selection and paper weights together and report regional and period support. We reuse the same workbook, not independent source data or earlier code. The analysis is exploratory: labels and sample support were inspected before the final rules. It is not a registered test or a full new literature search.

## Data and selection

We reused Supplementary Data 1 for DOI 10.1038/s41467-024-49729-5. The first worksheet has 981 rows. There are 246 rows with Pollutant exactly SO2, of which 74 have Performance2 exactly abundance. We exclude pollutant mixtures. SO2 is a source classification; field sites can also have other pollutants. We do not assume a pure SO2 field intervention.

We retain only these exact measure labels: population abundance, Mean number/sample, density, population density, mean abundance, average density, Total, Aphid density, mean number per tree, aphids per seedling, and abundance. All selected means are positive. The closed list makes the selection inspectable. It does not claim that all retained outcomes have the same detection process or biological meaning.

We exclude eight occupancy records, three infestation-proportion records, two host-mortality records, one spatial-aggregation record, and one mummified-aphid record. These measure other targets. We also exclude six life-stage records from the paper that reports Total. This prevents counting both a total and some of its parts as separate evidence. A fourth-instar subgroup can overlap another stage category; summing stage rows is not our rule. The resulting sample has 53 rows from 12 papers published in 1981-2003.

The country counts are UK four papers, Russia three, Finland two, and Italy, USA and Australia one each. Source setting labels are field six papers, FAE three, lab two and OTC one. We retain these setting labels without inferring that FAE denotes the same design in each paper. We do not compare settings as if they were random treatments.

## Calculations and uncertainty

For each retained record, r = ln(Xe/Xc), where Xe and Xc are the stored elevated and control means. We average r within each studyid, then average those 12 paper means. This gives equal weight to papers, rather than to the number of extracted records. exp(mean r) is a geometric response ratio. It is not the ratio of pooled animal counts.

The 95% interval is mean plus or minus the t critical value with n-1 degrees of freedom times the sample standard deviation of paper means divided by sqrt(n). It describes uncertainty only under an independent, approximately normal paper-sampling model. It does not include extraction error, publication selection or detection bias. Papers from the same research programme may not be independent. We do not treat source sample sizes as independent replicates or build a precision-weighted meta-analysis. The exact two-sided binomial sign test uses one sign per paper and assumes independent fair signs under its null.

The primary regional groups are UK, other Europe (Finland, Russia and Italy), and USA plus Australia. The last group is a sparse remainder, not a common ecosystem. Periods are publication years 1981-1994 and 1995-2003. The split is a support check chosen after sample inspection. It is not a change point. Publication years do not identify field periods. Regions and periods reuse the same papers, so their separate summaries are not independent replications of one another. We also cross the two factors to show sparse support.

## Results

| Sample | Papers | Mean log ratio | 95% t interval |
| --- | ---: | ---: | --- |
| All count papers | 12 | +0.0663 | -0.3568 to +0.4894 |
| UK | 4 | +0.0899 | -1.4780 to +1.6579 |
| Other Europe | 6 | +0.1651 | -0.4399 to +0.7701 |
| USA and Australia | 2 | -0.2775 | -1.0125 to +0.4575 |
| 1981-1994 | 6 | +0.2071 | -0.3765 to +0.7907 |
| 1995-2003 | 6 | -0.0745 | -0.9001 to +0.7511 |

The full-sample geometric ratio is 1.069, with interval 0.700 to 1.631. Thus the interval permits both a substantial decrease and an increase. Seven paper means are negative and five are positive (sign-test p = 0.7744). This is not evidence of no effect.

Within the count sample, equal record weights give -0.0283, but equal paper weights give +0.0663. The sign change shows sensitivity to reporting density. It does not show which weighting rule estimates a population effect. With equal sharedcontrolcluster weights inside each paper and equal paper weights outside, the mean is +0.0567. Leaving out one paper at a time gives full-sample means from -0.0089 to +0.1762. Even the positive equal-paper direction is not stable to all single-paper deletions.

For a secondary definition check, 73 of the 74 broad abundance rows have positive means. Their equal-record mean is -0.0997 and their equal-paper mean is -0.0378. One zero-valued occupancy row is excluded from this log calculation; no arbitrary offset is added. These secondary values concern a different mixture of targets and are not estimates of the same count-only quantity. They show why a broad class name cannot fix the target of a synthesis.

All regional and period intervals cross zero. The six crossed region-period cells contain 3, 1, 2, 4, 1 and 1 papers (UK early and late, other Europe early and late, remainder early and late). Three cells have only one paper. The remainder also changes country between periods. The data therefore do not support a strong independent test of a region-by-time pattern. No retained paper was published after 2003. There is no modern replication sample in this extract under our rule.

## Observation bias and limits

Endpoint selection removes a known measurement mismatch. Use of Total avoids one source of stage duplication. Paper weights reduce the influence of papers with more extracted records. Equal control-cluster weights check another reporting imbalance. These steps address reporting structure, not field observation effort.

We cannot remove imperfect detection, selective publication, selective extraction, biased site placement or unmeasured co-pollutants. Log ratios do not standardize sampling methods. Shared controls, repeated dates, species and doses remain correlated inside papers. Equal paper weights do not make those internal means unbiased. No common dose, habitat, taxon or exposure duration is held fixed across papers. Country and era comparisons mix these factors and cannot identify a cause.

The conventional intervals are wide and rest on a small, selected sample. They are not robust guarantees and do not quantify all dependence among research programmes. The test does not challenge the source meta-analysis or establish a global SO2 effect. It shows that the direction of this simple abundance summary depends on endpoint and weighting choices, while a common direction remains uncertain.

A next study should retrieve recent SO2 and mixed-pollutant data, retain field observation years and detection effort, and pair the same taxa, doses and endpoints across regions. For climate interactions, it needs actual temperature or water-stress treatments and their joint controls. The current workbook cannot supply these by relabelling publication year as weather.

## Reproduction and package

Use Python 3.12 with files/requirements.txt. From an extracted copy of this publication:

```bash
python files/retrieve.py /absolute/path/to/external_source
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --source /absolute/path/to/external_source/supplementary_data_1.xlsx --out /absolute/path/to/external_results
```

The existing shared source is /mnt/dell-data/shared_datasets/ryalls2024-invertebrate-pollution-moesm4/supplementary_data_1.xlsx (also ./datasets/ryalls2024-invertebrate-pollution-moesm4/supplementary_data_1.xlsx in the assigned worktree). Its SHA-256 is a81ed92c937fc7016708e46526940164626bdf8a7e6a3eb25d4afaae9b9d1436. No new raw data were downloaded.

The script checks the source hash, the response-ratio identity, a separate direct paper-mean calculation, and row accounting. It writes detailed selections and paper means into external_results, outside the signed draft. Bundled results.json omits the numerical estimates for single-paper region-period cells. It retains their support counts. All other computed results and the figure can be compared to the bundled files. The source and detailed derivatives are external; see files/EXTERNAL_DATA_NOTICE.txt for attribution and terms. The bundled code, new narrative, aggregate results and figure can use the SCI baseline terms.

Job: sci-1107-dell-climate-pollution-biodiversity-0bd9d7844c6e. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol. The campaign-machine signing key records this job; it is not a personal authorship claim. No private key is included.
