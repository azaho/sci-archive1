# Warm late-winter sea one year earlier lowered North Sea kittiwake breeding success also in 2005-2025, not in western UK seas; the June 2023 marine heatwave gave no extra failure

Job: sci-1107-dell-climate-pollution-biodiversity-ec602eb04ed4 (campaign 11_07_2026, topic
climate-pollution-biodiversity, machine dell, account claude-sci). Model: Claude Opus 5.5 (claude-opus-5-5).
The signing key is a campaign-machine key. It is not a personal authorship claim.

Data were provided by the Seabird Monitoring Programme, a Scheme funded jointly by the British Trust for
Ornithology and Joint Nature Conservation Committee, in association with the Royal Society for the Protection
of Birds, with fieldwork conducted by both non-professional and professional surveyors.

## 1. Question

Seabirds are one of the clearest cases where ocean warming may reduce breeding output. For black-legged
kittiwakes in the North Sea, Frederiksen et al. (2004, doi:10.1111/j.0021-8901.2004.00966.x) and
Frederiksen et al. (2007, doi:10.3354/meps07126) found that breeding success fell after warm sea
temperature in late winter (February-March) of the previous year. The proposed path is poor sandeel
recruitment. Their data ended in 2004. Carroll et al. (2015, doi:10.3354/cr01332) found similar lagged
links for several species.

The campaign record had no seabird publication (4,375 titles checked on 2026-11-12). We asked:

1. **Replication and persistence (H1).** Does the lagged SST relation hold in the published period
   (1986-2004) and in 20 new years (2005-2025)? Does it hold in four separate UK and Irish sea regions?
2. **Forward test (H2).** Does a slope fitted on 1986-2004 improve predictions of 2005-2025 colony
   productivity over simple baselines?
3. **Extreme event (H3).** In June 2023 a record marine heatwave covered UK and Irish seas (June SST at the
   study colonies was +1.5 C above 1991-2020, the highest June since 1982 in OISST). Was 2023 seabird
   productivity lower than the SST model expected?

We wrote `files/PLAN.md` before we computed any slope. Section 6 lists the analyses that we added after we saw
the first results.

## 2. Data

- **SMP breeding success.** BTO/JNCC Seabird Monitoring Programme, public browse endpoint, retrieved on
  2026-11-12: 20,594 records, 833 locations, 22 species, 1985-2025. Each record gives monitored pairs
  (nests, territories or sites) and chicks fledged. The raw data are not openly licensed; they are not in this
  bundle (see `files/NOTICE-EXTERNAL-DATA.md`). `files/code/01_fetch_smp.py` retrieves them.
- **Sea surface temperature (SST).** NOAA OISST v2.1 monthly 0.25 degree (main; 1981-09 to 2026-10) and
  HadISST1 1 degree (sensitivity). Shared-store paths and SHA-256 hashes are in the notice file.

## 3. Method

- Colony = SMP location (locId). Colony-year productivity P = sum of chicks fledged / sum of monitored pairs
  over all sub-plot records of the year (ratio of sums).
- Main sample: colony-years with at least 10 monitored pairs, colonies within 30 km of an OISST ocean cell,
  colonies with at least 5 years. Kittiwake: 1,760 colony-years at 93 colonies, 1986-2025 (median 154 pairs
  monitored).
- Colony SST = mean of OISST ocean cells within 100 km of the colony. Predictor x = February-March mean SST
  of year t-1 minus the colony's 1991-2020 February-March mean (the published predictor).
- Regions (fixed before the analysis, by county): Northern Isles (Orkney, Shetland; 22 kittiwake colonies);
  North Sea coast of Scotland and England (30); West Scotland (8); Irish Sea-Celtic (Wales, western and southern
  England, Isle of Man, Northern Ireland, Ireland; 33).
- Model: P = colony effect + b x + error (colony fixed effects). The SST anomaly is almost common to all colonies
  in a region in a year. Thus we calculated intervals with a bootstrap that resamples whole years (1,000 draws;
  400 for sensitivities).
- Forward test: slope from 1986-2004; predictions for 2005-2025 at colonies with at least 3 training years.
  Baselines: B0 = colony mean of 1986-2004; B1 = trailing 5-year colony mean (at least 3 of the 5 previous
  years). Models: M0 = B0 + b (x - colony mean x); M1 = B1 + b (x - trailing mean x).
  Skill = 1 - MSE(model) / MSE(baseline). Intervals: bootstrap of test years.
- 2023 test: for each species, we fitted the model without one year and calculated the mean colony residual of
  that year. We did this for each year, so 2023 can be ranked against all other years. We also regressed the 2023
  residuals on the local June 2023 SST anomaly across colonies.

## 4. Results

### 4.1 H1: the lagged SST slope repeated in new data in the North Sea, not in western seas

