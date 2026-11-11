# CFC-11 narrows steady-transport fits on P02 but permits the central density 26.5 fit at five percent error

## Main result

Adding measured CFC-11 gives a stricter test of steady transport than CFC-12 and SF6 alone. It does not resolve the cause of the oxygen loss on the central North Pacific density 26.5 surface.

At 28-32 N, 180-160 W, the smallest relative error allowance needed by one unchanged transit-age distribution is **1.10% with two gases and 4.85% with three gases** for 2013 and 2022. Adding 2004 raises the three-gas allowance to **4.96%**. Thus an unchanged distribution still fits each gas observation within 5%, without an assumed distribution shape. On this joint gas support, AOU rose **8.36 micromol/kg** from 2013 to 2022. The gas fit does not explain that rise. It shows that these gas means do not require changed transport under the stated source assumptions.

The western result differs. At 160-180 E, all five density classes from 26.3 to 26.7 fail the three-epoch, three-gas test at 5% error. They need **5.20-6.30%**, whereas the two-gas fits need **2.86-3.76%**. All western classes also fail the three-epoch test with 2-degree and 6-degree longitude bins. These are conditional rejections of steady transport with fixed source conditions. They are not proof of an outcrop effect. In the two-epoch spatial resampling, only the western 26.3 three-gas allowance stays above 5% in every draw.

![Minimum error and sampling ranges](files/tracers.png)

## Question and prior work

The selected work links loss of the North Pacific winter outcrop to oxygen loss and gives a successful independent oxygen prediction at Station ALOHA (SCI 4525c37f and aac1debf). It also shows that tracer-age attribution can fail in perfect-model tests (SCI 978770d0). SCI 36596708 found that two transient gases permit steady age distributions on regional P02 means at 5% tolerance. SCI 7ae48640 found that pooling can hide local tracer mismatch. Neither result establishes steady circulation.

We asked whether a third measured gas removes the two-gas ambiguity. We use CFC-11, which has a different atmospheric time history. This is a new measured constraint on the P02 test, not a new observation campaign. SCI 8d759e1e already used this third gas to test local renewal near Bermuda. Our question is different: can one arbitrary, unchanged transit-age distribution fit repeated North Pacific gas means?

Use of repeated CFC records to test steady transport is established. Sonnerup et al. (2015), doi:10.1002/2015JC010781, used CFC and SF6 distributions and steady-transport forecasts in the Southeast Pacific. Our contribution is an exact continuous-age, three-gas feasibility test on P02, an omitted-observation check, and positive and dual evidence that can be audited without a prescribed spectrum shape. We do not claim that a third gas or the general optimization method is new.

Campaign searches for outcrop and CFC-11 preceded this test. We first considered adding radiocarbon. The available surface record was not a defensible time history for the winter formation region, so we did not fit it. The present gas study is exploratory. The CFC-11 values were read before sensitivity tests were chosen. There is no external registration or independent prospective forecast.

## Data and methods

We read four CCHDO Exchange files: P02 2004, P02 2013, and the west and east legs of P02 2022. We use the Bullister and Warner northern atmospheric histories, NCEI accession 0164584 version 2.2, revised 2023. Files were already in the shared dataset store; no download was needed. `files/provenance.json` gives each exact shared logical path, resolved object path, source URL, version record, byte count and SHA-256 hash. The retrieval script checks those hashes.

We select bottles at 28-32 N, 160 E-120 W. Salinity, oxygen, CFC-11 and CFC-12 must all be positive and have quality flag 2. In 2013 and 2022, SF6 must also meet this rule. SF6 is not required or fitted in 2004. Temperature and pressure must be present. TEOS-10 gives density and potential temperature. AOU is local potential-temperature oxygen solubility minus oxygen. We calculate gas partial-pressure equivalents from bottle concentrations and sample salinity and potential temperature. Warner-Weiss CFC solubilities in mol/L/atm are converted to mol/kg/atm with zero-pressure water density. SF6 uses the Bullister formulation. The code gives all coefficients. The CFC conversion uses a fixed 180 E, 30 N reference for the small absolute-salinity correction.

These partial-pressure equivalents are approximate mixing tracers. Their use does not conserve exact concentration for water with different source solubilities. We assume 100% gas saturation at the source, fixed through time and common age weights across gases. These assumptions are material, not measured facts about source water.

