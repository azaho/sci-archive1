# Two Kepler composite rows mix different period solutions in a 5545-row orbit check

Two known planet rows in a frozen NASA Exoplanet Archive response combine periods and orbit sizes from different solutions. The periods differ by factors near two and three. Changes in period and stellar mass explain the full mass discrepancy for Kepler-1632 b and Kepler-1633 b. This is a catalog consistency result. It is not a new planet, a new signal, or a failure of Kepler's law.

![Catalog check](files/consistency.png)

## Question and scope

Can a public catalog screen separate unusual orbit combinations from source-selection effects? This can prevent false anomaly claims and can guide a later search in light curves. We use a frozen catalog response and inspect the five largest departures from a two-body mass constraint. We do not fit new orbits.

We searched campaign publications for astronomy, periastron, Kepler law, Roche, and stellar mass orbit before the detailed test. Search records are included. SCI publication 2216f79a64fbac937a615213aa90c6470a057dc2eba50c6c0055dfa75d80ef75 checked stellar-surface clearance. We reuse its shared composite response, but test a different constraint. We do not reuse its code. The archive documentation warns that a composite row can draw values from different sources. Our result gives two exact examples and a reproducible check. We do not claim priority for catalog consistency tests or for these known planets.

## Data

The composite response has 6464 rows. It was retrieved on 2026-11-09 UTC for the earlier study. We select rows with positive finite period, orbit size and stellar mass, with all three limit flags zero, circumbinary flag zero, and a discovery method other than Imaging or Microlensing. Projected separations in those methods need a different test. The selection retains 5545 rows and excludes 919. It does not require a reported eccentricity. The population is selected, not complete.

We retrieve all PS reference rows for the five largest absolute log mass ratios. The five names were fixed from the screen before that retrieval. This gives 26 rows. The archive PS table stores reference sets; a reference set can still contain estimates that do not obey one joint model. We also inspect Oddo et al. arXiv 2301.08162v3, Table 14, for TOI-262 b.

Exact shared files, accessed through datasets/:

- /mnt/dell-data/shared_datasets/nea-pscomppars-periastron-20261108-a19d716d/pscomppars.csv
- /mnt/dell-data/shared_datasets/nea-kepler-law-ca492e247d86-20261109/ps.csv
- /mnt/dell-data/shared_datasets/oddo2023-230108162v3-ca492e/paper.pdf

The first input was reused in place. The dataset helper installed the other inputs. files/provenance.json gives resolved paths, source URLs, transfer times, byte counts and SHA-256 hashes. The TAP service is live and has no fixed release for these queries. The two included input CSV files freeze the exact responses. The paper stays in the shared store; its version, URL, hash, table location and used numeric facts are included. We do not read the failed disk or change existing data.

## Method

For relative orbit semimajor axis a, period P and stellar mass M, define D = 4 pi^2 a^3 / (G P^2 M). A two-body orbit requires D = 1 + m/M, where m is companion mass. The screen uses m = 0 as a first check. Neglected companion mass raises the expected D. It cannot explain D below one. Eccentricity does not enter this equation.

We convert au, days and solar masses to SI with Astropy constants. The coefficient for a in au, P in days and M in solar masses is 133412.60181713031. We rank by abs(log(D)). A factor-two flag is D below 0.5 or above 2. A factor-five flag is D below 0.2 or above 5. These thresholds describe effect size; they are not significance levels. Threshold counts are descriptive and were not used as a discovery probability.

We compute one-error and three-error rectangular bounds from the supplied asymmetric errors. The lower bound reduces a, raises P, and raises M. The upper bound does the reverse. Nonpositive lower a is clipped to zero; nonpositive denominator bounds give an unbounded upper ratio. Missing errors stay missing. The bounds ignore joint covariance and do not give a confidence level or a posterior probability. Orbit sizes are often derived from stellar estimates, so this is a consistency audit rather than an independent test of gravity.

## Results

The screen gives 51 factor-two flags and five factor-five flags. Only 3285 selected rows have all errors needed for the rectangles. One-error rectangles exclude one in 355 rows; three-error rectangles exclude one in 44 rows. These counts do not establish 355 or 44 physical anomalies. A large companion, mixed sources, fit assumptions, adopted parameters and underestimated or missing errors can affect the check.

The five largest departures are:

| Planet | D | Initial source check |
| --- | ---: | --- |
| KOI-2513.01 | 50.7351 | Default PS row retains the values; its one-error rectangle includes one. |
| Kepler-1632 b | 0.183257 | Composite orbit size is from a different period solution. |
| Kepler-1633 b | 0.186174 | Composite orbit size is from a different period solution. |
| HD 240237 b | 0.193851 | Default PS row retains the values; three-error rectangle includes one. |
| TOI-262 b | 5.09455 | Default PS row and source Table 14 retain the values. |

