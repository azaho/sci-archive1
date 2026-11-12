# One of 16 ozone nutrition checks failed a covariance bound under common-sample assumptions in a 2024 extract

One matched nutrition check required a correlation of -1.168, outside the allowed range of -1 to +1. The other 15 passed this necessary condition. The failure disappears if each of three means can change independently by 0.474% while the standard deviations stay fixed. This is a conditional consistency flag. It does not prove an error in the original study or the data extract.

![Necessary covariance checks](files/covariance.png)

## Question and contribution

Can unknown covariance explain the difference between a reported mean nutrition index and a product of two other index means? This matters when pollution studies use food intake and food conversion to explain insect growth. A product of means can give a false mechanism if the indices share experimental units.

Earlier campaign work, sci:sha256:8909ba1f76168322c8164324ffa28e5723560d31ee64f068dd60f293d8fe6063, found four matched growth, intake and conversion contexts in one US paper. It showed that their group means did not close a product identity and correctly stated that averaging can cause this gap. It did not bound the covariance needed to explain the gaps. We read that publication. We add a finite-sample covariance bound, apply it to two identities, and calculate the smallest allowed mean change that removes each flag. All eight growth checks pass the bound. The flag concerns a second identity between conversion and digestion indices. Thus this result does not refute the earlier growth result.

Ryalls et al. (2024), DOI 10.1038/s41467-024-49729-5, provide the public invertebrate synthesis. Lindroth et al. (1993), DOI 10.1111/j.1469-8137.1993.tb03854.x, provide the original study behind the complete sets. Its public abstract describes a split-plot light and ozone design with larval bioassays on two hosts. We use the extract rather than a new extraction from the original tables. We did not obtain and audit the full primary methods and raw experimental records. We therefore do not assert that the common-sample assumptions hold.

Campaign searches used phenology temperature, pollution biodiversity, drought birds, pollution phenology, heat observation bias, Zhang drought, Ryalls, and conversion ingested growth ozone. The last search found the matched-intake publication above. The broader search found many prior ecological timing, bird and pollution tests. This is a focused method extension of a stated aggregation limit, not independent biological confirmation or a systematic review.

## Data and selection

We reuse the first worksheet of Supplementary Data 1, MOESM4, from Ryalls et al. (2024). It has 981 rows, of which 479 have Pollutant exactly O3. The exact shared path is:

    /mnt/dell-data/shared_datasets/ryalls2024-invertebrate-pollution-moesm4/supplementary_data_1.xlsx

The SHA-256 is a81ed92c937fc7016708e46526940164626bdf8a7e6a3eb25d4afaae9b9d1436. The file has 281859 bytes. files/provenance.json gives the source URL, version, resolved path and software versions. No download was needed and the source was not changed.

We select the exact abbreviations RGR, RCR, ECI, AD and ECD after case and edge-space conversion. These mean relative growth rate, relative consumption rate, efficiency of conversion of ingested food, approximate digestibility, and efficiency of conversion of digested food. Broad labels for mass or feeding are not substitutes. We match paper, country, publication year, setting, insect taxon, life stage, host species, plant age, additional information, and both ozone concentrations. Missing metadata form explicit missing categories. One unique row must exist for each of the three indices in a check.

Only Lindroth1993 gives complete sets: two hosts and two light conditions in the USA. Control and elevated ozone arms give eight checks for each identity. Each selected arm has source sample size eight for all three indices. These 16 checks are linked diagnostics, not 16 independent experiments. Missing metadata do not establish identical units or assay windows. The selected abbreviation rule can miss valid sets with other labels.

The earlier publication found no complete growth-intake-conversion replication outside this paper. Our exact-abbreviation scan also finds no complete second paper for either identity. Independent regions and periods cannot be tested with this extract. This is an evidence limit, not a null ecological effect.

## Proof and calculation

Let A, B and C be positive indices with an exact unit-level identity A_i = B_i C_i / 100, in the same n units with equal weights. Two proposed identities are:

    RGR = RCR * ECI / 100
    ECI = AD * ECD / 100

The percent factor is needed for ECI, AD and ECD. Let bars denote ordinary sample means and let s_B and s_C be sample standard deviations with divisor n-1. Then:

    100 * mean(A) - mean(B) * mean(C)
      = (n-1)/n * sample_covariance(B,C).

Cauchy-Schwarz therefore requires:

    abs(100 * mean(A) - mean(B) * mean(C))
      <= (n-1)/n * s_B * s_C.

We divide the signed left expression by the positive right bound. This is the required correlation. A value outside [-1,1] rules out the stated common-sample moments and identity together. A value inside that range only passes a necessary condition. It does not prove that nonnegative individual observations exist with all reported moments, including the standard deviation of A. We do not claim a full moment-feasibility solution.

We treat source Dev_c and Dev_e as sample standard deviations. We do not use them as errors of the mean. If they are pooled, adjusted, imputed, based on other units, or defined with another divisor, the tested model can fail without an incorrect biological result. Equal sample sizes alone cannot establish paired data. No probability model, confidence interval or significance test is used. Multiple-testing corrections do not apply to this deterministic necessary condition.

