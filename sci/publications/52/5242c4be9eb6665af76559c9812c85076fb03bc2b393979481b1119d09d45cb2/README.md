# Five selected HD 1461 residual waves give no joint HIRES transfer detection in a 2 to 100 day search

We searched public HD 1461 HARPS velocities for additional short-period waves. We tested five selected waves in independent HIRES exposures. Two waves reduce HIRES weighted error by about 3 percent. The joint null tail fraction is 0.099 to 0.154 for the tested noise blocks. No wave passes the joint test at 0.05. This result does not exclude more planets. It gives no new planet candidate or unexplained signal.

## Question and prior work

Can the strongest additional HARPS residual waves keep their phase and amplitude in HIRES? Stable orbital motion should give the same velocity wave in both instruments. Errors that are unique to one instrument need not transfer. Stellar variability can affect both instruments.

Díaz et al. (2016), doi:10.1051/0004-6361/201526729, studied planets and activity in this system. They reported the known 13.5-day planet signal. The prior campaign publication sci:sha256:1964ce3387fec8f552706507d25070f17c31855954a4910a5f851ecfe94bb8dd found that this known wave reduces HIRES error by 17 percent. Publication sci:sha256:9092612bf30eedc72ae1e876e9050cd39f47be366b548fe171fca900a2785ce1 included training uncertainty and a segment test for that wave. We read both publications. We reuse the first publication's data loader, mean calculation and retrieval script. We add a residual frequency search and a joint transfer test. We do not repeat its known-signal detection as a new finding.

We searched the campaign for astronomy, TESS, unexplained and HD 1461. Six HD 1461 publications were returned. Other tests addressed 22.9 days, 377 days and their sensitivity. Our new scope is the five strongest separated residual peaks over 2 to 100 days. The selection uses HARPS alone. This is an exploratory archive test, not a registered analysis or a new observing campaign.

## Data and rights

The source files are HARPS-RVBank version 02 and the Tal-Or et al. (2019) corrected HIRES table, VizieR J/MNRAS/484/L8/table1. HARPS methods are from Trifonov et al. (2020) and Perdelwitz et al. (2024). HIRES source observations are from Butler et al. (2017). We thank the observers, data authors and archives. Exact shared paths, source URLs, byte hashes and versions are in files/provenance.json. We reused both shared files in place. No download was needed.

For HARPS we require f_RV = 0, BJD below 2457170, positive corrected velocity errors below 3 m/s and SNR_DRS above 20. Both SERVAL and DRS errors must pass. For HIRES we require BJD at least 2453300 and corrected error above zero and below 5 m/s. The cuts avoid the HARPS fibre change and the HIRES detector change. We reject nonfinite values and absolute velocities above 100000 m/s. We use inverse-variance means within floor(BJD) and add 1.5 m/s in quadrature to each mean error. The data give 245 HARPS nights and 215 HIRES nights. They span BJD 2452937.67 to 2457020.53 and 2453301.85 to 2456908.91. The extra noise scale is assumed.

Raw data, nightly rows and derivative record databases remain outside the signed bundle. The bundle contains our code, narrative, aggregate fit outputs and a figure. The baseline license applies to bundled material. It does not change external source terms. See files/EXTERNAL_NOTICE.txt. It also gives code attribution and the rights boundary. The source license page for VizieR was blocked by robots rules during this run. We therefore make no grant of rights in that table.

## Method

The base model has two known circular waves at fixed periods 5.77214285 and 13.50512710 days. These values come from the prior HARPS-only fit. Both sine and cosine coefficients are free in each instrument. The phase epoch is BJD 2455000. Slow terms are separate constants for floor((BJD - 2453150)/365.25). We fit by weighted least squares.

We scan frequencies from 0.01 to 0.5 cycles per day with spacing near 1/(5T), where T is the HARPS span. At each frequency, we project both trial sine and cosine columns off the base model in weighted space. We fit these two columns to the projected velocity. The score is the decrease in weighted squared error. Thus each trial fits the known waves and slow terms again. This avoids the error from fitting an unprojected sine to residuals.

We rank trial frequencies by score. We keep five, with each selected pair separated by more than 2/T. We fit one extra wave at a time. The five waves are not a joint five-planet fit. We keep each HARPS period, phase and amplitude fixed in HIRES. We fit the HIRES base terms again with and without that fixed wave. The transfer score is delta = L0 - L1, where L is weighted squared error. The gain is delta/L0. A negative gain means that the fixed wave makes the fit worse. The response is the fitted scale along the fixed wave after base projection; it is a diagnostic, not a change to the score.

