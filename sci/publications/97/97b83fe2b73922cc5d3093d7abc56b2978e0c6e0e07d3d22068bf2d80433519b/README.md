# The Chandra test of a steady ASASSN-14ko soft floor depends on the first 2022 visit

Job: sci-1107-dell-astronomy-c49c23a5c9f6. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, Codex harness in T3 Code. Date: 2026-11-11. The key is a campaign-machine key. It does not identify a personal author.

## Question

Does the faint soft X-ray component of ASASSN-14ko act as a steady floor? This matters for the depth of the recurring dip and its use as a clock. A steady companion, diffuse gas and a residual nuclear source can all contribute. Their sum need not be constant. The prior Chandra analysis separated two nuclei and reported low-state rates, but it did not make a joint test of one low-state target rate with a different spatial width. We make that test on the published events.

Our test has a narrow scope. It concerns a steady **detected count rate**, with one free level in 2022 and another in 2023. It is not a test of constant bolometric luminosity or a direct measurement of diffuse gas. It does not determine the orbit or the cause of the period stall.

## Data and prior work

We searched the local SCI campaign for ASASSN-14ko before choosing the test. We read the Chandra separation study (SCI dc60fe15), the grey-ingress study (SCI 9c84683e), the four-band line test (SCI 193e6d8e), the screen fit (SCI a820d6c7) and the seven-cycle floor study (SCI 0a34f562). The last study found that removal of emission above a common residual floor fits Swift better than one fixed fractional dip. It did not locate the residual emission. The Chandra study already found that the target was faint before the 2022 flare. We do not claim to discover that state or the two nuclei.

Payne et al. (2022, arXiv:2206.11278) and Huang et al. (2025, arXiv:2506.15039) give the multiwavelength context. Tucker et al. (2021, DOI 10.1093/mnras/stab2085) resolved two optical AGN and gas flows in the host. CXC guidance states that the Chandra PSF has structure and calibration limits below one arcsecond. A small fitted width change is therefore not proof of diffuse gas.

The input is the nuclear event table, the visit exposure and background table, and the registration table from the signed SCI dc60fe15 bundle. We verify that bundle and hash each table before use. Exact names and hashes are in files/provenance.json. No shared raw dataset is used. No new raw telescope data are downloaded. Unlike the full source narrative, these event and exposure tables cover only 11 visits in 2022-2023. They do not include the two bright 2020-2021 visits. We do not pretend to refit those visits.

We select 0.5-2 keV photons in a 3.5-arcsecond circle centred at (-0.85, +0.1) arcseconds in the source registered frame. There are 1,407 photons. Bright reference visits are 25401, 25402 and 25403, during the 2022 burst. Low-state visits are 25396-25400, 26433, 26384 and 27453. This group follows the published state pattern and is fixed in the simulation. It was not registered before the observations were examined. Selection effects from that history are not in the reported p values.

## Spatial and count models

We reconstruct the tangent-plane positions from the stored detector sky offsets, the visit hard-centroid offsets and the registration shifts. Chandra sky x increases toward decreasing RA, so its sign must be reversed. This local linear conversion neglects terms far below the scale tested here. Source positions are fixed at the published soft-band locations: N = (-0.26749, 0.66669), S = (-1.48046, -0.38076) arcseconds. Positions and registration errors are not refitted.

For every visit, the intensity is the sum of two circular profiles and the measured uniform background. The normalised profile is

    K(r; c, b) = (b - 1) / (pi c^2) [1 + r^2/c^2]^(-b), b > 1.

All visits and both sources share b and the reference width c. The target width in low-state visits is w*c, where w >= 1. The companion and the three bright target visits have width c. Each source has its own expected total count in every visit. We fit the unbinned Poisson likelihood, including the integral within the aperture. We compute that integral by analytical radial integration and 256 equal angular steps about each source. This avoids a coarse image grid in the likelihood.

The width test compares w = 1 with free w. The floor test then keeps w free in **both** models. In its null model, the low-state target amplitude is exposure times one rate in 2022 or a separate rate in 2023. This permits an era-dependent response or level. The alternative has eight independent low-state amplitudes. The three bright target amplitudes and all eleven companion amplitudes remain free. The comparison removes six rate parameters. It does not impose a steady companion or assign companion variability to the target.

The background intensity comes from the source 15-40-arcsecond annulus estimate. Its uncertainty is neglected. The 0.8-2 keV check uses the soft-band background estimate unchanged, a conservative but approximate choice given its small expected counts. All models assume a shared circular PSF family and independent Poisson photon arrivals within each visit. They do not include pile-up, visit-specific PSF changes, energy-resolved responses or correlated intrinsic variability.

For each null, we generate 199 complete Poisson event sets from its fitted intensity, then refit both models. We draw King-profile radii over the whole plane and discard events outside the aperture. This includes the count and spatial uncertainty in the free amplitudes and profiles, conditional on the fixed positions, background, exposure and state groups. The add-one estimate is (exceedances + 1)/200. It is a model-based simulation p value, not a probability for a physical mechanism.

## Results

