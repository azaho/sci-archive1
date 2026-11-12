# Public POSS-I transient catalogues show no Earth-shadow deficit inside partly shadowed plates

**Job** sci-1107-dell-astronomy-7213d1755543 · **topic** astronomy · **machine** dell · **model** claude-opus-5-5 (Claude Code) · **date** 2026-11-12.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

**Question.** Villarroel et al. (2025, PASP 137, 104504) reported that fewer POSS-I red-plate transients
(1949-1956) fall inside the Earth's shadow at geosynchronous (GEO) altitude than coverage predicts. They
gave this as evidence for sunlit reflecting objects in orbit before 1957. Doherty (2026, arXiv:2604.00056)
repeated the result on the same private catalogue (107,875 rows). Watters et al. (2026, arXiv:2601.21946)
found no significant deficit in smaller public samples. The VASCO team replied that those samples have
too little power (arXiv:2602.15171). We asked: does the deficit occur in large public catalogues, and does
it follow the physical shadow?

**Data.** We used three public, CC BY 4.0 reproduction catalogues of the same POSS-I candidates
(jannefi/poss1-plate-slice). These are not the VASCO catalogue. They are independent rebuilds of its
pipeline. S1 has 95,770 candidates (15-arcmin edge cut). S0-paper-parity has 134,899 candidates. S0 has
122,758 candidates. All three cover 641 red plates. We built a plate log from the STScI plate list and
VizieR VI/25. We corrected the times (hundredths of an hour; local-evening dates).

**Method.** For each candidate we calculated the shadow in two ways. (1) A geocentric cap around the
antisolar point, as in the earlier papers. (2) The true topocentric umbra seen from Palomar, through the
exposure, for nine altitudes from 500 to 100,000 km. Then we applied four tests:

1. The naive test of the earlier papers: observed shadow fraction against plate-area fraction, Poisson z.
2. A within-plate test: we compared each plate with its 8 square-symmetry images (rotations and
   reflections of the candidate positions in the plate frame). This keeps the plate counts, the clustering
   and the edge pattern. Only the position of the shadow edge inside the plate changes.
3. A between-plate test: a negative-binomial model of candidates per plate with Galactic latitude,
   declination, year, hour angle and plate grade. It gives the in-shadow density ratio rho (1 = no effect).
4. Placebo shadows: we moved the shadow by 2 to 56 days (56 shifts). This puts the same geometry on other
   stars.

**Results at GEO (S1 catalogue).**

- The shadow touches only 10 plates (geocentric cap) or 8 plates (topocentric). One plate (XE422) is fully
  inside.
- The naive test repeats a deficit: 0.391 % of candidates against 0.479 % expected (z = -3.9). For the
  topocentric shadow it gives 0.346 % against 0.469 % (z = -5.5).
- **The naive test is not calibrated.** For the placebo shadows its z has a standard deviation of 7.0
  (geocentric) and 5.1 (topocentric), and it goes from -8.4 to +22.8. Over altitudes, the naive z goes from
  -9.7 to +12.1 in the three catalogues.
- **Within-plate test: no deficit.** The ratio of observed to expected is 1.013 (z = 0.18, geocentric) and
  1.017 (z = 0.35, topocentric). Injection tests show that this excludes rho < 0.72 (geocentric) and
  rho < 0.70 (topocentric) at 95 %. A deficit like the claimed one (rho near 0.6) gives z near -2.0 (topocentric) to -2.5 (geocentric).
  S0-paper-parity gives the same bounds.
- **Between-plate test: weak and not significant.** rho = 0.56 (95 % CI 0.24-1.48, geocentric) and 0.68
  (0.28-1.66, topocentric). The fully shadowed plate XE422 is at Galactic latitude 14 deg, where crowding
  lowers the counts of all plates. The true shadow position has fewer candidates than all 40 placebo
  positions that do not overlap it. But the placebo series is correlated over 8-12 days, so it has only
  about 11 independent positions. Thus p is approximately 0.09. The model intervals are too narrow: they
  exclude rho = 1 for 17 of 56 placebo shifts (geocentric).

**Conclusion.** In these public catalogues, the shadow edge has no effect inside the plates. A real
population of sunlit reflectors must give a deficit at the shadow edge inside each partly shadowed plate.
The plate-area deficit comes from plate-to-plate differences in candidate counts at about ten plates.
Placebo shadows give such differences often. Thus the data do not support reflectors at GEO. A plate-level
cause (sky brightness near the antisolar point, plate depth, crowding) can explain the small
between-plate signal, but we did not prove which cause.

**Main limitation.** We did not have the private 107,875-row VASCO catalogue. The public catalogues
reproduce its pipeline but they are not identical to it. The between-plate test has low power because
only about ten plates touch the GEO shadow.

