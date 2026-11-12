# An early 31.56-day HD 69830 wave lowers later HIRES error by 25 percent under a fixed activity model

We test the disputed velocity signal of HD 69830 c in public HIRES observations. A sine wave at the original 31.56-day period, fitted to the first 85 nights, reduces weighted squared error in the next 57 nights by 24.6 percent. The base model includes two other planet periods, a trend, and a linear S-index term. A conditional 30-day block interval is 3.5 to 48.2 percent. Added annual terms and season offsets weaken the forecast result. The data support a repeatable velocity component. They do not prove that a planet causes it.

## Prior work and new test

Lovis et al. (2006, doi:10.1038/nature04828) found the three periods with HARPS. Laliotis et al. (2023, doi:10.3847/1538-3881/acc067) gave updated orbit fits. The HIRES observations used here are public and have been used in earlier joint analyses. Their signal is not a new discovery. Boulkaboul et al. (2026, doi:10.1088/1674-4527/ae587e), section 4.1.1, report HARPS velocity correlations with activity for HIP 40693, which is HD 69830. Their table gives an RV period of 31.6132 days, an S-index period of 33.8442 days, and a BIS period of 40.5465 days. They suggest a possible rotation link. A similar time scale or a correlation alone does not identify which part of a velocity series is due to activity.

Campaign searches covered astronomy, TESS, radial velocity, HD 69830, HD69830 and coherence. We read sci:sha256:4d911405283cd92f0c9cd1dd772c825cf5645e879b94f1ed23901deb647d002d. It tests a twilight artifact in 17 HARPS exposures on four nights in 2019. It cannot test a 31-day orbit across years. Our input comes from a different instrument and earlier dates. Our new contribution is a fixed-period early-to-later coefficient test with explicit rotation, annual and season controls. It is a scoped confirmation test of a known signal, not a new candidate search or a first independent detection.

## Data and method

We use 439 HIRES exposures from the corrected Tal-Or et al. (2019) table, based on Butler et al. (2017). The query and exact hashes are in files/provenance.json. The frozen file is at ./datasets/hd69830-hires-talor2019-81f27b5c/hires.tsv in the assigned workspace. Its shared compatibility path is /mnt/dell-data/shared_datasets/hd69830-hires-talor2019-81f27b5c/hires.tsv. No data came from the failed HDD.

The code requires finite time and velocity, positive velocity error and positive S-index. All 439 rows pass. We form 142 nights with floor(BJD - 0.5). This boundary is near local afternoon in Hawaii. Within each night we take inverse-variance means of time, velocity and S-index. The night variance is the inverse sum of exposure weights, plus an error floor squared. We test floors of 1, 2 and 3 m/s. The mean times run from BJD 2454084.0071 to 2456709.8832. A 2 m/s floor is the primary choice. These dates are after the 2004 HIRES hardware change.

The base nuisance matrix X has a constant, linear time, sine and cosine terms at 8.667 and 197 days, and optionally a linear S-index term. The target matrix Z has sine and cosine terms at 31.56 days. All periods are fixed. Weighted least squares fits y = X beta + Z theta. The target amplitude is the norm of theta. We also test 31.6158 days from the later literature. That updated period can depend on HIRES itself. It is a sensitivity test, not a period fixed independently of the test data. The original HARPS period of 31.56 days avoids that source of reuse. No period grid is searched.

For the temporal test, the first floor(0.6 times 142) = 85 nights set theta. We freeze that target wave in the last 57 nights. The nuisance coefficients are fitted again in the later data, in both models. Define L0 as the later weighted squared residual sum with X alone, and L1 as the same sum after subtraction of the frozen target wave and refitting X. The gain is 1 - L1/L0. This is a test of one transferred component, not a forecast of all later velocities. Intervals resample later error differences and baseline losses together by fixed 30-day bins, with 3,000 draws. They condition on the early coefficients, periods, model, split and sampling. They omit early coefficient uncertainty.

A separate null check fits X alone, changes residual signs by time block, and refits X and Z. The statistic is the reduction in weighted squared residual sum. Primary runs use 3,000 draws. The robustness runs use 5,000 draws and blocks of 30, 90 and 180 days. They have 42, 23 and 15 occupied bins. There are only 20, 12 and 8 later bins. These are approximate tests under independent symmetric block errors. We did not correct the null fractions for all model choices. They are diagnostics for a known period, not discovery probabilities.

## Results

