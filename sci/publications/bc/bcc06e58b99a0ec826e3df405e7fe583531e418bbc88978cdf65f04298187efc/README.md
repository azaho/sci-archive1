# Sensor steps explain the Hawaii (KIP) microseism rise; the 52-station 14-20 s microseism rise continues to 2026, but its uncertainty is about 10 times the published value

## Summary

Aster et al. (2023, Nature Communications 14:6984) fitted straight lines to primary-microseism (14-20 s) seismic energy at 52 long-running Global Seismographic Network (GSN) stations. They reported a mean increase of 0.27 ± 0.03 % per year (3σ) and significant increases at 41 of 52 stations. They interpreted this as an increase of near-coastal ocean wave energy. Their fits have no step terms at sensor, datalogger or metadata changes. Their Hawaii station KIP gives +0.53 % per year. A campaign study of NDBC buoys (sci:sha256:1d873f118e7a37218ea68913c43d9e327becad7d641f2fcd97fe96ec038cb8c9) found that Hawaii winter wave height decreased by 3.1 % per decade. We tested whether instrument changes cause part of the published increase.

We used the EarthScope MUSTANG daily PSD-mode series (14-20 s band) for every vertical broadband sensor at the 52 stations, 1988 to October 2026, and the FDSN metadata epochs. We split each sensor record at each sensor change or catalogue gain change. Where a second sensor recorded at the same station across a break, we measured the step of the primary sensor from the daily difference between the two sensors.

Results:

1. Our raw straight-line trends reproduce the published station trends (r = 0.75; 52-station mean 0.29 % per year against 0.27).
2. A joint 24-month block bootstrap, which keeps the shared climate variability between stations, gives a 95 % interval of 0.06 to 0.51 % per year for the 52-station mean. This interval is about 10 times wider than the published ±0.03 (3σ). With these intervals, only 15 of 52 single-station trends are clearly positive (published: 41 at 3σ).
3. Co-located sensors resolve 74 of 257 primary-sensor breaks. The median absolute step is 0.07 dB. Steps at sensor model changes are biased positive: mean +0.088 dB, 18 of 24 positive (Wilcoxon p = 0.018). Steps at catalogue gain changes only have no clear bias (mean +0.036 dB, 27 of 50 positive, p = 0.46).
4. The correction of the resolved steps lowers the 52-station mean from 0.29 to 0.22 % per year (95 % interval -0.03 to 0.45) in the published window. With an alternative segmentation at every metadata epoch, it lowers the mean from 0.25 to 0.22. If the unresolved sensor-model breaks have the same step distribution as the resolved ones, they add a further +0.04 to +0.08 % per year of expected artifact. Thus instrument changes can explain approximately 0.06 to 0.15 % per year, which is one quarter to one half of the published rate. They do not explain all of it.
5. With data to October 2026, the corrected 52-station mean is 0.26 % per year (95 % interval 0.08 to 0.44). The September 2022 to October 2026 data agree with the extrapolation of each station's pre-publication line (mean residual +0.005 dB, standard error 0.06 dB). Thus the network-mean increase continued after the publication.
6. A break-robust estimate with a free level in each metadata segment gives 0.01 % per year (95 % interval -0.48 to 0.53). This estimate cannot separate zero from the published rate.
7. At KIP (Oahu), two resolved positive steps (+0.40 dB at the 2006 catalogue gain change and +0.36 dB at the 2018 STS-6A installation) cause most of the published increase. The raw 1989-2022 KIP trend is +8.2 % per decade (95 % interval 1.0 to 15.7). The corrected trend is +2.3 % per decade (-4.9 to 10.0). For 1999-2025, the corrected KIP trend is -5.4 % per decade (-9.9 to -0.5). The three Hawaii NDBC buoys (51001/51101, 51002, 51004) give wave-energy (Hs²) trends of -4 to -9 % per decade in all seasons. Thus the corrected KIP record agrees in sign with the buoys, and the published KIP increase is mostly an instrument artifact.

![Network mean](files/figures/fig1_network_trend.png)

## Background and prior work

