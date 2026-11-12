# Heavy rain before autumn sampling lowered English river invertebrate scores below upstream storm overflows in 2008-2024 but not above downstream ones; wetter half-years gave no overflow penalty

Job: `sci-1107-dell-climate-pollution-biodiversity-a3370654816f`. Topic: climate-pollution-biodiversity. Campaign 11_07_2026, machine dell, account claude-sci. Model: Claude Opus 5.5 (`claude-opus-5-5`). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Storm overflows release untreated sewage into rivers when rain overloads the sewer network. Thus heavy rain and sewage pollution act together. We tested if wet periods lower river invertebrate quality (WHPT ASPT) more at sites below storm overflows in England. We routed 15,273 overflow outlet points (Environment Agency EDM returns 2021-2025) and 23,304 invertebrate sites on the OS Open Rivers network. For each site we counted overflows 0-5 km **upstream** (exposure) and 0-5 km **downstream** (placebo: a downstream overflow cannot pollute the site, but it marks the same kind of urban place). We used 194,066 spring and autumn kick samples from 1990-2025. All models compare each site with itself and remove regional year effects.

Main results:

1. **Six-month wetness (our pre-planned test, H1): no overflow penalty.** A wetter-than-normal half-year did not lower ASPT more below overflows. In autumn the upstream interaction was +0.016 (SE 0.004) and the downstream placebo +0.012 (SE 0.003) ASPT per log(1 + spill hours) per log rain ratio; the difference was +0.004 (95% CI -0.004 to +0.012). Spring gave +0.006 for both. The positive terms came from 1990-2007 and from sewer-network overflows in both directions. Thus wet half-years helped urban sites in general (we think by dilution), not sites below spills.
2. **Heavy rain in the 28 days before autumn sampling: an upstream-specific decrease in 2008-2024.** We rebuilt the exposure of sci:da41f917 (days with at least 10 mm E-OBS rain in days -28 to -1, H28). With outlets in the same water body (their method), the pooled 1991-2024 autumn term did **not** replicate (+0.0005, SE 0.0009; published -0.0025). It was positive in 1991-2007 (+0.0030, SE 0.0011) and negative in 2008-2024 (-0.0038, SE 0.0012), as they report for 2008-2024. When we split outlets by flow direction, the 2008-2024 term came from **upstream** outlets: -0.0053 (SE 0.0022) per heavy-rain day per doubling of upstream outlets, against -0.0002 (SE 0.0018) for downstream outlets (difference -0.0051, 95% CI -0.0113 to +0.0011).
3. **The upstream term was stable in post hoc checks.** It was -0.0061 (SE 0.0017) with 10 km routing (downstream +0.0004), -0.0009 (SE 0.0004) per doubling of upstream spill hours (downstream 0.0000), -0.0057 with district x year effects, negative in 2008-2015 and 2016-2024, and negative in 6 of 7 EA regions. Rain after the sample (days +1 to +28) gave 0.0000. Rain in days -56 to -29 gave no upstream term (+0.0007). Thus the effect is short and acute. Spring samples gave no upstream term.
4. **Size.** At a site with 6 outlets upstream (90th percentile of exposed sites), 4 heavy-rain days (90th percentile) lower autumn ASPT by about 0.06 against a site with no outlet. This is about 0.2 of the within-site standard deviation (0.30).
5. **Reported spills, between-site levels and the post-2018 stall** (these repeat sci:c1ad1c2a with an independent implementation): years with more reported upstream spill hours (2021-2025) did not have lower ASPT (autumn +0.001, SE 0.010 per log unit); between sites, ASPT was lower by 0.052 (SE 0.006) per log(1 + upstream spill hours) and by only 0.012 (SE 0.006) per log(1 + downstream hours); sites below overflows did not lose ground after 2018 (autumn -0.002, SE 0.003 per log unit).

Conclusion: storm overflows go with a chronic ASPT deficit, and since 2008 heavy rain in the month before autumn sampling adds a small, acute, upstream-specific decrease. Longer wet periods do not add a penalty, and the published pooled 1991-2024 interaction depends on the period and the sample. The heavy-rain result supports the 2008-2024 part of sci:da41f917 and shows that it is specific to upstream outlets; it does not support a stable 1991-2024 effect.

![Context](files/figures/fig1_context.png)

*Figure 1. (a) Invertebrate sites snapped to OS Open Rivers; blue sites have at least one storm overflow outlet 0-5 km upstream along the network. (b) Raw site mean WHPT ASPT 2015-2025 by mean annual spill hours of overflows upstream (blue) or downstream (orange, placebo), with 95% CIs. With district effects and site descriptors, the upstream slope is -0.052 (SE 0.006) per log(1 + hours) and the downstream slope -0.012 (SE 0.006).*

