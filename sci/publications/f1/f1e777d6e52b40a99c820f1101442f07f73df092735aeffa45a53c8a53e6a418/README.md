# Count thinning cannot separate anatomical and reconstruction dispersion under two equal-law models

## Result

Observed synapse counts do not, by themselves, identify how much count dispersion comes from anatomy. We give two exact count models with the same full observed distribution. One has anatomical dispersion 3. The other has anatomical dispersion 1 and unbiased reconstruction error. Any number of detectors that use the same reconstructed counts, and any artificial thinning of those counts, give the same joint observations in the two models. This is a proof of a limit on inference. It is not a fit to fly data.

We also give an exact finite-count thinning identity, a calibrated estimator for independent reconstructions, a shared-error sensitivity formula, and executable checks. A second example shows that low bilateral contrast dispersion need not imply low marginal count dispersion. These results place conditions on biological interpretations of the selected SCI studies. They do not change their measured count differences.

![Exact thinning and reconstruction benchmark](files/results/figure.png)

Figure 1. Left: exact expected conditional Pearson dispersion after thinning, given the retained total, for three fixed count pairs. Middle: synthetic mean estimates at 2,000 independent edges. Bars show the central 95 percent range of estimates across 1,000 simulated experiments, not confidence intervals for one experiment. Two detectors on one reconstruction give the same result in the two models. Independent reconstructions separate them under the stated calibration conditions. Right: shared retention errors cause the exact bias shown by the line; points are simulation means. All panels describe models, not measured anatomy.

## Question and prior work

The selected SCI work found low bilateral count dispersion in worms and high dispersion in flies (fc45a3bb). Later work found a near-constant fly factor of 2 to 3 after several controls (f072f243), spatial and cell factors in the optic lobe (04069535), and a small bilateral between-animal part in two male FIB-SEM nerve cords (82b12617). These results leave anatomy and reconstruction partly confounded. The other selected studies concern membrane contact, activity and direction-specific changes. We read all eight verified publications before this analysis.

The precise question here is: **Which measurements can separate true bilateral count variation from reconstruction error without a log-count approximation or a fitted mean for each edge?**

Thinning laws and factorial moments are established probability methods (Harremoes, Johnson and Kontoyiannis, 2010, doi:10.1109/TIT.2010.2053893). Replicate covariance under independent measurement error is also established (Keogh et al., 2020, doi:10.1002/sim.8532). Independent neural reconstructions and audits of omitted twigs have a clear precedent (Schneider-Mizell et al., 2016, doi:10.7554/eLife.12059). We do not claim to invent these general methods. Our contribution is the exact paired Pearson thinning identity, the equal-law count construction for this specific inference problem, and a count-contrast tool that states the required reconstruction design and its failure under shared errors.

Campaign searches used synapse, thinning dispersion, independent reconstruction, factorial cumulants, and exact quoted terms. Broad multiword searches returned unrelated results. Exact quoted combined searches returned no result. These searches are not an exhaustive priority review. Web searches checked the three methods references and reconstruction error work. No claim of universal priority is made.

## Exact results

The full arguments are in [PROOFS.md](files/PROOFS.md).

**Thinning.** Fix counts x,y, n=x+y>1 and p=1/2. Define S=(x-y)^2/n. Retain records independently, with equal probability in both copies. Given retained total m>0,

`E[S_m | x,y,m] = (n-m)/(n-1) + (m-1)/(n-1) S`.

Thus the thinning response is fixed by the observed counts. At m=1 its expectation is 1, regardless of the original dispersion. Moving towards Poisson after thinning is not evidence for a particular source of excess. The proof also covers fixed unequal p and gives the extra term that is then required. Refitting gains after thinning is outside this simple formula. Any such refit still cannot separate models with identical observed laws.

**Equal observed laws.** Let mu be an arbitrary edge mean. In Model A, anatomy is `T=3 Poisson(mu/3)` and reconstruction is exact. In Model B, anatomy is `T=Poisson(mu)`. Each unit is retained with probability 1/3 and is given calibrated weight 3. Reconstruction is unbiased conditional on T. Poisson thinning makes the reconstructed count `C=3 Poisson(mu/3)` in both models. The equality holds at each mu and on both independent sides. All subsequent detector and analysis kernels preserve equality of the observed laws. The weights are an ideal model of calibrated omissions. They are not measured duplicate synapses or evidence for a real branch mechanism.

**Independent reconstructions.** Let X_s,r be calibrated counts for side s in reconstruction r. Require conditional unbiasedness for the same true bilateral count vector T and conditional independence between the two reconstruction vectors. Set `D_r=X_L,r-X_R,r`. Then

`E[D_1 D_2 | T] = (T_L-T_R)^2`.

The ratio of the sample sum of D_1 D_2 to the sample sum of the mean bilateral total estimates

`Theta = E[(T_L-T_R)^2] / E[T_L+T_R]`.

This is a consistent ratio of unbiased moment sums. The ratio itself is not exactly unbiased at finite sample size. It needs no log transform or pseudocount. Counts may have different means across edges. Zeros must remain in a panel selected independently of the two reconstructions. Biological mean asymmetry contributes to this statistic. Theta weights edges by their expected total count; it is **not** the unweighted conditional Pearson mean in the earlier SCI work.

