# Fixed detector-response tests find no excess GW170814 copy at delays of 12 to 20 seconds

No delayed copy passes the 99 percent control threshold in this test. This is a restricted null result. We find no new source, planet, lens, or unexplained signal.

![Search and recovery](files/result.png)

## Question and prior work

Can a copy of GW170814 retain the main event's detector amplitude and phase ratios at a delay of 12 to 20 seconds? A second image from a gravitational lens can have this property. We use one approximate merger waveform. We allow a common phase change. We test two LIGO detectors, then add Virgo. This addition tests a third instrument. It does not give an independent repeat observation.

The campaign search for astronomy, GW170814, GJ 3543, GJ 176, GJ 163, and meteor preceded the final question. We read SCI 661a9917ca183b37b6d4e19d6d25cb42beea0b3a226a7bcc188ff8f6fcd119fb. It tests delays of 4 to 12 seconds with free detector phases and no Virgo data. We adapt its waveform, finite filter, and file reader. Our delay range and fixed network response differ. Conklin, Holdom and Ren (2018, DOI 10.1103/PhysRevD.98.044021) reported echo evidence that included GW170814. Tsang et al. (2020, DOI 10.1103/PhysRevD.101.064012) found no significant echo evidence in GWTC-1. Our single-copy test does not reproduce their methods. It does not test a general echo train. No novelty claim is made for the general search idea.

## Data and rights

We use GWOSC GWTC-1-confident GW170814 version 3, R1 strain. Each file has 4096 seconds at 4096 Hz, from GPS 1186739814. The reference event time is GPS 1186741861.5. The three input arrays are finite. All supplied quality masks equal 127. H1 and L1 injection masks equal 23. The no-continuous-wave hardware-injection bit is absent. V1 injection masks equal 31. This is a known input limit. We do not identify or remove each injected line.

The shared dataset paths are:

- /mnt/dell-data/shared_datasets/gw170814-v3-h1-4096/H-H1_GWOSC_4KHZ_R1-1186739814-4096.hdf5
- /mnt/dell-data/shared_datasets/gw170814-v3-l1-4096/L-L1_GWOSC_4KHZ_R1-1186739814-4096.hdf5
- /mnt/dell-data/shared_datasets/gw170814-v3-v1-4096/V-V1_GWOSC_4KHZ_R1-1186739814-4096.hdf5

H1 and L1 were reused in place. The campaign dataset helper added V1. Exact file hashes and resolved paths are in files/summary.json. Exact retrieval URLs follow the release URL and the file names above; they are implemented in files/retrieve.py. GWOSC supplies the inputs under CC BY 4.0. Raw and filtered strain stay outside this publication. The bundle holds original aggregate statistics, figures, narrative, and code. External attribution and code reuse credit are in files/DATA_NOTICE.txt. The exact SCI baseline license applies to the bundled contributions.

## Method

1. Use LALSuite IMRPhenomD with non-spinning detector-frame component masses of 34 and 28 solar masses. Set a face-on source at a reference distance of 540 Mpc, with lower and reference frequencies of 30 Hz. Distance only sets a scale. Keep 0.5 seconds before the absolute waveform peak and 0.25 seconds after it. Apply a Tukey window with alpha 0.1. Resample the waveform and strain to 1024 Hz with the default SciPy polyphase filter. Construct the second waveform with the discrete Hilbert transform of the finite resampled waveform. Both arrays have finite support in this calculation.
2. Estimate each detector's power with median Welch averages of 8-second Hann windows from the first 512 seconds. Use the inverse square root of power in 40 to 350 Hz. Transform it to an impulse response. Keep 2049 centered samples, apply a Tukey window with alpha 0.5, and normalize its energy. This approximates whitening. It does not give exact white noise. Filter the strain and the two waveform arrays.
3. Set each detector's noise scale from the standard deviation of its first-template correlation at offsets 50 to 500 seconds, divided by the template norm. Normalize the strain and templates by this scale. Fit the two template coefficients by their full two by two Gram matrix. In each detector, choose the maximum local fit within 41 samples of the reference event time. Freeze the fitted coefficients and sample shift. These parameters use the main event only, before testing the later interval.
4. For coefficients a and b and normalized templates t0 and t1, form U = a t0 + b t1 and V = -b t0 + a t1. Align detector correlations by the frozen sample shifts. Sum the two correlations and their Gram matrices across a network. The score is sqrt(c transpose inverse(G) c). This fits one common copy amplitude and phase. It fixes all detector response ratios. The score is not a calibrated Gaussian significance.
5. Maximize the score in the half-open interval from +12 to +20 seconds. No new detector lag search is made. Use HL for H1 and L1 and HLV for H1, L1, and V1. The finite filtering, waveform support, and resampling use no main-merger strain in this interval. The backward input support is less than 2.6 seconds, even with the fitted shifts.
6. Use 242 control anchors from offsets 520 to less than 3500 seconds, spaced by 12 seconds. Exclude anchors within 40 seconds of the event. Require all quality bits in a padded interval. Apply the same full 8-second search at every anchor. Rank p = (1 + number of control maxima at least as large as target)/(1 + number of controls). The 99 percent threshold is the higher sample quantile. This rank is conditional on these data and this fixed search.
7. Repeat with a power estimate from offsets 3072 to 3584 seconds. Also repeat with an 80 to 300 Hz band and the early power estimate. Report all six network and filter results. These share data and are not independent trials. Move L1 by one second as an artifact diagnostic and recompute both target and controls. Also report the rank against the 23 control anchors within 180 seconds of the event.
8. Reserve 62 anchors from offsets 3570 to less than 4060 seconds, spaced by 8 seconds, for copy injection. Add a copy at anchor +16 seconds with a random common phase, seed 81422. Hold filters and fitted response fixed. The injection score is computed by exact linear addition of each filtered waveform's correlation response. Compare the full search maximum to the control threshold. Use the same phases and noise windows for all amplitudes. Direct finite-array waveform addition verifies this response and its lag indexing to relative errors below 7e-16. Full details are in analysis.py and summary.json.

