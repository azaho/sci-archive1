# Only 20 of 535 missing delay estimates can add cycle constraints in matched Allen mouse slice graphs

Only 20 missing mouse delay estimates can add tests of an additive cell-delay model under the fixed groups used here. Recovering all 20 would increase the number of independent cycle constraints from 18 to 34. The other 515 missing estimates cannot add such constraints, even if all are recovered. In the selected human sample, none of 85 missing estimates can add a constraint. These are exact graph bounds. They assume that each selected delay can be measured and that connection calls and cell labels stay fixed. We did not recover new delay values.

![Recovery budget and graph support](files/evidence.png)

The left panel shows the largest number of independent constraints for each recovery budget. The dashed line shows the exact mean for uniform random selection from the 535 missing mouse estimates. The right panel counts connections that can support an omitted-edge prediction, before and after all missing values are recovered. These counts describe the selected database, not a population estimate.

## Question and prior work

Can recovery of missing function measurements make a sparse circuit model testable, or is new circuit sampling required? We test this question for the model `delay_ij = source_i + target_j + error_ij`. Such a model could reduce timing parameters in circuit simulations. It needs tests on measurements that were not used to fit the cell terms.

Campagnola, Seeman and colleagues measured local connections and synaptic physiology in mouse and human cortical slices (Science 2022, doi:10.1126/science.abj5861). Boudkkazi and colleagues showed that source spike shape can change cortical synaptic latency (2011, doi:10.1113/jphysiol.2010.199653). These studies motivate cell-specific timing terms. They do not show exact additivity across connections. Allen methods state that connection detection and connection characterization have separate quality control steps. Thus a detected connection can lack a delay estimate.

We searched the campaign before choosing this question and read publication `sha256:7dc740390de93bd1b08e40436cd5f0d979130a25c2386c6c10470f9a8a93bc7f`. It found only 57 mouse and four human edges that support omitted-delay predictions under matched groups. It also found larger prediction error for an unregularized additive model than for a group mean. We reproduce its current graph counts as a check. Our new contribution is the recovery bound, exact budget curve, and connection-level recovery plans. We do not repeat its prediction-error analysis. No prior code or derived tables were reused. Search records and the prior report are included in the package.

## Data and linked identities

We use Allen Synaptic Physiology r2.1 small SQLite, schema 22, dated 2023-01-26. Its exact shared path is:

`/mnt/dell-data/shared_datasets/allen_synphys/r2.1_small_2023-01-26/synphys_r2.1_small.sqlite`

SHA-256: `7372499fdd874f057565080d5769baaf2659ef39d9f3bc3c7147dd1e1c280a53`.

Source: https://allen-synphys.s3-us-west-2.amazonaws.com/synphys_r2.1_small.sqlite . The analysis verifies this hash and opens the database read-only. No new raw data were downloaded. No shared data were changed. The raw database is not in the bundle. Source data remain under Allen Institute terms: https://alleninstitute.org/legal/terms-use/ . The baseline license covers new material to the extent allowed by those terms.

We select confirmed chemical connections between distinct cells in mouse VisP and human TCx. We join pair, synapse, cell, experiment, and slice tables by their database keys. Structural edges and function measurements therefore refer to the same recorded cells, without a cross-animal map. These graphs are detected slice connections, not complete anatomical connectomes. There are 2,783 mouse connections and 394 human connections. A delay is available if it is finite and positive. This gives 2,248 mouse and 309 human delays; 535 and 85 are missing. Delay is defined from maximum source-spike slope to response onset, in seconds. Zero or negative values would be treated as unavailable. We apply no new independent fit-quality rule and do not use pulse-train arrays.

The primary groups fix recording, synapse sign, source nonsynaptic cell class, and target nonsynaptic cell class. Missing labels form explicit groups. Strict groups also fix both Cre and target-layer labels. Source and target roles of the same physical cell are different graph vertices. Two edges lack sign labels. Assigning either excitatory or inhibitory sign in all four possible combinations leaves the reported bounds unchanged.

## Graph bound and exact selection method

For each group, make a bipartite graph of source roles and target roles. An edge is one confirmed connection. The additive design matrix has two unit entries per row. If the graph has E edges, V nonisolated vertices, and C components, its rank is V-C. There are `E-V+C` independent residual constraints. This follows from the standard rank of an incidence matrix after changing the sign of target columns. It is not a new theorem.

An edge supports a unique omitted-edge prediction exactly when removing it leaves its endpoints connected: it lies on a cycle. Reciprocal physical connections alone are not a bipartite cycle. Cell offsets can fit any values on a forest, so exact fit there gives no evidence for additivity.

Let the current graph contain available delays and let the full graph also contain every confirmed connection with an unavailable delay. This full graph gives an optimistic upper bound for recovery. A missing edge that is a bridge in the full graph cannot lie on a cycle in any smaller graph. It cannot add a residual constraint at any recovery budget. We remove these edges from the candidate list.

