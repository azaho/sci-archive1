# Winter wave heights at 47 NDBC buoys fell 3.1% per decade near Hawaii in 1985-2025 and rose in no US region; the few instrument steps found by neighbour tests do not cause the decrease

## Summary

We examined winter (November to March) significant wave height (Hs) at 47 long-record moored buoys of the US National Data Buoy Center (NDBC) for the winters 1985-2025. We asked two questions:

1. Did winter mean and upper-percentile Hs change, and does the El Niño-Southern Oscillation (ENSO) modulate them?
2. Do changes of buoy hull, payload or sensor put false steps into the records, and do such steps cause the trends?

Main results:

- **Hawaii (4 buoys):** winter mean Hs decreased by 3.1% per decade (95% CI 2.2 to 3.9) in 1985-2025, and the 95th percentile decreased by 3.9% per decade (2.6 to 5.1). The decrease continued in 2003-2025 (mean: -3.0% per decade, CI -4.3 to -1.7). All four buoys show the decrease separately (-2.3 to -3.1% per decade).
- **Other regions:** the Southeast Atlantic decreased by 1.4% per decade (CI -2.3 to -0.4). The Gulf of Mexico 95th percentile decreased by 1.6% per decade (CI -3.1 to -0.2). The US West Coast trend depends on the start year: -1.5% per decade (CI -3.5 to +0.5) from 1985, and -5.0% per decade (CI -8.3 to -1.5) from 1995. Alaska and the Northeast Atlantic shelf have no clear trend from 1985. In the Northeast Atlantic, the winter North Atlantic Oscillation (NAO) explains most of the 1995-2025 decrease.
- **No region shows an increase.** Of 38 buoys with long records, 30 have negative trends (11 with a 95% CI below zero) and 1 has a positive trend with a CI above zero.
- **ENSO:** in all six regions, the ONI coefficient is positive: winter Hs is higher in El Niño winters. Per +1 °C of the December-February Oceanic Niño Index (ONI), the effect is +0.9% to +1.9% in the mean and +0.1% to +2.8% in the 95th percentile (1985-2025). The 95th-percentile effect has p < 0.05 in five regions (not Alaska). The mean effect has p < 0.05 only in Hawaii and the Southeast Atlantic.
- **Instrument steps:** a pairwise neighbour test found 36 breaks in 32 of 167 buoy pairs and assigned 4 breaks to single buoys (44013 in 1995, 46026 in 1997, 46041 in 2000, 44005 in 2002). The step sizes are +31%, +14%, +11% and -16%. When we remove these steps, no regional trend changes by more than 0.54 percentage points per decade.
- **Detection power:** with synthetic steps, the test finds 10% of 5% steps, 41% of 10% steps, 79% of 16% steps and 93% of 22% steps, with no false breaks for zero steps. Thus the test cannot see steps smaller than about 10%.
- **2011-2025 metadata:** we read 342 deployment changes from NCEI NetCDF metadata and fitted a network model with one offset for each deployment. Each new deployment changes Hs relative to its neighbours by a median absolute 2.3%, with no systematic sign. A change from a 3 m discus hull to a 3 m foam hull raised Hs by a mean of 2.4% (n = 23, p = 0.003). The reverse change gave -0.3% (n = 14, not significant). Pooled with the sign reversed, foam hulls read 1.7% higher than discus hulls (n = 37, t-test p = 0.048, Wilcoxon p = 0.002). Most buoys changed from discus to foam in 2016-2022. Thus this effect probably adds a small false increase to recent years. It does not cause the observed decreases.

Main limitations: the neighbour test cannot see steps that occur at the same time at all buoys of a region. Before 2011 we have no hull metadata. Hawaii has only 4 buoys, 3 pairs within 1000 km, and low detection power. An independent check with satellite altimetry or a wave hindcast is necessary before the Hawaii decrease is accepted as a physical change.

## Scope and assumptions

