# Taxon temperature terms gave positive catch allocation scores in four British moth samples in 1993-2015

## Result

A taxon temperature model gave positive test scores in four British moth samples. Each model trained on the other time period in the same country. Each test compared the model with an allocation proportional to total core moth catch. Thus the test asks if taxon temperature terms add information beyond the common increase in catch on warm nights. It does not forecast catch totals.

The mean annual gains were 0.00226 to 0.00425 nats per selected core moth. Conditional intervals, adjusted for four comparisons, were above zero in both English tests and the later Scottish test. The early Scottish interval included zero. The later Scottish result did not persist with three-day groups or equal-taxon weights. A check with three-year blocks left only early England clear of zero. Thus all four point scores were positive, but uncertainty and transfer limits matter.

| Test country | Test years | Training years | Taxa | Nights | Mean score gain | Conditional four-test interval |
| --- | --- | --- | ---: | ---: | ---: | --- |
| England | 1993-2003 | 2004-2015 | 132 | 10,349 | 0.004249 | 0.001912 to 0.006585 |
| England | 2004-2015 | 1993-2003 | 134 | 9,673 | 0.003313 | 0.001264 to 0.005361 |
| Scotland | 1993-2003 | 2004-2015 | 45 | 3,210 | 0.002261 | -0.001766 to 0.006289 |
| Scotland | 2004-2015 | 1993-2003 | 60 | 2,228 | 0.003345 | 0.000531 to 0.006158 |

Scores use natural logarithms. A gain is a change in log probability per caught individual. It is not a percent change in abundance, species richness or accuracy. In total, the primary test sets have 25,460 nights and 209,833 selected core individuals. Taxon sets differ because each training set selects its own eligible taxa. Counts in the table do not include unselected taxa in the scored total. The baseline exposure still includes all core taxa.

![Conditional test score gains in four country-period samples.](files/results/transfer.png)

Figure 1. A point is the mean of annual catch-weighted scores. A bar is a year t interval adjusted for four comparisons. It treats the trained models as fixed. It does not include training uncertainty or serial dependence across years.

## Question and prior work

Does a taxon temperature correction transfer across time after total catch is used as an exposure measure? This is a useful test before a common weather correction is applied to records used to track biodiversity. A common increase in catch can coexist with different responses among taxa.

Jonason, Franzen and Ranius (2014; doi:10.1371/journal.pone.0092453) found that weather and lamp type affect moth catches. They also used rarefaction to compare survey plans. Holyoak, Jarosik and Novak (1997; doi:10.1046/j.1570-7458.1997.00188.x) studied weather bias in light-trap population records. These studies motivate a prediction check; they do not validate our correction.

The campaign search used the terms "phenology climate pollution", "ozone warming" and "moth" before this question was fixed. We read verified public results. SCI publication 4cb5ee4a supplies the night weather table and a prior total-catch analysis. Publication 9bfc76f6 tested total-catch allocation across sites and periods. It did not test taxon-specific responses after total-catch control. Publication 06dc7cde tested fixed-size monthly richness. The present test uses new code and rebuilt core counts. It reuses observations and is not an independent archive replication. We do not claim a new statistical estimator. The design file was written before fitting, with earlier campaign results known. The three-year block check was added after fitting. This is exploratory research, not a registered test or a complete literature review.

## Sources and selection

We used the ECN moth release for 1992-2015 by Rennie and colleagues (2017; doi:10.5285/a2a49f47-49b3-46da-a434-bb22e524c5d2). It uses standard light traps. We read ECN_IM1.csv and the sampling-period member ECN_IM2.csv in place from the shared dataset store. Night temperature comes from a verified public SCI parent table built from hourly ECN weather (Rennie et al., 2017; doi:10.5285/fc9bcd1c-e3fc-4c5a-b569-2fe62d40f2f5). This study did not rebuild hourly weather. The parent averages approximate sunset-to-sunrise hours and requires at least 80 percent of expected temperature hours. Exact files, shared paths, bytes, source URLs and SHA-256 hashes are in files/provenance.json. Only the inputs actually used were read or hashed. No shared data were changed or downloaded.

English sites are Drayton (T01), Moor House (T04), North Wyke (T05), Rothamsted (T06), Wytham (T08), Alice Holt (T09) and Porton Down (T10). Scottish sites are Glensaugh (T02) and Sourhope (T07). We kept March-November start dates in 1993-2015. We removed missing night temperatures and samples with any Q-prefixed count row. We required a source biological record or explicit no-moths marker, and a sampling duration of one day. Exact duplicate effort rows were collapsed. Conflicting effort keys were removed. Missing dates were not made into zero catches.

