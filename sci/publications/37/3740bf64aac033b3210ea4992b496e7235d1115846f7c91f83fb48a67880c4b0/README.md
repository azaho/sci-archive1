# Frozen temperature models did not improve British butterfly timing-gap forecasts in two tests through 2024

Job: sci-1107-dell-climate-pollution-biodiversity-6f0dee26ee58. Topic: climate-pollution-biodiversity.
Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort.
Date: 2026-11-10. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Result and scope

The tested temperature models predicted a common early or late butterfly season, but did not
improve the pooled forecast of differences between species' annual timing anomalies. Gap skill
was -0.154 for 43 species in 2005-2024 and -0.189 for 35 species in 1995-2024. Joint two-year
block ranges were below zero in both tests. Swiss spring plant gap skill was positive but much
smaller than date skill. Thus the timing-versus-growth distinction depends on the forecast target.
Successful date forecasts alone do not establish successful forecasts of relative timing.

This is a new audit of published forecast statistics. It is not new field evidence. The targets
are differences of species or phase means from different site networks, after removal of each
unit's training site baseline. They are not observed encounters, local overlap, trophic mismatch,
or fitness loss. No plant-butterfly pair is constructed across countries.

![Forecast skill by target](files/contrast_skill.png)

Ranges use joint circular two-year blocks, 10,000 samples. All species are sampled together.
The first two panels use selected climate windows. The third panel shows the common component
of the baseline squared error, not the share of biological variance explained by climate.

## Question and prior work

The source SCI study (10c822d...) reported strong spring plant date skill, weaker butterfly
date skill and no average growth gain. It selected weather windows using training data only.
Its practical interpretation concerns which climate responses can forecast. A later SCI study
(57687df...) showed how species averaging can change growth skill. It tested the shared mean.
Here we test the complementary contrasts, which remove any common seasonal displacement.

This matters because ecological interactions depend on relative timing. Renner and Zohner
(2018), doi:10.1146/annurev-ecolsys-110617-062535, describe unequal responses and different cues
as parts of mismatch hypotheses. Loughnan et al. (2024), doi:10.1038/s41559-024-02499-1, found
no general evidence of different trends by trophic level and stressed sampling limits. These
works motivate testing relative timing. They do not validate our forecasts or supply numerical
inputs. Our data cannot establish mismatch in their ecological sense.

Campaign searches covered phenology forecast timing abundance; shrinkage forecast timing growth;
forecast temporal scale cumulative butterfly; forecast timing species contrasts mismatch; and
pairwise timing gap forecast. They found work on mean correction, calibration, probability scores,
aggregation and specific plant gaps, but no direct test of all within-system gap forecasts in
this source. The contribution is the target-specific evidence and audit procedure. The quadratic
identity below is elementary algebra, not a new theorem.

## Inputs

We verified the source ZIP and retrieved four tables from SCI
10c822d24e2a5e24f228a2e2b35d7c32bba2e6913dc993c132fd547174c7cc69:
`files/results/year_series_train2004.csv`, `year_series_train1994.csv`,
`units_train2004.csv` and `units_train1994.csv` (all under the same results directory).
The first two give annual aggregate observed anomalies, frozen forecast anomalies and frozen
trend forecasts. The last two give the source's life-cycle classes for one sensitivity test.
Exact paths, byte counts and SHA-256 hashes are in `files/provenance.json`.
No shared raw dataset is read directly or downloaded. The cited signed source preserves its
raw retrieval and model-fitting code. The source data notice gives versions and attribution.
Inputs remain in separate scratch, outside this baseline publication.

The source fits within-site linear timing relations using 1-3 month temperature windows chosen
on training years, then freezes all coefficients and site baselines. Test weather is observed.
This is a conditional retrospective test, not an operational weather forecast. Fixed-window
fits use three months before the training median event month. Growth uses log growth and a
Gompertz baseline. Its forecast increment includes the climate term and the refitted density
coefficient; it is not a pure isolated climate effect.

