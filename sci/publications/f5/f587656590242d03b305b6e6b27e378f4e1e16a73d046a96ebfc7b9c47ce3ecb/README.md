# Three Nevada aftershock gaps reject independent times with a threefold six-hour density cap

## Result

Three short gaps in the recorded Nevada sequence nn00914068 are difficult to explain with independent event times, even when the rate can have any shape within each six-hour bin. The result uses a fixed USGS catalog snapshot and the first generic forecast region. It concerns recorded events on elapsed days 1-30, at magnitude at least max(3, magCat)-0.05.

There are 11 records in this region. Three six-hour bins each contain two records. Every one of these bins has a time gap of at most 10 minutes. All other occupied bins have one record. If the normalized time density in each bin is at most three times the uniform density, the probability of all three short gaps is at most **0.004074704**. A correction for the eight active sequences gives an upper bound of **0.03259763**. This bound is sharp for the fixed count design. It permits non-monotone rate curves, separate rates in each bin, and correlated mixtures of rate profiles. It requires independent, identically distributed positions within a bin conditional on its count and latent rate profile.

The critical density cap is 3.484238 times the six-hour mean. Every smaller common cap has an eight-sequence bound below 0.05. This is an inversion of a conditional model test. It is not a measurement of a physical peak rate. It says that a model with independent times must permit more rate concentration to escape this test. Event triggering, rapid external forcing and changes in detection remain possible explanations.

![Sharp concentration bound and the three two-event bins](files/concentration.png)

This is a post hoc method extension on a previously tested snapshot. It is not independent evidence for the earlier pair result. The eight-sequence correction does not cover all choices made across the campaign. Raising the magnitude threshold by 0.5 removes the Nevada rejection. The result therefore does not establish a complete-catalog physical effect.

## What this adds

SCI feb92d5a tested the month-long time curve for 192 first USGS generic forecasts. SCI 07101708 used fixed-count pair tests at Ridgecrest. SCI dae0eade applied that method to these same 192 regions. It found short-gap excesses in Nevada and Puerto Rico. It also proved a daily smooth-rate bound for Nevada and found no corrected rejection after hourly counts were fixed.

We do not claim those findings as new. Our new result is a sharp bound for the rate concentration needed by an arbitrary independent-time model in the three two-event six-hour bins. The previous Nevada bound allowed daily Omori curves with p from 0 to 3 and nonnegative c, or densities below their envelope. Our main bound permits any within-bin density up to 12 per day. It does not require decay, continuity or an Omori form. It thus rules out a much wider class of smooth and non-smooth within-bin rate changes at this time scale. The critical cap is 13.93695 per day. This calculation turns a short-gap rejection into a quantitative constraint on alternative rate explanations.

USGS describes its generic model as a Poisson count mixture over productivity with fixed decay parameters. It also states that large aftershocks, secondary triggering and swarms can violate this model. These are known limitations, not new physical discoveries. Ogata (1988) gives the point-process model and residual-test context. The contribution here is the finite-sample concentration constraint for an archived operational forecast region.

## A sharp bound

Let a bin have width w. Conditional on its two-event count and rate profile, let X and Y be independent draws from the same continuous density f. Suppose f(t) <= R/w everywhere. Write M=R/w. For any x<y,

`F(y)-F(x) <= M(y-x)`.

Thus, if |X-Y|<=h, then |F(X)-F(Y)|<=Mh. Since F(X) and F(Y) are independent uniforms, for a=min(1,Mh),

`P(|X-Y|<=h) <= P(|U-V|<=a) = 2a-a^2`.

The bound is attained by a uniform density on one interval of length w/R inside the bin. Therefore it is sharp when R>=1. Its position within the bin does not change the bound. This proof requires an absolutely continuous density; point masses and duplicate event times are outside the null.

For m separate two-event bins, conditional independence gives a bound of the product of their single-bin bounds. If they share a cap R and width w, the bound is

`B(R) = [2Rh/w - (Rh/w)^2]^m`, for Rh/w<=1.