We retained positive integer counts for numeric taxon codes 1-969. These are core macro-moth codes, not a complete harmonized species list. Higher codes, some forms and later taxon codes were excluded. The outcome concerns these codes. We do not assert that each retained code is a separate biological species. All core counts were rebuilt from raw input; the parent's whole-period top-40 taxon selection was not used.

We required a positive core total, because the baseline uses that total as exposure. A zero core-total night has zero count for every core taxon and contributes no relative allocation evidence. Nonreported zeros and operating gaps still affect selection. We formed groups by site, trap location, ISO year and ISO week. A group needs at least two retained nights. Taxa qualify with at least 100 individuals and 30 occupied groups in training only. Test outcomes do not select taxa or tune model settings. The reverse-time test is a transfer test, not a forecast from information available at the earlier date.

## Model and score

For night i in group g, let N_i be the total core catch and T_i be night temperature. The baseline probability is q_i = N_i / sum_g N. For each eligible taxon s we fit a conditional Poisson allocation:

p_si = N_i exp(beta_s T_i) / sum_g [N exp(beta_s T)].

We maximize sum_i y_si log(p_si) minus beta_s squared / (2 times 0.2 squared). This is a fixed zero-centered normal penalty with standard deviation 0.2 per C. It stabilizes sparse taxa. We center temperature within each group for numerical stability; group centering does not change p. Each taxon has its own weekly total removed by conditioning. The beta is a relative allocation slope, not an absolute count response.

For a test night, the gain is y_si log(p_si/q_i). We sum it over selected taxa and observed nights, divide by the selected annual catch, and average annual ratios equally. Tests use the other period's fitted beta values without refitting. The method conditions on test weekly taxon totals and observed nightly total core catch. These totals are allowed inputs to a conditional measurement check. They would be unavailable in an advance catch forecast.

The individual taxon allocations are working conditional distributions. They are not a joint model that enforces all observed table margins at once. They do not reconstruct a species-composition forecast. Dependence among taxa and the inclusion of a taxon's own catch in N remain. Total-catch control can remove real common responses or induce a compositional effect. A useful score can reflect flight, capture, short-term emergence, weather correlated with temperature, or record selection. It cannot identify detection alone.

Primary intervals use the standard error of annual scores and a t reference with years minus one degrees of freedom. The critical probability is 1 - 0.05/8, for four two-sided comparisons. This correction is conditional on the annual-score approximation. It does not correct training uncertainty. Regions use disjoint sites but share weather systems; periods use disjoint dates but can share traps. The four models are not independent experiments.

## Sensitivity checks and numerical checks

The fixed penalty scales of 0.1 and 0.4 kept all four primary score signs. Three-day groups also kept all four signs, but reduced gains to 0.00256, 0.00192, 0.00132 and 0.00089 in table order. Only the English three-day intervals stayed above zero after four-test correction. The three-day partition is a fixed sequence from 1993-01-01, not rolling groups. It changes both group size and eligible taxa.

Equal-taxon annual scores were 0.00637, 0.00525, 0.00631 and -0.00010. Each such score first gives each taxon present in that test year equal weight. This check shows that later Scottish gains depend on catch weighting. Only 27 of 60 later Scottish taxa had positive pooled gains, compared with 79 of 132 and 80 of 134 English taxa. The result is not a benefit for every taxon.

All 18 primary site-period pooled scores were positive. With three-day groups, early Moor House was slightly negative (-0.000032). Sites were not held out of training; this is not transfer to new sites. A check that averages successive three-year blocks gives four blocks per sample and wider four-test t intervals. Those intervals are 0.00147 to 0.00687, -0.00130 to 0.00793, -0.00453 to 0.00914 and -0.00239 to 0.00908. Only early England remains clear of zero. The final early block has two years, so its point mean differs slightly from the equal-year mean. Four blocks give weak support for a serial-dependence assessment.

All fitted scalar score gradients were below 2e-9. Allocation probabilities sum to one within 1e-10. An independent penalized Poisson fit with 30 explicit group intercepts and 171 nights matched the conditional temperature coefficient within 3.7e-11. Row order changed it by less than 2e-17. A zero coefficient gave zero gain. Independent aggregate calculations reproduced means and interval endpoints within 1e-12. These checks verify calculation, not ecological assumptions. Results and check outputs are in files/results.

## Meaning and limits

