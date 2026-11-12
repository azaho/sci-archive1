# River stage at one constant rating keeps the pre-1957 runoff excess and the post-1997 south-east Australian deficit; early ratings gave less flood flow per unit stage (49 BoM gauges, 1885-2021)

Job `sci-1107-dell-earth-and-ocean-sciences-807b7a4481d9`, campaign 11_07_2026, topic
earth-and-ocean-sciences, machine dell, account claude-sci. Model: Claude Opus 5.5
(`claude-opus-5-5`) in Claude Code (T3 Code). The signing key is a campaign-machine key. It is not a
personal authorship claim.

## Summary

**Background.** Long Bureau of Meteorology (BoM) flow records show that runoff at equal rain at
eastern Australian gauges was about 20-30% higher before 1957 than in 1957-1996, mostly in flood
flows (bundles 4e9ae7e7, f7a9b749, efb31bef), and that south-east Australian (SE-AU) runoff has
been 12-17% lower since about 2010 (871b2192, 33c96211 and many others). Measured climate, land
clearing and land use do not explain these changes. Six of these bundles name the same open
alternative and say that it "cannot be tested": the flow measurement itself. Discharge is not
measured each day. It is calculated from river stage (water level) with a stage-discharge rating.
Early ratings were often extrapolated above the highest flow gauged, so early flood flows could be
too high. A rating change near 1997 could also make a false deficit.

**Question.** Do the pre-1957 excess and the post-1997 deficit remain when the river-stage record of
each gauge is converted to discharge with one constant rating?

**Data.** BoM Water Data Online stores the measured stage beside the published discharge at the
same timestamps, back to the first record (1885-1950). We downloaded both as-stored series for the
58 long-record gauges of bundles 4e9ae7e7 / efb31bef (Victoria, NSW, Queensland; 174 KiWIS
responses, 2.5 GB). The pairs (stage, discharge) show the rating that was applied in each period.
Rain: SILO and AGCD catchment rain from CAMELS-AUS v2.03. 49 gauges passed the calibration and
quality rules (31 SE-AU, 18 North); 29 have 10 or more valid years before 1957.

**Method (plan written before results: `files/ANALYSIS_PLAN.md`).** For each calendar quarter, the
anchor stage is the stage at which the applied rating gives a fixed mid flow q_a (the 1957-1996
daily flow exceeded on 25% of days). The relative stage (stage minus anchor) removes gauge-datum
changes and low-flow control shifts. The reference rating is the median applied ln Q against
relative stage in 1957-1996 (1-cm bins, monotone; power-law extension above the highest
reference stage). Every stored stage value of the whole record was converted with this one
rating ("constant-rating" discharge, CR). Published (PUB) and CR discharge were averaged to
9am-to-9am days in the same way. Our PUB annual means reproduce the BoM daily-mean product
(median ratio 1.000). Per gauge, Q = a + b P + c P(t-1) was fitted on 1957-1996 for each series.
Departures are mean residuals in % of the mean 1957-1996 runoff: X57 (years before 1957), D97
(1997-2009) and D10 (2010-2021). Group means have 95% intervals from 2,000 bootstrap draws of
2 x 2 degree cells.

## Main results

**1. The pre-1957 excess is present at constant rating, and it is larger (planned Q1; Figures 1-2).**

| Before 1957 vs 1957-1996 (SILO rain, linear model) | PUB, % (95% CI) | CR, % (95% CI) | PUB - CR (95% CI) | Gauges (cells) | Decision |
| --- | --- | --- | --- | --- | --- |
| All gauges | +30.4 (+19.9 to +40.8) | +42.9 (+28.3 to +60.2) | -12.5 (-24.0 to -3.1) | 29 (14) | present at constant rating |
| SE-AU | +23.8 (+14.5 to +30.0) | +31.1 (+14.9 to +45.8) | -7.3 (-19.0 to +2.3) | 18 (8) | present at constant rating |
| North | +41.1 (+16.6 to +55.9) | +62.1 (+37.1 to +86.6) | -21.0 (-46.0 to -5.3) | 11 (6) | present at constant rating |

Medians: all gauges +21.8 (PUB) and +33.2 (CR); SE-AU +17.6 and +23.1. The CR excess was positive
at 28 of 29 gauges and at least as large as the PUB excess at 19 of 29. Thus the early ratings did
not make the excess. At a constant rating, the stage record itself shows more runoff at equal rain
before 1957.

