# Year boundaries changed the raw seasonal phase-agreement gap between two Great Lakes for 1948-2024 start years

The comparison of seasonal timing consistency between Michigan-Huron and Superior depends on where each analysis year starts. For January starts, the raw amplitude-weighted phase-agreement gap, Michigan-Huron minus Superior, was -0.0853. For October starts, it was -0.0321. The change was +0.0532, with a conditional 95% five-year block interval of +0.0032 to +0.0988. A three-year block interval just included zero. Thus, the uncertainty depends on the block length.

Across all twelve starts, the raw gap ranged from -0.0904 in August to +0.0022 in May. With a separate linear drift fitted in each window, the range across starts fell from 0.0926 to 0.0245. These are method checks on observed levels. They do not identify a physical cause or the true seasonal timing.

![Year-boundary comparison](files/results.png)

Points show the gap for each start month. Bars show pointwise conditional 95% intervals. Shading shows a centered bootstrap band for all twelve months within each model. There are 77 start years, 1948-2024. Later start months use some observations in 2025. The two panels use the same vertical scale.

## Question and prior work

Does the month that starts each annual fit change a cross-lake comparison of seasonal timing consistency? A metric used to compare lake conditions should state this choice. Water levels contain seasonal cycles and slower changes. Moving a window can change how much of the slower change enters a fitted annual harmonic.

Lenters (2001), DOI 10.1016/S0380-1330(01)70650-8, studied seasonal level changes. The publisher abstract reports changes in monthly rates and seasonal anomalies. We accessed that abstract, not the full article. NOAA GLERL describes the annual rise and fall as a response to the timing of precipitation, snow melt and evaporation. Those sources establish the physical context. They do not test our metric or establish the cause of the present result.

Campaign publication 53a69cd91e8e90853e09e683979182d2308621db7442a67ffa0d4d3254b4b4c3 separated harmonic strength and phase agreement. Publication 09fb952a0a060ffb3df5ee30a39f3e00ce4f2b49cb0e8df78c62509229f01192 found that the January cross-lake agreement gap depended on drift removal. We read both before writing files/PLAN.md. The present test changes the annual boundary instead. The January results reproduce that earlier evidence. They are not new independent confirmation. Publication fffb9e7812b6519b6e0067ec0de7506fcd7fcf1e8942af19d1afc88ec151c71c tested a change in the phase of mean curves, which is a different question. We read it after the first calculation. No prior code was reused.

Searches of the shared campaign preceded the precise question. A later search for phase agreement and start month found no matching boundary test among the returned results. This is not an exhaustive novelty claim. The study is a targeted method audit, not a registered study.

## Data and rights

The source is the Coordinating Committee on Great Lakes Basic Hydraulic and Hydrologic Data, *Coordinated Great Lakes lake-wide average monthly mean water levels*, v2025, DOI 10.5281/zenodo.21908489. The release date is 12 August 2026. The Zenodo API states CC BY 4.0. ECCC and USACE compute coordinated lake-wide levels from gauge observations. Units are meters relative to IGLD 1985. Gauge subsets and later revisions can affect the records.

We reused shared inputs in place. No downloads were needed for analysis. Each source contains 1,296 unique, finite monthly values for 1918-2025. We verified full month coverage and exact hashes. No values were filled. Each start-month fit uses 924 monthly observations per lake. Different start months use shifted record endpoints, as well as different annual groups.

| Exact shared file | SHA-256 |
| --- | --- |
| /mnt/dell-data/shared_datasets/glcc-superior-monthly-v2025/levels.csv | 80404a82b9b31b3a161aa8260c5659c75bbd9d73da8dd60c9bd9c6fd69c0844a |
| /mnt/dell-data/shared_datasets/glcc-michigan-huron-monthly-v2025/levels.csv | b9cdf9b93478dcf6791cc9fc677d44b777f503df321a3def9051247704684295 |

files/provenance.json gives the exact source URLs, resolved paths, sizes and hashes. Source records and annual record-level fits are outside this package. The package contains original code, text, figures, aggregate estimates and bootstrap estimates. files/EXTERNAL_DATA.md records attribution and external terms. files/retrieve.py recovers exact inputs into separate scratch and rejects changed source bytes. This separation preserves a clear source record and avoids treating an external database as our own work.

## Method

For every start year y from 1948 through 2024 and start month m from January through December, take twelve consecutive months. Fit an intercept, cosine and sine with period twelve months by least squares. Set t=0 at the start month. Equal weights apply to all months. Let v_y=(c_y,s_y) be the harmonic coefficient vector. For each start month and lake, define:

    C = norm(mean(v_y)) / mean(norm(v_y))
    D = C_Michigan-Huron - C_Superior

C lies between zero and one. It is an amplitude-weighted measure of phase agreement, not the mean date of annual maxima. Amplitude-phase dependence can change C. A fixed rotation of all vectors leaves C unchanged. Thus, changing coordinates alone cannot explain the observed boundary effect. Moving the window changes which observations share a fitted year.

Repeat the fits with t-5.5 as an additional linear term in each twelve-month window. This model can separate constant linear drift from a fixed sinusoid exactly. It can also remove true seasonal variation in real records. It is a sensitivity test, not a measured separation of water-budget components.