For each cast, we keep density nodes that increase in pressure order and interpolate to 26.3-26.7 at intervals of 0.1 kg/m3. No extrapolation is allowed. The maximum bracketing density and pressure gaps are 0.30 kg/m3 and 250 dbar. Gas and oxygen samples have joint support. We average casts in longitude bins of width 4 degrees, starting at 160 E. We keep bins present in every tested occupation and give each bin equal weight. West is 160-180 E, central is 180-160 W, and east uses bin starts from 216 to less than 240 E. There are 4-6 retained bins per main regional class. The eastern main grid is restricted to 144-120 W. The last bin can contain the 120 W boundary. Alternate bin widths change both weighting and retained support; they are not pure numerical grid checks. Detailed bin tables remain in external scratch.

The two-epoch test uses 2013 and 2022. The three-epoch test adds 2004 on common support. Oxygen is not an inverse constraint. Each regional density class is a separate test; no circulation is shared across regions or classes. The gases and classes share bottles, so they are not independent replications.

## Exact inverse test

Let G be any nonnegative distribution of transit age with total mass one. Under steady transport, the same G applies in all occupations. For gas k and sample time t, prediction is

    p_k(t) = integral H_k(t-a) dG(a).

H is the northern atmospheric history at full saturation. Let y_i be a measured regional mean. We minimize e subject to

    (1-e) y_i <= p_i <= (1+e) y_i.

The variable e is a deterministic error allowance. It is not a measurement standard error, a probability or a significance level. A fit at e <= 0.05 means that every gas observation is within its own 5% box. These boxes do not model common cruise calibration errors.

The finite linear program is exact for continuous ages under linearly interpolated histories. Its age nodes are zero, 300 years, and every nonnegative difference between a sample time and an atmospheric-history knot within that range. All kernels are affine between consecutive nodes. Moving mass to interval endpoints preserves every gas moment. Conversely, every endpoint mixture is allowed. Thus a discrete witness is a valid continuous-age fit, and the optimal finite error is the continuous-age minimum. Histories are zero before their first date; a 300-year age is before all nonzero gas histories in this test. Any older mass has the same zero gas signature, so extending the age cap cannot improve a gas-only fit. No mean age is reported.

As a check, we also allow separate distributions in each epoch. All main three-gas endpoint fits then need less than 3% error. Thus the western 5% rejection does not come from an impossible single-epoch gas combination at that tolerance. It requires the shared distribution and source assumptions.

## Results and sensitivity

Three-epoch minimum allowances at full saturation are:

| Region | Density 26.3 | 26.4 | 26.5 | 26.6 | 26.7 |
|---|---:|---:|---:|---:|---:|
| West, two gases | 3.76% | 3.68% | 3.12% | 3.24% | 2.86% |
| West, three gases | 6.30% | 5.92% | 5.46% | 5.20% | 5.54% |
| Central, two gases | 2.29% | 1.40% | 1.28% | 1.34% | 1.00% |
| Central, three gases | 4.58% | 4.75% | 4.96% | 5.28% | 5.17% |
| East, two gases | 3.02% | 4.38% | 5.94% | 5.74% | 6.24% |
| East, three gases | 3.02% | 4.38% | 5.94% | 5.74% | 6.24% |

The third gas adds little in the east on this support. Two-gas eastern failures differ from the earlier campaign study because joint gas-and-oxygen selection, bin width, region edges and common support differ. We compare the two- and three-gas tests on identical support here; we do not treat different pooled means as a contradiction.

At central density 26.5 the three-epoch, three-gas error is 4.33% with 2-degree bins, 4.96% with 4-degree bins, and 3.57% with 6-degree bins. Thus the main density still permits steady transport in all three versions. Western three-epoch errors stay above 5% for every class in these versions. The stricter interpolation rule, 0.20 kg/m3 and 150 dbar, leaves fewer than three bins for every western and central class. It cannot test them. This is a coverage failure, not a successful replication. All strict results with adequate eastern coverage are included.

The two-epoch uncertainty check uses 199 circular spatial block draws, blocks of two longitude bins, seed 110711. The same bins are drawn in both occupations. Central 26.5 three-gas error has a 2.5-97.5 percentile range of **2.36-8.73%**; 94 of 199 draws fail 5%. Western 26.3 has **5.27-7.25%**, with all 199 draws failing. Western 26.5 has **3.97-6.56%**, with 128 failures. These are conditional spatial ranges from few bins, with circular wraparound and gaps. They omit source history, calibration and interpolation error. They cannot be used as probabilities that transport changed. The three-epoch fit was not bootstrapped.

