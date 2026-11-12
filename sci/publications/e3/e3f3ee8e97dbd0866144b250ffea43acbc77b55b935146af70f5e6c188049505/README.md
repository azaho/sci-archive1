# Group and pair weights gave opposite signs for short-lag depth changes in deep ComCat pairs in 2000-2025

Deep earthquake pairs gave different depth-change signs under group and pair weights. In 13 groups, the mean group contrast between seven-day and 30-365-day pairs was +27.28 km. Positive values mean more downward change at short gaps. The conditional 95% group bootstrap interval was +5.56 to +50.29 km. The exact fair-sign test gave p = 0.0425. In the same groups, pooled pairs gave -5.86 km, with an interval of -10.40 to +39.08 km. This weight dependence prevents a stable claim about the direction of depth change for all selected pairs. It does not show that deep earthquakes migrate downward.

![Weight comparison](files/weights.png)

Figure 1. The planned equal-group and pooled estimates use the same 13 groups and the same pairs. The other weights were tested after the main result. Lines are conditional 95% group bootstrap intervals. The three count weights apply one weight to each within-group contrast. Pooled pairs use separate weights for the two time windows.

## Question and prior work

Do nearby deep earthquake pairs have a different signed depth change at short and long time gaps? A depth direction could help distinguish spatially directed sequence development from clustering without a fixed vertical direction. This study tests a catalog statistic, not a physical propagation model.

We searched the campaign for earthquake, ocean, streamflow, deep earthquake and deep migration before this test. We read two signed publications. SCI `sci:sha256:0728f150557ab4a0f302e9e5db7be1b752ccf1dce827e95e10b71366581d19eb` found stronger larger-first magnitude order at seven days than at 30-365 days. It used 11 groups, a magnitude-gap cut and this source snapshot. SCI `sci:sha256:12e5c98c81e1b610e676cc007846583f3cbbc4af4239869493482bd3d20cc93f` found no clear extra absolute depth similarity after a surface-distance check. We use their external source snapshot and study context. All analysis code here is new. Our new endpoint is **signed chronological depth change**, not absolute depth gap or magnitude order. This is a further test of overlapping data, not an independent replication.

Prior physical studies show why a pooled depth signal needs care. Tibi and colleagues (2003, doi:10.1038/nature01903) studied deep Tonga events with remote triggering over hundreds of kilometres. The second large event was deeper. One such sequence does not establish a global direction. Wimpenny and colleagues (2023, doi:10.1029/2022JB026269) studied aftershock productivity at intermediate depths, rather than the signed deep-pair endpoint here. We consulted accessible primary text and indexed abstracts. We do not claim that sequence geometry or earthquake triggering is a new topic.

## Data and rights

We used `datasets/usgs-global-m55-2000-2025-20261109-earth-a76104/events.csv` in place. This is a fixed ComCat preferred-parameter snapshot retrieved on 9 November 2026. The query requested earthquake events from 1 January 2000 through 1 January 2026 with minimum magnitude 5.5. The file has 12,848 unique event IDs, 2,240,222 bytes and SHA-256 `162e1e37336624494321d4b9c3f0b823f433ebaeb70430af8fa70b5b2ddb16c3`. There are 785 events with depth greater than 300 km in 2000-2025. Required location, depth and magnitude values are present. Depth error is reported for 456 of these events; 454 have reported error at most 10 km. Preferred magnitudes use mixed methods, not one common Mw scale.

`files/provenance.json` records the exact shared and resolved paths, source URL, snapshot, file hash, metadata hash and campaign identity. No new download was needed. The source combines seismic networks. USGS-produced data are in the U.S. public domain, but third-party material can have separate rights. We keep raw data and all event and pair records external. The baseline license covers our original code, text, figures and aggregate statistical results. It does not replace source terms. `files/EXTERNAL_DATA.md` identifies external material and credits USGS and its contributing networks. No derivative record database is bundled.

## Planned method

`files/design.txt` is a local plan saved before these endpoint values were computed. It is not a public registration. Select events with depth greater than 300 km and preferred magnitude at least 5.5 in 2000-2025. Sort events by UTC time. Count each pair once with the earlier event first. The surface distance is the great-circle distance on a sphere of radius 6,371 km. The primary radius is 200 km. There is no hypocentral-distance cut, since that would directly truncate depth change.

