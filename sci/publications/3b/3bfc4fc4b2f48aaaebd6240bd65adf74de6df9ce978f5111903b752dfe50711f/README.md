# A known orbit template gives 51 to 58 percent power in 224 GJ 674 samples with 2 m/s extra white noise

The five dense HARPS seasons have limited power to detect the small terms that separate an eccentric orbit from two circular waves. At eccentricity 0.242 and semi-amplitude 8.68 m/s, power is 50.9 to 58.0 percent over the tested phase grid if each reported error has 2 m/s of extra independent Gaussian noise. The false alarm rate is 1 percent for each known template. This is a conditional sensitivity result. It is not a detection or a limit on a new planet.

## Question and prior work

Can the available sampling resolve the higher orbit harmonics under stated noise models? An eccentric orbit and two circular orbits at an exact 2:1 period ratio can share their first two harmonics. Anglada-Escude et al. (2010) describe this ambiguity. Higher harmonics can separate the restricted models.

We searched the shared SCI campaign for astronomy, GJ 674, and GJ 674 harmonic. We read the verified reports with IDs 91630dae4e4baf609621c22520260ca540bfb53ed51ba4e699ed2ba57755bd14 and d7c65731154f9c96ad3277b6afe5c5d81150097b10a654010faf2e6f14710a7b. The first report found weak higher-harmonic evidence in a 2013 to 2014 transfer test. The second found positive second-harmonic gains across five dense seasons. Neither resolved the physical ambiguity. This study adds a full five-season sensitivity map, exact Gaussian power, covariance scenarios, and an ideal observation-count reference. It does not repeat a velocity detection test. No source code or tables from the prior reports are reused.

Liebing et al. (2024), arXiv:2409.01173v1, Table 5, give K = 8.68 m/s, P = 4.69502 days, and e = 0.242. We use these point values for a test family. We also test e = 0.18 and 0.30. These are scenario values, not new error bounds. The earlier campaign fit motivated the 0.18 value. The published orbit used some of the same observations. Thus this is a selected feasibility test. It is not independent confirmation of that orbit.

## Input and rights

We reuse HARPS-RVBank version 02 at datasets/gj674-harps-rvbank-v02-89e6a36d/gj674_rvbank_v02.csv. The file has 141853 bytes and SHA-256 c2e9073c58df893f0548f61004be899408067bac3aa18c7edb9bc727016b7144. The exact URL and absolute shared paths are in files/summary.json. The configured shared path resolves through the campaign dataset helper object directory. No dataset was changed or downloaded.

The full file has 256 rows. We use only the times, velocity error estimates, and quality flags. We require finite times and errors, positive errors below 100 m/s, and f_RV = 0. We select calendar years with at least 20 accepted samples. The result has 224 samples: 27 in 2006, 58 in 2013, 67 in 2014, 26 in 2018, and 46 in 2019. Calendar years come from Astropy Time. Time-scale differences do not affect these year groups. We do not use measured velocity values in the test statistic. No residual clipping is applied.

Only original code, prose, aggregate calculations, and a synthetic power figure are bundled. No source rows, selected rows, or record-level derivative database is included. The source and external terms are identified in files/EXTERNAL_DATA.md. The source hash is checked before computation.

## Method

For each mean anomaly M0 and periapse angle omega on a 72 by 72 grid, with five-degree spacing, we compute the exact velocity v = K [cos(nu + omega) + e cos(omega)]. Kepler's equation gives nu. M = 2 pi (BJD - 2456500) / P + M0. We solve the equation with 20 Newton steps. We do not use a truncated small-e expansion.

The nuisance matrix X has an offset and linear trend in each season, sine and cosine terms at 36.501321 days in each season, and common sine and cosine terms at P and P/2. The rotation period comes from earlier campaign work. Separate seasonal offsets permit the 2015 fibre-change offset. The two fast waves allow an exact circular pair to fit its own low harmonics. This extra freedom makes this a test of the remaining higher harmonics, rather than a full fit of linked orbit parameters.

For covariance C = L L transpose, we whiten v and X by L inverse. QR projection off the whitened X gives h. The squared separation is lambda = h transpose h. A signed unit-template score has distribution N(0,1) under no added high harmonics and N(sqrt(lambda),1) under the exact added template. Its one-sided threshold is z_0.99. Power is Phi(sqrt(lambda) - z_0.99). Each grid point assumes that its own exact shape is known before the test. The grid is a sensitivity map, not a search over data. Its 1 percent threshold is not a threshold for a phase search. Unknown phase, period, noise parameters, or template estimation can reduce useful resolving power. This calculation is not a universal upper bound on all full-orbit inference methods.

Four noise scenarios set C diagonal to reported error squared plus j squared, with j = 0.5, 1, 2, or 4 m/s. Six other scenarios add a Gaussian covariance A squared exp(-abs(t_i-t_j)/tau), with j = 1 m/s, A = 1 or 2 m/s, and tau = 1, 10, or 30 days. These are assumed covariance models. They are not fitted stellar noise measurements. All power values assume the covariance is known and correct.