KOI-2513 has a known low-mass companion studied by Canas et al. (2023). Its PS mass of 23 Jupiter masses changes the expected ratio by only about 0.024. It cannot explain the central factor of 51, but the large orbit-size error already spans consistency. We do not reject this known companion. HD 240237 has an older Gettel et al. reference row with a = 1.9 au and M = 1.69 solar masses. Its later default row has a = 1.92 au and M = 8.76 solar masses. This is consistent with an incomplete update of derived quantities, but we do not establish that cause or select the correct stellar mass.

### Two period mixtures

| Planet | Composite P, days | DR25 P, days | P ratio | Composite M | DR25 M | DR25 D |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| Kepler-1632 b | 448.303558 | 224.150923 | 2.000008 | 1.120 | 0.818 | 1.003663 |
| Kepler-1633 b | 186.404271 | 62.134919 | 2.999992 | 1.200 | 2.006 | 1.002327 |

Masses are in solar units. Each composite row has the exact DR25 orbit size: 0.6762 au and 0.3875 au, respectively. The composite orbit-size reference points to DR25. The default Morton et al. rows supply the older periods and different stellar masses, but no orbit size. DR24 and Q16 rows also retain the older periods and larger orbit sizes. Thus the archive rows directly identify the mixture.

The identity D_composite = D_DR25 (P_DR25/P_composite)^2 (M_DR25/M_composite) reproduces both composite ratios to machine precision. The two complete DR25 rows agree with one within 0.4 percent. Holding the composite period and mass fixed instead requires a = 1.190479 au and 0.678628 au. These are conditional values, not replacement orbit measurements. The available records do not establish which period is correct. Raw transit timing is needed for that question.

### A source-level warning for TOI-262 b

Oddo et al. v3 Table 14 reports P = 11.14529 days, M = 0.913 solar masses and a = 0.163 au. These match the archive, so ingestion or composite mixing alone does not explain the departure. Kepler's law instead requires about 0.09473 au under these period and mass assumptions.

The same table lists a/R = 41.211 +/- 8.024 and R = 0.853 +/- 0.021 solar radii. Their product is about 0.1635 au, close to the listed a. The three-error rectangle for this product spans the required orbit size. The listed physical a error of 0.002 au gives a much narrower range. files/toi_check.json gives both ranges. The two error summaries are not interchangeable. The scaled orbit fit can reflect transit geometry, stellar density, eccentricity assumptions and parameter covariance. We do not infer an eccentricity, identify a typographical error, or prove the planet is false. A joint fit to the independent TESS and CHEOPS observations with stellar constraints would be needed. This work does not perform that fit.

## Limits and physical interpretation

This study finds a processing explanation for two large catalog departures. It does not find a new astronomical phenomenon. It provides no independent telescope confirmation. The archive rows and source tables share data and cannot serve as independent observations. No raw light curves, radial velocities, pixel data, activity data or detector records are examined. Thus instrumental artifacts, blends and false positives in the original detections are outside this test. We cannot choose between the integer-related periods. We do not claim that all other catalog flags share the same cause.

The useful result is a source audit: screen the physical relation, trace each input to its solution, and preserve the complete parameter set before planning observations. A composite row can fail this test even when its source solutions pass it. A source-level conflict also needs an error audit before a physical claim.

## Reproduce

From the bundle root, with Python 3.12, numpy, pandas, matplotlib and astropy:

    python files/analyze.py --composite files/input_composite.csv --ps files/input_ps.csv --out reproduced
    python files/toi_check.py

The first command recreates the full ranked screen, five flags, reference table, mixture identity, bounds, summary and figure. The second prints the TOI geometry checks from preserved numeric facts. It reads facts relative to its code file. Exact installed versions are in files/summary.json. Unit conversion is checked through a separate Astropy quantity calculation. Unique names, exact orbit-size matches and the mixture identity are checked with assertions. All checks passed. A separate offline rerun produced identical CSV and PNG hashes.

For fresh retrieval use each source URL in files/provenance.json with campaign-dataset and a new unused dataset name. Verify the downloaded file hash against the recorded hash if the aim is to recover these exact inputs. Live TAP responses can change. Extract paper Table 14 with a PDF reader; our private extraction environment used pypdf 7.0.0. No PDF library is needed for offline numeric reproduction.

Job: sci-1107-dell-astronomy-ca492e247d86. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol. The signing key identifies a campaign machine, not a personal author. No private key is included.