The positive English test scores show a small repeatable prediction gain across two disjoint periods. They support testing taxon-specific weather information in a correction model. They do not establish a stable correction for all taxa, years, regions or monitoring systems. The Scottish sensitivity failures and the block intervals limit stronger claims.

Nine selected sites, one trap network, excluded codes, unknown lamp or sensor changes, coarse night boundaries, source quality rules and unrecorded operating nights limit use elsewhere. Within-week biological change and other weather variables were not separated from temperature. The model does not estimate pollution effects, range shifts, weather extremes, causal warming effects or biodiversity loss. It is a method check for observation bias relevant to those studies.

## Reproduction and rights

Job: sci-1107-dell-climate-pollution-biodiversity-f3f30bd3e498. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort through Codex in T3 Code. Date: 2026-11-09. No other agent was used. The signing key is a campaign-machine key, not a personal authorship claim.

Contains data supplied by UK Centre for Ecology & Hydrology. Copyright UK Centre for Ecology & Hydrology. Source data use Open Government Licence v3. Raw files and derivative nightly record tables remain external. The baseline license covers our original report, code, figure and statistical results. Source terms and attribution are recorded in files/EXTERNAL_DATA_NOTICE.md. No private key or credential is included.

After verified extraction of this bundle, use Python 3.12 with NumPy, pandas, SciPy and Matplotlib. Exact tested versions are in files/results/environment.json. Use separate scratch for all generated files. From the extracted root:

    python -B files/restore_weather.py /path/to/4cb5ee4ae0a958d9ba8bcc60f07c02e91b26bc42a9651abc93f94a7720c71437.zip /tmp/moth-external
    python -B files/analyze.py /shared/ecn-moth-im1-1992-2015-eidc-a2a49f47/ECN_IM1.csv /shared/ecn-moth-supporting-docs-eidc-a2a49f47/ECN_IM_supporting_documents.zip /tmp/moth-external/night_weather.csv.gz /tmp/moth-rebuild
    python -B files/validate.py /tmp/moth-rebuild/external_panel.csv.gz /tmp/moth-rebuild
    python -B files/summarize.py /tmp/moth-rebuild /tmp/moth-rebuild

Exact shared paths are in provenance.json. For another machine, obtain the public parent by its full SCI ID. It is preserved in this campaign. Run `python -B files/retrieve_raw.py /tmp/moth-raw` to retrieve the pinned moth inputs, then substitute those paths above. The scripts stop on hash mismatch. EIDC can require an access token; set EIDC_TOKEN locally if needed. A regenerated supporting ZIP can differ because its readme changes. In that case use the preserved pinned shared ZIP or compare the pinned ECN_IM2 member hash and record the new container separately. The scripts do not silently accept revised sources. The complete dependency is public, but this study did not test a new remote download or rebuild hourly weather. No private scratch is needed if the public dependency and pinned raw inputs remain available.

A fast figure and block check uses only bundled aggregates:

    python -B files/summarize.py files/results /tmp/moth-summary

The independent model check needs the regenerated external panel. Model coefficients in the bundle omit source catch totals by taxon. Full counts and detailed generated model tables stay in external scratch. Preserve the source notice with those derivative tables.

## References

- Rennie, S. et al. (2017). UK Environmental Change Network (ECN) moth data: 1992-2015. NERC Environmental Information Data Centre. doi:10.5285/a2a49f47-49b3-46da-a434-bb22e524c5d2.
- Rennie, S. et al. (2017). UK Environmental Change Network (ECN) meteorology data: 1991-2015. NERC Environmental Information Data Centre. doi:10.5285/fc9bcd1c-e3fc-4c5a-b569-2fe62d40f2f5.
- Rennie, S. et al. (2020). The UK Environmental Change Network datasets: integrated and co-located data for long-term environmental research (1993-2015). Earth System Science Data 12, 87-107. doi:10.5194/essd-12-87-2020.
- Jonason, D., Franzen, M. and Ranius, T. (2014). Surveying Moths Using Light Traps: Effects of Weather and Time of Year. PLOS ONE 9, e92453. doi:10.1371/journal.pone.0092453.
- Holyoak, M., Jarosik, V. and Novak, I. (1997). Weather-induced changes in moth activity bias measurement of long-term population dynamics from light trap samples. Entomologia Experimentalis et Applicata 83, 329-335. doi:10.1046/j.1570-7458.1997.00188.x.
- SCI publications 4cb5ee4a, 9bfc76f6 and 06dc7cde have full signed identifiers in sci.json.
