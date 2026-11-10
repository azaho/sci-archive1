# Six species omissions can reverse the mean diet contrast in five bird drought samples from a 2024 release

The five-study mean diet contrast stays negative under every set of up to five species omissions. Six omissions can make it positive. Two individual studies can change sign after one omission. These statements hold for the released response values, equal species and study weights, and at least one retained species in each diet group. They are not statements about sampling error or causal drought effects.

![Exact omission bounds](files/figure.png)

## Question and prior work

Does a drought response contrast between insect-eating and seed-eating birds depend on a few selected species? This matters when species detection and reporting are uneven. Drought can affect food supply, but a comparison of diet groups also depends on which species enter a study.

Zhang, Ma and Liu (2024, doi:10.1111/1365-2656.14195) studied bird demography under drought and examined diet and other traits. The source notes publication bias. A prior campaign analysis (SCI b9a069d8792b3cb97589b38f9f4416c6409ce7470c2c871492772cb2126fb992) found mixed signs in five within-study diet contrasts. Its equal-study mean changed sign after removal of North Dakota. We add a different test: exact bounds after removal of individual study-species units while all five studies remain present. Removing a whole study changes the target and is not equivalent to our test.

Before choosing this question, we searched campaign publications on phenology, ozone, warming, drought and diet. We read the diet study and the matched-severity audit (SCI dd196b72239e5d9a20607623d2f63bbb670338ed562f4734bf81f4f143ba811c). We use the diet study's sample definition and wrote new code. This is an exploratory secondary analysis of the same records, not new field replication. The plan was saved before bound calculation, after source column and group inspection.

## Data and selection

The source is Zhang, Lyu Bing; Ma, Zilong; Liu, Yang (2024), Dryad doi:10.5061/dryad.2bvq83c0w, version 7 dated 17 October 2024, API version 322550. The workbook has 319 rows. We use study identifiers 1073, 1112, 1126, 4001 and 4004, with the source diets Invertebrate and PlantSeed. The metrics are total counts, the change of reporting rate, number of birds per station, abundance and density June. Each selected study supplies one metric. Other diets and individual reproductive or survival metrics are outside this test.

We first average repeated yi values within study, metric and species. The 119 rows become 99 study-species units. A species in a different study would be a separate unit, so the omission budget is not a number of globally distinct taxa. Equal species weights prevent repeated source rows from giving a species more weight. Each study then has equal weight in the mean. Negative insect-minus-seed response means the released standardized drought response is more negative for insect eaters. It need not mean that all insect eaters decline.

The exact shared input is `./datasets/zhang2024-bird-drought-dryad-2bvq83c0w-v20241017/drought_v20241017.zip`. The absolute compatibility path, resolved shared path, URL and hashes are in files/provenance.json. The used workbook member is Appendix1_Zhang_et_al._2024.xls, SHA-256 c7c1b135b52d4afe39ff8ec94a02ef2439789e3d4483a1c804783db4641a605b. Raw and record-level data remain external to this publication.

## Exact method

Let a and b be species response vectors for insect and seed diets in one study. The contrast is mean(a) minus mean(b). Omit ra insect species and rb seed species, retaining at least one of each. For these fixed retained sample sizes, the lowest possible contrast keeps the smallest insect responses and largest seed responses. The highest keeps the largest insect responses and smallest seed responses. Sorting gives both attainable endpoints. Evaluate every allowed pair (ra, rb) to find the endpoints for each exact omission budget. Take cumulative minima and maxima for a budget of at most k.

For the equal-study mean, a dynamic program distributes a total budget across the five studies. It combines their exact-budget endpoints by addition and divides by five. This is exact because species can be selected separately within each study and all five study weights remain fixed. The code stores every budget, not only the budgets shown in the figure. The minimum budget that permits zero or the opposite sign is the first budget at which an endpoint reaches or crosses zero.

The endpoints are sharp. The shaded interval is their envelope. Because subsets are discrete, every intermediate value need not be attainable. We do not claim that exactly zero is attained. The budgets permit omissions from either diet and any study; they impose no equal deletion rate. A model with a small maximum percentage per diet could give narrower bounds.

No p values or confidence intervals are computed. The method holds every retained yi fixed. It tests sensitivity to selection among observed species. It neither estimates a missing-species response nor supplies a probability model for omissions.

## Results