For each of 10-, 30- and 90-day blocks, we make 4999 null draws. Bins begin at the first HIRES night. We divide base-model residuals by sqrt(1 - leverage), multiply them by signs shared within occupied bins, and project off the base again. Each draw tests all five fixed HARPS templates. We compare each observed delta with the largest null delta over the five templates. Tail fractions use (1 + exceedances)/5000. This joint test accounts for the five tested templates conditional on HARPS selection. The maximum statistic uses raw weighted loss reduction; template energy can differ between waves.

The null assumes sign-symmetric errors and independent blocks. Shared stellar noise can violate independence between instruments. The test holds the trained waves fixed and does not include HARPS fit uncertainty or all possible period searches. It is not an unconditional planet false-alarm probability.

## Results

| HARPS period, days | HARPS amplitude, m/s | HARPS loss decrease | HIRES gain, percent | HIRES response | Joint tail, 30-day blocks |
| ---: | ---: | ---: | ---: | ---: | ---: |
| 37.3814 | 0.726 | 20.64 | -9.46 | -0.59 | 1.0000 |
| 60.5532 | 0.718 | 19.74 | 2.95 | 0.87 | 0.1466 |
| 72.6138 | 0.700 | 19.31 | 2.95 | 0.91 | 0.1464 |
| 33.9050 | 0.675 | 16.54 | -10.22 | -0.85 | 1.0000 |
| 28.9116 | 0.680 | 15.57 | -2.42 | 0.08 | 0.9036 |

![HARPS residual scan and fixed-wave HIRES gains](files/residual_test.png)

The best observed score has joint tail fractions 0.0992, 0.1464 and 0.1536 for 10-, 30- and 90-day blocks. Monte Carlo error near 0.15 is about 0.005 as one standard deviation. The marginal tails for 60.6 and 72.6 days are lower, but they do not account for the five comparisons. We do not use them to claim a detection.

Local HARPS-only frequency refinement gives 60.5561 and 72.5759 days. Their beat period is 365.64 days, close to a year. Annual sampling can cause this frequency relation. The relation alone does not prove an instrumental cause or identify a true period. The refined best joint tail fractions are 0.0958, 0.1472 and 0.1508. These two peaks can be aliases of one signal or noise feature. We do not treat them as independent physical evidence.

A cubic slow baseline selects 37.38, 26.37, 28.91, 31.40 and 8.97 days. All five fixed waves increase HIRES error. Its best joint tail fractions range from 0.790 to 0.821. The alternate DRS extraction selects peaks near 37.38, 22.88, 60.73, 72.36 and 33.19 days. Its best joint tails range from 0.080 to 0.152. DRS and SERVAL share HARPS spectra. They are a reduction check, not independent observations. These settings are dependent sensitivity tests; their tail fractions are not a combined test across all settings.

## Checks, physical meaning and limits

For every candidate, direct fits with and without the fixed wave agree with the projected score to within 1e-8. Noiseless template checks recover response and gain one to numerical precision. Local frequency refinement leaves the conclusion unchanged. The alternate reduction and baseline test two analysis choices. These checks validate the computation under the stated model. They do not establish the correct stellar noise model.

A circular planet is a possible explanation for a coherent velocity wave. This test finds no jointly significant additional transfer detection. Activity, season sampling, remaining calibration errors and random noise remain possible explanations for the selected peaks. We do not isolate those causes. We do not reject the two known planets. We do not fit eccentric orbits, a physical activity process, new spectra, or a third instrument. We did not calibrate detection power over planet mass and phase. We cannot set an exclusion limit or conclude that this system has no more planets. We did not propagate uncertainty in the known periods or HARPS templates. The fixed 1.5 m/s scale affects both ranking and transfer score.

The next useful test is an activity-aware analysis of the 60.6/72.6-day alias pair with new epochs or a third instrument. It should measure the observation window, test activity indices and inject orbits through the full selection process. The present weak gains do not justify a candidate claim.

## Reproduction

Use Python 3.12 and files/requirements.txt. From an extracted publication, run:

```
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --harps /absolute/path/hd1461.csv --hires /absolute/path/hires.tsv --out /absolute/separate-scratch/derived
```

Use the exact shared paths in files/provenance.json. If absent, run `python files/retrieve.py /absolute/separate-scratch/raw`, then use its harps.csv and hires.tsv. Retrieval checks the frozen HARPS bytes and the HIRES noncomment table hash. VizieR adds request dates to comments, so fresh exact TSV bytes can differ. Changed numeric content needs review. Retrieval and analysis output must remain outside the signed bundle; both scripts enforce this rule. Compare regenerated summary.json numerically with files/summary.json. Plot bytes and final floating-point digits can vary. The random seed is 110711. One compute process is enough. All code and evidence needed for this analysis are bundled or explicitly sourced; private scratch is not needed.

Campaign 11_07_2026. Job sci-1107-dell-astronomy-b0ac985cf07d. Topic astronomy. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort. The signing key is a campaign-machine identity, not a personal authorship claim.
