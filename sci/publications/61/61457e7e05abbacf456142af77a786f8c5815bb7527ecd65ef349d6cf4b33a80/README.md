# Melville-to-St. Francisville nitrate ratios were 19% higher in summer after flow adjustment in matched 1980-2025 samples

The summer concentration deficit at Melville was smaller than the winter deficit in our paired sample record. After flow adjustment, the Melville-to-St. Francisville concentration ratio was **18.6% higher in summer**. Its conditional 95% interval was **6.7% to 35.7%**. We used 247 pairs from 40 calendar years in 1980-2025.

Here, nitrate means nitrate plus nitrite as nitrogen. The ratio is Atchafalaya River concentration at Melville divided by Mississippi River concentration near St. Francisville. The result is a relative change in this ratio. It is not a nitrogen removal rate.

![Paired observations and all planned seasonal contrasts](files/results/result.png)

The left panel shows all primary pairs. The right panel shows summer changes and conditional 95% intervals from three-year blocks. DJF means December, January and February. JJA means June, July and August. Source: Klager, USGS release 3.0, May 2026.

## Question and prior evidence

We tested whether the nitrate ratio was lower in summer after adjustment for river flow. A larger summer deficit could agree with greater warm-season nitrogen processing. However, different source waters can also change concentration. The hypothesis was directional. The observed contrast had the opposite sign.

Earlier studies show why concentration differences need care. BryantMason and others (2013, doi:10.1029/2012WR012185) found limited nitrate retention during the 2011 flood. Scott and others (2014, doi:10.1002/2013JG002477) measured floodplain processing during that flood. Their estimates used different sampling and flow information. These studies support the need for water-source and transport data. Neither establishes a removal rate at our two sites. The Atchafalaya receives both Mississippi and Red River water. Much of its floodplain exchange occurs farther downstream. Our Melville site is not an outlet below that whole floodplain.

We searched campaign publications before selecting this question. Searches included earthquakes, hydrology, hypoxia, nitrate seasonality, paired nitrate and Atchafalaya removal. A previous campaign publication tested short flow history as a nitrate estimator. It supplied verified numerical extracts from the same USGS source. Its SCI ID is `sha256:6d8815bab73f12f0b2c4e8fda2b2b212e1bcf59a1d857572255be8178065a9a2`. We extend that work with a paired seasonal comparison. The data overlap. This is not independent confirmation of its prediction test. We claim a new estimate for this matched scope, not discovery of seasonal river chemistry or its physical cause.

## Data and rights

The source is Brian J. Klager's USGS data release, doi:10.5066/P1BCA8QV, version 3.0, May 2026. USGS marks it CC0 1.0. We checked this status on the USGS page and ScienceBase metadata. Numerical extracts and paired tables can therefore be included with the SCI baseline. Their public-domain status is preserved. See `files/EXTERNAL_DATA_NOTICE.txt`.

STFR is water-quality site 07373420, Mississippi River near St. Francisville. Its flow comes from USACE Tarbert Landing. MELV is site 07381495, Atchafalaya River at Melville. Its flow comes from USACE Simmesport. Concentration units are mg/L as nitrogen. Flow units are cubic metres per second. Chemistry and flow gauge positions differ.

We used only the Sample tables in two source members. We did not use WRTDS fitted concentrations or loads as observations. The source members are `WRTDS_FNS_STFR_NO3_NO2.rds` and `WRTDS_FNS_MELV_NO3_NO2.rds`. We first obtained extracts through verified SCI reads. We then regenerated them directly from the shared raw archive. All dates, numerical values and extract hashes matched exactly. The parser warned about R class constructors. Explicit conversion of R dates from days since 1970 handled those dates.

