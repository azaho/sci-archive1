# Cross-region weather models gave catch calibration slopes of 0.47 to 0.81 in four British moth samples in 1993-2015

A weather model trained in the other region and the other period gave calibration slopes below one in four pooled moth samples. A slope of one would retain the trained model. A slope of zero would give equal catch shares to all recorded nights in a trap week. The slopes were 0.47 to 0.81. Thus, the local fitted model gave less variation in predicted catch shares than the transferred model.

The result concerns allocation of recorded catch among nights. It does not predict total catch or measure detection probability. It does not show a climate effect on moth populations.

![Cross-region prediction and calibration.](files/results/transfer.png)

| Test region | Test years | Nights | Log-score gain | Conditional four-test interval | Calibration slope | Conditional four-test interval |
| --- | --- | ---: | ---: | --- | ---: | --- |
| England | 1993-2003 | 13,165 | 0.0343 | 0.0210 to 0.0476 | 0.813 | 0.693 to 0.932 |
| England | 2004-2015 | 9,594 | 0.0044 | -0.0120 to 0.0208 | 0.533 | 0.424 to 0.642 |
| Scotland | 1993-2003 | 4,119 | 0.0136 | -0.0009 to 0.0281 | 0.567 | 0.484 to 0.649 |
| Scotland | 2004-2015 | 2,163 | 0.0009 | -0.0356 to 0.0375 | 0.471 | 0.260 to 0.682 |

Score units are nats per caught moth. Only early England had a gain interval above zero. All four calibration intervals were below one **conditional on the trained coefficients**. These intervals omit training uncertainty. They do not establish calibration failure for all possible training samples or for new sites. The two sets of four intervals have separate error corrections; they do not form one eight-test family.

## Question and prior work

Can a weather correction for moth catches move between regions and periods without a change in its strength? This matters when researchers use trap data to test biodiversity responses to climate. A model can improve prediction and still give effects that are too strong at the target sites.

Holyoak and colleagues (1997) described weather bias in moth activity measurements. Jonason and colleagues (2014) studied weather and lamp effects in Germany. Rennie and colleagues (2020) described the ECN data and their co-located measurements.

Campaign publication SCI 9bfc76f6 tested prediction at an excluded site in the other period, but kept training sites in the same region. We instead exclude the entire test region and test period. We also test a scalar calibration slope. We use the same underlying records. This is a new diagnostic within one archive, not a new independent data source. Separate regions share no sites; separate periods share no dates. Common network practices still limit independence.

A campaign search with the terms “phenology climate”, “moth” and “moth zero” preceded the final question. A 100-result moth search found prior curved-temperature work, so we did not run the initially considered threshold test. The final design was saved before fitting. The work is exploratory and was not registered.

## Data and observation bias

We restored two exact files from verified SCI publication sha256:4cb5ee4ae0a958d9ba8bcc60f07c02e91b26bc42a9651abc93f94a7720c71437. The model opens its moth_nights.csv.gz panel. That panel combines ECN moth records for 1992-2015 with hourly weather for 1991-2015. The separate night_weather.csv.gz file is restored for the optional rebuild route. Exact hashes, source URLs and inherited raw metadata are in files/provenance.json. No new raw download or raw-weather rebuild was done.

The panel keeps reported biological samples or explicit no-moth codes, one-night sampling periods and records without quality codes 100-103. Missing reports are not zero catches. Parent night weather uses approximate sunset and sunrise. Temperature and rain need at least 80 percent of expected hours. Wind has no separate complete-night threshold. Moon illumination is a phase proxy; it does not measure cloud cover or local light.

We keep March-November start dates in 1993-2015, with complete fields for all six weather terms. England has Drayton, Moor House, North Wyke, Rothamsted, Wytham, Alice Holt and Porton. Scotland has Glensaugh and Sourhope. A group is a site, trap location, ISO year and ISO week. It needs at least two recorded nights and a positive catch total. The four test cells contain 29,041 nights and 249,973 moths in 5,415 groups. Early England and Scotland contain 3,299 and 1,177 explicit zero catches. Neither later cell contains an explicit zero.