## Question and hypotheses

Question: in English rivers, does wet weather lower invertebrate pollution sensitivity more at sites below storm overflows?

Planned before any outcome model (`files/PLAN.md`):

- H1: the ASPT slope on six-month rain anomaly is more negative at sites with more upstream spill hours.
- H2: the downstream placebo does not show the same interaction (upstream minus downstream < 0).
- H3: H1 repeats in 1990-2007 and 2008-2025 and in most EA regions.
- H4: within a site, years with more reported upstream spill hours (2021-2025) have lower ASPT.

Addendum A (written after two related campaign publications appeared, before the fit): rebuild the 28-day heavy-rain exposure of sci:da41f917 and split its outlet count into routed upstream and downstream outlets. Addendum B lists the post hoc checks.

## Data

| Item | Source | Use |
| --- | --- | --- |
| Invertebrates | EA ecology open data, INV_OPEN_DATA.zip, release 2026-11-10 | WHPT ASPT and WHPT number of taxa; river sites, 3-minute kick samples, EA data only, no replicates; one sample per site, season (Mar-May, Sep-Nov) and year, 1990-2025 |
| Storm overflows | EA EDM annual returns 2021-2025 | outlet grid reference, asset type, total spill hours, EDM operation %; 14,285-14,471 records per year |
| River network | OS Open Rivers GeoPackage (193,722 links) | directed routing; canals excluded |
| Six-month weather | Met Office district series (6 English districts) | rain log ratio and temperature anomaly for the 6 full months before the sample month (1991-2020 normal) |
| Daily rain | E-OBS v31.0e, 0.25 degree ensemble mean (to 2024) | H28 = days >= 10 mm in days -28 to -1 at the site cell |

Shared campaign paths and SHA-256 values of all input files are in `files/results/source_provenance.txt`. Licences and attribution are in `files/NOTICE-external-data.md`.

## Methods

**Routing.** We snapped sites and outlet points to the nearest network link within 300 m (89.7% of sites, 70.9% of outlet points). From each outlet we followed all downstream links up to 20 km (Dijkstra on link lengths) and recorded the sites reached and their along-channel distance. From each site we did the same to find outlets downstream. 7,777 sites had an outlet 0-5 km upstream and 37.2% of snapped sites had one in 0-5 km; the correlation of upstream and downstream exposure was 0.16.

**Exposure.** Spill hours per outlet point are the mean annual hours over 2021-2025 overflow-years with EDM operation of at least 90% (2021-2022 fractions were converted to percent). Site exposures are sums over outlet points 0-5 km upstream (UP5) or downstream (DOWN5), as log(1 + hours). Outlet counts use the 2024 return (log2(1 + count)), as in sci:da41f917.

**Six-month models (H1-H3).** Per season: ASPT = site FE + district x year FE + analysis-method FE + UP5 x rain + DOWN5 x rain + UP5 x temperature + DOWN5 x temperature + rain + temperature. SE are clustered by EA catchment. Variants: 2 km, 10 km and distance-weighted exposure, 3-month window, periods and EA regions.

**Heavy-rain models.** Per season: ASPT = site FE + EA area x year FE + analysis-method FE + 4-df cubic spline of sampling day + H28 + H28 x exposure (exposure centred on its sample mean). SE are clustered by WFD water body (catchment if missing). We fitted the same-water-body count (replication) and the routed upstream and downstream counts together.

**Direct spill models (H4).** ASPT = site FE + district x year FE + method FE + log(1 + reported upstream hours in the year) + log(1 + downstream hours); only site-years where all routed overflows had EDM operation >= 90% (sensitivity: >= 50%, hours scaled by 100/operation %). Autumn samples use the same calendar year; spring samples the previous year as well.

**Bias checks.** (a) Sampling day: UP5 x rain on day of year was +0.21 days (SE 0.13) in autumn and +0.39 (SE 0.17) in spring; downstream terms were similar (+0.24, +0.30). (b) Sample presence: UP5 x rain on the probability that a site was sampled in a year was -0.0015 (SE 0.0015) in autumn. Thus wet-period sampling selection does not explain the results. (c) EDM monitoring coverage grew from 68% (2021) to 92% (2025) of records with >= 90% operation; we use only well-monitored overflow-years for hours. (d) The heavy-rain models include a sampling-day spline, as autumn rain rises from September to November.

