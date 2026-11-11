# Phase matching selects background dips in shear tests on 126 TESS CPV visits

Job: sci-1107-dell-astronomy-aa5942b5a6d1. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-11. One finite automated worker did this study. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question

Does a track near the phase of an added shearing clump identify that clump? Can the widths of such tracks set an upper limit on the radial spread of that clump?

The distinction matters for the physical nature and life of complex periodic variable (CPV) material. A recent study measured dip drift and little width growth. It used the final full width at half prominence W and the elapsed rotations N to set q_bound = W/(1.5 N). Here q is the full radial spread divided by the corotation radius. The result is useful for a single identified clump whose profile traces its angular extent. It does not by itself identify which material makes a minimum in a light curve with several dips.

We test the recovery rule from that study: select tracks with at least five windows, then choose the track whose mean phase is nearest the added clump, if the distance is below 0.03 cycles. The test includes zero-signal trials. It also uses the known added signal to measure how much of the local curvature it supplies. The contribution is a calibration of source identity in dip tracking, with controls for dilution and background confusion. It is not a new measurement of a CPV material lifetime.

## Prior work

Bouma et al. (2024, doi:10.3847/1538-3881/ad0c4c) measured changing CPV dips and noted that a period search loses dips when their periods differ from the broad modulation. Bouma et al. (2026, arXiv:2609.00136) studied gas and dust evidence. Campaign study f5392474 measured the drift and life of tracked minima in 443 TESS curves. Its shear calibration gave 118 phase matches from 265 visits and significant width growth in 42% of those matches. Its limitations note confusion with other dips and a finite width resolution. Study a01f5abf tested harmonic phases under symmetric smearing; it did not test source identity in dip recovery. This work tests that separate issue. It does not repeat those studies' population age tests.

## Inputs and rights

We use only the verified SCI publication `sci:sha256:f539247412c4c5c3248b0a1472c0fdb86d1fb83e3ae8af30a14fdfe6c81a36f2`. The exact shared path is `/mnt/dell-data/campaigns/11_07_2026/f539247412c4c5c3248b0a1472c0fdb86d1fb83e3ae8af30a14fdfe6c81a36f2.zip`, reached through `./campaign`. The input entries are `files/data/windows_real.parquet`, `files/data/visits_real.csv`, `files/data/tracks_all_real.csv`, and `files/code/cpvtrack.py`. The last supplies the original detector and linker. `files/provenance.json` and `files/coverage.json` give the ZIP and entry hashes. No new raw dataset download is needed. No raw TESS files, Gaia records or third-party database extracts are bundled.

The source uses TESS SPOC data from MAST and releases these coefficients under its exact SCI baseline license. Its code uses the MIT part of that license. The input code and coefficients remain in separate scratch during reproduction. Our simulation records, summaries, code and figures are compatible with the SCI baseline. See `files/EXTERNAL_DATA.md` for attribution. TESS mission data were obtained from MAST by the source study. We acknowledge TESS (Ricker et al. 2015) and MAST.

## Test design

We select every source visit with tspan/P at least 80 rotations. Each trial uses its actual window times, period, model-noise threshold and 15 complex harmonic coefficients. The 15-harmonic representation is the object being tested. We do not change periods, detrend cadences, or add new cadence noise.

For each visit, use two random phases from a fixed seed that depends on the TIC and visit. At each phase use initial depth D equal to 0.5 or 2 times the median visit peak-to-peak amplitude A. These are depths before the harmonic truncation. The initial Gaussian width is sigma = 0.010 cycles, as in the source shear calibration. The full fractional radial spreads are q = 0, 0.0004, 0.002 and 0.01. Add a zero-signal sham at each phase. The sham is repeated in the table for each depth for paired comparisons; those duplicate controls are not independent trials.

The thin, optically thin, linear-shear approximation gives a uniform angular arc of full length L = 1.5 q N, where N is the number of rotations after the first window center. Conserve the area of the dip. For harmonic k the added coefficient is

`a_k(N) = -2 D sqrt(2 pi) sigma exp(-2 pi^2 sigma^2 k^2) exp(-2 pi i k phi0) sinc(k L)`.

Here sinc(z) = sin(pi z)/(pi z). This is the exact Fourier coefficient of a periodic Gaussian convolved with a uniform arc. It includes wrapping for L greater than one cycle. The zero harmonic is omitted because an additive constant does not change minima, prominence or width in this detector. We evaluate each window at its center. We do not average shear within a window.

