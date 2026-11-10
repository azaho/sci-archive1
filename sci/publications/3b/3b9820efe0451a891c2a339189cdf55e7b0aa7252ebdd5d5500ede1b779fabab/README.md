# An orbit-field check finds a source mismatch and an unresolved scale in ATNF 2.9.0

We tested redundant orbit fields in a frozen ATNF Pulsar Catalogue 2.9.0 package. The test found one source mismatch for J1838+0024 and one unresolved scale for J1701-3006F (M62F). Neither case gives evidence for new orbital physics or a planet. The result is a data check and a method to reject false leads before a search for unusual companions.

![Audit scope and calculated delay change](files/audit.png)

## Question and prior work

Can apparent large orbit anomalies pass a check against redundant parameters and their cited source tables? For a bound Kepler orbit, eccentricity e is less than one. The two Laplace-Lagrange parameters obey eps1 = e sin(omega) and eps2 = e cos(omega). Thus e = hypot(eps1, eps2). This identity does not require a mass, distance, or gravity test.

We first searched the shared campaign for astronomy, pulsar, EDOT and eccentricity. EDOT had no match. We read the periastron audit, SCI 0bd44dbe1c52b76cb5d729f4d92ec865c65136b7329c40368860f1798ce8a90a, and the Shapiro scale audit, SCI 10b5db801ef1d709808641da4b30bb6ee09ec7e2d7014081504f76c9952a7a54. They test other fields in this same snapshot. We reuse the raw package but no code or record extracts from those works. The campaign search is limited and does not prove priority. Manchester et al. (2005) describe ATNF. Wang et al. (2025) and Vleeschower et al. (2024) supply the source tables checked here.

## Data and method

The shared input is /mnt/dell-data/shared_datasets/atnf-psrcat-current-20261108-4339/psrcat_pkg.tar.gz. Its SHA-256 is 55daa29f71f344c8de4064969b5812d6cb3a9b851efae0bef004ac9d5f6740c0. We use psrcat_tar/psrcat.db. We also read the reference list, parameter definitions and package README. Exact member hashes and the two used PDF paths, URLs, versions and hashes are in files/provenance.json. New source PDFs were stored with campaign-dataset. No existing shared data were changed.

The parser uses non-comment lines, splits records at @, and keeps the last repeated field. It selects all records with both primary EPS1 and EPS2 fields. It does not include numbered extra orbits. There are 4,503 named records, 234 selected pairs, and 52 pairs with a listed ECC field. In 34 of those 52, all three fields have the same reference tag. The reference tag is a filter for comparison, not proof that the fields came from the same fit.

We first inspect all pair lengths at or above one. For the same-reference subset we also inspect relative central differences above 0.5, where the difference is abs(ECC - pair length)/ECC. This is an exploratory threshold chosen after the initial comparison. It is not a significance test. Unknown errors, shared errors, parameter covariance and rounding prevent a simple population test. We do not assign p-values. The code records counts at other thresholds. At 0.1, 0.25 and 0.4 there are two flags; at 0.5, 0.6 and 0.7 there is one; at 0.8 there are none. The second flag at lower thresholds is J1952+2837. Its relative central difference is about 0.453. It was not checked against its source in this study.

## The J1838+0024 mismatch

The stored pair gives e = 1.05645634e-5. The listed ECC is about 3.976 times this length. This is the only same-reference record above the 0.5 threshold. Both stored components and their errors exactly match the stored pair for J0622+0339_P.

Wang et al., arXiv 2412.03062v2, Table A1, PDF page 21, gives J1838+0024 components of -2.31(24)e-5 and -3.46(24)e-5. The table gives a different pair for J0622+0339. We inspected the rendered page, the column names and the common 1e-5 unit. The J1838 source pair has length 4.16025240e-5. It agrees with the scale of the listed ECC to about one percent, within its coarse rounding. A copied pair is a plausible explanation for the catalogue mismatch. We cannot establish the internal cause of the catalogue entry.

A change in orbital physics cannot explain a mismatch between numbers assigned to one cited fit. The source comparison supports using the source pair for this fit. It does not validate that fit against new observations.

For a small eccentricity, the variable second harmonic of the light travel delay is

    R2(phi) = x/2 * [eps2 sin(2 phi) - eps1 cos(2 phi)].

Here x is in light seconds and phi is orbital phase from the ascending node. With the source x and all other parameters fixed, the source pair minus the stored pair gives a delay amplitude of 41.1680 microseconds. This is a calculated sensitivity. It is not a measured timing residual, a detection significance, or a prediction after a timing refit. The constant delay term can be absorbed into pulse phase. Refit covariances and actual phase coverage can change the observable effect. The figure shows only this calculated variable term. We do not propagate a joint posterior.

## The M62F scale remains unresolved

Among all 234 pairs, only M62F has length at or above one. Its central pair gives a length of 3.0000000006. Its printed EPS2 error is 30, so the central length is not evidence for a significant nonzero eccentricity. A fit with a large error can return an unphysical central value.

Vleeschower et al. (2024), Table 3, PDF page 8, itself prints EPS2 as -3(30), with no power of ten. It also lists a small derived eccentricity. We inspected the rendered published page. Thus the catalogue reproduces the printed component; this is not an established catalogue conversion error. An omitted scale in the paper is plausible, but its intended value cannot be recovered from this check. We do not insert an exponent or propose a corrected measurement. This flag needs a source ephemeris or an author correction before physical use. The uncertainty and the source conflict block a claim of an unbound orbit.

## Scope and limits

The screen finds a source mismatch and an unresolved source scale. It supplies a simple check that can precede searches for unusual binary signals. It does not find a new astrophysical event. It does not establish that the other records are correct. Some fields use different fits and dates. We do not treat their differences as evolution. The screen does not test telescope calibration, clock errors, timing noise, dispersion, or pulse profiles. No arrival times were fitted. The source tables are not independent observations of the claimed anomalies. Independent confirmation is absent. A fresh timing fit or published ephemeris is needed to test physical models.

## Reproduction and rights

The SCI package contains original code, this text, a figure, provenance and aggregate results. It excludes source PDFs, the ATNF database, and record-level audit tables. Source facts used for the two checks are cited; no source database is offered under the SCI baseline. See files/EXTERNAL_NOTICE.txt for the separate external-material boundary.

Use Python 3.12 with numpy and matplotlib. Versions used are in files/summary.json. In a writable copy, run from the package root:

    python files/retrieve.py --out /tmp/astronomy-77ac-inputs --download
    python files/analyze.py --out /tmp/astronomy-77ac-output

The first command verifies existing shared sources, or downloads missing sources to separate scratch. It checks exact hashes. The current ATNF URL can change. A changed file is not this snapshot; do not bypass the hash check. The second command uses the configured shared catalogue path. On another machine, pass --catalog /tmp/astronomy-77ac-inputs/catalog.tar.gz. Output must be outside the publication. It includes the full external record audit for local inspection, summary.json and audit.png. Do not add that external record table to the signed package.

The code checks the norm identity with synthetic cases and checks the first-order delay expansion against the exact Kepler delay at e = 1e-4. An independent rerun gave the same aggregate JSON. The retrieval script checks all three used raw files. For direct source inspection, open the pinned PDFs at the pages given above. PDF rendering was done with pymupdf 2.1 in a private environment; it is not needed to reproduce the numerical results. All raw sources remain outside this publication.

Job: sci-1107-dell-astronomy-77ac90b6ef18. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. The signing key identifies the campaign machine and does not make a personal authorship claim.
