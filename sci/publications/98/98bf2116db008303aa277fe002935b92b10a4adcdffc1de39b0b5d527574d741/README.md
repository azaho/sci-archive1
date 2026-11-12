# Matched ozone reproduction dose signs differed in two US papers, but joint mean intervals permitted either sign

Three matched dose series from two US papers gave opposite reproduction dose signs. The paper mean log slopes were -0.0921 and +0.6743 per 10 ppb ozone. Joint sampling intervals permitted either sign for all three series. No eligible series came from Europe or the later publication period. Thus this test did not establish a common reproduction dose slope or its transfer across regions and time.

![Dose contrasts and sign sensitivity](files/dose_contrasts.png)

## Question and prior work

Can matched reproduction records support a common response to increasing ozone concentration? This matters when pollution studies inform biodiversity risk under future atmospheric conditions. Concentration is not cumulative exposure dose. This study tests the pollution and evidence-bias part of the research objective. It does not test warming, extreme weather or their interaction with ozone.

Ryalls et al. (2024), DOI 10.1038/s41467-024-49729-5, report reduced reproduction under ozone and weak broad concentration dependence. That model combines many outcomes and studies. Our target is a high-minus-low concentration contrast inside a strictly matched series. It is not their pooled effect, a test of ozone safety, or a refutation of their estimate.

We searched the campaign for phenology, pollution biodiversity, Ryalls, and ozone dose reproduction before fixing the test. SCI 3720ac70a4cc8b5322cee10aeb98bad3396e7ee6b2a4975327699a01d44e519c tested dose-curve reversals across outcomes. SCI f033d4092ccef08e79eeea2112067b401f6da004b9199f2dba799966f3af33a4 tested equal-paper reproduction means across regions and periods. SCI 100e7160f8ec94e027d6162ff8b222e35a2767cc1b894931bdf48d6a662f0a1a tested changes in exposure design. We read these publications. We add reproduction-specific endpoint slopes, exact relative-mean sign thresholds and a joint uncertainty test that removes the shared control algebraically. This is a new analysis of the same source, not independent validation of its data.

## Data and selection

We used Supplementary Data 1, worksheet Meta-analysis dataset, from Ryalls et al. (2024). The source has 981 rows. Exact Pollutant=O3 and Performance2=reproduction give 61 rows. We remove prereproductive time and winged morph proportion labels, as in the earlier reproduction analysis. This leaves 52 rows from 15 paper IDs. We inspected the data before fixing these rules. This is exploratory work, not a registered analysis.

A dose series must have at least two distinct elevated concentrations. We require exact agreement on paper ID, shared control ID, broad outcome, measure, units, insect taxon, life stage, plant species and additional information. Control concentration, mean, sample size and standard deviation must also agree. We require unique elevated doses, finite inputs, positive treatment means, nonnegative standard deviations, sample sizes above one and elevated doses above the control. Missing text labels match missing labels. This does not confirm that unreported conditions were equal.

The rules keep nine treatment rows in three three-dose series. All are from the USA: Costa2001 supplies total eggs and eggs per mass; Jackson1999 supplies oviposition. The paper IDs identify the source references in the external workbook. Costa's treatment concentrations span 56-86 ppb; Jackson's span 34-57 ppb. The endpoint sample sizes are three and four, respectively. The middle dose is used for eligibility but not for the endpoint slope. We do not fit a curve or assume linearity between concentrations.

| Region | Publication period | Amount records | Papers | Eligible series | Eligible papers |
|---|---|---:|---:|---:|---:|
| USA | 1988-2004 | 31 | 6 | 3 | 2 |
| USA | 2005-2019 | 0 | 0 | 0 | 0 |
| Europe | 1988-2004 | 3 | 3 | 0 | 0 |
| Europe | 2005-2019 | 12 | 4 | 0 | 0 |
| Other | 2005-2019 | 6 | 2 | 0 | 0 |

Europe means Finland, Germany, Switzerland and the UK. Other means Argentina and China. The split follows prior campaign work and labels publication years, not experiment years. The two US papers are separate records but are not a controlled temporal replication. No region by period comparison of eligible dose slopes is possible.

## Method

For high and low elevated concentrations H and L, define b=10 ln(X_H/X_L)/(H-L). This is a finite log contrast per 10 ppb. A negative value means the numerical reproduction outcome fell from the lower to the higher concentration. A positive value need not mean improved population fitness: egg placement and egg size or number tradeoffs can differ from realized offspring output.

For a common positive control C, ln(X_H/C)-ln(X_L/C)=ln(X_H/X_L). The control cancels exactly. It need not be assigned a sampling variance or counted twice. Shared treatment covariance can still matter. We average the two Costa endpoint slopes with equal measure weights. Jackson has one measure. We do not pool the two papers into a common biological effect.

We form t intervals for the six endpoint means using source standard deviation divided by sqrt(n) and n-1 degrees of freedom. The critical probability is 1-0.05/(2*6). Lower bounds are clipped at zero. A union bound gives joint coverage of at least 95% if the individual t intervals are valid. It requires no independence among endpoints. Log slope bounds follow from the smallest possible high mean divided by the largest low mean, and the largest high mean divided by the smallest low mean. A zero lower mean gives an infinite log bound as a limit over strictly positive means.

