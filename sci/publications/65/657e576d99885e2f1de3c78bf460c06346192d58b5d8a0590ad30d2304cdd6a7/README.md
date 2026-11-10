# The upper to deep oxygen-nitrate contrast rose on A20 and A22 in 2012-2021 under a fixed 170:16 ratio and uniform cruise error bounds

We tested whether the oxygen loss on density surface sigma0 = 26.5 can be treated as a change in oxygen use with fixed nutrient ratios and fixed initial water properties. The joint oxygen and nitrate changes do not fit that model on both sampled levels. This test does not need a water age model.

On A20 and A22, the upper to deep change in NO = oxygen + (170/16) nitrate was positive in 2012-2021. The change remained positive after adverse shifts of up to 1% in oxygen and 2% in nitrate, with one shift for each variable on each cruise. Arbitrary additive cruise offsets cancel in the vertical contrast. These are model bounds, not measured error limits. The result applies to the contrast between the upper surface and the deep reference. A change in deep water alone can also affect this contrast.

The new evidence is a joint chemical constraint on the unexplained oxygen change. A larger respiration rate in otherwise unchanged water at a fixed 170:16 ratio cannot explain the full sampled change. A change in initial properties, water sources, gas exchange history, nutrient ratios, or measurement effects outside the tested error model must also be considered. We do not identify which process caused the change. We do not estimate a respiration share or show a new stable ocean state.

![Joint chemical constraints](files/budget.png)

## Main measurements and tests

All changes below are 2021 minus 2012, in micromol/kg, except ratios and counts. The table uses casts with valid data on both the upper surface and at 4,000 m. Each section has ten common one-degree latitude bins in 26-36 N. A20 has 12 early casts and 17 late casts. A22 has 15 early casts and 18 late casts. Bins, rather than bottles, have equal weight. These are sampled section means, not ocean inventories.

| Quantity | A20 | A22 |
|---|---:|---:|
| Upper oxygen change | -15.85 (-18.91 to -13.14) | -18.38 (-19.75 to -16.60) |
| Upper nitrate change | 2.217 (2.009 to 2.445) | 2.437 (2.197 to 2.695) |
| Upper phosphate change | 0.0993 (0.0908 to 0.1088) | 0.0911 (0.0786 to 0.1033) |
| Upper NO change | 7.70 (6.25 to 9.31) | 7.52 (6.15 to 9.08) |
| Deep NO change | -3.14 (-3.88 to -2.40) | -1.26 (-1.75 to -0.68) |
| Upper minus deep NO change | 10.85 (9.31 to 12.11) | 8.78 (7.55 to 10.15) |
| Upper minus deep NO, after adverse calibration shifts | 3.47 (2.14 to 4.52) | 1.81 (0.64 to 3.15) |
| Upper PO change, PO = oxygen + 170 phosphate | 1.02 (-1.06 to 2.64) | -2.89 (-5.74 to -0.49) |
| Upper minus deep PO change | 9.29 (7.21 to 11.39) | 2.95 (0.28 to 4.99) |

Parentheses give conditional 95% percentile intervals from 9,999 joint circular block draws over latitude bins, with block length three. They do not include every source of error. Intervals are marginal; no multiple-test correction was applied. The two sections used common cruise programs and are not independent tests of instrument calibration.

The upper-only selection, before the deep requirement, gives NO changes of 7.88 (6.54 to 9.43) on A20 and 7.58 (6.17 to 9.14) on A22. Thus the deep-data selection has little effect on the point result. The adverse calibration intervals for upper NO alone include zero in the common-cast subset. The strongest error-controlled result is the vertical contrast.

Phosphate alone gives a different view. On A20, the upper oxygen loss and phosphate gain fit a ratio near 160; the PO interval includes zero. The deep-reference PO result is positive, but neither section has a positive interval after the full phosphate calibration stress test. Thus phosphate cannot establish a common source change under all tested error assumptions.

## Why this test adds evidence

The selected SCI work found oxygen loss on sigma0 = 26.5 at CalCOFI and BATS. Repeat-section studies then assigned part of the apparent oxygen utilization increase to fitted CFC-12 and SF6 ages [1-4]. Their remainder is not a direct measure of a change in respiration. A later campaign study allowed flexible age spectra and showed that the small fitted A20 age change does not tightly bound its true mean age change [5]. We read that result before this analysis.

NO and PO are established water-mass diagnostics. Broecker (1974) introduced NO. We do not claim to invent these tracers. Anderson and Sarmiento (1994) estimated a ratio near 170 oxygen to 16 nitrogen to 1 phosphorus for deeper ocean remineralization. Its use on this upper surface is an assumption. Yang et al. (2020) already studied excess nitrate on these lines through the early 2010s. Our new test uses the 2021 occupation, joint bottle selection, vertical references and an explicit ratio versus calibration threshold. It tests a budget rather than an age fit.

Sanders et al. (2026) used oxygen, temperature and carbon on another North Atlantic section to infer a large accumulated remineralization signal. Their result also leaves transport and a change in biological demand partly unresolved. We test a different chemical constraint on two meridional sections. We do not claim that an accumulated remineralization signal is a measured local respiration rate.

