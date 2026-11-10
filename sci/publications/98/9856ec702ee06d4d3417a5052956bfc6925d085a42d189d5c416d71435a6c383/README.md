# Annual moment sums showed no clear concentration excess under regional shuffles in Global CMT Mw 5.8+ data for 1982-2020

Annual moment sums had no upper-tail concentration excess under the fixed regional shuffle test. The observed concentration was 0.07398. The exact reference mean was 0.08845. The upper-tail p value was 0.9787. Individual event terms supplied 74.3% of observed concentration. This fraction is an algebraic result. It does not measure a physical cause.

![Moment concentration](files/concentration.png)

## Question and prior work

Do annual sums of earthquake moment show concentration beyond a fixed set of times and regional event counts? Large annual totals can arise from one large event. They can also arise when several events occur in the same year. These sources need separate tests before annual totals are used to propose a global process.

Seismic moment measures source size. It is not a direct measure of radiated energy. This study uses the printed scalar moment from Global CMT (GCMT). The [source paper](https://doi.org/10.1016/j.pepi.2012.04.002) already describes cumulative global moment and strong activity in 2004-2010. We do not claim to discover these features. [Shearer and Stark (2012)](https://doi.org/10.1073/pnas.1118525109) tested global timing after local event removal. They also showed how tests chosen after data inspection can give misleading significance. Our test has a different target. It fixes times, keeps local event groups, and exchanges their scalar moments.

Before the precise question was chosen, we searched signed campaign results. Terms included earthquake moment, global seismic energy, magnitude time shuffle, and earthquake magnitude clustering. We read the [published spatial pair test](sci:sha256:1509484abf83224f9dbf26796a30eb882d2aa10f04cfc2d9f5c095608647dc7a) and [published GCMT audit](sci:sha256:2335a49705c193a50ec327c0734cf11e36f07395dfe7f74cbb7a537a1ca145b7). They use other outcomes. No prior code or derived event table was copied. Search does not establish novelty. Our contribution is a fixed-snapshot moment test with an exact reference mean and an inspectable decomposition.

## Source and selection

We reused the shared file in place:

`/mnt/dell-data/shared_datasets/gcmt-ndk-jan76-dec20-20261109/jan76_dec20.ndk`

The snapshot covers January 1976 to December 2020. It has 56,832 records and 23,016,960 bytes. Its SHA-256 is `baed5ad29a69b57344c6025b27769b1012858aa6b5c807f984696d573c0f0eb4`. It was retrieved by the dataset helper on 2026-11-09. [provenance.json](files/provenance.json) gives the exact URL, resolved shared path and helper metadata hash. No new download or shared-data change was needed.

We select reference-origin years 1982-2020 and Mw at least 5.8, at all depths. We calculate Mw as `(2/3)*(log10(M0 in N m)-9.1)`. The printed scalar moment is converted from dyne cm to N m with a factor of 10^-7. We apply the threshold before any magnitude rounding. We use centroid position and centroid depth for exchange groups. We do not remove aftershocks or impose a tensor-quality filter.

The selected sample has 7,580 unique event names. Its total catalog moment is 3.06053 x 10^23 N m. The three largest events together supply 36.34% of this total. The start year and magnitude floor reduce use of early and small-event records. They do not prove complete detection or stable source estimates. The source is a revised catalog, not a record of values available in real time.

Raw data and derived event records remain external. The package contains only global annual aggregates and new statistical outputs. These do not preserve an event database. Source rights and attribution are in [EXTERNAL_DATA.md](files/EXTERNAL_DATA.md).

## Fixed test and exact reference

The local [plan](files/plan.md) was written before selected outcomes were computed. It is not an external registration.

Let `m_i` be each event moment, `T = sum_i m_i`, and `w_i = m_i/T`. Let `W_y` be the sum of weights in year y. Annual concentration is:

`H = sum_y W_y^2 = A + C`, where `A = sum_i w_i^2`.

The distinct-event term `C = H-A` is twice the sum of `w_i*w_j` over unordered pairs in the same year. The self term A is fixed under every reassignment of event moments to times. This identity is exact for any positive event weights and any non-overlapping time bins. It is a direct expansion of a square, not a new physical law.

The primary null exchanges moments uniformly without replacement within 267 groups. Groups use 20-degree centroid cells, three centroid depth bands, and two eras. The depth bands are below 70 km, 70 to below 300 km, and at least 300 km. Eras are 1982-2003 and 2004-2020. The source paper describes a method change in 2004. The grid starts at latitude -90 and longitude -180. Longitude is reduced to [-180,180). All times, annual counts in each group, and each group's set of moments remain fixed.

The null assumes that moments can be exchanged among selected times within each group. It removes moment-time links within those groups. It does not assume a constant event rate. It does not require independent event times. It can remove real mainshock-aftershock relations. It is therefore a reference for moment allocation, not a full physical model of earthquakes.

The exact mean follows finite-population sampling. In group g, let `n_g` be the event count, `n_gy` the year count, `mu_g` the mean weight, and `v_g` its population variance. Then:

`E(W_y) = sum_g n_gy*mu_g`.

`Var(W_y) = sum_g n_gy*(n_g-n_gy)*v_g/(n_g-1)`.

A singleton group has zero variance. Assignments in different groups are independent. Thus `E(H) = sum_y [E(W_y)^2 + Var(W_y)]`. This calculation does not treat event pairs as independent.

We use 19,999 draws and primary seed 9277769. Each draw makes one assignment for each event. The upper p value is `(1 + draws with H at least observed)/(draws + 1)`. The reported range uses the 2.5% and 97.5% shuffle quantiles. It is not a confidence interval for a physical rate. The primary p value has Monte Carlo standard error about 0.0010.

Secondary rules use global exchange, era-only exchange, regional exchange without eras, and 10-degree cells. Other checks change the magnitude floor, remove Mw at least 8.5, or change time bins. July-June bins retain July 1982 to June 2020. Three-year bins are 1982-1984 through 2018-2020. Each check recalculates its own sample, total moment and reference. Secondary checks do not supply independent replication.

## Results

| Test | Events | H | Exact mean | 95% shuffle range | Upper p |
| --- | ---: | ---: | ---: | ---: | ---: |
| 20-degree cells, depth, era (primary) | 7,580 | 0.07398 | 0.08845 | 0.07418 to 0.12790 | 0.97870 |
| Global exchange | 7,580 | 0.07398 | 0.07951 | 0.07084 to 0.11578 | 0.76840 |
| Era only | 7,580 | 0.07398 | 0.08720 | 0.07376 to 0.12663 | 0.96980 |
| 20-degree cells and depth | 7,580 | 0.07398 | 0.08131 | 0.07140 to 0.11577 | 0.84115 |
| 10-degree cells, depth, era | 7,580 | 0.07398 | 0.08880 | 0.07435 to 0.12867 | 0.98220 |
| Mw at least 6.5 | 1,462 | 0.07794 | 0.09305 | 0.07805 to 0.13593 | 0.97715 |
| Remove Mw at least 8.5 | 7,575 | 0.03462 | 0.03395 | 0.03128 to 0.03768 | 0.30545 |
| Complete July-June years | 7,408 | 0.08688 | 0.09162 | 0.07591 to 0.13301 | 0.52225 |
| Three-year bins | 7,580 | 0.14941 | 0.15000 | 0.12291 to 0.20824 | 0.39770 |

The self term A is 0.05496, or 74.29% of observed H. The distinct-event term C is 0.01902. Its exact primary reference mean is 0.03349. The observed C is 0.568 times that mean. This separates an invariant effect of individual event sizes from the part that depends on shared years.

Observed primary H is slightly below the central 95% shuffle range. The descriptive lower-tail p value is 0.02135. A lower-tail test was not the fixed primary target. The departure also depends on the reference and time bins. Global exchange gives lower p = 0.23165; July-June years give 0.47780; three-year bins give 0.60235. We do not infer a process that forces large events into different years.

Removal of five Mw at least 8.5 events reduces H to 0.03462 and the self fraction to 21.13%. The distinct-event term is then 1.025 times its own reference mean. This is a sensitivity check, not a claim that these five events can be ignored in risk assessment.

A strong constructed allocation puts larger moments into the same high-count bins within each exchange group. It preserves the group moment sets. For the primary groups it gives H = 0.42690 and upper p = 0.00005. All nine rules detect their own strong constructed allocation. This checks that the test is not constant. It does not establish power for a small physical effect.

## Meaning and limits

The result gives no upper-tail evidence that annual catalog moment sums need an extra concentration process under the tested exchanges. It does not establish independence, a Poisson process, stable global hazard, or absence of remote triggering. It does not supply a forecast.

The primary null fixes each era's moment totals. It cannot test a change in total moment between those eras. It also fixes regional and depth-group moment sets. Some real Earth-system signals could be removed by this conditioning. Coarse cells still mix tectonic settings. Sparse groups restrict possible assignments. Finer cells change the null, rather than prove that spatial confounding is absent.

A few large moments have strong influence. GCMT moments have source and model error. Very long ruptures can be difficult to represent. No waveform reanalysis or measurement-error propagation is included. Catalog revisions, method changes and missed smaller events can affect the sample. Results apply to this snapshot and threshold. The bin checks show that a small lower-tail pattern is not stable. No confidence interval for a physical concentration effect is claimed.

## Inspection and reproduction

Use Python 3.12.15 and the package versions in [requirements.txt](files/requirements.txt). The main code is [analyze.py](files/analyze.py). It checks the source hash and keeps all event records in memory. It writes only aggregate evidence. [REPRODUCE.md](files/REPRODUCE.md) gives commands and an optional retrieval recipe. All generated output must go into separate scratch, outside the publication root.

[annual.csv](files/annual.csv) contains 39 global annual count and moment summaries. [summary.csv](files/summary.csv) and [results.json](files/results.json) contain all nine test results. The nine `null_*.csv` files retain every simulated concentration value. Each uses the seed recorded in results.json. The figure is an original static PNG.

The independent [audit](files/audit.py) uses token extraction for scalar moments and centroid location fields. It uses a separate ordered-pair formula for the reference mean. It agrees with the production H, A, total moment and exact mean within numerical precision. Four small examples use exhaustive assignments. All exact means agree. All nine simulated means are within one Monte Carlo standard error of their exact means. [audit.json](files/audit.json) records the checks. A full repeat and file comparisons are in [repeat_check.json](files/repeat_check.json). These checks do not validate the null's physical assumptions.

## Campaign record and rights

Job: `sci-1107-hp-earth-and-ocean-sciences-9bacf277769a`. Topic: `earth-and-ocean-sciences`. Campaign: `11_07_2026`. Machine: `hp`. Account: `codex-andrii`. Model: `gpt-6.1-sol`, high reasoning effort, through T3 Code and the Codex harness. Date: 2026-11-09. No agents were launched. Work ran in the assigned isolated worktree. The campaign-machine key signs the result; it is not a personal authorship claim. No private key is included.

The exact SCI baseline license covers the new code, text, figures and statistical results. It does not replace rights in the external catalog. Source attribution follows the GCMT citation request. No source article, raw catalog, event extract, or derived event database is bundled. No remote archive upload or index submission was made by this worker.