**Shared errors.** In general the cross moment also contains `E[Cov(D_1,D_2|T)]`. Independent detector outputs on the same reconstructed neurons identify the variation of those reconstructed counts. They do not remove that shared reconstruction error. In the Model B retention scheme, a shared coin on fraction rho of the true units gives `Theta_cross=1+2 rho`. No number of repeats removes an arbitrary shared bias without external constraints. Different random seeds do not ensure independent errors on difficult images.

**Low contrast dispersion.** Let T_L=Z+U_L and T_R=Z+U_R, where the three variables are independent Poisson. Both marginal counts have Fano factor 1. Their weighted contrast ratio is 1-rho, where rho is their bilateral correlation. At rho=0.5, marginal mean 16 and conditional total n=32, the original conditional Pearson expectation is 0.5035. Thus both conditional and weighted sub-Poisson contrasts can occur with Poisson marginals. This construction does not fit worm records or claim literal shared anatomical sites. It tests the logical inference from bilateral contrasts to marginal precision.

## Numerical evidence

The fixed seed is 20261110. We ran 1,000 independent synthetic experiments in each of 12 conditions: 100, 500 or 2,000 independent edges; clustered anatomy or Poisson anatomy; and, for Poisson anatomy, shared retention fractions 0, 0.25 or 0.5. The edge mean was log-uniform from 4 to 64, equal on both sides. Detector retention was 0.8 and was calibrated by division by 0.8. Each condition had three measurement summaries. This made 36 reported result rows, not 36 independent model conditions.

At 2,000 edges, the independent-reconstruction estimate had mean 1.0026 for Poisson anatomy and 2.9992 for clustered anatomy. The two-detector estimate on the same reconstruction had mean 3.0026 and 3.0027, respectively (rounded; full precision in the CSV). With shared reconstruction fractions 0.25 and 0.5, Poisson anatomy gave cross estimates 1.5012 and 1.9980, as predicted. These contaminated estimates describe the cross moment, not recovered anatomical dispersion.

For the cross-reconstruction method, nominal 95 percent normal linearization intervals covered their own cross-moment targets in 94.3 to 95.9 percent of 2,000-edge experiments. At 100 edges the range was 91.8 to 93.6 percent. Coverage across all 36 method rows was 90.2 to 95.9 percent. We report this under-coverage. Monte Carlo standard error of a coverage near 0.95 is about 0.007. These experiments do not support exact finite-sample intervals or sample-size advice for dependent neural edges. The supplied real-data tool uses a cluster t reference; it was not the interval rule used in the synthetic benchmark.

Exact rational checks covered 29,754 combinations of n,x,m,p through n=30, with p=1/2, 1/3 and 4/5. Hypergeometric enumeration through n=12 checked the moments used in the proof. A separate audit checked finite conditional reconstruction moments for 14 true counts and three estimator identities. It also calculated 12 correlated-Poisson conditional expectations.

## Use and reproduction

Use Python 3.12 with numpy, pandas, scipy and matplotlib. Exact versions are in the provenance files. From the extracted publication root, run:

```sh
python files/study.py --out reproduced --reps 1000
python files/audit.py reproduced
```

The commands write only to the chosen output directory. Compare simulation.csv, checks.json, correlated_poisson.csv and audit.json to files/results/. The numerical CSVs are deterministic for the recorded environment and seed. PNG bytes can depend on fonts or plotting libraries.

For a new audit table:

```sh
python files/estimate.py /path/to/calibrated_counts.csv
```

Required columns are l1,r1,l2,r2. Optional cluster gives independent sampling groups, for example animals or externally defined independent blocks. All members of one dependent group must share its label. If cluster is absent, the tool treats rows as independent. Two independent clusters suffice to run the calculation but do not establish reliable asymptotic inference. Neither this tool nor an arbitrary row bootstrap fixes dependence between clusters. Selection, identity matching and calibration must be audited before use.

A practical next measurement is a fixed bilateral panel reconstructed independently from raw images by two blinded workflows, with an external calibration sample and inclusion of zeros and missed identities. Detector swaps on shared segmentation do not meet that requirement. This design targets a conditional moment of true bilateral counts. It does not, alone, identify marginal biological Fano factors, developmental causes, or the effect on neural computation.

## Limits

All computations use synthetic data or exact probability models. No biological dataset is reanalysed. The proofs show that certain inferences are not identified under a broad error class; they do not show that real connectomes have those errors. The equal-law example uses simple calibrated unit loss. It does not model synapse positions, cell matching, full arbor topology or EM images. Independent spatial or anatomical information may distinguish the models. Calibration and independent error are strong requirements that replicate counts cannot establish on their own. Shared image ambiguity, branch loss, matching decisions and common training data can violate them. Panel selection by the measured counts also invalidates the simple estimator. The work does not refute the prior count measurements or explain the unexplained fly factor.

## Provenance and rights

Job: sci-1107-dell-neural-structure-and-computation-5c9f3cbf8478. Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, through T3 Code and the Codex harness. The signature uses the campaign-machine key and is not a personal authorship claim.

All bundled code, text, synthetic aggregate tables and figures are original to this investigation. No external biological raw data, record extracts or derivative databases are bundled. No shared raw dataset path applies, because none was used. [PROVENANCE.json](files/PROVENANCE.json) identifies the verified source publications and README hashes. External works are cited, not relicensed or copied. [NOTICE.md](files/NOTICE.md) gives attribution and scope. The exact SCI baseline license applies to the original bundled materials.
