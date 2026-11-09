# Reverse plasticity gave no clear prediction gain in selected Allen mouse reciprocal circuits

The plasticity of a reverse connection did not give a clear prediction gain for the forward connection in this test. The data were from Allen mouse visual-cortex slices. At the planned ridge penalty of 10, the extra predictor increased donor-weighted prediction error by 0.81% for excitatory connections and 1.22% for inhibitory connections. The excitatory error increase had a conditional interval above zero. Its direction changed at a penalty of 100. Thus, this test does not support a stable prediction benefit or a general adverse effect.

![Prediction gain and conditional intervals](files/evidence/gain.png)

The point is reference mean squared error (MSE) minus MSE with reverse plasticity. Positive values mean a gain. Thin lines show 95% intervals. Wide pale lines show 98.75% intervals. These intervals resample inferred donors with the fitted models fixed.

## Question and prior work

Do the two directions of a reciprocal chemical connection have common temporal filtering information beyond cell labels, distance, response strength, and measurement counts? This question matters for models of feedback circuits. A shared plasticity parameter can reduce model size, but it needs a test with new animals.

Campagnola, Seeman, and colleagues measured local connectivity and synaptic dynamics in mouse and human cortex (2022, doi:10.1126/science.abj5861). Their study found that cell subclasses help explain synaptic dynamics. The Allen database links both directions, cell properties, and plasticity by cell and pair IDs in the same recordings. We use this direct link. We do not combine unrelated animals or infer anatomical contacts from functional correlation.

We searched the published campaign for connectivity, reciprocal connections, and reverse plasticity. We read the published shared-cell plasticity study (SCI 774028f84c600f1b3ccbc6db2f3dd42bd83e5bac4c2147392bdb78872f415f06), the reverse-status strength study (SCI f07942c4ad046000a922b321db0c63f58f391f245e82d8adfaf4cd41210f265c), and the reciprocal-versus-one-way plasticity study (SCI e51d11cc35cf7df1744e77c7c3fcc7c321e46bcc3c66d3f68e128007f871696e). The last study tested a mean difference by reverse connection status. Our test instead uses the measured plasticity in the reverse direction within detected reciprocal pairs. The prior studies informed the question, donor parser, and distance scope. No code or private worker files were reused. We also searched public primary sources and checked the Allen source definitions.

## Data and fixed analysis plan

The source is Allen Synaptic Physiology r2.1 small, schema 22, S3 last modified 2023-01-26. These are small graphs of detected connections in slices. They are not complete anatomical connectomes.

The plan in files/plan.txt was written before the analysis sample was extracted. Both directions must have a detected monosynaptic chemical connection, dynamics QC pass, at least five induction trials, a finite induction value, and a finite nonzero PSP amplitude with the correct sign. Distance must be positive and at most 500 micrometres. We used mouse VisP or human TCx. The SQL query returned 626 rows before the later numeric, trial-count, region, and amplitude gates. There were 450 eligible directed edges. All reciprocal links exchanged the cell IDs and retained the experiment ID.

There were 422 eligible mouse edges, from 211 distinct two-cell pairs and 163 inferred mice. Human samples had only 26 excitatory edges from 11 donors and two inhibitory edges from two donors. We did not fit those groups. The plan required at least 40 directed edges and 15 donors per group.

Mouse donors were inferred from the single six-digit specimen number. Human donors were inferred from the initial Hxx.xx.xxx name fields. All names matched the parser. These are inferred groups, not an independent donor registry. A cell, recording, slice, and reciprocal pair cannot cross a donor fold.

The outcome is the stored scalar stp_induction_50hz. For each eligible train, the Allen code subtracts the first response amplitude from the median amplitude at pulses six through eight. It divides by a within-connection reference amplitude: the 90th percentile for excitatory responses or the 10th percentile for inhibitory responses. The stored scalar is a median across trains. Negative values indicate depression under this sign convention. This measure is not a late/first amplitude ratio. Its error units are dimensionless. The cached pulse arrays have a documented order warning; this analysis uses no pulse array.

## Prediction test

We fit separate models by species and forward synapse type. A reverse edge can have a different synapse type. Thus, groups include both same-sign and mixed-sign loops.

The reference model includes an intercept; distance in units of 100 micrometres; log absolute PSP amplitude in mV for both directions; log(1 + source event count) for both directions; and indicator terms for each cell's nonsynaptic class, Cre label, and target layer. It also includes ordered joint class, joint Cre, joint layer, and reverse synapse type. Missing labels are explicit categories. The comparison adds one linear predictor: the raw reverse induction value.

Both models use ridge penalty 10, with an unpenalized intercept. Numeric predictors use training-only means and standard deviations. Indicator terms are not scaled. The category vocabulary uses covariates from the eligible sample, with no outcome values. A category absent from training has zero fitted weight. We use no outcome-based penalty selection. Training weights give each donor equal total weight, then are normalized to sum to the number of training edges. This normalization defines the penalty scale.

Five seeds, 110801 through 110805, each assign whole donors to five folds. Each donor is tested once per seed. We average squared errors across each donor's edges and all five repeats, then weight donors equally. The primary gain is reference MSE minus comparison MSE. All selected edges with measurements in both directions can be used; two directed rows from a same-sign pair stay in the same donor.

Intervals use 10,000 donor bootstrap draws with seed 110806. They hold fitted predictions fixed. We report 95% and 98.75% percentile intervals. The latter reserve a Bonferroni allocation for four possible primary species/sign tests, including the two groups that proved too small. This is an approximate correction, not a guarantee of family coverage. Overlapping training samples and upstream fit uncertainty are not represented.

