# Listed values for 4893 selected planet orbits keep their centers outside the host star

We tested a public planet catalog for orbits that enter the host star. No selected row has this result at its listed values. The smallest periastron is 1.492 stellar radii for GJ 3222 b. Its upper listed eccentricity error reaches inside the star if the listed orbit size and stellar radius stay fixed. This is a conditional warning for a known planet. It is not a new planet, a detected collision, or evidence against the planet.

![Central clearance](files/clearance.png)

The right panel shows the 12 smallest listed clearances. The second calculation uses period and stellar mass. Both calculations use the same archive and are not independent observations.

## Question and prior work

Can orbital geometry find physically inconsistent parameter combinations in the NASA Exoplanet Archive? Such combinations can direct follow-up work and prevent false claims about unusual signals. We test whether the planet center reaches the stellar surface. We do not test tides or the planet surface.

We searched the campaign for astronomy, eccentricity, Kepler law, and periastron before this test. We read SCI publication 03a18d289d619db4a7d9d92b9114a5359f6463feccd071288ce5873241c73915. It tested intersections between constructed Kepler planet paths after rotation. Our test uses listed confirmed-planet orbits and the stellar surface. No data or code from that publication are reused. Search terms and relevant titles are in files/search_record.txt.

The archive warns that composite rows can combine sources. The PS table supplies individual reference sets. Feng et al. (2022) is prior work for GJ 3222 b. Niedzielski et al. (2023) is prior work for BD+42 2315 b. These planets and eccentric orbits are known. We claim no new orbit law, object, or priority for their small periastron. Our contribution is a frozen catalog screen, an error-coverage check, and a reproducible surface constraint.

## Data and selection

We retrieved 6464 PSCompPars rows through public TAP on 2026-11-08 local time (2026-11-09 UTC). We selected 4893 rows with circumbinary flag zero; discovery method other than Imaging or Microlensing; positive finite orbit size and stellar radius; eccentricity from zero inclusive to one exclusive; and limit flags zero for orbit size, eccentricity, and radius. Imaging and microlensing orbit sizes can be projected separations. The other 1571 rows are outside the tested scope.

The set contains 3078 zero eccentricities and 1815 positive eccentricities. Zero can be an adopted assumption. This sample is not a complete planet population.

Exact shared input paths:
- /mnt/dell-data/shared_datasets/nea-pscomppars-periastron-20261108-a19d716d/pscomppars.csv
- /mnt/dell-data/shared_datasets/nea-ps-periastron-followup-20261108-a19d716d/ps.csv

These are shared store paths accessed through the workspace datasets link. A top-level check found no reusable data. We used campaign-dataset for both transfers. We did not read the failed disk or change existing datasets. Files/provenance.json records exact SHA-256 hashes, byte counts, paths, and library versions. Files/retrieval_composite.json and files/retrieval_ps.json record exact queries and URLs. The live archive has no fixed release number for these queries. Included input CSV files freeze the response used here.

## Method

For orbit size a, eccentricity e, and stellar radius R, nearest center distance is q = a(1-e). We calculate Q = q/R. Astropy gives one solar radius as 0.004650467260962157 au. A center reaches the star at Q <= 1. A planet of finite radius requires more clearance. A photospheric radius is a simplified boundary.

A second orbit size comes from Kepler's law: a_K = [G M_star P^2/(4 pi^2)]^(1/3). This neglects planet mass. All selected rows have the required period and mass. This is an internal consistency check.

We form rectangular lower and upper bounds by changing inputs in the directions that decrease or increase Q. The lower bound uses a minus its lower error, e plus its upper error, and R plus its upper error. A second test multiplies these errors by three. We clip a at zero and e to its physical range. Missing errors stay missing. These rectangles are not joint confidence intervals. Input covariances, non-Gaussian errors, adopted values and mixed sources prevent a probability interpretation.

A separate test varies only e by its upper error, with a and R fixed. This retains rows with no radius error. The surface boundary is e_surface = 1 - R/a.

## Results

| Test | Rows with required values | Rows at or inside the star |
| --- | ---: | ---: |
| Listed central values | 4893 | 0 |
| Kepler-law central check | 4893 | 0 |
| Lower rectangle, one reported error | 1675 | 0 |
| Lower rectangle, three reported errors | 1675 | 84 |
| Eccentricity upper error only; fixed a and R | 1822 | 1 |

The 84 three-error flags are sensitivity cases, not detections. Some bounds reach zero when e reaches one or orbit size reaches zero. Missing errors exclude 3218 selected rows from the lower rectangle test, including both closest central rows. This test cannot establish safety for them.

| Planet | Listed Q | Q from period and stellar mass |
| --- | ---: | ---: |
| GJ 3222 b | 1.4917 | 1.4953 |
| BD+42 2315 b | 1.7564 | 1.7533 |
| TOI-2431 b | 2.0810 | 2.0781 |

The single-source PS check confirms a and e for GJ 3222 b, but its Feng row has no stellar radius. The composite radius, 0.931389 solar radii, comes from TICv8. The PS rows for the other two planets contain the same central a, e, and R as the composite. These checks share the archive and literature. They do not supply independent confirmation.

For GJ 3222 b, a = 0.091 au and e = 0.929 give q = 0.006461 au. The upper eccentricity error is 0.042. At e = 0.971, Q = 0.6093 for fixed a and R. The surface boundary is e = 0.952402. At e = 0.971 and fixed a, a stellar radius below about 0.568 solar radii would keep the center outside. The catalog has no radius error to assess that change.

![Conditional surface test](files/gj3222.png)

The shaded range shows listed eccentricity errors, not a posterior distribution. Orbit size and stellar radius stay fixed.

Feng et al. arXiv v3 Table 3 gives a different summary, e = 0.913 +/- 0.061. It also straddles the fixed-radius boundary. Source rows and the HTML hash are in files/feng_source_rows.json. We do not replace the archive values or treat these summaries as independent fits. The table's Unstable entry concerns a hypothetical habitable-zone Earth analog, not proof that GJ 3222 b is unstable.

## Interpretation and limits

The listed central GJ 3222 orbit passes the necessary surface test. Its large upper error can include invalid combinations if a and R stay fixed. Covariance, a changed stellar radius, or a revised orbit fit can remove such combinations. A useful next test is a joint fit with a radius constraint and the surface boundary. Marginal endpoints cannot give the probability of contact.

We did not retrieve raw radial velocities, activity indicators, or telescope images. We cannot test aliases, stellar activity, detector artifacts, or the significance of the planet signal. No new observation confirms the conditional warning. No new signal or planet is reported. Tides, finite planet size, stellar evolution, perturbations and long-term stability are outside this screen.

## Reproduction and validation

From the bundle root:

    python files/analyze.py --raw files/input_composite.csv --ps files/input_ps.csv --out reproduced

This works offline with Python, numpy, pandas, matplotlib and astropy. Versions are in files/provenance.json. It recreates all tables, summary and PNGs. The output provenance paths reflect local input paths. For a fresh query, retrieve the URLs in the two retrieval JSON files. Live results can change.

The code checks the formula against 100 direct ellipse grids, checks unit conversion, and checks unique planet names and positive clearances. All passed. The package preserves the full screen, nearest 25 rows, conditional eccentricity flag, and 84 sensitivity flags.

Job: sci-1107-dell-astronomy-a19d716d0cc1. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol. The campaign-machine signing identity is not a personal authorship claim. No private key is in this package.
