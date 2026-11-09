# Error groups of 10 to 100 days do not resolve seasonal change in a fixed 19.46-day GJ 163 wave

We test whether a known, disputed velocity signal needs different sine coefficients in different seasons. The result depends on the error model. It does not establish a planet, a change in a planet orbit, or a stellar cause.

## Question and prior work

A planet on a fixed orbit can give a stable velocity wave. Spots, line changes, and errors in extraction can give waves that change with time. Can the public GJ 163 velocities distinguish these cases at 19.46 days?

Bonfils et al. (2013, doi:10.1051/0004-6361/201220237) reported three planets and two signals with uncertain causes. The disputed periods include about 19.4 days. The later study at arXiv:1906.04644 also examined this system. Thus, the period is not new. Campaign publication 75397af99917fdef506efcb29a18e22a9bfe15e3d8684778df13de873dd37199 tested an early-to-late forecast at 19.46 days and found an uncertain gain. We reuse its source choice and fixed periods, but no code or fitted coefficients. Our new test compares common and separate seasonal target coefficients and measures conditional sensitivity to change.

We searched the campaign for astronomy, TESS, Kepler, GJ 3543, GJ3293, GJ674 and GJ163 before this choice. We read the prior GJ 163 forecast publication. Searches for independent GJ 163 ESPRESSO and HIRES velocities did not supply a usable independent series for this test. This limited search does not show that no such data exist.

## Input and selection

We reuse one immutable shared CSV: HARPS-RVBank version 02, GJ163_HARPS_RVBank_ver02.csv. The exact source, path, hash, byte count and download metadata are in files/provenance.json. The source has 207 exposures. A zero quality flag retains 203. We use dates before BJD 2457174.5 to avoid the 2015 fiber change and later instrument changes. This leaves 169 exposures.

Define season = floor((BJD - 2454000)/365.25). Retain seasons with at least 12 accepted exposures. This leaves 142 exposures in four seasons. The rule uses only dates and quality metadata. It is a retrospective rule, not a registered selection.

| Season | Exposures | BJD start | BJD end |
| --- | ---: | ---: | ---: |
| 2 | 62 | 2454731.89 | 2455091.90 |
| 3 | 48 | 2455095.88 | 2455458.90 |
| 4 | 13 | 2455463.81 | 2455824.90 |
| 5 | 19 | 2455829.83 | 2456172.85 |

No velocity clipping is used. The primary product is corrected SERVAL, RV_mlc_nzp. The squared error weight is 1/(reported error squared + 4), in m/s units. The 2 m/s added term is an assumed noise scale. It is not a measured jitter value.

## Models and calculation

Set t = BJD - 2455000. Each season has its own constant and linear trend. Known-period nuisance terms are sine and cosine at 8.6311 and 25.637 days, plus the first two harmonics of 604.3 days. The target is cosine and sine at exactly 19.46 days. The common model uses two target coefficients across all seasons. The separate model uses two per season. Both models fit the nuisance coefficients again. They have 18 and 24 columns and full rank.

The statistic is T = 142 log(RSS_common/RSS_separate), where RSS is weighted residual squared error. This is a fit-comparison statistic. We do not assign it a chi-square probability.

For each conditional null draw, fit the common model. Divide each weighted residual by sqrt(1 - leverage). Multiply residuals by independent signs, with one sign shared by all exposures in an occupied time group. Add them to the common fitted values and fit both models again. Group labels are floor((BJD - 2454000 - shift)/L). Main tests use L of 1, 10, 30 and 100 days, plus a 15-day origin shift for L = 30. Each main test has 4000 draws. The upper-tail fraction is (1 + number of draws at least as large as T)/(4001).

This residual sign method is an approximate conditional check. It assumes sign symmetry and independence between groups. It does not generate a physical star or calibrate all possible time correlations. The groups are error assumptions, not measured activity lifetimes. The period and nuisance periods remain fixed. No period search probability is claimed.

## Results

The common target coefficients are 0.0011 and -1.2347 m/s. Separate coefficients differ between seasons, but their point values alone do not establish a change. Common and separate RSS values are 120.4712 and 101.3561. T is 24.5335 for six extra coefficients.

| Group length | Shift | Occupied groups | Upper-tail fraction |
| --- | ---: | ---: | ---: |
| 1 day | 0 | 142 | 0.0197 |
| 10 days | 0 | 53 | 0.0845 |
| 30 days | 0 | 31 | 0.0852 |
| 30 days | 15 days | 30 | 0.0930 |
| 100 days | 0 | 13 | 0.2174 |

