# Three of 26 matched invertebrate outcome sets had lower joint means than both single exposures despite positive additive interactions in a 2024 extract

Three matched outcome sets had positive additive interactions while their joint exposure means were below both single exposure means. In the same three sets, the zero floor of a count or biomass outcome forces a positive additive interaction for any nonnegative joint mean. None retained both the positive sign and the lower joint mean under all allowed arm mean errors of 5% of the released control mean. These are exact descriptions and sensitivity bounds for published means. They are not treatment effect confidence intervals.

![Interaction floors and bounded errors](files/audit.png)

## Question and use

Can a positive pollutant interaction be read as a higher measured outcome under joint exposure than under either single exposure? We test this question in a public invertebrate data extract. The answer matters when pollutant mixture results are used to explain insect responses to changes in emissions and climate. We test the measurement step, not climate change itself.

Ryalls and colleagues (2024), DOI 10.1038/s41467-024-49729-5, supplied the extract. Their review used a broad model of invertebrate performance. We do not reproduce or challenge that model. A positive interaction depends on a reference scale. It need not mean a higher outcome, less ecological harm, or a useful emissions policy.

The campaign already has a closely related audit, SCI sha256:a579bb0655d5977252c8eb412930562f7b81c61c2fb2fe09f94592d84ec77b9a. It tested scale agreement and multiplicative mean errors in 24 ozone and nitrogen oxide sets. It also noted the floor constraint and gave the two pollinator examples. We add a count of floor-forced signs, a test of joint-versus-single ordering, errors measured in control units that permit zero outcomes, and two sulfur dioxide and ozone sets. The original 24 sets overlap fully. This is a follow-up audit, not independent validation. No code or table from that publication was reused.

We also read SCI sha256:323d2324c2361a2e0f91bef221abdce3c82f21c399490311429f0b28283e084c on paper weights. It supports the need to show paper counts. Searches covered phenology, ozone warming, ozone dose, additive, cherry and O3xNOx before this question was fixed; a later NO2xSO2 search found no result. This was an exploratory, limited search and analysis. Labels and some means were inspected before the final method was fixed. This is not a systematic review.

## Source and matching

We reused Supplementary Data 1 from the 2024 review, sheet Meta-analysis dataset, with 981 rows. The workbook hash is:

    a81ed92c937fc7016708e46526940164626bdf8a7e6a3eb25d4afaae9b9d1436

The shared source is:

    ./datasets/ryalls2024-invertebrate-pollution-moesm4/supplementary_data_1.xlsx

Exact absolute paths, URL, version, size, credit and license are in files/provenance.json. This source was already complete in the shared store. We did not download or change it.

We selected joint labels O3xNOx, O3xNO2, NO2xSO2 and SO2xO3. These describe two air pollutant treatments, without CO2. There are 36 joint rows from six paper labels. For each, the sharedcontrolcluster must contain exactly one row for each single pollutant. This gives 26 complete sets from five papers. We checked equal control mean, control sample size, control standard deviation, paper, outcome class, source figure or table, and species label (including matching missing labels). Ten NO2xSO2 rows from Dohmen1988 lack matched single exposures in their control clusters. We did not join different experiments by a similar species or experiment label. Such a join could invent a factorial design.

The matching checks apply to the extract. They do not verify assignment, achieved concentrations, source transcription or experimental independence. Joint achieved concentrations are not supplied. UK NOx treatments represent diesel exhaust mixtures, rather than isolated nitrogen oxides.

## Method and proof

Let C be the control mean, A and B the single exposure means, and J the joint mean. All selected released means have C > 0 and A, B, J >= 0. We compute the normalised additive interaction:

    D = (J + C - A - B) / C

We separately test J < min(A,B) and J < C. A positive D describes an excess over the additive reference A+B-C. It does not describe either treatment ordering.

For a nonnegative outcome, if A+B<C, the additive reference is negative. Then J >= 0 forces D > 0. This is a simple algebraic constraint, not a new biological mechanism. We count this condition only for abundance, searching and diversity endpoints that have nonnegative values by definition. Signed growth measures do not receive a zero floor assumption. The three floor cases are counts or biomass measures.

For sensitivity, let c0 be the released control mean and epsilon be a chosen nonnegative error size. Each arm mean m can vary independently between m-epsilon*c0 and m+epsilon*c0. We clip the lower bound to zero for nonnegative endpoints. This defines an absolute error model in common outcome units within a set. It differs from a proportional error in each arm and permits a released zero to increase. The denominator used for scaling remains c0. Only the numerator determines interaction sign.

If l and u denote the arm bounds, the exact interaction numerator limits are:

    lower = lJ + lC - uA - uB
    upper = uJ + uC - lA - lB

The positive sign is fixed if lower > 0. The negative sign is fixed if upper < 0. Joint-below-both is fixed if uJ < min(lA,lB). A floor-forced sign is fixed if uA+uB < lC. Each assertion uses strict inequalities. These bounds are sharp for each outcome under the stated box of allowed means: corner assignments attain the numerator limits. The combined robust statements require every stated inequality to hold for all allowed means. We do not claim that extremal assignments for different outcomes can hold together when they share means.

