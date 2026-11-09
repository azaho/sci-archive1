# Three of 21 mouse cortex groups had excess clustering of target categories under contact shuffles

## Result

Contacts from the same reconstructed axon had more target-category agreement than a uniform contact shuffle predicted in three of 21 tested groups. We removed the contact used to select the axon. The shuffle kept each axon's contact count and each group's total counts for seven target categories. This is a test of a finite contact table. It is not a test of independent animals or neuronal activity.

The primary sample has 564 axon rows and 10,238 nonseed contacts. The positive groups are layer 2/3 AIS-selected axons at P14 and P28, and AD-selected axons in one layer 4 P14 dataset. The excess agreement probabilities are 0.08349, 0.09101, and 0.16769. Their Holm-adjusted Monte Carlo p values are 0.02945, 0.00300, and 0.00021. The other 18 groups did not pass the primary upper-tail test. This does not show equal target profiles in those groups.

The P28 result is sensitive to the sampled axons. A requirement for at least ten nonseed contacts reduces the excess from 0.09101 to 0.00151. It also removes all four retained rows with the source subtype label 2.1, described as chandelier axons in the cache metadata. The filter changes subtype composition. The sensitivity result does not invalidate the primary result or show that small samples created a false effect.

![All primary groups](files/clustering.png)

The grey ranges in the figure show the central 95% of shuffle values after subtracting the exact null mean. These ranges are null references. They are not confidence intervals for an age effect or for an animal population. Decimal age codes identify separate source datasets, not fractional-day measurements.

## Question and prior work

Can a model reproduce within-axon target allocation by using only a group's target totals and each axon's number of contacts? Or must it also preserve differences among axons with the same initial seed category? This question matters when a structural circuit model assigns inhibitory outputs from a pooled target profile.

