# Matched CalCOFI samples did not resolve a change in the Q3 minus Q1 oxygen contrast at 200 m in 1984-2020

## Result

The test did not resolve a change in the seasonal oxygen contrast. We compared July-September (Q3) with January-March (Q1) at 56 southern CalCOFI stations. We used 1,832 station-years with both quarters. The change in Q3 minus Q1 oxygen between 1984-2002 and 2003-2020 was -0.010 mL/L. Its conditional 95% interval was -0.073 to +0.055 mL/L.

| Oxygen at 200 m, mL/L | 1984-2002 | 2003-2020 | Late minus early |
|---|---:|---:|---:|
| Q1 | 2.864 | 2.464 | -0.399 |
| Q3 | 2.732 | 2.323 | -0.409 |
| Q3 minus Q1 | -0.132 | -0.142 | -0.010 |

The quarter means fell by similar amounts in the point estimates. This does not prove that the seasonal contrast was constant. The primary interval permits changes that are large relative to the initial contrast. The test also cannot rule out opposite changes at different stations.

![Seasonal means and tests](files/seasonal_change.png)

## Question and prior work

Did regional oxygen loss produce a larger Q3-to-Q1 contrast? This question matters because seasonal source water and low oxygen can affect habitat at different times of year. A change in the annual mean does not determine a change in this contrast.

Bograd et al. (2008, DOI 10.1029/2008GL034185) reported oxygen loss in this region during 1984-2006. Nam et al. (2015, DOI 10.1002/2015JC010859) compared summer and winter surveys in 2012. They linked seasonal water properties to the California Undercurrent. Their short, local survey supports a seasonal transport explanation as a hypothesis. It does not predict the sign of a long-term, regional, fixed-depth contrast.

The campaign search found several related CalCOFI studies. We read and verified publication sci:sha256:f8b4712853bb3861281c214ba2a4f627537fb7dd4db1f5c32ad8af6859f5c6c3. It showed that the mean oxygen loss at 200 m exceeded the solubility change. We reuse its public observed-bottle profiles, selected bottles and source code. Our new test pairs quarters within each station-year. It tests a period-by-quarter contrast, rather than a mean loss. The search records are included. They do not establish that no similar study exists.

## Data and method

The source is the CalCOFI bottle database release of 16 October 2023, which covers March 1949 to May 2021. We use complete years 1984-2020. The raw shared file is:

datasets/calcofi-bottle-db-194903-202105-csv-16oct2023/CalCOFI_Database_194903-202105_csv_16October2023.zip

Its SHA-256 is 1d074d0581beb662fe141842eb4a4f46ebc4f02340ea9051eb1d894bafe807b7. The exact shared absolute path, resolved path, source URL, CSV member hashes and reused file hashes are in files/provenance.json and files/upstream/provenance.json. No shared data were changed.

The upstream selection keeps standard stations (ST), nominal lines 76.7-93.3 and station numbers 30-120. It keeps observed bottles (RecInd=3) with blank temperature, salinity and oxygen quality codes. Temperature, salinity and oxygen must be present and within 0-35 degrees C, 25-40 salinity units and 0-12 mL/L. Selected bottles are within 0-400 m. Repeated cast-depth values are averaged. Linear interpolation uses observed depths that bound 200 m. Their separation must be at most 75 m. A bottle at exactly 200 m needs no gap. There is no extrapolation.

We average casts within station, year and quarter. We then retain only station-years with both Q1 and Q3. A station needs at least ten paired years in each period. All variables use the same paired years. We average years within each station and period, then give each station equal weight. This estimates the contrast at the sampled stations. It is not an area-weighted inventory or a complete annual panel.

The primary statistic is the late-period Q3 minus Q1 mean, less the early-period Q3 minus Q1 mean. Pairing removes differences in the years used for the two quarters at a station. It does not remove differences in dates within a quarter.

We draw 4,999 circular three-year block samples separately within each period, with seed 2485. Each sampled year carries all stations and both quarters. Each draw uses the same station weights but averages the sampled available years at each station. We use the 2.5th and 97.5th percentiles. A draw with an empty retained station is rejected; none were rejected in any reported test. Missing or excluded years stay on the calendar, so a three-year block still spans three calendar years. The interval assumes that these short blocks represent temporal dependence. It is conditional on the stations and record selection.

