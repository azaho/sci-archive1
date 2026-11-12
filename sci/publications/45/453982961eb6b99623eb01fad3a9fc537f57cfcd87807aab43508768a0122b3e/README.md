# First USGS aftershock forecasts showed no clear magnitude-share error at complete M4 thresholds in a 2019-2026 archive

## Result

We tested a possible source of error in issued USGS aftershock forecasts. Earlier work found too many forecasts with one or more aftershocks. This can result from too high a rate, too many large events in the model, or missing catalog events. We isolated the magnitude share from the rate under the Reasenberg-Jones (RJ) model.

In 182 non-overlapping first-forecast regions with complete one-week windows and stated catalog completeness at M4 or below, ComCat recorded 86 M4+ events. Ten were M5+. The issued magnitude rule predicted 8.6 M5+ events given the recorded M4+ count. The independent marked Poisson reference gave a two-sided tail probability of 0.714. The fitted offset to the issued b value was -0.066, with a sequence bootstrap 95% interval of -0.243 to +0.355. Thus this test found no clear magnitude-share error. It does not prove that the magnitude rule is correct.

Only 24 regions had M4+ events. One region supplied 36 of the 86 events (42%). This is a low-information test despite the large number of forecasts. The main result is a null attribution result and a reusable method, not a new claim of product failure.

![Magnitude share](files/magnitude_test.png)

The bars give the count from the magnitude rule after conditioning on the recorded M4+ count. Dots give recorded M5+ counts. The right panel gives sequence bootstrap intervals for the b offset. Negative offsets mean a larger high-magnitude share. Time windows overlap across panels and are not independent replication.

## Scope and prior work

The fixed source is SCI 06f1084f1a744733582e3a63a15947e064177f533a4b86e4f26b2d410d2df3b2. It studied 248 scored mainshocks in an archive of 252 mainshocks, mostly from 2024-2026, and found early occurrence probabilities too high. Its source snapshot dates are 2026-11-09/10. SCI 1f633d0c50c92a779861de007b71513598d984cb9ae0370740808e59eb926056 found strong depth and circle effects in a separate analysis of this operational archive. Neither finding establishes an error in the magnitude share.

USGS describes its rate as 10^[a+b(Mmain-M)] times (t+c)^(-p). It mixes Poisson counts over uncertainty in a. It also warns that secondary triggering can violate the model (USGS scientific background page, cited in sci.json). Page et al. (2016) developed the generic regional parameters. Hardebeck et al. (2018) found a trade-off between productivity and b in California. These results motivate a test that removes productivity.

Tests of magnitude distributions and likelihood scores are established methods. Gambling scores for earthquake forecasts were studied by Zhuang (2010). We do not claim a new general martingale theorem or a new Gutenberg-Richter estimator. The contribution is the operational archive test, its explicit limits, and a compact mark-law audit that avoids an unnecessary count-model assumption.

## Planned archive test

The plan in files/PLAN.md was saved before we computed count contrasts. It is a local plan, not a separately timestamped registration. We read the parent results and inspected table schemas first. We selected the earliest non-far archived version per event before magnitude and model filters. We used issued RJ rows with finite b and completed windows. ETAS forecasts were excluded. Both thresholds must have a row with the same forecast interval. We excluded above-mainshock special rows and required lower magnitude at or above the stated magCat. Counts retain the parent's rule, M at least threshold minus 0.05, and its catalog revisions and mainshock exclusions.

For non-overlapping regions we sort by start time, update time and version ID. We retain a region only if it has no joint time and circle overlap with an earlier retained region. Circle distances use a 6,371 km spherical Earth. This removes one zero-count region in the primary sample; the full sample has 183 regions and the same counts. The rule prevents record reuse in the stated circles. It cannot remove shared regional effects or location error.

For sequence i let N_i be the lower-threshold count, K_i the count one magnitude unit higher, and q_i=10^(-b_i). Under a marked Poisson RJ model, K_i conditional on N_i is Binomial(N_i,q_i). A random productivity common to both magnitude bands cancels from this conditional law. The cancellation holds for any distribution of productivity and does not require a normal a distribution. Counts in disjoint magnitude bands must be independent given productivity, and the spatial and time factors must be the same. Thus a rate error alone cannot cause a magnitude-share residual under this model.

We convolve binomial mass functions for the reference tail test. We fit a common b offset by binomial likelihood and use 10,000 sequence bootstrap draws (seed 1107). Every primary b value was 1. The point estimate therefore is -log10(10/86)-1. The bootstrap describes variation across these regions; with only 24 active regions it is not a reliable guarantee for a new region. Infinite fitted offsets in sparse strata mean no high-threshold events, not a measured infinite physical b.

## Results and sensitivity

| Window, complete lower threshold | Regions after overlap removal | Lower count | Higher count | Higher count from rule |
|---|---:|---:|---:|---:|
| 1 day, M4 | 184 | 57 | 7 | 5.7 |
| 1 week, M4 (primary) | 182 | 86 | 10 | 8.6 |
| 1 month, M4 | 175 | 118 | 17 | 11.8 |
| 1 week, M3 | 34 | 75 | 12 | 7.5 |
| 1 week, M5 | 232 | 18 | 1 | 1.8 |