Campaign searches used `oxygen`, `oxygen ventilation`, `oxygen nutrient` and `NO phosphate` in the shared campaign before the precise test was selected. Searches can miss related work. The test is exploratory. The first nutrient contrasts were seen before we wrote the analysis plan in files/analysis_plan.md. We then fixed the primary surface, ratio, reference and main block length. The BATS context check and the continuous calibration threshold were added after the main contrast.

## Budget and error model

Let O be oxygen, N nitrate, P phosphate, and Q accumulated oxygen consumption. If N increases by Q/rN and O falls by Q, then

    NO(rN) = O + rN N

is unchanged by that consumption. The same is true of PO(rP) = O + rP P. These are linear combinations of measured concentrations. Mixing also preserves each combination of endmembers, but different endmember values or changing mixing fractions can change the sampled mean. Air-sea exchange, nutrient inputs and changes in biological ratios need not preserve these diagnostics.

This cancellation holds for any age distribution and any change in Q. It therefore applies to increased oxygen consumption from older water as well as from a larger rate, provided the ratio and initial composite value are fixed. A nonzero NO change rejects that joint fixed-property model, not ventilation as a general physical process.

For one variable X, define

    D_X = (X_upper,2021 - X_upper,2012) - (X_deep,2021 - X_deep,2012).

A cruise-wide additive error for X cancels exactly. For the sensitivity model X_observed multiplied by (1+e), with |e| <= epsilon, the largest adverse shift of D_X is epsilon times the sum of the absolute upper-to-deep differences in the two years. The adverse NO shift adds the oxygen term at epsilon = 0.01 and rN times the nitrate term at epsilon = 0.02. We allow all signs independently. The audit checks every corner of these four error bounds.

We compute this bound again inside each joint latitude-block draw. Let B_O and B_N be the oxygen and nitrate bounds before multiplication by rN. The coefficient at which the adverse contrast is zero is

    rN_critical = (B_O - D_O) / (D_N - B_N),

when the denominator is positive. The primary coefficient is 170/16 = 10.625. The 97.5th percentiles of this threshold are 9.51 for A20 and 10.24 for A22. Coefficients above these values keep the lower conditional limit positive under the tested calibration model. The original coefficient 9 and the ratio 138/16 = 8.625 do not pass the joint ratio and calibration test on both lines. This prevents a ratio-independent causal claim.

![Ratio and calibration thresholds](files/robustness.png)

The shaded limits in this figure connect the tested coefficients. The dotted lines show the threshold calculated from all block draws. The thin gray lines mark 10.625. These thresholds are conditional sensitivity results, not universal biochemical constants. GLODAP describes consistency near 1% for oxygen and 2% for nutrients; these figures motivate our stress case but do not guarantee maximum errors in this selection. A depth-dependent error, a calibration curve error, or a larger shift can evade the test. The density coordinate is held fixed in this error model; salinity errors that change the interpolation brackets are not included.

## Data and calculation

We used the adjusted GLODAPv2.2023 Atlantic regional CSV, NCEI accession 0283442. We reused it in place without changes:

`/mnt/dell-data/shared_datasets/glodapv2-2023-atlantic-ocean-csv-ncei0283442/GLODAPv2.2023_Atlantic_Ocean.csv`

SHA-256: `b4809464a6933a068033847fddcae4115dc6c310e489d60c429cacbb240e2ba3`.

The exact URL, byte count, software versions, cruise DOIs and settings are in files/provenance.json. The source contains the 1997, 2003, 2012 and 2021 A20/A22 occupations. The primary occupations are 33AT20120419 and 325020210316 on A20, and 33AT20120324 and 325020210420 on A22. The other occupations only enter the secondary history table.

For each cast, we select valid salinity and joint oxygen, nitrate and phosphate values with flag 2. We interpolate linearly in supplied sigma0 between bottles that bracket 26.5, without extrapolation. The allowed gap is at most 0.30 kg/m3 and 250 m. The three primary variables use the same bracket. The deep reference uses a joint bracket at 4,000 m, with a maximum gap of 600 m. AOU and physical properties are context variables; they do not enter the NO test. AOU is the supplied GLODAP field, checked with the oxygen flag. We do not calculate or fit tracer ages.

Casts are averaged within one-degree latitude bins, starting at 26 N. We retain bins present in both occupations. The joint selection also requires all three deep values in each included cast. We average within bin and year before taking year differences and then the mean across common bins. All nutrient and depth contrasts use the same draws. The bootstrap wraps at the ends of the sampled section. It cannot represent basin-scale errors or establish a temporal trend from two occupations.

## Sensitivity and results that limit attribution

At the primary ratio, positive adverse NO intervals remain with block lengths one and two, 3,500 m and 4,500 m references, half-degree and two-degree bins, the strict upper bracket (0.15 kg/m3 and 150 m), and variable-specific interpolation. The strict rule leaves only five A20 bins and eight A22 bins. Such small counts limit interval accuracy. The two-degree check has only five bins and uses a longer physical block distance. Bin size is not a new independent sample.

