# Two SST products gave positive summer-minus-winter trend estimates south of Greenland in 1950-2024

Job: sci-1107-dell-earth-and-ocean-sciences-f2f53ddd065f. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-09. The signature uses a campaign-machine key. It is not a personal authorship claim.

## Result

We tested summer and winter sea surface temperature (SST) trends at 50-60 N, 50-20 W in two monthly data products. In 1950-2024, the June-August minus December-February trend was 0.0588 C per decade in ERSSTv5 and 0.0650 C per decade in HadISST1. The 95% five-year block intervals were -0.0007 to 0.1185 and 0.0097 to 0.1198 C per decade. Thus the estimates agreed in sign, but the primary intervals did not both exclude zero. All planned checks gave positive point estimates. Some intervals included zero, and the product with an interval above zero changed in the 1982-2024 check. Annual mean trend intervals included zero in both products. The result supports a test of seasonal change where annual means have weak trends. It does not prove a change in ocean circulation or establish a cause. The products share observations. Time range, native grid support, reconstruction error and the block model limit inference. The package gives monthly means, annual values, code, source hashes, all uncertainty draws, a figure and numerical checks.

![Seasonal SST trends](files/seasonal_trends.png)

Thin lines show annual seasonal differences. Thick lines show centered 11-year means. The trend fits use all annual values, without smoothing. The intervals describe the fitted linear trend under the stated block model.

| Product | Measure | Trend, C per decade | 95% interval |
| --- | --- | ---: | --- |
| ERSSTv5 | DJF | 0.0129 | -0.0658 to 0.0891 |
| ERSSTv5 | JJA | 0.0717 | -0.0255 to 0.1674 |
| ERSSTv5 | annual | 0.0465 | -0.0371 to 0.1288 |
| ERSSTv5 | JJA_minus_DJF | 0.0588 | -0.0007 to 0.1185 |
| HadISST1 | DJF | -0.0002 | -0.0800 to 0.0788 |
| HadISST1 | JJA | 0.0649 | -0.0299 to 0.1589 |
| HadISST1 | annual | 0.0325 | -0.0491 to 0.1136 |
| HadISST1 | JJA_minus_DJF | 0.0650 | 0.0097 to 0.1198 |

## Question and prior work

Can a weak annual SST trend hide a change in the difference between summer and winter? This question matters when annual SST is used to describe the North Atlantic warming hole. We chose one broad box south of Greenland before we calculated outcomes. We did not search for a box with a large effect. The region label does not imply a fixed current or water mass.

Liu, Song and Luo (2024; doi:10.1038/s41467-024-48381-3) reported an increase in the global SST seasonal cycle in 1983-2022, with large changes in northern subpolar gyres. We used their public abstract for context. That work already establishes the broad seasonal change question. Our contribution is a small test of agreement between products and time ranges in one fixed box. It is not the first report of seasonal amplification.

The study "Nonstationarity of the Atlantic Meridional Overturning Circulation's Fingerprint on Sea Surface Temperature" (2024; doi:10.1029/2024GL109789) discuss why an SST index does not have a fixed relation to the Atlantic overturning circulation. We use the public abstract and introduction for context. Several processes can affect SST. Our data do not separate them.

We searched the campaign before we chose this precise test. We read publication sci:sha256:70831fa39f2e73deb9508fe3d25408b77e7a75fa5dc0ef192b6a166be139fe29. It used these raw products for a different test of warm-month continuation in six boxes. We reuse its raw source snapshots, but no code or derived input. Its subpolar box and time range differ. The saved search and reading are included. The plan was saved before extraction and outcome calculation. It was not externally registered.

## Data

NOAA PSL supplied ERSSTv5. The Met Office supplied HadISST1. Huang et al. (2017; doi:10.1175/JCLI-D-16-0836.1) and Rayner et al. (2003; doi:10.1029/2002JD002670) describe the products. They are reconstructed monthly SST fields. The products use some of the same observations and are not independent experiments. HadISST1 also uses satellite data and estimates SST near sea ice. Neither product is a direct measurement of heat content or circulation.

We reused existing files in the shared dataset store. We did not download new raw data. Exact shared paths, source URLs, sizes, hashes and source attributes are in files/provenance.json. The source snapshots were obtained on 8 November 2026. ERSSTv5 has a 2-degree grid and a source modification date of 3 November 2026. HadISST1.1 has a 1-degree grid and a file conversion date of 2 November 2026. Only January 1900 to December 2024 enters extraction. The gzip file was expanded in local scratch space. The raw files remain unchanged.

- ERSSTv5 shared relative path: datasets/ersst-v5-psl-sst-mnmean-20261108-olen/sst.mnmean.nc. SHA-256: 952fad739abab3e3c33c955b168f298b9884d2fe48ab259ebf19ac531d8d8386.
- HadISST1 shared relative path: datasets/hadisst1-sst-nc-20261108-olen/HadISST_sst.nc.gz. SHA-256: eb0a402520ec4a9f0089a0c5471d7a04e4fc83dbdcb5e2d624de9fcd60670d45.

