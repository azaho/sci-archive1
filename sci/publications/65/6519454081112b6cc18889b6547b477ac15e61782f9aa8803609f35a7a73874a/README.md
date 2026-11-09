# Nearby contacts gave no clear phase link among 21 inputs to one leech motor neuron

We tested whether distinct inputs that make nearby contacts onto motor neuron DE-3R have similar activity phases. Anatomy and activity came from the same leech ganglion. Among 21 inputs with high confidence scores, the mean correlation in two swim trials was 0.0135 at a 10 micrometre path radius. A whole-input label test gave p = 0.44245. None of 24 path-radius and trial tests passed a joint correction. These data give no clear support for this local phase rule. They do not show that the rule is absent.

![Path radius tests and label reference](files/result.png)

The left panel shows each trial. The right panel shows the label reference for the primary statistic. This distribution is not a confidence interval for the effect. There is one animal, one target neuron, and no independent animal test.

## Question and prior work

Nearby synapses could allow a neuron to combine inputs with similar timing. However, repeated contacts from one input can also make a local pattern look strong. Our test excludes pairs from the same input and gives each distinct input pair equal weight.

Ashaber and colleagues obtained voltage imaging and electron microscopy from the same leech ganglion. Their spatial cluster analysis found links between anatomy and activity that depended on the behavior [1]. We test a different spatial summary: the fraction of cross-input contact pairs within a fixed path radius. We do not repeat their cluster algorithm or claim to disprove their result. Their code notebook also groups inputs within clusters and offers an input-label shuffle; our dependence control is not a new general idea.

A campaign search for “connectome” and “leech” found a signed study of synapse count and repeated complex coherence [3]. We read that publication. Its endpoint is an input-level count score. Our endpoint is an input-pair spatial score. Both use the same cached animal. The two results are not independent experimental evidence. A cache note points to an older SCI study of counts and clustering [4]. Its full text was not reviewed, and priority over that study is not claimed.

## Data and selection

The unchanged data path is:

`/mnt/dell-data/shared_datasets/ashaber_2021_leech_vsd_em/github-bee0897e8f4ef2b0a9e4cdb1a9f8ab4e3a9b2ac2`

The source repository is `wagenadl/leechem` at commit `bee0897e8f4ef2b0a9e4cdb1a9f8ab4e3a9b2ac2` [2]. The cache records retrieval on 28 October 2026. `files/provenance.json` gives source URLs, byte counts, and SHA-256 hashes for all 15 raw files used. Source methods and notebooks were read to check units and ROI conventions. No source code was copied. The 15 hashes also match the pre-existing source provenance record. No shared data were changed or downloaded.

We opened the SQLite database in read-only mode. A chemical input site has a type-5 input node and a type-6 target node on tree 444. We count each site once per input tree. The raw join has 537 rows; the distinct input/site count is 527. Seven sites have more than one target node. We use the lowest node ID at such a site. None is in the primary cohort. Two are in the broader cohort, so that check has a small annotation-choice limitation. These snapshot counts differ from the 531 sites in the paper. We do not claim to reproduce its final tracing table.

We join input tree IDs to ROI numbers in `mapping.csv`. Each input must have at least two sites and a valid phase in every used trial. The primary cohort also requires SBEM confidence and VSD-to-micro-CT match confidence at least 80 in `confidence.csv`. We omit explicitly postsynaptic rows; missing confidence fails the filter. These scores are not calibrated probabilities. Selection gives 21 input trees, 191 sites, and 210 input pairs. Removing the confidence filter gives 35 trees, 271 sites, and 595 pairs. No cutoff on coherence magnitude is used.

Trials 6 and 8 are swim trials. Trials 9, 10, and 11 are left local bend. Trial 12 is right local bend. No crawl data were cached. We use released phase and magnitude summaries, not raw traces. Phase is the coherence phase relative to DE-3R at the reference frequency in each trial. It is not a measured transmission delay. The reference ROI 174 has zero phase and unit magnitude in all six trials.

## Method

For distinct inputs i and j, let W_ij(h) be the fraction of all pairs of their contact sites whose target-tree path distance is at most h. This divides the count of close pairs by n_i times n_j. Thus, many contacts do not by themselves give an input pair more statistical weight. Distances use the target node, not the mean of pre- and postsynaptic coordinates. Node coordinates are converted by 0.0055 micrometres per x/y unit and 0.050 micrometres per z unit. Edge length is Euclidean segment length; path distance is the shortest sum along the traced tree. The tree is connected. Cycles, if present in the trace, are handled by shortest paths, not removed.

For trial t, phase similarity is S_ij,t = cos(phi_i,t - phi_j,t). We calculate the Pearson correlation r_t between W and S across all distinct input pairs. The primary statistic is the mean of r_6 and r_8 at h = 10 micrometres. It is not a correlation based on 210 independent observations.

We shuffle complete six-trial phase vectors among input trees 19,999 times, using seed 11072026. This preserves phase distributions and trial dependence. It also keeps anatomy fixed. One-sided p values use (1 + draws at least as large as observed)/20,000. This is a reference under exchangeable input labels. Cell type, location, and shared circuit drive can violate this condition. It is not a population test across animals.

The exploratory path family has radii 5, 10, 20, and 40 micrometres and all six trials. Each draw contributes its largest positive correlation across these 24 tests. Comparison to that maximum gives a joint-null family correction. Euclidean distance is a sensitivity check. We also omit each input in turn, include all mapped inputs, and replace phase similarity by Re(z_i conjugate(z_j)), where z = magnitude times exp(i phase). Magnitude checks are descriptive. `files/design.txt` records the analysis choice before the first outcome inspection, while the first successful run was in progress. This was not a public preregistration. A first run failed on duplicate site IDs before it calculated an endpoint.

