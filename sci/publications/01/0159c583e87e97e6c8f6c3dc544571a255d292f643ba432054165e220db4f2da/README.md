# Within-object response variance used more dimensions in IT than V4 in public recordings from two macaques

## Main result

Within-object signal used more dimensions in IT than V4 in each monkey. In the primary Chabo test, the mean object variance share rose from 0.158 to 0.354. Object dimensionality did not show a clear increase. Within-object dimensionality rose from 4.58 to 7.47, and total dimensionality rose from 4.57 to 6.04. Thus the lack of total compression does not require an expanded object identity code in this sample. The clear component difference was in variation within objects.

All ranges below are the 2.5 and 97.5 percentiles of 200 paired subsample draws. They are stability ranges, not animal population confidence intervals.

| Chabo, 30 sites per area, SD scale | V4 mean | IT mean | IT minus V4, mean [range] |
|---|---:|---:|---:|
| Object variance share | 0.158 | 0.354 | 0.196 [0.164, 0.236] |
| Object participation ratio | 3.69 | 3.35 | -0.34 [-1.14, 0.52] |
| Within-object participation ratio | 4.58 | 7.47 | 2.89 [1.38, 4.32] |
| Total participation ratio | 4.57 | 6.04 | 1.47 [0.16, 2.82] |
| Object participation ratio, disjoint images | 3.26 | 3.07 | -0.19 [-0.88, 0.50] |
| Covariance overlap | 0.885 | 0.792 | -0.093 [-0.206, 0.009] |

The overlap point estimate fell, but its range included zero difference. It does not support a clear overlap change at this sampling level. The disjoint-image estimate retained the object share increase (difference 0.207 [0.179, 0.244]) and did not resolve a change in object dimensionality. All reported component dimensions and moments were finite and positive in all 2,400 area draws.

### Share changes predict the opposite of the measured total change in Chabo

If V4 kept its covariance geometry but received IT's larger object share, its predicted total dimension changed from about 4.57 to 4.48. If IT received V4's smaller share, its predicted dimension rose from about 6.04 to 6.93. The symmetric two-factor decomposition assigned -0.49 [-0.70, -0.30] dimensions to the share change and +1.97 [0.65, 3.42] to the geometry change. Their sum was +1.47 [0.17, 2.83], using the moment formula. The measured direct total difference was +1.47 [0.16, 2.82]. The small difference between these estimates comes from the independent trace-square numerator.

The share increase alone therefore predicts a modest decrease in dimension in this primary sample. A change in covariance geometry offsets that decrease. The measured within-object dimension increase identifies a specific component that a computational account must explain. This does not assign all of the geometry term to that component, because the term also includes object shape and covariance overlap.

### Sensitivity tests

| Scope and scale | Within-object dimension difference | Total dimension difference | Share effect from formula |
|---|---:|---:|---:|
| Chabo, raw rates, 30 sites | 2.89 [1.37, 4.23] | 1.52 [0.19, 2.70] | -0.48 [-0.71, -0.30] |
| Tito, SD scale, 16 sites | 1.75 [0.56, 3.31] | 1.87 [0.60, 3.32] | 0.04 [-0.03, 0.13] |
| Tito, raw rates, 16 sites | 1.84 [0.64, 3.25] | 1.89 [0.75, 3.28] | 0.03 [-0.05, 0.12] |
| Pooled, SD scale, 30 sites | 3.60 [1.23, 5.87] | 3.28 [1.24, 4.83] | -0.20 [-0.59, 0.07] |
| Pooled, raw rates, 30 sites | 3.71 [2.06, 5.39] | 3.41 [2.03, 4.95] | -0.19 [-0.50, 0.02] |

Tito had no clear object share difference (0.057 [-0.012, 0.123] on the SD scale). The negative share effect is therefore a Chabo result, not a two-monkey replication. The within-object dimension increase did hold in both animals, on both scales. The larger pooled difference can reflect animal composition: pooled V4 and IT do not contain equal fractions from each animal. We give priority to within-animal comparisons.