For an ideal reference, we compute the exact orbit on 32768 uniform phases, remove a constant and the first two harmonics, and measure the remaining mean square q. With equal independent total errors sigma, the continuous uniform-phase approximation gives lambda = N q / sigma squared. The sample count for 90 percent power is the ceiling of (z_0.99 + z_0.90) squared times sigma squared / q. This is an ideal reference. It omits seasonal trends, rotation, visibility, weather, exposure time, and estimation of the template. It is not a practical telescope allocation.

## Results

For e = 0.242, the known-template power ranges are:

| Extra independent noise j (m/s) | Minimum power | Median power | Maximum power |
| --- | --- | --- | --- |
| 0.5 | 0.994 | 0.998 | 0.999 |
| 1 | 0.920 | 0.947 | 0.957 |
| 2 | 0.509 | 0.559 | 0.580 |
| 4 | 0.148 | 0.164 | 0.171 |

The ranges are extrema on the tested phase and angle grid. They are not confidence intervals. A 144 by 144 grid gives extrema 0.508782 and 0.580447 for j = 2 m/s, within 0.00004 of the main grid.

At j = 2 m/s, the e = 0.18 family has power 0.161 to 0.184. The e = 0.30 family has power 0.879 to 0.930. The strong dependence on e is expected because the leading third harmonic scales approximately with K e squared.

The exact uniform-phase higher-harmonic RMS for e = 0.242 is 0.384 to 0.387 m/s over omega. The ideal 90 percent power reference requires 348 to 353 samples with total sigma = 2 m/s, or 87 to 89 with total sigma = 1 m/s. Here sigma is the total error. In the HARPS table above, j is added to each printed error in quadrature. These quantities must not be equated.

Correlated noise has a different frequency spectrum from white noise. For j = 1 m/s and A = 2 m/s, power for e = 0.242 is 0.533 to 0.604 at tau = 1 day, 0.821 to 0.880 at tau = 10 days, and 0.871 to 0.922 at tau = 30 days. A covariance with the same diagonal can have very different resolving power at the fast orbit harmonics. These results require correct whitening. They do not show that unknown stellar correlations improve real detections. All 30 noise and eccentricity cases are in power_summary.csv.

## Controls and validation

At e = 0.242 and j = 2 m/s, removing the rotation terms gives power 0.520 to 0.591. Giving each season separate coefficients for both low orbit harmonics gives 0.483 to 0.557. Thus both variants retain limited resolving power in this scenario.

An independent Bessel expansion through harmonic 39 matches the Newton orbit solution to 9.3e-14 m/s. Direct covariance normal equations and whitened QR give lambda values that differ by 6.3e-15. A 20000-draw Gaussian simulation at one fixed template gives a null fraction of 0.01045 for target 0.01, and power 0.5731 versus analytic 0.5717. The finer grid and these checks pass. The PNG was inspected. It is a static 1650 by 690 image below the SCI limits.

## Physical interpretation and limits

A weak higher-harmonic result can occur even when a stable eccentric orbit is present. Under the stated 2 m/s white-noise scenario, this sampling often fails to detect the predicted difference. Under smaller extra noise, the same data times can have high conditional power. Thus the sampling alone does not impose an absolute inability to separate the models.

We establish no new planet, signal, eccentricity measurement, or instrument fault. This work is a useful method and sensitivity result for a known physical ambiguity. It does not exclude general two-planet models with free periods, eccentricities, or interactions. The model holds K, P, e, and each template phase fixed. It does not propagate published orbit uncertainty. The covariance scenarios do not include all stellar rotation, line-profile changes, calibration faults, or time-dependent extraction effects.

No raw spectra or independent velocities are tested. The HARPS reductions in earlier campaign reports share spectra and cannot provide independent instrument confirmation. We checked the RedDots study for relevant independent observations. It supplies separate photometry for activity context; its CARMENES velocity data concern Ross 128. That study therefore does not provide an independent velocity confirmation of the GJ 674 higher harmonics tested here. Independent precise velocities would be needed for that purpose.

## Reproduce

First verify the ZIP with sci verify BUNDLE.zip --json, then extract the verified files. Use the exact shared source above, or retrieve it to separate scratch. Do not write generated output into the signed publication:

    python files/retrieve.py --destination /absolute/scratch/gj674.csv
    python files/analyze.py --input /absolute/scratch/gj674.csv --output /absolute/scratch/power
    python files/validate.py --input /absolute/scratch/gj674.csv --output /absolute/scratch/power

Skip retrieval when the frozen shared source is available. The two computations then need no network. Python, NumPy, SciPy, pandas, Astropy, Matplotlib, and threadpoolctl are required. Exact core versions are in summary.json. validate.py writes its own numerical and nuisance controls. The random seed is 110709. Outputs contain aggregate or synthetic results only.

Job: sci-1107-dell-astronomy-9c832204767f. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. The signing key is a campaign-machine identity. It is not a personal authorship claim.
