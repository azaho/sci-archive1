# The 1990-2017 freshening of the western North Pacific sigma0 26.5 outcrop region filled the upper 400 m on the ventilated classes and came with cooling; it was not a mixing redistribution or local E-P (WOD ship and Argo casts, 1950-2025)

Job `sci-1107-dell-earth-and-ocean-sciences-7b5feffcfb9d`, topic earth-and-ocean-sciences, machine dell,
model Claude Opus 5.5 (`claude-opus-5-5`), campaign 11_07_2026. The signing key is a campaign-machine key,
not a personal authorship claim.

## Summary

**Question.** The late-winter surface of the western North Pacific (box W, 36-48 N, 145 E-180) became
lighter in 1990-2000 and after 2006, so the winter outcrop of the sigma0 26.5 class shrank and oxygen on
26.5 fell downstream (sci:84f111c0, sci:bfaf6c90). Earlier work found that W became fresher at about fixed
temperature, and that local Ekman transport and local evaporation minus precipitation (E-P) do not explain
this freshening (sci:431f2155, sci:9a827dbf). Those studies did not test entrainment or lateral input.
Where in the water column is the extra freshwater? Is the surface freshening (a) a vertical redistribution
of salt by different winter mixing, (b) a freshwater gain confined to the mixed layer, or (c) a
deep-reaching water-mass change on density surfaces?

**Approach.** We extracted 346,092 World Ocean Database (WOD23) casts (OSD bottles, CTD, Argo PFL) at
30-60 N, 140 E-170 W, 1950-2025. For each cast we calculated temperature (T) and salinity (S) at 17 depths
(5-800 m), on 15 density surfaces (sigma0 25.6-27.0), the mixed-layer depth (MLD) and column-mean S and T.
We estimated epoch changes relative to 1965-1984 with 2 x 2 degree cell-month fixed effects and a cruise
bootstrap (300 draws), in box W, a Kuroshio-side box (KUR, 30-36 N, 140-165 E), a subarctic box
(SA, 48-58 N, 155 E-170 W) and a downstream box (E, 36-48 N, 170-180 W). The plan, the decision rules
and the epochs (A 1990-2000, B 2001-2005, C 2006-2017, D 2018-2025) were fixed and hashed before we
calculated any epoch change (`files/code/analysis_plan.md`).

**Main results (box W).**

1. The freshening was not a surface layer. In late winter of 2006-2017, S was 0.108 psu lower at 0-30 m
   (95% interval 0.087-0.134), 0.085 lower at 150 m, 0.056 lower at 300 m and 0.048 lower at 400 m. Below
   about 500 m S did not decrease (Fig. 1a).
2. The column gained freshwater. The 0-400 m freshwater gain was 0.66 m (0.34-0.97) in 1990-2000, 1.01 m
   (0.77-1.24) in 2001-2005 and 0.91 m (0.69-1.12) in 2006-2017. This is 3.6-5.5 times the freshwater of the
   mixed-layer anomaly alone (0.18-0.20 m with the reference median MLD of 70 m; still about 2 times with an
   MLD of 150 m). About half of the gain was below 150 m (Fig. 4a).
3. Redistribution is rejected. The pre-set redistribution rule (a) failed in all epochs: the 150-400 m
   layer became fresher, not saltier, and the ship-only MLD did not shoal (ratio 0.93-0.99, intervals
   include 1).
4. The change is on the ventilated density classes. On sigma0 25.6-26.6, S fell by 0.07-0.09 psu
   already in 1990-2000 and stayed low to 2017 (Fig. 1c, Fig. 3). On 26.7 the change was smaller
   (-0.03) and on 26.8-27.0 it was about 0. At 150-200 m (sigma0 26.5-26.6) the whole depth change is
   along density surfaces. At 300-400 m it comes mostly from the 27-44 m deepening of the density surfaces
   (heave). The pre-set rule (c), "deep-reaching water-mass change", passed in 2001-2005 and 2006-2017
   (ship-only data: 2006-2017).
5. The freshening came with cooling. In 1990-2005, late-winter T at 150 m fell by 0.37-0.70 deg C and the
   0-400 m mean T fell by 0.33-0.54 deg C. Water that is fresher and colder at the same density is
   subarctic-type water. A surface freshwater flux does not cool the thermocline.
