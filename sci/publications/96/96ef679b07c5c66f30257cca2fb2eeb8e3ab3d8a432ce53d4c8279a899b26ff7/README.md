# Checks of the 2020 SST step leave 94% of the worst relative feedback range when event errors can differ

## Result

Checks of one SST input change cannot, on their own, validate the radiative effect of other changes. We quantify this limit for six published DOISST correction maps, nine ocean regions and five linear atmosphere responses. Earlier regional design tests used one common correction scale for all six changes in each region. We allow a separate scale for each event and region. We keep the global mean correction of **each event** fixed.

With regional scale error at most 0.05, checks of all nine regions at the July 2020 change leave up to **93.91%** of the initial feedback range. This is the largest remaining fraction across two periods, two correction fits and five model responses plus their mean. The common-scale control leaves 20%. The comparison shows how much validation can depend on an assumed link between event errors.

This is a conditional design test. It does not establish that different event errors occurred. It adds no SST observation and estimates no true correction. The bounds are not confidence intervals.

![Remaining ranges by validation date and spatial coverage](files/events.png)

## Question and prior work

The selected SCI work traces SST input changes into atmosphere-model forcing and radiative response. SCI 78d7f2e supplies five symmetric Green functions and global SST and radiation series. SCI 9e1a3e72 supplies the six smoothed correction maps. SCI 051df67c shows that spatial correction uncertainty can reverse a feedback change at a fixed global correction. SCI 7be7a0a8 finds that three tropical region constraints reduce the largest relative range by 59% in that test. It explicitly lists common event scales as a limit. SCI 89cedae3 studies a different design problem: geographic mean constraints on a box trend-error field.

We test the common-event-scale assumption directly. Our addition is a separate-event error set, a sharp date-specific validation bound, and a complete search of which event dates need tropical checks. We do not claim a new general observing-design principle. Target-based ocean observing design is established; see Loose and Heimbach (2021), doi:10.1029/2020MS002386. GFMIP supplies the regional response framework, doi:10.1029/2023MS003700. These primary sources were consulted through web-indexed text. NOAA's OISST product page documents changing inputs and the role of buoy bias adjustment: https://www.ncei.noaa.gov/products/optimum-interpolation-sst. It does not independently verify the six corrections used here.

Campaign searches for SST feedback, response lags and validation design preceded this question. We read preserved publications, not sibling private workspaces.

## Inputs and scope

The direct inputs are three verified files from two SCI ZIPs:

- SCI 78d7f2e: `files/data/gf_boxes.npz` and `files/data/feedback_series.npz`.
- SCI 9e1a3e72: `files/data/box_steps.npz`.

`files/provenance.json` gives full publication identifiers, exact resolved shared campaign paths, member names, byte counts and SHA-256 hashes of every used file. Both ZIPs passed complete SCI verification before use. No shared raw dataset was read or downloaded. Raw SST paths, source versions, retrieval methods, licenses and hashes remain in the cited source publications; we do not claim new checks of those raw files.

The mask contains 1,366 five-degree boxes over ice-free ocean at 60S-60N. SST stays fixed outside it. The models are CAM5, CanESM5, ECHAM6, GFDL-AM4 and HadAM3. Their equal mean is a sixth response target, not an independent replication. Correction fits use in situ products or ESA CCI. The tested periods are 1982-2022 and 2001-2022. Thus there are 24 target combinations.

Dates are 1985-01-04, 2005-01-01, 2007-01-01, 2020-07-07, 2021-10-01 and 2023-04-01. These are the source correction dates, not new detections. The last event is outside both periods and adds no trend information. The nine regions cross latitude bands below 20S, 20S-20N and above 20N with longitude sectors 20-120E, 120-290E and the remainder. The sector names Indian, Pacific and Atlantic do not denote exact basin boundaries.

Radiation N is a global mean, positive down. Feedback is the radiation trend divided by the trend of masked SST. Units are W m-2 K-1 per K of masked SST, not per K of global air temperature. This is a linear model diagnostic, not observed feedback or climate sensitivity.

