# A frozen two-component size fit gives no clear NICER gain for 23 PSR J0537-6910 glitches

A density with two components fitted to 45 RXTE glitches gives almost the same predictive score as one positive Gaussian for 23 NICER glitches. The total log score gain is 0.0228 natural-log units. The mean gain is 0.0010 per event. Its fixed-fit, two-event block resampling range is -0.111 to +0.151. Thus this test gives no clear predictive gain for the mixture. It does not exclude two physical mechanisms. No new glitch or planet is reported.

![Frozen density test](files/density_test.png)

## Question and new contribution

Does a distribution with two components transfer from the RXTE size sample to the NICER size sample of the same pulsar? A glitch is a sudden increase in spin frequency. Two preferred sizes could reflect different pinning regions or triggers in a neutron star. A flexible density can also fit sample noise or selection effects. A test with fixed parameters and another detector helps separate these possibilities.

Anantharaman and Bhattacharya (2025, doi:10.1093/mnras/staf702) compared size distributions and vortex models. Their preferred fit combined a lognormal and a Gaussian. Our test uses this model family, but does not copy their fitted parameters or reproduce their binned fit. We use normalized event likelihoods and a separate instrument sample. This is a new transfer test, not a claim of priority for a mixture model. Their paper predates the full NICER report, but most NICER events here occurred before that paper. This is a retrospective detector split, not a prospective test after publication.

The campaign search covered astronomy, glitch, glitch activity, 0537 reservoir, Bactrian and glitch bimodal. No direct campaign test of this density transfer was found. The waiting-time benchmark (sci:sha256:dec316e468d04b7950a02bcad2db1ebae205b83d9bc304af18585cb03d331199) defines the same instrument split. The catalog audit (sci:sha256:f48c1887d72bbc7e752d8d462b64feaabfce70699f90a482ae721f1ce718952f) shows that catalog revisions can add events. The serial-wait and residual tests (sci:sha256:e05475b196c7539c29da1a0b6c60a4d02dc66d882530a65ac165cb97913850e9 and sci:sha256:2d88dba3bd143944192e0c1905947bac117ab63c10c219dfa6198cb996b4d7bb) show limits from small samples and timing errors. We read these reports. We wrote new code and did not use private worker files.

## Inputs and selection

We read two existing shared HTML snapshots in place. The old Jodrell Bank table is the Internet Archive capture 20180723174303. Its 45 J0537-6910 rows span MJD 51278 to 55819. The current shared snapshot has 23 rows with epochs above MJD 58000, from 58083 to 60762. These are the NICER sample. We include every size in each group, including the final event. A size-density test needs no next event. We do not use the long gap as a waiting time. We do not select sizes by error or significance. No new raw input was downloaded.

The shared name jbo-glitch-table-20261104 is not a formal release date. Its provenance records retrieval on 2026-11-08. Exact bytes define our version. The older training snapshot avoids adding later catalog revisions to the training list. Thus the training data have 45 events, not the 47 historical events in the newer table. Extraction requires exactly 45 and 23 events and checks both file hashes before use. Source units are fractional frequency steps in 10^-9. For numerical work x is the catalog size divided by 100, so x is the fractional step in 10^-7. No conversion to absolute frequency is made.

The source catalog requests attribution to Espinoza et al. (2011, doi:10.1111/j.1365-2966.2011.18503.x), Basu et al. (2022, doi:10.1093/mnras/stab3336), and https://www.jb.man.ac.uk/pulsar/glitches.html. The RXTE study is Antonopoulou et al. (2018, doi:10.1093/mnras/stx2429). The full NICER report is Ho et al. (2026, arXiv:2512.19800v1). The catalog and those papers are not independent measurements of the same events.

## Fixed models and test

We fit four densities to RXTE only: a Gaussian restricted to x > 0, a lognormal, a gamma, and a mixture of a lognormal and a positive Gaussian. The primary contrast is the mixture against the positive Gaussian. The other single densities check whether the result depends on an unsuitable reference. This choice follows inspection of prior work and was made before fitting. It was not registered.

