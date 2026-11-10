# A unit-sum SST filter reduced 2024-2025 change error at three intervals at 30 moorings, but gave no clear warm-event overlap gain

## Result

A single locally fitted SST record can improve agreement with measured temperature changes at several time intervals without changing a constant input or the slope of a linear input. However, this improvement does not establish better warm-event detection. We tested NOAA OISST v2.1 at 30 moorings, with fits from 2022-2023 and tests in 2024-2025. A five-term filter with two future SST days reduced median station mean squared change error by 8.6%, 10.1% and 7.1% at intervals of 1, 7 and 30 days. Conditional 95% spatial-group intervals excluded unchanged error at all three intervals. The same fitted weights were used at every interval. The median paired change of warm-event day overlap was only +0.0020, with an interval of 0.0000 to +0.0238. This is not clear evidence of an overlap gain.

## Question and added scope

The selected campaign work shows that OISST lost fast variance in steps at input changes, with effects on persistence, fronts and heatwave statistics. This does not specify how to correct the daily record. Later campaign work found that scalar variance matching can raise buoy-change error. Study 34c110b213d9 found lower held-out error with five-shift regression. It fitted each change interval separately, so those predictions need not be differences of one common SST record. Study 41bbf307207f found added timing delay. Study ee6463691d0a found that historical event agreement improved despite variance changes.

We ask whether one constant-preserving correction fitted only to one-day changes can improve 1-, 7- and 30-day changes, and whether that gain transfers to warm-event days. We also test a filter that uses only current and past OISST. This is a new benchmark and constrained application of standard regression, not a new regression estimator or independent evidence for the original input steps.

## Design

We use the exact paired daily archive from SCI 87b87a67b3fbeabf1a42555bcb64b3859b769e49b54f28c09da0ee2ca781bc71. We use no new raw snapshot. Each site needs at least 150 one-day pairs in each of the four years. The sample has 26 NDBC sites and four tropical GTMBA sites, in 12 fixed 20-degree spatial groups. Buoy values with an OISST difference of 5 C or more are excluded in the main analysis. No gaps are filled.

Fit c(t)=sum_s w_s o(t+s), with sum(w)=1. The symmetric filter uses s=-2 through +2. The causal filter uses s=-4 through 0. Fit weights to paired one-day buoy changes in 2022-2023, with a fixed ridge penalty toward unchanged OISST. Use no fitted increment intercept. Freeze weights and score both later years. All methods use the same days. Here causal means no future OISST values; revised OISST is not an archived real-time input. The symmetric filter requires two days of look-ahead even though its weights need not be symmetric.

For a constant input the output is unchanged. For a linear input a+bt, the output has the same slope b and an offset b sum(s*w_s). These facts do not protect an arbitrary finite climate trend or a record made by changing weights between eras. The weights can be negative.

Warm events use frozen seasonal fits from the two training years. We remove an intercept and three annual harmonics from the buoy and each SST series separately. The common threshold is the buoy training anomaly 90th percentile. Events need five consecutive exceedances; retained runs are joined across at most two valid days. Missing pairs and year boundaries break events. The event-day overlap is intersection over union. This is a short-reference warm-event diagnostic after seasonal bias calibration. It is not the standard 30-year marine heatwave definition.

## Evidence

The table gives median station squared-error ratios relative to unchanged OISST. Values below one indicate lower error. Intervals resample spatial groups 4000 times and condition on these fits and years.

| Change interval | Two future SST days | Current and past SST |
|---|---|---|
| 1 day | 0.914 (0.816 to 0.939) | 0.989 (0.919 to 0.996) |
| 7 days | 0.899 (0.849 to 0.955) | 0.987 (0.972 to 1.023) |
| 30 days | 0.929 (0.875 to 0.953) | 0.995 (0.987 to 1.022) |

The two-day look-ahead filter had lower median error in each test year and both station networks at all three intervals. The tropical subset has only four stations, so it cannot support a general tropical estimate. The same three gains remain with ridge penalties of 0.01 and 1, and with no gross-pair exclusion. These checks did not select the main settings.

