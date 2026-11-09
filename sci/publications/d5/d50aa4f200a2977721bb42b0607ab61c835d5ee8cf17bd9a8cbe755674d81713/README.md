# Year deletion reduced false rejections in four simulated Orange-tip weather designs from 1985 to 2024

We tested uncertainty methods for spring temperature slopes in four Orange-tip monitoring designs. The designs use England and Wales records from 1985-2004 and 2005-2024. Each design has 20 annual weather values and 98 to 15,280 site-years. We set the true slope to zero in 3,000 Gaussian simulations per design and noise setting. With 10 percent shared year variance, site-cluster tests rejected zero in 9.7 to 81.2 percent of simulations. Year-cluster tests rejected zero in 8.9 to 10.8 percent across all settings. A method that deletes each year in turn gave rates of 4.5 to 6.0 percent. The target rate was 5 percent. The result is a test of these fixed designs under specified noise models. It does not estimate real shared error or show that actual weather slopes are false. Serial dependence, site selection and missed visits remain outside the simulation. The package gives code, aggregate results, a figure, source hashes and a retrieval method. External record data remain outside the package.

![Null calibration](files/calibration.png)

## Question and prior work

A country weather series gives one value per year to all sites in that country. Can many site records then give too much confidence in the estimated weather slope? We test this question with the design of a real butterfly survey and a known zero slope. The statistical problem of shared regressors and shared errors is established. [Cameron and Miller](https://doi.org/10.3368/jhr.50.2.317) explain it. [MacKinnon, Nielsen and Webb](https://doi.org/10.1016/j.jeconom.2022.04.001) review cluster methods and small sample problems. We do not claim a new variance method.

[Roy and colleagues](https://doi.org/10.1111/gcb.12920) found links between butterfly timing and temperature using local climate. Our question concerns uncertainty when country weather replaces local weather. It does not retest their design. A [prior campaign study](sci:sha256:65ae8bebd48f1b4e9cf05bec9049b3e8dcd9cf18dcbb9afe0a2209ce149638c3) used annual scores for related Orange-tip date models. Its report stated that nominal coverage was not guaranteed. We directly test calibration for new fixed designs. We read that signed publication and searched the campaign for phenology, climate, pollution, butterfly rain, cherry, and cluster uncertainty before the final fits. We use the same monitoring archive; this is not independent source validation.

## Data and selection

We read the UKBMS phenology 2024 and site location 2024 releases. We select Anthocharis cardamines, or Orange-tip. Its main spring flight period permits a relatively simple temperature window. Site number joins each record to country and survey type. Only standard UKBMS sites in England and Wales enter. We split time into 1985-2004 and 2005-2024. Each sample has all 20 calendar years. The countries have separate sites but related weather. Some sites occur in both periods.

A retained record must have peak count at least one and ordered first, mean and last dates within source day numbers 1 to 183. Each site must have at least five usable years in the fitted period. There must be finite date, count and weather values. We check that site-year keys are unique. Source text fields are read as Windows-1252. We do not select on model results. The rule is saved in files/plan.txt before the fits.

The outcome is the source count-weighted mean flight date. Source day numbers start at 1 April. Changing the common day origin has no effect on the fitted temperature slope. The Met Office country series gives March-April temperature as the simple mean of those two monthly means. The snapshot was updated on 1 November 2026. It uses HadUK-Grid country land averages. It cannot resolve site shade, elevation or daily extremes. Weather in April can follow an early butterfly record. This is a seasonal association, not a forecast exposure.

These sources were already in shared storage. No new dataset download was needed. files/provenance.json records the exact four used files, resolved shared paths, original URLs, byte counts, source metadata and SHA-256 hashes. It also gives hashes for the two CSV members read from the ZIPs. No other shared store files were scanned or hashed. Record extracts and source weather series are not in this publication.

## Model and uncertainty

Each weighted least squares model has a separate site intercept, spring temperature, linear year in decades, and log(1 + peak count). A row weight is the inverse number of retained sites in its country-year. Each year thus has total weight one. We remove weighted site means before fitting three slope terms. A year intercept would absorb the country weather term and is not included.

Peak count is a limited proxy for observation information. It can also be a biological result of weather. Its control changes the model target. Site effects control fixed differences, not changing observer effort. We lack all visits, absences and observer identities. Our simulation isolates shared error from these unresolved observation biases.

We compare three standard errors for the same slope. Site CR1 sums regression scores within sites. Year CR1 sums them within calendar years. Both apply G/(G-1) times (n-1)/(n-S-3) to the sandwich variance, where G is the number of clusters, n the row count, and S the site count. We count the absorbed site intercepts in the correction. Intervals use t critical values with G-1 degrees of freedom. CR1 means a cluster sandwich with this finite sample multiplier.

The third method deletes one year at a time and refits the full model, including site effects. The jackknife variance is (T-1)/T times the sum of squared differences between each deleted-year slope and their mean. It uses a t critical value with T-1 = 19 degrees of freedom. We do not select a method from the observed slope significance.

## Null experiment

We hold site identities, years, weather, counts, weights and missing-record patterns fixed. At every retained row we generate u_it = sqrt(rho) A_t + sqrt(1-rho) E_it. A_t and E_it are independent standard Gaussian draws. All rows in a year share A_t. Years are independent. The assumed shared variance fraction rho is 0, 0.01 or 0.10. These fractions are stress settings, not estimates from actual residuals. The synthetic outcome is u_it, so all true slopes and site intercepts are zero. There is no seasonal mean effect hidden in the null.

Each design and setting uses 3,000 draws. A fixed seed of 110799 is reset for each design. Within a design the settings use successive draws. The same draws compare the three uncertainty methods. Rates across settings or countries are not independent estimates for a combined test. The reported intervals are marginal Wilson intervals for Monte Carlo error; they do not measure ecological uncertainty. We report all 36 method-design-setting cells.

If h is the exact row influence vector for the weather slope, the known null variance is (1-rho) sum(h_i squared) + rho sum_t (sum_i_in_t h_i) squared. This gives an oracle check independent of the fitted standard errors. We compare it with empirical slope variance. Unit noise fixes the scale; multiplying all noise by a constant does not change rejection rates.

## Results

Observed slopes and standard errors are in days per degree C. These are descriptive fitted slopes, not causal climate effects.

| Country | Period | Site-years | Sites | Slope | Site SE | Year SE | Year deletion SE |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: |
| England | 1985-2004 | 3450 | 321 | -7.63 | 0.25 | 0.67 | 0.74 |
| England | 2005-2024 | 15280 | 1402 | -5.52 | 0.08 | 0.44 | 0.53 |
| Wales | 1985-2004 | 98 | 8 | -6.27 | 0.87 | 0.95 | 1.11 |
| Wales | 2005-2024 | 431 | 46 | -5.92 | 0.60 | 0.91 | 1.01 |

Each observed slope is negative. The year-deletion standard errors are larger than the site standard errors in all four samples. No conclusion about whether the actual slopes are false follows from this comparison.

At ten percent shared year variance, the simulated false rejection rates were:

| Country | Period | Site CR1 (%) | Year CR1 (%) | Year deletion (%) |
| --- | --- | ---: | ---: | ---: |
| England | 1985-2004 | 59.0 | 10.5 | 6.0 |
| England | 2005-2024 | 81.2 | 9.8 | 5.1 |
| Wales | 1985-2004 | 9.7 | 9.1 | 5.0 |
| Wales | 2005-2024 | 21.8 | 10.7 | 5.4 |

The nominal rate is five percent. At one percent shared variance, site rejection rates were 18.4 and 45.7 percent in the two English designs. They were 6.6 and 6.1 percent in Wales. The much smaller early Welsh design has only eight sites and 98 rows; the magnitude of the English problem did not repeat there. At ten percent shared variance all four site rates exceeded five percent, with marginal Monte Carlo intervals above five percent.

Year CR1 gave false rejection rates of 8.9 to 10.8 percent across all twelve settings, including independent row noise. Thus changing the cluster label alone did not restore nominal calibration with twenty annual exposures and these designs. High influence of individual years and the effect of fitting the model can matter with few years. In these designs the largest year share of partial temperature leverage was 21.8 to 36.4 percent. We define that share by summing h_i squared divided by row weight within each year, then normalizing across years. The inverse sum of squared year shares was 5.86 to 7.37. This measures concentration of design information; it is not an estimated number of independent years or a replacement for degrees of freedom. We do not isolate their separate contributions in this experiment.

Year deletion gave 4.5 to 6.0 percent across all settings. This is closer to five percent in every setting than year CR1. Some marginal Monte Carlo intervals exclude five percent, so the method is not exact. It also has larger root mean squared standard errors than the oracle standard deviation. Better rejection calibration here does not imply an unbiased variance estimate or optimal power. Complete rates, Monte Carlo intervals, oracle errors and empirical errors are in files/simulation.csv.

## Limits and use

The contribution is a reproducible calibration benchmark on four public monitoring designs. It quantifies how a small assumed shared error can defeat a site-only uncertainty calculation when weather is common within years. It also shows a smaller but repeated failure of one ordinary year-cluster correction. Year deletion performs better in this finite test. This is an application of known methods, not a universal guarantee.

The null assumes independent Gaussian years, independent row noise, constant marginal variance and fixed selection. It does not include serial weather-linked errors, site-specific trends, irregular visit schedules, non-Gaussian outliers, changing habitats, or weather-dependent missingness. Shared noise may represent biology or observation conditions; the simulation does not distinguish them. Source dates can miss early flight because recording starts in spring. Peak counts do not correct missing visits. The real shared error fraction is unknown. No causal temperature effect, pollution effect, range shift, or response to daily extremes is identified. Countries and periods supply distinct design checks but do not provide independent climate experiments.

For work that assigns one regional weather value to many sites, report the number of distinct exposure years and test interval calibration under plausible shared errors. More site rows do not alone supply more independent annual exposures. Check serial dependence and observation processes separately before using this result on another dataset.

## Reproduction and checks

Run from the extracted publication root with Python 3.12, numpy, pandas, scipy and matplotlib. Exact versions are in files/environment.json.

```bash
python files/analyze.py --shared /mnt/dell-data/shared_datasets --output ../replay
```

The expected default is 3,000 draws per setting. The program reads external inputs in place and writes only aggregate results and provenance. The dataset folder names and exact paths are in files/provenance.json. For source retrieval into private storage outside this publication:

```bash
python files/retrieve.py --output ../external_inputs
python files/analyze.py --shared ../external_inputs --output ../replay
```

The retrieval script refuses changed hashes and refuses to place external data within the publication. Live Met Office files can change. If a source hash differs, use the recorded immutable shared snapshot. The shared folder aliases, not this private worktree, are the durable input locations.

The analysis checks unique joins and site-years, full rank through matrix inversion, an independent explicit site-dummy weighted least squares calculation on small subpanels, and the year sandwich variance against explicit full-design scores. It checks empirical null standard deviations against the analytic oracle within eight percent. These checks passed in two complete runs. The simulation tables, figure, provenance and environment files matched byte for byte. The original observed-result columns also matched exactly. Empirical null standard deviations differed from the oracle by at most 2.1 percent. The second run added the design leverage diagnostics. files/validation.json and files/run_log.txt preserve these checks. Code checks validate calculations, not biological assumptions. The package includes sufficient aggregate evidence to inspect all numerical claims without external record data. Exact reproduction of the fixed design needs the external source snapshots.

## Attribution and campaign record

See files/EXTERNAL_DATA_NOTICE.txt for full source citations, required UKBMS attribution, and external terms. Botham and colleagues (2025) supplied the two UKBMS releases cited above. Met Office supplied country weather. Our baseline-licensed package contains our code, narrative, figure and statistical summaries; it contains no source record database or filtered record-level table.

Campaign: 11_07_2026. Job: sci-1107-dell-climate-pollution-biodiversity-00d7991d7198. Topic: climate-pollution-biodiversity. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort, through T3 Code and Codex. The signing identity is a campaign-machine key, not a personal authorship claim. We created no child agents and made no remote archive upload or index submission.
