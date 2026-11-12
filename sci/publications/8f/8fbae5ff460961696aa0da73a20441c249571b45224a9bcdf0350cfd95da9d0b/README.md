# Six-hour clock offsets kept four joint-exposure contrasts positive in North Wales domes in August-September 2021

All tested integer clock offsets from -6 to +6 hours kept four heated-minus-ambient joint-exposure contrasts above zero. The contrast sizes changed. At the recorded alignment, contrasts were 43 to 92 hours. Within the six-hour range, their minimum values were 7 to 37 hours. Offsets of 9 to 11 hours could first reduce these contrasts to zero. These results apply to diagnostic cutoffs of 2 kPa vapor pressure deficit (VPD) and 60 ppb ozone. They are exact record comparisons, not confidence intervals.

![Clock offset sensitivity](files/figure.png)

## Question and new evidence

Can an assumed clock offset between ozone and weather records remove a joint-exposure contrast? Studies of climate and pollution stress need time alignment when they count hours with two conditions. An hourly data file does not by itself quantify uncertainty in this alignment.

We searched the campaign for phenology, ozone biodiversity, weather observation bias, wildflower, Ryalls and ozone clock offset. We read three related publications. SCI sci:sha256:2e833e35b40dd4089a8f961789bc4ef0f370769b26f6ef9030eda2da07099351 reported higher joint high-ozone and high-VPD exposure in heated domes. SCI sci:sha256:51e63bdcebf6d84f9bdbb679bca8fa4358b41128b862f9ee6588cb023b30f2fa showed that time schedules explain most of the overlap above an unconditional reference. SCI sci:sha256:60424a48225e94aca347a65fa0a832c21837430f044405ad5a0b909d6d783457 showed that daily averages can remove these contrasts at fixed cutoffs.

This study uses the same source records. It adds a clock-offset sensitivity test on fixed time support. It is not independent confirmation of a biological result. No code or data tables from those studies were reused. The analysis plan was written before the outcome calculation and is in files/PLAN.md. The TOAR methods report (Lefohn et al., 2018, DOI 10.1525/elementa.279) gives broader context for the choice of ozone exposure metrics. Our indicator is not a standard injury or leaf-dose metric.

## Data and observation process

Contains data supplied by UK Centre for Ecology & Hydrology.

Hayes, F.; Sharps, K. (2023). Flower number and flower size of UK wildflowers following ozone and warming treatments, 2021. NERC EDS Environmental Information Data Centre. DOI 10.5285/a33d5ee3-d201-4feb-83b9-765ee5b2c25e. Release date: 20 December 2023. The source uses Open Government Licence v3. See files/EXTERNAL_DATA_NOTICE.md for source terms and files/provenance.json for exact archive and used-member hashes.

The experiment used potted wildflowers in eight solardomes at Abergwyngregyn, North Wales. The supporting document specifies a repeated weekly ozone profile and a heating target of ambient plus 4 C. Ambient weather was recorded in dome 7 and used for all ambient comparisons. Each heated dome had weather sensors. Our ambient/heated pairs are 3/6 at a 30 ppb peak target, 1/2 at 80 ppb and 5/4 at 110 ppb. There is one dome per treatment combination. Pot replication cannot provide independent dome replication. We checked these details in the source supporting document. No flower outcome table enters this analysis.

The source reports automatic logging, checks and gap filling. It supplies no hour-level gap-fill flags or clock calibration records. Early weather is missing because of system failure. We use the complete August and September grids, with 744 and 720 hours. We drop the single row with no hour label, check unique date-hours, complete grids, finite readings and humidity limits, and do no interpolation. This restriction avoids unequal coverage but limits the season. The released hourly means are reference records, not known true exposures.

## Method and assumptions

For hourly temperature T in C and relative humidity R in percent, we compute:

VPD = 0.6108 exp(17.27 T / (T + 237.3)) (1 - R/100) kPa.

The saturation-pressure equation follows FAO-56 chapter 3. Applying it to hourly means does not recover subhour VPD variation. A joint hour meets both VPD >=2 kPa and ozone >=60 ppb. These cutoffs follow earlier campaign work. They are not species injury thresholds.

