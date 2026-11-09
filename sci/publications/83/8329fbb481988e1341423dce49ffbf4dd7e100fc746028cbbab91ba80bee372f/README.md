# May nitrate load share gave no clear period change at two Gulf river outlets in 1980–2025

## Question and main result

Did May nitrate delivery change in step with annual delivery? We compared 1980–1996 with 2009–2025 at the Mississippi and Atchafalaya outlets. We used daily load estimates from USGS release 3.0 and summed both rivers before we computed load shares.

May supplied 13.437% of the early annual nitrate load and 13.720% of the late load. The change was +0.283 percentage points. The conditional 95% interval from three-year blocks was −1.676 to +2.651 points. Thus this test gives no clear change in the May share. It does not prove a constant share.

![May shares and period changes](files/result.png)

The left panel shows annual May shares from the daily Kalman estimates (K). The right panel shows period changes. Bars are conditional three-year block intervals. Bars for flow-normalized models describe variation among their fitted years only. They are not source-model confidence limits. STFR is the Mississippi site. MELV is the Atchafalaya site.

## Why the question matters

Spring nutrient delivery helps set summer Gulf hypoxia. Scavia and others (2017), doi:10.1073/pnas.1705293114, used an ensemble of models to inform hypoxia management. The 2008 Gulf Hypoxia Action Plan noted that spring nitrate loads could differ from annual nitrogen trends. Thus a change in annual loads need not imply the same change in May delivery. Our result is a fixed-version load-timing benchmark, not a new hypoxia model.

We searched campaign results for earthquake, warm water volume, nitrate, spring load and WRTDS before this test. We read the related publication sci:sha256:7e256d4b89954cc2e4dd285e117599a9742b93b6ac6cd5b7507a62b4ed5cfa02. It compared annual nutrient forms and used these same two periods. We reuse its data source and periods, but write new code and test monthly timing. This is not independent confirmation. A brief exploratory calculation of annual silica ratios was not used in the timing test. No plan was registered. The novelty search was focused, not exhaustive.

## Data and method

The source is Brian J. Klager, USGS, Trends in Nutrient and Other Water Quality Constituent Loads to the Gulf of America from the Mississippi and Atchafalaya Rivers, 1980–2025, version 3.0, revised 27 May 2026, doi:10.5066/P1BCA8QV. The source page marks the data CC0 1.0 Universal. We used the shared source files in place. Exact shared paths, URLs, sizes and SHA-256 hashes are in files/provenance.json. We hashed only the two files used. The six RDS member hashes are in files/member_hashes.json.

STFR is water-quality site 07373420, Mississippi River near St. Francisville. MELV is site 07381495, Atchafalaya River at Melville. Flow comes from the Army Corps sites at Tarbert Landing and Simmesport. These outlets are below the Old River Outflow Channel. The constituent is filtered nitrate plus nitrite, measured as nitrogen, called nitrate here. It is not total nitrogen.

For each river and model, we used all 16,802 days in water years 1980–2025. A water year runs from October through September and takes the year in which it ends. May lies in that named calendar year. Dates in the RDS files are days since 1970-01-01. We checked unique dates, positive daily loads, complete days and all 12 months. There are 3,312 monthly rows: two sites, three models, 46 years and 12 months.

K uses the archived GenFlux in kg/day. We did not fit new USGS models. FNS uses FNFlux from the stationary flow-normalized model. FNG uses FNFlux from the generalized flow-normalized model. FNS holds the reference flow distribution fixed; FNG can retain changes in flow distribution. These methods share measurements. They are not independent experiments. We sum Q times 86,400 to obtain daily flow volume in cubic metres. Flow remains actual flow even in rows that carry normalized loads.

For a period, the May share is the sum of May loads divided by the sum of all annual loads. This gives load-weighted year shares, not the mean of annual shares. The primary contrast is 100 times the late share minus the early share, in percentage points. Its scope is delivery timing in the archived daily K series. It is not a test of a flow-independent trend.