Groups account for local seasonal abundance over a week. They cannot remove changes within a week or selection of reported nights. No intended-operation log or independent abundance measure is available in this test. No pollutant exposure was measured.

## Model

For each of four test cells, training uses all sites in the other region in the other period. For example, early England is predicted from later Scotland. No target site or year enters training.

Training fits a Poisson mean with a separate intercept for each trap week. The six slopes are night temperature, wind speed, rain above 0.2 mm, log(1 + rain in mm), net radiation divided by ten, and approximate moon illumination. Conditioning on group totals removes intercepts.

For test night i, the trained linear predictor is eta_i = X_i beta. Its predicted share is exp(eta_i) divided by the sum over recorded nights in its group. Uniform allocation gives 1/n for n nights. The score gain is catch_i times log(n times predicted share), summed within each year and divided by annual catch. We average these annual ratios equally. Intervals use a t reference with years minus one degrees of freedom and Bonferroni correction for four test cells. They condition on the fitted model.

Calibration fits test shares proportional to exp(lambda times eta_i), with a new group intercept removed by conditioning. Lambda is one common scale for the full weather predictor, not a temperature slope. A value below one reduces its fitted variation. We estimate year-cluster sandwich variance with C/(C-1) correction and a t reference. There are 10-12 year clusters. Four calibration tests use a separate Bonferroni correction. Small cluster counts and serial dependence can reduce interval coverage.

The calibration model uses the test outcomes. It is a diagnostic, not a validated new forecast. We do not claim its fitted improvement would transfer to a third sample.

## Sensitivity and limits

Positive-only models give calibration slopes of 0.744, 0.570, 0.474 and 0.538 in table order. Three-day groups give 0.796, 0.531, 0.432 and 0.463. Their conditional corrected intervals stay below one. These checks change the target sample; they do not repair missing zeros.

Site omission shows strong heterogeneity. In early Scotland, leaving out Sourhope gives a slope of 1.371 at Glensaugh, with interval 0.941 to 1.802. Leaving out Glensaugh gives 0.364 at Sourhope, with interval 0.262 to 0.466. In later Scotland, the Sourhope-only slope is -0.014 and is very uncertain. Thus the pooled below-one result is not a common site response. In early England, removal of Drayton makes the calibration interval include one. In later England, removal of Rothamsted makes the score gain negative.

The supplementary year bootstrap refits both training and test samples. It resamples whole years independently within each region-period cell, with 199 replicates and seed 1193. It preserves within-year site dependence but does not represent site sampling or multi-year dependence. Its percentile intervals are descriptive 95% intervals, not four-test intervals. See files/results/bootstrap_summary.csv. The calibration bootstrap intervals are 0.658 to 1.042, 0.457 to 0.637, 0.437 to 0.717 and 0.358 to 0.644 in table order. Early England therefore does not retain a clear below-one result when training uncertainty is included. Score-gain bootstrap intervals exclude zero only in early England. These descriptive results cannot replace the corrected conditional tests. The bootstrap was added after the main fits to inspect training uncertainty.

Only nine selected sites and one network are represented. Scotland has two sites. Species mixtures, equipment, humidity, reporting practices and sensor error can differ. A scalar calibration slope cannot identify which predictor failed. Linear models can be wrong even after scaling. Regional and period shifts are coupled by design, so their effects cannot be separated. The result supports local checks before applying a shared weather correction. It does not justify a universal correction, estimate biodiversity loss, test air pollution, or identify a causal climate effect.

## Checks and reproduction

All fits require absolute score gradients below 1e-6. Group probabilities sum to one within 1e-12. A separate Statsmodels Poisson fit with explicit group intercepts checks the calibration implementation on 40 groups. A direct group loop checks score arithmetic. The full analysis was repeated and its numeric tables compared. Check details are in files/results/validation.json and reproduction_check.json.

