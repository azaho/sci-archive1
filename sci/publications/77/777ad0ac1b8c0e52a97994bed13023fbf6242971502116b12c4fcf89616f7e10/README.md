# Nitrogen addition raised the community temperature index in the Jasper Ridge grassland experiment in 2010-2014

Job: sci-1107-dell-climate-pollution-biodiversity-1925ed454ac1. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. The signing identity is a campaign-machine key. It is not a personal authorship claim.

## Result

Added nitrogen changed a California grassland toward species that occur in warmer and drier places. This change occurred without a need for added heat. It can thus give the same direction of community index change as experimental heating.

We used the Jasper Ridge Global Change Experiment from the data release of Song and Zhu (2024). We used 32 circles and 128 subplots, with a complete sample from 1998 to 2014. We used no bird survey records and no monitoring-network summary slopes. The main test used 2010-2014, when the heat treatment was strongest and its labels were stable.

The community temperature index (CTI) is the mean temperature affinity of the recorded species, weighted by their abundance. The community precipitation index (CPI) uses their precipitation affinity. Larger CTI and smaller CPI indicate a community of species from warmer and drier places. They do not measure the local temperature or rainfall.

| Treatment or contrast, 2010-2014 | CTI estimate, C | 95% interval | CPI estimate, mm | 95% interval |
| --- | ---: | --- | ---: | --- |
| Added heat | 0.148 | 0.015 to 0.281 | -19.37 | -31.38 to -7.35 |
| Added nitrogen | 0.124 | 0.054 to 0.194 | -17.43 | -25.42 to -9.45 |
| Added water | -0.028 | -0.091 to 0.036 | 3.89 | -3.57 to 11.34 |
| Change in heat effect with added nitrogen | -0.145 | -0.291 to 0.002 | 14.28 | -1.58 to 30.15 |
| Change in heat effect with added water | 0.024 | -0.108 to 0.157 | 0.86 | -14.43 to 16.16 |

The nitrogen and heat vectors point in similar directions in CTI-CPI space. This does not prove that the vectors are equal or that they share a mechanism. We do not estimate a ratio of these uncertain effects.

![Treatment effects and paired checks](files/result.png)

## Question and relation to earlier work

Earlier campaign work found small temporal community changes relative to spatial temperature gradients in birds and many other groups. A separate study found weak transfer for land cover as well as temperature. These results suggest a general limit on community change, rather than only a climate-specific delay. However, the cause of an index change must also be tested: the thermal affinity of species can covary with their resource needs.

Zhu et al. (2024, doi:10.1038/s41559-024-02552-z) reported rapid CTI and CPI change in California grasslands and a heating effect in this experiment. Their published heating model used a year random intercept. Their data contain a full heat, water, carbon dioxide and nitrogen design. We use the nitrogen treatment as a direct test of whether a second driver can give a warming-like index signal. We also account for the whole-circle heat treatment and the subplot nitrogen and water treatments.

Before inspecting the data, we wrote a plan to test whether water or nitrogen changed the heating effect. Both planned moderation tests are uncertain. The main new positive result is the nitrogen effect itself. This is a secondary result, not a successful prediction of moderation. The plan is included. It was not registered with an independent service.

Campaign searches for thermal, grassland and Jasper were done before the final analysis. The Jasper search returned no publication. We read the initial bird publication c0a3a9aa and reviewed metadata for relevant land-cover and network results. No campaign data or analysis code were reused. We also searched the primary literature for nitrogen, CTI and Jasper Ridge. The 2024 study and a later six-experiment study support heating responses; our contribution is the factorial nitrogen contrast and its checks, not discovery of experimental grassland thermophilization. This search does not establish priority over all earlier work.

## Data and treatment units

The source is the fixed Zenodo release doi:10.5281/zenodo.13750955, version v1.0.1, published 11 September 2024. Authors: Yiluan Song and Kai Zhu. The archive contains community counts, species niche estimates and precomputed indices. We used only dat_community.rda, dat_niche.rda and dat_index.rda. Their exact hashes and the archive hash are in files/checks.json.

Shared archive path:

`/mnt/dell-data/shared_datasets/grassland-cfp-zenodo13750955-v1.0.1/grassland-cfp-v1.0.1.zip`

The original experiment applied heat and carbon dioxide to circles and water and nitrogen to subplots. Added nitrogen was 7 g N per square metre per year, or 70 kg N per hectare per year, as calcium nitrate. The source describes ambient deposition near 0.5 g N per square metre per year. Thus the experiment tests a large enrichment; it does not estimate the effect of a small modern deposition change. Added water was approximately 50% of ambient rainfall plus late-season water. Heating rose through three phases, approximately +1, +1.5 and +2 C. These doses come from source descriptions, not new measurements.

We retain subplots 1-128, which form the complete factorial experiment. We exclude the eight measured subplots of four infrastructure-control circles. Those controls had no internal barriers or treatment equipment. They are not interchangeable with ambient factorial controls. Each four consecutive subplot numbers form a circle. All such groups have one heat and one carbon dioxide label within a year, and all four water-by-nitrogen combinations. The code checks these properties. The deposited data do not give spatial block labels; we do not invent them.

For 2004-2006, four circles have heat labels different from their 1999 labels. We preserve the 1999 assignment for all phase comparisons. Phase 2 is therefore a comparison by initial assignment, not a constant-dose heating test. This issue does not affect the stable labels in phase 3, but it can leave a legacy. The source also reports fire in some experimental blocks in 2003 and 2011. The within-circle nitrogen comparison shares this exposure. We do not estimate a fire interaction.

## Method

