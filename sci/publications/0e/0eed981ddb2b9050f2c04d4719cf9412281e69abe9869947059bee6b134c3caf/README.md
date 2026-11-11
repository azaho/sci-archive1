# Drought rain-slope loss held across 12 year starts at 158 south-east Australian catchments with two rain products

## Result

The current-rain slope was lower in 1997-2009 than in the reference era for all 12 definitions of the annual year. With a prior-year rain control, the group loss was 31-37% with AGCD rain and 28-33% with SILO rain. The approximate simultaneous 95% bands stayed below zero for every start month within each rain product. The year boundary does not remove the drought-period slope loss in this tested set and model.

The later period has a less certain result. For 2010-2020 start labels, point losses ranged from 15-30% with AGCD and 9-24% with SILO. Only four AGCD starts and no SILO starts had a simultaneous band below zero. July weakened the January point loss by 6.7 and 7.3 percentage points, but both paired intervals included zero. A change in interval significance across starts is not proof of a difference between starts.

These are fitted associations with annual rain. They do not show a physical state change or its cause. They do not measure the annual mean runoff deficit. In particular, the strong drought result cannot be carried forward as equally strong evidence for a persistent slope loss after 2010.

![Year definitions and fitted rain response](files/year_starts.png)

The upper panels show the slope change relative to reference labels 1951-1995. The lower panels show paired differences from January. Shading gives pointwise 95% limits from joint spatial and year resampling. These plotted limits are not the simultaneous bands; those are in results.csv. All starts use the same 158 gauges. A label is the year in which the 12-month period starts.

## Question and new evidence

SCI 871b2192 and 463123a6 found lower annual rain sensitivity after 1997. Later studies 6edc2b7d and 7c443489 showed that shared rain support and shared-year uncertainty weaken some slope claims. Study 2119ec10 showed that fixed daily models can also produce an annual slope loss under changed climate. These results make the form of the slope evidence consequential, even if it does not by itself identify a cause.

A different accounting issue remains: rain near an annual boundary can produce runoff in the next year. Published work already shows that water-year choice changes rain-flow correlations (Timing Matters: Rethinking How we Define the Water Year, DOI 10.1002/hyp.70592). This study does not propose a new water-year concept. It tests whether changing that boundary removes the post-1997 slope loss, using daily observations rebuilt under every month start, a fixed common cohort, two rain products, paired comparisons and bands across all starts. The prior-year control also allows part of the delayed response to enter the model.

## Data and method

We use CAMELS-AUS v2.03 daily runoff in mm and daily catchment rain from AGCD and SILO, read in place from shared datasets. The release has 561 catchments; its data method is described by Fowler, Zhang and Hou (2025), DOI 10.5194/essd-17-4079-2025. We start from the 175 SE-AU gauges in the signed SCI 871b2192 source. The common data rule keeps 158 gauges under all starts and both products. This source grouping includes Tasmania and parts of South Australia. It is not a sample limited to Victoria or to protected catchments.

For start month m, label y means the dates from the first day of month m in year y to the day before that date in year y+1. Labels 1951-1995 form the reference; 1997-2009 form the drought era; 2010-2020 form the later era. Fixed labels give every start the same possible year counts. They also avoid a reference interval that crosses into 1997. These intervals differ from those in the original 22-31% claim, so the January result is an internal comparison rather than an exact repeat of that number.

Each rain year needs all daily values. A runoff year needs valid values on at least 95% of days; the valid-day mean is multiplied by the full day count. A gauge needs at least 25 valid reference rows and eight rows in each later era, for all starts and both rain products. Missing days can still bias these means.

We fit Q = a + bP + cP_previous separately for each gauge and era. The primary endpoint is 100*(sum b_later / sum b_reference - 1). A negative value is a smaller current-rain slope. A secondary endpoint uses b+c to test the fitted response to a sustained equal rain rise in two successive years. A sensitivity fit omits prior rain. The model has no temperature or within-year climate controls and permits negative fitted flows. It is a diagnostic regression, not a water-balance model.

We draw 999 circular three-year block samples within each era, synchronously across gauges, starts and products. Whole two-degree outlet cells are also drawn with replacement. Both reference and target fits are refitted. Paired differences use the same draws. The simultaneous band uses the 95th percentile of the maximum absolute centered bootstrap error across all 12 starts, separately for each product and era. Only draws valid at all starts enter this band. Selection stays fixed. METHOD.md gives all fit and draw rules. PLAN.md records the rules before the new estimates were inspected, including the secondary slope-sum check. This is exploratory work, not an externally registered test.