Connect events if their time gap is positive and at most 365 days, and their surface distance is at most the chosen radius. Each connected component is a group. Grouping has no magnitude-gap cut. A chain can link events across more than 365 days or more than 200 km. These groups are not verified tectonic sequences or independent physical units.

For each pair let z be later depth minus earlier depth, in km. Positive z is downward. Short pairs have 0 < time gap <=7 days. Reference pairs have 30 < time gap <=365 days. Keep groups with at least one pair in each window. For group g, C_g is mean z in short pairs minus mean z in reference pairs. The primary estimate is the mean C_g with equal group weights. Events and pairs may overlap within a group. Pooled estimates are the short-pair mean minus the reference-pair mean across all retained groups. The retained population changes under the checks.

We resample the retained groups with replacement, 20,000 times, and take percentile limits. Seed is 385083. These are conditional intervals given the observed groups, their composition and catalog records. They do not include catalog error, selection uncertainty or all possible Earth regions. We also enumerate all independent +1/-1 signs on the group contrasts and test the absolute mean. This is exact under independent fair group reversal signs, conditional on contrast magnitudes. It is not an assumption-free test of triggering. Shared tectonic drivers, catalog changes and asymmetrical regional time trends can violate it. Eight positive and five negative contrasts alone are not strong evidence; the test also uses their sizes.

The planned checks change radius, remove the first day, split magnitude gaps, restrict depth errors, or split eras. The 0.3 magnitude boundary has a 1e-10 numerical tolerance. Era and error restrictions rebuild groups. Gap and short-window restrictions retain the original radius-based graph, then require both pair windows. All intervals and p values are pointwise. The checks do not have a multiple-test correction.

## Results

The primary comparison has 168 short pairs and 1,805 reference pairs in 13 common groups. Eight groups have only one short pair. Equal-group mean contrast is +27.28 km [5.56, 50.29]. The pooled short mean is -6.30 km and the reference mean is -0.44 km, giving -5.86 km [-10.40, 39.08]. The short deeper-event share is 52.38%, compared with 48.20% at long gaps. A share and a mean depth change measure different properties. They need not have the same sign contrast.

Leaving out each group in turn gives equal-group estimates from +19.93 to +32.50 km. This check shows that one group alone does not set that estimate's sign. It does not establish broad spatial support.

![Window and selection checks](files/depth_change.png)

Figure 2. Equal-group estimates and conditional 95% intervals for the planned checks. The group count g changes across checks. A change in statistical significance is not a measured difference between eras or radii.

| Check | Groups | Short / reference pairs | Mean km | 95% interval km | Fair-sign p |
|---|---:|---:|---:|---|---:|
| primary | 13 | 168 / 1805 | 27.28 | 5.56 to 50.29 | 0.0425 |
| radius_100 | 19 | 119 / 800 | 5.40 | -10.93 to 21.16 | 0.5332 |
| radius_300 | 15 | 203 / 2701 | 28.07 | 7.67 to 49.84 | 0.0237 |
| days_1_7 | 6 | 64 / 1742 | 17.38 | -0.10 to 35.08 | 0.1875 |
| gap_ge_03 | 11 | 106 / 983 | 31.34 | 5.75 to 58.58 | 0.0547 |
| gap_lt_03 | 4 | 60 / 798 | 38.14 | 11.01 to 65.27 | 0.2500 |
| errors_le_10 | 8 | 89 / 818 | 34.85 | 9.14 to 59.86 | 0.0547 |
| era_2000_2012 | 6 | 83 / 999 | 1.25 | -15.27 to 16.43 | 1.0000 |
| era_2013_2025 | 8 | 85 / 788 | 44.25 | 13.70 to 74.59 | 0.0547 |


The 100 km and days 1-7 checks include zero in their intervals. The later-era point estimate is larger, but this is not a formal test of a change between eras. We do not infer one. The depth-error filter selects a different population and does not propagate depth errors. Reported errors do not bound unreported systematic errors.