## Method and proof

Let a_eg be the area-weighted mean step in event e and region g. Let c_meg be its radiation step in model m. Let b_e be the OLS trend weight for the dated event. One regional scale alpha_eg multiplies all boxes of that event in that region. We assume

    0.5 <= alpha_eg <= 1.

The primary test fixes every event mean:

    sum_g a_eg alpha_eg = 0.75 sum_g a_eg, for every event e.

It follows that the removed SST trend is fixed at 0.75 sum_eg b_e a_eg. The corrected denominator D is positive for all four period/reference combinations. With raw trends T and N_m, the raw-minus-corrected feedback is

    Delta_m = N_m/T - [N_m - sum_eg b_e c_meg alpha_eg]/D.

A check of event e in region g gives a measurement y_eg with error at most epsilon in alpha units. A check is a constraint on a regional event scale, not one buoy or one temperature reading. The precision is assumed, not demonstrated.

Take two candidate scale fields alpha and beta consistent with a common measurement outcome. Their difference d obeys the event mean equalities and

    |d_eg| <= l_eg,
    l_eg = 0.5 if unchecked, or min(0.5, 2 epsilon) if checked.

These conditions are sufficient as well as necessary. Set alpha = 0.75 + d/2 and beta = 0.75 - d/2. Both fields satisfy the mean and scale bounds. They agree with the central measured outcome y = 0.75 within epsilon. Thus a central outcome attains the largest possible posterior range; there is no hidden assumption about the outcome distribution.

The sharp radiation-trend width is

    W_m = sum_e min_theta_e sum_g l_eg |b_e c_meg - theta_e a_eg|.

Each event is a separate support problem because its global mean is fixed separately. Linear-program duality gives the scalar minimization; a weighted median of the ratios gives its exact solution. Zero area-step coefficients contribute constant terms. The feedback width is W_m/D. We compute widths first with primal linear programs, then check them with this separate dual calculation. For each target we divide a design's width by its own unchecked width. The design score is the largest fraction across the 24 targets. This is not a ratio of ensemble-average widths.

We also test two controls: tied scales alpha_g with one fixed total trend, as in the prior design study; and separate event scales with only the total removed trend fixed. The latter allows global error transfers between dates. The primary event-mean test prevents such transfers. Tied scales with one trend constraint and separate scales with six event constraints are different sensitivity sets; they are not claimed to be nested.

We use epsilon = 0 and 0.05. For tropical checks, we enumerate all 64 subsets of the six dates. A selected date constrains all three tropical sectors. Costs are equal per date, regardless of source data availability. The dates, regions, bounds and plans were chosen after reading prior results; this is not a preregistered test.

## Numerical evidence

Largest remaining relative range at epsilon = 0.05, in percent. Each entry takes the maximum over both correction fits and all six response targets for that period.

| Validation plan | Tied scales, 1982-2022 | Separate events, 1982-2022 | Separate events, 2001-2022 |
|---|---:|---:|---:|
| None | 100.00 | 100.00 | 100.00 |
| 2020, three tropical sectors | 40.78 | 94.93 | 86.64 |
| 2020, all nine regions | 20.00 | 93.91 | 83.95 |
| 2005, three tropical sectors | 40.78 | 70.93 | 78.98 |
| 2005 and 2020, three tropical sectors | 40.78 | 59.57 | 55.06 |
| All dates, three tropical sectors | 40.78 | 37.07 | 37.46 |
| All dates, all nine regions | 20.00 | 20.00 | 20.00 |

The 93.91% target is HadAM3, CCI-fit correction, 1982-2022. Its feedback width falls from 0.29608 to 0.27804 W m-2 K-1. At central outcomes the remaining raw-minus-corrected interval is -0.04328 to +0.23476. Thus even checks of all 2020 regions can leave both signs in this example. This does not give the sign or probability of the actual error.

Separate event scales with only the total trend fixed give a largest remaining fraction of 93.07% after all 2020 regions are checked. The large residual therefore persists with or without event-by-event mean information. Fractions use different unchecked denominators for different assumptions and cannot order their absolute widths.