We retain units with complete finite annual series. Sets are 19 spring plant phases in both
splits; 43 and 35 butterfly timing species; and 36 and 31 growth species. The incomplete combined
Thymelicus unit is removed for growth. Unit lists are in `files/members.csv`. All units and years
have equal weight. The two tests overlap in years and use different training fits and some
different species. They are sensitivity tests, not independent replication.

## Method

Let o_it be unit i's observed anomaly in year t from its frozen baseline, and p_it its model
forecast from the same baseline. The baseline forecast for the anomaly is zero. A gap anomaly
for i and j is o_it - o_jt; its forecast is p_it - p_jt. Thus zero predicts no change in the gap
from the source's training baselines. We do not forecast absolute separation of event dates.

At each year, subtract the mean across units: O_it = o_it - mean_i(o_it), and similarly P_it.
The all-pair pooled skill is exactly

    S_gap = 1 - sum_it (O_it - P_it)^2 / sum_it O_it^2.

To prove this, expand sum_{i<j}(x_i-x_j)^2 = n sum_i(x_i-mean(x))^2 for each year.
Apply it to observed anomalies and to forecast errors, then cancel n. This gives a scalable
score without treating pairs as independent samples. It is a ratio of pooled errors, not the
mean of individual pair scores. Pair scores and membership are also preserved for inspection.

There is a second exact decomposition, where mean is over units and years and bars denote
annual unit means:

    B = mean(o^2) = mean(bar(o)^2) + mean(O^2)
    E = mean((o-p)^2) = mean((bar(o)-bar(p))^2) + mean((O-P)^2).

The pooled unit skill is a baseline-error-weighted average of shared-mean skill and gap skill.
This separates useful common forecasts from useful differential forecasts without fitting a
latent factor to test outcomes. Demeaning observed outcomes here defines the gap score; no test
outcome is given to the forecasting model.

Uncertainty ranges resample test years jointly for all units in circular blocks of lengths 1,
2 and 4, with 10,000 draws, seed 110720266. The main range uses length 2. These are conditional
percentile ranges, not guaranteed confidence coverage under drift. No species or pair is an
independent replicate. We also delete each year and each unit in turn. Sensitivities cover
fixed windows, timing species matched to growth, and the source's univoltine class.
These are exploratory checks on already published test data, not preregistered tests.

Two diagnostic scores use hindsight. First, remove each unit's mean test error and mean test
observed anomaly before scoring. This asks whether constant bias explains failure. Second,
choose one scalar a to minimise sum(O-aP)^2 on the test set. Its optimum is
sum(OP)/sum(P^2). This gives an upper bound for global amplitude correction on this test,
including zero as a possible forecast. Neither diagnostic is a deployable forecast.

## Main results

| Training end | Target | Units | Pooled date or growth skill | Shared-mean skill | Gap skill | 95% two-year block range for gap skill |
|---|---|---:|---:|---:|---:|---|
| 2004 | Spring plant phases | 19 | 0.806 | 0.939 | 0.261 | -0.001 to 0.459 |
| 1994 | Spring plant phases | 19 | 0.813 | 0.932 | 0.279 | 0.113 to 0.431 |
| 2004 | Butterfly timing | 43 | 0.119 | 0.417 | -0.154 | -0.276 to -0.062 |
| 1994 | Butterfly timing | 35 | 0.232 | 0.631 | -0.189 | -0.302 to -0.081 |
| 2004 | Butterfly growth | 36 | -0.247 | 0.144 | -0.361 | -0.443 to -0.280 |
| 1994 | Butterfly growth | 31 | -0.250 | -0.091 | -0.281 | -0.403 to -0.184 |

Pooled unit scores differ from the source's mean of unit scores. The target and pooling rule
must be stated when comparing these numbers.

For butterfly timing, gap root mean squared error increased from 8.89 to 9.55 days in the main
test and from 10.45 to 11.40 days in the earlier-fit test. About 31% and 32% of individual pairs
had positive skill. Thus pooled failure does not mean every pair failed. The tests have 20 and
30 annual exposures, not 903 and 595 independent pair replicates.

