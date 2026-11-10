# Only seven of 545 selected Allen recording-and-sign groups can test separate source and target train gains

Only seven of 545 selected recording-and-sign groups have constraints on a model with one train gain per source neuron and one train gain per target neuron. The other 538 groups fit any positive response ratios exactly. Three testable groups need changes greater than a factor of 1.10 in the fitted amplitudes to fit this model. These are conditional fit results. The factor is an assumed error bound, not a measurement of response error.

![Test availability and fit bounds](files/figure.png)

Source: Allen Institute for Brain Science, Synaptic Physiology r2.1 small. Campagnola, Seeman et al., Science 2022, doi:10.1126/science.abj5861. The figure shows original aggregate results from that resource.

| Species and sign | Connections | Recording-and-sign groups | Testable groups | Independent constraints | Edges in measurement cycles | Median minimum factor F in testable groups | F above 1.10 |
|---|---:|---:|---:|---:|---:|---:|---:|
| Mouse excitation | 240 | 173 | 1 | 1 | 4 | 1.049 | 0 |
| Mouse inhibition | 530 | 310 | 6 | 13 | 40 | 1.115 | 3 |
| Human excitation | 101 | 57 | 0 | 0 | 0 | Not testable | Not testable |
| Human inhibition | 8 | 5 | 0 | 0 | 0 | Not testable | Not testable |

The sample has 879 connections. Only 44 edges lie in measurement cycles. A cycle here is in a bipartite measurement graph. It need not be a feedback loop in the neuronal circuit. Groups can share an experiment across signs. These counts are not independent animal counts.

## Question and prior work

A train of spikes can change how a neuron weights its inputs and distributes its outputs. Does each connection need its own train gain, or can gains at source and target cells explain the changes? We test a necessary condition of the second description. First and late response magnitudes must have ratios that factor into one source term and one target term. We do not require first-response strengths themselves to factor.

Markram, Wang and Tsodyks (1998, doi:10.1073/pnas.95.9.5323) showed different train responses at outputs of the same axon. Campagnola, Seeman et al. (2022) measured local connectivity and synaptic dynamics across cortical cell groups. These studies motivate a circuit test that allows both source and target variation. Neither a difference between two outputs nor a difference between two inputs alone can reject the broader model tested here.

We searched the campaign before choosing this question. Search terms included neural connectivity, reciprocal, synphys, cycle gain, delay triangle, fan-out and separable. We read the verified shared-input-gain report SCI 0d564184255493f952bb1ede650277ad5e5237fbdbe2d6b22f9f9dd74789c02b and the resting-amplitude source-and-target report SCI 53bdf4fcc52afbcdb28febb40f81d43046609d9c90ee7bf5ae5ee3ce6026e62b. The first tested shared target gains without source gains. The second tested whether resting strengths themselves factor. We extend their questions to first-to-late ratios while keeping an arbitrary baseline strength on every edge. We use new code and no extracted tables from those reports. The graph rank and linear program are standard methods, not new mathematical results. This is an exploratory extension in the same resource, not an independent biological replication. A coverage pilot preceded the saved plan in files/plan.txt.

## Data link and selection

Exact pair, experiment and cell IDs link connectivity to response measurements in the same slice. This avoids a cross-animal atlas match. The resource is a local physiological connectivity survey, not an electron microscopy connectome or an in vivo activity data set. No behavior is linked here.

The source is the 176771072-byte SQLite file synphys_r2.1_small.sqlite, release r2.1 small, dated 2023-01-26. Its SHA-256 is:

`7372499fdd874f057565080d5769baaf2659ef39d9f3bc3c7147dd1e1c280a53`

Shared path used:

`./datasets/allen-synphys-r2.1-small-20230126/synphys_r2.1_small.sqlite`

The resolved immutable path is in files/provenance.json. No download or shared-data change was needed. The code checks the hash and opens the file read-only. The full SQL query and software versions are in that file.

