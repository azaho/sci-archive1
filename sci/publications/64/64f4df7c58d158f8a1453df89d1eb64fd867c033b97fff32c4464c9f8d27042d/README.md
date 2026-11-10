# Independent magnitude draws gave larger-first pair order in a six-cell deep-earthquake branching test

We tested whether larger-first earthquake pair order requires dependent magnitude draws. We used 785 deep ComCat events in 2000-2025 to set a magnitude slope, event count and background locations. We ran 400 catalogs in each of six branching-model cells. Each new magnitude was drawn independently. With magnitude-dependent productivity, a global label-shuffle test rejected in 99.0% to 99.75% of catalogs. With constant productivity it rejected in 4.0% to 5.25%. An exact expectation for direct parent-child edges explains the sign. This is a test of a method, not a fitted physical explanation of the source catalog. One source snapshot, a simplified delay law, selected model parameters and no detection model limit use.

![Simulation test](files/result.png)

## Question and prior evidence

Can a model with independent new magnitude draws give larger-first pair order and reject a magnitude-shuffle reference? This question matters when a pair test is used to argue that earlier magnitudes predict later magnitudes.

The signed campaign study [f9fd8eb2](sci:sha256:f9fd8eb2868193adbdaee7aec08f4a19db013888e95177a1167b4f670ef632f3) found a signed score of 50 in deep close pairs. It compared the score with regional magnitude shuffles and stated that rejection need not disprove independent draws in a causal process. We make that limit concrete with a simulation and an exact direct-edge calculation. We searched campaign results before choosing this question and read that publication. We read no private worker files.

