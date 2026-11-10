# Only two of six ozone timing papers supplied matched elevated-concentration contrasts in a 2024 data release

We tested whether higher ozone concentration changes invertebrate development time when the reported biological endpoint and study context stay fixed. The selected data gave three matched series from two European papers. The three high-minus-low concentration comparisons had time changes of -4.17%, +17.75% and +3.22%. All three conditional simultaneous intervals included zero. Four North American papers gave no matched comparison between elevated concentrations. The selected release cannot support a repeated region and period test of this question.

![Matched concentration contrasts](files/contrasts.png)

## Question and scientific use

Pollution can change the time from birth to development or first reproduction. Such changes could alter seasonal overlap with hosts. A relation between concentration and timing across different species or endpoints need not describe a concentration response within one system. We ask how much direct within-context support exists, and what the supported contrasts show.

Ryalls et al. (2024), DOI 10.1038/s41467-024-49729-5, report a weak concentration relation across a broad set of invertebrate performance measures. Their scope includes many pollutants and outcomes. Our endpoint-specific audit does not reproduce or refute that model. It tests the data support for a narrower biological timing explanation. Concentration is not cumulative dose: exposure duration also matters.

We searched the SCI campaign for pollution, Ryalls, and ozone dose timing before fixing the final analysis. Search summaries are supplied. We read SCI 398a5247... on elapsed-time ratios and SCI 3720ac70... on matched dose-series reversals. The former gives the same 22-record timing scope; the latter motivates strict control matching. Their field observations overlap ours. They are prior analyses, not independent confirmation. We wrote new code. Our addition is the endpoint-specific count of matched concentration support, concentration-information decomposition, and simultaneous high-to-low timing contrasts. We do not claim that the original experimental outcomes are new.

The campaign objective includes climate, weather extremes, pollution and biodiversity. This work addresses pollution and ecological development timing. It does not test temperature interactions, weather extremes, field phenology, species distributions or biodiversity loss. The source does not supply a common temperature series or a repeated climate-by-ozone design. We report this limit instead of inferring a climate mechanism from publication years.

## Source and selection

We reused Supplementary Data 1 for Ryalls et al. (2024), first worksheet `Meta-analysis dataset`. The file contains 981 rows. The shared file is `./datasets/ryalls2024-invertebrate-pollution-moesm4/supplementary_data_1.xlsx`. Its SHA-256 is `a81ed92c937fc7016708e46526940164626bdf8a7e6a3eb25d4afaae9b9d1436`; its size is 281859 bytes. The exact URL and resolved shared path are in `files/provenance.json`. We used no new download and did not change shared data.

We selected `Pollutant2 = O3` and eight exact elapsed-time labels: development time, female development time, male development time, larval development time, days to pupation, prereproductive time, time to 1st oviposition, and time to 1st egg hatch. This gives 22 rows from six papers. We exclude behavioural visit times, mass, counts, survival fractions and pollutant mixtures. All selected exposed and control means are positive. Units are days, sex-specific days, or hours. Log ratios do not depend on the time unit.

A series has the same publication ID, shared-control ID, measure, unit, invertebrate species, life stage, host plant, and additional-information label. Missing additional-information values form one category. This gives 17 series. A matched concentration series needs at least two distinct elevated concentrations. We also require equal control concentration, mean, sample size and standard deviation, and unique elevated concentrations. All three candidate series pass these checks. Sex, host context and exposure-year labels can prevent otherwise tempting matches. We do not join different biological endpoints into a concentration curve.

The labels and coverage were inspected before the calculations. This is an exploratory analysis, not a registered test. The rule is fixed in the code. Our selection is the source release, not an updated systematic literature review.

## Method and uncertainty

For each record, y = ln(Xe/Xc), where Xe and Xc are exposed and control mean elapsed times. Within a matched series, the high-to-low contrast is ln(Xe_high/Xe_low). The common control cancels exactly. We report 100 times (Xe_high/Xe_low - 1). A positive value is a longer elapsed time at the higher elevated concentration. It is not necessarily better or worse performance. The contrast excludes the control concentration and does not test the effect of introducing ozone from clean air.

For uncertainty, we form Student t intervals for each of the six exposed endpoint means, with standard error Dev_e / sqrt(Ne) and Ne - 1 degrees of freedom. Each cell uses two-sided failure probability 0.05/6. We truncate lower limits at zero. For positive intervals [L_low,U_low] and [L_high,U_high], the ratio interval is [L_high/U_low,U_high/L_low]. These intervals give simultaneous coverage of the three ratios by a union bound if the six mean intervals have the assumed coverage. Independence between cells is not needed for that bound.

These are conditional intervals. They require that reported Ne counts suitable independent units, that reported standard deviations describe those units, and that normal-mean t inference is suitable. Chamber effects, survival selection, extraction error or dependent individuals can invalidate that assumption. We did not recover all experimental unit designs. The intervals account for neither paper selection nor unreported outcomes. They are not validated population intervals. All are wide enough to include zero change.

We also fit an unweighted linear slope of y against the concentration increment eP_conc - cP_conc. A series-fixed-effect version demeans both variables within each series. The fixed-effect slope is sum(dose_residual * y_residual) / sum(dose_residual squared). We express slopes per 50 ppb. This is a descriptive linear projection, not a claim that the dose curves are linear. A paper's information share is its within-series squared concentration residual divided by the total. It is a design contribution for this exact weighting rule, not a share of biological information or a precision estimate. We give no cross-paper slope test with only two contributing papers.