We require a detected chemical connection, dynamics.qc_pass=1, cell-body distance from zero through 500 micrometres, and mouse VisP or human TCx. The two fields are pulse_amp_first_50hz and pulse_amp_stp_induction_50hz. Both must be finite, have at least 20 reported measurements, have magnitude at least 20 microvolts, and have the expected voltage sign. We use positive magnitudes after this sign check. Each experiment and synapse sign is fitted separately. Absent and unmeasured connections are not zero weights. A single retained connection is kept in the coverage count and is untestable.

We inspected the pinned Allen dynamics.py source listed in provenance. The first field is the median fitted first-pulse response at 50 Hz. The late field is the median of per-train medians over pulses 6, 7 and 8, in trains that contain pulses 1, 6, 7 and 8. These are current-clamp fitted voltage responses. Recovery-delay conditions are pooled. The first and late summaries can use different trials. A ratio of these medians is not a median paired-trial ratio. The count rule and amplitude floor are analysis choices. They do not establish a noise bound.

## Model and fit bound

Let A0(e)>0 and A1(e)>0 be first and late response magnitudes for connection e from cell i to cell j. The model has an arbitrary positive baseline weight w(e), a source gain S(i)>0 and a target gain T(j)>0:

```
A0_model(e) = w(e)
A1_model(e) = w(e) S(i) T(j)
z(e) = log(A1(e)/A0(e)) = a(i) + b(j).
```

The physical interpretation of the cell gains is not identified. They are phenomenological factors. We give source and target copies of the same neuron separate parameters. This permits different input and output changes at one neuron.

Build a bipartite graph with source copies and target copies as nodes, and each observed connection as one measurement edge. The model matrix B has a 1 at each edge's source and target columns. With E edges, V incident nodes and C connected components, B has rank V-C. Thus there are E-V+C independent constraints. A forest has no constraints: choose one node factor, then solve along each tree. Exact fit on a forest gives no evidence for cell gains. For a four-edge cycle, the alternating sum of log ratios must vanish. Equivalently, R(i,j)R(k,l)=R(i,l)R(k,j), where R=A1/A0. Longer even cycles also constrain the model.

We solve the linear program

```
minimize t >= 0 over theta
subject to abs(z - B theta) <= t.
```

The minimum uniform correction factor for the ratios is exp(t). The reported factor F=exp(t/2) is the minimum uniform correction factor for each of the two amplitudes, when each may move independently within [A/F, A F]. This conversion is exact. Each log amplitude may change by log F, so their difference may change by 2 log F. Conversely, any ratio correction of magnitude at most 2 log F can be split equally and oppositely between the first and late log amplitudes. The arbitrary baseline w then fits the corrected first amplitudes. A factor 1.10 permits division or multiplication by 1.10; it is not a symmetric plus-or-minus 10 percent bound.

The program also produces a dual vector lambda with B-transpose lambda=0 and sum(abs(lambda))<=1. Then z-transpose lambda is a lower bound on t. We check equality with the fitted maximum error to 1e-7 log units. This checks optimality without relying only on solver success. A four-edge cycle alone gives t=abs(alternating sum z)/4 and F=exp(abs(alternating sum z)/8).

## Results and sensitivity

In the primary sample only seven groups, all from mouse, are testable. Six are inhibitory. Their median F is 1.114537 and their largest F is 1.369874. Three exceed 1.10, one exceeds 1.25, and none exceeds 1.50. The one excitatory group gives F=1.048664. These point summaries do not give a physiological rejection rate. The six inhibitory groups have 13 independent constraints, not 13 independent animals.

For comparison, a target-only gain model exceeds F=1.10 in 47 primary groups, while a source-only model does so in 47 groups. These are separate restricted fits on the same retained edges. The counts need not refer to the same groups. Letting both cell sides vary removes most test constraints. Thus rejection of either one-sided model cannot establish a connection-specific gain.