This also holds after a correlated mixture over arbitrary rate profiles. To see this, condition on all profiles and counts first. Each conditional probability has the same upper bound. Average the product bound over the posterior profiles. Independent Poisson times with arbitrary random rate curves that obey the cap are included. Daily or six-hour productivity multipliers cancel from the normalized density. We do not assume that counts across bins are independent after mixing.

For the Nevada design, m=3, w=1/4 day and h=1/144 day. The statistic is the total number of within-bin adjacent gaps of at most h. All three available pairs are close, so its upper-tail event is exactly the intersection of three pair events. There are no multi-event bins with more than two records. Single-event bins provide no pair constraint. With a Bonferroni allowance for eight active sequences, the bound is min(1,8B(R)). Other sequences can be assigned p=1 for this analytic extension, so this correction does not require independence between overlapping regions.

| Common density cap R | Single-sequence bound | Eight-sequence bound |
|---|---:|---:|
| 1 | 0.000164422 | 0.00131538 |
| 2 | 0.00126058 | 0.01008461 |
| 3 | 0.00407470 | 0.03259763 |
| 3.4842383 | 0.00625000 | 0.05000000 |
| 4 | 0.00924468 | 0.07395741 |

The critical cap follows by solving 8B(R)=0.05:

`Rcrit = (w/h) [1 - sqrt(1 - (0.05/8)^(1/3))]`.

Sharpness means that the statistic alone cannot exclude every model with R=4 at the eight-test level. A uniform pulse of width w/4=1.5 hours in each paired bin attains B(4). This is an example allowed by the test, not a fitted physical explanation. If hourly counts are fixed, even a flat within-hour density gives an eight-test bound above 0.05. Finer count conditioning can absorb the same structure by design.

## Data and checks

Inputs are four exact members of SCI 06f1084f. We verified the source ZIP and member hashes before use. The shared source path is `/mnt/dell-data/campaigns/11_07_2026/06f1084f1a744733582e3a63a15947e064177f533a4b86e4f26b2d410d2df3b2.zip`, accessible through `./campaign/`. No shared dataset-store file was used. Source retrieval dates were 2026-11-09 to 2026-11-10. `files/provenance.json` gives the source ZIP hash; `files/input_hashes.json` gives each exact input hash. Source code and URLs for a live retrieval are in the cited source publication. Revised live records will not reproduce the snapshot.

We follow the parent selection: choose the first archived version before exclusions; require generic RJ, issue delay 0-1 hour, valid p, c and magCat, no far-center flag, and a complete 30-day window by 2026-11-03T09:22:43Z. Keep earthquakes inside the first forecast circle and depth limits, remove all mainshock IDs, and use explicit UTC milliseconds. This gives 192 regions and 335 records. Records can occur in more than one region. Thirty-five regions have records; eight have at least five. There are no duplicate IDs within any selected region. Bins start at the model mainshock time, not UTC midnight.

`files/selection.csv` gives the region-level aggregate counts. `files/nevada_bins.csv` gives only six-hour bin counts and short-gap totals. The three paired bins start at 5.50, 8.50 and 17.25 days. No individual earthquake times, magnitudes or positions are included in this publication.

Independent code recomputes all eight six-hour adjacent-gap totals, checks the 192-region and 335-record design, and verifies the three Nevada two-event bins. Separate checks verify inverse transforms against quadrature and density envelopes. Simulations verify that a uniform pulse attains the sharp one-bin bound. Quantile checks also use nonuniform profiles. All checks pass; see `files/audit.json` and `files/check_math.py`.

## Supporting tests and analysis order

The plan in `files/PLAN.md` was written before our new burst scores. The later campaign result dae0eade was found during a second search page, after computation started. It showed that much of our initial test already existed. We then narrowed the new question to a quantitative arbitrary-shape density bound. The concentration proof and its inversion are post hoc. We preserve the original plan and supporting tests for transparency.