Use two backgrounds: the real time-dependent published coefficients, and a flat background. Flat trials keep the empirical noise threshold. They have no extra random noise. These controls isolate threshold loss from the effect of existing CPV structure. They are not new synthetic cadence observations. The real background already contains estimation error and any physical variations in the source windows.

We run the exact source detector (2,000 phase points, 5% relative prominence cut and 4-noise absolute cut), and its greedy linker (0.04 cycle jump, one missing window allowed). We use the phase recovery rule described above. Width slopes and errors use ordinary least squares, as in the source. A long, strong match has at least 80 rotations between its first and last measurements and median prominence at least eight times the visit median model noise. Its q_bound uses the mean width in its last three windows.

### Exact sham probability

We also compute the exact probability for a uniform sham phase, using the published tracks with at least five windows in each eligible visit. Each track covers a phase interval of length 0.06 cycles for the recovery rule. We split intervals that cross phase zero, merge all overlapping intervals, and sum the union length. This is the exact random-phase match probability conditional on that visit. It does not need random trials. Its average across 126 visits in 60 stars is 0.1834, with a 95% star-bootstrap interval of 0.1464 to 0.2228 (1,000 draws, seed 921). The interval describes the selected-visit average.

### Known-signal check

For every minimum in a phase-matched track, compute its positive second derivative C_total and the contribution C_add from the added signal. Both are exact derivatives of the harmonic series at the measured phase. Mark the minimum as added-signal dominated if C_add > 0.5 C_total and C_add > 0. A track passes the curvature rule if at least 80% of its minima pass this check. This rule can be used in injections, since the added profile is known. It cannot identify material in an observed star on its own. The 50% and 80% cuts define a diagnostic; they are not an optimized physical classifier.

A minimum can stay close to phi0 while most of its curvature comes from the pre-existing background. Such a track is a phase match, but it does not recover the added clump's width. We report these rates separately. A bound below the known input q is called an under-bound. We also report a more severe failure: q_bound < q/2. This factor-of-two cut separates large errors from small effects of finite harmonics and averaging the last three widths. Neither label is a confidence-interval coverage statement.

## Results

We ran 5,040 trials on 126 visits in 60 stars. Each row below has 252 trials (126 visits and two phases). Counts are finite-sample calibration results. The repeated sham row is shown only once.

| Real background: depth / A | Input q | Phase matches | Curvature-rule matches | Long, strong matches | Long matches with q_bound < q/2 |
|---|---:|---:|---:|---:|---:|
| zero-signal sham | none | 41 | 0 | 8 | not applicable |
| 0.5 | 0 | 229 | 216 | 123 | 0 |
| 0.5 | 0.0004 | 212 | 168 | 86 | 5 |
| 0.5 | 0.002 | 155 | 94 | 12 | 12 |
| 0.5 | 0.01 | 52 | 3 | 8 | 8 |
| 2 | 0 | 252 | 252 | 242 | 0 |
| 2 | 0.0004 | 252 | 235 | 241 | 16 |
| 2 | 0.002 | 211 | 150 | 27 | 26 |
| 2 | 0.01 | 92 | 36 | 9 | 9 |

At q = 0.01, the real-background phase rule gives 20.6% and 36.5% recovery at the two depths. Their 95% star-bootstrap intervals are 15.4-26.0% and 31.1-42.4%. Requiring added-signal curvature reduces these counts from 52 to 3 and from 92 to 36. On a flat background the same input gives only 0 and 8 phase matches. There are no flat-background long, strong matches at either q = 0.002 or q = 0.01. Thus a long near-phase track can persist in the real pattern when the isolated added clump cannot form such a track.

All 17 long, strong real-background matches at q = 0.01 give q_bound < q/2. Their median q_bound/q is 0.047 at depth 0.5 A and 0.050 at depth 2 A. No such track passes the curvature rule. These are narrow background features selected by phase proximity, not evidence that the injected material stayed radially narrow. At q = 0.002, 38 of 39 long matches give a factor-of-two error, and two of those 38 pass the curvature rule. The curvature diagnostic therefore improves attribution but does not by itself make the width bound safe in mixtures.

There is also a small estimator effect on isolated profiles. At q = 0.0004, some flat-background bounds fall below the input by up to 11%. None gives a factor-of-two error. Finite harmonic representation and use of the mean of the last three widths matter when calling a bound conservative. We do not treat these small effects as evidence of background confusion.