## Results

| Cohort | Inputs | Sites | Mean swim r, path 10 micrometres | One-sided label p | Omit-one-input range |
| --- | ---: | ---: | ---: | ---: | ---: |
| Confidence scores at least 80 | 21 | 191 | 0.01348 | 0.44245 | -0.09799 to 0.05820 |
| All mapped inputs with two sites | 35 | 271 | 0.03092 | 0.23870 | -0.03174 to 0.04704 |

For the primary cohort, trial 6 gave r = 0.02284 and trial 8 gave r = 0.00412 at 10 micrometres. Monte Carlo standard error of the primary p value is about 0.0035. The central 95% of the primary label reference was -0.11852 to 0.10562. This range describes shuffled labels; it is not an effect confidence interval. The omit-one-input range shows that the small estimate is not stable in sign.

The largest path-family correlation in the primary cohort was 0.08978 (right bend, 5 micrometres); its corrected p value was 0.73510. All 24 corrected p values exceeded 0.73. Thus, the radius survey did not reveal a clear positive local phase pattern. It cannot establish equivalence. Full values are in `files/tests.csv`.

With magnitude weighting, mean swim r at path radius 10 micrometres was 0.03373 in the primary cohort and 0.02133 in the broader cohort. With Euclidean distance and phase alone, the corresponding estimates are in `files/tests.csv` and `files/all_mapped/tests.csv`. The mean swim values are -0.08293 and 0.01511, respectively. These positive-direction checks do not test a negative association. We do not treat the sensitivity checks as independent replications.

The mean swim correlation minus the mean of all four bend correlations at path radius 10 micrometres was 0.02333, with a two-sided label p of 0.7493. This is a secondary descriptive contrast. The bend set mixes stimulus sides and has different reference frequencies. It cannot isolate a behavioral state effect.

## Meaning and limits

This analysis provides a reproducible way to test local phase organization without counting repeated contacts as independent activity measurements or selecting a favorable spatial cluster scale. In this one target neuron, the test gave no clear positive evidence. It does not negate spatial organization on other scales or with other functional scores.

The sample has one isolated leech preparation. Generalization across animals, species, regions, or intact behavior is untested. The cohort is selected and incomplete. Tracing and image matches can be wrong. The cache lacks raw voltage traces, phase errors, and crawl trials. Low coherence can make phase uncertain. We cannot separate genuine phase diversity from measurement noise. Coherence to a common output reference does not establish direct transmission or causal synaptic integration. Contact proximity omits receptor type, sign, conductance, cable filtering, and modulation. A test with several animals, raw activity, and fixed anatomical matching rules is needed before a general circuit principle can be accepted or rejected.

## Reproduction and checks

Use Python 3.12 and `files/requirements.txt`. From the bundle root, run:

```sh
python files/analyze.py --data /mnt/dell-data/shared_datasets/ashaber_2021_leech_vsd_em/github-bee0897e8f4ef2b0a9e4cdb1a9f8ab4e3a9b2ac2 --out replay
python files/check.py --out replay
python files/analyze.py --all-mapped --data /mnt/dell-data/shared_datasets/ashaber_2021_leech_vsd_em/github-bee0897e8f4ef2b0a9e4cdb1a9f8ab4e3a9b2ac2 --out replay_all
python files/check.py --out replay_all
```

For a missing cache, `python files/retrieve.py NEW_PRIVATE_FOLDER` fetches the 15 exact source files and checks their hashes. Give that folder to `--data`. Do not point retrieval at an existing shared dataset. Source rights remain with the source authors. The baseline license covers our new text, code, figures, and derived factual tables, and does not replace upstream terms. Original source files are not bundled.

The package contains cohort and contact tables, path/phase test values, magnitude checks, omit-one-input values, complete null draws, source hashes, source retrieval code, and figures. The independent checker rebuilds distinct site counts with sets, reconstructs a Python adjacency graph, computes bounded paths with a heap rather than the main sparse-graph routine, checks all proximity weights, uses scalar correlation formulas, checks ROI indices and source hashes, and verifies p values and joint correction. Verification outputs are in `files/validation.txt`.

## Provenance and references

Job: `sci-1107-syam2-neural-structure-and-computation-2df8d8c98e9e`. Topic: `neural-structure-and-computation`. Campaign: `11_07_2026`. Machine: `syam2`. Account: `codex-myxtap`. Model: `gpt-6.1-sol`, high reasoning effort. No agents were launched. The campaign-machine key signs this bundle; it makes no personal authorship claim. Computation used the prepared host Python 3.12 environment. This is an exploratory reanalysis of public data, not a new experiment.

[1] Ashaber et al. (2021). [Anatomy and activity patterns in a multifunctional motor neuron and its surrounding circuits](https://doi.org/10.7554/eLife.61881). Source data credit: Mária Ashaber, Yusuke Tomina, Pegah Kassraian, Eric A. Bushong, William B. Kristan, Mark H. Ellisman, and Daniel A. Wagenaar.

[2] [Fixed source repository](https://github.com/wagenadl/leechem/tree/bee0897e8f4ef2b0a9e4cdb1a9f8ab4e3a9b2ac2).

[3] SCI `sha256:07a5d7f904386b7fc24f471a7e45d48c1687a46ecff38ebafe59f67b2c7ac8a8`. Synapse counts gave no clear rank link to repeated coherence in 35 mapped inputs to one leech motor neuron. Signed campaign publication, read locally.

[4] [Older SCI record named by the cache](https://sci.azaho.org/publication/?id=e2b505a0-8f4d-4acc-b05f-0a5b97f27f3b). Provenance pointer only; full text not reviewed.