For the positive Gaussian, p(x) = phi((x-m)/s) / (s Phi(m/s)), for x > 0. For the lognormal, log(x) has a Gaussian density. The mixture is w times the lognormal plus (1-w) times the positive Gaussian. We maximize the sum of log densities of individual events. This is not a fit to histogram counts. All models are normalized on positive sizes. The model names normal and mixture in the code refer to these positive densities.

The positive Gaussian bounds are m in [-5,10] and s in [0.05,10]. The mixture bounds are w in [0.05,0.95], lognormal log-mean in [-6,3], log-standard deviation in [0.05,4], Gaussian m in [0,10], and Gaussian s in [0.05,10]. These bounds control singular components. Twelve fixed-seed starts fit the main mixture. A 64-start check agrees to less than 10^-5 log-likelihood units. Width-floor checks use 24 starts. Parameters are held fixed for all NICER scores. Mixture component count does not imply density mode count or a physical reservoir count.

For each NICER event, d is log(p_mixture) minus log(p_reference). We report the mean and sum. A circular block resampling of d uses blocks of 1, 2 and 4 events, with 20,000 draws for each contrast and block length. The primary range uses blocks of 2. This retains short order dependence but assumes a stationary event sequence. These percentile ranges describe sampling under that rule; they are not exact physical confidence intervals. They omit training uncertainty.

A second check resamples the 45 training sizes independently, refits both primary models, and resamples the NICER events in blocks of 2. It uses 150 draws and 4 mixture starts per draw. Its tails are coarse. It includes some training uncertainty under independent training draws, but not all dependence, model error or selection uncertainty. It is a sensitivity check, not a calibrated probability that either mechanism is true.

## Results

Log scores below use x in units of 10^-7. A common change of units shifts all log scores equally, so score differences do not change.

| RXTE model | Training BIC | NICER total log score | Mixture minus model, mean |
| --- | ---: | ---: | ---: |
| Positive Gaussian | 169.609 | -44.157 | 0.0010 |
| Lognormal | 206.558 | -54.086 | 0.4327 |
| Gamma | 180.822 | -47.637 | 0.1523 |
| Lognormal plus positive Gaussian | 172.244 | -44.134 | 0 |

The mixture improves training log likelihood by 4.393 over the positive Gaussian, but its three extra parameters give a higher BIC by 2.634. This small difference is descriptive. Mixture fits have nonregular parameter boundaries, so a BIC difference must not be read as a calibrated odds ratio here.

The fitted mixture weight of the lognormal is 0.1111. Its log-mean and log-standard deviation are -2.8119 and 1.1805. Its positive Gaussian has m = 2.6857 and s = 1.5953. The single positive Gaussian has m = 1.8559 and s = 2.0844. The m and s parameters are those of the parent Gaussian, not the mean and standard deviation after restriction. All fitted parameters are in files/summary.json.

The mixture has numerical density maxima near catalog sizes 1.51 and 268.43 on a fixed grid from 0.01 to 1000. The much smaller peak comes from very small glitches; it is not evidence for two comparable peaks among large glitches. Modes depend on the size coordinate. These modes refer to density in linear fractional size, not density in log size.

The primary mean gain ranges are -0.127 to +0.158 for blocks of 1, -0.111 to +0.151 for blocks of 2, and -0.099 to +0.122 for blocks of 4. All include zero. The joint training/test check gives -0.318 to +0.100; 26 percent of its 150 draws have positive gain. That fraction is not a posterior probability. Leaving one NICER event out at a time gives mean gains from -0.0602 to +0.0233. Removing the sole event below 50 catalog units gives -0.0602 on 22 events. The result depends strongly on this small-size part of the sample.

