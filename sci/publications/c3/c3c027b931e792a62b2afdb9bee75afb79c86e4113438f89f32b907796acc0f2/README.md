# A bounded planet-period error gives less than 0.938 m/s of the early GJ 3341 residual

In 61 early public HARPS visits to GJ 3341, a fitted 15.052-day residual has amplitude 2.262 m/s. A deterministic test gives a smaller upper bound for leakage from an error in the known planet period. The bound is 0.937732 m/s if the true period is 14.186 to 14.228 days, the fundamental amplitude is at most 5 m/s, and the first harmonic amplitude is at most 2 m/s. These assumptions define the scope. The result does not include noise, stellar activity, or other model errors. It does not establish a second planet.

## Question and prior work

Can an error in the fixed period of GJ 3341 b alone produce the early 15.052-day residual? Astudillo-Defru et al. (2015, A&A 575, A119) reported a planet period of 14.207 +/- 0.007 days. They also discussed longer residual variation and stellar activity. The period interval in this test is three times that quoted error on each side of the central value. It is a tested interval, not a new confidence interval.

We searched the public campaign for GJ 3341 before we chose this question. SCI 071303675e3a... found the early residual at 15.05186995 days. Its frozen early wave did not clearly predict later velocities. SCI f92ee6f46a24... tested coefficient changes. Its repeated-search test gave a large conditional tail fraction. Neither result establishes a new companion. We use their fixed period, split and quality rule. We add a bound on a specified deterministic explanation and fits with a variable planet period. We do not repeat their discovery search or claim independent selection.

The web search checked the discovery paper and the HARPS-RVBank papers by Trifonov et al. (2020) and Perdelwitz et al. (2024). The search was not a complete literature review. No independent instrument data are used here.

## Data and provenance

We use the existing immutable file at:

    /mnt/dell-data/shared_datasets/gj3341-harps-rvbank-v02-e91e2770/gj3341_rvbank.csv

The workspace alias is ./datasets/gj3341-harps-rvbank-v02-e91e2770/gj3341_rvbank.csv. The source is HARPS-RVBank version 02:

    https://exo-restart.com/wp-content/uploads/Stellar_parameters/Ver_02/GJ3341_RVs/GJ3341_HARPS_RVBank_ver02.csv

The file has 76,184 bytes. Its SHA-256 is 2ec89c0dddda24cc2daef76c82f4b41b6b18f18956dc09d685c3ed4e1b528c19. We checked this hash. files/rvbank.csv is an exact snapshot for offline use. files/provenance.json retains the source metadata and our use record. No download was needed and no shared data were changed.

There are 137 raw rows. We require f_RV = 0 and an absolute distance below 100 m/s from the unflagged SERVAL median. This leaves 135 rows. The prior study chose this rule after it saw one large unflagged departure in both extractions. The cause of that row remains unknown. We inherit that exploratory cut; it is not a blind selection. The split at BJD 2455700 gives 61 early and 74 later visits. All used dates precede the 2015 fibre change.

The corrected SERVAL product is the main input. Corrected DRS and uncorrected SERVAL are controls. These products share spectra and cannot give independent telescope confirmation. The source supplies nightly zero point corrections, but residual instrument errors can remain. This test does not inspect detector pixels or raw spectra.

## Model and bound

Set t = BJD - 2455700 days. The fixed model contains a constant, a linear time term, and sine and cosine pairs at P0 = 14.207 days and P0/2. The extra columns are sine and cosine at Pc = 15.05186995 days. The weights are the inverse square root of quoted variance plus (2 m/s)^2. The added term is fixed, not estimated. All amplitudes are Euclidean norms of sine and cosine coefficients.

Let X be the full eight-column design, W the diagonal weight matrix, and L the last two rows of (WX)^+ W. The plus sign denotes the Moore-Penrose inverse. The fitted residual coefficients for any velocity vector y are L y. Direct computation confirms that L annihilates the fixed six-column planet model.

For a true period P, let Z1(P) be its sine/cosine pair and Z2(P) its first harmonic pair. A noiseless waveform with coefficients a and b gives residual coefficients L Z1 a + L Z2 b. Thus:

    residual amplitude <= 5 ||L Z1(P)||_2 + 2 ||L Z2(P)||_2

when ||a|| <= 5 and ||b|| <= 2 m/s. The matrix norm is the largest singular value. The triangle inequality makes this an upper bound for every pair of phases, including phases that cannot occur in a single exact eccentric orbit. A constant and trend cancel. The assumed amplitude caps exceed the main fitted fundamental and harmonic amplitudes in all three time ranges; they are explicit assumptions, not measured hard limits.

We evaluate P on a 0.0001-day grid over [14.186,14.228]. The largest early bound is 0.925044 m/s. To cover all points between grid values, we add a derivative bound times 0.00005 day. For each harmonic k, the Frobenius norm of the derivative of its sine/cosine pair is sqrt(sum_i (2 pi k t_i/P^2)^2). A valid Lipschitz constant for the bound is:

    ||L||_2 sqrt(sum_i (2 pi t_i/Pmin^2)^2) (5 + 2*2)

