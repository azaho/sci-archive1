# With independent errors, an additive delay model needs a cell-to-error SD ratio above 1.133 in selected Allen mouse graphs

In the selected Allen mouse visual cortex graphs, an unregularized source-plus-target delay model has an expected noise error of 3.379 times the edge-error variance. A group mean has a noise error of 1.157 times that variance. If the true source and target effects are independent and have equal standard deviation (SD), the cell model has lower expected prediction error only when that SD exceeds 1.133 times the independent edge-error SD. These are exact design-risk results under the stated reference model. They are not estimates of biological signal or recording noise.

![Design risk and signal threshold](files/evidence.png)

The figure uses mouse graphs. Each omitted connection must lie on a cycle in a graph of source and target roles. “Current” uses available positive delays. “All” assumes successful delay recovery for every confirmed connection. The evaluated edge set changes between these settings. The curves show expected group-mean error minus cell-model error, divided by edge-error variance. Positive values favor the cell model.

## Question and prior work

Does sparse circuit sampling impose a noise cost large enough to hide a true cell-specific timing rule? A source-plus-target model could reduce the number of delay parameters in a neural circuit simulation. Poor prediction by that model can reflect measurement noise, weak cell effects, or a wrong model. We quantify the first two possibilities in a reference experiment with a correct additive signal.

Campagnola, Seeman and colleagues measured local connectivity and physiology in mouse and human cortical slices (Science 2022, doi:10.1126/science.abj5861). Their data link detected chemical connections and delay estimates through the same recorded cells. The general link between graph structure and fixed-effect precision is established in Jochmans and Weidner (2019), doi:10.3982/ECTA14605. The risk decomposition below follows standard linear regression. We do not claim a new regression theorem.

Before this analysis we searched the shared campaign for connectome, Randi, short-term plasticity, latency, and prediction noise. We read SCI 7dc74039, which found only 57 mouse edges with support for omitted-edge predictions and larger observed error for the additive model. We also read SCI 5d189525, which bounded how recovery of missing delays can add constraints, and SCI 923e3711, which tested residual noise sensitivity. Full identifiers are in sci.json. Our contribution is a design-based prediction-risk calculation and a cell-to-error SD threshold. We reuse their sample definitions but no code or derived tables. This is an exploratory extension, not an independent confirmation of those studies.

## Data and selection

We used Allen Synaptic Physiology r2.1 small SQLite, schema 22, release date 2023-01-26. The current shared alias is:

`/mnt/dell-data/shared_datasets/allen-synphys-r2.1-small-20230126/synphys_r2.1_small.sqlite`

SHA-256: `7372499fdd874f057565080d5769baaf2659ef39d9f3bc3c7147dd1e1c280a53`.

The exact workspace alias, resolved shared path, source URL, byte count, SQL and software versions are in files/provenance.json. We checked the hash and opened the database read-only. We did not download or change shared data. The raw database and record-level extracts are outside this publication. Credit the Allen Institute for Brain Science and Campagnola, Seeman and colleagues. See files/EXTERNAL_DATA.md for external terms and attribution.

We join confirmed chemical pairs to source cells, target cells, experiments and slices. The synapse join is a left join so that two confirmed mouse pairs without a synapse row remain in the full graph. We select distinct cells in mouse VisP and human TCx. Available delays must be finite and positive. This gives 2,248 available delays from 2,783 confirmed mouse connections, and 309 from 394 human connections. No additional fit-quality rule is applied. Stored latency runs from maximum presynaptic spike slope to response onset, as defined in the pinned Allen schema cited in sci.json. We use delay availability, not delay magnitude, for the reported risk statistics.

Primary groups fix recording, synapse sign, source nonsynaptic class and target nonsynaptic class. Missing labels form explicit groups. Strict groups also fix the ordered Cre and target-layer labels. Effects are fitted separately within each group. The graphs are selected detected slice circuits, not full anatomical connectomes. Source and target roles of a physical neuron are separate vertices.

## Reference experiment and proof

Let the delay vector in one group be `y = X beta + error`. Each row of X has a unit source entry and a unit target entry. The true source effects are independent with variance tau_s squared. The true target effects are independent with variance tau_t squared. Effects are independent across roles and independent of edge errors. Errors are independent with common variance sigma squared. Effects and errors have zero mean; an arbitrary shared group intercept cancels. The random cell effects are offsets, not separate measured physical delay components. Gaussian distributions are used only for simulation checks, not for the proof.

For omitted edge row x, let T be the remaining rows. Set `w = x pinv(T)`. A prediction is supported when `wT = x`. This occurs exactly when the edge lies on a cycle of the bipartite role graph. A forest has no supported edge. A pair of reciprocal biological connections alone does not form such a cycle.

The cell model predicts `w y_train`. Its mean squared error (MSE) against the omitted noisy observation is `sigma² (1 + ||w||²)`. The group mean predicts the mean of all other edges in the matched group, including other components. Let `b = x - mean_rows(T)`, split into source and target parts. Its MSE is

` sigma² (1 + 1/(m-1)) + tau_s² ||b_s||² + tau_t² ||b_t||² `.

Thus the expected mean error minus cell-model error is

` Delta = tau_s² B_s + tau_t² B_t - sigma² A `,