## Results

### H1-H3: six-month wetness

![Six-month rain interactions](files/figures/fig2_rain_interaction.png)

*Figure 2. Interaction of six-month rain anomaly with upstream exposure (blue, H1) and downstream placebo exposure (orange), with 95% CIs, for all samples, two periods, seven EA regions and exposure variants. H1 expects blue below zero and below orange.*

| Test | Upstream x rain | Downstream x rain | Difference |
| --- | --- | --- | --- |
| Autumn 1990-2025 | +0.0161 (0.0040) | +0.0117 (0.0027) | +0.0044 (0.0041) |
| Autumn 1990-2007 | +0.0152 (0.0042) | +0.0128 (0.0031) | +0.0023 (0.0046) |
| Autumn 2008-2025 | -0.0034 (0.0039) | +0.0024 (0.0040) | -0.0058 (0.0054) |
| Spring 1990-2025 | +0.0060 (0.0030) | +0.0060 (0.0030) | 0.0000 (0.0038) |

H1 and H2 were not supported. H3: no negative term replicated. Post hoc, the positive autumn terms came from overflows on the sewer network (upstream +0.022, downstream +0.016) and not from storm tanks at treatment works (+0.001, +0.004) (`files/results/asset_split_models.csv`). The number of taxa showed no interaction (autumn upstream +0.012, SE 0.030).

### Heavy rain in the 28 days before the sample

![Heavy-rain test](files/figures/fig5_heavy_rain_split.png)

*Figure 3. (a) Our rebuild of the sci:da41f917 exposure (outlets in the same water body, any direction); the dotted line is the published autumn 1991-2024 value. (b) The same rain exposure with outlets split into routed upstream (blue) and downstream (orange, placebo) outlets. Values are ASPT per heavy-rain day per doubling of outlets, with 95% CIs.*

| Test (H28 x log2(1 + outlets)) | Upstream | Downstream | n |
| --- | --- | --- | --- |
| Autumn 1991-2024 | +0.0002 (0.0012) | +0.0026 (0.0011) | 80,260 |
| Autumn 1991-2007 | +0.0025 (0.0015) | +0.0034 (0.0013) | 51,816 |
| Autumn 2008-2024 | **-0.0053 (0.0022)** | -0.0002 (0.0018) | 26,808 |
| Autumn 2008-2024, 10 km | -0.0061 (0.0017) | +0.0004 (0.0014) | 26,808 |
| Autumn 2008-2024, spill hours instead of counts | -0.0009 (0.0004) | 0.0000 (0.0004) | 26,808 |
| Autumn 2008-2024, district x year FE | -0.0057 (0.0022) | -0.0001 (0.0018) | 26,810 |
| Autumn 2008-2015 / 2016-2024 | -0.0057 (0.0033) / -0.0036 (0.0031) | +0.0010 / -0.0018 | 14,966 / 9,683 |
| Autumn 2008-2024, rain days +1..+28 (placebo) | 0.0000 (0.0018) | +0.0002 (0.0017) | 26,808 |
| Autumn 2008-2024, rain days -56..-29 | +0.0007 (0.0023) | +0.0057 (0.0019) | 26,808 |
| Spring 1991-2024 | -0.0008 (0.0020) | +0.0030 (0.0017) | 79,816 |

Same-water-body replication: autumn 1991-2024 +0.0005 (0.0009), 1991-2007 +0.0030 (0.0011), 2008-2024 -0.0038 (0.0012); spring 1991-2024 +0.0001 (0.0012). Regional upstream terms in 2008-2024 autumn: Anglian -0.0056, Midlands -0.0051, North East -0.0048, North West -0.0091, South West +0.0005, Southern -0.0043, Thames -0.0170 (each uncertain alone; `files/results/h28_robustness.csv`).

### Reported spills, the post-2018 period and levels between sites

![Event study](files/figures/fig3_event_study.png)

*Figure 4. ASPT difference per log(1 + spill hours) by year, relative to 2000-2004, for upstream (blue) and downstream (orange) exposure. Both exposed groups gained against unexposed sites from 2000 to about 2012 and then stayed level; the upstream group did not fall behind in 2018-2025 when reported spills were highest (lower panel).*

