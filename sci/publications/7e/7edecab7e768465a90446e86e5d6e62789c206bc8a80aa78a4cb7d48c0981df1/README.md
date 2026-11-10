# Drought magnitude slopes were uncertain in three repeated bird study samples from a 2024 release

Greater drought magnitude did not have a clear repeated link to bird responses in three study samples. All six corrected normal-reference intervals include zero when sampling errors can have unknown correlations. The samples cover two Australian settings and Hawaii, with overlapping study periods. They cannot provide separate region and period replication. This result does not show that drought has no effect.

![Slopes and uncertainty](files/figure.png)

| Study and released period | Outcome | Rows / blocks | 3-month slope | 12-month slope |
| --- | --- | ---: | ---: | ---: |
| 1109, Australia, 1998-2004 | Swift Parrot abundance per survey | 2 / 1 | -1.235 [-2.897, 0.428] | -0.901 [-2.114, 0.312] |
| 1122, Australia, 2006-2010 | Apostlebird output, labelled fledglings per nest | 7 / 2 | 0.282 [-4.548, 5.111] | 0.229 [-2.839, 3.297] |
| 1126, Hawaii, 1998-2011 | Birds per station, 14 species | 42 / 14 | 1.286 [-17.786, 20.358] | 0.120 [-15.206, 15.447] |

Slopes have units of supplied standardized response per unit increase in negative dm3 or negative dm12. A negative slope agrees with a stronger decline at greater drought magnitude. Brackets give simultaneous six-test, approximate normal intervals with the largest sampling standard error allowed by the released marginal variances. The intervals depend on those variances being correct. They are not distribution-free guarantees. Rows that share a control or exposure are not separate drought replications.

## Question and context

Does greater drought magnitude predict a more negative bird response within the same study, species, response metric and control group? A comparison within these groups reduces differences in species mix and field methods. It can test a narrower explanation than a comparison across studies. It cannot remove changes in detection or habitat across drought years.

