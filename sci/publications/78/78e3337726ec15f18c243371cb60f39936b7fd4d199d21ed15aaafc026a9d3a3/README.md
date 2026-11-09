# Deep GCMT pairs gave no clear extra tensor similarity under regional time shuffles in 1980-2020

We tested moment tensor similarity in deep earthquake pairs within 200 km and seven days. We used 1,064 Global CMT events with centroid depth greater than 300 km and computed Mw at least 5.5 in 1980-2020. We removed mean similarity in groups defined by year, region, distance and depth. The 106 close pairs had mean residual similarity 0.0246. In 9,999 regional time shuffles, the mean was -0.0001 and the central 95% range was -0.0429 to 0.0413. The upper-tail p-value was 0.1269. Thus this test gave no clear extra similarity. Six checks also gave no clear excess. This does not establish absence or reject triggering. Sparse groups, shared events, centroid errors, catalog selection and the time exchangeability assumption limit inference. The package gives original code, aggregate evidence, source hashes, a figure and an arithmetic audit. External catalog records are excluded.

![Tensor similarity test](files/similarity.png)

## Question and prior work

Does the close-pair count pattern also have a detectable moment tensor pattern? The campaign result SCI 3f3a445cedb4d57a6435d68b6ec65f2cc8353ab5006d6e5d0a26b4c5c9401a16 found excess close deep pairs in ComCat. We read that signed result after campaign searches for earthquake, deep earthquake mechanism and warm water volume. We then chose a new tensor test in a separate catalog. No private worker workspace was read. This is not an independent replication of its pair count result.

Deep earthquake clustering and similar mechanisms are known. Wiens and McGuire (2000, doi:10.1029/2000JB900097) described similar mechanisms in the 1994 Tonga sequence, with regional background similarity. A 2026 Tonga study (doi:10.1029/2025JB033217) groups mechanisms to study slab fault zones. Wilding and Ross (2022, doi:10.1029/2022GL098473) used tensor inner products to study changes within earthquake sequences. Our test has no assigned parent or before-after comparison. It asks a narrower catalog question with coarse spatial matching and a regional time null. It does not introduce tensor inner products as a new method.

## Data and rights

We reused datasets/gcmt-ndk-jan76-dec20-20261109/jan76_dec20.ndk in place. The file covers 1976-2020 and was retrieved on 9 November 2026. It has 23,016,960 bytes and SHA-256 baed5ad29a69b57344c6025b27769b1012858aa6b5c807f984696d573c0f0eb4. Exact source URL, shared path, resolved path and metadata hash are in files/provenance.json. We checked the NDK format document and Global CMT citation page. We cite Dziewonski et al. (1981) and Ekstrom et al. (2012) as requested.

We use centroid depth greater than 300 km, centroid location, reference origin time in UTC, and years 1980-2020. Computed Mw must be at least 5.5, without rounding. Mw is (2/3)(log10(M0)-16.1), with scalar moment M0 in dyne cm. We do not use body-wave magnitudes on the first NDK line. There are 1,064 unique selected event names. No quality filter is used. Completeness and source error are not estimated.

External catalog records, event tables and pair records are absent from this package. files/EXTERNAL_DATA.txt gives attribution and explains the external-data boundary. No explicit database relicensing grant was found. We therefore include only original code, text, figure and statistical summaries. We do not assert baseline rights in the external catalog or replace its terms. No derivative event database is bundled.

## Method and assumptions

files/design.txt records a local plan saved before analysis. It is not a public registration. Each unordered pair must be in the same UTC year. The primary radius is 200 km. We convert centroids to Cartesian positions at radius 6371 minus depth in km. Separation is the Earth chord distance. Time-close pairs have an absolute origin-time gap greater than zero and at most seven days. Cross-year pairs are excluded in observations and shuffles.

We form the full symmetric tensor from six NDK components. We rotate the local up, south and east basis into common Earth Cartesian coordinates at the centroid. We divide each tensor by its Frobenius norm. Similarity is the matrix inner product of normalized tensors, from -1 to 1. A value of 1 means identical normalized tensors; -1 means opposite tensors. The sign is retained. This is not a double-couple rotation angle. Non-double-couple terms remain.

Matching uses all 1,315 spatial pairs, including pairs more than seven days apart. A group has the same year, unordered pair of endpoint grid cells, 50 km distance bin, 100 km mean-depth bin and 50 km depth-difference bin. All bins start at zero and use floor division. Grid cells are 20 degrees wide and start at -90 latitude and -180 longitude. We subtract each group mean from pair similarity. There are 632 groups. Singleton groups have zero residual; 37 of 106 close pairs have zero residual to numerical tolerance. Tight matching can remove genuine signal and reduce power. Group means include time-close pairs.