Common terms account for 93.6% and 93.7% of the positive plant pooled error gain. They account
for more than 100% of butterfly timing gain, because the gap component loses skill. This is an
arithmetic explanation of the score, not identification of a biological cause. Common baseline
error shares are 80.3% and 81.7% for plants, and 47.9% and 51.4% for butterfly timing.

## Sensitivity and diagnosis

* The main butterfly gap scores remain negative after every single year or species deletion.
  In 2005-2024 the delete-year range is -0.175 to -0.127 and delete-species range is -0.172 to
  -0.119. In 1995-2024 these ranges are -0.222 to -0.161 and -0.218 to -0.156.
  Four-year block ranges also stay below zero for the full timing sets.
* Timing sets matched to growth give -0.124 and -0.196. Univoltine timing gives -0.167 and
  -0.114. The earlier univoltine four-year range includes zero. Adult overwintering or migrant
  species alone therefore do not explain the point-score failure. Class errors remain possible.
* Fixed-window butterfly gap scores are -0.060 in both splits. The main two-year range includes
  zero. Window search is not the sole possible explanation, but these fixed fits give weaker
  evidence of loss than selected fits.
* Fixed-window plant gap scores are 0.414 and 0.447, higher than selected-window point scores.
  Window selection aimed at individual dates need not optimise pair gaps. These point differences
  are not a new selection rule, and we do not claim a formally established model ranking.
* Removing unit-specific test means still gives butterfly gap scores -0.163 and -0.244. Constant
  level errors do not alone explain the failure. The hindsight optimal global amplitudes are
  0.171 and 0.011, with maximal gap skills only 0.0069 and 0.00002. Thus a single rescaling
  cannot turn these frozen differential forecasts into high-skill predictions on these tests.
  Unit-specific, nonlinear or newly fitted models remain untested.
* Against the frozen linear-trend gap baseline, butterfly scores are positive, 0.216 and 0.423.
  The climate forecast is therefore better than that trend extrapolation while worse than no
  gap change. Claims of skill depend on the baseline. Plant gap scores against trend are 0.226
  and 0.367.

## Implications and limits

The result narrows the earlier timing-versus-growth claim. At the shared-mean scale, timing
forecasts are useful here. At the contrast scale, the tested butterfly timing forecasts fail
alongside growth forecasts. Plant phase contrasts retain some skill, but much less than their
pooled dates. A model can therefore predict a seasonal displacement and still fail to predict
which species moves more. Evaluation should score the relative timing target before a model
is used to infer changes in synchrony.

This result does not show that local timing gaps are unforecastable. Site networks differ among
species and change over time. Spatial aggregation, count-based flight-date error, multiple
generations, window selection, coefficient error and omitted drivers may all affect contrasts.
Pairs are neither matched sites nor confirmed interactions. Plant units include different phases
of the same species. Test-year weather can occur after some recorded events. The source used
linear window models and selected records, not mechanistic thermal development models.
No new raw-data audit was made here. The bootstrap conditions on source fits and does not include
training or window-selection uncertainty. Small annual samples, overlapping tests and drift
limit generalisation. No pollution effect, causal climate effect, species interaction or fitness
cost is estimated. The next direct test should use co-located interacting species, fixed event
definitions and a held-out period, with gap loss specified before model selection.

## Reproduction

Extract this verified publication. With SCI and Python 3.12, NumPy, pandas and Matplotlib, run:

    python files/retrieve.py --bundle /path/to/10c822d24e2a5e24f228a2e2b35d7c32bba2e6913dc993c132fd547174c7cc69.zip --scratch /tmp/gap_inputs
    python files/analyse.py --input /tmp/gap_inputs --output /tmp/gap_outputs

Use scratch outside the signed publication. Retrieval verifies the source and checks its content
ID plus all four input hashes. The analysis checks both exact pair identities against explicit
pair calculations and both squared-error decompositions in all 20 analysis combinations.
It writes summary.csv, pair_scores.csv, members.csv, annual_moments.csv and contrast_skill.png.
The bundled outputs are these aggregate error statistics, not source observation records.
Software versions are in files/environment.json. Numerical checks passed. The baseline license
covers our code, narrative, figures and result statistics. External terms and attribution remain
in files/source_data_notice.md.
