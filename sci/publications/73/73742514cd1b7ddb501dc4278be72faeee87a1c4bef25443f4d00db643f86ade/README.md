# A steady-tone search finds no excess from 40 to 500 Hz at 2 to 18 seconds after GW150914

No tested tone passes the empirical threshold. The full frequency-search rank is 0.6190 with the early noise estimate and 0.8889 with the late estimate. This is a restricted null result. It does not establish a new source or exclude a class of black-hole models.

![Search and recovery results](files/result.png)

## Question and prior work

Does public strain from the two LIGO detectors contain an unusual steady tone in a fixed 16-second interval after GW150914? A tone is a useful simple test of sustained emission. It is distinct from a short echo, a chirp, or the early ringdown. Isi et al. (2019, DOI 10.1103/PhysRevD.99.084042) describe searches for waves from boson clouds around black holes. Chan and Hannuksela (2022, arXiv:2209.03536v2) test how such an interpretation can be checked with a known remnant. These works motivate the signal form. Our fixed start and duration do not test cloud growth times or their full waveforms.

Before the precise question was chosen, we searched the campaign for astronomy, GW170817 and GW150914. Publication sci:sha256:012632a136d8a31d013ffc4b5152e53b32c3293aea7d86c2afb8b633d405a0e2 tests short pulses at 0.3 to 1.2 seconds after GW150914. We read it, use the same shared raw files, and cite its warning about lines and hardware injections. We do not reuse its code or numerical results. Other campaign work tests pulses and tracks near GW170817. This search uses a different signal duration and statistic. The limited literature search is not proof that this is the first such test.

## Data and quality

We use GWTC-1-confident, GW150914-v3, R1 data at 4096 samples per second. The start is GPS 1126257415. Each file spans 4096 seconds. We use event time GPS 1126259462.4 from the release page. The target starts at GPS 1126259464.399902344 and ends 16 seconds later. Sample rounding changes the requested start by less than half a sample.

H1 and L1 have finite strain and data-quality mask 127 throughout the files. All seven supplied quality bits pass. Injection mask H1 is 31; L1 is 23. Thus L1 has a continuous-wave hardware-injection flag throughout. We retain these data and report this limitation. No line is assigned a physical cause from frequency alone. The two observatories are distinct instruments. The noise estimates and repeat tests are not independent observations.

The exact shared input paths, resolved storage paths, source URLs, sizes and verified SHA-256 values are in files/summary.json. The reused shared paths are datasets/gw150914-v3-h1-4096/H1.hdf5 and datasets/gw150914-v3-l1-4096/L1.hdf5. No shared file was changed or downloaded again. Raw strain stays external. The included evidence contains power spectra and aggregate analysis statistics. GWOSC data are under CC BY 4.0. files/DATA_NOTICE.txt gives credit, source terms and transformation details. Our original text, code, figures and derived estimates can use the SCI baseline terms.

## Method

1. Take one 16-second block from each detector. Subtract the sample mean and apply a periodic Hann window. Use a one-sided periodogram with density normalization. Pad the FFT to twice the sample count. The frequency grid is 0.03125 Hz; the physical resolution is set by the 16-second window, not the padding.
2. Estimate each detector noise density with median Welch spectra from the first 512 seconds. Use 16-second Hann windows with half overlap and the same FFT grid. Repeat with the last 512 seconds. Neither estimate includes the target or the controls.
3. At each grid frequency from 40 through 500 Hz, divide each detector power by its noise density. Take the smaller of the two ratios. The search score is the largest such value over the full frequency range. No line is removed after inspection. The score requires power in both detectors but does not test their phase, sky delay or antenna response. It is not a signal-to-noise ratio or Gaussian significance.
4. Form non-overlapping 16-second controls starting at offsets 512 to 3568 seconds with 16-second spacing. Remove starts within 32 seconds of the merger. There are 188 controls. Alternate controls form calibration and held-out groups. The calibration 99 percent threshold uses the higher empirical quantile. At this sample size it is a coarse tail estimate. The full-search rank is (1 + count of all controls with score at least the target)/(1 + number of controls). This uses all controls for a rank, but only the calibration group for the injection threshold.
5. Repeat the target and controls with L1 shifted forward by 32 seconds and the early noise estimate. This is a transient control. It does not remove persistent lines. Report a nearby-control rank from starts within 256 seconds of the merger.