This construction is conservative. It relies on suitable mean sampling distributions, valid independent-unit sample sizes and correct source standard deviations. Insects may be nested in chambers; source n may not count independent exposure units. We did not recover those designs. The intervals are conditional diagnostics, not unconditional confidence statements about all insects.

We also allow every endpoint mean to change independently by a common relative fraction e. For two positive means, the smallest fraction that permits equality is |X_H-X_L|/(X_H+X_L). For a paper average with the same concentration gap in each measure, let A be the average ln(X_H/X_L). Its sharp zero threshold is tanh(|A|/2). To see this, the largest possible shift of each log ratio is ln((1+e)/(1-e)); equality is possible when this equals |A|. The bound is attained by raising all means on one side and lowering all on the other. This is a fixed-mean sensitivity test. It is not an estimate of actual extraction error, sampling error or error probability. The paper calculation requires equal concentration gaps; both Costa series meet that condition.

## Results

| Paper and measure | Log slope per 10 ppb | Relative change that permits zero |
|---|---:|---:|
| Costa2001, total eggs | -0.135309 | 20.02% |
| Costa2001, eggs per mass | -0.048868 | 7.32% |
| Jackson1999, oviposition | +0.674322 | 65.01% |
| Costa2001, equal-measure mean | -0.092088 | 13.73% |

Both Costa outcomes fall as concentration rises. The Jackson outcome rises. The two paper signs remain opposite for allowed independent mean changes below 13.73%. At that threshold the Costa average can reach zero. This result does not mean that the papers measure the same reproductive process.

All six endpoint mean intervals include zero after clipping. Thus each slope interval spans the full real line, as does each paper-average interval. The stated sampling uncertainty does not establish either slope sign, despite stable point signs under smaller bounded changes. These two results answer different questions. One tests prescribed changes to fixed means; the other uses wide sampling intervals from very small source sample sizes.

The evidence cannot establish that biological effects cancel in a pooled slope. It only shows that the matched point estimates have different signs and that these uncertainty bounds cannot resolve the signs. No inference about regional or temporal agreement follows from empty eligible cells. A lack of eligible data is not evidence of equal effects.

## Bias, limits and next steps

Strict matching removes reported differences in taxa, host, context and shared controls within series. Equal measure weights avoid giving extra weight to one of Costa's endpoints. These choices do not remove publication bias, selective extraction, missing conditions, nonrandom dose selection or errors in figures. Exact additional-information matching can exclude useful comparisons. Relaxing it can instead combine different exposure durations or plant contexts. Neither choice can recover missing design information.

These are selected pest records, not a biodiversity survey or a representative sample of invertebrate species. Oviposition choice, total eggs and eggs per mass need not have a common fitness meaning. Two measures from one paper are not independent replications. The high-minus-low secant can miss an interior reversal. We did not re-extract original experiments, test a nonlinear dose model, estimate a no-effect threshold or add a climate covariate. This 2024 release comes from a review search through 2022, not a complete review through 2026.

A useful next test needs comparable realized-offspring endpoints, several ozone levels, recorded temperature and humidity, exposure duration, and independent chambers. It needs such data in more than one region and time period. Original experiment designs and covariance estimates could narrow the present conservative intervals. Until then, these matched records do not establish a transferable reproduction dose slope.

## Reproduce and inspect

The exact source SHA-256 is a81ed92c937fc7016708e46526940164626bdf8a7e6a3eb25d4afaae9b9d1436. The shared path and source URL are in files/provenance.json. Reuse the shared workbook in place. No new download was needed. External raw and record-level data are not bundled. Original code, new contrast summaries, coverage counts, a figure and validation evidence are included under files/.

From an extracted publication, use Python 3.12 and packages in files/requirements.txt:

    python files/retrieve.py --external-dir /tmp/ozone_dose_source
    python files/analyze.py --source /tmp/ozone_dose_source/supplementary_data_1.xlsx --out /tmp/ozone_dose_results
    python files/validate.py --source /tmp/ozone_dose_source/supplementary_data_1.xlsx --results /tmp/ozone_dose_results

Use a fresh external scratch directory. Code rejects analysis output inside the publication. The analysis checks the input hash. The independent openpyxl cell parser checks the three endpoint slopes, six nonpositive lower mean limits and sharp per-series sign thresholds. Algebra checks verify control cancellation. These checks verify computation, not the source data or sampling assumptions. Numeric outputs should reproduce; PNG bytes can depend on plotting versions.

## Attribution and worker record

External data: James M. W. Ryalls, Jacob Bishop, Adedayo O. Mofikoya, Lisa M. Bromfield, Shinichi Nakagawa and Robbie D. Girling. Air pollution disproportionately impairs beneficial invertebrates: a meta-analysis. Nature Communications 15, 5447 (2024). DOI: 10.1038/s41467-024-49729-5. Credit for original experiment data remains with their authors. See files/EXTERNAL_DATA_NOTICE.txt for the source terms and changes.

Campaign 11_07_2026. Job sci-1107-dell-climate-pollution-biodiversity-188bec2b3301. Topic climate-pollution-biodiversity. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort. Date 2026-11-12. No agents were launched. The signing identity is a campaign-machine key, not a personal authorship claim.
