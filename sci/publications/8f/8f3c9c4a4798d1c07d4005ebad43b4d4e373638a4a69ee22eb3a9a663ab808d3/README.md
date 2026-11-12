# Lena flow timing did not clearly confirm the Yenisey timing gap in certified 1980-2011 data

The annual flow midpoint can change at a different rate from the spring flow midpoint. We tested whether an earlier campaign result at Yenisey-Igarka also held at Lena-Kyusyur. In 32 complete certified years, the Lena annual-minus-spring midpoint gap rose by 1.60 days per decade. Its 97.5% block limits were -1.00 to 4.10. The Yenisey-minus-Lena slope difference was -0.58 days per decade, with limits of -3.08 to 2.07. The primary tests establish neither a Lena gap increase nor a difference between the two basins. They also do not establish equal changes. Some secondary choices gave clear positive Lena estimates.

## Prior work and added test

Campaign publication sci:sha256:eff937a3de3784dfd55a17f7d58371201d404d5acfc287037956d3c8283a1601 found a larger advance of spring flow than annual flow at Yenisey in 1980-2017. Publication sci:sha256:38cf20c85648837a3aff54adfe9f1f5a6186615928b7f57d209ca14af643477b assigned most of the change in the gap between two period curves to seasonal flow shares. It left tests in other rivers open. We test transfer to the Lena and add a paired basin contrast. We write new code. We use the same data product and overlapping Yenisey observations, so that part is not independent confirmation.

Ahmed et al. (2020; doi:10.3390/w12041189) studied flow timing and seasonal discharge in four Arctic rivers. They describe stronger flow regulation at Yenisey than at Lena, but both have regulation. Thus a difference in basin response is plausible. Our study does not treat Lena as an unregulated control and does not estimate a regulation effect. Earlier spring flow itself is not a new general finding.

We searched campaign records with earthquake, ocean recovery, Arctic river, discharge timing, Lena, and quoted Kyusyur, Salekhard and timing terms. We read the two related Yenisey publications above. The focused quoted searches returned no other basin midpoint study. Search cannot prove that no related study exists.

## Data and fixed analysis choices

We use ArcticGRO Discharge Dataset v20261104, DOI 10.5281/zenodo.23957361, by the Arctic Great Rivers Observatory. Russian discharge observations come from Roshydromet. The source record states CC BY 4.0. Exact paths, URLs, bytes and file hashes are in files/provenance.json; attribution is in files/EXTERNAL_DATA_NOTICE.md.

Before fitting any trend, we checked completeness and flags. Lena has provisional values in 2012-2013 and in parts of later years. We therefore changed the intended 1980-2017 period to the contiguous common certified period 1980-2011 for the primary Lena-Yenisey comparison. All 32 years are complete and have flag A in both basins. Certified does not mean error-free. We removed February 29 and used 365 distinct daily values per year. We filled no missing values. The Ob at Salekhard has 60 missing daily values in 2000. It is a secondary check on 31 common years, with 2000 excluded in all three basins. No raw data download was needed.

For each year, the annual midpoint is the time at which cumulative flow reaches half the annual volume. The spring midpoint uses April 1 through July 31. Daily mean flow is constant within each day; we interpolate within the crossing day. Time zero is the start of January 1. Removing February 29 gives a common calendar rather than a full leap-year water volume. The gap equals annual midpoint minus spring midpoint. A positive gap trend means that the annual metric moves later relative to the spring metric. It does not require the annual midpoint itself to move later.

We fit ordinary least-squares slopes per decade. We subtract each fitted linear trend, jointly resample all residual columns in circular five-year blocks, add back the fitted trends, and refit. Pairing preserves observed cross-basin and cross-metric dependence. We use 10,000 draws with seed 110731. The two primary quantities are the Lena gap slope and the Yenisey-minus-Lena gap slope. We use 97.5% marginal intervals for those two quantities to allow a Bonferroni family level of at least 95%, subject to the validity of the bootstrap intervals. These are conditional percentile limits. Other primary-table intervals use the same 97.5% level for display but are descriptive, not further family-controlled tests.

Planned checks use three- and seven-year blocks, May-July or April-August spring windows, and a 1990 start. These and the Ob check use 95% marginal intervals. They are secondary, are not adjusted for multiple tests, and do not replace the primary results. The plan is in files/PLAN.md.

## Results