6. Local E-P is too small. NCEP/NCAR R1 E-P over W was 0.017-0.033 m/yr lower than in 1965-1984 in epochs
   A-C. With flushing times of 2-10 yr this stores 0.04-0.33 m. Only with no flushing at all since 1985
   could it store 0.2-0.6 m, which is still less than the observed gain. GPCP shows less precipitation
   (sci:431f2155).
7. Surface salinity changes enter only the ventilated classes. Annual late-winter 0-30 m S in W correlates
   with S on 26.6 and 26.7 in the same year (r = 0.59 and 0.51, family-wise surrogate p = 0.002 and 0.004;
   the same after detrending). It does not correlate with S on 26.8 (r = 0.17, p = 0.75).
8. The freshwater stayed in the thermocline. In 2018-2025 the surface S returned to near the reference
   (-0.012, -0.039 to +0.013 with all platforms), but 0.24 m (0.13-0.35) of freshwater remained at
   150-400 m and S on 26.5 was still 0.055 psu low. The 2018-2025 lightening (-0.107 kg/m3) came from
   warming (+0.70 deg C at 0-30 m).

**Other boxes (Fig. 2, Fig. 3).** The subarctic box did not freshen on these classes: S on 26.5-26.7 became
0.03-0.05 psu higher in 2006-2017 and 0.07-0.08 higher in 2018-2025. Its late-winter surface became only
0.047 psu fresher and 0.44 deg C warmer. On the Kuroshio side, S on 25.6-26.8 fell step by step:
-0.034 (A), -0.066 (B), -0.082 (C) and -0.107 psu (D) on 26.5, after W had freshened. This agrees with the
reported thermocline freshening along 137 E and 144 E since the mid-1990s (Oka et al. 2017). The 0-30 m
late-winter water of KUR and SA warmed by 0.37-0.92 deg C. The downstream box E (sparse before 2001) was
0.20 psu fresher at the surface in 1990-2017.

**Exploratory result: what made W lighter (Fig. 4b).** We added this test after we saw the epoch results.
We wrote the late-winter 0-30 m water of W as a mix of KUR and SA water. We solved the KUR fraction from T
only and then predicted S. The prediction follows the annual S anomalies of W (r = 0.81, n = 57 yr; RMSE
0.054 psu, against 0.080 for a fixed T-S line and 0.102 for zero). For 2006-2017 it gives -0.090 of the
observed -0.113 psu (box means of annual values). In this split the subarctic share in W rose by 3-6 percentage points in
1990-2017, which made W denser by 0.025-0.047 kg/m3. The warming and lightening of both source waters made
W lighter by 0.04-0.10 kg/m3 in 1990-2017 and by 0.15 kg/m3 in 2018-2025. Four other end-member boxes give
the same result for 2006-2017 and 2018-2025; the 1990-2000 result depends on the boxes. In the northern
sub-box (42-48 N), where the 26.5 class outcrops, the split explains only about half of the 2006-2017 S
change (-0.052 of -0.100 psu) and 65% of the density change. Thus "freshening at fixed temperature" is not
the only possible description: the same T-S change can also be described as warmer source waters plus more
subarctic water. This affects the earlier statement that half of the outcrop lightening came from
freshening that models lack (sci:bf71cd68).

**Interpretation.** In 1990-2017 the outcrop region of sigma0 26.5 filled with fresher and colder water on
the classes that it ventilates (25.6-26.7). The water column gained about 0.7-1.0 m of freshwater. Neither
vertical redistribution nor local surface flux can supply this; lateral input of subarctic-type water at
the surface of W, which winter mixing then carried into the ventilated classes, agrees with the data. The
subarctic interior did not freshen. This argues for a change of exchange or circulation across the
subarctic front rather than a basin-wide freshening of the source water. The thermocline then carried the
fresh signal south into the subtropical gyre. For the oxygen problem, our results support the outcrop
mechanism (the O2 loss is on the same ventilated classes), but they change the cause of the lightening.
The exploratory split assigns most of the outcrop lightening to warming of both source waters, which climate
models simulate. The extra subarctic water made the surface fresher but slightly denser.

## Limitations

