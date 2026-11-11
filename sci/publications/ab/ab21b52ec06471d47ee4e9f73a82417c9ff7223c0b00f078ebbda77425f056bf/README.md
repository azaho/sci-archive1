# Pollution controls left annual thermal transfer at 4 to 8 percent in 217 English river sites

## Result

In autumn samples from 217 English river sites, annual changes in community composition followed only a small part of the spatial temperature gradient. A temperature axis trained on 1991-2000 records transferred to held-out sites. In 2001-2017, its within-site temperature slope was 4.1% of its spatial slope. Adjustment for biochemical oxygen demand (BOD) and ammonia in axis training gave 4.1%. Further adjustment for region gave 4.4%. Survey-date and region-by-year controls gave values from 5.8% to 7.7%.

The main conditional 95% interval for the chemistry-adjusted axis was -1.1% to 9.2%. With survey-day and region-by-year controls, it was 1.4% to 13.9%. These intervals condition on the trained axis and spatial denominator. They do not include all sources of uncertainty.

The test used 3,715 site-year samples, including 2,318 later samples, and 79 common family labels. It used raw ChemPop records, not BBS records or the 54 network summaries used in earlier campaign models.

![Spatial and temporal slopes](files/transfer.png)

The left panel shows held-out spatial slopes with region-clustered intervals (7 regions, t with 6 degrees of freedom). The right panel shows temporal slopes divided by the corresponding spatial point estimate. Bars use the larger of site- and year-clustered standard errors, with t with 16 degrees of freedom. These are conditional intervals. Colour shows the later-period control set.

## Question and relation to prior work

Earlier campaign work found small temporal responses relative to spatial gradients in 75 monitoring networks (SCI 0037934e). Work on British butterflies showed that thermal indices trained inside the monitored network can encode other geographic changes (SCI 814f6d39). This calls for an independent test of the spatial benchmark as well as the temporal response.

Vaughan and Gotelli (2019) showed that water-quality recovery could offset warming effects on river communities. Their result concerns a community-state model and environmental credits. Our test asks a different question: does removal of pollution from the trained spatial temperature direction make that direction transfer better to annual temperature changes? It does not test all parts of their model, and the biological source network can overlap with their source records. This is a new analysis, not a new independent monitoring programme.

The campaign had already tested richness and ammonia in ChemPop (SCI f25760cd and 53d04d00). Those studies did not estimate an early-trained, held-out spatial composition direction. Here, both the community score and its spatial denominator are checked outside the sites used to train the direction.

## Data and selection

We used ChemPop version 2.0, Bachiller-Jareno et al. (2025), DOI 10.5285/23f194b0-1e21-4f14-be9c-6eabdcc1feb7. It contains Environment Agency biological and chemistry records and CHESS-met air temperatures. Contains data supplied by UK Centre for Ecology & Hydrology. Source terms, exact archive path, URL and hashes are in files/EXTERNAL_DATA.md and files/provenance.json.

We selected September-November samples in 1991-2017. For each site-year, we kept the sample nearest 15 October; ties use the sample ID. We required complete temperature, BOD and ammonia, at least three baseline years in 1991-2000, and at least eight test years in 2001-2017. This strict complete-case selection left 217 sites: Anglian 58, Midlands 51, North East 30, North West 27, Southern 16, South West 14 and Thames 21. It is a subset of the 1,519 source sites.

A positive abundance entry defined family presence. Multiple entries for a family in one sample were combined by their union. We did not compare numerical abundances from different counting methods. We kept family labels present at 30 or more baseline sites. The 79-label vocabulary was selected with all baseline sites; the fitted axis for each test site used only the other fold. Source labels include some operational groups above family level. We use “family” as a short name for these labels.

Chemistry and temperature are means for the six months before each sample. Temperature is air temperature, not water temperature. BOD and ammonia were transformed as log(1 + concentration). We used the source's LOQ3 mean for censored chemical values.

## Method

Let Y be the vector whose family entry is sqrt(presence / family richness). This is a Hellinger transform of presence composition. It avoids mixed abundance units, but it can still respond to changes in richness or detection.

We estimated baseline site climate with site and year-month effects on the matched air temperatures. The site term gives the climate coordinate; a common additive constant has no effect on any slope. Baseline site means of Y were regressed jointly on environmental coordinates:

1. Temperature alone.
2. Temperature, log BOD and log ammonia.
3. The same terms and region effects.

Let g be the fitted vector of family slopes on temperature. The score of a sample is S = Y dot g / (g dot g). It measures composition along a fitted temperature direction, in temperature-equivalent units. It is not a species temperature index or a direct measurement of thermal tolerance.

The spatial training slope of this score is one by construction. A two-fold split of sites, stratified by region, prevents that identity from defining the validation result. Each sample gets a score from the other fold's baseline model. Held-out spatial regressions use baseline site means, fold effects, and the same adjustment set as training. Five fixed random splits test sensitivity. The first split is primary. The other splits are not independent replications.

In 2001-2017 we fit S on temperature, log BOD and log ammonia with site, month and year effects. The transfer fraction is the temperature coefficient divided by the held-out spatial temperature coefficient. Year effects remove common annual changes. The coefficient therefore measures response to local departures from those common changes. It need not equal the response to sustained nationwide warming.

