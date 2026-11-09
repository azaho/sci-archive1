# Warm January-February seasons were linked to wider plum-to-cherry flowering gaps in four Japan samples, 1953-2024

We tested whether seasonal warmth changes the gap between first plum and cherry flowers. We used 3,260 paired station-years at 48 Japan stations in 1953-2024. Models removed station means and a time trend and controlled March temperature. A degree C warmer January-February season was linked to a 6.58-day wider gap (95 percent interval 5.27 to 7.90). The link was positive in four separate East and West, early and late samples after correction for eight tests. Plum dates moved earlier more strongly than cherry dates. March slopes were negative but did not pass the corrected tests. The winter link remained positive with year effects, station trends, prior December adjustment, and on-site records. This is an observational result. Some weather occurred after plum flowering. Unknown visits, tree changes, selected long records and coarse weather limit inference. The study does not measure pollinator overlap, pollution, daily extremes or a causal climate-change effect. The package includes code, paired records, source hashes, numerical checks and figures.

## Question and prior work

Does warmth early in the year change the time from the first plum flowers to the first cherry flowers? This gap can change even when both events move earlier. It is a timing contrast between two tree types. It is not flower duration or a measure of food supply.

Hsu et al. (2023, doi:10.1016/j.agrformet.2023.109571) found different winter and spring links with cherry flowering along a Japan latitude gradient. Miller-Rushing et al. (2007, doi:10.3732/ajb.94.9.1470) found different temperature responses among cherry taxa at Mt. Takao. These studies support tests of relative timing. They do not establish the plum-to-cherry gap tested here.

We ran `sci search "phenology climate biodiversity pollution" --in ./campaign --json` and `sci search "cherry" --in ./campaign --json` before model inspection. Full verification searches did not finish and were stopped. We also searched published bundle metadata for cherry, plum, Japan and phenology. No plum gap study was found in those metadata. This is not a complete review. We then read publication f1084f2a with SCI. Its first-to-full cherry gap differs from our between-species gap. The raw archive overlaps; this is not an independent new observation network. No code or derived data from that study enter our analysis. Its verified main text is preserved in files/prior_cherry.txt.

This study is exploratory. The four region-period fits were added after the first pooled estimates were inspected. There was no external registration. East and West have separate stations. Early and late periods have separate years. Regions still share weather and observation rules; periods share station sites. These are separate samples, not independent experiments.

## Data and observation controls

JMA tables 001 and 004 give first flowering for plum (ume, Prunus mume) and cherry (standard Yoshino cherry). We use 1953-2024. JMA defines first plum flower as five to six open flowers on the sample tree. We keep only flags 8 and 9, which mark the standard type on the station grounds or nearby. Flags 6 and 7 mark substitutes and are excluded. Zero and invalid dates are missing. Dates are month times 100 plus day. October-December winter/spring records refer to the preceding calendar year. We preserve 38 such plum records as signed days from January 1, rather than discard them as late events.

We use the last station-history coordinates for each three-digit JMA station code. The scope is 30-40 N and 130-142 E. A station must have at least 50 paired years in total and 20 in each half. The final fixed set has 48 stations: 28 West (longitude below 137 E) and 20 East. There are 3,260 pairs out of 3,456 possible station-years (94.3 percent). Every model uses the same paired date rows within its sample. This controls changing station composition and unequal samples between species. The mean gap is 44.77 days. Two events can overlap or reverse their order; negative gaps are retained.

Temperature data were provided by NOAA PSL, Boulder, Colorado, USA. We use the GHCN-CAMS monthly land temperature snapshot in the shared store, version 3.01 in the file metadata. Fan and van den Dool (2008) describe the method. We match each current station position to the nearest 0.5-degree grid cell. January-February is the equal-month mean. March is a separate covariate. These are fixed calendar windows. Kelvin values are converted to degrees C. The nearest-cell data were complete for the paired rows. December of the prior year and June of the event year enter checks only.

Observation visits, tree replacement and cultivar changes are unknown. Station effects control stable differences, not changes in effort. Long-record selection can favor stable stations. Nearby and on-site codes are imperfect: before 1988, nearby observations can be coded as on-site. We therefore treat the on-site check as partial. Current coordinates can misrepresent past locations. Shared meteorological inputs can cause spatial dependence.

## Models and uncertainty

We fit equal-weight ordinary least squares:

`cherry_date - plum_date = station effect + winter_slope * JanFeb + March_slope * March + linear_time_trend + error`.

The trend is in decades. We use a two-way cluster covariance by station and calendar year, with finite sample corrections. A t reference has degrees of freedom equal to the smaller number of station or year clusters minus one. These intervals are approximate; few clusters can limit coverage. The pooled 95 percent intervals are descriptive. For the four region-period fits and two temperature slopes, we use Bonferroni limits at 1 - 0.05/8 per interval. The family error bound does not require independent tests. It does not correct for the full exploratory analysis history.