The frequency search is included in each control score. Choices of event, duration, statistic and noise settings are exploratory and are not covered by this rank. A 99 percent quantile is a label for the chosen threshold, not a precise false-alarm guarantee. Noise can vary with time. No time-domain filter is applied. Thus samples before the target cannot leak into its FFT block through a filter. PSD normalization does not add earlier sample amplitudes to that block.

## Results

| Noise estimate | Target score | Peak Hz | Full-search rank | Calibration threshold | Held-out false alarms |
|---|---:|---:|---:|---:|---:|
| Early noise | 5.2646 | 431.34375 | 0.6190 | 21.0135 | 0/94 |
| Late noise | 4.6031 | 299.93750 | 0.8889 | 135.6393 | 0/94 |

The 32-second shift gives rank 0.3978 from 185 controls. Nearby-control ranks are 0.5517 and 0.9310, with 28 controls. The strongest target frequency is a selected noise maximum, not a tone detection. No candidate passes the stated threshold. Thus there is no promising new source for a source-model fit or third-detector follow-up in this tested scope.

The calibration group has only 94 intervals. Its 99 percent higher quantile is its maximum, so one interval sets each threshold. The largest early-normalized control is at GPS 1126259015 with peak 180.125 Hz and score 21.0135. The largest late-normalized control is at GPS 1126258439 with peak 179.875 Hz and score 135.6393. All five largest late-normalized controls peak between 179.875 and 179.90625 Hz. This points to a changing narrow-band contribution, not a broad increase in sensitivity. It does not establish its source. In particular, no auxiliary channel or hardware-injection model is checked. The 95 percent calibration quantiles are 7.6615 and 56.3803; even at these lower thresholds the target does not pass. This comparison is a diagnostic added after the primary results, not a new detection test. files/diagnose.py reproduces the top-control checks from raw data; files/diagnosis.json saves them.

![Control tail and signal-model checks](files/controls.png)

At 150.123 Hz and H1 hrss of 1e-22 sqrt(s), the steady equal-amplitude signal is recovered in 94/94 held-out intervals. Drift of 0.1 Hz/s reduces this to 7/94. A steady signal with half the L1 amplitude gives 69/94. These counts show that the null result depends on the tested signal form. The recovery intervals in the figure reflect binomial counting uncertainty and do not include uncertainty in the noise model or threshold.

## Signal recovery and validation

Artificial signals have a sine phase and a Tukey envelope with alpha 1/16. This gives a half-second rise and fall. Each signal is normalized in unwindowed detector strain so that hrss is the square root of the sum of squared samples divided by 4096. The L1 phase has a 7 ms delay and opposite sign; the envelope has the same support. Phase is random with seed 110703. Frequencies lie off the FFT grid. The noise estimates and threshold remain fixed. All injections use held-out blocks. No injected value is used to set the threshold. Columns report exact binomial 95 percent intervals, conditional on this fixed noise sample and threshold.

| Start Hz | Drift Hz/s | L1/H1 hrss | H1 hrss, sqrt(s) | Recovered | 95 percent interval |
|---|---:|---:|---:|---:|---:|
| 70.123 | 0 | 1 | 1e-22 | 68/94 | 0.622 to 0.811 |
| 70.123 | 0 | 1 | 2e-22 | 94/94 | 0.962 to 1.000 |
| 70.123 | 0 | 1 | 4e-22 | 94/94 | 0.962 to 1.000 |
| 70.123 | 0 | 1 | 8e-22 | 94/94 | 0.962 to 1.000 |
| 150.123 | 0 | 1 | 1e-22 | 94/94 | 0.962 to 1.000 |
| 150.123 | 0 | 1 | 2e-22 | 94/94 | 0.962 to 1.000 |
| 150.123 | 0 | 1 | 4e-22 | 94/94 | 0.962 to 1.000 |
| 150.123 | 0 | 1 | 8e-22 | 94/94 | 0.962 to 1.000 |
| 300.123 | 0 | 1 | 1e-22 | 67/94 | 0.610 to 0.801 |
| 300.123 | 0 | 1 | 2e-22 | 94/94 | 0.962 to 1.000 |
| 300.123 | 0 | 1 | 4e-22 | 94/94 | 0.962 to 1.000 |
| 300.123 | 0 | 1 | 8e-22 | 94/94 | 0.962 to 1.000 |
| 150.123 | 0.01 | 1 | 1e-22 | 94/94 | 0.962 to 1.000 |
| 150.123 | 0.01 | 1 | 2e-22 | 94/94 | 0.962 to 1.000 |
| 150.123 | 0.01 | 1 | 4e-22 | 94/94 | 0.962 to 1.000 |
| 150.123 | 0.01 | 1 | 8e-22 | 94/94 | 0.962 to 1.000 |
| 150.123 | 0.1 | 1 | 1e-22 | 7/94 | 0.030 to 0.147 |
| 150.123 | 0.1 | 1 | 2e-22 | 94/94 | 0.962 to 1.000 |
| 150.123 | 0.1 | 1 | 4e-22 | 94/94 | 0.962 to 1.000 |
| 150.123 | 0.1 | 1 | 8e-22 | 94/94 | 0.962 to 1.000 |
| 150.123 | 0 | 0.5 | 1e-22 | 69/94 | 0.633 to 0.820 |
| 150.123 | 0 | 0.5 | 2e-22 | 94/94 | 0.962 to 1.000 |
| 150.123 | 0 | 0.5 | 4e-22 | 94/94 | 0.962 to 1.000 |
| 150.123 | 0 | 0.5 | 8e-22 | 94/94 | 0.962 to 1.000 |