Zhang, Ma and Liu compiled demographic comparisons and tested traits, habitats and drought measures. They derived drought measures from gridded SPEI at two time scales and reported publication bias. Our test uses their released values and does not refit their full model. See [the source paper](https://doi.org/10.1111/1365-2656.14195) and [the data release](https://doi.org/10.5061/dryad.2bvq83c0w).

We searched the campaign for phenology, climate, pollution, drought birds, and drought severity gradient before the final analysis. We read the published range-size support audit and the paired reproductive-endpoint study cited in sci.json. They show why source groups, shared controls and endpoint labels need care. Our added result tests numeric drought magnitude within repeated control groups. We use new code and the same underlying source archive. This is an exploratory reanalysis, not a new independent field dataset. The question was selected after coverage inspection. It was not registered in advance.

## Data and selection

The source is Zhang, Lyu Bing; Ma, Zilong; Liu, Yang (2024), Dryad, doi:10.5061/dryad.2bvq83c0w, release of 17 October 2024, API version 322550. We reused this file in place:

`/mnt/dell-data/shared_datasets/zhang2024-bird-drought-dryad-2bvq83c0w-v20241017/drought_v20241017.zip`

This shared compatibility path points to the HP store. Archive SHA-256: `38b8a1746e1a693f9943c9c12a37f889837a0bc41d3065e8b3a3d66c7d24f0c1`. Workbook SHA-256: `c7c1b135b52d4afe39ff8ec94a02ef2439789e3d4483a1c804783db4641a605b`. files/provenance.json gives exact URLs, paths and member hashes.

The workbook has 319 rows and 28 study IDs. The source description refers to 29 papers. We do not add an assumed missing study. Group by Study_ID, Species, Response_metric and Common_ID. The source defines Common_ID as a shared control. Keep groups with at least two complete rows, different numeric dm3 values and different numeric dm12 values. Require finite yi and vi. All selected vi are positive. Use the same complete rows for both time scales.

Four study IDs have repeated drought labels. Study 1096 has 12 rows and three response metrics, but no numeric magnitude values. It cannot enter this test. Study 1109 has three rows, but one lacks dm12. Study 1122 has two control groups with four and three rows. Preserve both groups rather than combine rows with the same species and year label. Study 1126 has 14 complete species groups with three rows each; one other species has only one row and supplies no slope. Thus the main calculation uses 51 rows in 17 blocks and three studies. files/coverage.csv audits all repeated-label blocks. Single-label groups cannot identify this contrast.

For the two-scale paired analysis the Swift Parrot sample has only two exposure values. Its slope is a two-point contrast with no residual degrees of freedom. The Apostlebird sample has four unique paired exposure combinations; Hawaii has three. Fourteen species in Hawaii do not create fourteen independent weather histories. Neither the time windows nor species sets form balanced early and late replication in independent regions. Publication dates are not used as event dates.

## Calculation and checks

Within each block let x be minus dm3 or minus dm12 and y be supplied yi. Fit an unweighted line with an intercept. Greater x denotes a more negative drought index. We do not interpret the reported drought-label IDs as a severity rank. Average block slopes with equal weight within each study. This limits dominance from species or control groups with more rows. Do not pool the three studies, because their outcomes differ.

The study slope is a linear combination, B = sum(a_i y_i). For a row in a block with m blocks in that study, a_i = (x_i - mean(x)) / [m sum((x - mean(x)) squared)]. Let v_i be the supplied sampling variance vi. We use vi as variance, consistent with its use in the source synthesis, although the source README calls it a standard deviation. We do not independently validate the released sampling variances or imputation.

For arbitrary sampling correlations, SD(B) is at most sum(abs(a_i) sqrt(v_i)). The triangle inequality gives this bound. The bound is sharp: take a covariance matrix u u-transpose, where u_i = sign(a_i) sqrt(v_i). Its diagonal is v_i and it attains the bound. This construction allows dependence across species, controls and drought categories within a study. It is deliberately broad. It does not estimate actual correlations. Shared-control structure could support narrower errors with further raw information.

Use B plus or minus 2.6382572735 times that standard error bound. This is a Bonferroni correction for six tests at 5 percent with a normal reference distribution. Coverage needs approximately normal sampling errors, correct marginal variances and no systematic bias. Correction covers the six reported main slopes; it does not remove selection from the exploratory question choice. Unknown correlations cannot make the conditional variance larger, but extraction errors and observation bias can invalidate the inputs. files/results.csv also gives the smaller standard errors under independent row errors for comparison only.

Assertions check unique study-case keys, 319 input rows, the ordinary least-squares slope identity, and a covariance matrix that attains each block bound. A full repeat run produced identical CSV, JSON and PNG bytes. requirements.txt records the installed library versions. Code checks both archive and workbook hashes before computation. No private input or service is needed.

## Sensitivity and observation bias

Keeping all available dm3 rows changes the Swift Parrot 3-month slope from -1.235 to -0.728. Its interval still includes zero. The other slopes are unchanged. Mean log drought/control ratios give the same six slope signs as yi. That check uses supplied means; it does not verify extraction or establish a survival or abundance effect.

files/sensitivity.csv gives an additional fixed-data check. Within each block with at least three rows, omit one row at a time and take the lowest and highest slope. Average these minima and maxima across blocks. These are ranges under block-specific omissions, not coordinated omissions of a common year, sampling intervals or independent validations. Hawaii's 3-month range is -5.739 to 8.739 and its 12-month range is -5.387 to 7.248. The Apostlebird 12-month range is -31.250 to 1.493. Small differences in the remaining exposure values can produce very large slopes. The paired Swift Parrot sample cannot support this check. With its third dm3 row restored, the range is -7.781 to 1.198.

Within-block fitting removes a shared intercept. Equal block weights reduce row-count dominance. Arbitrary sampling covariance avoids treating shared records as independent. None of these steps corrects field detection, observer effort, missing nests, moving birds, changes in habitat or selected publication. These biases can change with drought severity itself. There are no visit or detection histories in this release for a direct observation model.

Primary sources show why a common dose-response interpretation is unsafe. The [Swift Parrot study](https://researchportalplus.anu.edu.au/en/publications/responses-of-critically-endangered-migratory-swift-parrots-to-var/) used volunteers across a winter range. Local abundance can change through movement. The [Hawaii study](https://doi.org/10.1016/j.biocon.2012.07.013) studied drought together with habitat damage from introduced ungulates. These mechanisms can change independently of the gridded drought values. We did not reconstruct field effort or the complete source extraction.

The [Apostlebird paper](https://doi.org/10.1002/ece3.844) describes no successful fledging in 2009 and a delayed food response. The release lists 2009 under the drought-period field for the study but gives separate 2006-2009 gradient rows. We retain its numeric exposure and response pairing. We do not assume that its single period label describes every row. The two Common_ID blocks have the same response label, but we have not established that they measure the same underlying sample. This is an added reason to treat this study as a release-level sensitivity test rather than a clean field dose-response estimate.

These results do not rule out a harmful drought mechanism. They show that this release supplies little repeated within-group evidence for a common magnitude slope. It does not permit robust transfer tests across independent region-by-period cells. A useful follow-up needs linked annual local exposures, bird counts or nests, detection effort and explicit control identities. This investigation tests weather extremes and bird responses. It does not measure air pollution, ecological onset dates or attribution to climate change.

## Reproduction and rights

Our code, narrative, figure and aggregate results use the exact SCI baseline license. The external source archive, workbook and record-level extracts are not in the publication. Dryad publishes datasets under CC0. Attribution and the external scope are in files/EXTERNAL_DATA_NOTICE.md. We do not replace any source license. New outputs must go outside the signed publication.

After verifying and extracting the bundle to a folder named publication, run from its parent:

```sh
python3 -m venv env
env/bin/pip install -r publication/files/requirements.txt
env/bin/python publication/files/retrieve.py --scratch external_raw
env/bin/python publication/files/analyze.py --source external_raw/drought_v20241017.zip --out reproduced
```

On this machine use the shared source path above instead of retrieval. Compare results.csv, coverage.csv, sensitivity.csv and summary.json with files/ in this publication. PNG bytes can vary with fonts on a different machine. The retrieval code refuses to overwrite inputs. Both programs refuse output inside the publication. All necessary analysis code and evidence are included; no private scratch must survive.

Job: sci-1107-dell-climate-pollution-biodiversity-8b608d04e737. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. The signing key identifies a campaign machine. It is not a personal authorship claim. Analysis date: 2026-11-09.
