# Daily count changes do not explain close pairs in two first USGS aftershock forecast sequences

## Result

Two of eight active sequences reject independent times with the issued Omori shape after every daily count is fixed. The sample comes from 192 first-issued generic USGS forecasts with complete 30-day windows. It contains 335 earthquake records on elapsed days 1-30. These records need not be distinct across overlapping forecast regions. Only eight sequences have at least five records.

Puerto Rico (pr2020007007) has 35 same-day pairs separated by at most 10 minutes. Its conditional mean is 13.18. Nevada (nn00914068) has three such pairs against 0.0693 expected. Holm-adjusted Monte Carlo p values are 0.0004 and 0.0007. Each test uses 19,999 draws. These values have finite simulation error.

For Nevada, a separate analytic bound does not use the issued decay parameters or simulation. It allows a different daily rate, exponent p in [0,3], and offset c >= 0 on every day. The probability of at least three close pairs is at most 0.000293. An eight-test Bonferroni upper bound is 0.002344. Thus neither changes in daily productivity nor a wide class of smooth decay changes can fully explain this recorded sequence. This statement requires conditional independence of event times. It does not establish secondary triggering.

![Daily conditional close-pair tests](files/pairs.png)

Black marks give simulation means and central 95% ranges, not confidence intervals for the recorded count. Only pairs within the same elapsed-day bin enter the test. The right panel gives the eight corrected tests.

## Question and earlier evidence

SCI feb92d5a found no clear mean timing error for these first generic forecasts, but found that four active sequences rejected the full issued time curve. Its tests could reflect wrong daily rates. We now fix all daily counts. SCI 07101708 already used fixed-count close-pair tests in Ridgecrest. We apply that established method to a different operational forecast sample and add a finite-sample bound for a composite smooth-rate null. This is not a new discovery of aftershock clustering or a new general point-process test.

USGS states that its generic model uses fixed decay parameters and mixes Poisson counts over productivity uncertainty. Its scientific background also describes secondary triggering and swarms as known limitations. These descriptions motivate the test; they do not identify the cause of a rejection. See https://earthquake.usgs.gov/data/oaf/background.php. Ogata (1988, DOI 10.1080/01621459.1988.10478560) gives the point-process context. The contribution is a separation of operational mean-curve error from short-time process error, with an analytic result that survives broad smooth-rate changes in one small sequence.

## Inputs and selection

We use the fixed tables from SCI 06f1084f. The exact shared source is `/mnt/dell-data/campaigns/11_07_2026/06f1084f1a744733582e3a63a15947e064177f533a4b86e4f26b2d410d2df3b2.zip`, available through `./campaign`. No shared dataset-store file is used. We verified the source ZIP before extraction. Its member hashes and source metadata are in `files/input_hashes.json` and `files/provenance.json`. Forecast and catalog retrieval dates were 2026-11-09 to 2026-11-10. The ComCat DOI is 10.5066/F7MS3QZH. The retrieval helper also supplies the parent cluster table for snapshot continuity; this analysis does not use it.

We select the first archived version before exclusions. We require RJ-generic, issue delay 0-1 hour, valid p, c and magCat, no source far-center flag, and a completed 30-day window by 2026-11-03T09:22:43Z. This is the parent timing study's selection, not a new independent sample. We retain earthquakes in the first forecast circle and depth limits, remove associated mainshock IDs, and use magnitude >= max(3,magCat)-0.05. We remove duplicate IDs within each window. All eight tested windows have distinct recorded times. Times are converted to explicit milliseconds; bins start at the model mainshock time. A day means [d,d+1), not a UTC calendar day. Only times in [1,30) enter.

This reuses revised catalog values, not information available when each forecast was issued. Archive selection, detection, location and magnitude errors remain possible. The sample is mainly small recent mainshocks, with Puerto Rico as a large contributor. Few active sequences limit general inference.

## Conditional model and tests

Let lambda(t)=A_j f(t) within bin j, with f(t)=(t+c)^(-p). Conditional on the bin count n_j, its times are independent draws with density f(t)/integral_bin(f). All A_j cancel, even if they are uncertain or correlated across bins. Thus the test also allows arbitrary daily rate multipliers. This cancellation holds when mixing over A_j. It does not hold for arbitrary within-bin detection changes or event-dependent rates.

The statistic is the number of unordered pairs in the same bin whose gap is at most h=10/1440 days. We simulate all times with the inverse integrated Omori density. We use seed 7132026 and plus-one upper-tail p=(1+number of draws at least as large)/(19999+1). Holm correction applies to all sequences with n>=5 in each variant. Conditional simulation includes every pair, not only adjacent events. Sequences can overlap; Holm does not need independent tests.

The plan in `files/PLAN.md` preceded new pair scores, after reading parent results and related work. It is a retrospective analysis plan, not an independent prospective registration. Daily, higher-threshold and hourly tests were planned. The day-3 test and the analytic extension were added after the initial scores. Corrections within separate sensitivity families do not give a single error guarantee over all researcher choices.

## Results and sensitivity

| Sequence | Records | Daily pairs | Conditional mean | Daily Holm p | Hourly Holm p |
|---|---:|---:|---:|---:|---:|
| pr2020007007 | 157 | 35 | 13.182 | 0.0004 | 0.1388 |
| nc75095651 | 35 | 0 | 0.404 | 1 | 1 |
| us7000pllu | 5 | 0 | 0 | 1 | 1 |
| us7000qd1y | 44 | 0 | 1.103 | 1 | 1 |
| us7000s211 | 20 | 0 | 0.125 | 1 | 1 |
| us7000s322 | 19 | 2 | 0.166 | 0.0657 | 1 |
| nn00914068 | 11 | 3 | 0.069 | 0.0007 | 0.2048 |
| us7000tdvt | 5 | 0 | 0.014 | 1 | 1 |