- Data: NDBC standard meteorological annual files (`stdmet`, hourly or 10-minute WVHT), downloaded on 2026-11-08 for 47 buoys with at least 30 annual files and records to 2024 or later. We excluded Great Lakes buoys (45xxx) because they are removed in winter.
- Winter W is November of year W-1 to March of year W. We use winters 1985-2025.
- A winter is valid if at least 4 of 5 months have at least 50% of hourly Hs and the winter has at least 60% of hours.
- The metric "winter mean Hs anomaly" is the mean of hourly log(Hs) minus the station calendar-month mean of log(Hs). We report it as a percent. We also use the log of the winter 95th and 99th percentiles and the winter maximum.
- A regional composite is the winter effect c_w in a two-way fixed-effects fit y[s,w] = a_s + c_w. We use stations with at least 10 valid winters and winters with at least 2 stations.
- Trend model: c_w = b0 + b1 (W - 2005) + b2 ONI_DJF(W) + e. A second model adds the November-March mean PDO (Pacific regions) or NAO (Atlantic and Gulf regions). Confidence intervals are Newey-West HAC (2 lags) 95% intervals. We also give a station bootstrap interval in the tables.
- We assume that real wave climate changes are spatially smooth within about 1000 km, so that a step in only one buoy is an instrument effect.

## Methods

### 1. Data preparation and quality control

`parse_ndbc.py` reads all annual formats (2-digit years before 1999, the `mm` column after 2004, and units rows after 2006). It rounds times to the nearest hour and averages values in the same hour. NDBC missing codes (99.0) and Hs outside 0 to 25 m are set missing.

`qc_hourly.py` adds three rules after we found an unflagged sensor failure (buoy 51003 gave Hs of 0.01-0.02 m for all of February 2011; this made a false -45% Hawaii winter in a first run):

1. Hs < 0.05 m is set missing (8,750 hours).
2. Runs of 12 or more equal consecutive values are set missing (52,722 hours).
3. A station-month whose median differs from the station calendar-month median by more than a factor of 2 is set missing (10,679 hours).

At each station, these rules remove at most 2.3% of the winter hours. `files/data/qc_log.csv` lists the removed months.

### 2. Pairwise break detection (`homogenize.py`)

For each pair of buoys in the same basin within 1000 km (167 pairs), we compute D_ab(W), the mean of log(Hs_a / Hs_b) over common winter hours. We need at least 50% of the winter hours in common. Binary segmentation finds mean shifts in D_ab. Each split uses the largest two-sample t statistic with at least 3 winters in each segment. A permutation test (2,000 shuffles, max-t null) gives its p-value, and we keep splits with p < 0.01. We assign a break to a station when breaks in at least 2 of its pairs overlap within 1 winter and these pairs are at least half of its testable pairs. Assignment is greedy, as in the pairwise homogenization of Menne and Williams (2009). The step size is the median over unaffected neighbours of the change in pair mean. We shift earlier segments to agree with the latest segment. We use the same break years to adjust the percentile metrics from the pair differences of the 95th percentile.

We also apply the same test to the mean log ratio of buoy wind speed. Hull changes move the anemometer height, so a wind step at the same time can support an instrument cause. No wind break was assigned to a station.

Sensitivity variants: 600 km pairs (`km600`) and p < 0.05 (`a05`). Both variants find the same 4 main breaks, and `a05` adds 5 more. In all three variants, the adjustment changes a regional trend by at most 0.66 percentage points per decade (main: 0.54; `files/data/regional_trends_*.csv`).

### 3. Detection power (`injection_test.py`)

We add a synthetic step of 0%, 5%, 10%, 16% or 22% to a random buoy without a detected break, at a random winter with at least 3 pair winters on each side. Then we run the detection again. We use 150 injections for each step size. A hit is a break assigned to that buoy within 2 winters of the injected winter.

### 4. Metadata event study and network deployment model (2011-2025)

NCEI keeps NDBC data as monthly NetCDF files whose names give a deployment number. Each file holds group attributes for the hull (`hull_id`), the payload and the wave sensor. These files start in 2011. We sampled the directory listings for January, April, July and October of 2011-2025 (`collect_ncei_listings.sh`). We read the first sampled file of each of 461 deployments (`fetch_deploy_meta.py`). We kept the metadata, URLs and SHA-256 hashes, and deleted the NetCDF files.

`deployment_offsets.py` fits d_ab(t) = mu_ab + x[a, dep_a(t)] - x[b, dep_b(t)] + e to the deseasonalized monthly log ratios (21,349 pair-months from 2011). It finds one offset x for each station deployment, with the first deployment of each station fixed at 0. The change at a new deployment is x_new - x_old. Uncertainty comes from 300 bootstrap resamples of calendar years. We use the 265 changes with at least 12 pair-months on each side. For 96 of the 342 changes the hull is unknown in one of the two files, and we do not classify them. `event_study.py` gives a simpler window test (24 months before and after, neighbours with their own changes excluded, against 600 random placebo months). In this test, |step| after hull-class changes (median 2.4%) is larger than for placebo months (1.7%, Mann-Whitney p = 0.006), but the sign is not consistent (Wilcoxon p = 0.99).

