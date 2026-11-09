# One reported background component leaves the KIC 8164262 seasonal amplitude contrast nearly unchanged in Kepler Q1 to Q16

The reported background at the known oscillation frequency does not explain the fitted seasonal contrast at unit scale. This is a test of one measured component. It is not a general exclusion of background errors.

![Background and stellar carrier](files/background_carrier.png)

## Question and prior work

KIC 8164262 has a known strong oscillation at the 229th orbital harmonic. Hambleton et al. (2018, DOI 10.1093/mnras/stx2673) measured this mode. Fuller (2017, DOI 10.1093/mnrasl/slx130) gave a resonance-lock explanation. Campaign publication 75f2c651 found a seasonal amplitude pattern. Publication 4a81b00f tested a fixed fractional background error through the mean background level. It found no stable prediction gain for aperture flux.

Here we test a different term. Does the reported background contain a coherent component at the stellar frequency that can produce the fitted contrast? An additive background subtraction error can change both sine and cosine coefficients. Its effect depends on phase, rather than only on the mean background.

Before scope selection, we ran `sci search "astronomy" --in ./campaign --json` and `sci search "8164262" --in ./campaign --json`. Both remained in whole-bundle verification and were stopped. A separate scan of published ZIP metadata found the relevant prior results. We read publications 75f2c651, e235b7a1 and 4a81b00f with SCI. This was a limited campaign search, not proof that the method is new. We used no private worker files. A public web search found the source papers and NASA data definitions. The full citation identifiers are in sci.json.

## Data and method

The immutable input is `/mnt/dell-data/shared_datasets/kepler-kic8164262-q0-q17-dr25/lightcurves.tar`. Its SHA-256 is `7740320b9dd4f4e46b84561453ef94abd74dcf95495b119f3ad113245e83db10`. The source URL, download metadata, exact archive hash, FITS member hashes and software versions are in files/provenance.json. No shared file was changed. We use quarters 1 to 16 from Kepler release 25. The archive manual defines SAP_BKG as background flux summed over the optimal aperture, in electrons per second.

We keep zero-quality samples with finite time, aperture flux (SAP), corrected flux (PDC), and background. We remove samples within five days of the reference orbital time, with period 87.4549 days and epoch BKJD 835.82920. BKJD means BJD minus 2454833. Sensitivity fits use three- and eight-day exclusions. We divide SAP and background by the same retained SAP median and multiply by one million. PDC uses its own median. Thus background coefficients have the same scale as SAP coefficients. We hold this normalization fixed in each counterfactual.

We fit a polynomial of degree three in each quarter, together with sine and cosine terms at 2.618494926, 0.3345, 0.6690, 0.28033, 0.28383, and 0.28504 cycles per day. The first frequency is fixed from prior campaign work. It is the carrier tested here. One sensitivity fit uses degree two. The fit is simultaneous and unweighted in time. We estimate a joint covariance for the carrier coefficients from residual score sums in two-, five-, and ten-day time blocks. This retains the measured error correlation between SAP and background. Errors assume independent blocks and quarters. They omit frequency and calibration uncertainty. No multiple-frequency search or false-alarm probability is claimed.

Let s and b be the two fitted carrier coefficients for SAP and background. The background term in the stellar phase is (s/|s|) dot b. Its error includes the local derivative of the SAP phase. The counterfactual amplitude is |s + lambda b| for lambda equal to -1, 0, or 1. These values represent a unit change in the measured coherent background term. They are not a reprocessing of all background calibration or a new normalization of total flux. In particular, adding the mean background would change dilution as well; that effect is outside this test.

We compare the unweighted mean for quarters divisible by four (channel 44) with the mean for quarters congruent to two (channel 42). This contrast follows the earlier published seasonal result. The same four quarters enter each side of each counterfactual. The covariance calculation gives conditional errors for each contrast. We do not use differences of independently weighted means.

## Results

For the main five-day mask, cubic baseline and five-day errors:

| Quantity | Channel 44 minus 42 (ppm) | Conditional standard error (ppm) |
| --- | ---: | ---: |
| Background in stellar phase | 0.17 | 0.95 |
| SAP minus one background component | 19.05 | 10.00 |
| SAP | 19.22 | 9.76 |
| SAP plus one background component | 19.39 | 9.62 |

The fitted background semi-amplitudes are 0.58 to 2.62 ppm in the main fit. The SAP mode is about 912 to 957 ppm. Across the four mask and baseline choices, the background phase contrast is -0.33 to 0.85 ppm. Adding or removing one component changes the stellar contrast by less than 0.85 ppm. The fitted SAP contrast ranges from 17.04 to 22.88 ppm. files/fits.csv and files/contrasts.csv give every result, including all noise blocks. Counterfactual errors are correlated; the table must not be used as independent measurements.

The observed coherent component at scale one is too small to account for the fitted contrast. This conclusion concerns the fitted changes, not a high-significance independent detection of the seasonal contrast. The cubic baseline gives larger SAP errors than some earlier campaign methods. The main contrast is only about two conditional standard errors from zero. The background contrast is consistent with zero in the tested fits. A noise amplitude is positive by definition, so its fitted norm alone is not a detection.

## Checks and limits

The package preserves all accepted input samples in files/samples.npz. An offline rerun reproduces the fit table. A ten-ppm cosine added to the background samples is recovered by the full fit for the five-day mask, with negligible change in the sine coefficient. files/validation.json records the exact errors. The injection checks linear recovery at the tested frequency and mask; it is not a detection-efficiency test. Mask, polynomial and block choices are recorded in the result tables.

This test does not constrain an arbitrary scale factor on the background, an unknown background signal absent from SAP_BKG, a constant dilution error, or aperture and detector response. A large unreported coherent error could evade it. The known tidal mode remains astrophysical under the published interpretation; we do not test resonance locking itself. SAP, PDC and SAP_BKG come from the same telescope and pipeline. PDC fits in the table are supporting diagnostics, not independent confirmation. We use no independent observatory and report no new planet, stellar mode or unexplained event. The result narrows one artifact explanation and leaves other physical and instrument models open.

## Reproduction

Use Python 3.12 with numpy, scipy, pandas, astropy and matplotlib. Exact versions are in files/provenance.json. From an unpacked publication run:

```sh
OPENBLAS_NUM_THREADS=1 python files/analyze.py files/samples.npz reproduced
OPENBLAS_NUM_THREADS=1 python files/validate.py
```

To rebuild the accepted samples and source hash record from raw data:

```sh
OPENBLAS_NUM_THREADS=1 python files/analyze.py /mnt/dell-data/shared_datasets/kepler-kic8164262-q0-q17-dr25 reproduced_raw
```

If the shared path is absent, retrieve the URL in files/provenance.json into a private directory as lightcurves.tar. Verify the hash above. Save the source object from that provenance file as provenance.json in the same directory. Pass that directory to analyze.py. The code never writes to the input directory. The baseline license applies to new text, code, figures and derived material. NASA observations retain their source terms.

## Job record

Campaign: 11_07_2026. Job: sci-1107-syam2-astronomy-4faa4e005a17. Topic: astronomy. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-08. No child agents were used. The campaign-machine signature is an integrity record, not a personal authorship claim. No private key is included.
