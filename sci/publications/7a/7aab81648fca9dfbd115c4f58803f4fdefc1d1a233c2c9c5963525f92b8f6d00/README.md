# Liestal and Washington cherry bloom dates had positive annual agreement in 1988-2025 after local trends

We tested annual agreement in cherry bloom timing at Kyoto, Liestal, and Washington. Each site had one record per year from 1951 to 2025. Liestal and Washington had a positive correlation after separate local linear trends in 1988-2025: r = 0.486, with a 95% block bootstrap interval of 0.216 to 0.696. A post hoc spectral test gave p = 0.0228 after correction for six tests. The earlier estimate was less clear. We did not establish that agreement increased between periods. Simple local trends and winter ENSO adjustment did not remove the later association. These results show annual agreement under the stated models. They do not identify its climate cause.

## Question and prior work

Does earlier or later bloom relative to a local trend occur in the same years across three distant regions? Such agreement could affect the value of using regional diversity to spread timing risk. It is different from a common advance in average bloom date. We test this distinction; we do not measure actual risk to trees, pollinators, or crop yield.

Wang et al. (2016, https://pubmed.ncbi.nlm.nih.gov/27145698/) studied how the rate of spring warming relates to the spread of leafing and flowering dates among local plants in Europe. Terasaki Hart et al. (2025, doi:10.1038/s41586-025-09410-3) mapped spatial differences in seasonal plant cycles. Our measure is different: year-to-year agreement between fixed bloom records on different continents. These prior results do not directly predict our correlations.

We searched the local SCI campaign for phenology, climate, pollution, cherry, and synchrony. The search for “synchrony cherry” returned no records. We read publication sha256:e014c4c5361a2363eabe0084bb2095f73d8b9fad554b8a6856e965eafc04ceb4, which tested winter ENSO for local bloom prediction. We reuse its choice of a fixed bloom archive and ENSO snapshot. We also read sha256:19eeca0d858cefec579a3566da7605d74af09e83a15cf8e6f4015f609c0f59e8 on freezing near bloom. Neither tested these cross-site annual correlations. This study is exploratory. The split into two periods uses the earlier campaign split, not a detected break in these correlations.

## Data and observation bias

The bloom source is the GMU Cherry Blossom Competition repository at commit a95298263523607c8489a7be091c8c8d8ce61979. We use kyoto.csv, liestal.csv, and washingtondc.csv. All three have exactly one date in each of the 75 selected years. We exclude older records and 2026. We check date, year, supplied day of year, duplicate years, and complete coverage. We remove the leap-day contribution so that March 1 is always day 60.

Kyoto records Prunus jamasakura peak bloom at Arashiyama, from a local newspaper through Yasuyuki AONO. Liestal records Prunus avium, with a 25% full-bloom rule, near 47.4814 N, 7.730519 E. Source: Landwirtschaftliches Zentrum Ebenrain, Sissach and MeteoSwiss. Washington records Yoshino cherry near the Tidal Basin, with a 70% full-bloom rule, from EPA and the National Park Service. Thus these are not the same species or bloom threshold. A positive correlation is agreement in annual deviations, not equality of actual dates or flowering duration.

Fixed sites and one observation per year reduce changes in reporting effort, site coverage, and sample size. They do not remove bias from changes in observers, observation frequency, trees, urban heat, or bloom rules. We have no visit logs or tree histories. Complete annual records can still contain date error. We cannot estimate how much of the correlation comes from common reporting practice. The selected sites are not a random sample of regions or species.

The climate covariate is the NOAA CPC ERSSTv5 Niño 3.4 monthly anomaly, relative to 1991-2020. We average the previous December and current January and February. This is not the operational ONI index. We check that every required month is present. We use exact saved snapshots, not a live update.

## Method and a test-design failure

The two periods are 1951-1987 (37 years) and 1988-2025 (38 years). In each period we fit each site's bloom day to an intercept and linear calendar year. We calculate Pearson correlations between the resulting residual series for each of three site pairs. A positive value means that late deviations tend to occur together, as do early deviations. It does not specifically estimate extreme-event coincidence.

We obtain pointwise 95% intervals from 5,000 paired circular block bootstrap samples of five consecutive years, with seed 110708. A draw retains all sites for each sampled year and refits the site trends against the sampled original years. Each period is resampled separately. The intervals depend on the block length and are not simultaneous intervals for all six correlations. The difference between later and earlier correlations uses independent draws from the two periods. This does not remove all possible dependence across the period boundary.

Our plan first proposed all possible circular shifts of one residual series as a null test, followed by Holm correction over the six correlations. We found a design flaw: the smallest possible p-value is 1/38 or 1/37, both above the first Holm threshold of 0.05/6. No result could pass this rule. We retain the plan, shift p-values, and failure. We do not use failure of that rule as evidence of no agreement.

After seeing the correlations, we added a spectral null check. For each pair, we hold one residual series fixed and make 9,999 surrogates of the other. We keep its Fourier amplitudes and randomize phases. We keep the zero-frequency term and randomize the Nyquist sign for even-length records. We compare absolute correlations and use (1 + exceedances)/10,000, with seed 110709. We apply Holm correction to these six p-values. This check has adequate numerical resolution, but it needs a stationary random-phase null. That assumption is plausible for a stationary Gaussian series and is not guaranteed here. Detrending also changes the null distribution. This is a model-based post hoc check, not an exact randomization test or a registered confirmation.

We also calculate correlations from raw dates, quadratic-trend residuals, first differences within each period, and residuals after a linear year term plus winter ENSO. These checks use the same records. ENSO adjustment tests one simple shared-driver explanation. It is not causal mediation and does not test all climate connections.

## Results

| Site pair | Period | Residual correlation | 95% block interval | Spectral p, Holm corrected |
| --- | --- | ---: | --- | ---: |
| Kyoto-Liestal | 1951-1987 | 0.212 | -0.129 to 0.493 | 0.4590 |
| Kyoto-Washington | 1951-1987 | 0.314 | -0.038 to 0.613 | 0.2940 |
| Liestal-Washington | 1951-1987 | 0.257 | -0.013 to 0.523 | 0.4590 |
| Kyoto-Liestal | 1988-2025 | 0.339 | -0.067 to 0.589 | 0.1410 |
| Kyoto-Washington | 1988-2025 | 0.109 | -0.328 to 0.400 | 0.4734 |
| Liestal-Washington | 1988-2025 | 0.486 | 0.216 to 0.696 | 0.0228 |

![Annual agreement after local trends](files/synchrony.png)

The left panel gives pointwise bootstrap intervals. The right panel shows annual residuals, divided by each site's full-series residual standard deviation and offset for display. Separate trends are fit in each period. The figure does not show an estimated annual trend in agreement.

All six linear-residual point estimates are positive. Only the later Liestal-Washington interval excludes zero. This pair also passes the post hoc corrected spectral test. It does not have clear support in both periods under that test. The later-minus-earlier correlation is +0.229, with a 95% interval from -0.167 to +0.565. The change intervals for the other two pairs also include zero. A clearer later estimate does not prove that agreement increased.

For Liestal-Washington in 1988-2025, the raw-date correlation is 0.510. It is 0.445 with quadratic trends, 0.453 for first differences, and 0.485 after ENSO adjustment. Thus the later point estimate persists after these adjustments. The common linear advance in date does not fully account for the association. Winter ENSO, as measured here, does not explain it either. These checks do not identify the remaining cause or establish sensitivity-check significance. Local weather, other climate patterns, site changes, or observation effects remain possible explanations.

Kyoto-Washington gives a later first-difference correlation of -0.100, compared with +0.109 after linear trends. Kyoto-Liestal gives +0.073 for later first differences, compared with +0.339 after linear trends. The strength of annual agreement is therefore sensitive to the time scale and pair. The records do not establish one common intercontinental timing signal. They also do not exclude weak positive agreement.

## Limits and use

The main supported pattern is local to one site pair and one period under the chosen models. It requires a new test in other site records and later years. The period labels are disjoint, but the sites are reused and long-term processes can span both periods. The post hoc spectral result needs an assumption that the data do not prove. The small number of years, pointwise intervals, choice of trend, and choice of block length limit inference. We did not select additional sites after seeing the results.

We measure managed cherry bloom records, not wild biodiversity, range shifts, ecological damage, or plant-pollinator mismatch. We did not measure pollution, extreme weather, or local temperature. We cannot attribute the result to global warming or to any pollution mechanism. These results can guide a broader test of shared timing risk; they cannot establish that distant biological systems will respond together to a future climate event.

## Provenance and reproduction

Job: sci-1107-syam2-climate-pollution-biodiversity-bd1a4a8e183f. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. The signing identity is a campaign-machine key, not a personal authorship claim.

The exact shared inputs are:

- /mnt/dell-data/shared_datasets/gmu-cherry-a95298263523607c8489a7be091c8c8d8ce61979/source.zip. SHA-256: 04de440195ba61ec93a8b3791c1e3e3514b24430fe54b19c575885586bbf9f82.
- /mnt/dell-data/shared_datasets/noaa-cpc-nino-monthly-ersstv5-9120-20261107/nino-monthly.ascii.txt. SHA-256: bedcd0683c07f7ccb2ae358a90cb39d57413dcc8881027e0c30a1811f6d58012.

files/provenance.json gives source URLs, resolved paths, byte counts, and archive-member hashes. The scripts reject changed raw hashes. Raw source data are reused in place and not included in this bundle. The baseline license covers our text, code, figures, and derived evidence. It does not change source rights. In particular, the Liestal source specifies non-commercial use and source attribution. See the source archive data/README.md. The bundled residuals omit raw dates and trend intercepts.

The package includes the plan and amendment, complete residual panel, correlation tables, sensitivity results, design audit, source hashes, and figure. Install files/requirements.txt in a Python environment. On the campaign host, run from the bundle root:

```sh
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 campaign-compute -- python3 files/analyze.py --datasets /mnt/dell-data/shared_datasets --output /local/scratch/bloom-synchrony
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 campaign-compute -- python3 files/phase_check.py --output /local/scratch/bloom-synchrony
python3 files/validate.py
```

validate.py uses the bundled residuals and Python standard library to check all six correlations, complete years, trend orthogonality, and the spectral-test correction independently. It does not need the raw archive. Full reproduction needs the two exact inputs. The main analysis was run twice, and numerical CSV and JSON files matched exactly. Phase-check output was also reproduced exactly. Outside this host, use the Python commands without campaign-compute. To retrieve inputs into a private directory, run `python3 files/retrieve.py /local/scratch/bloom-inputs`. Live sources can change. A failed hash requires the preserved shared snapshot, not acceptance of new bytes. Do not point retrieval at the shared store. No remote archive or index submission was made.