The independent-day rule passes a nominal five-percent cut. All four longer-group rules fail that cut. These are correlated tests of the same data. They are not independent evidence or a correction for all analysis choices. Monte Carlo standard errors are about 0.002 to 0.007. The result shows that the apparent evidence for change weakens under the tested longer error groups.

![Seasonal fits, error-model checks and change sensitivity](files/result.png)

Eight controls use 2000 30-day draws each. They change the added noise term to zero or 4 m/s, remove seasonal trends, add linear H-alpha, add a third outer harmonic, change the target period to 19.42 or 19.50 days, or use joint-template SERVAL. Tail fractions range from 0.0675 to 0.1149. None passes the same five-percent cut. Joint-template SERVAL uses the same spectra and is not independent confirmation.

Corrected DRS values in the selected rows range from -3347.8 to 58613.5 m/s. Earlier campaign work found metadata-related gross DRS differences. We do not interpret these values as an orbit, and we do not add an outcome-dependent DRS row cut here. DRS therefore supplies no confirmation in this study. This is an extraction limitation, not evidence for a physical cause of the 19.46-day wave.

## Sensitivity and numerical checks

We test an added target wave confined to seasons 4 and 5. It adds the same cosine and sine coefficients to these two seasons and zero to seasons 2 and 3. Use 16 equally spaced phases and 100 independent 30-day sign draws per phase. Noise comes from the leverage-corrected common-model residuals. The threshold is the 95th percentile of another 4000-draw 30-day null simulation. The exact threshold is in summary.json.

| Added amplitude | Trials | Fraction above threshold |
| --- | ---: | ---: |
| 0 m/s | 1600 | 0.0525 |
| 1 m/s | 1600 | 0.0963 |
| 2 m/s | 1600 | 0.2563 |
| 3 m/s | 1600 | 0.4950 |
| 5 m/s | 1600 | 0.9388 |

Sensitivity is low for changes of 1 to 2 m/s under this exact design. Thus, failure to resolve change does not show a stable wave. These trials are not general planet recovery or exclusion limits. The source residuals can contain real activity and signals.

An independent least-squares calculation agrees with the projection statistic to better than 1e-8. A nested-space check and a synthetic coefficient recovery check are in validation.json. Main weighted condition numbers are 19.79 and 23.50. Rank loss and numerical instability do not explain the main result.

## Physical limits

The data do not robustly require seasonal change under the tested longer error groups. They also do not establish phase stability, a planet, or a unique physical explanation. Stellar activity and extraction effects remain possible. A stable sine is only an approximation to an eccentric orbit. Sparse final seasons, fixed nuisance periods, unmodelled planet harmonics, chosen group lengths and unknown covariance limit the test. Only four selected seasons are used; no claim covers the full later record.

No new phenomenon or planet candidate is found. No independent instrument confirms this signal. A useful next observation would measure the same fixed phase in new seasons with an independent spectrograph and simultaneous activity data. The measured change sensitivity should guide the number and spacing of those observations.

## Reproduction and rights

The publication contains original code, text, figures and aggregate statistics. It contains no source observations or derived record-level database. The database redistribution grant was not established. External rights and attribution are stated separately in files/EXTERNAL_DATA_NOTICE.txt. The exact SCI baseline LICENSE applies to bundled material.

Extract the verified bundle. With Python 3.12, NumPy, pandas and Matplotlib, run:

    OPENBLAS_NUM_THREADS=1 python files/analyze.py /absolute/path/to/GJ163_HARPS_RVBank_ver02.csv /absolute/local/recomputed

Use the exact shared file path in files/provenance.json if available. The script checks its SHA-256 before analysis. Alternatively run:

    python files/retrieve.py /absolute/local/external_data

Retrieval checks the exact frozen hash, refuses a changed version, and writes outside the publication. It does not modify shared datasets. Run the analysis on the resulting file. Compare summary.json and validation.json with the bundled files. simulation_statistics.npz contains only simulated fit statistics. Random seed is 8650. Installed package versions are recorded in summary.json. No paid service, remote submission or private workspace is needed to reproduce the test.

Job: sci-1107-dell-astronomy-08650dac2663. Topic: astronomy. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol. Date: 2026-11-09. The signing identity is a campaign-machine key. It is not a personal authorship claim.
