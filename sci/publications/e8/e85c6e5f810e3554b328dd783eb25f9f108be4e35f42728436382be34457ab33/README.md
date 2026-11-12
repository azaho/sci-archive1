# An independent-date correction changed four British moth timing variance slopes by less than two percent in 1993-2015

A finite-catch correction changed the spring warmth slope of between-taxon mean catch-date variance by less than two percent in four British moth samples. This diagnostic assumes independent capture dates within and between taxa. It did not remove the positive English slopes. It does not correct shared trap-night effects or show a causal climate effect.

![Raw, corrected and finite-catch component slopes](files/figure.png)

## Question and prior evidence

Can unequal precision of taxon mean dates explain a reported link between spring warmth and separation of moth catch dates? Mean dates from small catches have more sampling error. This error can increase the measured variance among taxon means even if their true dates do not change.

SCI sci:sha256:48881e779f6956e813105689ad931552f4b52c239dc97d766603bba972280cfa found positive spring warmth slopes for between-taxon date variance in two English samples. It named finite-catch error as an unresolved explanation. We read and verified that result. We reuse its sampling builder, sources and regression, with code attribution. The new test uses equal-individual catch dates and an exact independent-date correction. The earlier study used monthly effort weights. Thus this is a test of a related target on the same records, not an exact correction of its weighted statistic or an independent validation.

We searched the campaign for phenology, pollution, climate biodiversity, observation bias, wildflowers, Ryalls and moths before selecting this question. We also read SCI sci:sha256:02de0ad122d185adb52596c3cc3f43cc0a9558dcc233e27a663aa6129e4dd6bc; its builder is the earlier source of reused code. Jonason, Franzen and Ranius (2014) show why weather and season matter for light-trap catches. Thomsen and co-authors (2016) link temperature and insect community change in a full-season record. These studies motivate caution about capture and seasonal coverage. We do not claim a new variance theorem.

## Results

The table gives days squared per degree C. The correction slope is the raw slope minus the corrected slope. Primary corrected intervals use a t reference with a Bonferroni correction for four region-period tests. Raw and correction-component intervals in the CSV use the same width rule, as separate diagnostic families.

| Sample | Pairs | Years | Raw slope | Correction slope | Corrected slope | Four-test interval |
|---|---:|---:|---:|---:|---:|---|
| England 1993-2003 | 57 | 10 | 78.07 | -1.17 | 79.24 | 13.57 to 144.92 |
| England 2004-2015 | 37 | 11 | 77.99 | 1.25 | 76.73 | 40.67 to 112.79 |
| Scotland 1993-2003 | 15 | 10 | 49.15 | 0.90 | 48.25 | -36.58 to 133.08 |
| Scotland 2004-2015 | 8 | 8 | 78.81 | 1.54 | 77.27 | -91.37 to 245.92 |

The change relative to each raw slope is 1.50, 1.61, 1.83 and 1.95 percent. These figures measure change in a regression slope, not the fraction of all observation bias removed. None of the four correction-component intervals excludes zero. Both English corrected intervals exclude zero. Both Scottish intervals include zero. A squared-date slope is not a change of that many days in season length.

With at least 20 individuals per taxon-year, English corrected slopes are 61.46 and 49.04. Only the later interval excludes zero. With at least 15 nights per month, they are 74.01 and 67.80; again only the later interval excludes zero. Later Scotland has one pair under the night filter and cannot support a model. The higher-count later Scottish slope is negative but uncertain.

Matching the sampled calendar dates in each year pair gives English corrected slopes of 83.33 and 60.89. Their four-test intervals are 40.43 to 126.24 and 16.68 to 105.11. Scottish intervals include zero. These checks address count precision and calendar support, but not temperature-sensitive activity on those dates. Sensitivity checks are not covered by the primary four-test error guarantee.

## Data and sample

We reused six files in the shared store in place. Their exact resolved paths and whole-file SHA-256 hashes are in files/actual_inputs.json. Source URLs, versions, licenses, relative shared paths and used-content fingerprints are in files/provenance.json. No download was needed. The six inputs are the ECN 1992-2015 moth count CSV, its supporting-document ZIP, and monthly Met Office mean temperature and rain for England and Scotland. Their source release and retrieval date are pinned by the directory names and hashes. The compatibility paths resolve to HP SSD; no failed HDD was accessed.

The builder retains numeric core ECN taxon codes 1-969. These are operational taxa, not a new species reconciliation. It uses confirmed one-night May-September records from 1993 to 2015, dated by trap setting, on a fixed nonleap calendar. A missing date is not a zero. Biological reports or explicit XX markers confirm sampling. It removes Q flags, site quality-note periods, all ambiguous duplicate effort rows and inconsistent one-day labels. Before annual filters, there are 22,861 summer nights and 245,349 core individuals. Detailed rules are executable in files/prior_methods.py and are described in the cited prior publication.

Each trap-year needs at least ten confirmed nights in every May-September month. A pair uses consecutive years at one trap within one period. Each retained taxon has at least ten raw individuals in both years; each pair needs at least five shared taxa. The same set of taxa is used in both years of each pair, but sets can change among pairs. Countries have separate biological records; periods have separate years. Sites can recur across periods and weather can be correlated across countries. These are separate sample tests, not independent experiments. Main samples contain 7, 6, 2 and 2 sites in table order.

Unlike the prior statistic, every individual here has equal date weight. We retain monthly coverage filters but do not weight individuals by inverse sampled nights. The target is the distribution of recorded capture dates under the observed schedule. It is not the full emergence-date distribution or an effort-corrected seasonal distribution.

## Correction and assumptions