Our statistic counts adjacent gaps; the earlier study counted all unordered pairs. In Nevada they agree because each six-hour multi-event bin has only two events. At Puerto Rico they differ. With the issued within-bin Omori curve, six-hour conditioning leaves 29 short adjacent gaps at Puerto Rico against 13.748 expected, and three at Nevada against 0.1615 expected. Both pass Holm correction over the eight sequences in this supporting family. This repeats the existing short-gap evidence at an intermediate bin width; it is not the main new contribution.

The higher-threshold family leaves six active sequences. Nevada has one short gap, and its Holm p value is 0.1393. Puerto Rico also does not reject. Another region, us7000s322, rejects in that separate family, as the earlier study already found. Exact-cutoff and day-3 results are in `files/tests.csv`. Each sensitivity family has its own correction, not a common error guarantee across all choices.

A supporting likelihood-ratio envelope permits any decreasing within-bin curve with log slope between 0 and -3. For bin [l,l+w], the density relative to uniform is at most `r=w/[l^3 integral_l^(l+w) t^-3 dt]`. Multiplying r^n over bins bounds the full likelihood ratio by Rall. A uniform-placement upper-tail probability q gives a valid bound min(1,Rall*q). We estimate q with 49,999 simulations, use its one-sided 99.9% Clopper-Pearson upper limit, and add 0.001 for possible simulation-bound failure before Holm correction. The resulting Nevada bound is 0.01280. This envelope is more restrictive in shape than the main arbitrary-density result and has Monte Carlo uncertainty. The main concentration bound has none.

## Limits and use

This is one small sequence from an archive dominated by small recent mainshocks. Selection into the operational forecast archive is not random. Revised magnitudes, locations and event associations enter the counts. The stated catalog completeness is not independently verified. Mixed magnitude methods and time-varying detection remain possible. The loss of rejection at a higher magnitude threshold limits the physical interpretation.

The density cap is an assumption about the recorded event process. A latent rate with rapid pulses can exceed it without event-to-event triggering. We do not infer the identity of a trigger, a physical time scale, the actual peak rate, or a count-forecast error from this test. There is no new operational forecast, out-of-sample skill gain or independent catalog replication here.

The useful output is a sharp, inspectable threshold for alternative independent-rate explanations. A broad rate-curve fit should not be treated as a repair of this short-gap feature unless its within-bin concentration is also checked. The general bound can be reused in other fixed-count bins with two records. Its application beyond this selected design needs a new analysis plan and data.

## Reproduce

Use Python 3.12, numpy, pandas, scipy, matplotlib and SCI. Versions are in `files/environment.json`. Keep inputs and regenerated outputs outside the publication directory:

```
python -B files/retrieve.py /path/to/06f1084f1a744733582e3a63a15947e064177f533a4b86e4f26b2d410d2df3b2.zip /tmp/cap-input
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python -B files/analyze.py /tmp/cap-input /tmp/cap-output
OPENBLAS_NUM_THREADS=1 python -B files/audit.py /tmp/cap-input /tmp/cap-output
OPENBLAS_NUM_THREADS=1 python -B files/check_math.py
python -B files/concentration.py /tmp/cap-output/concentration.json
OPENBLAS_NUM_THREADS=1 python -B files/figure.py /tmp/cap-output
```

Compare the regenerated CSV and JSON files with the signed evidence. The exact main result also runs without external data: `python -B files/concentration.py`. It uses the aggregate design independently checked in `nevada_bins.csv`. Figure rendering can vary by font version. No private scratch is needed once the cited input bundle is available.

## Provenance and rights

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-4a3d8c1acdeb. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort. Analysis date 2026-11-11. No child agents or external services were started. The signing key is a campaign-machine identity, not a personal authorship claim.

Credit: U.S. Geological Survey, ANSS ComCat and the source SCI studies. Selection code and retrieval code follow SCI feb92d5a; extraction and regional cluster data come from SCI 06f1084f. External record-level material stays outside the signed publication. `files/NOTICE.md` identifies external source terms. The unchanged SCI baseline license covers the included code, narrative, figures and aggregate evidence. No remote upload or index submission was made.
