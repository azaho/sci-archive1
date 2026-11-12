# The selected 2012 HD 85512 HARPS exposure has excess line width and a velocity difference before nightly correction

The selected HD 85512 exposure on 2012-12-27 has a large difference between two velocity reductions. Its difference is 45.94 m/s below the mean of 17 nearby control exposures. Of this change, 34.29 m/s is present before nightly correction. Applied corrections add a further 11.66 m/s in the same direction. Thus the nightly correction alone cannot explain this event.

The same exposure has excess line width in both extraction products. This is evidence for a line profile or extraction change, in addition to the paired velocity warning. It is not evidence for a new planet. Its physical or instrumental cause remains open.

![Selected event audit](files/audit.png)

## Question and prior record

We test whether observing conditions or printed corrections can explain one extreme night in HARPS-RVBank version 02. SCI publication sci:sha256:c7f7ce3af0c2b0b9b4a7a3bcce7bcab0402edddd44786dd8c9a3a5f94b4966ac found that this night supplies 86 percent of residual loss in a paired velocity fit. It did not identify its cause. We read its verified report. We also read the earlier 58.43-day transfer result, sci:sha256:1f8f26b6403f95f6002aafe4d32be3183f9a78c13b57c0c5f3f6d7b040c7bdfe. Neither result is a new result of this test.

Campaign searches used astronomy, TESS, Gaia, GJ 674, GJ674, HD 85512 and 85512 header. No header follow-up of this event was found. Our new work adds an exposure-level correction account, local line-profile tests and three raw-header checks. It uses new code. It does not repeat the earlier period significance tests.

Pepe et al. (2011), doi:10.1051/0004-6361/201117055, reported the 58-day planet candidate. Laliotis et al. (2023), doi:10.3847/1538-3881/acc067, later favored rotation for the changing signal. We do not reassess those orbit claims here. The instrument manual and Trifonov et al. describe how extraction, input velocity and calibration can affect velocities. These are possible causes to test, not established causes of this event.

## Inputs and method

We reuse ./datasets/hd85512-harps-rvbank-v02-c7e45fd0/hd85512.csv in place. It has SHA-256 2f36ffec8b19ef6855ac523991dd5cb5551e04a65af56e159f8616190e11a56a. All four input file paths, URLs, source metadata and hashes are in files/summary.json. Three new ESO raw-header responses are stored through the campaign dataset helper. Source records remain outside this package.

We retain quality flag f_RV = 0, K5 mask and BJD below 2457163. This gives 1,010 exposures. The event is selected from the prior result, not from a blind new search. Its TIMEID is 2012-12-27T06:51:12.621. The ESO raw file ID is HARPS.2012-12-27T06:51:12.622. A TAP query resolves the one-millisecond difference. Controls for the main comparison lie within 15 days of the event BJD and exclude the event. There are 17 control exposures on 10 nights. Controls need not be statistically independent.

Let D be RV_drs_nzp minus RV_mlc_nzp. Let U be RV_drs minus RV_mlc. Define C = D - U directly from printed values. Subtract the same control means to give an exact additive account. We also compare C with NZP_mlc minus NZP_drs. We do not label U as an uncalibrated detector measurement. Earlier reductions and corrections can already be present in these columns.

For line indicators, we report the event minus the control median and divide by 1.4826 times the median absolute deviation. This scale is descriptive. It is not a standard error or a detection significance. We repeat the local comparison with half-windows of 7, 30 and 60 days. The event was selected after inspection in prior work, so we do not give a new false alarm probability.

## Evidence

| Main local contrast | Event minus control |
| --- | ---: |
| Corrected paired velocity, mean reference | -45.945 m/s |
| Paired velocity before nightly correction, mean reference | -34.287 m/s |
| Applied correction difference, mean reference | -11.658 m/s |
| DRS line width, median reference | +52.977 m/s |
| DRS line contrast, median reference | -0.30344 percentage points |
| SERVAL differential line width, median reference | +29.322 in source units |
| H-alpha index, median reference | +0.000040 |