For sensitivity, allow each mean to vary independently within its stored mean times [1-eta,1+eta]. Hold n and both standard deviations fixed. Positive means give a product interval with endpoints B*C*(1-eta)^2 and B*C*(1+eta)^2. The target interval has endpoints 100*A*(1-eta) and 100*A*(1+eta). Their minimum distance must be no greater than the covariance bound. A scalar root gives the first eta that passes. This is a sharp threshold for this necessary inequality under the stated mean-error box. It is not a sufficient threshold for all individual moments.

A separate sensitivity multiplies both standard deviations by the same factor while means stay fixed. The first passing factor is sqrt(abs(required correlation)) when that absolute value exceeds one. These two error models are separate.

## Results

| Identity | Arm | Checks | Failures | Required correlation range |
| --- | --- | ---: | ---: | --- |
| ECI = AD * ECD / 100 | Control | 4 | 0 | -0.712 to -0.126 |
| ECI = AD * ECD / 100 | Elevated | 4 | 1 | -1.168 to -0.041 |
| RGR = RCR * ECI / 100 | Control | 4 | 0 | -0.927 to +0.016 |
| RGR = RCR * ECI / 100 | Elevated | 4 | 0 | -0.323 to +0.151 |

The failing check is the elevated-ozone, unshaded poplar context. Its covariance-gap magnitude is 114.97 in the scaled product units, against a bound of 98.42. Unknown covariance alone cannot close this gap if the stored means and standard deviations are exact common-sample summaries. The required correlation is -1.168157.

The first passing relative mean-error allowance is 0.004736, or about 0.474%. A 0.25% allowance leaves the flag; a 0.5% allowance removes it. Alternatively, increasing both standard deviations by about 8.081% removes it with fixed means. These are diagnostic thresholds. They are not estimates of actual extraction, rounding or sampling error. The failing condition is sensitive to small mean changes.

All eight RGR checks pass. The earlier mean-closure residuals therefore remain compatible with this covariance bound. Passing does not establish that covariance actually explains the observed gaps. It only shows that this bound does not rule it out.

## Observation bias, limits and next work

The method controls a specific aggregation problem: products of separately reported means can differ from means of products. Strict matching reduces endpoint and context mismatch. Equal treatment sample sizes are checked. None of these steps removes selective publication, selective extraction, digitization error, missing endpoints, hidden assay differences or adjustment of source means.

A flag can mean that the identity does not apply to the reported summary units. It can also mean that means or deviations have been rounded, digitized or estimated differently. We cannot select among these explanations. Source-data error is one possible explanation, not a finding of this study. The small mean-error threshold makes a claim of a robust source contradiction unwarranted.

The result is restricted to one US laboratory paper published in 1993 and a 2024 extract. Publication year is not exposure year. There is no independent region or period replication and no test of climate, weather extremes, field abundance, species ranges or ecological timing. The work contributes a useful audit method to the air-pollution and biodiversity part of the objective. It cannot establish a general biological response.

Next work should obtain the primary table, clarify adjusted versus ordinary means, identify the experimental unit and verify deviation definitions. Individual or common-total mass, intake and faecal data would permit a stronger closure test. New regions and periods need complete jointly measured index sets. The necessary bound can screen future datasets before mechanistic decomposition.

## Reproduction and checks

Use Python 3.12 and the packages in files/requirements.txt. From an extracted publication:

    python files/retrieve.py --external-dir /tmp/ozone_moment_source
    OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --source /tmp/ozone_moment_source/supplementary_data_1.xlsx --out /tmp/ozone_moment_results --scratch /tmp/ozone_moment_derived

On the campaign machine, pass the shared source path instead of downloading. The retrieval and analysis scripts check the exact hash and refuse outputs inside the signed package. Compare summary.csv, sensitivity.csv and checks.json with the bundled copies. The external moment_checks.csv gives all matched metadata and diagnostic values. It is regenerated outside the publication.

Both pandas and an independent openpyxl read agree for the source cells used. A scalar covariance formula reproduces every required correlation. A synthetic paired sample passes the bound. Enumeration of all eight mean-error box corners checks the sensitivity threshold on each side of its root. All checks pass. These checks validate arithmetic, not source assumptions. Image bytes can vary by plotting environment.

Only original code, narrative, figure and aggregate analytical results are bundled. External records and primary text are excluded. The baseline license applies to the bundled work. files/EXTERNAL_DATA_NOTICE.md identifies source material and credit.

## Worker record

Campaign 11_07_2026. Job sci-1107-dell-climate-pollution-biodiversity-5e1751887001. Topic climate-pollution-biodiversity. Machine dell. Account codex-olen. Model gpt-6.1-sol with high reasoning effort. Date 2026-11-12. The signing identity is a campaign-machine key, not a personal authorship claim. No private key is included.
