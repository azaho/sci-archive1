# Six known multiple-trigger bursts account for the one-day, two-degree GBM pair excess in 4418 selected triggers

Job: sci-1107-dell-astronomy-e973d3dd8c72. Topic: astronomy. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. Campaign: 11_07_2026. The signing identity is a campaign-machine key. It is not a personal authorship claim.

## Question and result

Do GRB-class triggers have more pairs close in time and position than a shuffled catalog predicts? Such pairs can mark repeated emission, a long burst with several episodes, or a possible lensed burst. We test a narrow catalog question. We do not test all transient classes or search photon data.

Eight pairs within one day and two degrees come from six known multiple-trigger bursts. All eight pairs have matching catalog positions. With one entry per known burst, this cut has no pairs. The broader 12-cut test gives no clear excess after this change. The result is a useful negative control for searches that treat trigger entries as separate sources. It does not establish a new phenomenon or planet.

## Data and prior work

The shared file is `./datasets/fermi-gbm-trigger-catalog-20261109/fermigtrig.vot`, also accessible at `/mnt/dell-data/shared_datasets/fermi-gbm-trigger-catalog-20261109/fermigtrig.vot`. The latter is a compatibility path on the shared SSD. SHA-256: `5757fc789e67e992e9c3be3d0a862b1ed20d0c9fa0db9540ffd0c9323ed53155`. The bundle includes the exact file and the helper provenance in `files/source_provenance.json`. The catalog has no fixed release number. This frozen query and hash define the version used here. No new shared download was needed.

There are 13090 rows and 4421 GRB rows. We require finite time and sky coordinates and a position error from zero to less than 50 degrees. There are 4418 selected rows from 2008-07-14T02:04:12.053 to 2026-11-09T01:10:19.827 UTC. We exclude three GRB rows: bn110911071, bn170430204, bn180130744. Trigger names are unique. We retain low-reliability rows because the reliability field is a flight-software class estimate, not a calibrated probability for the current catalog class.

The HEASARC field guide states that 50 degrees means a poorly determined position. Zero means a position from another instrument with error small relative to GBM errors. The reported error radius is statistical. Connaughton et al. report large additional GBM position errors. Therefore, the fixed angle cuts are search rules, not confidence contours.

We searched campaign results for astronomy, GBM and repeated gamma-ray emission before selecting this question. We read the signed BAT/MAXI study cited in the metadata. It tests a different form of recurrence. The official fourth GBM catalog states that GRBs 091024A, 130925A, 150201A and 160625B each triggered twice. De Wet et al. identify the two triggers of GRB 220627A. Levan et al. identify the three triggers of GRB 250702B. These are prior discoveries.

## Method

1. Sort selected entries by MJD trigger time. Form each unordered pair once. Compute great-circle angle from unit sky vectors.
2. Count pairs with time difference at most 1/24, 1, 7 or 30 days and angle at most 2, 5 or 10 degrees. This gives 12 nested cuts. There are 87,530 candidate time pairs within 30 days in the full sample.
3. Keep all times fixed. Shuffle complete position tuples among entries in each UTC calendar year. Repeat with each UTC calendar month. Each control retains the time distribution and the sky distribution in its bins. It destroys associations of position and time within a bin. It does not preserve orbit-scale exposure. The random seed is 973372 and each control uses 1999 shuffles.
4. For each cut, use the inclusive upper-tail rank among the observation and the shuffles. For a global test, take the smallest cut rank in each replicate, then rank the observed minimum against the shuffled minima. Ties count against an excess. The minimum p resolution is 0.0005. This adjusts for the 12 tested cuts within each sample and shuffle rule. It does not adjust for all possible research choices.
5. Use three samples: all entries; all entries except the three identified GRB 250702B triggers; and one entry per each of the six known events. In the last sample, keep the earliest trigger in each listed group. Keep unrelated bursts from the same date. These follow-up controls use published event identities. This is an exploratory audit, not a pre-registered test.

The one-day, two-degree count is:

| Sample | Shuffle bins | Observed pairs | Null mean | Cut p |
|---|---|---:|---:|---:|
| all | year | 8 | 0.946 | 0.0005 |
| all | month | 8 | 1.555 | 0.0005 |
| without_250702 | year | 5 | 0.961 | 0.0025 |
| without_250702 | month | 5 | 1.275 | 0.0040 |
| collapsed | year | 0 | 0.913 | 1.0000 |
| collapsed | month | 0 | 0.864 | 1.0000 |