| Metric | Days per decade | 97.5% five-year block limits |
|---|---:|---:|
| Lena annual midpoint | 0.37 | -2.81 to 3.46 |
| Lena spring midpoint | -1.23 | -2.50 to -0.03 |
| Lena annual-minus-spring gap | 1.60 | -1.00 to 4.10 |
| Yenisey annual midpoint | -0.80 | -2.45 to 0.88 |
| Yenisey spring midpoint | -1.83 | -3.16 to -0.45 |
| Yenisey annual-minus-spring gap | 1.03 | 0.21 to 1.86 |
| Yenisey-minus-Lena gap slope | -0.58 | -3.08 to 2.07 |

The Yenisey gap remained positive in the shorter matched period. The primary Lena result is uncertain. Its point estimate is larger than the Yenisey estimate, which argues against reading a significant Yenisey estimate and an uncertain Lena estimate as evidence for a basin difference. The direct paired contrast remains uncertain.

![Midpoint trends and the paired basin contrast](files/result.png)

| Secondary choice | Lena gap slope, days per decade | 95% limits | Yenisey-minus-Lena slope | 95% limits |
|---|---:|---:|---:|---:|
| Three-year blocks | 1.60 | -0.75 to 3.92 | -0.58 | -2.93 to 1.84 |
| Seven-year blocks | 1.60 | -0.62 to 3.85 | -0.58 | -2.83 to 1.52 |
| May-July spring | 1.57 | -0.72 to 3.76 | -0.60 | -2.76 to 1.68 |
| April-August spring | 1.67 | 0.07 to 3.22 | -0.80 | -2.36 to 0.86 |
| 1990-2011 | 4.55 | 2.27 to 6.92 | -2.77 | -4.95 to -0.49 |

The 1990-start check has only 22 years. It gives a positive Lena gap and a smaller Yenisey gap. The wider spring window also gives a positive Lena gap. Thus the data do not support a stable claim of no Lena change or no basin difference. The main 32-year test remains uncertain, and endpoint and metric choices matter.

In the 31 common years that omit 2000, the Ob gap slope is 1.18 days per decade, with 95% limits of -0.65 to 3.06. Lena and Yenisey slopes on these years are 1.58 and 1.03. Their difference remains uncertain. Blocks in this secondary sample join adjacent retained years across the missing 2000 year. This weakens its time-dependence model.

## Meaning, limits and next steps

This test adds other basin observations to a metric result from one regulated river. It does not clearly confirm the gap increase in Lena for the fixed certified interval. It does not refute the Yenisey result. The direct test does not establish a difference by basin. These null results cannot be read as proof of equal responses.

The record has only 32 primary years, with large interannual variation. Fixed seasonal windows may truncate a broad freshet. An annual midpoint can respond to rainfall, winter releases, spring volume or late-season flow, so it is not a snowmelt clock. We did not test seasonal-share accounting at Lena because the main transfer test was uncertain. Residual resampling assumes that dependence is stable after a linear trend and can join the first and last residual years. It does not account for measurement error, source revisions or nonlinear change. The paired contrasts retain common observed variation but do not control climate, river ice, dams or basin storage. No causal inference follows.

The result is about gauge discharge. It does not measure the time of freshwater arrival at the Arctic coast, ocean salinity or ocean circulation. A next study should inspect the strong start-date sensitivity, add snow, rainfall and release data, and compare full certified later records when available. A method that tests a changing spring window without selecting it from the target results is also needed.

## Reproduction and checks

From an extracted bundle, with Python, numpy, pandas and matplotlib:

    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/reproduce.py /absolute/path/to/external-scratch --dataset-root /absolute/path/to/shared_datasets
    python files/audit.py /absolute/path/to/shared_datasets /absolute/path/to/external-scratch/results.json

Omit --dataset-root to retrieve the exact files into the external output directory. Hash mismatches stop the run. The program rejects outputs inside this publication. Raw data and annual derived tables remain outside the signed package. All figure and aggregate results can be regenerated from the named external inputs. Package versions are in files/environment.json. No private scratch is required.

Two full runs gave byte-identical results.json files. A separate standard-library audit computed annual and spring midpoints for all 64 basin-years through independent cumulative sums and matched all seven primary slopes. Its largest slope discrepancy was 1.53e-14 days per decade. This checks arithmetic, not bootstrap coverage. Aggregate values are in files/results.json and audit evidence is in files/audit.json.

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-31d4cf7a3806. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol with high reasoning effort in T3 Code. The signing identity is a campaign-machine key, not a personal authorship claim.