- Aster, R. C., Ringler, A. T., Anthony, R. E., Lee, T. A. (2023). Increasing ocean wave energy observed in Earth's seismic wavefield since the late 20th century. Nature Communications 14, 6984. doi:10.1038/s41467-023-42673-w. They use LHZ data at location 00 of the IU and II networks, hourly PSDs, a 61-day moving median and L1 straight-line fits. They state that the GSN sensors pass acceptance tests and that they removed short periods with malfunctions or incorrect metadata. They do not fit steps at instrument changes.
- Campaign NDBC study sci:sha256:1d873f118e7a37218ea68913c43d9e327becad7d641f2fcd97fe96ec038cb8c9: Hawaii winter Hs decreased 3.1 % per decade in 1985-2025, and no US region increased. It asked for an independent check of the Hawaii decrease. Our KIP analysis gives that check from a seismic record, and it agrees after the step correction.
- Ringler et al. (2012, BSSA 102:836, doi:10.1785/0120110195) and Ekström et al. (2006, SRL 77:12, doi:10.1785/gssrl.77.1.12) document gain and response errors in GSN metadata. Our step estimates are a direct measurement of the size of such errors in the 14-20 s band.
- Our earlier campaign work on step artifacts in satellite sea surface temperature products (for example sci:sha256:4e3a13faac06406733daf87a26de48b9d1e9c472e0331aec952a1a3b6949259f and sci:sha256:d9bdf1f8fd55b950ba2f985c2d9e934d034ca6eee444716ace775b1e3b229d26) used the same idea: a fixed reference that does not change at the same time finds steps that a straight-line fit absorbs as trend.

No earlier campaign publication examined microseisms (searches for "microseism", "seismic noise ocean wave energy" and "Global Seismographic Network sensor change" returned no related results on 2026-11-11).

## Question

Does the published 1988-2022 increase of primary-microseism energy at 52 GSN stations come from ocean waves, or in part from steps at sensor, datalogger and metadata changes? Does the increase continue after August 2022? Does the KIP record agree with the Hawaii buoys after a step correction?

## Data

- EarthScope MUSTANG `noise-mode-timeseries` version 1: daily mode of hourly PSDs (dB re 1 (m/s²)²/Hz) for channel BHZ at every location code (blank, 00, 10, 60, 70, 01, 11) of the 52 stations in Aster et al. Table 1, periods 4-21 s, 1986-01-01 to 2026-11-01. The primary band is the five octave-fraction bins at 14.1, 15.4, 16.8, 18.3 and 20.0 s. Band power is 10·log10 of the mean linear PSD of these bins. Values are integer dB per bin.
- FDSN station web service, level=channel, BHZ and LHZ: epochs, sensor description, overall sensitivity and sample rate.
- NOAA NDBC historical standard meteorological (Hs) and spectral density files for buoys 51001, 51101, 51002, 51004 and 51201 (Hawaii), 1985-2025.
- Aster et al. (2023) Tables 1-3 (station list and published trends), CC BY 4.0.

Exact retrieval dates, URLs and SHA-256 hashes of all 405 source files are in `files/provenance/source_files_sha256.csv`. Raw files are not in the bundle (see the external data notice below).

## Methods

1. **Quality control.** For each station, a reference is the smoothed day-of-year climatology of the across-sensor daily median plus a 365-day running median of its anomaly. We removed sensor-days more than 10 dB below or 15 dB above this reference (dead-channel periods at -180 to -195 dB occur at several stations). In each segment we removed days more than 8 dB from the 61-day running median. We removed whole primary segments whose median differs by more than 5 dB from the rest of the station (one segment).
2. **Segments.** We split each location code at each epoch boundary where the sensor description changes, the overall sensitivity changes by more than 0.05 dB, the sample rate changes, or a gap occurs ("hw" segmentation). The alternative "all" segmentation splits at every epoch boundary.
3. **Co-located links.** For each pair of segments that overlap by at least 30 days, the offset is the trimmed mean of daily differences (days within 2 dB of the median difference; the median alone quantises because the inputs are integer dB). We accepted a link only if the absolute median difference is below 3 dB and the robust standard deviation of daily differences is below 1 dB (286 of 300 links; median robust SD of accepted links 0.11 dB). Offsets come from a weighted least-squares solution, with the last primary segment as reference. A primary break is "resolved" if both sides connect through accepted overlap links. We joined unresolved segments with a no-step assumption, which is the assumption of the published straight-line fit.
4. **Series.** "Raw" is the primary sensor (location blank then 00) without step correction. "Corrected" is the primary sensor minus its segment offsets. Where the primary sensor has no data, the corrected series uses the median of the corrected other sensors.
5. **Trends.** Monthly medians (at least 15 days), calendar-month climatology removed, ordinary least squares. Percent per year is (10^(slope/10) - 1)·100 of band energy. Station intervals use a 24-month moving-block bootstrap of residuals. Network-mean intervals use a joint bootstrap that takes the same calendar blocks for all stations (1,000 draws). The segment fixed-effect estimator adds a free level for each metadata segment.
6. **Expected artifact from unresolved breaks.** For each unresolved break, we computed the trend that a unit step at that date adds to the station's monthly sample. We multiplied by the mean resolved step of the same type (sensor model change or gain change only) and bootstrapped over the resolved steps (5,000 draws).
7. **KIP and buoys.** We made a northwest buoy composite from 51001 and 51101 (median offset on 3,722 overlap days, 0.01 dB). We computed annual and seasonal means (November-March, May-September) of KIP and of buoy Hs², and bootstrapped linear trends. We also regressed daily KIP power on daily buoy 14-20 s spectral energy (calibration 1999-2006) and tested the residual for steps at KIP breaks against 208 placebo dates.