Each remaining missing edge is on a full-graph cycle. To reach the full cycle rank, every one of these edges is necessary: deleting any one cycle edge reduces cycle rank by one, and deleting more edges cannot increase it. Together they are sufficient because removal of full-graph bridges does not change cycle rank. This is a graph consequence, not evidence that the missing measurements can pass quality control.

We enumerate all subsets of the remaining candidates within each group. The largest candidate count per group is three, so enumeration is small. For each budget we save the largest cycle rank and a witness set of pair IDs. A dynamic program combines the group solutions and gives the exact optimum for each total budget. The objective is the number of independent residual constraints. It does not optimize prediction error, measurement precision, donor coverage, or recovery cost. Each successful estimate has unit cost.

We also calculate the exact mean cycle rank for uniform random selection of K missing estimates without replacement. For a specified subset of k useful edges among m useful edges in one group, the probability is `choose(N-m,K-k)/choose(N,K)`, where N is the total missing count for that sample. Summing cycle rank times this probability over subsets and groups gives the reference mean. This is a selection reference, not a model of laboratory success.

## Results

| Sample and labels | All connections | Missing delays | Current constraints | Full constraints | Missing edges needed for full constraints | Current edges on cycles | Full edges on cycles |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Mouse, primary | 2783 | 535 | 18 | 34 | 20 | 57 | 111 |
| Mouse, strict | 2783 | 535 | 11 | 22 | 15 | 39 | 79 |
| Human, primary | 394 | 85 | 1 | 1 | 0 | 4 | 4 |
| Human, strict | 394 | 85 | 1 | 1 | 0 | 4 | 4 |

In primary mouse groups, a selected budget of 12 estimates can raise the constraint count to 30. A budget of 20 reaches 34. Uniform random selection of 12 or 20 missing estimates gives mean counts of 18.2710 or 18.4539. The selected 20 are 3.74% of all 535 missing estimates. This contrast is conditional on equal cost and successful recovery of the selected estimates.

Current mouse cycles occur in 10 groups; the full graph has cycles in 21 groups. Recovering all missing values raises the number of available, already measured mouse edges on cycles from 57 to 91. The other 20 edges on full cycles are the selected missing ones. Full support is only 111/2783 = 3.99% of all confirmed mouse connections. The strict-label bound is 79/2783 = 2.84%. In human TCx, support remains 4/394 = 1.02%. Thus missing estimates explain part of the mouse limit, but they do not remove the broad graph-sampling limit.

The full graph has more groups than the available graph because some groups have no measured delays. This does not change the count of constraints. Counts are exact for these records and groups. We give no confidence intervals because no population sampling claim is made. Mouse versus human also changes brain region and sampling design; it is not a species effect estimate.

## Checks, limits, and use

An independent checker uses numerical matrix rank, rather than graph traversal, to check cycle rank and edge support for all 4,364 primary and strict groups, both full and current. It also checks all saved global witness plans. All checks passed. Exhaustive tests cover 511 nonempty 3-by-3 bipartite graphs and 729 absent/available/missing states of a 2-by-3 graph. They verify that bridge pruning preserves the optimum at every budget. The observed current counts agree with the prior publication.

The plans identify where a trace review could help. They do not show that usable raw traces exist, that a missing estimate can be recovered, or that all successful estimates have equal precision. Fit failure may be systematic. Connection calls and class labels can be wrong. New calls or revised labels can change the bounds. Our strict-label test changes matching assumptions, not those underlying records. Unobserved anatomical connections are outside the bound.

Each independent cycle is one algebraic constraint, not an independent biological replicate. Shared cells and recordings can cause correlated error. A constraint need not have useful statistical power. New measurements can also improve noise estimates or model fitting even if they add no cycle. The null result for human graph support does not mean that recovering those measurements has no scientific value.

These bounds apply to unrestricted fixed source-plus-target effects within the stated groups. Regularized models, pooled class models, or mechanistic constraints can predict on forests under additional assumptions. This study does not test those models or claim a new law of neuronal computation. It provides a method and a small list of candidate records for a better test of a circuit timing hypothesis. It establishes no intact-brain, behavioral, or cross-species timing principle.

## Reproduction and job record

See [reproduction instructions](files/REPRODUCE.md). The package includes source code, the exact SQL query and source hash, selected edge records, all group audits, per-group and global optimum witnesses, exact random reference values, an independent checker, and the figure. Core graph analysis uses only Python standard libraries. Numerical checks use NumPy; plotting uses Matplotlib. All substantial runs used `campaign-compute` with library threads set to one.

Job: `sci-1107-dell-neural-structure-and-computation-48b5975e172c`.
Topic: `neural-structure-and-computation`. Campaign: `11_07_2026`.
Machine: `dell`. Account: `codex-andrii`.
Model: `gpt-6.1-sol`, high reasoning effort, Codex harness in T3 Code.
No agents were launched. No remote SCI archive or index was used. The campaign-machine signing key is not a personal authorship claim. Credit the Allen Institute for Brain Science and Campagnola, Seeman and colleagues for source data.