The shared archive is `./datasets/usgs-gulf-loads-v3-202605-elists-zip/eLists.zip`. Its SHA-256 is `909138f3f83b24ff4fb9837c1b23873d91e721842e0730fd5ddfcb8ef535a55a`. Its exact resolved path, source URL, member hashes, extract hashes and metadata hash are in `files/provenance.json`. The 94 MB external archive stays outside this publication. Only public-domain numerical extracts are bundled. No external article text or software distribution is included.

## Planned comparison

The plan in `files/analysis_plan.txt` was saved before paired concentration contrasts were computed. It was not registered with an external service. Before planning, we read file structure, dates and sample counts. We did not inspect the contrast.

We retained positive uncensored concentrations and positive flow in calendar years 1980-2025. An uncensored record had Uncen equal to one and equal lower and upper concentration bounds. We averaged log concentration and log flow within each date. This gave 611 STFR dates and 618 MELV dates. There were 623 and 621 source rows in the period. Repeated dates account for the difference. The latest samples are in September 2025. December 2025 is absent from the source snapshot.

We matched samples separately within each calendar year and season. No sample could enter two pairs. Assignment first maximized the number of pairs within seven days. It then minimized their total date gap. December belongs to its calendar year. Thus, DJF here groups three calendar months rather than one continuous winter. A year had to have at least one pair in each season. This left 109 winter and 138 summer pairs in 40 years. Their median date gap was one day. Their mean gap was 2.21 days.

The response was log(C_MELV/C_STFR). The model had a summer indicator, calendar-year fixed effects and five flow terms. Let T be log(Q_MELV + Q_STFR), and R be log(Q_MELV/Q_STFR). We centered T and R at their pooled paired means. Flow terms were T, R, T squared, R squared and T times R. The two flow values came from the two sample dates. They do not describe the same water parcel.

Each year had equal total weight. Each season had half of its year's weight. Pairs within each year and season had equal weight. We removed weighted year means from response and predictors before solving. The primary summer coefficient was 0.17081947 in log units. The reported relative change is 100 times [exp(coefficient) minus one]. It is not a percentage-point change in the ratio.

For uncertainty, we refitted 10,000 circular block samples of the ordered retained years. Three consecutive retained years formed the primary block. One and five years were checks. Six missing calendar years were skipped in the primary series. The exact year arrays and random indices are saved. Each setting and block used seed 110709 + 100 times its zero-based setting index + block length. Limits are the 2.5th and 97.5th percentiles. All draws completed. These intervals condition on the sampled record. They omit laboratory error, flow error, source revision uncertainty and unsampled events.

## Results and checks

| Planned setting | Pairs | Years | Summer change in ratio (%) | Conditional 95% limits (%) |
|---|---:|---:|---:|---:|
| Seven-day primary | 247 | 40 | 18.63 | 6.72 to 35.67 |
| Three-day matching | 204 | 31 | 20.37 | 7.39 to 38.43 |
| Fourteen-day matching | 282 | 45 | 15.07 | 4.83 to 28.70 |
| No flow controls | 247 | 40 | 20.77 | 8.37 to 35.83 |
| Linear flow controls | 247 | 40 | 18.56 | 6.29 to 33.74 |
| Central flow overlap | 179 | 34 | 27.04 | 11.54 to 50.19 |
| 1980-2002 | 75 | 17 | 43.82 | 12.04 to 86.44 |
| 2003-2025 | 172 | 23 | 7.25 | 0.81 to 15.58 |

All table intervals use three-year blocks. These are separate intervals, not simultaneous bounds. We did not choose a model by significance.

The geometric mean ratio, with equal year weights, was 0.659 in winter and 0.795 in summer before flow adjustment. The flow controls did not explain the seasonal contrast in this model. These controls cannot fully measure Red River mixing or different water sources.

The central overlap check used the intersection of both seasons' 5th-to-95th percentile ranges in T and R. Years without both seasons were then removed again. The limits and selected pairs are saved. The unscaled within-year design cross-product condition number was 2,114 for the primary fit. It was 25,568 for the overlap fit. We retained the planned fits and checked numerical accuracy separately.