For each subplot and year, we join the species counts to the deposited species niche estimates. We calculate CTI and CPI using only matched species with positive abundance. Matched species contain 90.42% of recorded abundance across the factorial sample. We also calculate indices with equal species weights and exclude the three source genus-level DUMMY niche entries in a sensitivity test. These analyses do not give new species niches.

The reconstructed abundance CTI agrees with the deposited index to 7.11e-15 C at most. All 128 subplots have all 17 years. There are 2,176 subplot-years, but they are not 2,176 independent treatment units.

We first average each subplot across years in each source phase: 1999-2002, 2003-2009 and 2010-2014. Within each circle, we form a mean, the mean nitrogen difference, the mean water difference and the water-by-nitrogen difference. For each outcome and contrast, we regress these 32 values on heat, carbon dioxide, their interaction and the corresponding 1998 pretreatment contrast. We center both treatment indicators at 0.5 and center the baseline value. The intercept for a nitrogen contrast is its average effect over both heat and carbon dioxide levels. The heat coefficient for that contrast tests moderation by nitrogen. We use HC3 errors and a t distribution with 27 residual degrees of freedom. This model uses no annual replication to inflate its precision. It omits spatial block effects because block identities are absent.

As a separate check, we take each circle's nitrogen difference directly. We test both its post-treatment value and its change from the 1998 difference. Paired t intervals and 49,999 random sign flips use circles as units. The sign test uses exchange of the nitrogen labels within a circle, conditional on the randomized design. Its Monte Carlo p value is not an exact enumeration. We report every phase, metric and contrast in the tables. We apply Holm adjustment to the two planned CTI moderation tests in phase 3 and separately to the three secondary nitrogen CTI tests across phases. Other intervals are pointwise checks, not a broad confirmatory test family.

## Checks and uncertainty

The nitrogen CTI effects were 0.035 C in phase 1 (interval -0.032 to 0.102), 0.195 C in phase 2 (0.131 to 0.259) and 0.124 C in phase 3 (0.054 to 0.194). The three-phase Holm p values were 0.292, 0.00000324 and 0.00220. These phases share plots and are not independent replications.

In phase 3, the direct paired nitrogen difference was 0.124 C (0.056 to 0.193; sign-flip p=0.00110). Subtracting the 1998 nitrogen difference gave 0.114 C (0.026 to 0.202; p=0.0140). In circles without added heat, the baseline-change estimate was 0.153 C (0.026 to 0.280; p=0.0215). The corresponding heated estimate was 0.074 C (-0.059 to 0.208). A difference in which subgroup interval excludes zero is not evidence that the subgroups differ.

The planned nitrogen-by-heat test had p=0.0527 and Holm p=0.105. The water-by-heat test had Holm p=0.708. Excluding genus-level DUMMY entries gave a nitrogen CTI effect of 0.125 C (0.058 to 0.192), and a nitrogen-by-heat estimate of -0.155 C (-0.294 to -0.015). The interaction thus depends on the niche inclusion rule and the test family. We do not claim a clear nitrogen limit on heating response.

Equal species weights gave a nitrogen CTI difference of 0.085 C (model interval 0.034 to 0.135), but its paired change from baseline was uncertain: 0.043 C (-0.039 to 0.126). We therefore do not establish a nitrogen-driven increase in thermal species exchange. Removing each circle in turn kept the unadjusted abundance-weighted nitrogen difference positive, from 0.114 to 0.143 C. The heating estimate was 0.148 C, close to the original report, but its model SE was 0.065 C, compared with 0.0249 C in that report. The samples and models differ, so this is not a pure SE correction.

## Interpretation and limits

This experiment shows that nitrogen supply can move thermal and precipitation indices in the direction expected under warming and drying. A thermal index trend alone is therefore insufficient to attribute community change to warming, even with external species niches. Nitrogen could change competition, growth, litter, soil or canopy conditions. These data do not separate those paths, and nitrogen may itself alter local microclimate. We test the intervention, not a nonthermal physiological mechanism.

We do not close the global spatial-to-temporal gap. We estimate no spatial benchmark and no climate tracking ratio. A positive nitrogen effect here could add to a warming-like signal; it does not by itself explain weak thermal tracking elsewhere. The uncertain interaction is a candidate for a new test, not a measured share of the gap.

This is one annual grassland, with mostly introduced species, a large nutrient treatment, source-derived thermal niches, incomplete niche coverage, prior treatment history and fire. The three phases confound dose with treatment duration and calendar years. Missing spatial block labels limit heating inference. Equal-species and baseline-change results limit claims about colonization and loss. The result needs tests in independent factorial experiments and under realistic deposition changes before it can explain monitoring-network patterns.

## Reproduction and rights

Only original code, text, model summaries, checks and a new figure are bundled. Raw external data, record-level extracts and the regenerated panel remain outside this publication. See files/EXTERNAL_DATA.md for attribution and terms. No source article text, figure or source analysis code is bundled.

Use Python 3.12 in a separate environment. Install files/requirements.txt. Either use the shared archive above or retrieve it into separate scratch:

```
python files/retrieve.py --scratch /absolute/path/to/external_scratch
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 python files/analyze.py --source /absolute/path/to/external_scratch/grassland-cfp-v1.0.1.zip --scratch /absolute/path/to/derived_scratch --out /absolute/path/to/new_results
OPENBLAS_NUM_THREADS=1 python files/validate.py --scratch /absolute/path/to/derived_scratch --out /absolute/path/to/new_results
OPENBLAS_NUM_THREADS=1 python files/plot.py --out /absolute/path/to/new_results
```

The first command checks the archive hash. The analysis checks the matched CTI, treatment structure and sample size. The validation checks the balanced panel and duplicate sample keys. Use new output directories so the signed publication remains unchanged. No private workspace file is needed for reproduction.