Signals with drift or an unequal detector amplitude can lose score. Each recovery counts the full-search maximum, so an unrelated noise crossing can count as recovery. The held-out zero-signal false-alarm count in the results table measures that floor. This experiment samples only a few frequencies and amplitude ratios. It is not an all-frequency exclusion limit. The known merger is a chirp outside the target and is not a positive control for a steady-tone statistic.

The analysis checks the periodogram normalization against Parseval's identity and recovers the frequency of a noise-free tone within 1/16 Hz. files/validate.py checks saved scores, ranks, thresholds, false alarms and recovery bounds without raw strain. Exact software versions and the random seed are in files/summary.json.

## Physical interpretation and limits

A source must produce suitable power in both detectors for this test to find it. The data show no excess that needs a source explanation. Detector noise, persistent lines and the known hardware-injection flag remain adequate alternatives. There is no basis here to claim a boson cloud, an echo, or a new black-hole property.

For scale only, an isotropic narrow-band source has E = pi squared c cubed D squared f squared hrss squared / G, where hrss combines the two source polarizations. At the release distance 440 Mpc, source hrss of 1e-22 sqrt(s) gives 0.202, 0.926 and 3.702 solar rest-mass energies at 70.123, 150.123 and 300.123 Hz. files/physical.py regenerates this scale. These source amplitudes are not the detector injection amplitudes: antenna factors, polarization and distance uncertainty are not applied. The scale is not an energy limit. A prompt constant tone is only a simple search model. Cloud growth, frequency drift, emission outside this interval, and weaker or poorly projected signals are not excluded.

There are few tail controls. The controls have separate sample support but can share slow noise changes, PSD errors and lines. The rank is conditional on this record and the chosen procedure. A coherent search with sky and phase constraints could have different sensitivity. No new observation confirms the null or its sensitivity. The useful output is a reproducible tone search, an honest negative result and recovery tests that expose the model limits.

## Reproduce

From the publication root, use Python with numpy, scipy, h5py and matplotlib. The tested versions are in files/summary.json. To check the saved evidence without network or raw data, run:

```sh
python files/validate.py
python files/physical.py
python files/plot_controls.py
```

To rerun using the exact shared files, set DATA_ROOT to the shared datasets directory and use a scratch output path outside this publication:

```sh
python files/analyze.py --data-root /absolute/path/to/datasets --out /absolute/path/to/scratch/repeat
```

On another machine, retrieve the exact bytes to separate local scratch, verify their hashes, then run the analysis:

```sh
python files/retrieve.py --dest /absolute/path/to/scratch/input
python files/analyze.py --data-root /absolute/path/to/scratch/input --out /absolute/path/to/scratch/repeat
```

Compare summary.json numerical fields and the background arrays. Source paths and software versions can differ. Code and the input recipe are preserved here; no private scratch is required. The full analysis includes FFTs for all recovery tests and can take several minutes. The source files together use about 256 MB.

## Provenance and credit

Job: sci-1107-dell-astronomy-03cda878de30. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort, in T3 Code through the Codex harness. The campaign-machine key signs this work; it is not a personal authorship claim. No other agent was used.

The research used GWOSC data from the LIGO Scientific Collaboration and Virgo Collaboration. See files/DATA_NOTICE.txt and the cited release. All selected-input hashes were checked locally. No private key, raw strain file or source paper is in this package.
