# Paired bird surveys identify linear relative detection drift only when time varies within calibration cycles under free method intercepts

Job: sci-1107-dell-climate-pollution-biodiversity-d3da6459e892.
Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell.
Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort.
The campaign-machine signing key is not a personal authorship claim.

## Result

A second detection method does not automatically separate detection drift from
bird community change. Under a paired mean model with free human and recorder
intercepts, linear **relative** drift is identified exactly when survey time
has a nonzero contrast around at least one cycle of the human-recorder graph.
Repeated use of the same pair at different times meets this condition. A
connected graph, or repeat surveys of one human with new uncalibrated devices,
can fail it. If pair interactions are also free, only repeat pairs give this
information. Absolute drift still needs an external reference constraint.

We also tested the historical scope for repeated calibration in the North
American Breeding Bird Survey (BBS). Among eligible baseline runs, the same
observer was on the same route at the exact endpoint in **52.3% after 5 years,
34.4% after 10 years and 15.1% after 20 years**. These are schedule facts,
not forecasts of participant retention. No recorder calibration data exist in
this audit. We do not estimate a new detection correction or ecological lag.

![Calibration design, endpoint retention and precision scenarios](files/results/calibration.png)

## Contribution and prior work

The selected campaign work finds weak thermal tracking across networks
(SCI 0037934e) and low bird tracking despite strong local spatial gradients.
A hearing study reports a frequency-dependent tenure pattern (SCI b9959b67).
A subsequent proof shows that observer turnover cannot identify its linear
component when observer cohort effects are free (SCI f7eaf981). That proof
suggests a stable or calibrated paired reference, but does not specify its
assignment design or precision requirement. We develop those requirements.