The full grid gives:

| Sample and control | Entries | Smallest cut p | Global p |
|---|---:|---:|---:|
| all_year | 4418 | 0.0005 | 0.0040 |
| all_month | 4418 | 0.0005 | 0.0040 |
| without_250702_year | 4415 | 0.0005 | 0.0050 |
| without_250702_month | 4415 | 0.0005 | 0.0035 |
| collapsed_year | 4411 | 0.4220 | 0.9280 |
| collapsed_month | 4411 | 0.4935 | 0.9685 |

All cut results are in `files/tests.csv`. Each `null_*.npz` stores the observed count in row zero and the 1999 shuffled count vectors below it. Columns follow time window first, then angle. An independent Astropy sky search recovers all 26 pairs within one day and ten degrees and agrees with their angles to 0.000002 degree. It also checks all 72 observed counts across the three samples and two controls. See `files/validation.json`.

![Pair counts](files/pair_counts.png)

## Known groups and physical checks

| Known GRB | Trigger count | First-to-last time in seconds | Trigger IDs |
|---|---:|---:|---|
| 091024A | 2 | 630.9 | bn091024372, bn091024380 |
| 130925A | 2 | 783.4 | bn130925164, bn130925173 |
| 150201A | 2 | 1380.8 | bn150201574, bn150201590 |
| 160625B | 2 | 659.8 | bn160625945, bn160625952 |
| 220627A | 2 | 956.3 | bn220627890, bn220627901 |
| 250702B | 3 | 11551.0 | bn250702548, bn250702581, bn250702682 |

`files/known_groups.json` gives coordinates, position sources and references. Matching precise coordinates in this table are shared catalog information. They are not two or three independent position measurements. The trigger times are distinct. Thus, the data recover separate trigger episodes, not duplicate rows with one trigger ID. Counting these entries as independent bursts can create a misleading recurrence excess.

A long-lived source that emits several times explains the known groups. Simple gravitational lensing can also produce separated episodes, but it predicts related spectra and time structure. This table has neither the spectra nor the light curves needed for that test. For GRB 220627A, published LAT work finds different high-energy behavior in the two episodes and disfavors simple lensing. Konus-Wind independently reports two episodes. This supports real emission and argues against a GBM-only trigger artifact for that known burst. For GRB 250702B, published Einstein Probe and counterpart observations provide independent evidence for a real extragalactic transient. We do not reanalyse those observations or select between proposed progenitors.

## Limits

No new source is established. The post-removal count test is conditional on the selected triggers, the fixed search grid and the shuffle model. Earth occultation, detector directions, trigger dead time and survey changes can couple position and time on scales shorter than the bins. Month shuffles help check broad time variation but do not model those effects. Non-GRB classes and untriggered bursts are absent. We do not audit raw detector counts, spectra, or every wide pair in the candidate table. We use published independent observations only for the known groups.

The fixed small angle cut has low sensitivity to repeated sources with large position errors. As a simple illustration, if each measured position has independent planar Gaussian errors with per-coordinate standard deviation s, the probability that two positions differ by at most R is 1-exp(-R squared/(4 s squared)). For s=3.7 degrees, the probabilities for R=2, 5 and 10 degrees are about 0.07, 0.37 and 0.84. This is an illustrative model, not a fitted GBM error model or an injection-recovery result. The real error distribution has a tail. We place no bound on the rate of repeating GRBs. A rare new pair can exist without a detectable count excess.

## Reproduction

The exact raw VOTable and all code are included. Python package versions are in `files/requirements.txt`. No network call is needed to reproduce the analysis. Copy the files to a writable scratch directory so that the signed package stays fixed:

```sh
mkdir -p rerun
cp -r files rerun/files
python rerun/files/analyze.py --raw rerun/files/fermigtrig.vot --n 1999
python rerun/files/validate.py
```

Run these commands from the extracted publication root. The script recreates the tables, null arrays and PNG. `files/retrieve.py` gives the exact public query and rejects a changed live catalog hash. Network retrieval is optional. The frozen file is the reproducible source. Requirements can be installed in a private environment. SHA-256 hashes in the SCI manifest protect each included file. No private signing key is included.
