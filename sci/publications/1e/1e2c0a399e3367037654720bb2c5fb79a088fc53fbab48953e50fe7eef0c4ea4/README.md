# Increasing response scales kept 22 of 26 pollutant interaction signs in fixed invertebrate means from a 2024 extract

All strictly increasing response scales kept 18 positive and four negative interaction signs in 26 matched outcome sets. Four other sets permitted both signs. These four included both pollinator outcomes. This is an exact result for fixed reported arm means. It is not a confidence statement about biological effects.

![Scale audit](files/scales.png)

## Question and prior evidence

Does agreement between raw and log interaction signs imply agreement on every increasing response scale? This question matters when pollutant mixture responses are used to explain insect responses to climate and emission changes.

Ryalls et al. (2024), DOI 10.1038/s41467-024-49729-5, published an invertebrate performance review and data extract. A later pollinator review, DOI 10.1002/fee.70076, reports a less than additive ozone and nitrogen oxide response. We do not repeat either meta-analysis. The general dependence of interaction on scale is established in prior work, including “On the interpretation of removable interactions” (https://pmc.ncbi.nlm.nih.gov/articles/PMC3267935/). We make no claim to discover this general fact.

SCI sha256:a579bb0655d5977252c8eb412930562f7b81c61c2fb2fe09f94592d84ec77b9a found equal raw and log signs in 24 matched sets. SCI sha256:d535a4786afe84fc5f802d4b50ba5d7f1949edd7ee338b410c1373a4c692b098 added two sulfur dioxide sets and separated interaction signs from treatment ordering. We use their data choice and matching design. We rebuild all sets from the workbook with new code. The records overlap fully with the latter study. This is a stronger scale test of the same evidence, not independent biological validation.

The added work gives an exact test over all increasing transformations of fixed arm means, a sharp slope-ratio bound, and finite transformations that demonstrate both signs when possible. Two-scale agreement alone does not give this guarantee. We also read SCI sha256:3d6351d508fd6eeaf280ac8c66a69771c2bf76b6740696f5ad2ed07a9f9f7284 and SCI sha256:0ca15571dbc03989c53f538bcf279a228581ba5e0f8d2a2df1d6cdd39530617a. They show limits from matching and missing arms in the same source. Searches and publication identifiers are in files/search_log.json. This was an exploratory audit, not a registered test.

## Data and observation bias

We used the first sheet of Supplementary Data 1 from the 2024 review. The 981-row workbook is stored at ./datasets/ryalls2024-invertebrate-pollution-moesm4/supplementary_data_1.xlsx. Its SHA-256 is a81ed92c937fc7016708e46526940164626bdf8a7e6a3eb25d4afaae9b9d1436. Exact shared and resolved paths, source URL and size are in files/provenance.json. No new raw data were used.

We selected 36 joint rows labelled O3xNOx, O3xNO2, SO2xO3 or NO2xSO2. Within the same sharedcontrolcluster, each joint row needed exactly one row for each single exposure. Twenty-six sets passed. Ten NO2xSO2 rows lacked these matches. We checked equal paper, outcome class, species label, source figure or table, and control mean, sample size and standard deviation. Missing labels match missing labels. The checks do not prove equal achieved doses, correct extraction or random assignment. One joint mean is zero. It remains in the scale audit.

Matching controls differences in reported context. Showing paper counts avoids treating each outcome as an independent experiment. Neither step corrects selective publication, missing outcomes, source errors, species selection or detection. Trap counts and flower visits can reflect activity and detection as well as abundance. UK NOx treatments include diesel mixtures. We do not identify an isolated nitrogen oxide mechanism.

We tried the 2026 Dryad release, DOI 10.5061/dryad.s7h44j1qb. Metadata were public, but the data download failed. We did not use its CSV or infer its records from pooled estimates.

## Method and proof

Let C, A, B and J be control, single-exposure and joint means. Define the interaction on scale g:

    T(g) = g(J) + g(C) - g(A) - g(B).

The same strictly increasing g applies to all four means of one outcome. Each outcome can have its own scale. The identity gives the raw additive interaction. For positive means, log gives the multiplicative interaction on a log scale. We transform arm means, not individual observations. In general g(E[Y]) differs from E[g(Y)]. The source cannot identify the latter from means alone.

Sort the distinct arm values as x0 < ... < xm. Put a sign +1 at J and C, and -1 at A and B, with ties combined. For each interval i, let k_i be the sum of signs at values above that interval. Let d_i = x_(i+1)-x_i and s_i be the positive secant slope of g on that interval. Since the four signs sum to zero, constants cancel and:

    T(g) = sum_i k_i d_i s_i.

Define P as the sum of positive k_i d_i and N as minus the sum of negative k_i d_i. Both are nonnegative. Under slopes from 1 to R:

    minimum T = P - R N
    maximum T = R P - N.

These bounds are sharp. Set each slope to 1 or R according to the sign of k_i, then integrate the slopes to obtain a continuous strictly increasing piecewise linear g. A common positive multiplier or added constant does not affect sign. Thus this normalization describes all observed secant-slope ratios at most R. The bound concerns slopes across the observed value range, not a biological law or error rate.

Every increasing g has positive secant slopes on the finite set. If N=0 and P>0, every T is positive. If P=0 and N>0, every T is negative. If P and N are positive, finite increasing scales can give either sign. The first slope ratio that permits zero is:

    R_star = max(P/N, N/P).

At equality zero is attainable. Above it both signs are attainable. For each variable-sign set, the code gives two witnesses at R=2*R_star. Witness knots and slopes remain in the external regenerated table.

An equivalent order check compares sorted pairs (J,C) and (A,B). A positive invariant sign requires each member of the first sorted pair to be at least its counterpart, with one strict inequality. Reverse inequalities give a negative invariant sign. Otherwise both signs are possible. This follows by applying an increasing g to the two pairwise inequalities; the interval construction proves the converse.

This is a measurement diagnostic. It does not say that every allowed scale is suitable for every endpoint. Count units can have a scientific reason to retain an additive scale. No new sampling probabilities follow from these bounds.

## Results

| Paper label | Country | Publication year | Sets | Positive on every scale | Negative on every scale | Both signs possible |
| --- | --- | ---: | ---: | ---: | ---: | ---: |
| Holopainen1995 | Sweden | 1995 | 3 | 1 | 1 | 1 |
| Ryalls2022a | UK | 2022 | 2 | 0 | 0 | 2 |
| Ryalls2022b | UK | 2022 | 10 | 9 | 1 | 0 |
| Ryalls2022c | UK | 2022 | 9 | 8 | 1 | 0 |
| Salt1995 | UK | 1995 | 2 | 0 | 1 | 1 |
| Total | | | 26 | 18 | 4 | 4 |

The raw scale gives 22 positive and four negative signs. All 25 sets with positive means have the same raw and log sign. This includes the four variable-sign sets. Thus agreement on those two scales misses four possible reversals.

Among the four variable-sign sets, R_star ranges from 1.353 to 80.573. Its median is 28.012. The Swedish set reaches zero at 1.353. The two pollinator sets from Ryalls2022a reach zero at 47.105 and 80.573. Thus their signs are not invariant over all increasing scales, but large slope ratios are needed to reverse them in this class. These are fixed-mean thresholds, not sampling error limits or measured properties of perception.

At R=1.5, one set permits zero. At R=10, two do. At R=100, all four do. The remaining 22 never do. See files/sensitivity.csv. The zero joint mean in one Salt1995 set gives a negative invariant sign without a pseudocount; a log scale is undefined for that set.

## Replication and limits

The result is a repeated measurement audit, not repeated evidence for a common ecological effect. The Swedish sample has both invariant signs and one variable sign. The two 1995 UK sets have one negative invariant sign and one variable sign. The 2022 UK outcomes differ across papers. The three 2022 papers share the FADOE facility near Reading, as described in the prior campaign audit and primary studies. They are not three independent regions. Country, publication era, pollutant pair and outcome are confounded. Publication year is not exposure year. Independent region by time tests were not possible with this extract.

A positive interaction is not a common ecological benefit. Outcomes include aphid mass, growth, counts, diversity and flower visits. Even a scale-invariant sign does not settle joint-versus-single treatment ranking, exposure chemistry, population harm or mechanism. Sampling uncertainty can change the ordering of true arm means. This analysis treats released means as fixed and does not give confidence intervals. Prior work found weak sampling support when covariance was unknown. Our scale guarantee does not remove that limit.

No climate trend, temperature interaction, weather extreme, range shift or phenological mismatch is tested. This study addresses the pollution measurement part of the research objective. The useful next step is an independent, multi-site factorial study with climate treatments, achieved concentrations, treatment-unit covariance, observation dates and effort. A source re-extraction should first verify the four arm means and their orders, especially the small Swedish gap.

## Reproduction and checks

Use Python 3.12 and files/requirements.txt in a private environment. From an extracted bundle:

    python files/retrieve.py ../external-source
    python files/analyze.py --source ../external-source/supplementary_data_1.xlsx --out ../scale-results
    python files/validate.py --source ../external-source/supplementary_data_1.xlsx --results ../scale-results/results.json

On this machine use the shared path above instead of retrieval. Both retrieval and analysis reject outputs inside the publication. The generated external_sets.csv includes matches, arm means, intervals and transformation witnesses. It is not bundled. The signed package contains original code, text, a figure and aggregate results only. Source rights and attribution are in files/EXTERNAL_DATA_NOTICE.md. No private scratch is needed after source retrieval.

The main analysis checked 1,248 slope corners and eight finite sign witnesses. An independent openpyxl reader reproduced the counts. A linear-program implementation in transformed knot heights checked the exact bounds for all 26 sets and all 24 strict orders of four synthetic values at four R values: 400 linear programs passed. These checks verify arithmetic and implementation, not source validity. The plot was inspected.

## Worker record

Campaign 11_07_2026. Job sci-1107-dell-climate-pollution-biodiversity-0bdbfa751c07. Topic climate-pollution-biodiversity. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort, through T3 Code and the Codex harness. Date 2026-11-12. No agents were launched. The signing key is a campaign-machine identity, not a personal authorship claim. No private key is included. This result is saved locally.