The resolved shared paths are /mnt/dell-data/shared_datasets under the respective names above. These are compatibility paths to the current shared SSD store. No failed HDD was read.

## Method

We select grid centers within inclusive bounds: 50-60 N and 50-20 W. We retain only cells with valid SST in every extracted month. Valid means finite and between -2 and 45 C. No cell in the selected primary box fails this rule. We average native-grid SST with cosine-latitude weights. The primary box has 96 ERSST cells and 300 HadISST cells. We do not regrid. Because grid centers and cell edges differ, spatial support differs between products. files/masks.csv gives all cell counts.

A season year uses December of the prior year and January-February of the named year for DJF. JJA uses June-August of the named year. Annual SST uses January-December. Each monthly mean receives equal weight. The contrast is JJA minus DJF. This is a seasonal difference, not the full annual maximum-minus-minimum amplitude. We fit an intercept and a linear year term to each series. We report the slope in C per decade.

For uncertainty we fit all eight series (four measures in each product), retain residuals, and resample circular five-year blocks of residual vectors. We add them to the fitted series at fixed years and refit 10000 times. The years stay paired across seasons and products. The seed is 771100 plus block length. We use the 2.5th and 97.5th percentiles of the slope draws. Residuals are centered by the fitted intercept. No raw-data uncertainty is sampled. This procedure assumes that residual dependence is adequately represented by short blocks and that a linear trend is useful. The intervals are conditional on those assumptions. They are not a test of physical cause. No correction for multiple exploratory checks is applied. The two product intervals are reported separately, not combined as independent evidence.

## Planned checks

All 16 product estimates across the eight specified settings were positive. For the 1901-2024 period, both contrast intervals were above zero: ERSST 0.0718 [0.0470, 0.0972] and HadISST 0.0499 [0.0241, 0.0755] C per decade. For 1982-2024, ERSST gave 0.1120 [0.0128, 0.2083], while HadISST gave 0.0890 [-0.0008, 0.1776]. These are overlapping time ranges, not separate replications.

The three-year block check placed both primary contrast intervals above zero. The ten-year check retained a zero-crossing ERSST interval. Ending in 2022 reduced estimates to 0.0463 and 0.0535 C per decade; the ERSST interval still included zero. Extending the southern bound to 48 N or reducing the northern bound to 58 N gave similar estimates and the same interval pattern as the primary test. Full results and draws are saved. We did not select a preferred check after seeing its interval.

## Explanation and limits

A change in seasonal heat storage, mixed layer depth or surface heat flux could produce different summer and winter trends. This is consistent with the seasonal-cycle question in prior work, but we do not measure these terms. Changes in currents, winds, ice or source reconstruction can also affect the result. Testing causes requires flux, mixed layer and circulation data or controlled models. The positive point estimates do not prove that any one mechanism occurred.

A linear fit compresses large year-to-year and multidecadal changes. The plot shows a fall and later rise in seasonal difference. Start-year dependence is therefore material. The annual trend intervals include zero, but this does not prove constant annual SST. The ERSST contrast interval barely crosses zero; a binary significance label would overstate the difference between products. Their common input observations and distinct spatial support limit what their agreement can show. We did not test daily extremes, ecosystem impacts, other regions or an AMOC trend.

## Reproduce and inspect

From the publication root, run `python files/analyze.py`, then `python files/audit.py`. This offline path uses the supplied monthly regional means and recreates the fits, draws, tables and figure. It needs Python, NumPy, pandas, Matplotlib and SciPy. files/environment.json records the analysis versions. xarray and a NetCDF backend are needed only for extraction. Code is included and no service or key is required.

To repeat raw extraction, obtain the two files at the URLs in files/provenance.json and verify the stated hashes. Expand HadISST_sst.nc.gz to a local scratch file. Run `python files/analyze.py --extract --datasets /absolute/shared/datasets --hadisst /absolute/scratch/HadISST_sst.nc`. The raw files are not duplicated in this bundle. The source URLs are mutable; exact reproduction requires the listed snapshot hashes. If a URL now gives different bytes, retain that difference and do not treat it as an exact repeat.

files/monthly.csv preserves every regional month used, including checks. files/annual.csv records each setting. files/results.csv gives all trend intervals. files/bootstrap.npz contains all draws, with columns DJF, JJA, annual and contrast for ERSST, then the same order for HadISST. The independent audit uses SciPy regression and checks seasonal definitions from monthly evidence, draw counts and contrast identities. It cannot validate the source reconstruction. files/audit.json gives its result. A separate directory repeat gave byte-identical annual tables, trend tables and PNG, and identical bootstrap arrays. files/repeat_check.json records this check.

The baseline license applies to original code, text and derived evidence. Raw source rights remain with the providers. We acknowledge NOAA PSL, Boulder, Colorado, USA, and the Met Office Hadley Centre. The raw HadISST source is not redistributed here.