Let m_i be the sample mean date of taxon i, n_i its number of individuals, and s_i squared its sample date variance with denominator n_i minus one. For K taxa, define:

    B = mean_i (m_i - mean_j m_j)^2
    C = (1 - 1/K) mean_i (s_i squared / n_i)
    B_corrected = B - C

For fixed sample sizes and a fixed taxon set, suppose capture dates are independent and identically distributed within taxa and independent across taxa. If the true taxon mean is mu_i and its date variance is sigma_i squared, then Var(m_i) = sigma_i squared / n_i. Expanding B gives E[B] = Var_i(mu_i) + (1 - 1/K) mean_i Var(m_i). Since s_i squared is unbiased, E[B-C] = Var_i(mu_i). We leave negative corrected values unchanged.

These assumptions are a narrow diagnostic model. Individuals caught on one night share weather and sampling conditions. Counts can be overdispersed. Taxon dates can covary. Conditioning on a count threshold can select seasons and taxa. For dependent taxon errors, the expected extra term is trace(Sigma)/K minus sum(Sigma)/K squared, where Sigma is the covariance matrix of taxon mean errors. C does not estimate that general term. A small C slope therefore cannot exclude a large shared-night or capture effect. The correction also uses estimated sampling variances; no claim is made that the IID model is true.

For each outcome, we regress consecutive-year change on change in February-April country mean temperature, with change in May-September mean temperature, total February-September rain, and trap intercepts. Temperature is an equal-month mean; rain uses units of 100 mm. Trap intercepts in differences allow trap-specific linear trends in levels. Pair weights are equal. Errors cluster by the second year, with G/(G-1) times (n-1)/(n-k) correction. Intervals use t with G-1 degrees of freedom. The four-test family is the corrected outcome in four samples. Few years and adjacent pairs limit this inference; it is not robust to every form of serial dependence. Later Scotland has only three residual degrees of freedom. The early English result is fragile to coverage filters, as in the prior study.

## Checks and reproduction

files/analysis_plan.txt records the question and tests before correction estimates. We fixed empty matched-pair handling after a first run stopped. We added a non-null exact enumeration check after the first successful estimates. No result-dependent sample rule was added.

The code checks centered, individual-count date variances against second moments across the source taxon-years. It verifies slope additivity and exhaustive independent-date examples. The equal-mean example has zero expected corrected variance. An unequal-mean example with unequal sample sizes returns the true between-taxon variance. These checks test code and the model identity, not biological independence. files/validation.json reports numerical errors. A complete repeat run checks aggregate reproducibility in files/reproduction.json.

Use Python 3.12 and files/requirements.txt. From any directory, with the extracted bundle at PUBLICATION:

    python PUBLICATION/files/retrieve.py /absolute/new_external_inputs
    python PUBLICATION/files/analyze.py --datasets /absolute/new_external_inputs --out /absolute/new_external_output

To use the shared inputs on this machine:

    python PUBLICATION/files/retrieve.py /mnt/dell-data/shared_datasets --check-existing
    python PUBLICATION/files/analyze.py --datasets /mnt/dell-data/shared_datasets --out /absolute/new_external_output

Output directories must be new and outside the publication. Source records, taxon-year tables and year-pair tables are regenerated there and remain external. Compare results.csv and validation.json with the bundle. The retrieval script checks exact used content, allowing only changed archive wrappers or unused appended weather years. New authentication requirements or changed historical values can block future retrieval; do not silently accept them. All six present files match the pinned whole-file hashes. No signing key or private workspace is needed for analysis.

## Limits and next tests

The narrow independent-date correction is too small to remove the English point estimates. This result does not establish biological separation, loss of host synchrony, biodiversity harm or attribution to climate change. It does not test air pollution or daily weather extremes. Missing flights outside May-September, changes in generation mixtures, migrants, unequal effort, taxon selection, local weather and lamp response can each affect the target. The Scottish tests do not establish regional replication. The prior result and this test share all biological records. The next useful test is a shared-night covariance estimate or night-level sampling model, with local daily weather and full-season independent emergence observations. Independent regions and monitoring methods remain necessary.

## Attribution and rights

Contains data supplied by UK Centre for Ecology & Hydrology. Copyright UK Centre for Ecology & Hydrology. Source: Rennie, S. and co-authors (2017), UK Environmental Change Network (ECN) moth data: 1992-2015, NERC Environmental Information Data Centre, doi:10.5285/a2a49f47-49b3-46da-a434-bb22e524c5d2. Methods: Rennie and co-authors (2020), Earth System Science Data 12, 87-107, doi:10.5194/essd-12-87-2020.

Met Office weather: contains public sector information licensed under the Open Government Licence v3.0. Crown copyright. Source URLs and hashes are in provenance.json. External source terms apply to external raw and derived record tables; those materials are not bundled or relicensed. files/EXTERNAL_DATA_NOTICE.md preserves attribution. Our narrative, code, figure and aggregate statistical results use the exact SCI baseline license. Reused code retains the prior baseline MIT terms and attribution.

References: Jonason, D., Franzen, M. and Ranius, T. (2014), Surveying Moths Using Light Traps: Effects of Weather and Time of Year, PLOS ONE 9, e92453, doi:10.1371/journal.pone.0092453. Thomsen, P.F. and co-authors (2016), Resource specialists lead local insect community turnover associated with temperature, Journal of Animal Ecology 85, 251-261, doi:10.1111/1365-2656.12452.

Job: sci-1107-dell-climate-pollution-biodiversity-b3065eef5f8f. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. One worker; no agents. The signing identity is a campaign-machine key, not a personal authorship claim.