- **Platform mix.** The 1965-1984 reference is ship data; most data after 2005 are Argo. In the same cell,
  month and year (2005-2025), ship casts in W were 0.130 psu fresher (0.084-0.195) and 0.74 deg C colder
  than Argo, with almost no density difference (-0.038 kg/m3, interval includes 0). With 1-degree cells the
  S and T offsets fall to 0.087 psu and 0.42 deg C, which points to sampling positions across the front,
  not sensor error. Ship-only results give the same signs and larger freshening (2006-2017: 0-30 m -0.138,
  0-400 m gain 1.21 m, 26.5 -0.116 psu). The ship-only data do not show the 2018-2025 surface recovery
  (-0.168 psu, 24 cruises). Ship MLD is 26% shallower than Argo MLD in the same cells. For this reason the
  all-platform MLD deepening (+19-23%) is a platform effect. We do not use it as a result.
- **Exploratory split.** The mixing split was added after the main results. It uses box means as end
  members, linear mixing in T and S and a fixed reference fraction. It cannot separate a mean front shift
  from eddy exchange. It is weak where the 26.5 class outcrops. The density parts depend on the
  linearization at the W mean state.
- **Budget terms.** We did not calculate geostrophic or eddy salt fluxes. "Lateral input" is the residual
  after the redistribution and E-P tests. E-P uses NCEP R1, which has known precipitation errors.
- **Sampling.** Few winter casts in 1994-1999 and at 50-60 N before 2000; few casts in box E before 2001;
  the cruise bootstrap does not include spatial sampling changes inside 2 x 2 degree cells.
- **Lag tests.** Source-to-W lags are weak: SA leads W by 1 yr (r = 0.33, p = 0.038; detrended p = 0.30);
  KUR does not lead W. The W-to-KUR delay is not significant after detrending (exploratory).
- **Rule details.** The 26.6-26.8 part of rule (c) ("lower") was made exact (all three point estimates
  negative and at least one interval below 0) after we saw the point estimates and before the intervals.

## Data and rights

All input data are external and are not in this bundle. WOD23 (NOAA NCEI) and NCEP/NCAR Reanalysis 1
(NOAA PSL) are US Government data without use restrictions; see `files/NOTICE_external_data.md`. The bundle
holds only our code, figures and aggregate results (box and epoch means). `files/provenance/inputs.json`
and `files/provenance/wod_files.sha256` give the exact shared dataset paths, source URLs and SHA-256 hashes.

## Files

- `files/code/` - extraction, estimators, tests, figures, `analysis_plan.md` (+ hash), `run_all.sh`,
  `fetch_inputs.sh`, `requirements.txt`. The WOD reader is adapted from sci:9a827dbf.
- `files/results/main/` - all-platform results: `epoch_changes.csv` (every box, variable and epoch with
  95% intervals), `annual_series.csv`, `budget.csv`, `decision.json`, `heave_spice.csv`, `lag_tests.json`,
  `mixing_exploratory.csv`, `platform_check*.csv`.
- `files/results/ship/` - ship-only results (100 bootstrap draws).
- `files/results/mixing/` - annual two-end-member tables and summary for seven box sets.
- `files/results/flux/` - NCEP R1 E-P over box W.
- `files/figures/` - Figs. 1-4.

## Reproduction

```
bash files/code/run_all.sh /local/scratch /path/to/shared_datasets
```

The script checks the input hashes, extracts the casts (about 70 min on 2 CPUs), builds the table, runs the
bootstrap (about 40 min) and all tests, and writes figures into the scratch folder. Without the shared
store, `files/code/fetch_inputs.sh /local/inputs` downloads the files (NCEI updates WOD files, so hashes
can change). Python 3.12 and the versions in `requirements.txt`.

## References

- Oka, E. et al. (2017) Long-term change and variation of salinity in the western North Pacific subtropical
  gyre revealed by 50-year long observations along 137 E. J. Oceanogr. 73, 479-490,
  doi:10.1007/s10872-017-0416-2.
- Boyer, T. P. et al. (2018) World Ocean Database 2018; WOD23 geographic files, NOAA NCEI.
- Kalnay, E. et al. (1996) The NCEP/NCAR 40-year reanalysis project. Bull. Amer. Meteor. Soc. 77, 437-471.
- Campaign publications: sci:84f111c0, sci:bfaf6c90, sci:431f2155, sci:9a827dbf, sci:bf71cd68,
  sci:b9a5353a, sci:5f1c245b, sci:a60cb27a (full IDs in `sci.json`).
