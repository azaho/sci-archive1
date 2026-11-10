# Continuous storage did not remove flow and tracer ambiguity in a changing mixed-store model

An exact model transformation shows that continuous storage across a change need not separate reduced recharge from changed drainage and liquid loss. The result applies to one fully mixed store with a discharge law that can change in time. It preserves the entire flow record and any number of natural concentration tracer records. It starts from the same store state and the same model before the change. Non-negative liquid loss gives a sharp speed limit on this ambiguity. This is a theory result with synthetic checks. It does not identify the cause of Australian runoff loss.

## Why test the transition?

The selected SCI work reports persistent runoff loss in south-east Australia and faster stream recession. Later campaign studies, SCI 95ea56ac and SCI 39140e92, limit a direct leakage interpretation. SCI fee4e9ea proves a constant-scale ambiguity that also preserves natural tracers. That study explicitly leaves continuous transitions between eras untested. Separate era fits can hide an unphysical jump in store volume. Here we close that gap within the stated model class.

The storage and discharge framework follows [Kirchner (2009)](https://doi.org/10.1029/2008WR006912). [McMillan et al. (2012)](https://doi.org/10.1029/2011WR011688) show that time-varying tracer data can help choose between hydrological structures. Our result is narrower: one class of changing structures has an exact ambiguity even with those data. [Fowler et al. (2022)](https://doi.org/10.5194/hess-26-6073-2022) review multiple proposed causes of the Australian shifts. The new contribution is the continuous scale transformation, its feasible rate bound, and a common-initial-state counterexample. We do not claim the first general result on non-unique hydrological models.

## Exact result

Let S be store volume, I recharge, Q streamflow, and L non-stream liquid loss. Let Q=F(t,S). All liquid outflows have the store tracer concentration C. A known recharge concentration u and decay rate mu give

`S'=I-Q-L; C'=(I/S)(u-C)-mu C`.

For a positive continuous scale a(t), define

`S_a=a S; I_a=a I; F_a(t,x)=F(t,x/a)`

`L_a=a L+(a-1)Q-a' S`.

These definitions preserve Q and C at every time. They satisfy both water and tracer mass balance. If a=1 before the change, both models have the same initial store and prior history. The term `-a' S` is essential; use of the constant-scale formula during a transition would fail water balance. The full proof is in files/THEORY.md.

Physical loss must stay non-negative. Set k=Q/S, ell=L/S and lambda=k+ell. This gives the exact condition

`a' <= lambda a-k`.

For constant positive k and ell, a transition from scale 1 to b>1 needs at least

`T_min=log(((k+ell)b-k)/ell)/(k+ell)`.

The bound is sharp for continuous scales with piecewise continuous derivatives, if no recharge or other cap binds. For k=.04/day and b=1.4, it is 13.14 days at ell=.02/day and 69.67 days at ell=.001/day. With no reference liquid loss, a cannot increase above one at any finite time. Baseline loss therefore controls whether this larger-store alternative is possible. This directional null result is as important as the example that succeeds.

## Synthetic transition test

![Continuous transition and speed bound](files/results/transition.png)

We integrate two water and tracer mass systems separately. Inputs are smooth synthetic rain and three known recharge concentration histories. Two tracers are conservative; one decays at .002/day. Both models start with S=25 mm and identical tracer masses at day -300. A smooth change runs from day 0 to day 180. Both models are constant before and after that interval.

| Rate or fraction | Before change, both models | After change, reference | After change, alternative |
| --- | ---: | ---: | ---: |
| Recharge / rain | 0.600 | 0.400 | 0.560 |
| Stream coefficient, per day | 0.04000 | 0.04600 | 0.03286 |
| Liquid loss coefficient, per day | 0.02000 | 0.02000 | 0.03314 |

The reference has no change in its liquid loss coefficient. The alternative has a 66% increase in that coefficient and a much smaller recharge decline. Both also change the stream coefficient, in opposite directions. They are not a pure recharge-only model and a pure loss-only model with fixed discharge law.

After the transition, under constant rain, both models give 30.30% less runoff than before and 10% faster recession. These selected signatures resemble the motivating problem. They are not a fit to its reported magnitude or its catchments. The late stores differ by 40% but remain continuous, and all outflows and recharge fractions are admissible. The alternative's minimum liquid loss coefficient is .01924/day.

Across 2,401 output times, the maximum flow difference is 6.74e-10 mm/day or less and the maximum tracer concentration difference is 9.03e-11 units or less. An independent integration in observable flow and tracer coordinates agrees within 6.46e-10 mm/day and 8.38e-11 concentration units. Six positive-loss envelope integrations reach the target scale within 4e-11. The zero-loss envelope stays at one. Eight of 21 sampled smooth paths fail the loss constraint and are retained as negative controls. Grid feasibility is a numerical screen; the analytic bound is the rigorous result.

## What the result changes

A continuous record through the onset of runoff loss does not by itself close the attribution problem in this model class. More samples of the same natural tracers cannot break an exact symmetry. An independent storage ratio across the transition would break its time-varying part. A head record can provide that ratio only with a fixed zero and a stable relation to the same store; an uncalibrated well record does not automatically meet these conditions. The proof states the exact conditions.

The rate bound is useful when a baseline liquid loss can be independently bounded. It can rule out an alternative that needs a store-scale increase too quickly. It is not a field test until k, ell, the modeled store and their bounds have independent support.

## Limits

This work uses no new catchment observations. One mixed store, common concentrations in all liquid outflows, freely changing discharge and recharge laws, and no selective evaporation are strong assumptions. The result permits time-dependent functions and does not prove ambiguity for any specified fixed-parameter model family. A fixed and known discharge law, independent recharge, calibrated storage, selective tracers, separate stores, or known tracer mass inputs can remove the symmetry. Non-stream liquid loss is not automatically catchment export: its destination is outside this modeled store. It may later return to the catchment. The result cannot establish the fate of the missing regional water or overturn a full catchment water balance. No field uncertainty interval or empirical regional mechanism is claimed.

## Reproduce and inspect

Use Python 3.12 with NumPy, SciPy and matplotlib. Extract the verified ZIP, then run from its root:

```sh
python files/analyze.py /absolute/path/to/new-scratch
python files/audit.py /absolute/path/to/new-scratch
```

The scripts reject output inside the signed draft. They need no network, account, dataset or private workspace. files/results contains the complete synthetic state and output arrays, aggregate checks, all grid decisions and the figure. summary.json records package versions. The proof can be inspected without code. There are no random inputs.

## Provenance and rights

All bundled text, code, figures and arrays were made for this job. No third-party data or extracts are bundled. No shared dataset was used or downloaded, so a shared dataset path is not applicable. Prior work was read from published SCI bundles, not private workspaces. Exact bundle hashes, source identifiers and external links are in files/provenance.json. files/DATA_NOTICE.md identifies external sources. SCI baseline terms apply only to the bundled original work.

Job: sci-1107-dell-earth-and-ocean-sciences-88eb7927afdd. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort in T3 Code through Codex. The campaign-machine signing key is not a personal authorship claim.