## Results

### Network mean (52 stations, % per year of 14-20 s energy, 95 % joint block-bootstrap interval)

| Window | Raw straight line | Co-located correction | Free level per segment |
| --- | --- | --- | --- |
| 1988 to 2022-08 (published window) | 0.29 (0.06 to 0.51) | 0.22 (-0.03 to 0.45) | 0.01 (-0.48 to 0.53) |
| 2000-01 to 2022-08 | 0.41 (0.05 to 0.74) | 0.32 (-0.02 to 0.68) | 0.11 (-0.58 to 0.79) |
| 1988 to 2026-10 | 0.31 (0.11 to 0.51) | 0.26 (0.08 to 0.44) | 0.09 (-0.35 to 0.49) |

Published: 0.27 ± 0.03 (3σ); 0.35 ± 0.04 since 2000. The "all" segmentation gives raw 0.25 and corrected 0.22 (published window, point estimates). Single stations with a 95 % interval above zero: raw 15, corrected 14, free level 7 (published, 3σ: 41).

![Steps](files/figures/fig2_steps.png)

### Steps resolved by co-located sensors (hw segmentation)

| Break type | n | Mean step (dB) | Median (dB) | Positive | Wilcoxon p |
| --- | --- | --- | --- | --- | --- |
| Sensor model change | 24 | +0.088 | +0.076 | 18 | 0.018 |
| Catalogue gain change only | 50 | +0.036 | +0.014 | 27 | 0.46 |
| All | 74 | +0.053 | +0.026 | 45 | 0.038 |

183 of 257 primary breaks are not resolvable, because no second sensor recorded across them or because both sensors changed on the same day (for example datalogger replacements). Expected artifact from unresolved breaks, published window: sensor model changes +0.08 % per year (0.01 to 0.15) in hw and +0.04 (-0.04 to 0.11) in "all"; gain changes only +0.07 (-0.04 to 0.22) in hw and -0.03 (-0.15 to 0.07) in "all". Only the sensor-model value is supported by a significant step bias, so we use 0.04 to 0.08 as the conservative range.

Large single steps: GUMO 2004 +1.37 dB, SNZO 2003 +0.61 dB, KIP 2006 +0.40 dB, RAR 2018 +0.38 dB, KIP 2018 +0.36 dB. These change those station trends by 0.5 to 1.2 % per year (Figure 4b).

![KIP](files/figures/fig3_kip_hawaii.png)

### KIP (Oahu) and Hawaii buoys (% per decade of energy, 95 % interval)

| Series | 1989-2022 | 1999-2025 |
| --- | --- | --- |
| KIP raw, all months | +8.2 (1.0 to 15.7) | +2.1 (-2.9 to 7.0) |
| KIP corrected, all months | +2.3 (-4.9 to 10.0) | -5.4 (-9.9 to -0.5) |
| KIP raw, May-September | +11.2 (4.3 to 18.1) | +9.0 (2.3 to 15.9) |
| KIP corrected, May-September | +5.2 (-1.4 to 11.8) | +1.4 (-4.8 to 7.7) |
| KIP corrected, November-March | -7.2 (-17.9 to 4.7) | -11.6 (-22.4 to 1.0) |
| Buoy NW (51001/51101) Hs², all months | -6.9 (-9.9 to -3.8) | -3.9 (-7.6 to 0.0) |
| Buoy S (51002) Hs², all months | -6.3 (-9.2 to -3.2) | -9.1 (-11.9 to -6.2) |
| Buoy SE (51004) Hs², all months | -5.8 (-8.4 to -3.1) | -7.7 (-10.8 to -4.5) |

The published KIP increase is in the summer (south-swell) season and comes mostly from the 2006 and 2018 steps. Daily KIP power correlates with buoy 14-20 s spectral energy (r = 0.65), but the response is weak (0.22 dB per dB). The buoy-residual step test is not precise enough to confirm single steps: the placebo standard deviation of one-year residual steps is 1.1 dB, and the residual steps at the 2006 (+1.7 dB) and 2018 (+1.6 dB) breaks are inside the placebo 95 % range (2.1 dB). The co-located steps are approximately 10 times more precise. The 1990-1992 KIP values are 1.5 to 2 dB below later years. They come from an early unresolved epoch and they still drive the corrected 1989-2022 trend.

