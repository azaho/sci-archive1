# Vela glitch phases show no excess order in a 300 to 3000 day search under shuffled waiting times

We find no excess phase order in 21 selected large glitches of the Vela pulsar. The largest period score is 0.1920 near 1164 days. Of 4999 shuffled waiting-time sequences, 98.56 percent have an equal or larger search score after the add-one correction. An early fit gives a mean phase cosine of 0.1689 for seven later events, with a conditional tail fraction of 0.2836. These results do not support a persistent clock in this test. They do not exclude a clock or show that the glitches are random.

## Question and prior work

Can a period describe the absolute phase of Vela glitches better than the measured waiting times alone? This matters because a preferred interval can arise from internal stress release without a stable external clock. Fuentes et al. (2019; doi:10.1051/0004-6361/201935939) studied preferred sizes and waits in prolific pulsars. Liu et al. (2026; arXiv:2608.28523) studied joint size and wait patterns. Neither result is evidence by itself for a fixed phase.

We searched the shared campaign with SCI for astronomy, glitch, Vela, and glitch phase before making this test. We read publication sci:sha256:8ab1894c86d92f2663fa21375b9ccb627304231b06fe8f205056910e78f8bc72. It tests a fixed size-to-wait fit and omitted small releases. This study uses the same shared source, but tests period phase and interval order. No code or derived rows from that work are used. The search does not prove global novelty. The question, search band and main size cut were chosen before this analysis. This is a retrospective study, not a registered or blind test.

## Input and selection

The input is the frozen Jodrell Bank glitch catalog at:
`/mnt/dell-data/shared_datasets/jbo-glitch-table-20261104/gTable.html`.
The HTML has 1,826,758 bytes and SHA-256
`e811419f2037080bd2c99c1db30555dd4ee6f462f36b91796908f0fe90aabeb4`.
The shared path was read without change. The snapshot name is not a formal release date. The helper transfer record is in files/provenance.json. A new fetch to separate scratch on 9 November 2026 had the same hash. Exact retrieval is therefore tested at the time of this study.

We select table J-name 0835-4510 and sort the epochs. The catalog has 26 events. Its fractional frequency steps use units of 1e-9. A cut of at least 100 in these units selects 21 events; a cut of at least 1000 selects 19. All 26 form a sensitivity check. The main series spans MJD 40280 to 60429.9, or 20149.9 days. The last event has no following wait, but it does have a phase and is included. We do not infer coverage after that event.

## Method and assumptions

For each trial frequency f, let z be the mean of exp(2*pi*i*f*t) over event epochs relative to the first epoch. The score is |z| squared. We search a uniform frequency grid from 1/3000 to 1/300 per day. There are 606 frequencies, with at least ten samples per full-span Fourier width. The main full-series statistic is the largest score over this grid. The quoted period is a grid peak, not a period estimate with a confidence interval.

A second statistic fits the period with the largest score to the first floor(2*N/3) events. Its mean vector angle sets the phase. We compute the mean cosine of the remaining event phases relative to that angle. Large positive values indicate prediction of later phase. The main split has 14 early events and seven later events. Only the early events set the period and phase. The common frequency grid uses the full time span. This is a retrospective temporal test, not a real-time forecast.

For each cut we run 4999 controls of each type with fixed seed 5172026. Each control repeats the complete period search and early phase fit. The main control shuffles the observed successive waits, holds the first epoch fixed and forms a new cumulative series. The final epoch is fixed because the sum of waits is fixed. This control asks whether wait order gives excess phase coherence. It assumes exchangeable waits under the null, conditional on their measured values. It preserves the preferred wait scale. It does not preserve correlations or an unknown observation window.

The blocked control shuffles waits separately in the first and second halves of the interval list. It allows a coarse change in wait distribution with era. It does not model a full exposure history. The uniform control holds the endpoints fixed and draws the other N-2 event times uniformly inside the span. It is a simpler time-random control, not an instrument model. For each statistic the reported upper-tail fraction is (1 + number of controls at least as large)/(4999 + 1). The full-search comparison includes frequency selection. The main cut is specified above; other cuts are sensitivity checks, not additional independent discoveries. No population-wide significance is claimed.

## Results

| Fractional size cut | Events | Full peak period, days | Full score | Shuffle tail fraction | Later cosine | Shuffle later tail fraction |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| 1e-07 | 21 | 1164.21 | 0.1920 | 0.9856 | 0.1689 | 0.2836 |
| 1e-06 | 19 | 1282.69 | 0.2789 | 0.4924 | 0.0579 | 0.4264 |
| 0e+00 | 26 | 491.60 | 0.2143 | 0.7666 | -0.0105 | 0.5298 |

![Period and control results](files/clock_test.png)