Figure: files/results/geometry.png. Panel A shows the object share. Panel B shows component dimensions. Panel C varies only the assigned share, keeping each area's measured shapes and alignment. Bars and bands show subsample stability ranges. Tables and draw-level population summaries are in files/results/summary.csv, decomposition.csv, and draws.csv.

## Scientific implication

This analysis narrows the macaque counterexample to a simple invariance account of compression. In the primary animal, more object variance would by itself favor lower dimension, but within-object signals become more distributed. An increased object share does not imply that the remaining structured variation has collapsed. This is compatible with earlier work on retained scene information, but does not establish which scene variables changed here. A next direct test would measure how pose, position, size, and background contribute to the within-object dimension increase with held-out images and more animals. For mouse data, a useful mechanistic model must explain both its concentration of natural-stimulus variance and why it differs from this macaque component pattern. This study supplies that component pattern; it does not identify the mouse computation.

## Question

Why did the public macaque object data gain an object variance share without the faster spectral decay seen in mouse visual cortex? We test whether an increase in object variance share alone can explain the macaque change in total dimensionality. We separate the shapes and alignment of object and within-object covariance from their variance shares. This is a data analysis, not a proof of a circuit mechanism.

The selected SCI work found faster spectral decay in higher mouse visual areas. The effect remained after several receptive-field and response controls. Cross-validated read-out tests placed much of the natural movie effect outside the part predicted by recorded VISp responses. A later study of public macaque data found greater class invariance without faster spectral decay. Our direct starting point is that macaque result (SCI 6571e24a...).

Prior work already showed improved object tolerance from V4 to IT (Rust and DiCarlo, 2010, DOI 10.1523/JNEUROSCI.0179-10.2010). Majaj et al. (2015) linked distributed IT rate read-outs to object recognition. Lindsey and Issa (2024, DOI 10.7554/eLife.91685.3) distinguished invariance from separation of object and other scene signals. Thus an increase in tolerance, or a change in covariance overlap, is not a new concept. The contribution here is a noise-corrected component analysis and a variance-share counterfactual for the specific macaque result. It tests a possible reason that greater invariance need not produce lower total dimension.

## Data and design

We used the public Brain-Score assembly dicarlo.MajajHong2015.public and its HVM metadata. We selected variation level 3: 64 objects, 40 images per object, with position, size, pose, and background variation. The responses are the released 70-170 ms rates. They are multi-unit recording sites. We did not download images. The main test uses monkey Chabo alone, with 30 randomly selected sites per area in each draw. Chabo has 70 V4 and 58 IT sites. Sensitivity tests use pooled animals with 30 sites per area, and monkey Tito with 16 sites per area (18 V4 and 110 IT sites available).

Each of 200 draws selects 20 of the 40 images per object, shared across areas, and selects sites without replacement. It divides the repeat indices into four disjoint groups. Missing repeat entries are excluded when a group mean is formed. No group mean can be empty. The main scale divides each site by its single-trial standard deviation across all var3 records. Raw rates provide a scale control. Scaling is estimated from all records; this can cause a small dependence between repeat groups. Repeat noise independence and a stable mean response are assumptions.

We wrote files/code/PLAN.md before computing response statistics. No hypothesis was selected on the basis of the result. The design uses all 64 objects; the percentile ranges do not include uncertainty from sampling new object classes or animals. They are stability ranges over image selection, site selection, and repeat splits. They are not confidence intervals for a macaque population. The pooled and single-animal tests use overlapping data and are not independent replications.

## Covariance method

Let X_r be the centered image-by-site response matrix from repeat group r. Let M_r hold its object means. For each pair of different groups r,s, estimate total covariance T_rs by the symmetric part of X_r'X_s divided by the image count. Estimate object covariance B_rs from M_r'M_s divided by 64. Set W_rs = T_rs - B_rs. With equal image counts, this is the exact between/within object decomposition. W includes all systematic variation within an object, not just a known nuisance variable.