For the early data this is 253.758 m/s/day. The added margin is 0.012688 m/s. The continuous-interval bound is therefore 0.937732 m/s. This proof uses exact-arithmetic inequalities evaluated in ordinary double precision, not certified interval arithmetic. Numerical validation is supplied.

This is a bound on the deterministic contribution from period error. It is not a bound on total fitted amplitude when noise is present. It is not a false-alarm probability.

## Results

| Data range | Visits | Fitted fixed-period residual amplitude, m/s | Period-error upper bound, m/s |
| --- | ---: | ---: | ---: |
| Early | 61 | 2.2623 | 0.9378 |
| Later | 74 | 1.2449 | 0.3713 |
| All | 135 | 1.4208 | 0.8378 |

The upper bounds in the table are rounded upward. The same planet-period and amplitude assumptions apply to all rows. The results do not say that the remaining amplitude is physical. Noise can add a vector in the fitted coefficient plane. Subtracting these bounds from an observed amplitude does not give a confidence bound on another signal.

We also let the planet period vary. In a dense search from 14.0 to 14.4 days, the early planet-only fit has period 14.274775 days. With the extra fixed wave, the period is 14.257994 days and the residual amplitude is 2.3752 m/s. The weighted error decrease from the extra wave is 14.8139. At the original fixed planet period, it is 16.4977. Thus, this broad planet-period adjustment does not remove the early residual in the tested harmonic model. The fitted early periods are outside the quoted discovery interval. They are descriptive fits to this subset, not new orbit measurements.

The broad check repeated from 13.9 to 14.5 days gives the same minima to numerical precision. A fit restricted to 14.186 to 14.228 days reaches the upper boundary in both models and leaves a residual amplitude of 2.3542 m/s. Such boundary fits must not be read as unconstrained estimates.

files/fits.csv gives 81 fits across three products, three time ranges, three fixed error terms (0, 2, 4 m/s), and one to three planet harmonics. Its main variable-period interval is 14.15 to 14.26 days. Some early fits reach the upper boundary. files/wide_check.json resolves that concern with wider searches. In early corrected SERVAL, fixed residual amplitudes range from 2.181 to 2.262 m/s across these controls. The main corrected DRS amplitude is 2.111 m/s. These are shared-data checks; they do not establish instrument independence. The rigorous bound above applies only to the stated main weights and two-harmonic model.

The figure shows the early error profiles and the period-error leakage bound. It does not display statistical confidence regions. No discovery p value is assigned to the previously selected extra period.

## Validation and limits

Ten thousand random phase and period trials compare direct weighted fits with the linear operator. The largest coefficient difference is below 6e-15 m/s. The largest sampled leakage is 0.9032 m/s, below the continuous upper bound. At the exact fixed period, the noiseless control leaves less than 3e-15 m/s. A separate normal-equation fit agrees in weighted error to 8e-15. These trials check the implementation; the analytic margin supplies the between-grid bound.

A stable companion, variable active regions, imperfect orbit shape, correlated noise, and shared reduction errors remain possible sources of residuals. An exact Kepler orbit includes higher harmonics. Our primary bound allows only a fundamental and first harmonic; it does not cover unrestricted eccentric or interacting systems. The bounds do not measure activity or total instrument contamination. The source period errors are not independent of HARPS data. We do not establish signal coherence, exclude planets, or confirm a new phenomenon. This work narrows one explanation under explicit assumptions and preserves a reusable leakage test.

## Reproduction

From an extracted bundle, run these commands in order:

    OPENBLAS_NUM_THREADS=1 python files/analyze.py
    OPENBLAS_NUM_THREADS=1 python files/validate.py
    OPENBLAS_NUM_THREADS=1 python files/wide_check.py

They need no network and write derived files only within files/. Python and package versions are in files/summary.json. The code needs NumPy, pandas, SciPy, and Matplotlib. analyze.py takes about one minute on the study host. The other checks are short. accepted.csv, fits.csv, profiles.csv, leakage.csv, summary.json, validation.json, wide_check.json, and evidence.png preserve the results.

To retrieve the raw file elsewhere, use the exact source URL above and check the SHA-256 before use. If the campaign helper is available, use a new name:

    campaign-dataset gj3341-rvbank-v02-retrieval --url https://exo-restart.com/wp-content/uploads/Stellar_parameters/Ver_02/GJ3341_RVs/GJ3341_HARPS_RVBank_ver02.csv --filename gj3341_rvbank.csv --max-gib 0.02

Reuse an existing file with this hash. Never replace an existing shared dataset. The bundled snapshot permits reproduction if the service changes or fails.

## Job record

Campaign 11_07_2026. Job sci-1107-dell-astronomy-6ce18c054a86. Topic astronomy. Machine dell. Account codex-andrii. Model gpt-6.1-sol with high reasoning effort, through the Codex harness in T3 Code. One finite worker performed this study. No agents were launched. The campaign-machine key signs the bundle; it is not a personal authorship claim. The cited authors supplied the observations. The baseline license applies to this work and does not remove source rights. No private key is included. This publication is saved locally and is not submitted to a remote archive or index.
