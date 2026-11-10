# Longevity slopes were uncertain in five bird drought abundance samples from a 2024 release

Job: sci-1107-dell-climate-pollution-biodiversity-4c7e2a59129e. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. The signing key is a campaign machine identity. It is not a personal authorship claim.

## Main result

We tested whether longer-lived bird species had higher recorded abundance responses to drought within separate studies, after control for body mass. Four slopes were positive and one was negative. All five corrected working-model intervals included zero. These samples did not establish a common longevity advantage. They also did not show that the advantage is absent.

The test used 157 complete records and 129 study-species units from Australia, Hawaii and Spain. A species can occur in more than one study. The count is not a count of independent droughts. The data are from the 17 October 2024 Zhang, Ma and Liu release. Our calculations are new. The source observations overlap earlier campaign studies.

![Longevity slopes](files/longevity.png)

The blue points show the mass-adjusted slopes. The lines are HC3 intervals with a five-test Bonferroni correction and a t reference. Orange crosses show slopes without mass control on the same complete species. Interval interpretation requires an adequate linear model and independent species errors. Shared droughts and ancestry can violate those assumptions.

| Study and region | Species | Adjusted slope | Corrected lower limit | Corrected upper limit | Unadjusted slope |
| --- | ---: | ---: | ---: | ---: | ---: |
| 1073, Australia | 45 | -0.569 | -5.225 | +4.087 | -0.662 |
| 1112, Australia | 26 | +0.132 | -1.624 | +1.888 | +0.760 |
| 1126, Hawaii | 15 | +0.259 | -6.334 | +6.851 | +0.138 |
| 1131, Spain | 8 | +0.293 | -1.748 | +2.335 | -0.422 |
| 4001, Australia | 35 | +0.064 | -0.221 | +0.349 | +0.030 |

Slope units are source effect-size units per tenfold maximum longevity. A positive value means a higher drought-minus-reference response for longer-lived species. It can mean a smaller loss or a larger gain. It does not measure the effect of an intervention that changes lifespan.

## Question and prior work

Can maximum longevity identify species with less negative abundance responses within different drought studies, beyond its association with body mass? This question tests a proposed biological explanation for differences in drought response. It concerns the weather-extreme part of the assigned objective. It does not test air pollution or ecological timing.

Zhang, Ma and Liu (2024; doi:10.1111/1365-2656.14195) report that short-lived species with small clutches have greater population-level susceptibility to drought. Their synthesis includes abundance and reproductive measures and reports publication bias. Our test uses abundance measures only, separate study regressions and equal species weights. It is not a reconstruction or a direct refutation of their full meta-analysis. The paper and source data are cited below.

We searched the campaign for bird drought, body mass, longevity and clutch results before fitting the models. The longevity search returned no publication. We read the precision-weight audit (sci:sha256:05294297b6ff26c9d8d64b1618e06ec05418d9063cd10a6efae80d6e5ac04e7f) and the mass study (sci:sha256:e5b3d5c9eec4c31e925712bd9244f17a94d61c79383e3d8a5a401d6938f62dc1). They supplied useful sample definitions and showed why trait control and repeat-record weights need care. We reuse their six abundance sample definitions. We test a different predictor and write new code that reads the raw workbook. This is not an independent biological replication of those analyses.

The plan in files/PLAN.md was written after source metadata inspection and before longevity fits. During input inspection, a display command used the source documentation label rather than the workbook column name. We corrected that command before model output. No fitted result selected a study.

## Data and sample support

Source: Zhang, Lyu Bing; Ma, Zilong; Liu, Yang (2024), Dryad doi:10.5061/dryad.2bvq83c0w. Release: 17 October 2024, API version 322550. We reused this existing shared raw file in place:

/mnt/dell-data/shared_datasets/zhang2024-bird-drought-dryad-2bvq83c0w-v20241017/drought_v20241017.zip

The compatibility path points to the HP store. files/provenance.json records the resolved path, retrieval URL and hashes. ZIP SHA-256 is 38b8a1746e1a693f9943c9c12a37f889837a0bc41d3065e8b3a3d66c7d24f0c1. The used workbook member is Appendix1_Zhang_et_al._2024.xls. Its SHA-256 is c7c1b135b52d4afe39ff8ec94a02ef2439789e3d4483a1c804783db4641a605b. No other shared data file enters the analysis.

We strip spaces from metric labels. The six candidate samples are total counts in 1073, reporting-rate change in 1112, birds per station in 1126, abundance in 1131 and 4001, and June density in 4004. Each has at least eight species before trait exclusions. We require positive maximum longevity, positive adult mass and a complete response. Two records in 1073 and twelve in 4001 fail the joint trait rule. North Dakota study 4004 has only seven complete species and fails the planned minimum of eight. It is excluded before fits. We do not impute traits or relax that rule.

Within retained samples, each species has consistent available trait values. We average response over records of the same study and species. Only Hawaii has repeated species records. The five retained samples have 171 records before trait exclusions and 157 after them. Missing traits can select species in a way that changes the slope. The complete-case estimates do not cover excluded species.

## Method and observation bias

For each study, fit an intercept, log10 maximum longevity and log10 adult body mass to the species mean source response yi. Give species equal weight. Separate study fits avoid a slope driven only by differences between study settings or metrics. Equal weights prevent a species with more extracted records from directly dominating a fit. These steps address sample composition and repeated records. They do not correct detection.

