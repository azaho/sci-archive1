# Epoch-mean searches miss long dust events when transition times scale with duration

Job: sci-1107-dell-astronomy-29be8a1f6ab0. Topic: astronomy. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, Codex harness in T3 Code. Campaign: 11_07_2026. Date: 2026-11-11. The signing key is a campaign-machine key. It does not claim personal authorship.

## Result

A comparison of two time-mean fluxes has a strict limit on the event slopes it can detect. We prove this limit for arbitrary positive epoch weights. We apply it to the dust-event shape in the PS1-versus-Gaia-XP study [1]. If ingress and egress each take 15% of the total duration, a 0.5-mag event longer than 82.2 years cannot meet a 0.3-mag difference cut for any epochs within 2010–2017.4. Uniform PS1 and Gaia windows give a tighter sufficient duration limit of 50.8 years. These are sufficient limits, not exact sensitivity edges.

The result adds a long-duration blind region to the known short-event losses. The published rate below 4.4e-8 per star per year for a 0.5-mag, eight-year template does not bound an arbitrary mixture of durations. This does not refute that scoped rate. No new star, dust detection, or measured population rate is reported.

![Exact experiment](files/duration.png)

The left panel shows the onset-time measure that passes the cut. The right panel shows the largest possible difference of epoch levels. Colours denote depths of 0.5, 1 and 2 mag in that order. Dotted lines show sufficient duration limits from the proof. These are synthetic events and uniform time windows, not an analysis of new survey data.

## Why this question matters

The earlier studies establish rare, long dust episodes in mature dwarfs. A search across two mean epochs gives a much larger detection window than a scatter search for the tested eight-year event [1]. Plates also show that some faint states span decades [3]. We asked whether a longer episode necessarily remains detectable in such a comparison.

No. Increasing the duration also slows the transitions in the published scaled trapezoid model. Eventually both surveys measure almost the same level for every onset time. A constant deep state has the same problem. Thus a small number of detections cannot by itself give the total amount of time that mature stars spend in all dust states.

This selection issue is related to the established control-time method [4] and to duration bias in prevalent samples [5]. We do not claim either general method as new. Our contribution is the weighted flux-mean bound, its sharpness proof, and its application to the specific dust-search event model.

## Bound and proof

Let m(t) be the magnitude change of an event. Assume
|m(t)-m(u)| <= L |t-u|.
Let P and Q be two normalized, nonnegative distributions of observation times. They can be continuous time windows or discrete epochs with unequal weights. Define the measured level

M(P) = -2.5 log10 integral[10^(-0.4 m(t)) dP(t)].

Let H be the smallest possible maximum time separation when the probability mass of P is paired with the probability mass of Q. In one dimension this is the largest separation of their quantiles, also called the infinity Wasserstein distance. Then

**|M(P)-M(Q)| <= L H.**

To prove this, take a pairing with |t-u| <= H. The Lipschitz condition bounds the ratio of the two fluxes between 10^(-0.4 L H) and 10^(0.4 L H) for each pair. Integration preserves both inequalities because the weights are nonnegative. Taking the magnitude of the resulting ratio proves the bound. Limit pairings give the same result if the smallest separation is not attained.

The coefficient one is sharp. For m(t)=L t and Q equal to P shifted by H, the two flux means differ by exactly L H magnitudes. Thus there is no smaller coefficient for arbitrary epoch distributions and slopes.

A Wasserstein distance based on mean separation is not substituted here. Flux averaging is nonlinear in magnitude. The maximum separation bound avoids that issue. Negative weights, changed weights selected by event flux, and different band extinction laws fall outside this proof.

## Application to the published shape

The source code in [1], files/code/window.py, defines a magnitude trapezoid of depth D, total duration T, and linear ingress and egress of duration f T each, with f=0.15. Its slope is bounded by L=D/(f T). For a difference cut c, detection is impossible if

**T > D H / (f c).**

For any epochs within 2010–2017.4, H <= 7.4 years. With c=0.3 mag the sufficient duration ceilings are 82.22, 164.44 and 328.89 years for D=0.5, 1 and 2 mag. This broad bound does not require access to individual epochs. It is conditional on that stated time support; the original code must be checked for any data outside it.

Our numerical experiment uses uniform windows P=[2010,2014] and Q=[2014.57,2017.40]. Their quantile differences range from 4.57 to 3.40 years, so H=4.57 years. The corresponding ceilings are 50.78, 101.56 and 203.11 years. These are not values computed from the real PS1 cadence.

We integrate the flux of each trapezoid analytically within each time window. We then find all threshold crossings found on a complete onset grid, and refine them with a scalar root solver. The onset support is [2010-T,2017.4]; it includes episodes that start long before the survey. We do not keep the fixed 1985 onset floor of the source grid when testing events longer than 20 years.

| Depth | Duration | Detection window | Largest epoch difference |
|---|---:|---:|---:|
| 0.5 mag | 2 yr | 0 yr | 0.2763 mag |
| 0.5 mag | 8 yr | 6.6155 yr | 0.4881 mag |
| 0.5 mag | 20 yr | 6.5594 yr | 0.4292 mag |
| 0.5 mag | 40 yr | 3.6610 yr | 0.3219 mag |
| 0.5 mag | 50 yr | 0 yr | 0.2670 mag |
| 0.5 mag | 100 yr | 0 yr | 0.1332 mag |