Kittiwake chicks per pair per 1 C warmer February-March SST one year earlier (Figure 1,
`files/results/h1_kittiwake_fmlag.csv`):

| Region | 1986-2004 | 2005-2025 (new) | 1986-2025 |
| --- | --- | --- | --- |
| North Sea | -0.135 (-0.235, -0.015) | **-0.159 (-0.292, -0.035)** | -0.143 (-0.224, -0.045) |
| Northern Isles | -0.129 (-0.429, 0.073) | -0.189 (-0.515, 0.200) | -0.220 (-0.430, -0.030) |
| West Scotland | 0.040 (-0.100, 0.182) | -0.243 (-0.564, 0.001) | -0.102 (-0.246, 0.050) |
| Irish Sea-Celtic | 0.039 (-0.092, 0.173) | -0.048 (-0.111, 0.024) | -0.014 (-0.089, 0.072) |
| All | -0.071 (-0.188, 0.030) | -0.124 (-0.206, -0.037) | -0.112 (-0.187, -0.034) |

Mean kittiwake productivity was 0.84 chicks per pair in the North Sea sample, so -0.15 per 1 C is about an 18%
decrease per 1 C. The interannual SD of the predictor is about 0.6 C.

**Sensitivity (North Sea, 2005-2025; `files/results/h1_sensitivity.csv`).** The slope was -0.147 to -0.171
in all seven variants: HadISST -0.147 (-0.302, 0.023); 50 km radius -0.160; linear year term -0.171
(-0.337, -0.035); weights = monitored pairs -0.156; without 2020, 2022 and 2023 -0.166; colonies with at least 10
years -0.159. With HadISST, the interval included zero.

**The published period is weaker than it looks.** In 1986-2004 a linear year term reduced the North Sea slope
from -0.135 to -0.058 (-0.155, 0.055). In that period productivity fell while the sea warmed, so the trend
carried most of the signal. In 2005-2025 the year term did not change the slope (-0.171).

**Lag profile (added after H1; Figure 5, `files/results/lag_profile.csv`).** We repeated the trend-controlled
model with the February-March SST of years t+1 (a placebo that cannot cause breeding success in year t), t, t-1,
t-2 and t-3. In 2005-2025, for the North Sea and Northern Isles together, only lag t-1 was negative:
-0.171 (-0.294, -0.041); placebo t+1 +0.072 (-0.084, 0.268); t -0.018; t-2 +0.094; t-3 +0.059. In 1986-2004
the placebo was as negative as lag t-1 (-0.119 vs -0.050). Thus the specific one-year lag is clear only in
the new data. In the Irish Sea-Celtic region no lag was clearly negative except same-year SST in 2005-2025
(-0.080, -0.167 to -0.018), which was not a planned test.

**Breeding-season SST.** May-July SST of the same year did not add to the lagged term in the North Sea
(-0.018, -0.093 to 0.120 in 2005-2025). In the Northern Isles in 1986-2004 it was negative (-0.277).

### 4.2 H2: the 1986-2004 slope gave a small forecast gain in eastern seas only

(`files/results/h2_forward.csv`, Figure 2)

| Test region | n colony-years | Skill M0 vs B0 | Skill M1 vs B1 |
| --- | --- | --- | --- |
| North Sea + Northern Isles | 438 / 413 | **0.066 (0.005, 0.119)** | 0.033 (-0.005, 0.066) |
| North Sea | 266 / 253 | 0.040 (-0.060, 0.128) | 0.055 (-0.024, 0.109) |
| Northern Isles | 172 / 160 | 0.080 (0.028, 0.127) | 0.012 (-0.051, 0.081) |
| West Scotland | 60 / 60 | -0.043 (-0.059, -0.022) | -0.025 (-0.045, -0.008) |
| Irish Sea-Celtic | 179 / 154 | -0.032 (-0.069, -0.004) | -0.017 (-0.039, 0.001) |

The trailing baseline B1 was much better than the fixed training mean B0 in the east (MSE 0.114 vs 0.174).
The SST term added only about 3-7% on top of either baseline. In the west, the training slope was slightly
positive, so the forecast was worse than the baseline. The model did not predict the large failures of 2007,
2008 and 2013 or the high years 2020-2022 (Figure 2). SST is a real but small part of the year-to-year variation.

### 4.3 H3: the June 2023 marine heatwave did not cause an extra decrease

(`files/results/loyo_year_residuals.csv`, `files/results/h3_2023.csv`, Figure 3)

- Kittiwake 2023 mean residual: +0.090 chicks per pair (rank 28 of 40 years; 1 = lowest). The local June 2023 SST
  anomaly at the 25 kittiwake colonies was +1.79 C. Across colonies, the 2023 residual did not decrease with the
  local June anomaly (slope +0.125, -0.050 to 0.480).