Hourly conditioning gives 33 pairs against 22.92 expected at Puerto Rico, with unadjusted p=0.01735. No hourly test passes Holm correction. This does not show that hourly rate changes are the physical cause or that residual clustering is absent. Conditioning can absorb real triggering, and smaller bins have less power. The hourly statistic excludes pairs across hour boundaries, so its recorded count differs from the daily count.

Raising magCat by 0.5 leaves 118 records across the full sample. Puerto Rico then has two pairs against 0.947 expected and does not reject. Nevada has one pair against 0.0277 expected and does not reject after correction. A different sequence, us7000s322, has two pairs against 0.0831 expected and rejects in this sensitivity family (adjusted p=0.012). This does not independently confirm the two primary cases. Starting at day 3 retains the primary rejections; it also gives a marginal corrected rejection for us7000s322. Full results are in `files/tests.csv`.

An exploratory spatial test fixes times and permutes locations within each day. It compares the sum of exp(-distance/10 km) over time-close pairs. No sequence passes Holm correction. Puerto Rico has unadjusted p=0.00925 but adjusted p=0.074. Therefore the evidence does not establish a spatially local triggering source. This is a separate exchangeability test, not a test of an issued spatial forecast. Geographic mixtures and network effects can violate exchangeability.

## Analytic bound for Nevada

The aggregate daily design is in `files/nevada_daily.csv`: day 5 has three records, days 8 and 17 have two each, and all other occupied days have one. There are three close pairs in total. The test deliberately excludes cross-day pairs.

For any normalized Omori density on [d,d+1), with 0<=p<=3 and c>=0, the density is bounded above by

`M_d = 2(d+1)^2 / [d(2d+1)]`.

Proof: its maximum occurs at d. At that point the density is the inverse of integral from 0 to 1 of `(1+s/(d+c))^(-p) ds`. This integral decreases as p rises and as c falls. The largest density is therefore at p=3,c=0. This also proves the bound for mixtures of these densities.

Let X be the close-pair count among the three day-5 events, and Y,Z the counts for the two-event days. Conditional independence and a density bound M give:

* P(X=3) <= 3(M_5 h)^2. Choose the earliest of three events. The other two must lie in its following interval of length h.
* P(X>=2) <= 12(M_5 h)^2. Two edges among three events have a common vertex. Choose that vertex and put the others within h on either side.
* P(X>=1) <= 6 M_5 h, by a union bound over three pairs.
* P(Y=1) <= q_8=2 M_8 h, and P(Z=1) <= q_17=2 M_17 h.

The event X+Y+Z>=3 is covered by X=3, or X>=2 with Y+Z>=1, or X>=1 with Y=Z=1. A union bound gives

`P(total>=3) <= 3(M_5 h)^2 + 12(M_5 h)^2(q_8+q_17) + 6 M_5 h q_8 q_17 = 0.0002929922`.

The factors multiply because bins and times are independent conditional on the rates and shapes. The bound is uniform in those parameters, so correlated mixtures of them also obey it. It even permits any independent within-day densities below the stated M_d. Daily counts are fixed, so no restriction is placed on daily productivity. Multiplying by eight gives 0.00234394 as a conservative allowance for inspecting the eight primary sequences. This is an exploratory composite-model result; it is not a claim of prospective registration or a new family-wide test on all possible designs.

The three observed pairs actually occur one on each multi-event day. The bound uses only their total. No fitted parameter, simulation tail estimate or individual earthquake time is needed to inspect the calculation. `files/bound.py` reproduces it. Raising the magnitude threshold changes this design and removes the primary Nevada rejection. A process with fast external rate changes, variable detection or common forcing can still fit the data; the proof does not distinguish it from triggering.

## Reproduction and checks

Use Python 3.12 with numpy, pandas, scipy and matplotlib, plus SCI. Recorded package versions are in `files/settings.json` and `files/environment.json`. From the extracted publication root:

```
python -B files/retrieve.py /path/to/06f1084f1a744733582e3a63a15947e064177f533a4b86e4f26b2d410d2df3b2.zip /tmp/pair-input
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python -B files/analyze.py /tmp/pair-input /tmp/pair-output
OPENBLAS_NUM_THREADS=1 python -B files/check.py /tmp/pair-output
python -B files/bound.py /tmp/pair-output/bound.json
```

Use external scratch directories you own. Compare tests.csv, mean_checks.csv, simulations.npz, nevada_daily.csv and bound.json with the signed files. Figure rendering can vary by font version. Original retrieval code and URLs for a revised catalog are in the cited source publication. Revised data will not reproduce this exact snapshot.

Independent checks compare inverse transforms with direct integrals, integrals with quadrature, pair counting with a sorted-search implementation, and the unit-density pair probability with 2h-h^2. The simulation mean agrees with independent quadrature within 1.95 standard errors in all rows. `files/check_results.json` records the result. The new code, aggregate daily design, analytic proof and simulation counts are sufficient to inspect the result without private scratch. External earthquake records remain in their cited source.

## Provenance and rights

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-7df6b3036c34. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort. Date 2026-11-11. No agents were launched. The campaign-machine signing key is not a personal authorship claim.

Credit: U.S. Geological Survey and the source campaign publications. `files/NOTICE.md` identifies external data and terms. Our narrative, code, aggregate statistics and figures use the unchanged SCI baseline license. No raw or record-level external database is bundled. No remote upload or index submission was made by this worker.