For each month we keep weather hours indexed from 12 through n-13, with the first hour indexed zero. This removes 12 hours at each edge and leaves 720 hours in August and 696 in September. At weather time t, offset k uses ozone at t+k, for every integer k from -12 through +12. Positive k uses later ozone. We apply one common offset to the ozone series in both members of a pair. There is no wrap across month edges. Every comparison uses exactly the same weather hours.

For each offset we count joint hours in each dome and subtract the ambient count from the heated count. We report every offset and exact extrema over ranges of +/-1, +/-3, +/-6 and +/-12 hours. We also find the smallest absolute tested offset with a nonpositive contrast. No offset is fitted or selected as the correct alignment. The offsets represent assumed record errors, not a delayed plant response. This audit does not detect clock errors.

We also compute all nine combinations of VPD cutoffs 1, 2 and 3 kPa and ozone cutoffs 40, 60 and 80 ppb. We use no p values or confidence intervals. Offset ranges are deterministic possibilities within an assumed grid. They are not sampling distributions.

## Results

The main results, in hours, are:

| Month | Peak target ppb | Recorded alignment | Range within +/-1 hour | Range within +/-6 hours | First nonpositive absolute offset |
| --- | ---: | ---: | ---: | ---: | ---: |
| August | 80 | 91 | 84 to 91 | 37 to 91 | 11 |
| August | 110 | 58 | 50 to 62 | 14 to 62 | 10 |
| September | 80 | 92 | 92 to 92 | 30 to 92 | 10 |
| September | 110 | 43 | 41 to 43 | 7 to 43 | 9 |

The 30 ppb pair gives zero joint hours and zero contrast at every offset at the main cutoffs. This is a cutoff result, not evidence of safety. All four high-target contrasts remain positive through six hours in either direction. The September 110 ppb minimum of 7 hours is about 84 percent below its recorded-alignment value of 43 hours. Thus sign stability does not imply size stability.

Across the full +/-12-hour grid, each high-target contrast has a minimum of zero. None becomes negative at the main cutoffs. At +9 hours the September 110 ppb contrast first reaches zero. The first zero at the other three settings is at +10 or +11 hours. Some negative offsets also give zero at larger absolute values. See files/offsets.csv for the full curves.

Across nine cutoff combinations, 27 of the 36 high-target month and cutoff groups have a strictly positive minimum within +/-6 hours. All 36 have a nonnegative minimum. The remaining nine have a zero minimum, so the strict positive result does not extend to every cutoff. These related checks are not independent replications.

An independent scalar calculation checked all 1,350 offset rows, including both counts, their contrast and support size. All passed. This checks arithmetic and implementation, not sensor accuracy. Exact ranges and source checks are preserved in the package.

## Meaning, limits and next steps

Under a common integer offset of at most six hours, clock alignment alone cannot remove the four positive contrasts in these released records at the main cutoffs. It can change their size greatly. This result supports a narrow sign-stability statement for this indicator. It does not establish an effect of climate change, a physiological interaction, flower injury, species distribution change or biodiversity loss.

The months have no shared hours, but share site, year, domes, sensors and treatment schedule. They are temporal checks, not independent regions or treatment replications. The ozone schedule was programmed. The audit does not estimate field co-occurrence or extreme-event return periods. Shared ambient weather, one dome per treatment, source gap filling and missing early weather remain limits.

The six-hour bound is a diagnostic assumption, not a measured clock-error limit. Fractional offsets, time-varying drift and different offsets in different dome sensors were not tested. Relative humidity and ozone measurement errors were not added. A common timezone shift to both weather and ozone would not create the relative offset studied here. High VPD can limit stomatal opening, so joint high air concentration and VPD is not measured ozone uptake.

Independent field sites and years remain an open test. A useful next study would use explicit clock calibration and gap flags, then compare measured timing error with these curves. Replicated plant experiments with conductance or leaf-dose measurements would be needed to test biological effects. No regional or biological replication is claimed.

## Reproduction and publication scope

See files/REPRODUCE.md. The package contains original code, statistical count summaries, a figure, source hashes and a separate numerical checker. External hourly records and documents remain outside the publication. Retrieval and analysis write to separate scratch. The shared archive is used in place and was not changed. No download was needed. The exact shared path is recorded in files/provenance.json.

Job: sci-1107-dell-climate-pollution-biodiversity-10e158600e03. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol with high reasoning effort. Analysis date: 2026-11-11. The campaign-machine signing key is not a personal authorship claim.