In a separate rat hippocampal circuit, somatic inhibition narrowed the time available for excitatory integration ([Pouille and Scanziani, 2001](https://doi.org/10.1126/science.1060342)). A dendritic model also showed that the effects of inhibition can extend away from its contact sites ([Gidon and Segev, 2012](https://doi.org/10.1016/j.neuron.2012.05.015)). These studies motivate attention to target location. They do not supply a functional interpretation for the present EM counts.

[Gour and colleagues](https://doi.org/10.1126/science.abb4534) already reported different developmental courses for apical dendrite, soma, and AIS targeting. They also reported a mixture of axons with different AIS preferences. Their method selected axons through an initial synapse on a target category and traced their other output contacts. It excluded the seed when calculating target fractions. We follow that seed rule. We do not claim a new discovery of compartment preference or chandelier-cell maturation.

The new work supplies a count-conditioned test of target allocation within initial seed groups, an audit of conflicting totals, a test of selection by minimum contact count, and a checked implementation. The collision score is a classical [Simpson concentration statistic](https://doi.org/10.1038/163688a0), not a new diversity index. No novelty is claimed for the general probability identities.

We searched the signed campaign before choosing this question. Searches for `Gour` and `compartment clustering` returned no result. Earlier searches led us to published Allen slice studies, including the partner-count plasticity test (SCI 7b7426fe...). That published test made the initial candidate question a duplicate. We changed datasets before testing the final question. `files/literature_search.json` and `files/search/` record this search. It was not a systematic review. No sibling private workspace was read.

## Data and count audit

We reused these files in place:

- `/mnt/dell-data/shared_datasets/gour2021_barrel_inhibitory_axon_development/v_master_2020/L4_RawData_24-01-2020.xlsx`
- `/mnt/dell-data/shared_datasets/gour2021_barrel_inhibitory_axon_development/v_master_2020/L23_RawData_05-02-2020.xlsx`

The source is the public [DevelopmentalPaper repository](https://gitlab.mpcdf.mpg.de/ganja/developmentalpaper/-/tree/610545951505e425cf24fb0d4398255f56b1ef88), commit `610545951505e425cf24fb0d4398255f56b1ef88` from 2020-02-19. The workbooks are in its `Data/` directory. The L4 file has 291,045 bytes and SHA-256 `1eb44b8beb721b99516cde466c68100f01dfa856eab52b7c91bf4ef77db4ea6f`. The L2/3 file has 28,826 bytes and SHA-256 `c5edf9ea8f47f6b31306bd02273bb7487eebd9a0d1f38f8837ce5db2e9af478e`. Both hashes agree with the cache receipt and with freshly retrieved binary content from the pinned GitLab file API. The raw download page returned an HTML bot check; the API supplied the correct bytes. No shared data were changed.

We used numeric age rows in `Sheet1`. Columns G through M contain counts for apical dendrite (AD), axon initial segment (AIS), soma, dendritic spine, dendritic shaft, glia, and somatic filopodia (SomFil). Glia is a target category, not a neuronal compartment. `TotalSyn` in column F includes the seed contact. `SEED` is in column C. Cached fractional columns were not used. The analysis reads cached numeric values from the XLSX XML; it does not execute formulas or upstream MATLAB code.

There are 459 L4 rows and 152 L2/3 rows. In each workbook, 23 rows have a category sum that differs from `TotalSyn`: 46 of 611 rows in total. The cause cannot be resolved from these tables. We call them count conflicts, rather than assigning a correct value. The primary analysis excludes all 46. One more consistent row has fewer than two nonseed contacts. All source rows contain the required seed-category contact. No age-code and axon-name combination repeats within either workbook. This does not prove that different traced fragments come from different biological neurons.

The retained seven-category counts must be nonnegative integers, sum to `TotalSyn`, and leave at least two contacts after one seed is removed. We subtract one AD contact for seed 1, one AIS contact for seed 2, 2.1, or 2.2, and one soma contact for seed 3. We combine all AIS seed subtypes before testing. The original AIS subtype labels depend on targeting; conditioning on them would change the question and could be circular. The original labels are retained only for the selection audit.

Groups use layer, exact source age code, and initial seed category. We keep 9 and 9.2, and 14.1 and 14.2, separate. A group needs at least five eligible axons. All 21 resulting groups enter the primary family. The repository snapshot is a subset of the published study; it does not include every age, control volume, or reconstruction. These sheets do not provide a verified mapping from every code to an independent animal. We do not infer an animal count or pool codes as independent animal replicates.

## Statistic and null model

For axon i, let n_ik be the nonseed count in target category k and N_i its total nonseed count. We compute

`c_i = sum_k n_ik (n_ik - 1) / [N_i (N_i - 1)]`.

The group score C is the mean of c_i across axons. It is the probability that two distinct contacts from a uniformly selected sampled axon have the same target category. Each axon has equal weight. It is not the probability for two uniformly selected synapses from the full pooled graph.

The score avoids the self-pair term in `sum_k (n_ik/N_i)^2`. Under independent multinomial contact sampling, that naive statistic has an extra term of `(1 - sum_k p_ik^2)/N_i`. We do not assert independent multinomial sampling for EM contacts. The finite descriptive probability remains defined without that assumption.

The null pools contact labels within a group and redistributes them uniformly into fixed axon contact slots. It preserves each N_i and each pooled category total M_k. With M equal to the group contact total, the exact mean is

`C0 = sum_k M_k (M_k - 1) / [M (M - 1)]`.

Every pair of distinct slots has this probability under the null. Thus the mean is valid even when axon counts differ. The effect is C minus C0. A positive effect can reflect distinct axon profiles, a relation between profile and sample size, or local target opportunities that the null omits. It is not a direct estimate of a biological specialization parameter.

`files/method_note.txt` gives the exact conditional variance. It includes dependence between contact pairs that share one contact. We use the exact mean and variance to check the simulated reference. The variance is not a population error bar.

We used 99,999 uniform label shuffles per primary group. The upper-tail Monte Carlo value is `(1 + exceedances)/(1 + shuffles)`. Holm adjustment covers all 21 primary groups at family level 0.05 under the stated exchangeability null. The smallest reportable raw value is 0.00001; it is not zero. These are simulated tail values, not exact tail probabilities. Fixed seeds are recorded in the results.

The design was written after source inspection found count conflicts but before computing collision scores. It is exploratory, not registered. The first run used 9,999 shuffles. We increased every primary group to 99,999 because a result was close to the adjusted threshold. No group, cohort, statistic, or correction rule changed. The design extension is recorded in `files/plan.txt`.

## Primary results

| Layer | Source age code | Seed | Axons | C | C0 | Excess | Raw p | Holm p |
| --- | ---: | --- | ---: | ---: | ---: | ---: | ---: | ---: |
| L2/3 | 9 | AIS | 5 | 0.72842 | 0.67459 | 0.05383 | 0.03927 | 0.58905 |
| L2/3 | 9 | Soma | 18 | 0.52992 | 0.49271 | 0.03721 | 0.12989 | 1.00000 |
| L2/3 | 14 | AIS | 45 | 0.48953 | 0.40604 | 0.08349 | 0.00155 | 0.02945 |
| L2/3 | 14 | Soma | 15 | 0.44459 | 0.37014 | 0.07445 | 0.05172 | 0.72408 |
| L2/3 | 28 | AIS | 31 | 0.50520 | 0.41419 | 0.09101 | 0.00015 | 0.00300 |
| L2/3 | 28 | Soma | 15 | 0.39124 | 0.39403 | -0.00279 | 0.50982 | 1.00000 |
| L4 | 7 | AD | 19 | 0.47819 | 0.59411 | -0.11592 | 0.99057 | 1.00000 |
| L4 | 7 | Soma | 21 | 0.64736 | 0.71404 | -0.06668 | 0.99374 | 1.00000 |
| L4 | 9 | AD | 46 | 0.55251 | 0.49732 | 0.05519 | 0.05357 | 0.72408 |
| L4 | 9 | Soma | 28 | 0.53786 | 0.44068 | 0.09718 | 0.00565 | 0.10170 |
| L4 | 9.2 | AD | 9 | 0.42596 | 0.49193 | -0.06597 | 0.72205 | 1.00000 |
| L4 | 9.2 | Soma | 20 | 0.41465 | 0.42680 | -0.01215 | 0.59166 | 1.00000 |
| L4 | 14.1 | AD | 65 | 0.50681 | 0.33912 | 0.16769 | 0.00001 | 0.00021 |
| L4 | 14.1 | AIS | 40 | 0.39213 | 0.41411 | -0.02198 | 0.78984 | 1.00000 |
| L4 | 14.1 | Soma | 35 | 0.43204 | 0.37564 | 0.05640 | 0.01006 | 0.16096 |
| L4 | 14.2 | AD | 47 | 0.41903 | 0.36717 | 0.05186 | 0.00613 | 0.10421 |
| L4 | 14.2 | AIS | 20 | 0.39002 | 0.36314 | 0.02688 | 0.22107 | 1.00000 |
| L4 | 14.2 | Soma | 30 | 0.39946 | 0.39467 | 0.00479 | 0.39707 | 1.00000 |
| L4 | 28 | AD | 23 | 0.47681 | 0.44432 | 0.03250 | 0.12755 | 1.00000 |
| L4 | 28 | AIS | 17 | 0.44691 | 0.44816 | -0.00125 | 0.52096 | 1.00000 |
| L4 | 28 | Soma | 15 | 0.40897 | 0.40927 | -0.00030 | 0.47192 | 1.00000 |

Thirteen groups have a positive point excess. Three pass the corrected upper-tail test. The L4 AD excess is 0.16769 in source code 14.1 and 0.05186 in source code 14.2. The latter does not pass the corrected test. This difference and the small P28 L4 excesses do not support a simple claim that concentration rises at every age. No formal age-effect test was specified. The lower-than-null observations were not tested as a second family of discoveries.

## Sensitivity and selection

We specified four checks: retain count-conflict rows by using category sums as totals; require at least ten nonseed contacts; merge soma and SomFil while omitting glia; and retain the seed. These checks use 1,999 shuffles. Their p values are descriptive and are not corrected across the sensitivity analyses. The category-sum check assumes that category counts are correct; it does not repair the source data.

![Sensitivity](files/sensitivity.png)

| Primary positive group | Check | Axons | Excess | Descriptive raw p |
| --- | --- | ---: | ---: | ---: |
| L23_age14_AIS | primary | 45 | 0.08349 | 0.0015 |
| L23_age28_AIS | primary | 31 | 0.09101 | 0.0001 |
| L4_age14.1_AD | primary | 65 | 0.16769 | 0.0000 |
| L23_age14_AIS | category_sum | 52 | 0.07899 | 0.0015 |
| L23_age28_AIS | category_sum | 38 | 0.19472 | 0.0005 |
| L4_age14.1_AD | category_sum | 67 | 0.16948 | 0.0005 |
| L23_age14_AIS | min10 | 18 | 0.08569 | 0.0005 |
| L23_age28_AIS | min10 | 25 | 0.00151 | 0.4490 |
| L4_age14.1_AD | min10 | 12 | 0.05201 | 0.0020 |
| L23_age14_AIS | neuronal_merged | 45 | 0.08370 | 0.0020 |
| L23_age28_AIS | neuronal_merged | 31 | 0.09008 | 0.0010 |
| L4_age14.1_AD | neuronal_merged | 65 | 0.16797 | 0.0005 |
| L23_age14_AIS | seed_retained | 45 | 0.01914 | 0.1740 |
| L23_age28_AIS | seed_retained | 31 | 0.08302 | 0.0005 |
| L4_age14.1_AD | seed_retained | 65 | 0.14620 | 0.0005 |

All three primary positive groups keep positive excess in the category-sum and merged-category checks. The P28 L2/3 AIS excess changes from 0.09101 to 0.19472 when count-conflict rows are admitted. The source conflicts therefore have a material effect on its magnitude.

The ten-contact check keeps 25 of 31 P28 L2/3 AIS axons. It removes six rows with two to eight nonseed contacts. Four removed rows carry source subtype 2.1, and two carry 2.2. No 2.1 row remains. Before the count-consistency filter, there are nine 2.1 rows; five of those nine have count conflicts. Thus the combination of count and contact-number filters changes the representation of the source subtype strongly. It cannot be treated as a pure noise-reduction test on the same population. The original subtype labels describe this repository snapshot; we do not assert that every label matches the final paper's classification.

The other two positive groups retain excesses of 0.08569 (L2/3 P14 AIS) and 0.05201 (L4 code 14.1 AD) after the ten-contact filter. Retaining the seed reduces the P14 L2/3 AIS excess to 0.01914. Seed removal does not undo selection by the seed target. Every result remains conditional on that selection.

## Checks and limits

The independent checker rebuilt row scores, group margins, observed effects, and exact means from the two source workbooks. It checked all primary and sensitivity groups. It read every saved primary shuffle, rebuilt raw and Holm p values, checked null quantiles, and compared simulated moments with exact moments. It also checked the exact variance against all allocations in three small tables with 20, 210, and 15 allocations. Homogeneous and strongly segregated synthetic examples behaved as expected. All checks passed. `files/validation.json` records the results. These checks do not validate the original microscopy or synapse annotations.

The randomization null omits geometry, target cell identity, local category availability, axon branch location, tracing coverage, and synaptic strength. Contacts on one postsynaptic cell can be dependent. The null does not preserve those dependencies. A failed exchangeability model cannot by itself show active target recognition, pruning, or an inhibitory mechanism. Axons selected through target contacts can also be sampled in proportion to their access to those targets. One removed seed does not remove this ascertainment.

A minimum-count filter can remove a specific type of axon, as it does in this P28 table. Equal axon weights and synapse weights answer different questions. Neither a small sample nor a large sample is automatically the right target population. The source count conflicts prevent a unique numerical conclusion for all rows without an assumption about which counts to trust.

The study has no paired activity, behavioral state, synaptic conductance, or chloride reversal measurement. It cannot establish the sign or strength of inhibition, integration times, representation reliability, or dynamics in these developing circuits. Layers and ages are from small selected volumes. No result establishes a rule across animals, brain regions, species, or behavior. The useful conclusion is narrower: uniform contact allocation with fixed totals is insufficient for three selected groups under the primary rules, and sample selection changes the P28 AIS result sharply. Circuit models based on these data should retain per-axon target allocation and report their selection rules.

## Reproduce

The package includes new code, the design note, exact source hashes, upstream API receipts, per-row derived scores, conflict locations, all group results, 2,099,979 primary null draws, figures, and validation results. The raw workbooks are not included. No upstream code is executed or redistributed. `files/evidence/provenance.json` records the original shared paths, source URLs, file versions and hashes, and runtime versions. `files/inspected_source_files.json` records two upstream files read for context.

Use Python 3.14.4 and install `files/requirements.txt` in a private environment. The calculation used NumPy 2.5.4 and Matplotlib 3.11.2. Exact dependencies are pinned. Set `DATA` to the shared source directory shown above. From the unpacked publication root, run:

```sh
export OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1
campaign-compute -- python3 files/analyze.py --data "$DATA" --out reproduced
campaign-compute -- python3 files/check_evidence.py --data "$DATA" --evidence reproduced
campaign-compute -- python3 files/plot.py --evidence reproduced --out reproduced_figures
```

To check the packaged evidence, use `--evidence files/evidence`, or omit that option. Omit `--data` for a check of the bundled tables and mathematical controls without raw data. Full source-score reproduction needs the workbooks. Outside this campaign, run the same Python commands directly with one library thread. Output must stay outside the shared store.

If the shared files are absent, run `python3 files/retrieve.py --out local_source` with a new local directory and use that path as `DATA`. The script retrieves pinned GitLab API objects, decodes them, and refuses a hash mismatch. It never writes to an existing directory. Retrieval was tested against both shared files. No reusable dataset was added to the shared store.

All substantial computations used `campaign-compute` with one library thread. No child agents were used. `files/execution_note.txt` records a final shell status of 143 after all analysis outputs and the closing audit were written. The independent final checker and figure step exited 0. Complete saved evidence was validated before signing. No calculation remains active.

## Attribution and job record

Credit Anjali Gour, Kevin M. Boergens, Natalie Heike, Yunfeng Hua, Philip Laserstein, Kun Song, Moritz Helmstaedter, and the source research team. The repository contains no explicit license in the inspected snapshot. Raw workbooks and upstream code remain under their source rights and are not redistributed. The SCI baseline license applies to this report, new code, new figures, and derived analysis to the extent that the publisher can grant those rights. It does not grant rights in the original source files.

Job: `sci-1107-hp-neural-structure-and-computation-5e8ad4638f52`. Topic: `neural-structure-and-computation`. Campaign: `11_07_2026`. Machine: `hp`. Account: `codex-myxtap`. Model: `gpt-6.1-sol`, high reasoning effort, Codex harness in T3 Code. Date: 2026-11-08 UTC. The campaign-machine signing key is not a claim of personal authorship. This publication is stored locally only. No remote archive or index submission is made.
