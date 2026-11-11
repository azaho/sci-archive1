# Biomass per recorded species made 77% of a nutrient contrast for novel plants in warmed tundra plots

Nutrient addition raised the biomass of novel plants after seed addition in one warmed tundra experiment. An exact split assigned 77% of this contrast to biomass per recorded novel species, rather than the number of recorded novel species. The 95% bootstrap interval was 68-90%. This is a new quantitative test of published data. It is not a new discovery that nutrients affect plant invasion.

## Question and prior evidence

SCI studies found weak community thermal change relative to spatial temperature gradients across monitoring networks (SCI 0037934e). Bird source-distance results suggest that access to colonists can limit change (SCI 79a502af). We ask a different question: after seeds reach a site, can a resource constraint limit their contribution to biomass more than their recorded presence or richness?

Pichon, Kaarlejarvi and Eskelinen (2023; DOI 10.1111/ele.14219) already showed that seed-origin effects depended on nutrients, herbivores and warming. They also reported resident displacement. Our added contribution is an exact split of the nutrient contrast into recorded richness and biomass per recorded species, with uncertainty, a plot-level treatment test and an independent numerical audit. We do not claim the general product split or resource limitation as new methods or concepts. We use a different experiment from the campaign's bird, butterfly, moth and plant-transplant data.

## Data and design

We used Dryad version 411478 (2023-09-25; DOI 10.5061/dryad.n5tb2rc0p). The public release has endpoint observations from 2019 for an experiment started in 2009 at Kilpisjarvi, Finland. It has 56 whole plots: seven for each warming, nutrient and herbivore combination. Each plot has one seeded and one unseeded 25 x 25 cm subplot. Seeds from 14 novel and 11 local species were added in 2009 and 2010. Novel means absent from the site at the start; it does not mean that all those species had high thermal affinity.

NPK addition was a strong resource treatment. The warming chambers were removed during reindeer grazing. Warming mainly affected spring and autumn air temperature. This experiment does not represent year-round warming or ordinary atmospheric nitrogen deposition. The release gives richness and biomass for origin groups, not individual species. Only the all-groups data table was used in computation. Hashes, source paths, licenses and retrieval details are in files/EXTERNAL_DATA.md.

## Estimates and uncertainty

Let B be mean novel biomass in a group, R be mean recorded novel richness, and Y = B/R. Y is total novel biomass divided by total novel species records. It is not a mean growth rate or a species-level trait. For a nutrient contrast, with 0 for no added nutrients and 1 for added NPK:

B1 - B0 = (R1 - R0)(Y1 + Y0)/2 + (Y1 - Y0)(R1 + R0)/2.

This symmetric split is exact and gives equal weight to the two orders of changing the factors. The first term is the recorded-richness part; the second is the biomass-per-recorded-species part. We also split B = P M, where P is the fraction of subplots with any novel plant and M is mean novel biomass among positive subplots. Neither split is causal mediation. Changes in species identity, individual size, abundance, survival and measurement can all enter Y or M.

For the intervention estimate, we first subtract unseeded from seeded novel biomass within each whole plot. We then compare this paired response between nutrient treatments within warmed plots, with equal weight for the two herbivore conditions. We use 10000 bootstrap draws within each of the eight whole-plot treatment cells. Each draw keeps the two seed subplots together. Intervals are nominal percentile intervals. A two-sided treatment-label test keeps seven nutrient labels in each warmed herbivore stratum. It tests a sharp null of no nutrient effect on the paired response. The analysis and choice of warmed contrast are exploratory and followed data inspection; intervals do not correct for selection.

## Results

| Seed-added condition | Plots with novel plants | Mean novel richness | Mean novel biomass, g | Biomass per species record, g |
|---|---:|---:|---:|---:|
| Unwarmed, no added NPK | 12/14 | 1.929 | 3.748 | 1.943 |
| Unwarmed, added NPK | 13/14 | 2.071 | 5.231 | 2.525 |
| Warmed, no added NPK | 10/14 | 1.143 | 0.132 | 0.116 |
| Warmed, added NPK | 13/14 | 2.000 | 6.941 | 3.471 |

All biomass values refer to a 25 x 25 cm subplot, not a square metre. In warmed, seed-added plots, the nutrient biomass contrast was 6.809 g (95% interval 3.453-10.529). The recorded-richness part was 1.537 g (0.419-2.934). The biomass-per-recorded-species part was 5.272 g (2.776-7.910), or 77.4% (68.2-90.5%) of the contrast. Biomass per species record rose about 30-fold.

The separate presence split assigned 0.821 g to the fraction of plots with any novel species and 5.988 g to biomass among positive plots. The latter supplied 87.9% (77.1-100.0%). Thus the main result does not depend on using presence rather than richness, though the numerical shares differ. It is incorrect to identify these terms with colonisation or demographic growth rates.

After correction with the paired unseeded subplots, the nutrient difference in the seed-addition response was 6.790 g (3.438-10.514). The two-sided label-test p value was 0.000300 from 10000 draws. Removing any one warmed whole plot left the equally weighted contrast between 5.389 and 7.454 g. The effect is not due to a single plot.

The unwarmed seeded nutrient contrast was uncertain: 1.483 g (-7.949 to 9.230). Its ratio-based component shares are not stable because the total contrast can cross zero. Most importantly, the warming difference in the paired nutrient contrasts was 5.325 g (-3.257 to 14.989). The study does not establish that warming makes the nutrient response larger. A result within warmed plots is not evidence for a warming interaction.

![Novel biomass and exact components](files/evidence.png)

The left panel shows seeded group means. The right panel shows the warmed seeded contrast components and the nutrient difference in paired seed-addition responses. Error bars are nominal stratified-bootstrap 95% intervals. The first two estimates sum to the seeded contrast; the third also uses the unseeded controls.

## Meaning and limits

This test places a quantitative constraint on an arrival-only account of this experiment. Equal seed input did not produce similar novel biomass across resource conditions. Novel plants were recorded in most warmed plots without NPK, yet their biomass was small. Most of the measured nutrient contrast lay beyond the number of recorded species. This supports studying resource constraints after arrival, alongside source access, when explaining community change.

It does not assign any fraction of the bird or multi-network thermal gap to nutrients. We fitted no thermal index and no spatial temperature benchmark. We measured no pollution exposure. The NPK treatment adds three nutrients at high dose, so it cannot identify a nitrogen-specific effect. There is one site and one endpoint year, only seven plots per factorial cell, and no independent regional or temporal replication. Seeded mixtures also included local species, so the experiment cannot isolate effects of adding novel seeds alone. Neighbouring subplots may exchange seeds or share roots. Site-level plant presence differs from subplot records. The yield split cannot separate within-species growth from changes in which species dominate. These limits prevent a general claim that nutrient supply explains weak climate tracking.

The next decisive test needs repeated species-resolved abundance and demography after controlled arrival, across sites with measured nutrient supply. It must compare thermal and resource responses without treating recorded establishment as full community adjustment.

## Reproduction and rights

files/REPRODUCE.md gives commands. files/analyze.py regenerates the aggregate tables and figure from the exact hashed external data member. files/audit.py checks the main estimate through an independent reader. Data row counts and origin-group totals passed checks. The publication contains original code, narrative, aggregate estimates and a static figure. Source data remain external and are CC0 according to the Dryad API. The exact SCI baseline license applies to this package. External attribution is in a separate notice.

Job: sci-1107-dell-climate-pollution-biodiversity-d7bad673e654. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol. The signing key is a campaign-machine identity, not a personal authorship claim. No agents were launched.