Double-observer detection methods are established: Nichols et al. (2000),
[doi:10.1093/auk/117.2.393](https://doi.org/10.1093/auk/117.2.393).
Those methods use detection-history assumptions beyond the contrast model here.
Our result does not invalidate them. Farmer et al. (2014),
[doi:10.1002/ece3.1101](https://doi.org/10.1002/ece3.1101), gives independent
hearing evidence. Darras et al. (2020),
[doi:10.7717/peerj.9955](https://doi.org/10.7717/peerj.9955), tests how microphone
quality affects acoustic sampling. Jarrett et al.,
[doi:10.1111/1365-2664.70000](https://doi.org/10.1111/1365-2664.70000), discusses
long-term acoustic bias. Sharma et al.,
[doi:10.1371/journal.pone.0350789](https://doi.org/10.1371/journal.pone.0350789),
provides a local acoustic calibration framework. Thus the need for recorder
calibration is not new.

The mathematics also builds on established fixed-effect graph methods. See
[Jochmans and Weidner, 2017](https://cemmap.ac.uk/wp-content/uploads/2020/08/CWP2617.pdf)
and [Halkiewicz, 2026, v2](https://arxiv.org/abs/2608.04839v2), which explicitly
uses cycle contrasts. We do not claim a new general graph theorem. The new
contribution is its use to specify which paired bird calibration schedules can
resolve the prior detection ambiguity, the separate absolute-reference error
bound, and an audit of historical follow-up opportunities. The package includes
a small design audit tool. This is a method and design study, not a field
validation. The plan was written before the schedule calculation; the 2020
endpoint sensitivity was added after the main result.

## Model and proof

Suppose both methods measure the same abundance and availability A at the same
event. The human expected count is A exp(a_i+d_H t), and the recorder expected
count is A exp(b_j+d_R t). Their log mean contrast is

    z_e = a_i - b_j + delta t_e,    delta = d_H - d_R.

With B the human-device incidence matrix, delta is identified if and only if
t is outside the column space of B. The orthogonal complement of that column
space is the cycle space. Thus a cycle must have a nonzero alternating time
sum. This is an exact mean-model result; logs of observed counts need a
separate estimator, especially at zero. A cycle may consist of two visits to
the same pair. For independent contrast variance sigma squared, the relative
drift information is t' M_B t / sigma squared, where M_B removes method effects.

More methods alone cannot identify absolute drift. Add h to every method drift
and subtract h t from log A at each event. All expected counts remain unchanged.
An external bound or estimate of reference drift must anchor this common part.
Full derivations, scope and design examples are in files/METHOD.md.

If arbitrary pair interactions replace additive human and device effects,
repeat measurements of at least one pair are needed. A four-pair cycle with
no repeat pair then has zero information. If habitat or date changes cause
method-specific time drift, the estimated delta can include those changes.
This study does not show that the estimated difference would be hearing loss.

## Schedule data and results

We used the BBS release for 1966-2025, doi:10.5066/P144YU3S. Source metadata
cite Ziolkowski Jr., Lutmerding, Skalos, English and Hudson (2025). We thank
the thousands of US and Canadian survey participants and coordinators.
Only Weather.csv and the metadata file were read. Exact shared paths, source
URLs, byte sizes and hashes are in files/provenance.json. Raw records remain
external. No bird count, temperature or hearing measure enters this audit.

We retain RunType=1, RPID=101, positive observer ID and year at least 1966.
Route ID combines country, state and route. We sort and remove duplicate
route-years. This gives 130,303 runs, 5,319 routes and 10,417 observers, as in
the prior audit. For lag L, a baseline is eligible when its year is at most
2025-L. Success requires the same observer ID and route at exactly year t+L.
It permits intervening gaps and observer returns; it does not require continuous
service. We also count any standard run on that route at t+L.

| Years | Eligible baseline runs | Same observer and route | Fraction | Any route run at endpoint |
| --- | ---: | ---: | ---: | ---: |
| 1 | 127,744 | 98,221 | 0.769 | 106,026 |
| 5 | 117,225 | 61,308 | 0.523 | 86,648 |
| 10 | 105,287 | 36,228 | 0.344 | 72,416 |
| 15 | 91,248 | 20,987 | 0.230 | 59,999 |
| 20 | 77,399 | 11,723 | 0.151 | 48,942 |

The unit is a baseline run, not a unique participant. Baselines overlap, so
these counts are not independent samples or counts of possible independent
calibration pairs. At ten years, roughly half of routes with an endpoint run
had the same observer (36,228/72,416). Route continuation alone overstates the
opportunity to repeat the same person. Baseline-decade results are bundled.
For ten years, fractions range from 0.280 in the partial 2010s cohort to 0.387
in the 2000s. This range is descriptive and affected by the years included.

BBS had no 2020 runs. Excluding baselines whose endpoint is 2020 raises the
five-, ten- and twenty-year fractions to 0.536, 0.354 and 0.157. The conclusion
that long follow-up loses many same-person opportunities persists. These
fractions combine route loss, missed surveys and observer change. They do not
measure permanent retirement or device survival.

## Precision scenarios and a reference error floor

For n independent pairs measured at times 0 and L, with single-visit contrast
SD sigma and a known stable reference, the relative slope SE is

    sigma sqrt(2/n) / L.

For an ideal additive CTI calibration, assume sigma=0.05 C and a target Gaussian
95% half-width of 0.005 C per decade. This is a chosen scale, near the small
corrected trend in the prior audit; sigma is not an estimate from bird data.
The required completed pairs are:

| Follow-up years | Completed pairs | Baselines for that expected yield at historical fraction |
| --- | ---: | ---: |
| 1 | 76,830 | 99,924 |
| 5 | 3,074 | 5,878 |
| 10 | 769 | 2,235 |
| 15 | 342 | 1,487 |
| 20 | 193 | 1,275 |

The last column divides by the pooled historical endpoint fraction. It is an
expected-yield scenario, not a probability guarantee, feasible recruitment
plan or cost optimum. It assumes random attrition, independent completed
pairs and the same drift in survivors. Real calibration can violate all three.
The apparent benefit of waiting assumes a linear drift for up to 20 years;
reference maintenance and delay costs are absent. With sigma=0.02 or 0.10 C,
requirements change by factors near 0.16 or 4; the full integer grid is bundled.
A CTI contrast does not necessarily cancel the ecological signal as species
count contrasts do. The additive CTI model needs field validation.

Even infinite paired samples cannot remove uncertainty in reference drift.
For an independent reference slope SE s_R, total variance is
2 sigma squared/(n L squared) + s_R squared. To meet this half-width target,
s_R must be below **0.002551 C per decade**. For an unknown fixed reference
bias bounded by K, K must be below 0.005 C per decade. These are conditional
accuracy requirements, not measured performance of an acoustic recorder.
An amplitude calibration alone does not establish them.

## Checks, limits and use

All five design examples match their exact information values. An independent
vertex-potential algorithm agrees with matrix projection on 1,000 random
graphs (857 with information). Algebra checks confirm the common drift alias.
Three Gaussian experiments with 20,000 draws each agree with the analytic SE;
95% interval coverage is 0.948 to 0.950. They test the formula under its own
assumptions, not real field coverage. Decade totals and endpoint nesting pass
independent aggregate checks. Results are in files/results/validation.json.

The study does not estimate biological lag, a true CTI trajectory, hearing
loss, detection variance or a climate effect. Its exact identification results
are conditional on a shared target, linear method drift and stated nuisance
effects. Human and recorder footprints may differ; both can share changes in
song availability. Such shared changes cancel from the contrast and remain
confounded with abundance. Device, classifier and habitat changes need their
own calibration. Survivor bias can make a precise slope unrepresentative.
Known Gaussian error was assumed for the precision examples. The historical
schedule contains no device identity, so the graph examples are synthetic
proposed designs, not claims about a real calibration network.

A practical next study can register repeated simultaneous pairs, retain device
and classifier versions, use controlled sound sources across frequency and
habitat, and estimate a stable reference error bound. It should test the design
matrix before data collection and estimate contrast covariance in a pilot.
These steps resolve defined parts of the detection problem. Habitat changes
and ecological response rates still need separate evidence.

## Reproduce

Python 3.12 with numpy, pandas, scipy and matplotlib is sufficient. Tested
versions and seeds are in files/results/summary.json. From the bundle root:

    python files/code/retrieve.py /absolute/external_inputs
    OPENBLAS_NUM_THREADS=1 python files/code/analyze.py /absolute/external_inputs/Weather.csv /absolute/recomputed
    python files/code/validate.py /absolute/recomputed

Use a directory outside this signed publication for inputs and outputs.
The retrieval script checks the fixed source hash and never overwrites an
existing input. To reuse campaign data, replace the input path by
/mnt/dell-data/shared_datasets/bbs-2026-release-weather-6a0b0b0a/Weather.csv.
The source may change or become unavailable; the fixed hash then fails safely.
The prior SCI publication also records retrieval provenance.

For a proposed design CSV with human,device,year columns, run:

    python files/code/design_audit.py /absolute/design.csv
    python files/code/design_audit.py /absolute/design.csv --pair-effects

The tool reports relative slope information for unit independent error. It
uses dense least squares and is intended for small planned calibration designs.
It never identifies an absolute drift without an external reference constraint.
Bundled outputs are our aggregate schedule counts, synthetic diagnostics,
scenario calculations and original figure. No record-level table is bundled.
The separate external-data notice explains source terms. No private scratch
file is needed to reproduce the work.