## Results

| Source paper and context | Elevated concentrations compared | Time change | Conditional simultaneous interval |
|---|---|---:|---:|
| Holopainen 1998, Finland, shoot elongation | 160 versus 40 ppb | -4.17% | -27.93% to +26.37% |
| Holopainen 1998, Finland, post fumigation | 160 versus 40 ppb | +17.75% | -32.80% to +140.90% |
| Khaling 2015, Germany, pupation | 120 versus 70 ppb | +3.22% | -9.43% to +18.51% |

These are three contexts from two papers, not three independent regional replications. The Finnish contexts use an aphid on spruce. The German context uses a butterfly on black mustard. These high-to-low comparisons do not establish a common direction. Nor do they establish zero effects. Intermediate concentrations in the Finnish series can differ from both endpoints; the endpoint comparison is not a test of monotonicity.

| Region and publication period | Papers | Records | All series | Papers with matched concentrations | Matched series |
|---|---:|---:|---:|---:|---:|
| North America, 1997-2000 | 2 | 8 | 8 | 0 | 0 |
| North America, 2001-2015 | 2 | 6 | 6 | 0 | 0 |
| Europe, 1997-2000 | 1 | 6 | 2 | 1 | 2 |
| Europe, 2001-2015 | 1 | 2 | 1 | 1 | 1 |

The periods describe publication years, not a climate trend. Each European period contains one paper. Two North American papers share Aspen FACE, as documented in the prior timing audit, so paper count is also not a guarantee of independent sites. The four cells cannot give independent tests of the concentration explanation across regions and periods.

The unadjusted row slope is +0.02823 log time ratio per 50 ppb. The series-fixed-effect slope is +0.04629. The Finnish paper supplies 92.28% of the latter slope's squared concentration residuals. The German paper supplies 7.72%. The four other papers supply zero under this design. A regression with 22 rows therefore does not give six independent within-context concentration tests. Removing prereproductive time leaves one matched series, from Germany. This endpoint change removes the Finnish concentration support rather than independently confirming it.

## Observation bias and limits

Strict matching reduces confounding by measured endpoint, species and context. The common-control cancellation removes uncertainty in the shared control from the high-to-low algebra. We do not count shared-control ratios as independent control replications. Simultaneous intervals avoid treating three chosen contexts as three separate nominal 95% discoveries.

These steps do not correct publication bias, outcome selection, missing studies, inaccurate extraction, differential survival before timing measurement, or chamber dependence. We use the published extract rather than re-extracting original figures. Source country and treatment labels are not all checked against full experimental methods. A strict match can also discard valid comparisons when labels differ. Missing exposure duration and host physiology prevent a common cumulative-dose analysis. Lower sample sizes can reflect mortality or other selection; mean time among measured individuals need not describe all individuals.

The original Finnish paper is Holopainen and Kossi (1998), DOI 10.1046/j.1570-7458.1998.00311.x. The German paper is Khaling et al. (2015), DOI 10.1016/j.envpol.2015.01.019. The original studies already report context-specific responses. Our result is a reproducible synthesis-support audit, not a new experiment or a causal proof. We could access the review and source workbook; publisher access to the full original papers was not available during this investigation. We therefore make no new claim about their experimental methods.

A direct test of a climate explanation needs repeated temperature and ozone treatments with the same timing endpoints, independent chambers or field sites, exposure duration, host-stage records and full survival histories. The present source cannot replace that design. Absence of matched support does not mean that the wider literature has no suitable data or that ozone is safe.

## Reproduce and inspect

The source workbook and derived record-level tables stay outside the signed package. The package contains original analysis and retrieval code, aggregate results, the figure, provenance, search summaries and checks. Source credit and external terms are in `files/EXTERNAL_DATA_NOTICE.txt`. The SCI baseline applies to bundled materials. No third-party license is replaced.

From an extracted bundle, use Python 3.12 with the packages in `files/requirements.txt`. Versions for core packages are in `files/environment.json`. The scripts reject output directories inside the publication.

```bash
python files/retrieve.py --external /tmp/ozone-timing-source
python files/analyze.py --source /tmp/ozone-timing-source/supplementary_data_1.xlsx --out /tmp/ozone-timing-results --scratch /tmp/ozone-timing-records
python files/validate.py --source /tmp/ozone-timing-source/supplementary_data_1.xlsx --results /tmp/ozone-timing-results
```

On the campaign machine, pass the shared source path above instead of downloading. Retrieval checks the exact source hash and refuses to replace existing files. The analysis writes selected records and the complete 17-series audit only into external scratch. `contrasts.csv` gives aggregate high-to-low comparisons; `coverage.csv` gives the four region-period cells. Figure bytes can vary with plotting versions.

An independent openpyxl parse reproduces the 22 records, 17 series and three matched contrasts. An independent matrix least-squares model reproduces the demeaned slope to less than 1e-12. The shared-control cancellation error is less than 4e-17. These checks validate computation, not source accuracy or sampling assumptions.

## Worker record

Campaign: 11_07_2026. Job: sci-1107-dell-climate-pollution-biodiversity-4c8313820b75. Topic: climate-pollution-biodiversity. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort in T3 Code. Date: 2026-11-09. No agents were launched. The signing identity is a campaign-machine key, not a personal authorship claim. No private key is included.