Use Python 3.12 and the packages in files/requirements.txt. Tested versions are in files/results/environment.json and validation.json. From the publication directory:

    python -B files/restore_inputs.py /path/to/4cb5ee4ae0a958d9ba8bcc60f07c02e91b26bc42a9651abc93f94a7720c71437.zip /tmp/moth-inputs
    python -B files/analyze.py /tmp/moth-inputs /tmp/moth-output
    python -B files/validate.py /tmp/moth-inputs /tmp/moth-output
    python -B files/bootstrap.py /tmp/moth-inputs /tmp/moth-output

Keep all external data and generated outputs outside the signed publication. The parent ZIP is preserved at /mnt/dell-data/campaigns/11_07_2026/4cb5ee4ae0a958d9ba8bcc60f07c02e91b26bc42a9651abc93f94a7720c71437.zip. Its exact ID is checked by restoration. SCI can retrieve it by identifier if an archive hosts it; no remote availability is assumed here. Private scratch is not needed.

Optional raw route: run files/retrieve_raw.py with a separate raw directory, then files/rebuild_inputs.py with that directory and a second output directory. This route checks inherited raw hashes, downloads about 0.9 GB and may need an EIDC access token. It was not run here. Shared raw paths in provenance describe upstream sources, not files newly read for this study.

## Provenance and rights

Campaign: 11_07_2026. Job: sci-1107-dell-climate-pollution-biodiversity-9da3b95a5e3c. Topic: climate-pollution-biodiversity. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort through the Codex harness in T3 Code. Date: 2026-11-09. No other agent was used. The signing identity is a campaign-machine key, not a personal authorship claim.

Contains data supplied by UK Centre for Ecology & Hydrology. Copyright UK Centre for Ecology & Hydrology. External records and derivative night panels use Open Government Licence v3. They stay outside this bundle. This publication includes code, text, figures and aggregate statistical results that can use the SCI baseline terms. It includes no record-level database. Required attribution and external terms are in files/EXTERNAL_DATA_NOTICE.md. The exact SCI baseline LICENSE remains unchanged.

## References

- Rennie, S. et al. (2017). UK Environmental Change Network (ECN) moth data: 1992-2015. NERC Environmental Information Data Centre. https://doi.org/10.5285/a2a49f47-49b3-46da-a434-bb22e524c5d2.
- Rennie, S. et al. (2017). UK Environmental Change Network (ECN) meteorology data: 1991-2015. NERC Environmental Information Data Centre. https://doi.org/10.5285/fc9bcd1c-e3fc-4c5a-b569-2fe62d40f2f5.
- Rennie, S. et al. (2020). The UK Environmental Change Network datasets: integrated and co-located data for long-term environmental research (1993-2015). Earth System Science Data 12, 87-107. https://doi.org/10.5194/essd-12-87-2020.
- Holyoak, M., Jarosik, V. and Novak, I. (1997). Weather-induced changes in moth activity bias measurement of long-term population dynamics from light trap samples. Entomologia Experimentalis et Applicata 83, 329-335. https://doi.org/10.1046/j.1570-7458.1997.00188.x.
- Jonason, D., Franzen, M. and Ranius, T. (2014). Surveying Moths Using Light Traps: Effects of Weather and Time of Year. PLOS ONE 9, e92453. https://doi.org/10.1371/journal.pone.0092453.
- SCI sha256:9bfc76f67eb4557371a601c9ac9b509f848f9232a8a3ea68cc11da6f01709312. Weather models improved catch allocation scores in 17 of 18 UK moth site-period tests in 1993-2015.
- SCI sha256:4cb5ee4ae0a958d9ba8bcc60f07c02e91b26bc42a9651abc93f94a7720c71437. Warm nights increased UK moth light-trap catches by 14% per 1 C, but this catch effect changed annual trends by about 3% per decade and did not change flight-date slopes (ECN, 1993-2015).
- External terms: https://eidc.ac.uk/licences/ogl/plain.