The mixture clearly improves the conditional score over the single lognormal under all three block checks. This does not support bimodality because the positive Gaussian gives almost the same score. The gamma contrast is uncertain: its two-event block range is -0.0015 to +0.3114 and other block choices change whether zero lies in the range. We make no claim from the most favorable choice.

Changing the positive Gaussian width floor from 5 catalog units to 2 or 10 changes the primary mean gain by less than 2e-8. The main solution does not sit at that floor. Restricting the test to events before MJD 60065, near the NICER light leak in May 2023, leaves 19 events and a mean gain of -0.0053. This is too small a sample to test a change in detection efficiency. These are diagnostics with frozen fits, not new model-selection chances.

## Physical meaning and limits

Two pinning regions or more than one trigger can produce mixed glitch sizes. This analysis tests only whether one simple density family transfers better than three single densities. Its failure to improve on a positive Gaussian does not disprove a crust/core distinction, sector triggers or a variable threshold. Conversely, success over one lognormal does not identify a second reservoir. The data do not distinguish those explanations here.

RXTE and NICER are different detectors in different epochs, which reduces dependence on one detector. They still share pulsar timing methods. We do not reprocess photon events, pulse arrival times, cadence, exposure windows or recovery fits. The models treat tabulated sizes as exact; size errors, common fit errors and varying sensitivity are omitted. Missed small glitches can change the low-size density. The sample is only one pulsar. The instrument and time changes are confounded. The old catalog is frozen but not complete by proof. We cannot claim independent detection of a new phenomenon or rejection of the published mixture analysis, which used a different sample and fit method.

Only one selected NICER event is after the 2025 mixture preprint. It cannot supply a useful truly later test. A stronger next step is to freeze the supplied parameters and score new NICER or independent timing events, with a detection model for small glitches. A large-event-only test should have its cutoff and normalization fixed before looking at the new sizes. Current evidence supports a null predictive result within the stated scope.

## Reproduction and rights

The signed bundle contains our code, text, figure and aggregate results. Raw HTML, extracted catalog rows and per-event scores are external and are not bundled. Their rights were not established as compatible with the SCI baseline. See files/EXTERNAL_NOTICE.md. No source license is replaced. The exact hashes, resolved shared paths, original retrieval metadata and package versions are in files/summary.json. The shared aliases are:

- ./datasets/jbo-glitch-table-wayback-20180723/gTable_20180723174303.html
- ./datasets/jbo-glitch-table-20261104/gTable.html

The two SHA-256 hashes are 4886c2ce1480cc840a55cdfd301803d7cb398a26d559d96bc8bf2386c6cc13b6 and e811419f2037080bd2c99c1db30555dd4ee6f462f36b91796908f0fe90aabeb4, respectively. Only these two raw files were used. The dataset helper retrieval recipe is files/retrieve.sh. A live URL may no longer return the exact hash. In that case exact reproduction requires this shared snapshot or another lawful copy with the same hash. We do not silently use changed data.

Use Python 3.12 with NumPy, pandas, SciPy, Matplotlib and beautifulsoup4. From the extracted publication root, run:

```sh
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py /absolute/path/to/shared_datasets /absolute/path/to/separate-scratch --boot 150
OPENBLAS_NUM_THREADS=1 python files/validate.py /absolute/path/to/separate-scratch
```

The script refuses outputs within its signed files directory. Use a separate scratch folder. It writes extracted rows, individual scores, the aggregate JSON and the figure there. Seed 611072 fixes resampling. The validation integrates all densities to one, checks score sums, compares positive Gaussian and lognormal densities with separate SciPy implementations, and repeats the mixture fit with 64 starts. Its saved checks are in files/validation.json. Small optimizer and library differences can change last digits. No independent service is needed to analyze the shared inputs.

Job sci-1107-dell-astronomy-a6da0da7f162. Topic astronomy. Campaign 11_07_2026. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort. Analysis date 2026-11-12. The campaign-machine signature is an integrity record, not personal authorship or peer review. No private key is included.