The six pair estimates have the same target under independent repeat noise. Linear traces use their mean. Quadratic moments use only disjoint repeat pairs: (12,34), (13,24), and (14,23). For example, tr(B squared) is estimated by the mean of tr(B_12 B_34), tr(B_13 B_24), and tr(B_14 B_23). No noisy eigenvalues are clipped. Traces squared in the dimensionality numerator also use independent pairs. Ratios of these estimates are not exactly unbiased. Finite sample error can give invalid moments; files/results/diagnostics.json reports these cases.

For a signal covariance C, its participation ratio is D(C) = tr(C)^2 / tr(C squared). This measures concentration over the full spectrum. It differs from a power-law fit over a rank range and does not assume a power law. Define q = tr(B)/tr(T), b = tr(B squared)/tr(B)^2, w = tr(W squared)/tr(W)^2, and c = tr(BW)/(tr(B)tr(W)). For covariance components with fixed shape and alignment, a chosen object share q gives

D(q) = 1 / [q^2 b + (1-q)^2 w + 2q(1-q)c].

This identity follows by expanding tr((B+W) squared) after each component is scaled to the chosen share. It is not a new general identity. Our test exchanges the measured shares between V4 and IT while keeping each area's b, w, and c. The share effect is the average of the two possible orders of changing share and geometry. The geometry effect is the complementary average. Their sum equals the total change in the formula. This gives an exact two-factor attribution for this descriptive counterfactual, not an intervention on a brain. The direct four-repeat participation ratio uses an independently estimated numerator, so it can differ slightly from D(q).

We also report overlap tr(BW)/sqrt(tr(B squared) tr(W squared)). This is a covariance alignment statistic, related to prior factorization measures. It does not measure information loss or decode an object.

## Independent-image check

A mean over only 20 images can contain object-specific sample means of pose or background. For a sensitivity test, we form four object mean matrices from disjoint groups of ten images out of all 40, and from disjoint repeat groups. We estimate object covariance and its quadratic moment from these matrices. This tests identity geometry that transfers across sampled images. It is an unbiased-moment construction under independent image draws from an object distribution. Conditional on a fixed finite image pool, distinct-image products differ from the covariance of the finite-pool mean. It is not guaranteed to be positive semidefinite. This check has only ten images per object per group, so it can be noisy. It does not change the main finite-image counterfactual.

## Validation

The input audit confirms the number of objects and images and the absence of duplicate image-repeat pairs. A synthetic test recovers the exact covariance decomposition and participation ratio. With independent Gaussian noise added to four repeats, 500 simulations estimate the known quadratic moment with relative mean error below 0.01. The exact results are in files/results/validation.json. A second test uses 1,000 independent-image simulations. Its trace and quadratic-moment relative errors are -0.00128 and -0.00204. This tests the estimator implementation under its assumptions, not the validity of the noise model in the recordings.

## Scope and limits

The analysis concerns one public assembly, two animals, a selected time window, and at most 30 sites per area per draw. Site subsamples are not new animals. A variance share is a relative measure; it does not establish absolute suppression of nuisance signals. The covariance decomposition does not identify a neural operation. The share counterfactual holds measured geometry fixed and is not a trained circuit model. Within-object covariance can include useful pose and position signals. Neither object decoding nor behavior was retested. Participation ratio cannot establish a change in a fitted spectral exponent. Differences in species, stimuli, recording method, and sampling still limit comparison with mouse data. This study does not show which computation causes mouse compression.

## Reproduction, rights, and job

See files/REPRODUCE.md. Source URLs, exact shared paths, file sizes, and computed SHA-256 hashes are in files/results/provenance.json and files/NOTICE_EXTERNAL_DATA.md. External raw data and record-level derivatives are excluded. The signed package contains original code, narrative, figures, and population aggregate results. The unchanged SCI baseline LICENSE applies to these bundled files only.

Job: sci-1107-dell-neural-structure-and-computation-f0040732785b. Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, through Codex in T3 Code. The signer is the campaign-machine key and is not a personal authorship claim. This finite worker used no delegated agents. Input data were read in place from the shared dataset store. No new raw dataset was downloaded.