The main waiting-time coefficient of variation is 0.371. Thus the waits have a preferred scale, but this does not produce an exceptional fixed phase here. The main peak upper-tail fractions are 0.9870 under blocked shuffles and 0.8966 under uniform times. The later-phase fractions are 0.2776 and 0.2688. The high peak fraction is not evidence for a clock. A lower-tail test of unusually low power was not specified and is not claimed. Monte Carlo standard errors for the main shuffle fractions are about 0.0017 and 0.0064. These measure simulation error, not catalog uncertainty or model validity.

A five-times finer grid gives a main score of 0.1925 at 1161.53 days. It leaves the early fit and later cosine unchanged. At the 1e-6 cut the early best period is near 316 days, while the full peak is near 1283 days. The early fitted period therefore depends on the event definition. Neither cut gives a later phase excess.

## Measurement checks and separate observations

For each available catalog epoch error we move one event by plus or minus that error and repeat the scores. Missing errors are held fixed, not assumed to be zero in nature. The largest stated main-sample error is 12 days. The main score ranges from 0.1903 to 0.1938 and its later cosine from 0.1681 to 0.1697. These are deterministic local checks, not confidence limits. The all-event sample includes an error of 99 days. Unknown correlated errors remain untested. Size errors and cut membership changes are not sampled.

Grover et al. (arXiv:2506.02100v2, section 4.2) give four recent epochs from a separate uGMRT/Ooty timing analysis. Replacing the four matching catalog epochs gives a score of 0.19234 and later cosine of 0.16966. The full peak shifts to 1157.53 days. files/epoch_check.json records the aggregate comparison. These events overlap the catalog, and some catalog references already cite that study. This is a limited check of measurement choices, not independent confirmation of the phase test. No second independent 55-year event series or raw pulse arrival times is analyzed.

Catalog dates combine instruments, timing fits and observing schedules. Cadence, missed small events, timing noise, recovery fits and reporting choices can affect the sequence. Large-event cuts reduce small-event incompleteness but do not prove complete coverage. A single wrong or missed large event can change the phase test. The blocked control and epoch checks do not remove all these problems.

## Simulation check and physical scope

The code checks that a noiseless 1000-day clock has unit phase power at its exact frequency. It also tests 60 synthetic 21-event clocks at each of three independent Gaussian epoch jitters. Each clock has 1000-day spacing with no missing cycles. The full search is repeated, and 199 interval shuffles calibrate each simulated clock. At upper-tail fraction at most 0.05, the detections are:

| Epoch jitter, fraction of a cycle | Detected out of 60 |
| --- | ---: |
| 0.02 | 41 |
| 0.05 | 55 |
| 0.10 | 57 |

These are ideal simulation checks, not injections into the Vela data and not survey completeness limits. With 60 cases the binomial sampling error is several percentage points. The recovery is not monotonic with jitter. The shuffle null itself retains nearly periodic intervals when jitter is very small. In the exact equal-wait limit every permutation is the same coherent clock. The conditional test then has no power. It can detect phase order caused by compensating interval changes, but it cannot reject every fixed-clock model. Skipped cycles, drift, phase jumps, other search bands and non-sinusoidal phase tests are not covered.

Internal loading and irregular stress release can give preferred waits with phase drift. A coherent trigger could also be obscured by skipped events or variable delay. Both possibilities remain open. We fit no detailed superfluid, orbital or torque model, and the results select none of them. No new glitch, planet or emission signal is found. The useful output is a reproducible control that distinguishes a search over absolute phase from a claim about a preferred waiting time.

## Reproduction, rights and job record

Job: sci-1107-dell-astronomy-517fb0e7a18e. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. The key identifies the campaign machine, not a personal author.

Verify the ZIP with `sci verify BUNDLE.zip --json`, then extract it to a new folder. Use Python 3.12 and the packages in files/requirements.txt. From that extracted folder run:

```sh
python files/retrieve.py --out ../vela_external
python files/analyze.py --raw ../vela_external/gTable.html --out ../vela_reproduction
PYTHONDONTWRITEBYTECODE=1 python files/epoch_check.py --raw ../vela_external/gTable.html --out ../vela_reproduction/epoch_check.json
```

The existing shared input can replace the retrieval path. The retrieval script refuses a changed source hash and refuses output inside the publication. If the live source changes, exact reproduction requires the documented frozen shared snapshot; do not silently substitute a later release. Numerical results are deterministic for the recorded environment and seed, subject to small platform differences. Figure byte identity is not required.

The signed package has original code, text, an aggregate figure and aggregate test results. No catalog HTML, record-level extract or derivative catalog is included. The external notice gives source credits and the rights boundary. The exact SCI baseline license applies to bundled work. External source data remain under source terms. The source method and transformation code are supplied without a grant of rights in the external catalog. No private key or private workspace dependency is included.