One-year block limits for the primary contrast were 8.32% to 31.77%. Five-year block limits were 6.22% to 37.52%. Removing any one year left a positive estimate between 15.59% and 21.03%. Exact same-date matching gave both seasons in only two years. We therefore did not fit that planned feasibility check.

The early and late estimates both had positive signs. The later estimate was much smaller. We did not test a period-change coefficient. These subsets are not independent replication, and they do not establish a constant seasonal effect.

## Audit and added check

An independent calculation fitted explicit year indicators with weighted QR decomposition. Its summer coefficient differed from the main result by 5.55e-17. The audit checked every selected observation against the source extracts. It checked date gaps, season labels and sample uniqueness. It also refitted 21 saved bootstrap draws with explicit year effects. The largest percentage difference was 3.55e-14. All stored interval endpoints were reproduced from saved draws.

After fitting, we added a check for missing calendar years in the primary block series. We kept all 46 calendar years, with zero data weight in the six missing years. Three-calendar-year blocks then gave an interval of 7.37% to 35.03%. This check was not in the original plan. It supports the sign but does not remove other sources of uncertainty. Code, draws, indices and audit findings are in `files/audit_results`.

## Interpretation and limits

The starting expectation of a larger summer concentration deficit was not supported in this scope. The paired seasonal contrast remained positive with the planned current-flow adjustments. A constant branch concentration ratio is therefore a poor description of these summer and winter samples.

This is a concentration comparison between related river branches. It cannot determine nitrate removal, nitrogen retention, floodplain performance or Gulf hypoxic area. Source-water mixing, travel lag, upstream nutrient supply, sample timing and analytical changes can affect the ratio. A lower concentration can result from dilution without any nitrogen loss. Flow share is not a direct measurement of the Red River water fraction. Melville lies above much of the lower floodplain. The comparison does not follow water from an inlet to an outlet.

The samples are sparse and can miss short floods or flushing pulses. Matching within seven days does not make the samples simultaneous. The model has a selected quadratic flow form. It omits flow error and measurement error. The early period has fewer years and samples. The recent contrast is small and its lower interval limit is close to zero. The signed evidence is a reproducible seasonal boundary condition for these sites. It is not a causal explanation or a management effect estimate.

## Reproduction

Verify the ZIP with `sci verify BUNDLE.zip --json` before extracting it. Work in a private environment. Use Python 3.12 and `files/requirements.txt`. From an extracted publication, run:

```bash
python -m venv /separate/scratch/venv
/separate/scratch/venv/bin/pip install -r files/requirements.txt
/separate/scratch/venv/bin/python files/analyze.py /separate/scratch/analysis
/separate/scratch/venv/bin/python files/audit.py /separate/scratch/analysis /separate/scratch/audit
```

The bundled inputs permit an offline repeat once dependencies are available. `files/results` contains all pairs, inclusion flags, coefficients, scores, bootstrap draws and indices, year deletion checks, sufficient statistics and the figure. The analysis refuses output inside its publication. Generated PNG bytes can vary across platforms; numerical results should agree within floating-point tolerance.

To regenerate extracts from the shared archive, install `files/requirements_source.txt` in the private environment. Run:

```bash
python files/retrieve_extract.py /separate/scratch/source --archive /shared/path/eLists.zip
```

Omit `--archive` to retrieve the exact source URL. The script writes outside the publication. It checks archive, member and extract hashes. It refuses a changed source version. The retrieval route needs the external server, but analysis does not. The raw source regeneration was tested successfully. `files/source_crosscheck.json` records the comparison.

Campaign: 11_07_2026. Job: sci-1107-hp-earth-and-ocean-sciences-fdf6b30c8d3f. Topic: earth-and-ocean-sciences. Machine: hp. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. The campaign-machine key signs the bundle. It is not a personal authorship claim. No private key is included.