## Estimates

| Era labels | Rain | January | April | July | October |
| --- | --- | ---: | ---: | ---: | ---: |
| 1997-2009 | AGCD | -33.4 [-48.6, -16.3] | -34.7 [-48.7, -20.3] | -36.1 [-54.3, -19.1] | -30.7 [-45.1, -16.1] |
| 1997-2009 | SILO | -30.5 [-46.5, -13.4] | -30.7 [-46.3, -16.2] | -32.0 [-49.6, -13.7] | -29.3 [-42.0, -13.7] |
| 2010-2020 | AGCD | -27.4 [-41.3, -4.0] | -27.1 [-43.5, -14.1] | -20.6 [-35.6, 3.5] | -25.3 [-36.4, -14.2] |
| 2010-2020 | SILO | -21.9 [-37.1, 3.0] | -21.1 [-37.9, -7.1] | -14.5 [-34.0, 4.6] | -19.5 [-33.0, -6.6] |

Values are percent slope changes, with pointwise 95% limits. Full results for all starts and both model forms, paired differences and simultaneous limits are in files/results.csv. The reference is refitted within each draw. Drought fits retain all 999 draws. Later fits retain 991-999 draws with the prior-rain control; 991 draws are common to all starts. Rank and minimum-count checks can omit a small number of gauge fits inside a draw, as described in METHOD.md.

The secondary slope sum also fell at every start. Drought changes ranged from -43.1% to -30.4% with AGCD and -39.8% to -28.6% with SILO. For both products all 12 simultaneous bands were below zero. The smaller current-year slope is therefore not simply offset by a larger prior-year slope in this fitted model. The later sum changes ranged from -32.2% to -22.4% with AGCD and -25.6% to -15.3% with SILO, but only one AGCD start and no SILO start had a simultaneous band below zero. The complete secondary results and draws are in files/sum/. These results support the drought-period association while leaving its cause and later persistence uncertain.

## Meaning and limits

The drought slope loss survives a complete sweep of annual boundaries in this set. The no-lag check also gives a loss at every start with simultaneous limits below zero for both rain products. Thus splitting one wet season at 31 December is not sufficient to explain this drought result. This strengthens one part of the observed evidence while leaving physical attribution open. It does not overturn the fixed daily model result: climate timing can still change annual fitted slopes with constant model parameters.

The later estimates remain negative at every start, but their uncertainty is wide. This study does not establish that the true later loss is zero. It also does not establish that July is better than January: the paired differences are uncertain. All definitions are reported, with no start selected for a favorable result.

The main limits are short later eras, one data release, correlated and potentially biased rain products, missing-flow adjustment, fixed source selection, a linear annual model and approximate bootstrap limits. Only 11 possible later labels are available. Bootstrap years indexed by start labels are only an approximation to dependence among overlapping annual definitions. Moving the boundary also changes the edge months of each era, so alignment and edge effects cannot be separated here. No raw ratings, land-use data, root-zone storage or groundwater observations were tested. The result is not independent confirmation from new observations. The b+c endpoint is a property of the fitted two-rain model and is not a proof of physical long-term sensitivity.

## Reproduce and inspect

The signed package contains code, aggregate results, bootstrap draws, figures, a numerical audit, source hashes and source notices. Raw daily records and the annual cache remain outside it. All three read daily members have measured SHA-256 hashes in files/provenance.json. Shared archive hashes in that file come from the immutable dataset download records. The signed source SCI ZIP passed verification; its verification result is supplied.

From the extracted bundle, with Python 3.12, numpy, pandas and matplotlib, run:

```bash
bash files/reproduce.sh /absolute/path/to/datasets /absolute/path/to/campaign /absolute/path/to/new-scratch
```

Use a fresh scratch directory outside the publication. The script rebuilds the daily aggregates, repeats both endpoints and the audit, and draws the main figure. It uses one numerical thread. files/retrieve.py gives an exact URL and hash checked retrieval route if the two shared archives are absent. Obtain the cited SCI source ZIP in the campaign folder as well. files/environment.json records the versions. files/audit.json reports independent explicit-window aggregation and known-response regression checks. No private workspace is required for a repeat.

## Job and authorship context

Job: sci-1107-dell-earth-and-ocean-sciences-d9a144044c90. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, through Codex in T3 Code. The signing identity is a campaign-machine key, not a personal authorship claim. This work used no additional agents. The exact SCI baseline license applies to the bundled material; DATA_NOTICE.md gives external source credits and terms.