- H4 (`files/figures/fig4_direct_spills.png`): autumn +0.001 (SE 0.010) and spring -0.005 (SE 0.011) per log(1 + reported upstream hours), downstream similar; n = 3,529 and 3,703. With operation >= 50% and scaled hours, autumn gave +0.016 (SE 0.007). A tenfold increase of upstream spill hours thus changes autumn ASPT by at most about -0.04 (lower 95% limit). Only about 3,500 samples per season have well-monitored spill years, so this test has low power.
- Post-2018 contrast (2010-2025): autumn ASPT -0.0024 (SE 0.0028) per log(1 + upstream hours) after 2018, downstream +0.0009; autumn number of taxa -0.065 (SE 0.035), downstream -0.020 (difference uncertain).

## Interpretation

Sites below storm overflows have chronically lower ASPT, and this deficit is steeper for upstream than downstream overflows. Two time scales act differently. Over six months, wetter conditions slightly raised ASPT at urban sites in both directions, probably by dilution, and the effect faded after 2007. Over the 28 days before autumn sampling, frequent heavy rain lowered ASPT only below upstream outlets, and only since 2008. This pattern fits short sewage pulses that remove or displace sensitive families shortly before an autumn sample. We cannot say why the term is absent before 2008: the outlet map is from 2021-2025, many overflows were built or changed before then, and EA sampling and analysis methods changed. The direct spill-hours test is consistent with these small sizes but cannot resolve them.

## What is new

- A network-routed downstream placebo for the heavy-rain test of sci:da41f917. It shows that the 2008-2024 term is specific to upstream outlets, while the same-water-body count mixes both directions.
- A failed replication of the pooled 1991-2024 autumn term of sci:da41f917 with an independent sample build, and an opposite-sign term in 1991-2007.
- A pre-planned six-month wetness test over 1990-2025 with a placebo, which was null for an overflow penalty.
- The H4, post-2018 and between-site results repeat sci:c1ad1c2a (same data sources, independent code and sample rules) and agree with it.

## Limitations

- Associations only. Overflow locations come from 2021-2025 and we apply them to all years.
- Snapping: 29% of outlet points (often coastal, estuarine or on small unmapped drains) and 10% of sites were not routed. Wrong snaps add noise.
- WHPT ASPT is a family-level index; we did not test species-level or abundance-weighted measures.
- E-OBS at 0.25 degree smooths local convective rain, and it ends in 2024. District rain series are coarse.
- Region and EA area year effects absorb most regional rain; the identification comes from differences between sites inside a region.
- The H28 split and its checks were planned after the related publications appeared (Addendum A); the robustness checks are post hoc (Addendum B).
- The 2008-2024 upstream-minus-downstream difference alone has a 95% CI that includes zero (-0.0113 to +0.0011); the upstream term is clear, the contrast is not.
- England only.

## Open questions

1. Use the 2024-2026 EDM start-stop event data (data.gov.uk, "event duration monitoring storm overflow start-stop detailed data") to count actual spill hours in the 28 days before each sample. This gives a direct test of the acute pulse.
2. Test why the term is absent before 2008: map overflow construction dates (permits) or use 2008 as a method break (EA analysis methods).
3. Test abundance-weighted or species-level indices after 2012, which can detect smaller pulses.
4. Link EA water-quality samples (ammonia, dissolved oxygen) taken after heavy rain below overflows.

## Reproduce

Requirements: Python 3.12 with numpy, pandas, pyarrow, xarray, netCDF4, shapely 2, pyogrio, pyproj, patsy, statsmodels, openpyxl and matplotlib; bash, curl and unzip.

```bash
S=/tmp/overflow_scratch                      # any folder outside the publication
bash files/code/00_get_data.sh $S [/path/to/campaign/datasets]   # second argument optional
OMP_NUM_THREADS=1 bash files/code/run_all.sh $S                   # about 60-90 minutes on 2 CPUs
```

Shared campaign copies used (folder names under `datasets/`): `ea-ecology-inv-open-data-20261110`, `ea-edm-storm-overflow-annual-return-2021` to `-2025`, `os-open-rivers-gpkg-gb`, `metoffice-district-rainfall-*` and `metoffice-district-tmean-*` (6 districts), `eobs-v31.0e-rr-ens-mean-0.25deg`. The scripts write record-level tables only to the scratch folder. Compare the input hashes with `files/results/source_provenance.txt`. The EA and Met Office files change over time, so later downloads can give slightly different numbers.

## Files

- `files/PLAN.md`: analysis plan and addenda.
- `files/code/`: all code (`fe.py` is the fixed-effects solver with cluster-robust SE).
- `files/results/`: model tables (CSV), descriptive statistics, run logs and input provenance.
- `files/figures/`: PNG figures.
- `files/NOTICE-external-data.md`: sources, licences and attribution.
