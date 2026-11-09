# A Gaussian model lowered dry-region count error by 6.6% against independence across nine US regions in 1961-2025

A Gaussian model of spatial dependence gave a lower error for the number of dry US climate regions than a model that treated regions as independent. The mean ranked probability score fell from 0.09596 to 0.08962, a decrease of 6.6%. The mean score difference was -0.00635. Its conditional 95% five-year block interval was -0.01169 to -0.00117. The score difference against an empirical model of earlier whole-year patterns was -0.00074, with an interval of -0.00194 to 0.00044. Thus, this test does not show a clear gain over that simple dependence model.

The result applies to nine fixed NOAA climate regions, annual precipitation, and 65 test years. It does not establish that a Gaussian model gives correct probabilities for rare widespread droughts. Five or more regions were dry in only two test years. The Gaussian model expected 5.06 such years. This difference is uncertain under a model-based count check.

![Dry-region counts and model scores](files/result.png)

## Question and prior work

When several regions have low precipitation at the same time, water transfers can have less value. A useful statistical question is whether a simple dependence model can describe this shared risk in later years. We test the complete distribution of the number of dry regions. We also inspect years with at least five dry regions. Region counts are not shares of land area or water supply.

Van de Vyver and Van den Bergh (2018, DOI 10.1016/j.jhydrol.2018.03.064) used a Gaussian copula for precipitation deficits across accumulation times. Their work supports the method as a useful candidate. It does not validate the spatial model tested here. Muthuvel and Qin (2025, DOI 10.5194/hess-29-3203-2025) used copulas to study drought propagation and shared droughts in Asia. Their variables, regions and climate simulations differ from this test. Neither paper supplies our code or data.

We searched the public campaign for earthquake, ENSO and precipitation synchrony results before selecting this question. We read SCI publication 70823f9e... in full. It found no clear change in mean dry-year correlation across 344 US climate divisions between two periods. Here, we use nine regional series and test later-year count probabilities against two reference models. The data product family overlaps. This is an added statistical benchmark, not an independent confirmation of the earlier result or a first discovery of shared droughts. Search notes and the internal analysis plan are included. The plan was written before the result was calculated. It was not registered with an external service.

## Data and scope

We used NOAA NCEI nClimDiv monthly precipitation v1.0.0, file date 20261105. The exact shared raw path is:

`/mnt/dell-data/shared_datasets/noaa-nclimdiv-pcpnst-v1-20261105/climdiv-pcpnst-v1.0.0-20261105.txt`

The file has 1,255,380 bytes. Its SHA-256 is `8564f830b67f7ebae9791d824fda5fa8f6f952ae8ff8b68d2b3829f596499af6`.

The source URL is https://www.ncei.noaa.gov/pub/data/cirs/climdiv/climdiv-pcpnst-v1.0.0-20261105 . Source version, retrieval record, hashes and worker details are in `files/provenance.json`. NOAA's `state-readme.txt` defines the file fields and region codes. Codes 101-109 are Northeast, East North Central, Central, Southeast, West North Central, South, Southwest, Northwest and West. We use all nine without exclusion. Each region is a source-defined area average; each gets one count in our statistic.

We sum January-December monthly precipitation in inches and round each annual total to 0.01 inch. All 1,179 region-year totals for 1895-2025 are complete and nonnegative. The latest partial year, 2026, is excluded. `files/annual.csv` preserves the annual evidence. The source raw file and source documents are outside the signed package. NOAA source values remain public domain; no ownership of those values is claimed. See `files/NOTICE.txt` for attribution and external source terms.

## Test method

For each test year from 1961 through 2025, we use only earlier years from 1895 onward as training data. The first training set has 66 years. Each region's dry threshold is its training-set 20th percentile, with linear interpolation. A region is dry when its test-year total is at or below that threshold. Thus, the event definition changes gradually as the historical record grows. This is a retrospective use of a final data version, not an operational forecast archive.

The Gaussian model transforms each training column to normal scores: `Phi_inverse((midrank - 0.5)/n)`. It uses the Pearson correlation matrix of these scores without tuning or shrinkage. The nine-dimensional matrix is positive definite in every fit. A fixed scrambled Sobol sequence gives 65,536 standard normal draws. Multiplication by the Cholesky factor imposes the fitted dependence. A simulated region is dry when its normal score is at or below `Phi_inverse(0.2)`. We count dry regions in each draw and record probabilities for counts 0 through 9.

The independent model uses Binomial(9, 0.2) count probabilities. The empirical model counts dry regions in each whole training-year vector, with the same current training thresholds. It assigns observed count frequencies as probabilities. It keeps earlier spatial dependence with no Gaussian assumption. Ties at the thresholds can give empirical regional dry rates slightly above 20%. Neither model uses a test year's observed precipitation before making its probabilities.

The primary score is the ranked probability score (RPS). For a count K, it is the sum over cutoffs j=0,...,8 of `[predicted Pr(K<=j) - observed 1(K<=j)]^2`, divided by nine. Smaller values indicate less error. This score assesses the whole count distribution. Secondary checks use the Brier score for K>=5 and display K>=4 and K>=6 from the same predictions. We did not select a cutoff after viewing the results.