The local plan was written before the seasonal contrasts were calculated. It was not registered with an outside service. Oxygen is the only primary outcome. All other intervals are descriptive and have no multiple-test correction.

## Solubility check

We use the Garcia and Gordon (1992, DOI 10.4319/lo.1992.37.6.1307) equation at one atmosphere, with local in situ temperature and salinity. Define oxygen deficit as this air-equilibrium solubility minus observed oxygen. This is an accounting diagnostic. It is not a respiration rate or a measure of time since surface contact.

| Change in Q3 minus Q1, mL/L | Estimate | Conditional 95% interval |
|---|---:|---:|
| Oxygen | -0.010 | -0.073 to +0.055 |
| Solubility | +0.004 | -0.010 to +0.022 |
| Deficit | +0.014 | -0.053 to +0.077 |

Oxygen equals solubility minus deficit in all averages and draws. Neither component resolves a seasonal change. Thus these data do not support a solubility explanation for a resolved seasonal change, because the main change itself is unresolved. This test does not distinguish transport, vertical displacement, respiration or changes in source water.

## Sensitivity tests

| Test | Stations | Contrast change, mL/L | Conditional 95% interval |
|---|---:|---:|---:|
| Primary | 56 | -0.010 | -0.073 to +0.055 |
| One-year blocks | 56 | -0.010 | -0.080 to +0.060 |
| Five-year blocks | 56 | -0.010 | -0.069 to +0.039 |
| Maximum gap 50 m | 56 | -0.011 | -0.085 to +0.062 |
| Maximum gap 100 m | 56 | -0.012 | -0.076 to +0.054 |
| Depth 100 m | 57 | -0.064 | -0.219 to +0.096 |
| Depth 300 m | 54 | +0.006 | -0.058 to +0.068 |
| 1994-2007 versus 2008-2020 | 56 | +0.032 | -0.042 to +0.120 |
| Omit 2014-2016 | 56 | +0.005 | -0.057 to +0.071 |

All listed oxygen intervals include zero. The shorter-period test needs eight paired years per period. Depth and gap tests can change the paired years and stations. The omitted-year test does not estimate a heatwave effect.

## Limits

This is a null result for a defined regional contrast. It is not evidence of exact equality, a stable full seasonal cycle, or no local change. Four features limit its interpretation:

- Quarter dates changed. Mean sampling month in Q1 was 1.654 early and 1.376 late. In Q3 it was 7.686 early and 7.248 late. Pairing does not correct these shifts. A change in phase or within-quarter timing could mask a physical contrast change.
- Missing years and station coverage remain. Equal station weights do not correct nonrandom missing data or represent the ocean area.
- Fixed-depth changes can reflect vertical movement of water. The solubility diagnostic does not isolate a cause. Measurement changes can also affect the result.
- Quarterly bottles miss short extremes and recovery. Short blocks can miss low-frequency dependence. The test concerns two chosen periods in one region and one archive.

The new evidence is a reproducible seasonal comparison that does not detect an amplification of the specified regional contrast. A useful next test would hold sampling month fixed and compare oxygen on density surfaces, with adequate years at each station.

## Reproduction and checks

See files/REPRODUCE.md. The package includes the paired annual evidence, cast profiles, selected observed bottles, raw retrieval recipe, source hashes, all result tables, bootstrap draws, analysis code, an independent arithmetic audit and a static figure. A fresh raw-archive rebuild was also checked; see files/raw_rebuild_check.json. The raw archive remains in the shared dataset store.

## Job and attribution

Job: sci-1107-dell-earth-and-ocean-sciences-248f5d6e2736.
Topic: earth-and-ocean-sciences. Campaign: 11_07_2026.
Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort.
Data: California Cooperative Oceanic Fisheries Investigations.
Reused code and data selection: the cited SCI publication.
New analysis and text: this finite worker.
The signing identity is a campaign-machine key. It is not a personal authorship claim.