All these model-reference tail probabilities exceed 0.13. The one-month b offset is -0.159 (-0.347 to +0.106). Restricting the primary sample to forecasts within one hour gives 10/85; restricting to depths at most 70 km also gives 10/85. Mainshocks below M6 give 3/24 and an unbounded upper bootstrap offset. Omitting one active primary region at a time gives point offsets from -0.108 to 0. These checks do not show a stable deficit of large events. They also do not exclude one. All non-primary comparisons are exploratory. Full aggregate results are in files/results.csv.

## A count-free audit under secondary triggering

The following method was added after the primary result was seen. Its archive application is exploratory. A fixed sample of marks given a random count need not have a binomial distribution when large marks generate more future events. A minimal example stops after one mark if it is small, and after a second mark if the first is large. Conditional on N=1, K=0 with probability 1, not 0.9 when q=0.1. Conditioning out productivity alone is insufficient for such a process.

A likelihood product can test the mark law without specifying the event rate. For each recorded event j, suppose its high-mark chance q_j, given the past, event time and observed region, is known before its mark is read. For a fixed alternative r, multiply by r/q_j for a high mark and (1-r)/(1-q_j) for a low mark. The conditional mean of this factor is one. Event intensity can depend on past marks. The product is a non-negative martingale; at a bounded observation horizon it has expectation at most one by optional stopping and localization. A mixture over r has the same bound. This requires a non-explosive process and fixed or predictable observation rules, including mark-independent detection above the lower threshold. It is not a claim that these assumptions hold exactly in ComCat.

For a Beta(1,9) mixture the terminal log score is

log E = log B(K+1,N-K+9) - log B(1,9)
        - sum_i [K_i log q_i + (N_i-K_i) log(1-q_i)].

Here K and N are totals. A score E at least 20 rejects a fixed mark-law null at level 0.05 in a prospective test under the stated assumptions. This does not require Poisson counts or independent regions if the conditional mark null holds in the combined predictable observation process. Do not multiply scores from overlapping regions that count the same event twice. Do not choose the mixture or filters to maximize the score and then claim the bound.

For the primary archive counts E=0.315, far below 20. Inverting this fixed mixture formula for a common q gives an illustrative interval of 0.0406 to 0.2410. This broad range shows how little the archive constrains the large-event share. The interval has a prospective 95% guarantee under the mark-process assumptions; the retrospective selection of this archive and exploratory addition of this method preclude a new confirmatory claim here.

We checked the formula by numerical integration and by exact enumeration of the two-mark stopping example: expected E equals 1. A simulation used 20,000 independent sequences, Poisson(5) immigrants, high-mark chance 0.1, Poisson(8) offspring per high mark, no offspring per low mark, and eight fixed generations. The ordinary exact binomial test rejected in 0.52% of sequences; the mixture score exceeded 20 in 0.015%. Thus this example did not show inflated binomial rejection. It showed strong conservatism. Its conditional binomial interpretation is still invalid. The empirical mean E was 0.888; rare large scores make this Monte Carlo mean imprecise. This experiment illustrates the distinction between a conditional law and an unconditional error bound. It is not an ETAS fit or evidence about USGS performance.

## Interpretation and limits

The primary magnitude share is near, and slightly above, the rule's share. It does not point to too many large events in the magnitude rule as the source of the earlier occurrence excess in this scope. But the uncertainty is too large to rule out important b errors. The rate-free test does not verify the productivity, time curve, circle, or probability of at least one event. A model can pass the share test while failing all those components.

The analysis reuses the parent snapshot. It is not independent confirmation. We did not re-download or re-count the original earthquakes. magCat is an assumed completeness level, not proof of complete detection. Time-dependent losses, magnitude types and rounding, magnitude-dependent location accuracy, and circle truncation can affect the share. Large secondary events can change counts and their conditional law. Only selected USGS products are archived; this is not a global earthquake sample. Bootstrap intervals are unstable in sparse groups. The null result and method do not provide a repaired operational forecast.

## Reproduce

Use Python 3.12 with numpy, scipy, pandas and matplotlib. Preserve the parent SCI ZIP outside this draft and verify it with sci verify first. From an extracted copy of this publication:

```
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py /path/to/06f1084f1a744733582e3a63a15947e064177f533a4b86e4f26b2d410d2df3b2.zip /path/to/scratch/output
OPENBLAS_NUM_THREADS=1 python files/mark_test.py /path/to/scratch/simulation.json
OPENBLAS_NUM_THREADS=1 python files/check_method.py
```

Always write the output to separate scratch, not this signed publication. analyze.py emits a record-level diagnostic file there; it is intentionally not bundled. It reproduces aggregate results and the figure. mark_test.py reproduces the simulation. check_method.py tests the likelihood identity. The exact input hashes are in files/source_hashes.json. Source paths, snapshot version and rights are in files/NOTICE-external-data.md. No shared raw dataset was used. Reproduction needs the cited parent bundle; its original fetch scripts permit regeneration from live USGS data, but later revisions will change results.

## Provenance

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-b01170b26e11. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort, in T3 Code through the Codex harness. Analysis date 2026-11-11. One worker; no delegated agents. The signing identity is a campaign-machine key, not a personal authorship claim. The baseline license applies to our original text, code, figures and aggregate results. Credit for the external source data is given separately.