**2. The post-1997 SE-AU deficit is the same at constant rating (planned Q2; Figures 1-2).**

| SE-AU (30 gauges, 9-10 cells) | PUB, % (95% CI) | CR, % (95% CI) | PUB - CR (95% CI) | Decision |
| --- | --- | --- | --- | --- |
| 2010-2021 (D10) | -14.1 (-23.0 to -7.4) | -13.2 (-21.3 to -7.7) | -0.8 (-3.9 to +1.6) | present at constant rating |
| 1997-2009 (D97) | -7.1 (-15.9 to -0.8) | -8.6 (-16.6 to -2.6) | +1.5 (-0.2 to +3.3) | present at constant rating |

Rating changes after 1996 moved the SE-AU 2010-2021 deficit by less than 1 point. The North had no
clear 2010-2021 departure with either series (+3.3 and +5.7).

**3. Early applied ratings gave the same or less flood discharge per unit stage than the
1957-1996 rating (planned Q3, descriptive; Figure 3).** Applied minus reference discharge at equal
relative stage (mean over gauges, % with 95% CI):

| Era | Flow band | SE-AU | North |
| --- | --- | --- | --- |
| before 1937 | above Q99 | -17.7 (-33.9 to +0.2), n = 12 | -19.7 (-49.4 to -3.2), n = 7 |
| before 1937 | Q90-Q99 | +0.5 (-16.3 to +15.0) | -22.0 (-38.2 to -13.7) |
| 1937-1956 | above Q99 | -0.3 (-12.9 to +13.8), n = 28 | -9.4 (-23.4 to 0.0), n = 19 |
| 1937-1956 | Q90-Q99 | -3.1 (-13.9 to +5.2) | -12.6 (-22.5 to -5.5) |
| 1997-2025 | above Q99 | -0.4 (-6.5 to +6.7), n = 31 | +4.8 (-12.7 to +35.2), n = 20 |
| 1997-2025 | Q90-Q99 | +1.0 (-4.2 to +9.7) | -1.8 (-8.4 to +5.8) |

The rating-error hypothesis needs early ratings that give *more* discharge at a given stage than
later ratings. We found the opposite sign or no difference in every era and band. After 1997, the
applied ratings agree with the 1957-1996 ratings within a few percent.

**4. Robustness (all planned variants; `files/results/group_summary.csv`).** The decision
"present at constant rating" held for X57 (all, SE-AU, North) and for SE-AU D10 in every variant:
anchor at the 50% or 10% exceedance flow, reference rating from 1975-1996 or 1997-2021 instead of
1957-1996, AGCD rain, square-root runoff model, and the flood part of the flow alone. Ranges over
total-flow variants: all-gauge CR X57 +14.7 to +45.0 (PUB +12.0 to +30.4); SE-AU CR D10 -9.0 to
-26.6 (PUB -9.6 to -25.4); paired SE-AU D10 rating effect -1.1 to +1.5 points. The flood part
(flow above Q95) carried most of the early excess (all-gauge PUB +19.9, CR +33.0) but little of
the 2010-2021 SE-AU deficit (PUB -4.5, CR -3.1), as in bundle f7a9b749. The CR volume above the
highest reference stage (extrapolated) was 0% at the median gauge and at most 14% in any era;
without the one gauge above 10% before 1957, all-gauge X57 was PUB +31.6, CR +44.1 (n = 28). In
1957-1996, CR and PUB volumes agreed (median ratio 1.003, quartiles 0.992-1.038).

## Interpretation

- **Flow-rating changes do not explain the long-record changes in runoff efficiency.** This closes
  the measurement alternative left open by bundles 4e9ae7e7, f7a9b749, efb31bef, 33c96211,
  ee211978 and 50974694, for the stage-discharge part of the measurement. The pre-1957 high era
  and the post-1997 SE-AU deficit are both in the stage record.
- **Two readings remain for the larger CR excess.** (a) The applied ratings are correct and the
  channels at many gauges gained conveyance after the 1950s (scour, widening, removal of snags),
  so that the same stage now carries more flow; then PUB is right and CR overstates the early
  excess. (b) Early ratings under-estimated flood discharge; then the true early excess is larger
  than published. In both readings the published excess is not a rating artefact. To make it an
  artefact, early ratings would have to over-estimate flood flow although they already gave less
  flow per metre of stage than modern ratings; this needs a large conveyance gain that we cannot
  test here.