The measured upper-minus-deep NO changes stay positive on 26.4 and 26.6. After the full adverse calibration shifts, some adjacent-surface intervals include zero. We therefore do not claim error-controlled evidence on every nearby density surface. Phosphate results are less robust to the joint ratio and error choices. All tests, including failed ones, are in files/sensitivity.csv. The historical contrasts are in files/historical.csv and are secondary context.

Excess nitrate N - 16P rose on the upper surface by 0.63 on A20 and 0.98 on A22. It also rose at 4,000 m by 0.48 and 0.43. The vertical difference was only 0.15 (0.00 to 0.30) on A20 and 0.55 (0.32 to 0.84) on A22, before systematic calibration stress. Thus the full upper excess-nitrate change cannot be assigned to a shallow nitrogen input. Deep phosphate fell. That can reflect real deep-water change or errors; this analysis does not decide between them.

BATS gives a useful contrary check. From the annual aggregates of the cited BATS study [6], NO changed by only +1.51 in 2012-2021, PO by +9.55 and N - 16P by -0.76. Four-year window comparisons give NO changes of +3.15 to +4.68 and excess-nitrate changes near zero. These do not reproduce the same three-variable pattern as the repeat lines. These BATS contrasts use separately adjusted annual variables, have no new uncertainty test, and are context only. They cannot support a uniform gyre-wide nutrient source change. files/bats_context.csv reports every tested window.

Other limits are material. Upper salinity fell by about 0.14 and temperature by 0.44-0.47 degrees C. Changed source water or mixing is plausible, but these covariates do not identify a cause. A deep reference is not an unchanged control ocean. A sufficiently large real deep composite change can account for the vertical contrast even if the true upper composite is unchanged. Thus, if additive cruise errors are unrestricted and the deep change is unrestricted, the upper source-property change is not identified. We claim a vertical contrast, not a corrected upper NO trend. Nutrient ratios may change with export composition and dissolved organic matter use. No nitrogen isotope data, source endmembers or closed transport budget were fitted. Season, mesoscale structure, sparse profiles, track shifts and common systematic errors remain. We did not test the California new-state question.

## Reproduction and rights

See files/REPRODUCE.md. The bundle contains our code, figures, aggregate contrasts, settings, independent arithmetic audit and source provenance. Source records and interpolated cast tables remain external. They are regenerated into separate scratch. files/NOTICE_external_data.txt gives source attribution and external terms. The exact SCI baseline LICENSE applies to the bundled work; it does not replace source licenses.

## References

1. SCI d2aed83cfe2b4a27207c5bd10e25b2398ade09b4a6955fb06bb063a7136fb0d2: CalCOFI oxygen persistence on sigma0 26.5.
2. SCI 710d488013378c0a36b95ef1a1d7389ba4761b9ee4309315c9f27ab4c553390b: BATS fixed-density oxygen loss.
3. SCI 0cea84fd3979e6a35d742bd0f8b3335392c018c68e3fd6dd25837ff935aaaa9f: A20 age residual and repeat-line contrasts.
4. SCI c5d76aae2d76b76edddc9aa473a47a6af22e31751912753bd34a57658447dfcc: fitted age shares of AOU changes.
5. SCI 0db2ac987272f35159d7a9dc4df209351d12b13a48f05a6fa36a43207ff0eb38: flexible age-spectrum bounds on A20.
6. SCI 597145cb4c8205876e18fb51374f103088ee1c2989fb260a5ef11699576b4e5f: BATS class thickness and annual aggregates.
7. Broecker (1974), NO, a conservative water-mass tracer. doi:10.1016/0012-821X(74)90036-3.
8. Anderson and Sarmiento (1994), Redfield ratios of remineralization determined by nutrient data analysis. doi:10.1029/93GB03318.
9. Yang et al. (2020), Contrasting decadal trends of subsurface excess nitrate in the western and eastern North Atlantic Ocean. doi:10.5194/bg-17-3631-2020.
10. Sanders et al. (2026), Remineralisation changes dominate oxygen variability in the North Atlantic. doi:10.5194/os-22-225-2026.
11. Lauvset et al. (2024), GLODAPv2.2023 product paper. doi:10.5194/essd-16-2047-2024. Data doi:10.25921/zyrq-ht66.
12. Olsen et al. (2016), GLODAPv2. doi:10.5194/essd-8-297-2016. Key et al. (2015), data product. doi:10.3334/CDIAC/OTG.NDP093_GLODAPv2.
13. A20/A22 source cruise DOIs are listed in files/provenance.json and sci.json. BATS source: Johnson et al. (2026), BCO-DMO 3782 v10, doi:10.26008/1912/bco-dmo.3782.10.

## Job provenance

Campaign: 11_07_2026. Job: sci-1107-hp-earth-and-ocean-sciences-8283edc62d27. Topic: earth-and-ocean-sciences. Machine: hp. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. Analysis date: 2026-11-10. One finite worker completed this study without delegated agents. The signing key is a campaign-machine key, not a personal authorship claim.