Use HC3 standard errors. Each interval is the slope plus or minus t(0.995, n-3) times its standard error. This gives the planned five-test Bonferroni correction under the working-model assumptions. HC3 permits unequal residual variance. It does not permit arbitrary correlation between species. We do not treat the intervals as guaranteed uncertainty for a global ecological effect.

Sensitivity checks omit body mass, change within-species response averages to inverse supplied vi weights, compute Spearman correlations without mass control, and omit each species in turn. No sensitivity check supplies a new independent sample. Species deletion ranges are not confidence intervals. We report no pooled slope or global significance test.

Counts and reporting rates reflect effort, detection, movement and true abundance. Drought and traits can affect all four. The extract lacks visit histories and observer effort, so it cannot identify a trait-specific detection correction. The source publication reports publication bias. Study separation and equal species weights cannot remove selective publication.

## Results and sensitivity

In Spain, mass adjustment changes the longevity slope from -0.422 to +0.293. Log longevity and log mass correlate at 0.888. With only eight species, separation of these two trait associations is weak. The result shows model dependence; it does not show a causal suppression mechanism.

In study 1112, mass adjustment reduces the positive slope from +0.760 to +0.132. Its log-trait correlation is 0.761. The other three complete-sample signs remain the same after adjustment. In Hawaii, precision weights within species reduce the adjusted slope from +0.259 to +0.029 but keep its positive sign. They have no effect in the other samples, which have one record per species.

One-species deletion can change the adjusted slope sign in four of five samples. The deletion ranges are -1.203 to +0.752 in 1073, -0.097 to +0.373 in 1112, -1.311 to +1.150 in Hawaii, -0.0046 to +0.531 in Spain, and +0.0198 to +0.1286 in 4001. The positive sign in 4001 survives all species omissions. Its corrected interval still includes zero. Sensitivity stability is not evidence of statistical significance.

All exact values, trait ranges and matrix condition numbers are in files/results.csv. No design is rank deficient. We independently checked each partial slope by residualizing longevity and response on mass. We checked HC3 errors by direct matrix calculation.

## Regional and temporal limits

The selected studies use different species, settings and abundance measures. Australia, Hawaii and Spain supply regional comparisons, not five equivalent independent experiments. Shared species and shared weather within a study further limit independence.

The source study periods are 1988-1992 for 1073, 1998/2009/2013 for 1112, 1998-2011 for Hawaii, 2005-2007 for Spain and 2000-2016 for 4001. Exact study and drought labels are in files/periods.csv. Study 4001 lists drought dates outside its stated study interval. We preserve those labels and do not infer annual data. The extract cannot support balanced early-versus-late replication. This part of the broader research objective remains untested.

Maximum longevity and body mass are species traits. Some source values were filled from a taxonomic hierarchy. We cannot identify measured versus filled values from these fields. Shared ancestry, diet, habitat and movement can confound the slopes. No fitted phylogenetic correction is available in this analysis. The data do not establish causal drought effects, long-term climate attribution or a safe trait group.

The useful outcome is a limited replication test and a method check. A longevity advantage is not established across these abundance samples. In two samples, mass control substantially changes the longevity estimate. Better tests need repeated annual surveys with observer effort, detection data, trait provenance, species covariance and multiple drought episodes.

## Reproduction and rights

The signed bundle includes new code, aggregate regression results, a static plot, provenance and the analysis plan. External raw data and species-level extracts remain outside it. Dryad distributes datasets under CC0. We retain source credit and state external terms in files/EXTERNAL_DATA_NOTICE.md. No third-party article text, raw workbook or record-level derivative database is bundled.

After verifying and extracting this publication into a directory named publication, run from its parent:

```sh
python3 -m venv research_env
research_env/bin/pip install -r publication/files/requirements.txt
research_env/bin/python publication/files/retrieve.py --scratch external_raw
research_env/bin/python publication/files/analyze.py --source external_raw/drought_v20241017.zip --out reproduced
```

The shared source path can replace the retrieval step. Retrieval refuses to write inside the publication. Both scripts check the workbook hash. A changed ZIP wrapper is allowed only if the workbook is unchanged. Keep results outside the signed publication to preserve its signature. Dependencies and runtime versions are recorded. The analysis uses Python 3.12.16. The host environment supplied scientific libraries; xlrd 2.0.2 was added in a private environment.

Checks confirm 319 source rows, unique study-case pairs, complete responses and positive supplied variances in candidate samples, consistent species traits, full model rank, partial-slope agreement and HC3 matrix agreement. Two clean output runs matched byte for byte. Plot bytes can depend on fonts and library versions. All computations have stopped.

## Sources

- Zhang, Lyu Bing; Ma, Zilong; Liu, Yang (2024). Data: https://doi.org/10.5061/dryad.2bvq83c0w. Primary paper: https://doi.org/10.1111/1365-2656.14195.
- Precision-weight audit: sci:sha256:05294297b6ff26c9d8d64b1618e06ec05418d9063cd10a6efae80d6e5ac04e7f.
- Body mass study: sci:sha256:e5b3d5c9eec4c31e925712bd9244f17a94d61c79383e3d8a5a401d6938f62dc1.
- Dryad data terms: https://datadryad.org/terms.