## Results tables

Break-adjusted regional trends of winter mean Hs (% per decade, ONI model, HAC 95% CI):

| Region | Buoys | 1985-2025 | 1995-2025 | 2003-2025 | ONI effect (% per °C), 1985-2025 |
|---|---|---|---|---|---|
| Alaska | 4 | -0.7 [-1.8, +0.5] | -0.9 [-3.2, +1.4] | -1.8 [-4.0, +0.4] | +0.9 |
| US West Coast | 18 | -1.5 [-3.5, +0.5] | -5.0 [-8.3, -1.5] | -3.0 [-6.0, +0.1] | +1.9 |
| Hawaii | 4 | -3.1 [-3.9, -2.2] | -3.9 [-5.1, -2.7] | -3.0 [-4.3, -1.7] | +1.7 |
| Gulf of Mexico | 7 | -0.9 [-2.1, +0.3] | -1.3 [-3.2, +0.6] | -2.3 [-5.5, +1.1] | +1.3 |
| Southeast Atlantic | 6 | -1.4 [-2.3, -0.4] | -1.1 [-2.1, -0.1] | -0.6 [-2.5, +1.4] | +1.6 |
| Northeast Atlantic shelf | 8 | +0.0 [-1.4, +1.5] | -1.3 [-2.3, -0.2] | -2.0 [-3.9, -0.1] | +1.0 |

Winter 95th percentile Hs (% per decade, 1985-2025): Alaska -0.7 [-1.8, +0.4]; US West Coast -1.4 [-3.3, +0.6]; Hawaii -3.9 [-5.1, -2.6]; Gulf of Mexico -1.6 [-3.1, -0.2]; Southeast Atlantic -2.0 [-3.7, -0.2]; Northeast Atlantic shelf -0.4 [-3.0, +2.1].

With the PDO or NAO added, the 1985-2025 trends stay similar. Hawaii is -3.7% per decade [-4.6, -2.7]. The Northeast Atlantic 1995-2025 trend becomes -0.6% [-1.5, +0.3], because the NAO coefficient is -4.4% per index unit (p < 0.001). With ONI in the model, the PDO coefficients in the Pacific regions are small and negative (-0.3% to -2.0% per index unit). They have p < 0.05 only for Hawaii mean Hs (p = 0.004) and the Alaska 95th percentile (p = 0.03). ONI and PDO are correlated, so we do not interpret the PDO sign physically.

Figures:

- `files/figures/fig1_regional_composites.png`: regional composites with the ONI value of each winter.
- `files/figures/fig2_regional_trends.png`: trends by region, metric and start year, raw and adjusted.
- `files/figures/fig3_breaks_power_deployments.png`: two assigned breaks, detection power, and 2011-2025 deployment offset changes.

## Interpretation

The 1985-2025 decrease is spatially broad. No region increased. An earlier study reported increasing wave heights off the US Pacific Northwest (Ruggiero et al., 2010). That study used records that ended in the 2000s, and Gemmrich et al. (2011) found that hull and processing changes caused part of the increase. In our data, the largest US West Coast winters are 1998 and 1999. A start in 1995 therefore gives a strong decrease, and a start in 1985 does not give a clear trend. We do not interpret the US West Coast trend as a stable long-term rate.

The Hawaii decrease is the most consistent result. It is in each of the four buoys and in each start period, and the ONI, PDO and break adjustments do not remove it. Hawaii winter Hs is mostly North Pacific swell. A decrease could thus come from changes in North Pacific storm tracks. The data also agree with an instrument change at the same time on all four buoys before 2011, which the neighbour test cannot see. The 2003-2025 decrease (-3.0% per decade) is mostly in years with hull metadata. In those years, the network model gives Hawaii deployment offsets of -6% to +9% with no consistent sign. The net 2011-2025 offset of each Hawaii buoy is -1.7% to +0.1%. But each Hawaii buoy has only one or two neighbours, and the model cannot see a shift that is common to all four buoys. We consider the Hawaii decrease probable but not confirmed.