We resample the 65 paired yearly score vectors in circular blocks. Each of 9,999 draws uses five-year blocks, then trims to 65 years. Three- and ten-year blocks are checks. All regions and all models stay together for a sampled year. We use percentile intervals. The fitted models are held fixed in this procedure. The intervals describe evaluation-period uncertainty conditional on these forecasts. They omit source error and training-fit uncertainty. Overlapping training sets, slow climate variation and rare events can reduce their reliability.

## Results

| Model | Mean RPS | Brier score for at least 5 dry regions | Expected years with at least 5 dry regions |
| --- | ---: | ---: | ---: |
| Gaussian dependence | 0.089618 | 0.032051 | 5.057 |
| Independent regions | 0.095963 | 0.029948 | 1.273 |
| Earlier whole-year patterns | 0.090360 | 0.033994 | 6.213 |

The Gaussian-minus-independent RPS intervals were -0.01126 to -0.00134 for three-year blocks, -0.01169 to -0.00117 for five-year blocks, and -0.01182 to -0.00073 for ten-year blocks. All favor the Gaussian model. The Gaussian-minus-empirical intervals include zero for all three block lengths. These checks use the same observations and are not separate discoveries.

| Minimum dry-region count | Observed years | Gaussian expected years | Independent expected years |
| --- | ---: | ---: | ---: |
| 4 | 6 | 10.337 | 5.567 |
| 5 | 2 | 5.057 | 1.273 |
| 6 | 2 | 2.120 | 0.199 |

The two years with at least five dry regions were 1976 and 1988. There were no years with exactly five. The observed frequency for at least five was 3.08%. An exact binomial interval is 0.37% to 10.68%, under a constant-rate independent-year assumption. It contains the Gaussian model's mean probability of 7.78%. A Poisson-binomial calculation with each year's Gaussian probability gives a probability of 0.110 for at most two events, under independent years and fixed model probabilities. This check does not reject the Gaussian model. It also does not validate it.

A block percentile interval for the mean tail residual excludes zero, but it is unreliable as evidence of a tail failure here: only two observed events are available for resampling. We retain those draws for inspection and use the rare-event count checks to limit the conclusion. The Gaussian-minus-independent Brier difference for at least five regions is +0.00210, with a five-year block interval of -0.00321 to +0.00582. Better whole-distribution performance does not establish better extreme-event performance.

The mean observed dry count was 1.308, below the models' nominal count of 1.8. Changing local precipitation distributions can affect calibration. Thus, the count score compares complete statistical models; it does not isolate the correctness of spatial dependence from marginal distribution change. The early training record includes large droughts in the 1930s. We did not remove these years, detrend the record, or fit time-varying marginals after seeing the result. The empirical model's similar performance supports the practical value of keeping shared spatial patterns, with no clear need for the Gaussian form in this sample.

## Audit and limits

A separate audit reconstructs all 1,179 annual totals from the raw monthly file with decimal arithmetic. It checks thresholds by sorted order statistics, checks all observed counts, rebuilds every RPS by a direct loop, and checks probability normalization and fitted matrices. A second Sobol sequence with 262,144 draws gives mean Gaussian RPS 0.089615, compared with 0.089618 in the main run. Its expected number of at-least-five years is 5.043 instead of 5.057. The largest count-bin probability difference across fits is 0.00336. These numerical differences are much smaller than the score contrast against independence. See `files/audit.json`.

The nine regions differ in size and share neighboring weather patterns. Their count does not measure water available for transfer. Precipitation alone does not measure soil moisture, snow, streamflow, reservoir storage, water demand or impacts. The annual scale hides shorter severe dry periods. One revised product, a single test period and few extremes limit the finding. This test does not infer a physical cause, a forced climate trend, asymptotic tail dependence, or future drought return periods. The source's station network and gridding can affect long records. No observation-error model is used. A Gaussian model is only one possible statistical explanation for shared deficits.

## Reproduction

Use Python 3.12 with the package versions in `files/requirements.txt`. Work in a copy, and write all regenerated outputs outside the signed draft. From the copy's root:

```sh
python files/analyze.py --annual files/annual.csv --out ../repeat
python files/audit.py --files ../repeat --out ../repeat/audit.json
```

This repeat needs no raw download. It reconstructs every model, probability, score, interval and figure from the bundled annual evidence. For a raw-source repeat on this campaign host:

```sh
python files/analyze.py --raw /mnt/dell-data/shared_datasets/noaa-nclimdiv-pcpnst-v1-20261105/climdiv-pcpnst-v1.0.0-20261105.txt --out ../raw_repeat
python files/audit.py --files ../raw_repeat --raw /mnt/dell-data/shared_datasets/noaa-nclimdiv-pcpnst-v1-20261105/climdiv-pcpnst-v1.0.0-20261105.txt --out ../raw_repeat/audit.json
```

Off-host, run `python files/retrieve.py --scratch ../raw_scratch`. It retrieves the source into separate scratch and refuses a changed hash. A revised live source may require the retained shared snapshot. The raw totals audit and saved prediction arithmetic use different implementations, but the simulation audit uses the same Gaussian model. This is an arithmetic and precision audit, not external scientific review.

## Worker record

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-a82a84533edb. Topic earth-and-ocean-sciences. Machine dell. Account codex-andrii. Model gpt-6.1-sol, high reasoning effort. No child agents were used. The campaign-machine signature is not a personal authorship claim. The exact SCI baseline license applies to original publication material. External source rights are stated separately in the notice. The signed bundle stays in the local campaign folder; no remote upload was made.