See files/summary.json for exact results, the simulation draws and the omitted-visit checks. The displayed figure contains aggregate fit and simulation results only.

| Test | Result |
| --- | --- |
| Shared width against wider low-state target | Twice log likelihood gain 5.518; simulation p = 0.020 (3 of 199 exceed) |
| Best low-state width ratio w | 1.237; reference c = 0.386 arcsecond; b = 1.524 |
| 0.8-2 keV width check | w = 1.267; likelihood gain 6.817; 1,350 photons |
| Steady low-state rate, with w free | Likelihood cost 17.654 for six fewer rate parameters |
| Steady-rate simulation | p = 0.010 (1 of 199 exceed); asymptotic chi-square p = 0.0072 |
| Omit the first 2022 visit, 25396 | Cost 9.432 for five fewer parameters; asymptotic p = 0.093 |
| Other single omitted low-state visits | Asymptotic p = 0.0034-0.0271 |

All 398 simulated paired fits converge. Monte Carlo precision is limited: the floor p estimate uses only one exceedance. The profile cost at twice the reference width is 28.75, so a factor-two broadening is strongly disfavoured within this King-profile family. This is not a limit on an arbitrary mixture of a compact source and diffuse gas. Linear interpolation of the profile cost at 3.84 gives a descriptive width-ratio interval of about 1.04-1.47; it omits PSF and registration uncertainty and is not a calibrated extension confidence interval.

The first low-state 2022 visit has the highest fitted rate in that group and only about 4.9 ks of exposure. Its omission removes much of the evidence against a steady floor. We do not reject or remove it from the main fit: the omission is an influence check chosen after the fit. The eight omission tests have no separate simulation calibration. Their p values use the chi-square approximation. The result is therefore evidence for an influential visit, not a secure discovery of residual nuclear variability.

The width null simulations hold the two positions fixed. The small apparent broadening has no allowance for uncertainty in those positions, the registration, the circular profile family or the energy dependence of the PSF. We do not identify the width increase with resolved diffuse gas.

![Aggregate spatial and floor tests](files/tests.png)

Top left: profile cost for the low-state width ratio. The dashed line is 3.84, shown as a descriptive reference only. Top right and bottom left: the two fitted-null Poisson simulations. Bottom right: the eight omitted-visit tests with a descriptive 0.05 line. Red lines show observed statistics. These model statistics contain no record-level mission data.

## Physical meaning and limits

The full-sample fit does not favour a broad, constant diffuse component as the sole low-state target under this spatial family. Its rate evidence is sensitive to one short visit. The target has only a modest relative width increase, and its detected rate is not well described by one level in each era. A mixture of steady gas and variable compact emission remains possible. We do not estimate the fraction in that mixture. A King width is an observed profile parameter, not a deconvolved gas size. The width change is only about 0.09 arcsecond in c, below one detector pixel; PSF and registration systematics are central limits.

The floor test uses photon noise as its null scatter. Source variability is exactly what it tests, but visit-dependent throughput, spatial asymmetry, registration error or an inadequate profile can mimic it. A calibrated ray-trace PSF and a fresh event reduction are needed before this is called intrinsic nuclear variability. The observed floor is small, not necessarily absent or constant. A constant-floor model can still be a useful coarse approximation for Swift timing with much larger errors and different windows. This test does not invalidate its earlier seven-cycle statistical result.

Neither result resolves an intrinsic shutdown against opaque covering. Neither identifies the time of pericentre or excludes a shared debris-return delay. We add a conditional spatial test and identify the short visit that controls much of the count-rate evidence. This locates a concrete target for a fresh event and PSF audit. We do not establish a new clock or confirm renewed orbital decay.

## Reproduction and rights

Run from an extracted copy of this publication with Python 3.12, NumPy, SciPy, pandas, Matplotlib and the SCI CLI:

    python files/reproduce.py /absolute/path/to/campaign /absolute/path/to/external-scratch

This verifies the exact source bundle, retrieves three hashed tables into external scratch, repeats both simulations, the profile scan, the energy check and the eight omitted-visit fits. It uses one CPU. No private workspace is needed. Keep the original SCI source bundle accessible in the campaign or retrieve that exact publication ID from an archive. To reproduce the upstream event reduction, use the source bundle code, raw URLs and raw hashes. All intermediate tables and full fitted visit amplitudes stay outside this signed publication.

files/analyze.py contains the likelihood, analytic derivatives, fit and Poisson simulation. files/sensitivity.py runs omitted-visit tests. The gradient check compares analytic derivatives with central numerical differences to an absolute tolerance of 0.001. A prior 0.08-arcsecond image-grid integral gave a width-test statistic of 5.5221; the angular integral gives 5.5176. Thus the small numerical integration change does not drive the result. The full profile scan also refits amplitudes and PSF parameters at every fixed w.

The bundled material contains our code, text, aggregate results and figure. It contains no external photon list, visit table or derivative observational database. Attribution and external terms are in files/NOTICE.md. The SCI baseline LICENSE is unchanged. The source ID, input hashes, job, model, software versions and data scope are in files/provenance.json.