The statistic is the mean residual among time-close pairs. Large clusters can contribute many dependent pairs. A shuffle randomly assigns the fixed time list to fixed event records within each year and grid cell. Locations and tensors stay together. Groups are shuffled independently. Matching means stay fixed. We use 9,999 draws and seed 110719. The upper-tail p-value is (1 + number of shuffled statistics at least as large as observed)/10,000. There is one primary test. Checks are pointwise, without multiple-test correction.

The null assumes time exchangeability within each year and cell. It preserves regional bursts, but breaks fine location-time and tensor-time relations together. Spatial centering reduces a simple geometry effect; it does not isolate a causal tensor effect. Migration, separate active slab segments, changing detection and sequence errors can violate the null. Null ranges are not effect confidence intervals. No independent-pair standard errors are used.

## Results

| Test | Events | Close pairs | Residual mean | Null mean | Null 95% range | Upper p |
|---|---:|---:|---:|---:|---|---:|
| primary | 1064 | 106 | 0.0246 | -0.0001 | -0.0429 to 0.0413 | 0.1269 |
| radius100 | 1064 | 74 | 0.0249 | -0.0003 | -0.0529 to 0.0501 | 0.1722 |
| radius300 | 1064 | 137 | 0.0107 | -0.0002 | -0.0354 to 0.0359 | 0.2740 |
| grid10 | 1064 | 106 | 0.0240 | -0.0001 | -0.0354 to 0.0345 | 0.0889 |
| depth400 | 914 | 103 | 0.0253 | -0.0003 | -0.0429 to 0.0419 | 0.1150 |
| mw6 | 388 | 29 | 0.0093 | 0.0001 | -0.0105 to 0.0108 | 0.1497 |
| without2018 | 1022 | 98 | 0.0148 | 0.0000 | -0.0398 to 0.0399 | 0.2317 |


Primary raw similarity is 0.6585. That high value alone does not show a time relation: nearby slab events can have similar mechanisms. The residual mean lies inside the central null range. Its difference from the null mean is 0.0247. We did not establish extra similarity under this null. Each planned check also has an upper-tail p-value greater than 0.05. That is not proof of no effect.

The primary shuffle mean pair count is 95.51, with central 95% range 84 to 108, against 106 observed pairs. This diagnostic is not a replication of the ComCat result. Source locations, depth definitions, magnitude selection and years differ.

Deleting one year at a time gives residual means from 0.0094 to 0.0338, and upper-tail p-values from 0.0545 to 0.3346. These are influence checks, not confidence bounds. All checks and all shuffle statistics are saved as aggregate tables.

## Interpretation and limits

A triggered event may share a mechanism with its parent, but need not do so. A common stress field can also give similar mechanisms without triggering. This null result does not reject either process. It does not establish equal mechanisms in close and distant times, rule out a modest effect, or bound a true physical effect. No power or equivalence test was made.

Only relatively large events enter. Close pairs are few and many matching groups are sparse. Centroid errors affect distance and depth matching. Tensors come from long-period inversions, not resolved rupture planes. We do not propagate tensor or location errors. Fixed and free centroid depths are mixed. Catalog methods and detection can change with time. Dense sequences get more weight. Grid and year boundaries are artificial. Other matching choices can give other results. This test does not forecast hazard or identify a water or ocean cause.

## Reproduction and validation

Verify and extract the SCI ZIP. Use Python 3.12 with numpy, pandas and matplotlib. Exact installed versions are in files/environment.json. Use the exact shared source above. To retrieve separately, run:

    python files/retrieve.py --scratch /absolute/path/new-external
    python files/analyze.py --source /absolute/path/new-external/jan76_dec20.ndk --out /absolute/path/new-results
    python files/audit.py --source /absolute/path/new-external/jan76_dec20.ndk --results /absolute/path/new-results --out /absolute/path/new-audit.json

The retrieval script refuses the publication as scratch and checks the source hash. If live bytes change, exact reproduction needs the preserved shared snapshot. No shared file is modified. Output folders must be new. Analysis takes several minutes. files/summary.csv, files/*_draws.csv and files/year_deletions.csv preserve all reported aggregate evidence. The static figure meets SCI display limits.

The audit parses selected centroid fields, scalar moment and times independently. It builds tensors by sums of basis dyads and checks all spatial pair membership with a spherical cosine formula. It checks observed counts, residual means and the p-value against stored results. Maximum tensor difference is 2.2e-16; maximum pair distance difference is 1.1e-09 km. The audit passed. It also replays the first 100 permutations and matches their saved scores. It shares the matching function and does not independently regenerate every permutation. It validates arithmetic, not physical assumptions.

## Campaign record

Job: sci-1107-dell-earth-and-ocean-sciences-19d3bb42105f. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort, through T3 Code and the Codex harness. Date: 9 November 2026. No agents were launched. The signing key identifies the campaign machine, not a personal author. No private key is included. No remote upload or index submission was made.