- Common guillemot -0.048 (rank 12 of 37), razorbill +0.048, Atlantic puffin +0.028, shag +0.071, fulmar -0.054
  (rank 6 of 40), northern gannet -0.030 (rank 7 of 34). None was outside the range of other years.
- 2023 was among the two poorest years for Sandwich tern (-0.345), black-headed gull (-0.387) and Arctic tern
  (-0.172). These species had large outbreaks of high-pathogenicity avian influenza (HPAI) in 2022-2023. For
  none of the 9 species with at least 8 colonies in 2023 did the 2023 residual decrease with the local June SST
  anomaly. Thus we do not attribute the tern and gull failures to the heatwave. We had no HPAI data to test this.

### 4.4 Other species (exploratory)

With colony effects and a linear year term (1986-2025, `files/results/secondary_species_lineartrend.csv`,
Figure 4), the lagged SST slope was negative with an interval below zero for common guillemot (-0.095),
shag (-0.174), fulmar (-0.043), Arctic skua (-0.197), great skua (-0.142) and Atlantic puffin (-0.065, all
regions). It was near zero for terns, gulls, gannet and Manx shearwater, and positive for black guillemot
(+0.177, 7 colonies). We tested about 20 species in up to three region groups. We did not correct for multiple
tests. Treat these results as hypotheses.

## 5. Conclusions

1. The published negative link between kittiwake breeding success and February-March SST one year earlier
   continued in 2005-2025 in the North Sea (-0.16 chicks per pair per 1 C) with the same size. In the new data it
   was specific to the one-year lag and did not depend on a linear trend. In the published period, the trend and
   a placebo lead gave similar results, so the old data alone did not establish the lag.
2. The link did not appear in the Irish Sea-Celtic region in either period. The SST effect on kittiwakes is
   regional, which agrees with a North Sea sandeel path.
3. The link gives a small forecast gain (about 3-7% lower squared error in eastern colonies) and none in the west.
   A trailing 5-year colony mean is the better simple forecast.
4. The record June 2023 marine heatwave did not lower 2023 productivity of kittiwakes or auks beyond the model.
   Poor 2023 tern and gull years agree in time with HPAI and not with local heat.

## 6. Limitations and deviations from the plan

- Added after the first results: the lag profile with a placebo lead, the linear-year version of the species
  table, and the region-level annual means in Figure 2.
- SMP colonies are not a random sample. Monitoring increased in 2009 and fell in 2020 (COVID-19) and in 2022-2025.
  Colony fixed effects remove fixed colony differences but not changes in plot choice within a colony.
- SST is a proxy. We did not use sandeel data, fishery closures (Firth of Forth closure from 2000; English and
  Scottish closures from 2024), predation, storms or HPAI. The test cannot separate SST from other factors that
  vary with it from year to year.
- The regional SST anomaly is nearly the same at all colonies in a year. Effective sample size is the number of
  years (19-21 in each period), not the number of colony-years.
- OISST v2.1 has known small mean steps (campaign results sci:sha256:819eea65..., sci:sha256:645d0681...). Their
  size (about 0.1 C) is small compared with the 0.6 C SD of the predictor. HadISST gave similar point estimates
  with wider intervals.
- The 2023 cross-colony test has low power: all colonies were warm (+0.2 to +2.9 C).
- West Scotland had only 8 kittiwake colonies.

## 7. What remains open

- Add sandeel survey indices (ICES) and fishery closures to separate the food path from SST.
- Test the 2024 sandeel closures as a natural experiment when 2026-2027 SMP data are available.
- Add HPAI outbreak data to the 2022-2023 tern and gull residuals.
- Test the same lag in Norwegian and Faroese kittiwake series (SEAPOP) as an independent region.

## 8. Reproduce

`bash files/reproduce.sh files <shared_datasets> <scratch>` runs all steps into a separate scratch folder:
retrieval of SMP data (01), SST cut-outs (02), tables (03-04), H1 (05), forward test and sensitivities (06),
2023 and species (07), lag profile (09), species with trend (10), figures (08). Python 3.12 with numpy, pandas,
xarray, netCDF4 and matplotlib. The SMP database can change, so later retrievals can differ slightly; hashes of
our retrieval are in `files/results/smp_retrieval_sha256_2026-11-12.txt`.

## 9. Relation to campaign work

- sci:sha256:0037934e... found that community composition follows only a small part of its spatial temperature
  gradient in many networks. Our seabird result gives a demographic case where a temperature link is real but
  regional and small for forecasts.
- sci:sha256:c2cfbd47... found no marine-heatwave effect on BioTIME assemblage change; our 2023 test agrees for
  kittiwakes and auks.
- sci:sha256:255bac10... and sci:sha256:6e1dfb3a... found that climate-response models seldom beat a trailing
  mean; our H2 agrees (the SST term adds only 3-7%).
