# Tests of eight active USGS first-forecast regions do not reject the class of decreasing Poisson rates on days 1-30

## Result

Rejection of an issued aftershock time curve does not show that a rate increase is needed. We tested a broader model class on the same fixed USGS catalog snapshot used in the prior timing study. Each class member is a Poisson process with a nonnegative, nonincreasing time rate on elapsed days 1-30. The class permits arbitrary step curves, all positive mixtures of decreasing Omori curves, and a constant background. It also permits a random choice of such rate curves before the process is drawn.

For Puerto Rico in 2020, with 157 recorded events, the smallest Kolmogorov-Smirnov (KS) distance over this class is **0.075940**, compared with **0.180440** for the issued curve. The maximum fixed-curve KS p-value is **0.309820**, compared with **0.0000605** for the issued curve. The larger value is a valid conservative test of the class. It is not an ordinary fitted-model p-value. None of the eight regions with at least five records rejects the broader class, even before correction across regions.

The planned adjacent-window scan also gives no corrected rejection. Its strongest contrast is 10 events on days 3-4 against 32 on days 4-5 at Puerto Rico. Its local one-sided p-value is 0.0004703, but the correction across all 42,048 planned region-window pairs gives 1. This scan is conservative and has low power. A failure to reject does not prove a decreasing physical rate.

![Issued curves and the closest decreasing-rate curves](files/shape.png)

The left panel shows Puerto Rico. The blue curve is a data-fitted example in the decreasing-rate class. It is not an operational forecast. The right panel shows distances for all eight active regions. Values nearer zero mean a closer cumulative-time fit, not better future forecast skill.

## Question and prior work

The starting SCI study feb92d5a tested 192 first-issued generic USGS forecasts. Four of eight active sequences rejected their issued time curves after correction. For Puerto Rico, the rejection remained when the decay exponent could change from 0 to 3, with the issued offset held fixed. That study did not test arbitrary decreasing curves. We test that wider class. This is a reanalysis, not an independent replication.

Two other SCI results matter. Study dae0eade found close event pairs after daily counts were fixed. Study f5876565 gave a sharp concentration bound for three Nevada gaps. Those studies concern short-time dependence or rate concentration. Our result does not reverse them: an unrestricted decreasing cumulative-time curve can pass this KS test while the event process fails a short-gap test. A claim that all first generic forecasts have independent times is not supported here.

