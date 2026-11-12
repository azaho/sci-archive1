# Sensor-error bounds permitted equal longest joint-exposure runs in September but not August in North Wales in 2021

In a controlled wildflower experiment, heated domes had longer recorded runs of joint high ozone and high air drying demand. Under errors of up to 0.5 C, 5 relative-humidity percentage points and 5 ppb ozone, the longest-run difference remained positive in August. In September, equal longest runs were possible. The total joint-hour difference stayed positive in both months. A stable total-hour sign therefore did not ensure a stable duration sign. These are exact bounds under stated assumptions, not confidence intervals or measured sensor errors.

![Duration contrasts and sensor-error bounds](files/figure.png)

## Question and new test

Does a positive heating contrast in total joint-exposure hours also imply more sustained exposure? A few isolated hours and one continuous episode can have the same hour count. This distinction can matter when climate and pollution studies seek explanations for plant responses. We test atmospheric exposure duration, not biological damage.

The campaign record already reports joint-hour counts for this source. SCI sci:sha256:2e833e35b40dd4089a8f961789bc4ef0f370769b26f6ef9030eda2da07099351 reports exposure and missing-hour bounds. SCI sci:sha256:51e63bdcebf6d84f9bdbb679bca8fa4358b41128b862f9ee6588cb023b30f2fa shows that weekday and clock schedules describe most overlap. SCI sci:sha256:27ecd0924230cdb0a9bf8ef5050cdb1483f67268704b282d23a9503586984b04 gives sensor-error bounds for total hours. We read all three. We use the last study's diagnostic cutoffs and error boxes, but no prior code or derived data. The new test concerns uninterrupted runs and hours in long runs. Biological and weather records overlap completely with those studies. This is an exploratory method extension, not independent confirmation.

Before selection we searched the campaign for phenology, pollution biodiversity, temperature birds, solardomes, the source identifier, Ryalls, and ozone runs. Several other candidate questions already had extensive coverage. The search log gives returned identifiers and titles. Quoted searches for ozone/wildflower and Ryalls returned no matches; unquoted and source-identifier searches found the relevant record.

## Source and observation process

Contains data supplied by UK Centre for Ecology & Hydrology.

Hayes, F.; Sharps, K. (2023). Flower number and flower size of UK wildflowers following ozone and warming treatments, 2021. NERC EDS Environmental Information Data Centre. https://doi.org/10.5285/a33d5ee3-d201-4feb-83b9-765ee5b2c25e .

Eight solardomes held potted wildflowers at Abergwyngregyn, North Wales. Heating targeted ambient plus 4 C. Ozone followed a weekly episode profile. The paired ambient/heated domes were 3/6 at the 30 ppb target, 1/2 at 80 ppb and 5/4 at 110 ppb. Targets describe weekly peaks, not constant concentrations. Ambient weather came from one sensor in dome 7; heated domes had separate sensors. There was one dome per treatment combination. Ten pots do not give ten independent dome assignments.

The release has one row with no hour label. We remove it and verify unique date-hours. We use August and September, with complete grids of 744 and 720 hours. Early weather is missing after equipment failure. We do not interpolate missing values or treat early complete cases as a full season. The source reports some gap filling but provides no flag for it. Gap filling can itself alter runs. We cannot assess that effect. We assume the released hour labels are correct and ordered in the source's time convention. We make no daylight-saving conversion.

## Method and proof

For hourly mean temperature T and relative humidity R, air vapor pressure deficit is:

`V = 0.6108 exp(17.27 T / (T + 237.3)) (1 - R/100)` kPa.

The formula follows FAO-56, chapter 3. Transforming hourly means does not recover subhour exposure. A joint hour has V at least 2 kPa and ozone at least 60 ppb. These inherited diagnostic cutoffs are not plant injury thresholds.

A run is a maximal sequence of consecutive joint hours within one calendar month. Runs can cross midnight. Month edges truncate them. The longest run is zero if no event occurs. H6 is the sum of hours in runs of at least six hours. It counts every hour in a qualifying run, not just the hours after the sixth. We also report H3 and H9 as duration sensitivity checks. These durations were selected before examining duration outputs and have no species-specific biological calibration. We do not use run number, which can decrease when two runs merge.

Error box A allows each true reading to differ by at most 0.5 C, 5 humidity points and 5 ppb ozone. Box B doubles these limits. Humidity stays in [0,100]. Errors can vary by hour and sensor. The shared ambient weather correction stays shared across the target pairs. These are assumed limits, not instrument specifications or estimated errors.

V increases with T and decreases with R in the tested range. Lower event indicators result from lower T and ozone and higher R. Upper indicators use the opposite choices. Thus each allowed true indicator sequence lies between lower and upper binary sequences, coordinate by coordinate.

Both the longest run and Hk are nondecreasing when any false indicator becomes true. Adding a true hour can extend or merge runs; it cannot remove any previously qualifying hours or shorten the longest run. For either statistic F, the exact heated-minus-ambient limits are:

`[F(heated_lower) - F(ambient_upper), F(heated_upper) - F(ambient_lower)]`.

The endpoints are attainable by the extreme readings in the error boxes. They are sharp under this flexible error model. Intermediate integer values need not all be attainable. Shared calibration constraints could narrow the limits. This proof extends the prior total-hour bounds to duration. It does not apply to run number or mean run length.

We compute all nine cutoff combinations of VPD 1, 2, 3 kPa and ozone 40, 60, 80 ppb, at error scales 0, 1 and 2. No resampling or p value is used. The bounds express allowed readings for fixed records, not sampling uncertainty.

## Results

At 2 kPa and 60 ppb, the main results are:

| Month | Peak target | Longest run A/H | Longest difference | Box A limits | H6 A/H | H6 difference | Box A limits |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| August | 80 | 2 / 11 | 9 | 5 to 10 | 0 / 57 | 57 | 24 to 121 |
| August | 110 | 2 / 9 | 7 | 3 to 10 | 0 / 32 | 32 | 13 to 71 |
| September | 80 | 3 / 10 | 7 | 0 to 10 | 0 / 54 | 54 | 0 to 130 |
| September | 110 | 3 / 9 | 6 | 0 to 9 | 0 / 23 | 23 | 0 to 58 |

All values are hours. A/H means ambient/heated. Box A can erase the positive longest-run and H6 contrasts in both September pairs. It cannot reverse them at the main cutoffs. The lower bound of zero is attainable. August keeps positive limits for both duration measures.

For total hours, box A lower differences are 25, 7, 42 and 6 hours in the same row order. These reproduce the prior count result. They remain positive even where the duration bounds reach zero. At the 30 ppb peak target, no main-cutoff joint hours occur in either month. This is a threshold result, not absence of ozone or evidence of safety.

Box B allows September longest-run differences down to -3 hours and H6 differences down to -6 hours at both targets. August still has positive longest-run lower limits of 2 and 3 hours, and H6 lower limits of 6 and 7 hours. Thus duration can be less robust than total hours in one month and more robust in another. The temporal arrangement, not only the marginal count, controls this result.

Across the 36 high-target month and cutoff combinations, box A has positive lower limits in 21 total-hour comparisons, nine longest-run comparisons and 14 H6 comparisons. These counts are diagnostic summaries of related thresholds, not independent tests. All estimates, including zeros, are in duration.csv and contrasts.csv.

## Meaning and limits

This study shows that a sensor-error audit of total exposure hours cannot substitute for a duration audit. August and September share domes, sensors and a season. They are separate windows without shared hours, not independent regions, years or treatment assignments. The broad campaign goal of regional replication remains open.

The result tests no climate-change trend, weather return period, flower timing, species distribution or biodiversity loss. The floral response table is not used. High air VPD can reduce stomatal conductance, so more atmospheric joint exposure need not mean more ozone enters leaves. Grossiord and colleagues (2020), DOI 10.1111/nph.16485, review plant responses to VPD. We fit no conductance or injury model. Fixed dome differences, shared ambient weather, watering, unknown filled values and subhour changes remain unresolved. Month truncation can shorten runs at the boundaries. No statistical absence of a duration effect is claimed.

A next study should apply the monotone bounds to field records from separate regions and years, with calibration logs and explicit missing/filled-hour flags. A plant test needs replicated treatment units, soil water and conductance observations. It should specify biologically relevant durations before testing outcomes. Different statistics need separate monotonicity checks.

## Reproduce and inspect

The package contains original code, text, a figure, aggregate statistics and provenance. External raw data and record-level derivatives remain outside it. The exact source URL, shared path, version and used-file hashes are in files/provenance.json. External terms and attribution are in files/EXTERNAL_DATA_NOTICE.md.

Use Python 3.12 with numpy, pandas and matplotlib; run versions are recorded in provenance.json. From an extracted publication:

```sh
python files/retrieve.py /absolute/path/to/new_external_scratch
python files/analyze.py --archive /absolute/path/to/new_external_scratch/data.zip --out /absolute/path/to/new_analysis
python files/validate.py /absolute/path/to/new_external_scratch/data.zip /absolute/path/to/new_analysis
```

On this machine, skip retrieval and use `/mnt/dell-data/shared_datasets/ukceh-wildflower-ozone-warming-2021-a33d5ee3/data.zip` in place. Always write regenerated output outside the signed package. Compare duration.csv and contrasts.csv exactly; figures and local path fields can differ by environment. The independent validator uses scalar math and CSV parsing. All 4,860 source endpoint checks passed. Exhaustive enumeration of 2,187 seven-hour indicator envelopes confirmed exact duration endpoints. Full-grid, finite-value, physical-range and bound-inclusion checks passed. These checks validate computation, not sensor assumptions.

Job: sci-1107-dell-climate-pollution-biodiversity-f2e00eb88e8a. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol with high reasoning effort. Analysis date: 2026-11-11. The signing key is a campaign-machine identity, not a personal authorship claim.