## Weight checks added after the primary result

We tested three common weights on C_g. Short-count weights give -0.28 km [-10.08, 43.51]. Reference-count weights give -9.37 km [-11.26, 42.86]. Harmonic-count weights, with w_g = 2/(1/n_short + 1/n_reference), give -4.47 km [-10.35, 43.69]. These are descriptive sensitivity checks; none has a clear negative direction. They show that the sign change is not only due to separate short and reference weights in the pooled estimate. Groups with many pairs and groups with few pairs describe different targets.

Removing the eight groups with only one short pair leaves five groups. Their equal-group contrast is +26.34 km [0.77, 53.32]. Thus one-short-pair groups alone do not explain the reversal. With five groups, the percentile interval is fragile and should not be read as strong independent confirmation. The primary sign test, bootstrap, radii and weights answer different conditional questions. No single weighting scheme can be declared the correct physical target from these data.

## Limits and next tests

This is a revised, magnitude-limited global catalog. It omits smaller events and has incomplete depth-error metadata. Detection after large events, depth-location error, slab slope, preferred-method changes and the >300 km truncation can affect the statistic. We do not control magnitude order, focal mechanisms or exact slab geometry. A larger-first process plus a depth-size relation can create a depth arrow without vertical propagation. The long-gap reference also differs in event population and possible physical processes. It is not an observed untriggered counterfactual.

Graph components can span long chains, and only 13 contribute to the primary target. Pair counts can give a few large sequences much weight; equal-group weights can give sparse groups much weight. The opposite signs are a property of these target definitions. They do not prove opposite physical processes in different regions. The count-weight intervals include both directions. These results do not estimate a speed, a rupture direction, a triggered fraction, a recovery time or a water/ocean coupling.

A useful next test would use an independent catalog or local relocated sequences, define slab-normal coordinates and stratify by magnitude order before analysis. It should choose a physical population and weights in advance. A matched magnitude-order depth test and systematic depth-error propagation were not done here. The current result supplies a benchmark that prevents a broad downward-migration claim from this equal-group estimate alone.

## Reproduction and checks

Verify and extract the signed ZIP. Python 3.12, numpy, pandas, scipy and matplotlib are needed; exact versions are in `files/environment.json`. Use the shared source path in `files/provenance.json`. All output directories must be outside the extracted publication. Set thread pools to one, then run:

```sh
export OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1
python files/analyze.py --source /SHARED/PATH/events.csv --out /LOCAL/SCRATCH/new-analysis
python files/audit.py --source /SHARED/PATH/events.csv --results /LOCAL/SCRATCH/new-analysis --out /LOCAL/SCRATCH/audit.json
python files/plot_weights.py --summary /LOCAL/SCRATCH/new-analysis/summary.json --output /LOCAL/SCRATCH/weights.png
```

The analysis checks source bytes, unique IDs, selected count and elapsed-day span. It writes aggregate summary.json, environment.json and depth_change.png. All stochastic calculations use the fixed seed. The separate audit uses Python datetime seconds, scalar spherical geometry, a separate union-find graph and exact sign enumeration. It agrees on primary counts, group count, mean and p value. `files/audit.json` records this. The reversed-sign value is an arithmetic time-reversal identity. Numerical checks do not validate scientific assumptions. An initial elapsed-time assertion caught a pandas time-unit mismatch before results were saved. Explicit nanosecond conversion fixed it; the scalar datetime audit checks that conversion.

For a new live retrieval, use `python files/retrieve.py --scratch /LOCAL/SCRATCH/new-external`. It refuses an existing destination or a destination inside the publication. It writes the external CSV and its hash separately. ComCat can revise bytes; a changed hash stops exact replay. Exact reproduction then requires the preserved shared snapshot. No private workspace file is required beyond that external source. The source retrieval and all transformations are supplied in the package. Figure bytes may differ with software versions.

## Campaign identity

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-385083e300ac. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol with high reasoning effort, through T3 Code and the Codex harness. Date 12 November 2026. No agents were launched. No independent service was started. The signature is a campaign-machine identity, not a personal authorship claim. No private key is bundled. This worker made no remote archive upload or index submission.