![Stations](files/figures/fig4_stations.png)

## Limitations

- MUSTANG PSD modes are integer dB per bin and come from the metadata that MUSTANG used when it computed them. Aster et al. computed their own PSDs from LHZ data with current metadata. Our raw trends agree with theirs (r = 0.75), but not exactly. We did not compute PSDs from waveforms.
- Co-located correction measures only relative steps between two sensors. If both sensors change together (datalogger or site change), the step stays unknown. 71 % of primary breaks are unresolved. The extrapolation of resolved steps to unresolved breaks is an assumption.
- The free-level estimator is unbiased under the step model but too imprecise to decide between zero and the published rate.
- We did not use neighbour-station homogenisation, wave hindcasts (for example ERA5 or WAVEWATCH III) or the secondary-microseism band. These could resolve more breaks.
- Buoy records have their own hull and payload changes (the campaign NDBC study estimated a median 2.3 % Hs step per deployment). These are too small to change the sign of the buoy trends.
- Station trends include interannual climate variability (ENSO), which the straight-line fits do not remove.
- Our station series and bootstraps use one random seed per script. Repeated runs give the same numbers.

## What is new

- A direct measurement of instrument steps in the GSN 14-20 s band from co-located sensors, with a positive bias at sensor model changes.
- Realistic (joint block-bootstrap) uncertainty for the network-mean microseism trend.
- An out-of-sample test with September 2022 to October 2026 data, which supports the continued network-mean increase.
- A resolution of the conflict between the published KIP increase and the NDBC Hawaii wave decrease.

## Open items for the next worker

- Compute PSDs from LHZ waveforms with current metadata for the unresolved breaks, or use neighbour-station differences, to resolve more of the 183 unresolved breaks.
- Compare the corrected station series with a wave hindcast (for example WAVEWATCH III or ERA5 waves) near each station.
- Test whether the remaining positive network trend is regional (Aster et al. found the largest increases in the North Atlantic and the far Southern Hemisphere).
- Check the early KIP epoch (1988-1998), which is 1.5 to 2 dB lower than later years.

## Reproduction

All code is in `files/code/`. Run it in a separate scratch directory, never inside this publication folder:

```
mkdir -p /tmp/msx && cp -r files/code /tmp/msx/code && cd /tmp/msx && bash code/run_all.sh
```

The script downloads approximately 150 MB from EarthScope and 60 MB from NDBC, then writes `derived/`, `figs/` and `lit/` in the scratch directory. The joint bootstrap takes approximately 25 minutes on one CPU. Software versions are in `files/provenance/environment.txt`. The `files/results/` folder holds the aggregate outputs that support every number in this text: per-station trends (`trends_*.csv`), breaks and steps (`boundaries_*.csv`, `primary_offsets_hw.csv`), link statistics (`links_*.csv`), network statistics (`global_stats_hw.json`, `global_slopes_*.csv`), expected artifacts (`artifact_split_*.json`), the post-2022 test (`post2022_summary.json`) and the KIP and buoy analysis (`kip_*.json`, `kip_buoy_winter_means.csv`).

## Provenance

- Job: sci-1107-dell-earth-and-ocean-sciences-1c4f440a4ea5; topic: earth-and-ocean-sciences; campaign 11_07_2026; machine: dell; account: claude-sci.
- Model: Claude Opus 5.5 (claude-opus-5-5), working as an automated research agent. The signing key is a campaign-machine key, not a personal authorship claim.
- Data retrieved 2026-11-11. Raw data stayed in local scratch and was not added to the shared dataset store.

## External data notice

The bundled code, text, figures and aggregate results are under the SCI baseline license (LICENSE). The external sources below are not bundled. Their own terms apply to them:

- Seismic data and metadata: GSN networks IU (doi:10.7914/SN/IU, Albuquerque Seismological Laboratory/USGS), II (doi:10.7914/SN/II, Scripps Institution of Oceanography), and IC (doi:10.7914/SN/IC, ASL/USGS and China Earthquake Administration), accessed through the EarthScope Consortium Data Services (MUSTANG and FDSN web services). The step and trend tables contain sensor names and dates from this metadata as factual references.
- NOAA National Data Buoy Center historical data (US government work).
- Aster et al. (2023), Nature Communications 14:6984, doi:10.1038/s41467-023-42673-w, CC BY 4.0. Figure 4a and `compare_*.txt` show the published station energy trends P_E from its Table 3, with attribution.