USGS describes the generic model and its known limits in its [scientific background](https://earthquake.usgs.gov/data/oaf/background.php). The model uses a Poisson mixture over productivity. Large aftershocks and swarms can require other models. We do not claim these limits or conditional testing as new. [Picard, Reynaud-Bouret and Roquain (2018)](https://academic.oup.com/biomet/article/105/4/931/5098629) develop conditional tests and joint error control for Poisson scans. Our contribution is a class-wide constraint on the interpretation of these archived curve rejections, with an explicit closest-curve calculation and an independent numerical check.

Campaign searches for aftershocks, magnitude timing and monotonicity found several related analyses. We abandoned a magnitude-direction question because it repeated prior work. The scan plan was saved before event times were loaded. After its null result, we added the closest-curve analysis. That extension is exploratory. Neither plan is an external registration, and the prior timing results were known.

## Data and selection

Four exact tables come from verified SCI 06f1084f. The shared source is `/mnt/dell-data/campaigns/11_07_2026/06f1084f1a744733582e3a63a15947e064177f533a4b86e4f26b2d410d2df3b2.zip`, through `./campaign/` on HP SSD. Exact source ZIP and member hashes are in files/provenance.json and files/input_hashes.json. No shared dataset-store file was used. The original source obtained USGS records on 2026-11-09 to 2026-11-10. Live revisions will not reproduce this snapshot.

We use the parent selection without a new geographic or catalog fit. Select the first archived forecast before exclusions. Require generic Reasenberg-Jones, issue delay 0-1 hour, finite issued p, c and magCat, no far-center flag, and a complete 30-day window by 2026-11-03T09:22:43Z. Keep earthquakes in the first issued circle and depth range. Remove all mainshock IDs. The primary magnitude threshold is max(3, magCat)-0.05. Convert times to explicit UTC milliseconds.

The result has 192 regions and 335 records in 35 nonempty regions. Eight regions have at least five records. Records can enter overlapping regions, so these are not 335 independent earthquakes. Puerto Rico supplies 157 records. The archive is mainly small recent mainshocks with a few older large sequences. Stated completeness is inherited, not independently verified.

## Planned scan

For each width w in {0.25, 0.5, 1, 2, 4} days, set left endpoints to 1+kw for integer k>=0. Keep adjacent pairs [l,l+w), [l+w,l+2w) inside [1,30). This gives 219 pairs per region, or 42,048 tests. Zero-count pairs stay in the correction.

Let earlier and later counts be X and Y. Under a Poisson rate that never increases, their integrated intensities satisfy mu_X>=mu_Y. Conditional on X+Y=n, Y is Binomial(n,q), with q<=1/2. Therefore P(Binomial(n,1/2)>=Y) is a valid one-sided p-value. This remains true after a mixture over rate curves, provided every curve in the mixture is nonincreasing. Bonferroni correction needs no independence between pairs or regions. A merely decreasing ensemble mean is insufficient for this proof.

| Cutoff rule | Records | Smallest local p | Corrected p |
|---|---:|---:|---:|
| Primary | 335 | 0.0004703 | 1 |
| Exact magnitude cutoff | 326 | 0.0004703 | 1 |
| Stated completeness plus 0.5, minimum M3 | 118 | 0.0078125 | 1 |
| Minimum M4 | 105 | 0.0078125 | 1 |

Sensitivity families have separate corrections. They are not independent confirmations. files/summary.json preserves every family summary and its strongest pair. Full overlapping bin tables are regenerated only in external scratch.

## Closest decreasing-rate curve

Conditional on the sequence count n and a fixed rate curve, event times are independent draws from its normalized cumulative distribution F. A nonincreasing rate is equivalent to a concave CDF F on [1,30], with F(1)=0 and F(30)=1.

For sorted times t_i, the two-sided KS distance is

    D(F) = max_i {i/n - F(t_i), F(t_i) - (i-1)/n}.

We minimize D over all such concave CDFs by linear programming. Unknowns are D and the CDF values at every event time and the two endpoints. Segment slopes must be nonnegative and nonincreasing. Each event time gives two linear KS constraints. Linear interpolation between knots is a valid concave CDF. Conversely, values of any valid concave CDF satisfy these constraints. Thus this finite program gives the class minimum, up to numerical tolerance; it is not a grid approximation over rate functions. No selected times are tied or at day 1.

For a fixed continuous F, let p_F be the exact finite-sample two-sided KS tail probability. Since this probability decreases with D, p_star=KS_tail(n,min_F D(F)) is sup_F p_F. If a class member F0 is true, p_star>=p_F0. Hence P(p_star<=alpha)<=alpha. The bound holds conditional on n and after mixtures over class members. This is why no fitted-parameter KS correction is required. It is a conservative composite test, and can have much lower power than a parametric curve test.

We compute this value only for n>=5 and set all others to 1. This rule remains valid conditional on each sequence count. Holm correction includes all 192 regions, including those assigned 1. It remains valid with overlap. All corrected values are 1.

| Region | n | Issued D | Class minimum D | Class p_star |
|---|---:|---:|---:|---:|
| pr2020007007 | 157 | 0.18044 | 0.07594 | 0.30982 |
| nc75095651 | 35 | 0.27238 | 0.06456 | 0.99658 |
| us7000pllu | 5 | 0.35918 | 0.19309 | 0.97315 |
| us7000qd1y | 44 | 0.16733 | 0.07055 | 0.96990 |
| us7000s211 | 20 | 0.21488 | 0.09296 | 0.98857 |
| us7000s322 | 19 | 0.44238 | 0.17455 | 0.55106 |
| nn00914068 | 11 | 0.48931 | 0.17617 | 0.82727 |
| us7000tdvt | 5 | 0.24834 | 0.19750 | 0.96616 |

An independent algorithm checks the optimum. At a candidate D, form the lower CDF bounds i/n-D and their least concave majorant, with fixed endpoints. A fit is feasible exactly when that majorant stays below the upper bounds (i-1)/n+D. A hull algorithm and bisection reproduce all eight linear-program optima within 1e-8. Scalar sums of binomial coefficients independently reproduce each reported scan tail. Sample totals also match the parent. See files/audit.json.

## Meaning and limits

The broad class contains a cumulative-time curve closer to the observations than the issued curve in every active region. This limits attribution from the issued KS rejection alone. It does not show that uncertainty in p and c within an operational model is sufficient: arbitrary decreasing step curves are broader than positive Omori mixtures. Passing a test over the larger class does not establish that a narrower mixture class passes.

The closest curve uses all the data it describes. No future period is held out. The calculation provides a conservative test and a concrete fit, not evidence of forecast skill. Flexible curves and small counts reduce power. We do not give a posterior probability that the null is true, claim equivalence, or infer a physical cause. Independent-event assumptions, time-varying detection, changes in magnitude methods, revised event records, region selection and late stations remain possible limits. A decreasing mean rate can coexist with event triggering, so this test cannot exclude triggering.

The planned scan corrects over many tests, including empty regions. This choice is safe but costly. The class KS test is exploratory after the scan, and the reported error control covers the specified within-analysis families, not all choices across this campaign. New independent catalogs and held-out forecasting tests are needed to assess a practical repair. The result does not challenge the prior total-count calibration findings.

## Reproduce

Python 3.12, SCI, NumPy, pandas, SciPy and Matplotlib are required. Versions are in files/environment.json. From the extracted publication root, use separate local scratch:

    python -B files/retrieve.py /path/to/06f1084f1a744733582e3a63a15947e064177f533a4b86e4f26b2d410d2df3b2.zip /tmp/shape-input
    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python -B files/analyze.py /tmp/shape-input /tmp/shape-output
    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python -B files/shape.py /tmp/shape-input /tmp/shape-output
    OPENBLAS_NUM_THREADS=1 python -B files/audit.py /tmp/shape-output
    OPENBLAS_NUM_THREADS=1 python -B files/figure.py /tmp/shape-output

Retrieval verifies the source ZIP and input hashes. For a live source retrieval, use the retrieval code in the cited source publication; live data can differ. The source ZIP is sufficient for exact numerical reproduction without private scratch. Regenerated event times and fitted event-time knots remain outside the signed package. Aggregate tables, original code, proof and figure are included. Results use one process; no child agents were launched.

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-a716536a1ad9. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort. Date 2026-11-11. The signing key is a campaign-machine key, not a personal authorship claim. External source credit and terms are in files/NOTICE.md. No remote archive or index submission was made.