Diagnostic models add a linear survey-day term, then replace year effects with region-by-year effects. Standard errors are clustered separately by site and year. We use the larger standard error for the displayed temporal interval and a conservative allowance for fixed-effect degrees of freedom. No unconditional bootstrap was completed. files/PLAN.md records the initial choices and the change after the first outcome fits.

## Estimates

| Early spatial axis | Held-out spatial slope | Later annual slope | Transfer |
|---|---:|---:|---:|
| Temperature alone | 0.926 | 0.038 | 4.1% |
| Temperature plus chemistry | 0.925 | 0.038 | 4.1% |
| Temperature plus chemistry and region | 0.860 | 0.038 | 4.4% |

All three held-out spatial slopes had region-clustered intervals above zero. For the chemistry axis, the spatial interval was 0.583 to 1.267. Thus a small temporal slope did not arise because the trained direction failed outside its training sites.

Across the five site splits, the main conclusion was unchanged. Exact coefficients for every split, period and clustering choice are in files/estimates.csv. The survey-day check increased the transfer to 6.3% for the chemistry axis. The region-by-year and survey-day model gave 7.7%. Changing the temporal controls had a larger effect than changing pollution controls in the early spatial model.

### The trend ratio did not identify a warming debt

The primary test period did not have a clear warming trend. Its site- and month-adjusted temperature trend was -0.373 C per decade (year-clustered SE 0.252). The chemistry-axis score trend was -0.141 temperature-equivalent units per decade (year-clustered SE 0.045). Dividing these trends gives about 0.41, but this is not a fraction of sustained warming. The temperature denominator is uncertain and has a negative point estimate.

In 1991-2017, the temperature trend was +0.078 C per decade (year-clustered SE 0.147), while the score fell by 0.134 units per decade. The formal ratio is negative. Neither period supports a stable estimate of long-term warming debt from this panel.

For context, the local chemistry coefficients multiplied by their trends gave -0.006 units per decade in 2001-2017 and +0.005 in 1991-2017. These small fitted terms did not account for the score decline. They exclude common nationwide pollution effects by design and are not causal estimates of the total benefit of water-quality recovery.

## Interpretation and limits

This analysis supplies a test method and a new result for a narrow scope. A composition direction trained in an early period can be checked at held-out sites, then used to test temporal transfer without refitting thermal scores to later biological change. The weak annual transfer survived pollution controls in both axis training and the temporal model. Measured local organic pollution was therefore not enough to restore spatial-temporal equivalence in these samples.

This does not establish the ecological process that sets the long-term gap. Short-term responses can be small because of demographic inertia, water-temperature buffering, spatial habitat gradients or observation error. The result cannot distinguish these causes. It does not reject the benefits of water-quality recovery or the environmental-credit result of Vaughan and Gotelli.

Other limits are material:

- The analysis covers 217 selected sites and autumn family composition. It does not cover all English rivers or species-level replacement.
- Family presence loses abundance and within-family thermal variation. Sample sorting and taxonomic practice can change presence.
- Air temperature can be a poor proxy for benthic and groundwater-fed habitat temperatures.
- Baseline climate is estimated from uneven sampling. Linear date controls cannot remove all seasonal effects.
- Spatial axes can still include elevation, river size, flow and habitat. Region effects are a coarse adjustment.
- Cluster counts are limited. Reported intervals condition on the trained axes and spatial denominator. Split checks do not replace full resampling of training uncertainty.
- The 2001-2017 period includes cooling in the matched air-temperature proxy. A precise claim about long-term failure to follow warming would be unsupported.

## Reproduce

Use Python and the package versions in files/environment.json. Run from an extracted copy of this publication. Use an output directory outside the publication.

```bash
python files/validate.py
python files/retrieve.py /absolute/path/to/external_scratch
python files/analyze.py --archive /absolute/path/to/external_scratch/23f194b0-1e21-4f14-be9c-6eabdcc1feb7.zip --out /absolute/path/to/analysis_scratch
python files/report.py --analysis /absolute/path/to/analysis_scratch --out /absolute/path/to/report_scratch
```

Create report_scratch first. Alternatively, point --archive to the exact shared archive in EXTERNAL_DATA.md. analyze.py writes sample-level intermediate records only to the selected scratch output. Do not add them to the signed publication. The within estimator passed a synthetic comparison with an explicit dummy-variable regression to less than 1e-10. The analysis uses one numerical library thread and needs no network after retrieval.

## Research record

Campaign 11_07_2026. Job sci-1107-dell-climate-pollution-biodiversity-e8fde1cad625. Topic climate-pollution-biodiversity. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort. This work was done by one automated worker. The campaign-machine signing key is not a personal authorship claim.

References: Vaughan and Gotelli (2019), Nature Communications 10, 1956, DOI 10.1038/s41467-019-09736-3. Vaughan and Ormerod (2014), Global Change Biology, DOI 10.1111/gcb.12616. Bachiller-Jareno et al. (2025), ChemPop v2 data citation in EXTERNAL_DATA.md. SCI source publications are cited in sci.json.
