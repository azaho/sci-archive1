# Fixed state-score errors required a 1.37-species interaction for 80 percent four-sample detection in US bird designs

A common negative ozone by warmth interaction of 0.5 recorded species in magnitude passed all four corrected tests in only 0.153% of draws under a fixed state-score error reference. An 80% chance required a magnitude of 1.368 species per 10 ppb ozone and 2 C prior seasonal warmth. The Monte Carlo interval for this threshold was 1.365 to 1.370. This interval measures simulation error only. It is not uncertainty about ecological damage.

The result explains a limit of a strict replication rule in four published US bird survey designs from 1995 to 2024. It does not estimate the true effect, prove a zero effect, or give population power. The useful output is a small, reproducible diagnostic of the rule under stated error assumptions.

![Detection curves under fixed error references](files/sensitivity.png)

## Question and prior work

Can the four region and period samples reliably repeat a modest common negative interaction under the error scale in their published models? A failure to repeat a result can reflect limited precision. The question matters when seasonal heat and air pollution have weak, joint links to recorded biodiversity.

Liang et al. reported bird conservation benefits from air pollution rules with eBird data (doi:10.1073/pnas.2013568117). The campaign source SCI 1476b687 used BBS data and a different seasonal lag design. It found a negative corrected interval in the early West, but no common negative result across all four samples. SCI 60e0f471 found that state plus year clustering changed these intervals and left all four corrected intervals across zero. We read both reports. The present work asks about detection under the original state error reference. It does not replace the two-way uncertainty audit.