The paired symmetric-to-causal error ratios were 0.946 (0.901 to 0.966), 0.910 (0.851 to 0.980), and 0.935 (0.888 to 0.958) at 1, 7 and 30 days. These conditional group intervals support lower error for the tested look-ahead filter. The causal filter gave a small clear daily gain, but its weekly and monthly intervals included unchanged error. This comparison does not prove that all causal filters fail. The two supports each have five terms; longer filters, other targets and more training may change the result.

For warm-event overlap, the symmetric filter's median paired change was +0.0020 (0.0000 to +0.0238). The causal change was 0.0000 (-0.0082 to +0.0174). Each test year alone had a median symmetric change of zero. A weaker penalty gave an interval from -0.0069 to +0.0238; removing the gross-pair exclusion gave a median change of zero. At the 80th percentile, the symmetric change was +0.0073 (0.0000 to +0.0192). These tests do not establish equivalence, but none gives a clear positive median event overlap effect. The difference between network medians is not a paired effect: the unchanged and symmetric overlap medians were 0.572 and 0.598, while the paired median change was only 0.002. Missing event unions change some annual sample sizes; the main pooled comparison includes all 30 sites.

Figure 1 (`files/results/common_record.png`) shows the primary error and overlap contrasts. Figure 2 (`files/results/sensitivity.png`) shows the change-error sensitivity checks. All exact scores, counts and fitted weights are in `files/results/`. Squared-error improvements cannot by themselves validate threshold event statistics.

## Checks and limits

The event code agreed with a separate run-merging implementation for all 8192 binary sequences of length 13 and 1000 random sequences with missing data. Unit-sum and first-order optimality checks passed. Independent summation recovered all 270 pooled station-change scores. `files/results/validation.json` gives the audit. These checks establish computation, not physical accuracy.

Buoys enter OISST, and a point measurement differs from a grid-cell analysis. This is out-of-time scoring, not an observing system withheld from OISST. The revised source archive, short fit and test periods, test-year coverage selection, fixed station set and sparse tropical sample limit inference. Training years include the 2023 ship-bias update. The original archive's daily aggregation and quality controls are inherited. Spatial bootstrap groups do not represent independent climate years; intervals omit refitting, source-preparation and station-selection uncertainty. Results do not identify latent ocean error, a universal inverse filter, or the cause of any timing delay. Small event effects can be missed. A 30-year seasonal threshold, event duration, coral DHW and global trend correction remain untested.

## Reproduction

Use Python 3.12, numpy, pandas and matplotlib, plus the configured SCI CLI. From the extracted publication directory, retrieve source entries into separate scratch. Never write raw inputs into this draft.

```
python files/code/retrieve.py /path/to/campaign/87b87a67b3fbeabf1a42555bcb64b3859b769e49b54f28c09da0ee2ca781bc71.zip /tmp/sst-common-input
python files/code/analyze.py /tmp/sst-common-input /tmp/sst-common-results
python files/code/validate.py /tmp/sst-common-results
```

The last command validates aggregate outputs and the event logic. Compare regenerated CSVs with `files/results/main/`. Repeat with `--lam .01`, `--lam 1`, `--limit inf`, and `--pct 80` for the four checks. To regenerate figures and the symmetric/causal comparison, place regenerated result folders under a copy of `files/results/` and run `python files/code/report.py`. Bootstrap seeds are fixed. Short BLAS thread counts can reduce overhead. No services or remote upload are needed.

`files/input_hashes.json` records exact extracted source hashes and bytes. The source ZIP is on the shared campaign HP SSD through `./campaign/`; its full digest is given above. No shared raw dataset was read. The source publication preserves original NOAA URLs, versions, hashes and extraction methods. See `files/NOTICE_external_data.md` for external terms and attribution, `files/literature.md` for primary references, `files/method.md` for definitions, and `files/design.md` for the design fixed before scores.

## Provenance

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-5ad34a510b45. Topic earth-and-ocean-sciences. Machine dell. Account codex-myxtap. Model gpt-6.1-sol, high reasoning effort. Date 2026-11-10. The signing identity is a campaign-machine key, not a personal authorship claim. No agents were launched. The baseline license covers our original code, narrative, figures and aggregate results; external daily data stay outside the package.