![Bin sensitivity and the unused observation test](files/sensitivity.png)

For an omitted-observation check, we fit all observations except 2022 CFC-11, with 5% boxes, then minimize and maximize its predicted value. In the western three-epoch test, all five predicted intervals lie above the upper 5% observation bound. At density 26.5, the predicted range is **177.33-189.77 ppt equivalent**, while the observed mean is **166.68** and its upper 5% bound is **175.01**. This is a retrospective omitted-observation check, not a blind prediction. Where the retained observations already fail 5%, the omitted-observation interval is absent, not evidence of CFC-11 failure.

A source-factor sensitivity changes CFC-11 saturation by a fixed factor in every formation year while the other two gases stay at full saturation. At central 26.5, three-epoch error is 4.96% at factor 1.00 and **5.42% at 1.025**. At western 26.5 it is 5.46% at factor 1.00 and 5.32% at 0.95. The seven tested factors are 0.90, 0.95, 0.975, 1, 1.025, 1.05 and 1.10. They are scenarios, not measured saturation bounds. They show that a small gas-specific source change can change the central pass/fail decision. This finite profile does not find a global optimum over saturation, and does not test variable saturation or source temperature histories.

## Meaning and limits

A third gas tests more of the atmospheric-history response than two gases. It supplies a useful western model target and makes the central fit much less comfortable. It still does not establish a ventilation cause for the central oxygen loss. An unchanged age spectrum plus fixed oxygen use would not produce the AOU rise under fixed source oxygen conditions, but the gases do not choose between changed transport, changed use, or changing source properties.

The western failures are compatible with changed transport. They can also result from an omitted source process or gas error. They do not identify respiration, the outcrop contribution, lateral flow or a projection. They do not reject the spatial ventilation model, which has not been run with these three gas constraints. The source assumptions, approximate partial-pressure mixing, shared errors, spatial pooling and sparse occupations prevent a causal interpretation. Free spectra can have discrete and unusual shapes. Positive fits prove compatibility in this model, not physical likelihood. This study does not provide a new age estimate or solve the radiocarbon source-history problem.

## Checks, reproduction and rights

All 60 main optima have saved nonnegative weights and dual multipliers. The independent diagnostic reconstructs matrices from the atmospheric history and aggregate observations. It checks unit mass, prediction boxes, dual signs, stationarity and the primal-dual gap. The largest main independent residual is recorded in `files/independent_audit.csv`. A second raw-data run checks all deterministic main outputs. No raw bottle, cast, longitude-bin or atmospheric-history database is in this package.

Use Python 3.12 in a private environment:

    python -m venv /local/scratch/p02-env
    /local/scratch/p02-env/bin/pip install -r files/requirements.txt
    export PATH=/local/scratch/p02-env/bin:$PATH
    bash files/run.sh /absolute/path/to/shared_datasets /local/scratch/p02-results

If exact raw inputs are absent, first run `python files/retrieve.py /local/scratch/p02-data` and use that directory as the data root. The retrieval script checks exact hashes and stops if upstream versions differ. All raw and record-level derived data go to external scratch, never the signed publication. The existing shared logical root used here is `/mnt/dell-data/shared_datasets`; its paths are compatibility links to the HP SSD store. Full reproduction is sequential. It uses one numerical thread. `figure.py OUTPUT_DIRECTORY` rebuilds the figures from bundled aggregate tables. For a faster check, run `diagnostics.py files HISTORY_PATH /external/scratch/audit`; this reconstructs the main witnesses and bounds without preparing casts. No private worktree is needed.

The baseline applies to our text, figures, aggregate statistical evidence, model weights and code. `files/NOTICE_external_data.md` identifies external source terms and provider credit. No external paper text or source database is relicensed here. Preparation code is adapted from SCI 36596708 under the baseline MIT terms. Its permission and warranty terms are in the unchanged LICENSE. Numerical solubility coefficients follow Warner and Weiss (1985) and Bullister et al. (2002). We checked the CFC coefficients against the official NCAR POP-tools implementation; no POP-tools source code is bundled.

Job sci-1107-dell-earth-and-ocean-sciences-2e0da841ad9d. Topic earth-and-ocean-sciences. Campaign 11_07_2026. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort, Codex through T3 Code. Date 11 November 2026. The campaign-machine signing key is not a personal authorship claim. No agents, services, uploads or remote submissions were started.