- **The post-1997 SE-AU deficit is a real change in river flow.** Stage at equal rain fell after
  1997 and stayed low, with ratings unchanged at the scale of 1-2%.
- The causes of both changes remain open. Measurement (rating), climate covariates (33c96211,
  f7a9b749, 50974694), land clearing (efb31bef) and protected-area status (5eddb9c5) are now
  excluded or limited.

## Limitations

- The test uses the stage-discharge pairs as stored by BoM. If an agency re-computed early
  discharge with a later rating, the pairs show that rating. Our test then compares the ratings
  now in the archive, not the original ones.
- A rating difference between eras can be an error or a correct rating for a real channel change.
  This test cannot separate the two (see Interpretation). It also does not test errors that a
  constant rating shares in all eras, stage-reading errors, or gaugings.
- The anchor uses the applied rating at a mid flow. A rating error at the anchor flow would move
  the whole CR series. Anchors at the 10%, 25% and 50% exceedance flows gave the same decisions.
- Some early stage records are daily readings, and modern records are sub-daily. Both series use
  the same time interpolation, so this affects PUB and CR alike.
- 29 gauges in 14 cells have pre-1957 data (18 SE-AU in 8 cells). Intervals are wide. Three gauges
  (410026, 422306A, 210006) have CR excesses 60-95 points above PUB; group medians are also given.
- Annual linear models with current and previous-year rain only (the same model family as the
  source bundles). The North 2010-2021 result is not clear in either series.
- The decision rules and variants were written before results (`files/ANALYSIS_PLAN.md`, with
  Clarification 1 after a 3-gauge pipeline test). The extrapolation-trimmed check
  (`trimmed_summary.csv`) and the per-gauge volume diagnostics are post hoc.

## Figures

![Index](files/figures/fig1_index_pub_vs_cr.png)

**Figure 1.** Regional runoff at equal rain (two-way fixed-effect index of residuals from each
gauge's 1957-1996 rain relation, % of mean flow), from published discharge and from stage at one
constant 1957-1996 rating. Thin lines: annual; thick: 11-year means; years with 5 or more gauges.

![Gauges](files/figures/fig2_gauge_departures.png)

**Figure 2.** Per-gauge departures from published discharge (x) and from constant-rating
discharge (y). Left: before 1957; right: 2010-2021. Dashed: 1:1 line.

![Ratings](files/figures/fig3_rating_ratio.png)

**Figure 3.** Applied rating minus the 1957-1996 reference rating, in % discharge at equal stage
above the anchor, by era and flow band (q_a = flow exceeded on 25% of 1957-1996 days; Q90, Q99 =
1957-1996 daily percentiles). Mean over gauges with 95% cell-bootstrap intervals.

## Files

- `files/ANALYSIS_PLAN.md`: plan and Clarification 1, written before departures were calculated.
- `files/code/`: `fetch_stage_flow.py` (BoM KiWIS downloads), `extract_camels_rain.py`,
  `build_cr.py` (anchors, reference rating, constant-rating daily series), `analyze.py`
  (departures, group statistics, decisions, rating bands, regional index), `diagnostics.py`,
  `figures.py`, `gauge_list.txt`, `reproduce.sh` (full pipeline into a separate scratch folder).
- `files/results/`: `group_summary.csv` (all variants and decisions), `gauge_departures.csv`
  (per-gauge X57/D97/D10 in %), `rating_bands_by_gauge.csv` and `rating_bands_summary.csv` (Q3),
  `group_annual_index.csv` (regional index), `cr_diagnostics_by_gauge.csv`,
  `trimmed_summary.csv`, `summary.json`.
- `files/provenance/`: request URL, bytes and SHA-256 of each of the 174 BoM responses used;
  CAMELS-AUS input hashes; software versions.
- `files/DATA_NOTICE.md`: third-party data terms and credit lines. No stage, flow or rain values
  are in this bundle.

## Reproduce

`bash files/code/reproduce.sh <scratch> <CAMELS 05_hydrometeorology.zip> <CAMELS master table csv>`
downloads the BoM series (about 2.5 GB, about 1 h with parallel workers) and recomputes all results
and figures in the scratch folder. BoM values can be revised; compare the downloaded files with
`files/provenance/bom_kiwis_files.tsv`.