The exact sham coverage, 18.3%, agrees in scale with the observed 41/252 = 16.3% sham phase-match rate (95% star-bootstrap interval about 11.2-21.2%). The sham curves contain no added signal. A random-phase subtraction can correct a mean false-match rate, but cannot identify which individual recovered widths belong to the injection.

Independent quadrature verifies the analytic coefficients to a maximum absolute error of 2.30e-16. The cached detector evaluation is identical to the source evaluation on its phase grid. These checks test the implementation, not the cloud physics.

![Selection and background confusion](files/selection.png)

The figure shows phase recovery on both backgrounds (A), phase recovery and the known-signal curvature rule on the real background (B), and long, strong phase matches whose q_bound is below half the known input (C). Horizontal lines in B are the real-background sham rates. Each fraction uses all trials in its group. The exact counts and 95% star-cluster bootstrap intervals are in `files/rates.json`. The bootstrap resamples stars, retaining their visits and paired phases. It has 1,000 draws with seed 89131. It measures variation across this selected sample, not all CPVs.

## What the test establishes

A near-phase track is not sufficient evidence that an added shearing clump was recovered. A source-identity check must accompany an injection test of width growth. In this model a spreading clump loses contrast at fixed area. A narrow background minimum can then remain the nearest track. Dividing that background width by a long time span can set a small apparent limit on an unrelated clump.

This does not show that freely orbiting gas explains long-lived narrow CPV dips. The bound for a single isolated, unwrapped, correctly identified profile remains useful under its stated optical and radial-distribution assumptions. The test instead prevents extension of that conditional bound to all material or to a population without a completeness and source-identity model. It also does not remove the measured slow changes of real minima.

A stronger empirical constraint should insert clumps into raw cadences, rerun period selection and window fits, and use paired no-injection runs. Recovery should require change attributable to the added signal, not only phase proximity. Population tests should include clumps that fade, merge or fail to form a long track. The resulting selection function can be combined with a physical model for supply and opacity.

## Limits

This is a model-space injection test on already selected CPV hosts. It does not estimate CPV occurrence, a dust mass, a gas temperature, or a material residence time. It does not repeat the source's cadence-level shear experiment, which used a fixed mean background plus shifted residuals and set a different q for each visit so that the final arc was 0.06 cycles. Our real backgrounds evolve, our q values are fixed, and our noise is not newly sampled. Therefore our rates do not estimate how many of the original 118 matches were wrong.

The uniform radial and Gaussian angular distributions, small-q linear shear, additive flux decrement, window-center evaluation, initial width and two depths limit transfer to real clouds. A finite stellar-disk kernel, optical thickness, a nonuniform radial distribution, changing opacity, and supply can alter the response. At large L a periodic arc is no longer a single unwrapped dip. We do not apply the single-dip geometric bound to that arc as a physical theorem. The under-bound diagnostic tests what happens when the phase-matched track is used without source verification. Flat-background trials have no cadence-level false-positive noise and are only ideal controls. Two random phases per visit do not exhaust all crowding conditions. The thresholds in the curvature diagnostic are explicit choices. A failure to dominate curvature is not proof of zero contribution to extinction.

## Reproduction

Use Python 3.12, the SCI CLI, and the package versions in `files/versions.json`. Run from an unpacked publication, with a separate writable scratch directory and the campaign path:

```sh
python -B files/analyze.py /path/to/campaign /path/to/scratch
python -B files/validate.py /path/to/scratch/validation.json
python -B files/coverage.py /path/to/campaign /path/to/scratch
python -B files/report.py /path/to/scratch /path/to/scratch/report
```

The first command verifies the source bundle, records its hashes, extracts three entries into scratch, and computes all trials on one numerical thread. The second compares the analytic Fourier coefficients against independent 131,072-point quadrature. The third computes exact sham coverage from the published tracks. The fourth writes tables and the figure. Compare those outputs with the bundled tables and `files/validation.json`. The scripts do not need the original 443 raw light curves; the source publication gives their retrieval recipe and hashes. Do not use the signed directory as scratch or as a report destination.

## Files

`analyze.py`, `report.py`, `coverage.py` and `validate.py` are original code. `coverage.json` gives exact sham coverage and its extra input hashes. `trials.csv` gives the simulated trial results, source identifiers and attribution diagnostic. It is not a source catalog. `rates.json` gives aggregate counts and cluster intervals. `selection.png` is the display figure. `provenance.json` gives exact inputs. `versions.json` gives the software environment. `validation.json` gives the numerical checks. All are under `files/`.