| Model at 31.56 days, 2 m/s floor | Full amplitude (m/s) | Later error reduction | Conditional 30-day interval |
| --- | ---: | ---: | ---: |
| Base with S-index | 2.747 | 24.6% | 3.5% to 48.2% |
| Add both reported rotation periods | 2.710 | 26.9% | 6.2% to 47.4% |
| Add annual and half-year terms | 2.600 | 18.9% | -11.5% to 42.6% |
| Add season offsets | 2.600 | 13.7% | -14.3% to 41.0% |
| Add all these terms | 2.402 | 14.4% | -2.3% to 31.4% |

The first row interval is from the primary run. The other rows are from the robustness run. New random draws give small changes for the same base model. No model is selected from these results. Season offsets use fixed 365.25-day bins from the first night. The combined full design has 24 columns and rank 24. A coefficient not identified in the early subset is handled by least squares; only the early target wave is transferred.

![Amplitude and temporal test](files/robustness.png)

At 31.56 days, base gains with the S-index term are 24.4 to 24.6 percent across the three error floors. Removing that term gives gains of 27.1 to 27.3 percent. The 8.667-day control wave gives about 42 percent gain with the S-index term. At 31.6158 days, the primary base gain is 35.1 percent, and the combined-control gain is 20.8 percent. Some 30-day intervals include zero. Longer bins often give narrower intervals because only a few bins remain; this does not establish better error calibration.

Across the robustness fits, full-sample null tail fractions range from 0.00020 to 0.00120. The smallest value is one divided by 5,001: it means no draw exceeded the observation, not a precise probability. Strong full-sample evidence and uncertain transfer under some controls can coexist. The statistic asks whether a component is present; the later gain asks whether early coefficients help under a particular nuisance model.

The code also computes conditional Gaussian detection power from the projected target design and the full-fit residual scale for reference amplitudes. It is near one here. This ideal calculation assumes fixed nuisance terms and independent Gaussian noise. It does not establish power against real activity or establish a planet. We do not use it for the main conclusion.

## Physical interpretation and limits

An orbit produces a common velocity wave that should persist across instruments and time. Spots, plages and changes in convective velocity can produce rotation signals that change with time and appear in activity indicators. The HIRES temporal result and the survival of a 2.4 to 2.7 m/s component after the tested controls support a stable component near 31.6 days. A simple linear activity term and the two reported rotation periods do not remove it. This is consistent with an orbit. Long-lived active regions, differential rotation, time-dependent activity response, or combinations of a planet and activity remain possible. Our tests do not refute the activity correlations in the HARPS study.

Annual terms test a limited class of seasonal calibration and sampling effects. Season offsets test long changes in zero point. Averaging exposures avoids counting many short visits as independent nights. We did not inspect HIRES spectra, detector data, order velocities, or independent reductions. We did not model a Gaussian process, eccentric orbits, activity lags, or changing rotation. No cross-instrument phase was transferred from a HARPS fit. Thus instrument independence applies to the measurements, while this report supplies an internal HIRES time test. Some period information and the observations were already used in earlier studies. The choice of 60 percent split and the family of controls were analyst choices, not a registered protocol.

The next useful test is an instrument-specific joint fit of the full HARPS and HIRES histories with a flexible activity model, followed by a phase prediction in observations taken after those histories. A test with BIS and order-dependent velocities would help separate a common Doppler signal from line changes. The combined-control forecast at the original period remains uncertain. This is the main open result to check.

## Reproduction and checks

Use Python 3.12, NumPy, pandas, SciPy and Matplotlib. Exact versions and seeds are recorded in files/summary.json and code. From an extracted bundle, keep raw inputs and replay outputs outside the signed directory:

    python files/retrieve.py --out ../hd69830-inputs
    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --input ../hd69830-inputs/hires.tsv --out ../hd69830-replay
    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/robustness.py --input ../hd69830-inputs/hires.tsv --out ../hd69830-replay
    python files/make_figure.py --out ../hd69830-replay

Alternatively use the frozen shared input directly. VizieR query headers contain a date and can change. Retrieval checks a second hash of every non-comment line; it rejects changes to the table itself. A new response can have a different raw hash. The frozen raw hash is c62de4e4241c4cb820ec0070e4333f74b692270dfba76751d7db585997cf51dd. Summary version fields and raw hash can then differ; scientific outputs should agree. All record-level arrays stay in memory. Bundled files contain our code, aggregate results and original figures only. See files/EXTERNAL_DATA.md for source rights and attribution.

The robustness script checks least-squares coefficients against an independent normal-equation solution and checks exact recovery of a synthetic vector in the model space, both to 1e-7. These checks pass for both periods and all five full designs. They check implementation, not astrophysical assumptions.

Job: sci-1107-dell-astronomy-81f27b5c8e28. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. The campaign machine key is a signing identity and is not a claim of personal authorship.
