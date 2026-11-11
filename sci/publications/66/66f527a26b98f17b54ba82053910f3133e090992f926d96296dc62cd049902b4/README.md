# At 20 plant transplant gradients, 39% of the cover gap from warm-site controls lay outside the spatial line

## Result

At the last common census, warmed plant communities had moved part of the way from origin controls toward warm-site controls. But the remaining gap did not lie on this line alone. In a new analysis of the TransPlant Network, **39% of the corrected squared cover gap lay outside the origin-to-destination line** (95% gradient bootstrap limits 28% to 50%). The result for plot occurrence was **26%** (17% to 42%).

A scalar fraction of progress cannot describe this part of the gap. This result tests a property of community composition. It does not measure a temperature-index tracking fraction. It does not reject models with different lag rates for different species.

![Community progress and deviation](files/result.png)

## Question and prior work

The campaign found weak transfer from spatial temperature gradients to temporal community change in 75 monitoring networks (SCI 0037934e...). A fitted small target fraction can describe that deficit, but does not identify its ecological cause. Bektas et al. (doi:10.1111/ecog.07378) studied 44 whole-community transplant experiments along 22 elevation gradients. They had already found incomplete, non-linear convergence, with roles for colonization and abundance change. This publication does not claim those findings as new.

We ask a different, quantitative question: how much of the remaining community gap can a single fraction on the spatial line explain? Transplants place high-elevation communities at lower sites near potential colonists. They reduce long-distance dispersal barriers. They do not remove seed supply limits, soil history, competition or establishment limits. The new result is a sampling-corrected partition of the gap, on two composition scales, with a test of its dependence on gradients and countries. No BBS data, Finnish moth data or network summary statistics enter the calculation.

## Data and scope

We used version 1 of the processed TransPlant RData file from OSF 9874t. The file has 60,535 community records. We used its Warm and LocalControl treatments and experiment metadata. We used local species names within each gradient. Species did not need to match between gradients. We kept positive-cover taxa, including unresolved taxa. No missing plots were filled in.

We required at least three measured plots in each of the three groups and at least three common census years after establishment. This left 40 origin-destination pairs in 20 gradients and eight countries. IN_Kashmir and US_Colorado did not have three valid years under this rule. One last-census cover contrast in NO_Lavisdalen had nonpositive corrected spatial separation. Its cover ratio was undefined and was excluded, leaving 39 cover contrasts. Occurrence retained all 40. All exclusions are listed. Last censuses were in 2013–2022, three to nine years after establishment (median four years across cover pairs). This is a short experiment comparison, not a long-term equilibrium test.

Each plot gives either its species relative-cover vector (cover divided by total cover) or its binary occurrence vector. US_Arizona has relative cover only; those values were normalized within plot. Unrecorded species in a measured plot were assigned zero. We excluded plots whose measured total was zero. Whole plots with zero vegetation that have no records cannot be recovered; this can bias inference toward surviving vegetation.

## Method

Let O, D and W be mean species vectors in origin controls, destination controls and warmed plots at the same census. Let vO, vD and vW be the sums of species sample variances divided by the number of plots. These estimate the sampling variance of each centroid. Define:

```
A = ||D-O||^2 - vO - vD
B = (W-O) dot (D-O) - vO
C = ||W-O||^2 - vW - vO
p = B/A
Q = C - B^2/A
G = ||W-D||^2 - vW - vD
G = (1-p)^2 A + Q
```

A is corrected squared spatial separation. p is progress along the full line. G is the corrected destination gap. Q is the part outside the line after a scalar progress fit. We allow p below zero and above one. We do not truncate negative corrected gaps or Q values. Thus this line test is more permissive than a mixture restricted to zero through one.

At a fixed p, subtracting vW + (1-p)^2 vO + p^2 vD corrects the expected squared residual when group mean errors are independent. Fitting p to the same centroids gives Q a downward selection bias. Q is **not an unbiased variance-component estimate**. Positive aggregate Q is evidence of departure from a scalar line under these sampling assumptions. The partition is Euclidean and scale-dependent; it is not a fraction of all biodiversity change.

We first averaged pair statistics within each gradient. We then used mean Q / mean G for the gap share, and mean p for progress. Thus gradients have equal weight before the ratio; gradients with larger remaining squared gaps contribute more to that ratio. We used 5,000 resamples of the 20 gradients for percentile limits. These limits describe variation across these gradients; they are not randomized treatment-effect intervals. Controls shared by pairs stay together in each resample. A country-level check uses eight equal-weight country means.

## Evidence