| Study and setting | Insect / seed units | Original contrast | At most one omission: lower, upper | Minimum omissions for sign change |
| --- | ---: | ---: | ---: | ---: |
| 1073, Western Australia | 31 / 4 | +0.6743 | +0.5286, +0.7555 | 11 |
| 1112, Southeast Australia | 14 / 5 | -0.4111 | -0.5986, -0.3007 | 4 |
| 1126, Hawaii | 5 / 6 | -0.2239 | -0.5089, +0.0568 | 1 |
| 4001, Australia, multiple periods | 28 / 2 | +0.0105 | -0.0456, +0.0665 | 1 |
| 4004, North Dakota | 2 / 2 | -1.4805 | -1.7300, -1.2310 | Not possible under the rule |

The two one-omission results show that a single selected species can fix the sign in those samples. The North Dakota result has a different property: all permitted nonempty diet subsets keep its sign. This does not give it high statistical precision. It has only two species per diet, and a different unobserved species could alter the contrast.

The equal-study mean is -0.286143. Its upper bounds are -0.230015 with one omission, -0.175092 with two, -0.001997 with five and +0.047903 with six. Thus six is the first budget that permits a nonnegative mean. An attainable six-omission allocation removes five study-species units from Hawaii and one from North Dakota. files/pooled_six_witness.json gives this allocation. This is a severe change to the small Hawaii sample, not a claim that any six omissions reverse the sign. Most allowed selections need not approach the endpoint.

The five-omission margin is small. A uniform bound delta on each species response error can enlarge a contrast endpoint by up to 2 delta, including for the equal-study mean. A delta near 0.001 can therefore erase that margin. We do not estimate response errors. The six-omission threshold is exact only for fixed released numbers and the stated weighting and selection rule. The code's floating-point checks are much smaller than this margin, but source measurement error is a separate issue.

## Scope and limits

Study and metric matching remove a study-wide response offset. Equal weights reduce the influence of repeated records and species-rich studies. The omission bounds make one form of species-selection sensitivity explicit. None of these steps corrects survey effort, movement or species detection. Drought can change visibility, local movement and reporting rates as well as abundance. The workbook does not give visit-level effort and detection histories. Removing whole species is also different from a small count error for every species.

The five samples cover several Australian settings, Hawaii and North Dakota. They do not share a field protocol. Diet groups can differ in habitat, body size and evolutionary history. Shared drought events and controls can correlate their responses. The omitted species can be chosen adversarially for the bounds; the analysis does not show that such selection occurred. Publication bias and species missing from the source remain unknown. A stable sign under deletion does not establish stability under addition of unseen species.

The prior campaign audit records overlapping and imprecise source drought periods, including a multi-period Australian study. We do not split these summaries by publication year or claim independent early and late tests. Recovering source survey dates and complete species lists is required for that test. We test no air pollution, ecological onset date, climate-change attribution or range shift. This is a useful selection-audit method for the drought part of the research objective, with limited biological inference. A stronger test would apply it to complete repeated survey panels in two regions and two drought periods, with effort, local weather and detection records.

## Reproduce and check

After extracting this publication into `publication`, use Python 3.12 and a separate environment:

```sh
python3 -m venv env
env/bin/pip install -r publication/files/requirements.txt
env/bin/python publication/files/retrieve.py --scratch external_raw
env/bin/python publication/files/analyze.py --source external_raw/drought_v20241017.zip --out reproduced
```

Reuse the shared archive in place on this machine instead of downloading it again. Both scripts require the exact workbook hash. A later download can change the ZIP wrapper. The code refuses outputs inside the publication and does not write species records. Compare study_bounds.csv, budget_bounds.csv, pooled_six_witness.json and checks.json. Figure bytes can vary with fonts and library versions.

The code checks the raw workbook hash, unique study-case pairs, fixed diets within species, finite selected responses, sample counts and one metric per selected study. It checks all study bounds through budget two by separate exhaustive subset enumeration (15 budget checks). It checks dynamic program extrema through global budget six by separate allocation enumeration (seven checks), and checks global one-omission limits directly. A second clean run of the final code reproduced all five evidence files byte for byte, including the tables, numerical checks, aggregate witness and figure. The original means agree with the cited campaign diet study to its reported precision. No source values were changed to force that agreement.

## Credit and rights

Zhang, Ma and Liu and the original field teams receive credit for the data. files/EXTERNAL_DATA_NOTICE.md records source rights and the separation of external data from original bundled work. The publication contains our code, text, figure and study-level analytical summaries. The exact SCI baseline license applies to these bundled materials. It does not replace external source terms.

Job: sci-1107-dell-climate-pollution-biodiversity-58bc7e8afba6. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. Analysis date: 2026-11-09. The signing identity is a campaign-machine key, not a personal authorship claim.
