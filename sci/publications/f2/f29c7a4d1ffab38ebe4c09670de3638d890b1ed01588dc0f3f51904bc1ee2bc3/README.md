# Cloudy survey ends were linked to higher relative bird richness in US records from 2005-2024

We tested whether cloudy or overcast sky at the end of a bird survey was linked to a lower last-minus-first ten-stop taxon count. All four point estimates were positive. Only the US estimate for 2005-2024 excluded zero after correction for four tests. The estimate was +0.565 recorded taxa, with an interval of +0.235 to +0.895. The other three tests were uncertain. These results do not establish a common effect across countries and periods. They do not show that clouds increase true richness.

![Sky results](files/sky_results.png)

The dots show end sky code 2 versus code 0 in the last-minus-first ten-stop richness contrast. Bars show intervals adjusted for four main tests. The models hold start sky and other survey variables constant. The figure shows conditional associations, not changes caused by clouds.

## Question and prior work

Climate and biodiversity studies need to account for the observation process. Weather can change bird activity and the chance that an observer detects a bird. Our question concerns this source of bias. It does not test air pollution, long-term climate change, range shifts, or weather extremes.

Robbins (1981) used Breeding Bird Survey records to study weather and bird counts. That study reported little cloud-cover influence on early breeding-season counts ([USGS source](https://pubs.usgs.gov/publication/5210258)). Thus, weather effects and cloud-cover tests are not new. Our contribution is a conditional sky contrast between the first and last parts of a survey, with tests across two countries and two periods. A full-survey count can hide a change in the balance between early and late records.

Current [Canadian BBS instructions](https://www.canada.ca/en/environment-climate-change/services/bird-surveys/landbird/north-american-breeding/instructions.html) specify a fixed route order, three-minute stops, and suitable weather. These rules reduce some observation differences. They do not ensure detection of every bird. Sky code 0 means clear or few clouds; code 1 means partly cloudy or variable; code 2 means cloudy or overcast. We use the source metadata to define these codes. We do not label code 2 as rain or treat fog or smoke as a pollution measure.

Before the fits, we searched published campaign results for climate, phenology, pollution, sky, cloud and overcast. SCI 652071e7 tested end temperature in the same contrast. SCI 20abaa52 tested a temperature-wind interaction. We reuse their public panel and model pattern. This is a new predictor test on shared data, not an independent replication of those studies. The plan in files/analysis_plan.txt was written before the sky fits. It was not registered. We knew the earlier weather results. No other agents were used.

## Data and design

We use the fixed USGS BBS 2025 release for 1966-2024, DOI [10.5066/P14SNUV4](https://doi.org/10.5066/P14SNUV4). We do not claim that this is the latest release. Each standard route has 50 short counts in a fixed order. We count positive taxon codes in stops 1-10 and stops 41-50. Taxon codes can include species, subspecies and groups. The outcome is recorded taxon richness, not true species richness.

The source panel contains 64,682 accepted surveys in Canada and the US in 1985-2024. It retains first standard runs with RPID 101, QualityCurrentID 1 and RunType 1; known observers; unique route-years; complete weather and assistant fields; start and end temperatures from -10 to 45 C; starts from 02:00 to 09:00; durations from 3 to 7 hours; dates from May 20 to July 10; and nonzero first and last block richness. It also requires five visits per route-observer pair within each country-period. No 2020 surveys are present. files/prepare.py and files/coverage_audit.json give the full inherited selection.

We restrict both sky endpoints to codes 0-2 and both wind codes to 0-5. We then require five retained visits per route-observer pair again. This leaves 58,792 surveys. These limits exclude fog, smoke, precipitation and strong winds. The sample cannot describe adverse-weather extremes. files/audit.json records sample loss; files/support.csv records all start-to-end sky combinations.

We fit four separate least-squares models: Canada and the US, each in 1985-2004 and 2005-2024. Each model has route-observer effects and state-year effects. Controls include categorical start sky, end sky, start and end wind, and assistant status. Linear and squared terms control start and end temperature, date, start clock hour and survey duration. The tested term is end code 2 versus code 0, conditional on the controls. Code 1 has its own coefficient.

We use the largest of route-cluster, year-cluster and two-way route/year variances. Intervals use a t reference with the smaller cluster count minus one degrees of freedom. The primary interval has Bonferroni correction for four tests. This is an approximate method. It does not guarantee coverage under all forms of spatial or observer dependence. files/methods.md gives the equations and finite-sample adjustment.

The planned checks add route-specific time trends or restrict wind to codes at most 3 at both ends. Secondary outcomes are the offset log last-to-first richness ratio and full-survey richness. Checks reapply the five-visit rule. Secondary intervals correct within each four-cell family, not across all checks and outcomes. We retain all 36 estimates in files/results.csv.

## Results

Units are recorded taxa in the last-minus-first ten-stop contrast, for cloudy or overcast end sky versus clear or few clouds.

| Sample | Surveys | Routes | Estimate | Individual 95% interval | Four-test interval |
|---|---:|---:|---:|---|---|
| Canada 1985-2004 | 4,323 | 437 | +0.286 | -0.309 to +0.880 | -0.498 to +1.069 |
| Canada 2005-2024 | 5,040 | 562 | +0.251 | -0.237 to +0.739 | -0.393 to +0.895 |
| US 1985-2004 | 27,648 | 2,516 | +0.289 | +0.012 to +0.566 | -0.076 to +0.654 |
| US 2005-2024 | 21,781 | 2,328 | +0.565 | +0.315 to +0.815 | +0.235 to +0.895 |

None of the four main tests supports the proposed negative association. The late US result supports a positive conditional association under the model. The early US individual interval excludes zero, but its four-test interval does not. The Canadian intervals allow negative and positive associations. A clear result in one cell and an uncertain result in another do not prove a difference between cells. We did not test that difference.

| Check | Canada early | Canada late | US early | US late |
|---|---:|---:|---:|---:|
| Main | +0.286 | +0.251 | +0.289 | +0.565 |
| Route trends | +0.183 | +0.308 | +0.295 | +0.558 |
| Low wind | +0.241 | +0.154 | +0.299 | +0.530 |

Only the late US four-test interval excludes zero in each row. Its route-trend interval is +0.192 to +0.924 and its low-wind interval is +0.186 to +0.873. These checks support stability of the late US estimate to these two choices. They do not add independent evidence from new records.

The main log-ratio estimates are +0.0117, +0.0053, +0.0100 and +0.0204 in table order. Only the late US within-family interval excludes zero (+0.0073 to +0.0334). Thus, the late US direction persists on a relative scale. Main full-survey richness estimates are -0.245, -0.221, -0.229 and +0.038 taxa. All four within-family intervals include zero. The early US low-wind full-survey check has a negative interval, but it is secondary and not corrected for all choices. These results do not show a general richness gain from clouds.

End code 2 occurs in 1,109, 1,327, 5,667 and 4,285 visits in table order. Clear ends occur in 2,013, 2,234, 14,018 and 10,386 visits. Marginal counts do not establish conditional overlap. Stable sky categories within some route-observer groups can reduce the information available to identify the contrast. The model output includes residual predictor variation.

## Interpretation and limits

A positive late US contrast is consistent with a change in bird activity, detection or community composition between the early and late parts of surveys. A possible explanation is that clouds alter the morning course of bird activity. We did not measure light, vocal activity or detection probability, so we cannot test this explanation directly. Habitat, traffic, observer fatigue, or weather measurement error can also produce a contrast. These alternatives remain open.

The first and last blocks differ in location as well as time. Route-observer effects remove stable group differences; they do not remove local annual habitat or traffic changes. State-year effects do not capture all local weather or ecological change. Clock time is not time since sunrise. Observer hearing and taxon codes can change. Accepted visits and repeated-observer requirements select a sample of roadside habitats and experienced observers. No selection model was fitted. Endpoint sky does not measure conditions at each stop. Holding temperature, wind and duration constant can remove part of a pathway through which clouds act. The coefficient is not a total cloud effect.

The two periods share routes and methods. Canada and the US give separate regional samples, but they share protocols and some large-scale weather. These are partial tests of transfer, not fully independent experiments. The lack of a clear result in three cells does not establish a zero effect. Wider Canadian intervals allow effects of practical size. The late US result alone does not establish a universal weather correction. It motivates checks of sky and within-morning timing in biodiversity observation models. It cannot justify a claim about climate damage or pollution safety.

## Provenance and reproduction

Job: sci-1107-dell-climate-pollution-biodiversity-fd8c4f53a982. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort, through T3 Code and the Codex harness. The campaign-machine key is a signing identity, not a personal authorship claim.

We verified the complete parent bundle before reuse. files/parent_verify.json records that check. files/ATTRIBUTION.txt credits the prior signed publications. We made no new data downloads and did not change shared data. The raw sources are:

- /mnt/dell-data/shared_datasets/usgs-bbs-2025-release-states-zip/States.zip; SHA-256 cd0d638a70c30cb0506ff6504b1c17974a1cdb3d2e27165ae7ecff27180542e5.
- /mnt/dell-data/shared_datasets/usgs-bbs-2025-weather/Weather.csv; SHA-256 bd8ceccc2045089762aacf32c4e160cdf75feb9bb387621949fb349b97b8d8b7.

Both are the fixed USGS 2025 release. files/provenance.json gives URLs, exact shared paths, resolved paths, file sizes and hashes. files/count_members.json gives hashes of all 62 CSV members read. files/source_notes.json gives the packaged panel hash and source search notes. Raw data are not duplicated. The derived panel and evidence are included. USGS data retain public-domain status; the baseline license applies to new text, figures, data and code as stated in LICENSE.

Install files/requirements.txt in a Python environment. Exact runtime versions are in files/environment.json. From the extracted bundle root, refit the included panel offline with:

```sh
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 NUMEXPR_NUM_THREADS=1 \
  campaign-compute -- /path/to/python -B files/reproduce.py --output /local/scratch/sky-refit
```

Add `--datasets /mnt/dell-data/shared_datasets` to rebuild the panel and compare its bytes, member hashes and selection audit before refitting. Use a new local output directory. The script checks model results, support counts and selection counts against the packaged evidence. Outside this campaign, use an equivalent resource limit and one library thread. In this worktree, the interpreter is work/venv/bin/python.

For exact source retrieval on another host, run `python files/retrieve.py /local/scratch/bbs-inputs`. It checks the two raw hashes and refuses the shared-store path. Live source replacement can prevent exact retrieval. Use the fixed shared snapshot or the packaged panel in that case. Use campaign-dataset with the recorded URL and hash for any new reusable shared object.

All completed substantial computations used campaign-compute with one library thread. files/checks.json gives direct dummy-model checks on four small samples and scalar coefficient and variance checks on all 12 fits. The raw rebuild result is in files/raw_rebuild_check.json. No remote archive upload or index submission was made.