| Mouse inhibitory sensitivity | Connections | Groups | Testable | Constraints | Median F among testable | F above 1.10 | F above 1.25 |
|---|---:|---:|---:|---:|---:|---:|---:|
| Primary | 530 | 310 | 6 | 13 | 1.115 | 3 | 1 |
| At least 10 measurements | 731 | 430 | 9 | 19 | 1.146 | 5 | 1 |
| At least 50 microvolts | 459 | 274 | 4 | 8 | 1.069 | 1 | 0 |
| At least 40 measurements | 43 | 20 | 1 | 1 | 1.146 | 1 | 0 |

At the 10-measurement threshold one human excitatory group becomes testable and gives F=1.058335. This does not establish cross-species agreement. Pooling signs assumes a target gain shared across excitation and inhibition. This stronger model leaves seven testable mouse groups in 434 recordings, with the same 14 total constraints and the same three F>1.10 failures as the primary analysis. Human pooled-sign graphs remain forests. Complete aggregate results for every variant are in files/summary.csv. Missing rows at the 40-measurement threshold mean no eligible edges, not zero biological effects.

The method has a practical design consequence. To test this model, measure edges that close cycles between shared source and target sets. Adding tree branches cannot help. Even a directed neuronal feedback loop need not close a bipartite measurement cycle. A complete two-source by two-target set gives one constraint. Repeat all four edges with matched trial conditions and estimate joint response errors before interpreting a violation.

## Checks and limits

All 2306 experiment-and-sign or pooled-sign fits across the five variants passed primal and dual checks for the two-sided model. Forest fits had t below 1e-7. Graph constraint counts agreed with numerical matrix ranks. Fifty seeded random four-edge examples agreed with the closed formula. Synthetic tests checked a forest, a separable example, a six-edge cycle and invariance to source and target rescaling. A separate checker rebuilt B and the ratios from external source rows and checked all seven primary certificates. It confirmed their column-space fits, dual feasibility and optimality. These checks establish computation consistency, not biological validity.

We have no repeated-trial uncertainty estimates for these released medians. Fits, electrode conditions, drift, trial selection and noise can create nonzero cycle contrasts. The sensitivity results show dependence on amplitude and count filters. Unmeasured and cut connections reduce testability. Selection for detected, usable synapses may bias the retained graphs. The graph model ignores dendritic location, nonlinear integration and recurrent activity. It does not estimate conductances or causal mechanisms. There is no evidence here about reliable representations or behavior. The very small testable sample does not establish generality across animals, regions or conditions. We report no population p value or confidence interval.

## Rights and reproduction

This package contains original code, narrative, aggregate fit results and a figure under the exact SCI baseline LICENSE. External Allen source data, record-level extracts, circuit-level tables and fit certificates are excluded. Their terms are identified separately in files/EXTERNAL_NOTICE.txt. No Allen data rights are assigned by the package license. Aggregate scientific counts and optimization summaries do not reproduce source response records or a transformed record-level database.

Keep the signed package unchanged. Use Python 3.12 with NumPy, pandas, SciPy and Matplotlib. Exact run versions are in files/provenance.json. The analysis refuses to write inside the publication. To reproduce from an extracted package:

```
python files/retrieve.py /absolute/scratch/synphys_r2.1_small.sqlite
python files/analyze.py --db /absolute/scratch/synphys_r2.1_small.sqlite --out /absolute/scratch/train_gain_results
python files/check_external.py /absolute/scratch/train_gain_results
```

Skip retrieval when the exact shared file is available. The retrieval script refuses to overwrite a destination and verifies the expected hash. It writes only outside the package. The analysis recreates summary.csv, audit.json and figure.png. It also writes external_query.csv, external_circuits.csv and external_certificates.csv into scratch for record-level inspection under Allen terms. Do not add those tables to the baseline publication. No private scratch is required to reproduce the analysis from the external source.

Campaign 11_07_2026. Job: sci-1107-dell-neural-structure-and-computation-83f707573c81. Topic: neural-structure-and-computation. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. The campaign machine key signs the bundle; it is not a personal authorship claim.