[Ogata (1988)](https://doi.org/10.1080/01621459.1988.10478560) gives a basis for earthquake point-process models. [Dascher-Cousineau et al.](https://doi.org/10.1029/2019JB018111) report low productivity for deep events. A [2022 review](https://doi.org/10.1038/s41598-022-25276-1) describes debate about magnitude correlations. We used accessible abstracts and indexed text for context. This study does not introduce branching models or prove a new general law. Its contribution is a reproducible stress test tied to the published deep-pair score. Our exponential delay model is not a fitted ETAS model.

## Source and scope

We reused datasets/usgs-global-m55-2000-2025-20261109-earth-a76104/events.csv in place. It has 12,848 distinct IDs. We retained 785 records with depth greater than 300 km. All have preferred magnitude at least 5.5. Source version: ComCat snapshot retrieved on 9 November 2026. SHA-256: 162e1e37336624494321d4b9c3f0b823f433ebaeb70430af8fa70b5b2ddb16c3; size: 2,240,222 bytes. Exact shared and resolved paths, query and fields are in files/provenance.json.

ComCat has parameters from multiple networks. Credit: U.S. Geological Survey and contributing seismic networks. The source records and all event-level derived tables stay outside this package. files/EXTERNAL_DATA.md records source rights. The SCI baseline covers our own code, text, figure and aggregate results. The simulation table gives only whole-catalog counts and scores; it contains no event locations.

## Methods

files/design.txt records the local plan before computation. It was not publicly registered. Choices were informed by prior work on these data.

We map source locations to Cartesian points at radius 6371 km minus depth. For the observed and simulated data, a pair enters once if its time gap is positive and at most seven days and its three-dimensional chord distance is at most 200 km. Its score is +1 when the earlier magnitude exceeds the later by at least 0.3, -1 for the reverse, and zero otherwise. S is the sum. A tolerance of 1e-8 handles decimal roundoff. The observed graph has 175 edges; 112 pass the magnitude-gap cut, with S=50. This repeats the published count.

New magnitudes have a continuous truncated exponential density on [5.5,8.5]. We fit its slope by maximum likelihood to the 785 source magnitudes. The fitted b is 0.9265, with beta=b ln(10)=2.1333. We did not correct source magnitude rounding. This fit supplies one illustrative magnitude distribution; it is not a completeness estimate.

For each of six cells we generate 400 catalogs. The mean offspring count n is 0.1, 0.2 or 0.3. Alpha is 0 or 0.7. An event of magnitude m has a Poisson number of direct offspring with mean

k(m) = n 10^(alpha (m-5.5)) / E[10^(alpha (M-5.5))].

The expectation uses the fitted bounded magnitude density, so the mean branching ratio is n. Immigrant count is Poisson with mean 785(1-n). Immigrant times are uniform over 2000-2025; locations are independent draws with replacement from the source deep locations, without source magnitudes. Each offspring delay is exponential with mean 0.25 days. Its position is its parent's Cartesian point plus three independent Gaussian displacements of standard deviation 30 km. The displacement is redrawn until radius is below 6071 km, which keeps depth greater than 300 km. This geometry rule does not use magnitude. Post-end offspring are dropped. There is no pre-start history. We do not condition total counts or graphs to match observations.

Every immigrant and offspring magnitude is a new independent draw from the same density. Parent magnitude affects how many later events exist, not the magnitude law of a new event. The realized catalog, conditional on its future times and graph, need not have exchangeable labels. This distinction is the tested point.

For each observed or simulated graph we use 499 global magnitude permutations, holding all times and positions fixed. We recompute gap selection for every draw. Each inclusive tail uses a plus-one correction and denominator 500. The two-sided p value is twice the smaller tail, capped at one. We count p<=0.05 as rejection. The smallest two-sided p is 0.004; the largest attainable value below 0.05 is 0.048. We use seed 933122 for the entire ordered run. This is a global reference, not the earlier paper's regional reference. The global reference tests the selected mechanism because the generated mark law is the same everywhere and at every time. We do not claim a replication of that paper's p value. Our observed global p is 0.004, at the simulation resolution floor, not an estimate with four-digit accuracy.

Rejection fractions have 95% Wilson intervals across independent simulated catalogs, including finite permutation noise. These intervals describe the simulation procedure conditional on the selected source and model. Score intervals are central empirical 95% ranges, not confidence intervals for a mean. All six planned cells are shown. There is no selected best cell or data-based fit of n or alpha.

## Exact check

Let F be the bounded magnitude CDF and d=0.3. For a parent of magnitude m, the mean direct-edge signed score is

h(m) = F(m-d) + F(m+d) - 1.

An edge samples its parent in proportion to k(m). Thus the expected score per direct edge is E[k(M)h(M)]/n. At alpha=0 this is zero, since two independent magnitudes have a symmetric difference. For positive alpha, k and h both increase with magnitude, so their covariance is positive. The direct-edge expectation is therefore positive even though the child mark was drawn independently of the parent mark.

This calculation applies to direct genealogical edges before time censoring, not all proximity pairs. The graph score also has siblings, later descendants and chance pairs. It need not equal the direct-edge formula. At alpha=0.7 the formula gives 0.47610. The empirical direct-edge values range from 0.47395 to 0.47748. At alpha=0 the formula is zero and the empirical values range from -0.00282 to 0.00202. files/audit.py checks the integral through separate numerical integration and checks observed counts through a scalar spherical-distance calculation.

## Results

| Alpha | n | Mean events | Mean pairs | Mean S | S central 95% | Rejections | Rejection fraction (95% limits) |
|---:|---:|---:|---:|---:|---|---:|---|
| 0.0 | 0.1 | 786.5 | 128.1 | -0.4 | -16 to 17 | 18/400 | 4.50% (2.87 to 7.00) |
| 0.0 | 0.2 | 786.9 | 254.0 | 0.4 | -26 to 28 | 16/400 | 4.00% (2.48 to 6.40) |
| 0.0 | 0.3 | 784.4 | 439.7 | -0.2 | -38 to 37 | 21/400 | 5.25% (3.46 to 7.89) |
| 0.7 | 0.1 | 784.8 | 143.6 | 40.7 | 22 to 64 | 396/400 | 99.00% (97.46 to 99.61) |
| 0.7 | 0.2 | 784.3 | 343.9 | 92.4 | 47 to 147 | 399/400 | 99.75% (98.60 to 99.96) |
| 0.7 | 0.3 | 784.2 | 724.3 | 158.1 | 81 to 276 | 396/400 | 99.00% (97.46 to 99.61) |

With alpha=0.7, rejection occurs in 99.0% to 99.75% of catalogs, despite independent new magnitude draws. With alpha=0 it occurs in 4.0% to 5.25%; each Wilson interval includes 5%. This control removes magnitude dependence from productivity while retaining branching.

Rejection here is rejection of fixed-graph random labels. It is not a false positive for that precise random-label null. It would be an error to treat it as a test of independent causal magnitude draws.

At n=0.1 and alpha=0.7, mean S is 40.67 and the central 95% range is about 22 to 64. The observed S=50 falls in this range. This is descriptive only. We do not choose parameters to match it, give a goodness-of-fit probability for it, or infer which source pairs are triggered. Mean pair count is 143.62, compared with 175 observed; other model features were not validated. files/summary.json gives every cell. files/simulations.csv preserves each catalog's aggregate counts, score and p value.

## Limits and use

This test supplies a possible mechanism, not an explanation established for Earth. Source locations are reused and data overlap the prior campaign result. Model values of n, alpha, spatial scale and delay are selected examples, not estimates. A bounded magnitude law, rounded source magnitudes, mixed preferred magnitude scales, source revisions and possible missed events affect calibration. The exponential delay is unlike a full aftershock decay law. The spatial rule omits faults and slab structure. No detection model, uncertainty propagation for b, measurement error, time-varying background or ocean and water forcing is included. Startup and endpoint effects are not removed.

Global and regional shuffles test different conditional nulls. Our result does not invalidate the earlier regional p value or show that its excess is fully due to productivity. It shows why a stronger causal reading needs a fitted process and a detection model. The general distinction was already stated in the prior paper; the finite example is the added evidence. This is a methodological result, not a new discovery of physical magnitude dependence.

## Reproduction

Verify the signed ZIP with sci verify BUNDLE.zip --json before extraction. Use Python with numpy, scipy, pandas and matplotlib. Exact environment versions are in files/environment.json. Use new output paths outside the signed draft:

    python files/analyze.py --source /absolute/path/to/shared/events.csv --out /absolute/path/fresh-run
    python files/audit.py --source /absolute/path/to/shared/events.csv --results /absolute/path/fresh-run --out /absolute/path/fresh-audit.json

The script checks the source hash and creates a new output folder. Compare summary.json and simulations.csv with the bundled files. Figure bytes may vary with the plotting environment. To retrieve a live source, run python files/retrieve.py --scratch /absolute/path/new-external. That script rejects destinations inside the publication. Revised live records cannot replace the fixed snapshot for exact reproduction.

The scalar audit checks source counts and score, all rejection counts, score bounds, and direct-edge integrals. An early timestamp conversion failed a time-span assertion before simulation. The final code converts to explicit nanoseconds. Only corrected outputs are included. A full second run matched summary.json and simulations.csv byte for byte. files/repeat_check.json records their hashes. The output-path guards added after this repeat do not change calculations.

## Campaign record

Job: sci-1107-dell-earth-and-ocean-sciences-933bc122cf99. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, through T3 Code and the Codex harness. Date: 9 November 2026 local time. No agents were launched. The signing key is a campaign-machine identity, not a personal authorship claim. No private key is included. No remote upload or index submission was made.