The discus-to-foam effect (+1.7%) has the wrong sign to explain the decreases. If it is real, the 2016-2022 transition makes the recent decreases slightly smaller than the true values.

## Limitations

- The neighbour method sees only steps that are local to one buoy. Simultaneous changes at all buoys in a region are not visible.
- Detection power is low for steps below 10%. Each new deployment adds steps with a typical size of 2-3% that the annual test cannot find. These steps add noise to station trends. Because they have no systematic sign, they probably do not bias the regional trends much, but we did not prove this for the period before 2011.
- Hull metadata is available only from 2011. The deployment dates come from quarterly samples, so they can be wrong by up to 3 months.
- Real changes in the spatial pattern of waves (for example a storm-track shift) can also change pair ratios. Some assigned breaks may thus be real. The 4 assigned breaks occurred in 1995-2002 and are large (11-31%). This agrees with known NDBC system changes in that period, but we have no metadata to confirm it.
- Trends over 20-40 winters are sensitive to start year and to large ENSO winters. HAC intervals with 2 lags may be too narrow if there is decadal variability.
- We did not use an independent data source (satellite altimetry or a hindcast). This is the most important next step.
- Regions are defined by station-number prefix and latitude. Alaska has only 4 buoys.

## Reproduction

Python 3.12.15 with numpy 2.5.4, pandas 3.1.1, scipy 1.18.1, statsmodels 0.15.0, matplotlib 3.11.2, h5py 3.16.0, pyarrow and lxml.

```
mkdir -p W/code W/raw W/derived W/figs
cp files/code/* W/code/
gunzip -c files/provenance/stdmet_index.html.gz > W/raw/stdmet_index.html
cp files/provenance/station_table.txt W/raw/
export ONI_HTML=<path>/oni_v5.html PDO_DAT=<path>/ersst.v5.pdo.dat NAO_ASC=<path>/norm.nao.monthly.b5001.current.ascii
W=$PWD/W bash W/code/run_all.sh
```

`run_all.sh` downloads 1,901 NDBC files (about 400 MB) if `W/raw/ndbc` is not present. Check them against `files/provenance/ndbc_provenance.csv`. NDBC can revise archive files, so new downloads can give other hashes. The step that fetches NCEI metadata reads about 1 GB and keeps only attributes. The included `files/data/ncei_deployment_meta.csv` lets you skip this step. With 8 cores, the full run takes about 1 hour. The trend bootstrap and the injection test are the slowest steps.

Data provenance is in `files/provenance/PROVENANCE.md`. All derived tables used for the claims are in `files/data/` and are described in `files/data/README_data.md`.

## Provenance of this work

- Campaign job: sci-1107-hp-earth-and-ocean-sciences-669182da9aa9; topic: earth-and-ocean-sciences; machine: hp; account: claude-olen.
- Model: Claude Opus 5.5 (claude-opus-5-5), working as an autonomous research agent. The signing key is a campaign-machine key. It does not make a personal authorship claim.
- Analysis dates: 2026-11-08 to 2026-11-09.

## References

- Gemmrich, J., Thomas, B., Bouchard, R. (2011). Observational changes and trends in northeast Pacific wave records. Geophysical Research Letters. doi:10.1029/2011GL049518
- Ruggiero, P., Komar, P. D., Allan, J. C. (2010). Increasing wave heights and extreme value projections: the wave climate of the U.S. Pacific Northwest. Coastal Engineering. doi:10.1016/j.coastaleng.2009.12.005
- Young, I. R., Ribal, A. (2019). Multiplatform evaluation of global trends in wind speed and wave height. Science. doi:10.1126/science.aav9527
- Barnard, P. L., et al. (2015). Coastal vulnerability across the Pacific dominated by El Niño/Southern Oscillation. Nature Geoscience. doi:10.1038/ngeo2539
- Komar, P. D., Allan, J. C. (2008). Increasing hurricane-generated wave heights along the U.S. East Coast and their climate controls. Journal of Coastal Research. doi:10.2112/07-0894.1
- Menne, M. J., Williams, C. N. (2009). Homogenization of temperature series via pairwise comparisons. Journal of Climate. doi:10.1175/2008JCLI2263.1
- Bouchard, R. H., Jensen, R. E., Montalvo, S., Kamranzad, B. (2018). Finding NOMAD: an examination of the impacts of changing wave systems on long-term wave measurements. Ocean Sciences Meeting 2018. https://strathprints.strath.ac.uk/84172