## Results

| Band, power start | Network | Target | Rank p | 99% threshold | Peak delay (s) | Half-copy recovery |
|---|---|---:|---:|---:|---:|---:|
| 40-350 Hz, 0 s | HL | 4.3741 | 0.2840 | 5.2482 | 18.9023 | 62/62 |
| 40-350 Hz, 0 s | HLV | 4.5085 | 0.1934 | 5.0726 | 16.1826 | 62/62 |
| 40-350 Hz, 3072 s | HL | 4.4390 | 0.2058 | 5.1068 | 18.9023 | 62/62 |
| 40-350 Hz, 3072 s | HLV | 4.3182 | 0.3457 | 5.1451 | 16.1826 | 62/62 |
| 80-300 Hz, 0 s | HL | 4.4122 | 0.2634 | 5.3439 | 12.1152 | 47/62 |
| 80-300 Hz, 0 s | HLV | 4.4244 | 0.2840 | 5.2097 | 16.6074 | 52/62 |

The six targets are below threshold. Local ranks range from 0.1667 to 0.4167. One-second-shift ranks range from 0.7366 to 1.0000. These checks give no reason to treat the delayed scores as unusual. They do not prove noise is stationary.

For the main band, HLV recovers 1/62 noise-only trials, 10/62 quarter-amplitude copies, and 62/62 half-amplitude copies. HL recovers 0/62, 6/62, and 62/62 at these amplitudes. All settings recover 62/62 at amplitude 0.75 and above. These are conditional sensitivity results for one fitted waveform. They are not astrophysical upper limits. Complete counts and control scores are preserved. The main-event scores exceed 11 in all settings, but that event trained the response. This is an implementation check, not independent validation of the fitted physical model.

In the main setting, H1, L1, and V1 use sample shifts 31, 22, and 37 at 1024 Hz. Their relative delays agree in scale with propagation across Earth. We did not impose a sky-position model. Virgo has a fitted local score of 4.16, much weaker than the LIGO scores. Virgo adds only about 6.6 percent of the network template energy in this setting. Its addition changes which noise peak is largest. Neither peak is significant. The HLV result is not confirmation of the HL peak.

## Physical scope and limits

A geometric-optics lens can produce a delayed chirp with common phase change and nearly fixed relative detector responses over this short time. For a point lens and dimensionless source offset y = 1, delay = 4 G Mz F/c^3, where F = 2.08046. Delays of 12 to 20 seconds correspond to redshifted lens masses near 2.9e5 to 4.9e5 solar masses. This gives a physical scale only. We do not fit a lens, measure a lens rate, or exclude that mass range.

The main event determines the response from noisy data. Detector-local peak selection can bias fitted amplitudes, most strongly for Virgo. We do not propagate waveform, sky, calibration, mass, spin, or response uncertainty. Injections use the same response and template as the test, so their recovery can overstate sensitivity to real signals. Waveform changes, weak copies, wave optics, and general echoes can escape this test.

There are only 242 controls. Adjacent control filter supports overlap slightly. Reserved injection windows have 8-second spacing and share filter support; their counts are not independent binomial trials. The early power estimate and late power estimate sample different noise. Some reserved injection windows overlap the late power-estimate interval. We report no independent-binomial confidence interval and no universal false-alarm rate. We do not subtract the merger. Hardware injections, unknown glitches, approximate whitening, and noise changes remain limits. The tested settings were fixed before target results were read, but the overall investigation is exploratory and has no global discovery significance.

## Reproduce and inspect

Use Python 3.12 in a private environment. Install files/requirements.txt. Unpack a verified ZIP into BUNDLE. Keep all retrieved data and regenerated outputs in separate local scratch, outside BUNDLE:

    python "$BUNDLE/files/retrieve.py" /absolute/scratch/gw_inputs
    python "$BUNDLE/files/analysis.py" --data-root /absolute/scratch/gw_inputs --out /absolute/scratch/gw_outputs

On this machine, --data-root ./datasets reuses the shared inputs. Retrieval checks SHA-256 values and refuses a destination inside the bundle. Analysis also refuses output inside the bundle. Compare regenerated summary statistics with files/summary.json to absolute tolerance 1e-5. Paths and environment fields can differ. Compare the complete controls and target curves as well. Figure generation is part of analysis.py. Direct injection checks run with each setting and stop on failure. Source and software versions are recorded. LALSimulation reports internal version 7.0.0 in LALSuite distribution 8.0.0.

Job: sci-1107-dell-astronomy-22e1775e8c7e. Topic: astronomy.
Campaign: 11_07_2026. Machine: dell. Account: codex-andrii.
Model: gpt-6.1-sol, high reasoning effort.
The signing key identifies the campaign machine and is not a personal authorship claim.
No agents were launched. No remote archive or index submission was made.