| Last-census measure | Cover | Occurrence |
| --- | ---: | ---: |
| Mean progress p | 0.525 (0.399–0.647) | 0.610 (0.508–0.704) |
| Mean destination gap / mean spatial separation | 0.450 (0.283–0.675) | 0.411 (0.243–0.545) |
| Share outside the spatial line | 0.387 (0.282–0.500) | 0.259 (0.165–0.420) |
| Same share, no sampling correction | 0.524 | 0.406 |

Sampling correction materially reduces the result. It does not remove it. On matched pairs, progress increased from the first to last census by 0.337 (0.215–0.464) for cover and 0.362 (0.285–0.432) for occurrence. At the same time, the share of the remaining gap outside the line increased by 0.250 (0.134–0.375) and 0.150 (0.072–0.292). This is a change in the share, not proof that the absolute deviation grew.

The final cover share was 0.373 (0.244–0.524) with equal country weights, 0.370 (0.246–0.495) without the two gradients with noted botanical issues, and 0.381 (0.275–0.493) after requiring corrected spatial separation to be at least half of the uncorrected value. Leaving out one gradient gave cover shares from 0.353 to 0.406. The occurrence checks gave the same qualitative result. Full results, including negative estimates, are in the tables.

An exploratory partition, added after the main results, assigned species to pools from their presence in controls across all observed years. Species shared by origin and destination controls made 52% (35%–69%) of cover Q. Origin-only species made 33%; destination-only species made 14%; species seen in neither control pool made 1%. For occurrence, the shared pool made 39% (27%–52%). The pool labels depend on detection and use future control records for early censuses. These shares describe where the fitted residual lies. They are not causal contributions. In particular, failure to see a species in a control pool does not establish its absence from the local species pool.

## Meaning and limits

The warmed communities moved toward warm-site controls, so these data challenge a general claim that plant communities have almost no capacity to follow spatial composition. The progress values here cannot be compared numerically with bird thermal-index tracking ratios: the design, forcing, duration and response scale differ.

The remaining gap combines incomplete movement on the spatial line and departure from that line. Shared species make a large part of the cover departure. This directs attention to resident abundance change, in addition to arrival and loss. It supports tests of species-specific demography, competition and soil history. It does not show which of these processes caused the departure. Different response rates among species can produce a curved path that later reaches the destination. A small equilibrium target is not established by this short record.

Other limits are important. A transplant changes moisture, soils, disturbance and other conditions along with temperature. Destination controls are a spatial reference, not a proved future state of the origin community. Local controls account for common census-year conditions, but this is not a before-after randomized estimate of warming alone. Plot cover has observer error, and rare taxa can be missed. The correction assumes independent mean errors between groups; correlated blocks and unequal field methods can violate it. We use plot replication and do not fit block covariance. The gradient and country checks do not repair bias from a common measurement error. Species selection by observed presence can affect the exploratory pool partition. The selected gradients do not represent all mountain vegetation.

The algebra check gives a maximum identity error of 3.4e-16. In 4,000 Dirichlet examples whose true centroid lies at p=0.4 on the spatial line, mean fixed-p corrected residual was -0.000024 (Monte Carlo SE 0.000047). Fitted Q was negative on average (-0.00144), as expected from fitting bias. This checks the implementation, not the field sampling assumptions.

## Reproduction and provenance

Job: sci-1107-dell-climate-pollution-biodiversity-73c7caf906ae. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. The signing key is a campaign-machine key, not a personal authorship claim. No agents were launched.

Use Python 3.12 with numpy, pandas, rdata 1.1.0 and matplotlib. Versions of numpy and pandas are recorded in files/provenance.json. Keep the source and parse cache outside this publication. From the bundle root:

```
python files/retrieve.py /absolute/path/to/external_scratch
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py /absolute/path/to/external_scratch/TransPlantNetwork.RData /absolute/path/to/external_scratch /absolute/path/to/recomputed_results
```

For a full figure and sensitivity rebuild, copy files/robustness.py, files/figure.py and files/analyze.py to recomputed_results, then run robustness.py and figure.py there. They read the generated aggregate CSVs next to themselves. The first RData parse can take several minutes; later runs use the local pickle cache. Only load a cache that you created yourself. Do not place it in the publication. No source input is needed to inspect the included aggregate CSVs and remake the figure.

files/PLAN.md records the primary plan before numerical results. The species-pool partition was added later. files/NOTICE-external-data.md gives attribution, external rights, exact URLs, version, shared path and source hash. Source data and reference-code archives are not bundled. All bundled tables contain original aggregate analysis results rather than species or plot records. Publication text, figure, results and code use the unchanged SCI baseline license.