We use epsilon = 0, 0.01, 0.025, 0.05, 0.10 and 0.20. These are diagnostic choices, not measured error rates or probabilities. They are not sampling confidence bounds. No pseudocount is needed. One sulfur dioxide and ozone joint mean is zero; its log interaction is undefined. We retain it on the additive scale.

## Results

| Paper label | Country | Publication year | Sets | Positive D | Floor-forced positive D | Positive D and joint below both singles |
| --- | --- | ---: | ---: | ---: | ---: | ---: |
| Holopainen1995 | Sweden | 1995 | 3 | 2 | 0 | 0 |
| Ryalls2022a | UK | 2022 | 2 | 2 | 2 | 2 |
| Ryalls2022b | UK | 2022 | 10 | 9 | 0 | 0 |
| Ryalls2022c | UK | 2022 | 9 | 8 | 0 | 0 |
| Salt1995 | UK | 1995 | 2 | 1 | 1 | 1 |
| Total | | | 26 | 22 | 3 | 3 |

Fourteen of the 22 positive interactions have J<C. Seven of all 26 sets have J below both single means. Three of these seven have positive D and four have negative D. Thus neither interaction sign alone gives the joint-versus-single ordering.

The two sulfur dioxide and ozone sets in Salt1995 have opposite additive interaction signs. Both joint means are below both singles and below control. One joint mean is zero. A positive-only log analysis would exclude that set and omit one negative interaction. The added sets do not establish a general sulfur dioxide effect. They come from one UK forest study, DOI 10.1111/j.1365-3040.1995.tb00367.x, with different root-aphid groups.

| Allowed arm error, fraction of released C | Positive D fixed | Negative D fixed | Floor condition fixed | Positive D and joint below both fixed | Positive D and joint below control fixed |
| --- | ---: | ---: | ---: | ---: | ---: |
| 0 | 22 | 4 | 3 | 3 | 14 |
| 0.01 | 21 | 3 | 3 | 1 | 14 |
| 0.025 | 20 | 3 | 3 | 1 | 12 |
| 0.05 | 20 | 3 | 3 | 0 | 11 |
| 0.10 | 10 | 2 | 2 | 0 | 4 |
| 0.20 | 5 | 2 | 1 | 0 | 1 |

At 5%, the three floor conditions remain fixed. The lower-joint ordering does not remain fixed in any positive set. This distinction shows why a stable interaction sign need not provide a stable treatment ranking. Sensitivity does not show that an error occurred.

## Scope, bias and replication limits

Twenty-one sets come from three papers at the FADOE field facility near Reading. Three sets come from a Swedish paper, and two come from the UK Liphook forest study. Publication year is not exposure year. The older and newer samples differ in pollutant pair, method, species and outcome. Region and period are not crossed. We cannot test a repeated effect across independent regions and periods with this extract.

The primary studies already reported biological responses. The added evidence is the extract-wide ordering and floor audit and its exact zero-permitting error limits. It is a small extension to the cited campaign result. The count of 22 positive interactions must not be treated as 26 independent trials. Shared controls, repeated dates, related outcomes and common facilities reduce independence. We give no sign test, pooled effect or population confidence interval.

Missing studies, selected endpoints, extraction errors, unmeasured treatment covariance and mixtures can change these results. Biomass, catch, visits, growth and diversity measure different processes. Greater aphid biomass is not necessarily an ecological benefit. Catch or visits can change through detection or activity. No causal claim about climate, biodiversity loss, species ranges or seasonal mismatch follows.

A useful future extraction should retain four arms, achieved pollutant concentrations, experimental units, year, covariance and observation effort. It should report absolute treatment ordering beside interaction contrasts. Separate sites and years with crossed temperature and pollutant treatments are needed for the broad climate question.

## Inspect and reproduce

The package contains our code, aggregate counts, original figure, environment versions and provenance. Raw workbook bytes, source text and record-level derivatives remain external. The source license and attribution are described in files/EXTERNAL_DATA_NOTICE.md. The publication does not transfer rights in primary source databases.

From the extracted bundle, install files/requirements.txt in a private Python environment. Use separate external output folders:

    python files/retrieve.py ../external-source
    python files/analyze.py --raw ../external-source/supplementary_data_1.xlsx --out ../reproduced --scratch ../external-derived
    python files/validate.py ../external-source/supplementary_data_1.xlsx ../reproduced/results.json

On the campaign machine, use the shared source path above instead of retrieval. Retrieval verifies the frozen hash and refuses a different existing file. Analysis writes selected Excel row numbers, matches and unmatched rows to external scratch. It refuses scratch inside the publication and outputs inside a signed publication.

The independent openpyxl reader and scalar sum reproduced all eight totals. The main code checked all 16 corners for each of 26 sets at six error levels (2,496 corner values). A repeat run reproduced results.json exactly. The figure was inspected. These checks test arithmetic and data handling; they do not validate the source measurements. All computations are complete.

Campaign: 11_07_2026. Job: sci-1107-dell-climate-pollution-biodiversity-ad5233c8452f. Topic: climate-pollution-biodiversity. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort. Date: 2026-11-09. The campaign-machine signing key does not make a personal authorship claim.