## Figures

- `files/figures/fig1_plate_counts.png`: candidate counts against Galactic latitude, and the shadow plates
  against the count model.
- `files/figures/fig2_altitude_scan.png`: naive and within-plate z against the assumed altitude, for the
  three catalogues.
- `files/figures/fig3_placebo_shifts.png`: naive z and model rho for the placebo shadows.
- `files/figures/fig4_injection.png`: sensitivity of the within-plate test to an injected deficit.

## Detailed results

### Main table (GEO, 35,786 km altitude; `files/results/geo_shadow_tests.csv`)

| catalogue | shadow | plates touched | observed % | area-expected % | naive z | within ratio | within z | within rho 95 % lower bound | model rho (95 % CI) |
|---|---|---|---|---|---|---|---|---|---|
| S1 (95,770) | geocentric cap | 10 | 0.391 | 0.479 | -3.93 | 1.013 | 0.18 | 0.72 | 0.56 (0.24-1.48) |
| S1 | topocentric | 8 | 0.346 | 0.469 | -5.53 | 1.017 | 0.35 | 0.70 | 0.68 (0.28-1.66) |
| S0-paper-parity (134,899) | geocentric cap | 10 | 0.436 | 0.479 | -2.27 | 0.968 | -0.54 | 0.70 | 0.68 (0.32-1.58) |
| S0-paper-parity | topocentric | 8 | 0.348 | 0.469 | -6.47 | 1.019 | 0.38 | 0.71 | 0.72 (0.34-1.60) |
| S0 (122,758) | geocentric cap | 10 | 0.451 | 0.479 | -1.43 | 0.943 | -0.96 | not run | 0.78 (0.36-1.74) |
| S0 | topocentric | 8 | 0.361 | 0.469 | -5.51 | 0.998 | -0.04 | not run | 0.82 (0.38-1.74) |

The three catalogues share most rows. They are not independent samples. They show that the result does
not depend on the edge cut or on the veto details.

### The geocentric cap is not the physical shadow

Seen from Palomar, the GEO umbra has a radius of about 9.9 deg at the zenith. Parallax moves it up to
8.7 deg from the antisolar point near the horizon. The earlier papers used a geocentric cap of 8.5-8.7 deg.
In S1, the cap and the topocentric shadow agree for only about half of the shadow-weighted candidates
(overlap 186 of 332-375). The cap and the true shadow touch different plates (for example XE617 is inside
the cap but not inside the topocentric shadow; XE532 is the opposite).

The naive deficit is larger for the topocentric shadow (ratio 0.74-0.77) than for the cap (0.82-0.94) in all
three catalogues. A reflector population would give this pattern. But this difference comes from the same
8 plates, and the within-plate test, which is sensitive to the shadow edge, shows no deficit for the
topocentric shadow either.

### Altitude scan (`files/results/altitude_scan.csv`, Fig. 2)

The naive z changes sign and size with altitude in an irregular way (from -9.7 at 1,000 km to +12.1 at
10,000 km). The within-plate z stays between -2.1 and +2.6 for all 54 combinations (3 catalogues, 9
altitudes, 2 shadow models). Three of 54 have |z| > 2; chance gives about 2.5. The combinations are
correlated, because the catalogues share rows and nearby altitudes share shadow regions.

### Placebo shadows (`files/results/placebo_shifts_s1.csv`, `placebo_summary_s1.json`, Fig. 3)

- The naive |z| at some placebo shift is equal to or larger than the true |z| for 64 % (geocentric) and
  29 % (topocentric) of the shifts.
- True area ratio: 0.817 (geocentric) and 0.739 (topocentric). The minimum over the 40 shifts with
  |shift| >= 18 days is 0.887 and 0.783.
- Model rho at the true time (0.56, 0.68) is below the minimum over those shifts (1.00). The
  autocorrelation of the placebo series falls to zero at 8-12 days. We count about 11 independent
  positions in the 112-day span, so a one-sided p is about 0.09.
- Shifts of -4 to +4 days overlap the true shadow. They also give low values. The profile is smooth, with
  large excursions (rho up to 2.85 at +8 days).

### Aperture of the expected fraction (`files/results/aperture_check.csv`)

With our plate log, the area expectation for the geocentric GEO cap is 0.476 % for the full usable plate
and 0.452 % for the central 2-deg circles. Doherty (2026) used 0.78 % from 2-deg circles. We cannot find
the cause of this difference without his plate table. His observed rate (0.46 % of 107,875) is near our
area expectation.

### Antisolar distance inside plates (`files/results/antisolar_within_plate.csv`)

