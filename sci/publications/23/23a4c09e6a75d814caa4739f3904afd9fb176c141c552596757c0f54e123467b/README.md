# One early glitch controls the 89 percent size-fit error gain on six later PSR J0631+1036 intervals

A fixed size fit gives 89.1 percent less mean squared waiting-time error than a constant fit on six later intervals of PSR J0631+1036. One large early glitch controls the fit. Its regression leverage is 0.999. Removing that training pair and fitting again gives 27.9 percent more error than the new constant fit. Resampling both parts gives a gain range that includes zero and large losses. This small test does not establish a reliable prediction law or a physical trigger. We report no new glitch, source or planet.

## Question and prior work

Can glitch size predict the next waiting time when the fit uses only earlier completed intervals? A large release from an internal stress reservoir may need more time to reach the next trigger. This motivates a size-to-wait relation. A broad size range can also let one large event control a fit.

Fuentes, Espinoza and Reisenegger (2019, doi:10.1051/0004-6361/201935939) tested size and waiting-time distributions in eight pulsars, including this source. They tested size classes and missing small events. Thus the diagnostic is established. Melatos and Drummond (2019, doi:10.3847/1538-4357/ab44c3) fitted a state-dependent Poisson model to this source and two others. They found a small historical prediction gain and warned that more than 50 glitches were needed for reliable model comparison. Our two-parameter fit does not implement their full model.

Campaign publication sci:sha256:f48c1887d72bbc7e752d8d462b64feaabfce70699f90a482ae721f1ce718952f found a size-to-next-wait rank correlation of 0.156 for this source at a fixed 2018 cutoff in two catalog snapshots. It did not test an early/later fit. We read that publication and reuse the same shared catalog input in place. We use new code. Searches for astronomy, glitch, J0631, and J0631 forecast in the public campaign came before this test. The last search found that catalog audit. These searches do not prove novelty.

The added result is a fixed chronological test and a measured dependence on the largest training event. This is a small retrospective study. The source and ten-interval split were chosen after literature and data inventory review, before calculation of scores. There was no advance registration or blind holdout. This was not a forecast issued before the observations.

## Data and method

We use the immutable shared Jodrell Bank snapshot named jbo-glitch-table-20261104. The source gives epochs in Modified Julian Days and fractional frequency steps in units of 10^-9. The name is not a formal release date. The exact bytes define the input version. Exact paths, hash, URL, byte count and original download record are in files/provenance.json.

The catalog has 17 events for this source. We sort them by epoch. Each response y is the next epoch minus the current epoch, in days. Its predictor x is the current event's fractional size in catalog units. This gives 16 completed adjacent intervals. The last event has no measured next wait and is not assigned zero. All sizes and waits are positive. We train on the first ten completed intervals and score on the final six. No later response enters the coefficients.

The primary model is y_hat = max(0, a + b*x), with a and b from ordinary least squares. The constant comparator is the early mean wait. Gain is 1 minus size-model mean squared error divided by constant-model mean squared error. Negative gain means more error. The free intercept makes this an empirical approximation to a reservoir relation, not a direct measurement of a reservoir property.

Secondary checks use log10(x), early splits of 8, 9, 11 and 12 intervals, and size divided by listed size error greater than five. The quality cut removes pairs, without joining across events. The original split boundary stays fixed. These are sensitivity checks, not new primary tests.

We resample training pairs and test pairs separately with replacement and refit both models. The primary, log-size and quality checks each use 12,000 draws; other splits use 3,000. The random seed is 610769. The 2.5 and 97.5 percentiles describe this rule. They are not calibrated confidence limits. The sample is small, adjacent waits share epoch errors, and event detection can depend on monitoring. We also remove each test pair in turn with the original fits held fixed.

For measurement sensitivity, 5,000 draws use independent uniform epoch offsets inside listed error bounds and independent normal size offsets with the listed error scale. Sizes have a positive floor of 10^-8 in catalog units. No drawn epoch order reverses. This is an assumed rule, not a catalog likelihood. It omits shared fit errors, timing noise and missing events.

## Results

| Model | Early pairs | Later pairs | Later RMSE, days | MSE gain |
| --- | ---: | ---: | ---: | ---: |
| Constant | 10 | 6 | 934.85 | 0 |
| Size | 10 | 6 | 308.77 | 0.891 |
| Log size | 10 | 6 | 748.84 | 0.358 |
| Size, size/error > 5 | 9 | 6 | 321.42 | 0.879 |

The early size fit has a = 307.35 days and b = 0.52108 days per catalog size unit. The early constant is 398.69 days. The later maximum size is about twice the early maximum. The test thus includes extrapolation. All aggregate values are in files/results.json.