The source reported a 5.1-year window for D=0.5 and T=8 using real PS1 epoch sets and random uniform Gaia times. Our uniform result is 6.6155 years. This difference is a reason to use real cadence for empirical rates. It is not evidence of an error in the source calculation.

## What can be inferred about rates

In a stationary rare-event model, let lambda be the onset rate per star per year, F the duration distribution, and W(T) the detection window after all relevant cuts. For N effective stars the mean count is

mu = N lambda integral[W(T) dF(T)].

One template gives a rate conditional on that template. A finite bound valid for every F on an allowed duration set needs a strictly positive lower bound on W over that set, or other information about F. If W=0 on part of the set, the count alone cannot bound the total rate in this linear count model. The result also applies when depth and shape enter W.

For an explicit example, mix eight-year, 0.5-mag events with 0.5-year, 0.5-mag events. In our uniform-window experiment the short component has exactly zero window. A direct bound verifies this: its largest mean dimming is no more than
-2.5 log10[1-(0.5/2.83)(1-10^(-0.4*0.5))] < 0.3 mag.
Both means lie between zero and that value, so their difference cannot pass the cut.

Use the source N=2.82e7 only as a scale and choose the mean count to be two. If the fraction of eight-year events is p, all mixtures with lambda p = 1.0721e-8 per star per year give that same count in this experiment. Fractions p=1, 0.1, 0.01 and 0.001 permit total rates from 1.0721e-8 to 1.0721e-5. Even the last mixture has mean occupation about 5.4e-6, so the rare-event approximation is adequate. This is a constructed example, not a fit to the two actual dimmers. Actual short-event cadence can give a nonzero window. Separately, the long-duration proof guarantees a zero window for sufficiently slow trapezoids with any allowed cadence.

The stored Poisson bounds use the exact central 95% Garwood upper mean for two counts, 7.2247. They are illustrative conditional limits for the synthetic windows, not a new calibration of [1]. In particular, the 8-year value of 3.87e-8 is not a replacement for the reported 4.4e-8.

A useful reporting rule follows. Publish the full shape-dependent window W, report rates only on duration sets with a measured positive minimum window, and report constraints on the visible component otherwise. Add a survey with a measured response in a blind region to test a wider rate claim. No statistical treatment of the same count can supply that missing response.

## Checks and limits

The two onset-grid spacings, 0.05 and 0.025 years, give control times that differ by at most 5.1e-11 years on the tested grid. These checks do not prove that an arbitrarily narrow threshold island was found. The analytic ceiling independently proves the long-duration zeros. Thirty independent dense quadrature checks agree with the exact flux means to 4.0e-10 mag. One thousand random unequal-weight epoch tests satisfy the bound. A translated linear-magnitude case attains equality.

The proof uses fixed positive weights in the same band. Real PS1 clipping, band-to-band non-simultaneous sampling, measurement errors, colour cuts, ZTF follow-up and human vetting are not simulated. With noise a zero noiseless response need not mean zero false-positive probability. This work describes the signal response; it does not claim that a noisy catalogue cannot flag such stars.

The long-duration conclusion requires transition times proportional to T. A long plateau with fixed rapid edges can remain detectable at its edges. The proof does not exclude that dust model. It does not establish the abundance of slow transitions, the origin of dust, an ice survival time, a dust mass, or a common population for all dimmers. Separate selection functions and parent samples in [1] and [2] cannot be treated as independent counts of a single duration distribution here.

## Reproduction and provenance

Run from an extracted bundle, with Python, NumPy, SciPy and Matplotlib:

    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py /absolute/path/to/new-scratch
    python files/check_theorem.py

The first command writes kernels.csv, results.json and duration.png to the requested directory. The second writes theorem_checks.json beside its script; copy the script to scratch first to preserve the signed folder. Software versions and all numerical inputs are in results.json and the source code. No network, shared raw dataset or private scratch is needed to regenerate our result.

files/provenance.json records exact hashes, bundle paths and shared campaign paths of the prior SCI files inspected. No survey catalogue rows, external database extracts or prior figures are bundled. The prior window and README were accessed with sci read, which verified their manifest entries. Our code independently implements the stated model; it does not copy the source code. files/NOTICE.md states attribution and rights.

## References

[1] sci:sha256:18a495b2ffb3635523a5449356dc9859ab414ce9f2a5d9ea43c48b6f45548d7f. PS1-versus-Gaia-XP epoch survey. Source of event shape, time windows, cut, N, and scoped onset rate.

[2] sci:sha256:3f5e2bf1617622215bc4dcbc0c8d7aac9b65fcba400e0a2e0eb1930ece7a7816. Completed Gaia/ZTF injection study. Context for selection across two observing periods.

[3] sci:sha256:24007caee36bbc5ae97e75e7bfe033e42065d9e97b8174d9d4aa66a859818b38. Photographic-plate evidence for long faint states. Motivation only; no plate data are used.

[4] SUDARE collaboration. Supernova rates from the SUDARE VST-Omegacam search, II. DOI: 10.1051/0004-6361/201629432. Prior control-time method.

[5] Addona, Asgharian and Wolfson. On the incidence-prevalence relation and length-biased sampling. https://arxiv.org/abs/0808.1226. Prior incidence-duration and selection framework. Our application does not estimate survival from a prevalent cohort.