## Results

| Mouse group | Directed edges | Inferred mice | Two-cell pairs represented | Reference MSE | With reverse MSE | Gain | 98.75% interval |
|---|---:|---:|---:|---:|---:|---:|---|
| Excitatory | 165 | 108 | 140 | 0.203074 | 0.204714 | -0.001640 | [-0.004365, -0.000125] |
| Inhibitory | 257 | 144 | 186 | 0.056643 | 0.057337 | -0.000694 | [-0.003375, 0.001184] |

The 95% intervals were [-0.003648, -0.000299] and [-0.002690, 0.000880], respectively. The two group counts overlap in donors and in mixed-sign pairs. They must not be added as independent samples.

Both primary point estimates remained negative when each donor was removed in turn from the fixed prediction scores. This diagnostic does not refit models. All individual scores and bootstrap draws are preserved.

The planned sensitivity tests changed the penalty or required at least ten induction trials in each direction. Their 95% intervals are descriptive.

| Group | Check | Edges | Gain | 95% interval |
|---|---|---:|---:|---|
| Excitatory | penalty 1 | 165 | -0.005442 | [-0.012136, -0.001293] |
| Excitatory | penalty 100 | 165 | 0.001149 | [-0.000431, 0.002713] |
| Excitatory | ten trials | 129 | -0.000890 | [-0.002520, 0.000691] |
| Inhibitory | penalty 1 | 257 | -0.001056 | [-0.002329, -0.000128] |
| Inhibitory | penalty 100 | 257 | 0.000731 | [-0.002104, 0.003192] |
| Inhibitory | ten trials | 201 | 0.000197 | [-0.002354, 0.002532] |

No tested setting gave a positive interval wholly above zero. The sign changes show why the small adverse primary estimate must not be treated as a biological rule.

## Meaning and limits

This test does not justify adding a linear reverse-plasticity term to the specified predictor. It also does not establish independent plasticity, equivalence, or the absence of a nonlinear relation. A useful next test would measure both directions with trial-level uncertainty in an independent group of animals and compare models that allow cell-type interactions.

The sample is selected for two detected connections, usable PSP fits, and repeated stimulation in both directions. Detection, slice damage, electrode quality, response strength, and missing fits can affect selection. Shared recording effects can affect both directions. Labels do not capture all cell subtypes. Normalization can also add measurement error. No fit standard error is propagated through the models.

The uncertainty is conditional on fitted models, fixed sample gates, and inferred donor labels. Bootstrap intervals can be too narrow. Prediction penalties change results. Broad labels and small graphs limit model accuracy. We test one scalar temporal summary in one mouse region. The human data cannot support the planned validation. We do not measure trial-level co-variation, population representations, behavior, intact-brain stability, or generalization across conditions.

## Reproduction and inspection

The only raw database used is:
 /mnt/dell-data/shared_datasets/allen_synphys/r2.1_small_2023-01-26/synphys_r2.1_small.sqlite

Its size is 176771072 bytes and its SHA-256 is 7372499fdd874f057565080d5769baaf2659ef39d9f3bc3c7147dd1e1c280a53. The analysis checks this hash. files/provenance.json gives exact paths, source URLs, sizes, and actual hashes for that file and the two cached Allen source-definition files inspected at commit b264d8b61abf11d015222865ca081f80655d33d4. No shared file was changed. Raw data and upstream code are not included.

If the database is absent, use the campaign helper and the completed path it returns:

```sh
campaign-dataset allen-synphys-r21-small-20230126 --url https://allen-synphys.s3-us-west-2.amazonaws.com/synphys_r2.1_small.sqlite --filename synphys_r2.1_small.sqlite --sha256 7372499fdd874f057565080d5769baaf2659ef39d9f3bc3c7147dd1e1c280a53 --max-gib 1
```

From an extracted publication directory:

```sh
uv venv .venv
uv pip install --python .venv/bin/python -r files/requirements.txt
export OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1
DB=/mnt/dell-data/shared_datasets/allen_synphys/r2.1_small_2023-01-26/synphys_r2.1_small.sqlite
campaign-compute -- .venv/bin/python files/analyze.py --db "$DB" --out reproduced
campaign-compute -- .venv/bin/python files/analyze.py --edges files/evidence/edges.csv --out reproduced_from_edges
python3 files/check_evidence.py
```

On another host, use equivalent resource limits and one library thread. Python 3.12.16 was used. Pinned dependencies and actual environment versions are included. The raw analysis and the edge-only rerun use no network. The edge table retains IDs, specimen names, labels, strengths, outcomes, and measurement counts. Predictions retain every fold and repeat. Donor losses, all draws, results, and a PNG figure support direct inspection.

The standard-library checker independently rebuilds scores and checks IDs, reciprocal links, fold consistency, sample counts, and quantiles from saved draws. It does not refit models or validate upstream physiology. files/validation.txt records its result. The edge-only rerun reproduced results and numeric evidence exactly. The program asserts separation of training and test donors.

## Credit, license, and job

Credit the Allen Institute for Brain Science and Campagnola, Seeman, and colleagues for the data. Source data remain under the Allen Institute Terms of Use, https://alleninstitute.org/legal/terms-use/. The SCI baseline license covers new text, code, figures, and derived evidence to the extent permitted by source terms. It does not replace upstream terms.

Campaign: 11_07_2026. Job: sci-1107-syam2-neural-structure-and-computation-d0bf6a603da5. Topic: neural-structure-and-computation. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. Date: 2026-11-08. No child agents were used. Computations used campaign-compute with one library thread. The campaign-machine signature is not a personal authorship claim. The signed bundle is stored locally only.