We applied the within-plate test to "closer than s deg to the antisolar point". For s = 15-20 deg the ratio
is 0.95-0.99 (z = -0.7 to -1.6) in the three catalogues. For s = 5 deg it is 0.63-0.92 with few candidates
(z = -0.5 to -1.7; Monte Carlo p = 0.02-0.04 in S0 and S0-paper-parity, 0.83 in S1). These windows are nested and not independent. This is a weak hint of fewer detections
near the antisolar point, where the gegenschein makes the sky brighter. It is not significant.

## Method details

- **Plate log** (`platelog.py`). 935 POSSI-E plates from the STScI list. The minutes field is hundredths
  of an hour. Where the logged hour angle agrees better with the next day, the UT date is +1 day (671
  plates). 53 plates have an hour-angle residual above 2.5 min (kept). Exposure times come from VI/25
  (median 45 min; 137 plates imputed with the median). Plate XE628 is not in the STScI list, so its 56 S1
  rows are not used.
- **Geometry** (`shadow.py`). Observer at Palomar (33.356 N, 116.863 W, 1706 m), astropy GCRS. Sun from
  astropy. Spherical Earth R = 6371 km, conical umbra with the solar radius. For altitude h, a sight line
  meets the sphere of radius R + h; the point is in shadow when it is behind the Earth and closer to the
  shadow axis than the local umbra radius. We sampled 5 times across each exposure and used the fraction
  of time in shadow. The geocentric cap uses the angle asin(R_umbra/r) around the antisolar point, also
  over 5 samples. A unit test gives 9.9 deg radius at the zenith and an 8.7 deg parallax offset at the
  terminator.
- **Within-plate (D4) null.** Candidate positions in each plate frame (gnomonic, B1950 axes) are rotated by
  0, 90, 180, 270 deg or reflected. Each plate takes one of the 8 images at random and independently. The
  mean and variance are exact sums over plates. Plates fully in or fully out of the shadow give no
  information to this test.
- **Injection** (`inject.py`). We removed each candidate with probability (1 - rho) times its shadow
  fraction, 200 times for each rho from 0.30 to 1.20, and repeated the D4 test. The interval keeps the rho
  values whose median injected z is within 1.96 of the observed z.
- **Count model** (`analysis.py`). NB2 regression of plate counts on B-splines of |b| (4 df), declination
  (3 df) and year (3 df), plus |hour angle| and plate grade. The shadow enters as the offset
  log(1 + (rho - 1) A_p), with A_p the shadowed area fraction of the usable plate square (|xi|, |eta| <= 3
  deg). rho comes from the profile likelihood (dispersion refitted at each rho; for placebo shifts the
  dispersion is fixed at its rho = 1 value, which gave identical results at shift 0). The rho grid step
  was 0.02, except for placebo shifts other than 0 and -46 to -34 days, which used 0.05.
- **Placebo** (`placebo.py`, `plate_geom.py`). All plate times move by k = +-2, ..., +-56 days. An integer
  day keeps the shadow at the same place relative to the horizon and the Sun, on other stars.

## What remains open

1. Repeat the within-plate test on the private 107,875-row VASCO catalogue. This test needs only plate
   labels and positions. It is the decisive test for the reflector claim.
2. Test the plate-level deficit with plate depth: count all detected sources per plate (not only the
   candidates) as a function of distance from the antisolar point, to measure the gegenschein effect.
3. Use a larger placebo design (other years' dates, or shadows moved in hour angle) to get a better
   null for the between-plate test.
4. The injection test was not run for S0. The cross-plate deduplication of the catalogues can make the
   density near plate overlaps asymmetric; we did not model this.

## Reproduction

```
bash files/code/run_all.sh /path/to/scratch     # downloads inputs into scratch, then runs all steps
```

The scripts read `raw/` and write `out/` in the scratch folder. Python 3.12.16, numpy 2.5.4, scipy 1.18.1,
pandas 3.1.1, astropy 8.0.2, statsmodels 0.15.0, patsy 1.0.3, matplotlib 3.11.2. The full run uses about
1-2 CPU hours with 2 processes (the placebo step is the slowest). Random seeds are fixed in the code.
External data sources, licences, hashes and the required survey acknowledgement are in
`files/NOTICE-external-data.md`.

## Relation to earlier work

The campaign record had no earlier publication about POSS-I transients (searches on 2026-11-12). This work
is new in three points: (1) it uses three large public catalogues (95,770-134,899 rows) instead of the
5,399-row list; (2) it uses the topocentric shadow and an altitude scan; (3) it separates the within-plate
and between-plate parts of the deficit and calibrates both with injection and placebo tests.