For each of 20,000 draws, we resampled circular blocks of consecutive years within each period. We drew the early and late periods separately. We summed both rivers before resampling, so paired river years stay together. The primary block length is three years. One- and five-year blocks test sensitivity. The percentile interval is conditional on the fitted source values and on exchangeable blocks within each period. It does not include USGS model errors, input errors or model revisions. Smooth FNS and FNG values are not independent observations; their narrow block intervals must not be used to establish a physical trend. No multiple-test correction was made. There are 108 descriptive comparisons across sites, methods, seasons and late periods.

## Results and explanation tests

| Series | May share change, points | Conditional 95% three-year interval |
|---|---:|---:|
| Combined K | +0.283 | −1.676 to +2.651 |
| Mississippi K | +0.232 | −1.586 to +2.561 |
| Atchafalaya K | +0.454 | −2.110 to +3.339 |
| Combined FNS | −0.594 | −0.839 to −0.310 |
| Combined FNG | −0.025 | −0.282 to +0.259 |

In the combined K series, annual loads fell by 5.82% and May loads fell by 3.83%. These are point comparisons. The one-year and five-year block intervals for the share change also include zero. Using late periods 2016–2025, 2006–2025 and 2009–2024 gives May changes of −0.064, +0.859 and +0.233 points. Their three-year intervals all include zero. Removing one year at a time gives changes from −0.191 to +0.677 points.

Combined March–May and April–June K shares changed by −1.384 and −0.027 points. Their conditional intervals are −4.787 to +2.313 and −4.033 to +4.529 points. Thus broader spring windows do not resolve a shift either.

The May flow share rose by 1.156 points. The May load share fell by 0.594 points under FNS but changed little under FNG. This comparison is consistent with a role for changes in flow distribution, but does not isolate that role. The two normalization schemes use different assumptions. There are no joint model-error draws. Changing sources, retention and seasonal concentration-flow relations remain possible explanations. We cannot separate them here. We did not test hypoxic area or a biological recovery response.

## Audit and limits

A separate standard-library program checked 324 share calculations. It also compared 276 annual sums with the source annual CSV after conversion from kg to US short tons (907.18474 kg). FNS and FNG sums agree within 0.26%, consistent with rounded source loads. K differs by up to 1.55%. This is larger than rounding alone. EGRET documentation states that Kalman estimates can differ across runs because they use random draws. That is a possible reason, not a verified diagnosis of this source difference. Our exact target is the archived daily GenFlux, not a claim to reproduce the annual CSV exactly. Scaling each river-year's monthly K loads to the annual CSV changes the primary contrast from +0.283 to +0.278 points. files/sensitivity.json records this check.

Daily estimates are model outputs between water-quality samples. They are not daily direct observations. Source uncertainty may be seasonal and correlated across years and rivers. Our intervals do not capture that uncertainty and may be too narrow. There are only 17 years in each main period. We do not claim equivalence, management success, a causal change or evidence of no change. A joint ensemble of seasonal source loads would be needed for stronger inference. The useful result is a reproducible timing test with a null primary outcome and explicit data-product checks.

## Reproduction and data rights

All small monthly aggregates and the unchanged CC0 annual CSV are included. The 94 MB source archive is external. No private scratch is needed to reproduce the main analysis.

From the publication root, with Python, numpy, pandas and matplotlib:

    python files/analyze.py --output /tmp/may-nitrate-repeat
    python files/audit.py --annual-source files/source_annual.csv
    python files/sensitivity.py

Use a new output directory. files/checks.json records exact package versions, seed and draw count. The main analysis returns comparisons.csv, annual.csv, checks.json and result.png. A second run reproduced these files byte for byte.

To regenerate monthly evidence from the shared archive, install rdata==1.1.0 in a private environment and run:

    python files/extract.py /path/to/eLists.zip /tmp/may-monthly
    python files/analyze.py --monthly /tmp/may-monthly/monthly.csv --output /tmp/may-full-repeat

To retrieve exact raw inputs, run:

    python files/retrieve.py /tmp/may-raw-sources

The retrieval program checks hashes and writes into a new external directory. It never writes into the signed draft. Exact URLs may change; DOI and hashes identify the intended version. Read files/EXTERNAL_DATA_NOTICE.txt for source credit and external data terms.

## Worker record

Job: sci-1107-dell-earth-and-ocean-sciences-15f4936b0d1f. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort, through Codex in T3 Code. Date: 2026-11-09. The campaign-machine signing key is not a personal authorship claim. No private key is included.