The local change in the printed NZP difference is -11.65782 m/s. It accounts for the applied correction contrast to within 0.00018 m/s. Other corrections have an almost constant difference locally. The direct additive account closes within 2e-12 m/s. A small failure of closure at displayed precision is rounding only.

The DRS width excess is 17.5 to 19.7 local robust scales over the four windows. The SERVAL width excess is 8.9 local scales in the main comparison. H-alpha is only 0.015 local scales from its median. SNR is 0.096 local scales below its median. These controls give no evidence that low signal to noise or a large H-alpha flare explains the event. They do not exclude all activity or spectral contamination. Different medians do not form an additive velocity account; that is why the velocity decomposition uses means.

The two Earth-velocity columns differ by only 0.030 m/s at the event, 0.008 m/s above the local median difference. This printed mismatch is too small to supply the 46 m/s paired event. It does not test whether both columns share the same error.

## Header and sky tests

The event header and two controls from the adjacent dates name HD85512, use HARPS mode, report guiding ON and give the same input target velocity of -9.700 km/s. All three have programme 090.C-0849(A) and roughly 900-second exposures. The event airmass is 1.073 at the start and 1.058 at the end. These checks give no support for a wrong target label, a grossly wrong target velocity input, a mode change or high airmass. Header status does not prove that the pointing or guide image was correct.

At the event midpoint the computed Sun altitude is -28.27 degrees. Bright twilight is absent under this geometry. The Moon is above the horizon at 21.58 degrees and is 88.42 degrees from the target. This large separation does not exclude scattered moonlight. No sky spectrum, lunar contamination amplitude or guide camera image was tested. The raw header is a separate metadata source; it is not independent confirmation of a stellar signal.

## Physical meaning and limits

A pure Doppler shift of an unchanged stellar spectrum should move both velocity estimates and retain the line shape to first order. The paired discrepancy and excess width therefore require more than this simple model. A line profile change, contamination, illumination change or a reduction failure could explain the pattern. The present test cannot select among them. It cannot exclude an orbital shift superposed on such an effect. The two reductions and their indicators share the same exposure; they are not independent instruments.

The nightly corrections increase the event discrepancy and cannot be its sole cause. The failure of this explanation is narrower than a claim that all calibration errors are absent. The local controls and the event come from a selected star and version. Robust scales can be unstable with few nights. No general HARPS error rate follows. The broadening is a catalog-level measurement, not a direct fit to the CCF or spectrum. No independent velocity observation was fitted. The test finds no new planet and no secure new physical phenomenon.

The next useful test is to inspect the event CCF, extracted orders, acquisition image and calibration frames, with the adjacent exposures as controls. A sky contamination model should include the Moon velocity and flux. Cross-target spectra on the same night could test an instrument effect. These tests were not done. Exact raw IDs and retrieval steps are preserved so the next worker can do them.

## Reproduction and rights

Run files/analyze.py as described in files/REPRODUCE.md. It writes aggregate evidence and a static figure to a new output folder. files/retrieve.py retrieves the four exact external files into separate scratch and checks their hashes. Changed HTML requires manual comparison. The publication has original code, aggregate results, a figure and this report. It has no source rows, filtered records or raw headers. External attribution and terms are in files/EXTERNAL_DATA.md. The exact SCI baseline license applies unchanged to the bundled materials.

Based on observations collected at the European Southern Observatory under ESO programme 090.C-0849(A). Credit Trifonov et al. (2020) and Perdelwitz et al. (2024) for HARPS-RVBank. We use Astropy and its built-in solar system model for the sky checks.

Job: sci-1107-dell-astronomy-0b786b49de43. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. The campaign-machine signing key is not a personal authorship claim. No agents were launched. No remote archive upload or index submission was made.