The exact date search selects 2005 for one tropical-check date (78.98% remaining), then 2005 and 2020 for two dates (59.57%), then also 2007 for three (48.52%). Adding 1985 gives 41.16%; adding October 2021 gives 37.46%. The 2023 date gives no gain in these periods. The optimal sets happen to be nested; the search did not impose this property. These are optima among the 64 tested date subsets, not all observing plans.

Allowing separate event errors does not remove the value of tropical coverage. Checks at every event in all three tropical sectors leave at most 37.46%. What fails is transfer from one checked date to unchecked dates. Under tied scales, a check at any date constrains every date by assumption. The primary test removes that transfer.

## Checks and limitations

The independent dual audit agrees with all 1,008 LP widths to 2.3e-16 W m-2 K-1 and all 1,536 portfolio target fractions to 4.5e-16. Source full-correction temperature and radiation trends reconstruct within 1e-6; exact errors are in `files/audit.json` and `files/reconstruction.csv`. `files/witnesses.csv` stores explicit pairs of feasible fields for the mean response at epsilon 0.05. These fields attain the widths at a common central outcome. They are certificates, not proposed physical corrections.

We repeat the analysis with annual means and annual trends. The main 2020-all fraction becomes 93.92%; the best one- and two-date sets remain 2005 and 2005 plus 2020. The two-date fraction becomes 59.58%. Monthly calculations preserve the source calendar-month anomaly convention, which can leave a very small seasonal trend imprint from a partial-month event before a tested period. Annual means remove that imprint. `files/annual_bounds.csv` gives this check.

The half-to-full correction scale range, known event global means, constant regional scales and assumed measurement precision are strong conditions. These are sensitivity sets, not empirical uncertainty distributions. Separate event variables do not assume statistical independence; there is no probability model. Event errors could in fact be strongly linked. We do not estimate that linkage. Within-region variation, missing dates, smooth drift, input dependence, nonlinearity and response-map error are excluded. All six dates remain in the model even though some have little or no leverage in a given window. Models and windows are related. Excluded-model transfer and real reference sampling are not tested. The latest source date is not the latest possible input change.

Buoys used by SST analysis can understate an input change away from buoys. A real validation program must justify independence and regional coverage, not just measure more stations. We give no instrument count, deployment plan or measurement feasibility claim. The result supports checks that span input transitions or an explicit model of error transfer across transitions. It does not weaken the evidence that SST corrections matter for model forcing, or establish a revised magnitude for true feedback.

## Reproduction

Use Python 3.12, NumPy, SciPy, pandas and Matplotlib, with the SCI CLI. The inputs are preserved SCI publications; no private scratch is required. Put their full-hash ZIPs in a campaign directory. With this package at P, run:

    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python P/files/analyze.py --campaign /path/to/campaign --scratch /path/to/separate-scratch --out /path/to/new-results

The script verifies both ZIPs, checks member hashes through SCI verification, extracts only three files into scratch and writes new results outside P. Add `--annual` to repeat the annual check. Run one instance at a time for low CPU use. Each run takes about one minute on one CPU here. It starts no service.

For an independent offline check using only bundled aggregates:

    OPENBLAS_NUM_THREADS=1 python P/files/audit.py

The audit reads `coefficients.csv`, `bounds.csv` and `event_portfolios.csv`. It writes only standard output. `dual_audit.json` records the checked result. The coefficient table retains event-by-region projections and time weights, so every width can be reconstructed without the source arrays. `best_event_portfolios.csv` gives the best date sets; bit positions follow the six dates listed above. `provenance.json` pins source inputs. `NOTICE.md` identifies source credit and external data terms. Raw or restricted databases are not bundled.

## Job provenance

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-fd3748c09781. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol with high reasoning effort. Analysis date 2026-11-11. No agents were launched. Computations used at most two single-thread processes. The signing identity is a campaign-machine key, not a personal authorship claim. This publication includes new code, narrative, figures and aggregate results under the exact SCI baseline license. No remote upload or index submission was made by this job.