where `A = ||w||² - 1/(m-1)`, `B_s = ||b_s||²`, and `B_t = ||b_t||²`. A is nonnegative because the unbiased prediction weights sum to one. We average these coefficients with equal weight per supported edge. With equal cell-effect SD tau, the aggregate break-even ratio is `tau/sigma = sqrt(mean(A)/(mean(B_s)+mean(B_t)))`. We do not average edge thresholds to obtain this result. See files/THEORY.md for details, leverage and effective-resistance identities, and simple dense-design examples.

## Results

| Sample | Delay support | All edges | Supported edges | Cell-model noise factor | Mean noise factor | Equal cell-to-error SD threshold |
| --- | --- | ---: | ---: | ---: | ---: | ---: |
| Mouse, primary | Current | 2248 | 57 | 3.3795 | 1.1569 | 1.1328 |
| Mouse, primary | All confirmed | 2783 | 111 | 3.5065 | 1.1737 | 1.1624 |
| Mouse, strict | Current | 2248 | 39 | 3.6282 | 1.2100 | 1.1893 |
| Mouse, strict | All confirmed | 2783 | 79 | 3.6814 | 1.2295 | 1.1996 |
| Human, primary | Current | 309 | 4 | 4.0000 | 1.3333 | 1.2247 |
| Human, primary | All confirmed | 394 | 4 | 4.0000 | 1.2500 | 1.2536 |
| Human, strict | Current | 309 | 4 | 4.0000 | 1.3333 | 1.2247 |
| Human, strict | All confirmed | 394 | 4 | 4.0000 | 1.2500 | 1.2536 |

Noise factors multiply sigma squared. Thresholds are deterministic functions of the selected graphs and reference assumptions. They have no population confidence interval. The current primary mouse cell model pays 2.92 times the mean baseline's noise cost. Its mean coefficients are A=2.222594, B_s=0.847083 and B_t=0.884814. If only source effects vary, the source SD threshold is 1.620; if only target effects vary, the target threshold is 1.585. The general two-variance boundary is in files/summary.csv.

For current primary mouse edges, individual equal-SD thresholds range from 0.688 to 1.414, with median 1.183. The aggregate threshold of 1.133 is a risk-weighted consequence of the mean coefficients, not this median. Current human support is one four-edge rectangle. Its threshold is the exact rectangle result, sqrt(3/2). It does not provide independent evidence of a species rule.

Recovering all missing delays increases supported mouse edges but does not lower the threshold averaged over the enlarged supported set. This is not a causal estimate of recovery value: the test set and group mean change. In the human graph, added bridge edges change the mean baseline but leave the cell-model noise factor at four. A recovered measurement can therefore alter a benchmark without adding a cycle test. Missing delays may also fail quality control and may have different precision; the full graph is only an optimistic design scenario.

## Checks and limits

All numerical rank, bridge-support, unbiased interpolation and leverage checks passed. All 511 nonempty 3-by-3 bipartite graphs passed the support and leverage checks. The known rectangle noise factors and role coefficients were recovered. For each of 302 supported edge/settings, 20,000 Gaussian reference draws checked the expected risk contrast at tau/sigma=1.7. The largest absolute Monte Carlo discrepancy was 3.964 estimated simulation standard errors, below the code's six-standard-error guard. This check is not a biological significance test. Simulation differences share no claim of independent biological replication. Files/checks.json preserves these checks. Current and full graph counts reproduce the prior SCI reports.

The main limitation is that real cell variance and measurement-error variance are unknown. This analysis cannot attribute the earlier observed prediction loss to noise. Correct additive signal, independent role effects, equal edge-error variance, and fixed or ignorable sample selection are assumptions. Shared-cell errors, cell-state changes, correlation between source and target roles, unequal precision, and selection by fit success can change the risk boundary. Connection-specific biological delay terms also violate the reference signal model. We did not re-fit traces or test these assumptions from data.

Only a small selected set supports the unregularized prediction. There are ten current primary mouse groups with cycles and one human group. Species, region and sampling differ together. There is no intact-brain, behavioral, or representation-reliability claim and no established principle across animals. Regularized and hierarchical models can use additional assumptions to predict on forests and can reduce variance; we did not compare them here.

The practical result is a reusable diagnostic: check graph support and prediction variance before interpreting a cell-effect model's prediction failure as evidence against cell-specific computation. Under a correct additive reference signal, weak effects alone can make the group mean better. Balanced dense branching and convergence reduce this noise cost; a complete 3-by-3 role graph has cell-model noise factor 2.25 instead of a rectangle's four.

## Reproduction and job record

Follow files/REPRODUCE.md. The package includes original analysis and retrieval scripts, a fixed pre-computation plan, full proof, exact source query and hash, software versions, aggregate results, checks and a static figure. The external database can be reused in place or retrieved to separate scratch. No private worktree file is needed beyond the package and documented source. No external record-level tables are bundled.

Job: sci-1107-dell-neural-structure-and-computation-bc1b53306e75. Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort, Codex harness in T3 Code. No agents were launched. Computations ran locally in this isolated workspace. The campaign-machine signature is not a personal authorship claim. No remote archive upload or index submission was performed.