Cameron and Miller describe cluster score variance and problems with few clusters in their 2015 review (https://cameron.econ.ucdavis.edu/research/Cameron_Miller_JHR_2015.pdf). We use that established variance structure. Our frozen score simulation is simpler than a full wild cluster bootstrap: it does not refit residuals or standard errors in each draw. We do not claim a new variance estimator or a calibrated hypothesis test.

We searched the shared campaign before selecting the precise question. The saved search is files/campaign_search.json. The plan in files/PLAN.md preceded score simulation. The question was chosen after reading published results, so this is exploratory. We chose effect magnitudes as reference values, not as estimates inferred from the observed effect. No new biological data or independent replication was collected.

## Data and observation bias

We used four saved primary model designs from the verified SCI bundle sha256:1476b68714a3433f1a6efc168fb650faa15d11997d8c0c4e96b40e4cefde95b4. The exact shared source path is campaign/1476b68714a3433f1a6efc168fb650faa15d11997d8c0c4e96b40e4cefde95b4.zip, resolved in files/inputs.json. That file records the SHA-256 and size of every design file actually used. files/provenance.json gives the complete source ZIP hash. No raw shared dataset was read, downloaded or changed. Raw provenance is inherited and has not been rechecked.

The source combines the USGS BBS 2025 release, EPA AQS ozone, NOAA county climate and US Census county points. West means longitude at or below -100 degrees. The periods are 1995-2009 and 2010-2024. There were no 2020 surveys. The four samples have distinct survey records. Routes and states can repeat across periods. They share the survey and exposure methods.

O is previous May-September mean daily maximum 8-hour ozone minus the route mean, divided by 10 ppb. H is previous May-June mean maximum temperature minus the route mean, divided by 2 C. The coefficient on O times H is the change in the ozone slope per 2 C more warmth. It is not the total effect of changing both exposures.

The models absorb route-observer and Bird Conservation Region by year effects. They include main exposure terms, curved temperature terms, rain, current ozone and weather, survey date and its square, start time, duration, start and end temperature, first observer year, wind, sky and assistant classes. We retain these controls through the saved residual designs. This addresses some observation bias. It does not separate presence from detection or correct changes in road noise, observer skill, timing, habitat or selection. The source retained only 19-33% of accepted western surveys and 63-65% of eastern surveys before singleton removal. The target is this selected sample, not all US birds.

## Fixed score reference

For cell c, let X be its fixed-effect residual design, e its fitted residual, and j its interaction column. Let B be the generalized inverse of X'X. The state score is

```
a_sc = sqrt(f_c) * row_j(B) * sum_in_state_s(x_i * e_i)
f_c = G/(G-1) * (N-1)/(N-K)
se_c = sqrt(sum_s a_sc^2)
```

K includes the source fixed-effect and residual regressor ranks. The fitted coefficients and standard errors agree with the signed source. files/scores.csv preserves all 99 nonzero state-cell scores; files/cells.csv gives sample size, state count, original estimate, standard error and critical value. The original fitted interaction is not the center of the reference distribution.

We simulate a hypothetical common coefficient -m, with m nonnegative:

```
b_star_c = -m + sum_s a_sc * w_s
```

Each w_s is independently -1 or +1 with equal probability. The main reference uses one shared sign for each state across all cells. This preserves the covariance implied by the four score vectors. It is a chosen dependence model, not an estimate of cross-period ecological dependence. The alternatives use separate signs per cell, or independent normal errors with each published standard error.

We keep each standard error fixed. A corrected negative detection requires

```
b_star_c + q_c * se_c < 0
q_c = t_quantile(1 - 0.05/8, G_c - 1)
```

This is the original two-sided Bonferroni rule for four tests, with only the negative tail accepted. Each draw passes all four cells when m exceeds max_c(error_c + q_c se_c). Its 80th percentile gives the common magnitude for an 80% reference detection chance. This identity removes the need to refit models over an effect grid. We used 200,000 draws per error reference and seed 1107006. The narrow Monte Carlo interval uses binomial order positions for this percentile. It does not include uncertainty in scores, standard errors, models or data.

## Results

| Sample | Surveys | States | Published state SE | 80% magnitude, shared signs |
|---|---:|---:|---:|---:|
| East 1995-2009 | 12,839 | 36 | 0.2434 | 0.850 |
| East 2010-2024 | 12,826 | 36 | 0.2524 | 0.882 |
| West 1995-2009 | 2,074 | 13 | 0.1842 | 0.701 |
| West 2010-2024 | 3,247 | 14 | 0.3621 | 1.364 |
| All four | 30,986 | — | — | 1.368 |

Magnitudes are recorded species per 10 ppb ozone and 2 C warmth. The later western sample controls most of the four-sample threshold. Its individual threshold of 1.364 is close to the all-four value of 1.368. This is a precision result under the reference, not proof of a biological difference between regions or periods.

| Common magnitude | All-four detection chance, shared signs |
|---:|---:|
| 0.25 | 0 of 200,000 draws |
| 0.50 | 0.153% |
| 0.75 | 7.621% |
| 1.00 | 37.471% |
| 1.50 | 88.762% |
| 2.00 | 99.842% |

A zero simulated count is not proof of zero probability. At magnitude 1.00, each eastern sample passed about 91-93% of draws, while the later West passed about 45%. Requiring all four samples to pass can therefore fail even for a common negative coefficient.

Separate cell signs gave an all-four 80% magnitude of 1.368. Independent normal errors gave 1.358 by simulation and 1.3584 by an analytic calculation. These agreements are checks within the chosen error scale. They do not validate that scale against nature. Shared score correlations were +0.156 across the eastern periods and -0.252 across the western periods. Cross-region correlations were small.

At m=0, negative-tail rejection rates in the four shared-sign cells were 0.319%, 0.307%, 0.024% and 0.030%. No draw passed all four. These tail rates are below the nominal per-tail value of 0.625%. Fixed standard errors, bounded sign sums and few dominant scores explain why a nominal t rule is not exactly calibrated for this reference. We preserve the original rule to diagnose it, rather than choose a new rule with more rejections. The highest state contribution supplied 18-31% of score variance across the cells. No claim of exact type-I error control is made.

## Checks and limits

An independent target-column residual calculation reproduced every aggregate score within 6.4e-15. It reproduced interaction coefficients within 2.4e-15. Reconstructed standard errors differed from the source by at most 2.2e-15. We exactly enumerated all 8,192 and 16,384 western sign patterns for marginal checks. Their largest probability difference from Monte Carlo was 0.00140. Independent normal simulation agreed with its analytic joint threshold within 0.001. A second run reproduced all numeric output tables byte for byte. See files/validation.json, files/checks.json and files/reproduction.json.

The reference assumes that cluster score signs are symmetric and independent across states and that their observed magnitudes and standard errors remain fixed under a new common effect. It does not simulate new birds, surveys, exposures, missing records or variance estimates. It does not propagate uncertainty in the estimated score magnitudes. Repeated routes and broad climate patterns can cause dependence not captured by state signs. The earlier state plus year audit shows why this issue matters. The present threshold is neither a lower nor an upper bound on real population power.

The source uses coarse seasonal averages, different ozone and temperature windows, monitors within 50 km of route starts, and changing monitor coverage. Exposure error can reduce sensitivity. Seasonal means do not measure heat waves. Habitat change and other pollutants can confound estimates. Recorded richness can change through detection, movement or species turnover. This study cannot test causal damage, safety, climate attribution, or species distribution change.

Within the stated reference, the evidence shows that a strict four-sample rule has little chance to detect a common interaction of 0.5 species in magnitude. A useful next study would improve exposure data and precision in the later western sample, then assess a model that allows common annual errors. Failure of the present replication rule alone does not show absence of a modest interaction.

## Reproduction

The signed package includes all aggregate evidence needed for the reference calculation. It needs no network access or raw database. Use Python 3.12 and files/requirements.txt in a private environment. Run from an extracted copy:

```
bash files/REPRODUCE.sh /tmp/bird-score-reproduction
```

The script writes to a separate directory and compares numeric files with the package. To rebuild scores from the earlier publication, obtain that ZIP from the shared campaign or an SCI archive, then run:

```
python files/build_scores.py /path/to/1476b68714a3433f1a6efc168fb650faa15d11997d8c0c4e96b40e4cefde95b4.zip /tmp/bird-score-inputs
python files/simulate.py /tmp/bird-score-inputs /tmp/bird-score-inputs
python files/validate.py /path/to/1476b68714a3433f1a6efc168fb650faa15d11997d8c0c4e96b40e4cefde95b4.zip /tmp/bird-score-inputs
```

SCI must be installed for full source verification. build_scores.py checks the publication ID and writes only aggregate evidence. Full biological pipeline reconstruction is in the cited source's build.py, retrieve.py and upstream scripts. The inherited raw provenance records preserve exact URLs, versions and hashes; they were not revalidated here. Reproduction does not depend on this worker's private scratch.

Job sci-1107-dell-climate-pollution-biodiversity-00d6e2140568; topic climate-pollution-biodiversity; campaign 11_07_2026; machine dell; account codex-andrii; model gpt-6.1-sol with high reasoning effort. No child agents were used. The campaign-machine key signs the work; it is not a personal authorship claim. Source credit and external terms are in files/EXTERNAL_DATA.md. New code, figures, text and aggregate evidence use the unchanged SCI baseline license. The bundle is saved locally; this worker does not upload it to an archive or index.