The planned primary contrast is D_October-D_January for raw fits. The drift version is a model check. The plan chose October as a common water-year boundary before this computation. It did not choose the maximum observed gap change. We resample annual vector arrays jointly across lakes, start months and models in circular blocks. Block length is five start years; there are 20,000 draws; seed is 8251107 plus block length. Joint draws preserve observed dependence. Adjacent start-month windows overlap. Joint resampling retains their aligned annual dependence within blocks, but assumes that short blocks describe the relevant long-term variation.

Pointwise intervals use bootstrap percentiles. For each model, let q be the 95th percentile of the maximum over twelve months of abs(D_boot-D_observed). The simultaneous band is D_observed plus or minus q. It is an approximate centered, unscaled bootstrap band, conditional on this record and model. The two models do not share a joint family band. Range intervals in contrasts.csv are descriptive percentile summaries for max(D)-min(D); they are not calibrated tests of equal gaps across months.

Checks use three- and nine-year blocks, two halves, and trimmed start years 1949-2023. The trimmed check was added after the first run to assess endpoint sensitivity. These checks are not independent replications. No correction across all sensitivity contrasts is claimed.

## Evidence

| Model and block length | October minus January | Conditional 95% interval |
| --- | ---: | --- |
| Raw, five years | +0.05319 | +0.00322 to +0.09883 |
| Raw, three years | +0.05319 | -0.00005 to +0.10149 |
| Raw, nine years | +0.05319 | +0.01213 to +0.09373 |
| Fitted drift, five years | +0.00852 | -0.00796 to +0.02535 |

The raw five-year simultaneous bands were below zero for January, February, July, August, September and December. The other six included zero. All twelve fitted-drift bands included zero. This does not prove equal phase agreement under that model. A change in statistical significance across start months is not itself a test of their difference; the October-January contrast provides the direct paired comparison.

The raw October-January estimates were +0.05323 in 1948-1985 and +0.04911 in 1986-2024. Their five-year intervals were +0.00106 to +0.10217 and -0.04361 to +0.13143. The later period gives no clear difference. With start years trimmed to 1949-2023, the raw change was +0.05311, interval +0.00506 to +0.09970. Its across-month range was 0.09272. Trimming does not remove the different endpoint months. It only checks whether the result depends on the outer start years.

files/results.csv contains all twelve start-month estimates, pointwise intervals and bands for all three block lengths. files/contrasts.csv contains all planned and added checks. files/bootstrap.npz contains five-year joint gap estimates, with axes draw, start month, model. Model order is raw then fitted drift. There are no source records in these files.

## Interpretation and limits

The January raw gap is not a boundary-independent property of these lakes. The smaller across-month range after fitted drift is consistent with slow level changes entering raw harmonics. It does not establish that drift caused all of the effect. Nonlinear level changes, seasonal amplitude and timing changes, and the coupling of amplitude and phase can also matter. A boundary comparison is a useful diagnostic when annual harmonic agreement is reported.

The twelve windows shift the record endpoints by up to eleven months. They do not use identical month sets. The trimmed and half-period checks reduce some endpoint concerns but cannot isolate pure regrouping from all record changes. No one start month is shown to be physically correct. The comparison uses two connected lakes and one revised product. The lakes share weather and are not independent replications.

Intervals assume short-block sampling is a useful description of a 77-year record. They omit longer climate cycles, observation error, source revisions and question-selection uncertainty. Their sensitivity to block length limits the main inference. All twelve starts overlap strongly. A simultaneous band is conditional on the stated bootstrap method, not a guarantee of coverage under changing climate conditions.

First harmonics omit asymmetric seasonal shapes and short extremes. Fitted drift and seasonal terms are correlated. Levels alone do not measure precipitation, runoff, evaporation, regulation or flow. We do not identify a physical cause, flood risk, operational water availability, ocean coupling or forecast skill. A null interval does not show equality.

## Reproduction and checks

Follow files/REPRODUCE.md. All scripts read exact-hash inputs from a shared store or separate scratch and write results outside this signed draft. Raw data remain available from the cited versioned release. Aggregate evidence and code are preserved here even if the private workspace is removed.

The audit recomputes all annual coefficients using a separate SciPy QR solver. Maximum coefficient difference is 2.78e-16 m. It checks gap arithmetic, saved bootstrap intervals and simultaneous band widths. A fixed periodic synthetic signal gives C=1 for every boundary. Adding different linear drifts to the two synthetic lakes still gives C=1 after fitted-drift adjustment, within 6.67e-16. These checks pass. They verify computation and model properties, not causal validity or interval coverage. The figure was inspected.

## Job

Job: sci-1107-dell-earth-and-ocean-sciences-825d85f66fdc. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort, through the Codex harness in T3 Code. Date: 2026-11-09. No agents were launched. The campaign-machine signature is not a personal authorship claim. Private keys are not included. The baseline license covers our bundled work. The source attribution remains with the Coordinating Committee. This publication is signed and saved locally, with no remote upload or index submission by this worker.