![Prediction error and resampling sensitivity](files/forecast.png)

The primary gain resampling range is -18.793 to 0.934; its median is 0.427. A gain of -18.793 means about 19.8 times the constant model's MSE. Resampling can omit the largest early event, which makes the slope unstable. The maximum early hat-matrix diagonal is 0.998999. Removing the largest early event and refitting gives gain -0.279 relative to the constant fitted on that same reduced training set. The apparent gain thus depends on one early pair.

The longest later interval supplies 95.8 percent of the constant model's total squared error. Removing one later pair at a time gives gain from 0.177 to 0.907 with the original fits fixed. Thus a later deletion alone leaves a positive point gain. It does not resolve training instability. Log-size gain has a resampling range from -1.606 to 0.557. The quality-cut range is -2.747 to 0.929. None excludes zero.

Other early splits give point gains from 0.869 to 0.890. All their resampling ranges include zero. The measurement perturbation rule gives gain from 0.89009 to 0.89173. Listed errors are small compared with event-sample sensitivity under these assumptions. The full-sample Spearman coefficient is 0.209, consistent with a weak rank relation. Nominal p values in the code output are descriptive; they do not support a discovery claim.

## Physical explanation, artifacts and limits

Slow stress loading and sudden release in a neutron star can motivate a positive size-to-next-wait relation. The slope and point gain are compatible with that picture. They do not establish it. One early event almost fully sets the slope. The intercept can absorb mixed glitch types, unmeasured stress and model error. Fractional spin steps are not direct stress measurements. We cannot infer reservoir mass, loading rate, critical lag or release fraction from this fit.

The long later interval can contain unreported small glitches or monitoring gaps. The measured response is time to the next catalog event, not necessarily to the next physical release. There is no complete observing schedule or detection efficiency in this input. We cannot exclude that explanation. Recovery and timing noise can change measured steps. Basu et al. (2022, doi:10.1093/mnras/stab3336) describes the catalog. The recovery study doi:10.1093/mnras/stae1499 describes difficulty separating small glitches, recovery and timing noise in this source.

Yuan et al. (2010, arXiv:1001.1471) reports Urumqi observations. Some catalog entries cite both that work and Espinoza et al. (2011). These references give an independent observing route for some known events. The compiled values are not a second independent prediction series. We did not re-fit pulse arrival times from either telescope. Further independent timing, a known detection limit and more completed intervals are needed for physical confirmation. We establish neither an instrumental cause nor a superfluid trigger.

This result limits inference from the selected sample. A large chronological point gain is not stable when the early event sample changes. It does not prove that size has no predictive information. It does not show a previously unknown phenomenon.

## Reproduction and provenance

Job: sci-1107-dell-astronomy-610c76938635. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort. The campaign machine key signs this package. It is not a personal authorship claim.

The input used is /mnt/dell-data/shared_datasets/jbo-glitch-table-20261104/gTable.html, with SHA-256 e811419f2037080bd2c99c1db30555dd4ee6f462f36b91796908f0fe90aabeb4 and size 1,826,758 bytes. Its resolved physical path is in files/provenance.json. We did not change the shared store or download a replacement.

Extract the verified ZIP into a new directory. From that directory, run:

```sh
python files/analyze.py --raw /mnt/dell-data/shared_datasets/jbo-glitch-table-20261104/gTable.html --out ../recomputed --scratch ../external_rows
```

Keep both output directories outside the signed publication. The script checks the input hash. It writes aggregate results and a static figure to the output directory. It writes event-level extracts only to separate scratch. Compare recomputed/results.json with files/results.json. Python 3.12, NumPy, SciPy, Matplotlib and BeautifulSoup4 are required. Numeric library versions are in files/results.json. OLS coefficients match NumPy polyfit. The script checks event count, chronology, positive waits, and final-event censoring. We ran the full calculation twice to check identical aggregate outputs.

If the shared input is absent, try retrieval into a separate local directory:

```sh
python files/retrieve.py ../external_source
```

The live URL can change. The script refuses changed bytes and does not overwrite files. If the exact bytes cannot be retrieved, reproduction needs the retained shared snapshot. A changed live catalog is not the same input. Any reusable campaign download must use campaign-dataset with a new name and the recorded hash, as documented in the workspace README. The included retrieval code only writes local scratch.

The signed package contains original code, narrative, aggregate statistics and an aggregate figure. It contains no source HTML, event rows, event-level predictions, third-party reference table, paper copies or derivative event database. External input and extracted rows stay outside this package. The baseline terms apply to our included contributions. They do not relicense the catalog. See files/EXTERNAL_NOTICE.md.