Checks add year effects, separate station trends, prior December temperature, or future June temperature. Other checks retain only code-8 pairs or remove cross-year plum dates. We also fit each species date on the same predictors, and leave out each station in turn. The independent check uses within-station demeaning and NumPy least squares to verify the pooled coefficients.

## Results

The pooled winter slope was +6.58 days per degree C (95 percent interval +5.27 to +7.90). It remained positive in all four samples with eight-test adjusted intervals. March slopes were negative, but all four adjusted intervals included zero.

| Region | Years | January-February slope | Adjusted interval | March slope | Adjusted interval | Pairs |
| --- | --- | ---: | --- | ---: | --- | ---: |
| East | 1953-1988 | 6.36 | 3.29 to 9.43 | -0.30 | -3.18 to 2.59 | 689 |
| East | 1989-2024 | 6.31 | 3.27 to 9.36 | -2.73 | -5.91 to 0.45 | 668 |
| West | 1953-1988 | 8.34 | 5.50 to 11.18 | -1.82 | -4.79 to 1.15 | 957 |
| West | 1989-2024 | 5.83 | 2.33 to 9.34 | -2.08 | -6.09 to 1.94 | 946 |


![Four sample results](files/four_samples.png)

In the same pooled sample, January-February slopes were -7.43 days per degree C for plum and -0.84 for cherry. Their difference gives the +6.58-day gap slope. March slopes were -0.63 for plum and -2.90 for cherry, which gives the -2.26-day gap slope. Thus the pooled gap links agree with unequal seasonal responses of the two dates.

The winter gap slope was +5.52 with year effects (95 percent interval +2.47 to +8.57), +6.64 with station trends, +6.57 for on-site pairs, and +6.53 without cross-year plum records. Prior December adjustment reduced it to +4.20 (+2.72 to +5.67); December itself had a +4.51-day slope. This shows that the winter signal is not confined to January-February. The June control slope was +0.16 (-1.81 to +2.12), which gives no clear future-month link. This null check cannot prove absence of confounding.

The pooled March slope was -2.26 (-3.64 to -0.89). With year effects it was -2.00 (-5.05 to +1.06). A common precise March effect is therefore not supported across designs. Leave-one-station-out winter slopes ranged from 6.50 to 6.70; March slopes ranged from -2.35 to -2.21.

## Interpretation and limits

Warm early-year seasons were linked to wider first-flower gaps, mainly through stronger advancement of plum dates. This is consistent with different seasonal temperature responses. It does not isolate a biological mechanism. Daily chilling, heat sums, light, rainfall and management were not measured. January-February includes weather after some plum dates; March includes weather after most plum dates and some cherry dates. These covariates describe seasonal conditions, not past-only forecast inputs. A warm-season coefficient is not a causal warming effect.

The two species do not directly pollinate each other. A wider first-date gap does not prove a wider resource gap, less flower overlap, or harm to biodiversity. Such tests need flower end dates, abundance and insect records. We do not test air pollution or daily weather extremes. This study addresses the ecological timing part of the campaign objective. Generalization beyond this selected Japan network requires other regions and observation systems. The useful result is a reproducible between-species contrast that can be tested with those data.

## Reproduce and inspect

The main result can be checked without the large raw weather file:

```sh
python files/check_panel.py
```

Run from any directory. The script finds its paired panel beside itself. It repeats the four fits, the corrected intervals, the figure, and the independent pooled least-squares check. All checks passed; the largest pooled coefficient difference was below 1e-9. `panel.csv` stores the paired dates, flags, station coordinates and temperatures in degrees C. `estimates.csv` stores all model slopes. `four_samples.csv`, `leave_one_out.csv`, and `checks.json` preserve additional evidence.

For a full rebuild, use Python 3.12.16 and the package versions in files/summary.json. Supply the shared dataset root:

```sh
python files/analyze.py /mnt/dell-data/shared_datasets
python files/check_panel.py
```

The builder hashes each used raw file. It reads shared sources in place. A local scratch copy of the weather file was used to avoid repeated remote reads; the final builder checks its hash if that optional cache exists. That cache is outside the publication. The raw files are not included in the bundle. Exact logical paths, resolved immutable paths, source URLs, download metadata and full SHA-256 values are in files/provenance.json. To retrieve elsewhere, download each source URL to its named dataset directory under your chosen root and require an exact hash match. Mutable source URLs can change; in that case use the retained shared snapshot. Derived evidence remains inspectable without retrieval.

## Job and rights

Job: sci-1107-syam2-climate-pollution-biodiversity-e970dbcddd0f. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. One worker performed this study; no agents were launched. The campaign-machine signing key records package integrity, not personal authorship. No private key is included. The baseline license covers our text, figures, derived data and code; source data remain subject to their source terms.
