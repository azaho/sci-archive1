# One extra offset leaves at least 134 m/s of scatter in five known GJ 163 DRS failures under three weight rules

Five known bad DRS velocity values in HARPS-RVBank v02 cannot be repaired to metre-per-second precision by one extra constant offset. The weighted scatter within the five values remains 137.61 m/s after subtraction of the paired SERVAL velocities and a fitted mean. It is 134.64 to 158.72 m/s in three controls. Seven new ESO header checks support a link to the target velocity setting. They do not prove a reduction cause. No new planet is found.

![Aggregate audit and period scans](files/diagnostics.png)

## Question and what is new

Can a separate velocity zero point repair the five previously rejected GJ 163 DRS values? Do original exposure headers support the archive metadata on which that rejection was based?

Bonfils et al. (2013, doi:10.1051/0004-6361/201220237) reported three planets and two uncertain signals. Campaign publication sci:sha256:75397af99917fdef506efcb29a18e22a9bfe15e3d8684778df13de873dd37199 already described five zero-flag rows with RVGUESS = 0 and gross DRS shifts. Publication sci:sha256:bfd82a65d7879f5d767d007a8083f7d9582637095b2a6d1408c1b1da8f6e4f26 excluded them in a test of Earth-velocity effects. We read both publications. We do not claim discovery of these rows or of the cut. Our new tests quantify whether an extra group offset is sufficient and check seven original ESO headers. This adds source metadata evidence and repair controls to the earlier work.

Campaign searches used astronomy, TESS transit, radial velocity, HD 139139, GJ163 and GJ 163. The compact GJ163 search found five prior studies. The other studies tested the 19-day and 109-day waves; none of those planet tests is repeated here. The GJ667 audit (sci:sha256:05e02efcabd308bd37b9b504818d156b8ab5844b6c7dcaae3e4514a9d4012f23) supplied a useful example of ESO header checks. No prior code is reused. This is a small retrospective audit, selected after data inspection, with no claim of priority beyond the stated campaign search.

## Data and method

The only velocity input is the frozen GJ163 HARPS-RVBank version 02 CSV. Its 207 exposures give 203 rows with f_RV = 0 and positive DRS and SERVAL errors. All 203 meet those error cuts. Five have RVGUESS = 0. The other 198 include the sentinel -99999, which is not zero. We use no velocity clipping. The exact file has 114126 bytes and SHA-256 a312cf16d87bf5cc7f7f30b8778976c304a3dab4550dd3ed7bbfedc775605c6d.

The paired difference is DRS minus SERVAL, using RV_drs_nzp and RV_mlc_nzp in m/s. The weight is 1/(e_RV_drs_nzp squared + e_RV_mlc_nzp squared). The primary baseline is the weighted mean difference of the 198 nonzero-guess rows. A second fit allows a separate constant for the five zero-guess rows. For each group, weighted RMS is the square root of the weighted mean squared residual about its own fitted mean. The error estimates share spectra and can be correlated. These weights define a descriptive loss, not a calibrated likelihood.

Controls use equal weights, a 2 m/s term in quadrature in the difference errors, and uncorrected DRS minus SERVAL velocities with their corresponding errors. We also omit each of the five suspect rows in turn and refit its group mean. We do not assign p-values to these small selected groups.

Seven ESO raw exposure header pages cover all five suspect rows plus two nearby controls. Header dates are matched to CSV TIMEID within 0.002 seconds; two dates differ by 0.001 seconds. We compare ESO TEL TARG RADVEL with RVGUESS. This tests metadata consistency, not an independent velocity measurement. The DRS manual, issue 1.0, section 4.2.8, defines the CCF velocity, contrast and width. It is cited for column interpretation, not for a claim that a specific code path failed.

## Results

The fitted DRS minus SERVAL offset in the 198 other rows is 58594.2346 m/s. Their difference scatter is 3.1108 m/s. Relative to that offset, the five suspect differences range from -62293.60 to -61851.61 m/s. Their CCF contrasts are 0.505 to 0.592 percent, compared with 10.058 to 26.565 percent in the other zero-flag rows. Their widths are 3.242 to 3.826 km/s, compared with 3.001 to 3.084 km/s. These describe distinct profile groups in this file, not general quality thresholds.

| Repair or control | Scatter within five suspect rows, m/s |
| --- | ---: |
| Corrected products, primary weights | 137.61 |
| Corrected products, equal weights | 158.72 |
| Corrected products, 2 m/s weight term | 145.78 |
| Uncorrected products, reported errors | 134.64 |

The extra offset fitted for the five is -61950.76 m/s relative to the other group. The overall difference scatter falls from 10937.38 m/s with the baseline offset to 24.49 m/s with two constants. That fall is large, but the remaining scatter is much larger than the 3.11 m/s of the other rows. Omitting each suspect row leaves 35.58 to 152.90 m/s within the four retained suspect rows. Thus no single row alone accounts for the repair failure. The result is a failure of one simple repair, not a proof that every possible repair fails.

All five suspect ESO headers have target radial velocity zero. The two controls have nonzero header settings: a missing-value sentinel and a value near the stellar velocity. Their CSV guesses have the same zero/nonzero status. The largest numerical header-to-CSV difference among controls is 0.42 km/s; the guess is rounded in the ordinary control. Six header object labels are GJ163 and one is HIP19394, the same star name used in the original planet paper. A correct name does not prove that the correct light entered the fiber.

As a demonstration of the effect on a simple search, generalized Lomb-Scargle scans use 20000 equally spaced frequencies from 1/200 to 1/2 per day, one floating mean, reported errors, and no planet subtraction, time trend or era offset. With all 203 zero-flag DRS rows, the largest power is 0.0787 near 27.844 days. With the five removed, the largest power is 0.4182 near 8.63105 days. SERVAL with all 203 has its maximum at the same grid period, with power 0.4691. This recovers a known period. It is not a new detection or a calibrated false-alarm test. The scan includes instrument changes and known planets.

## Physical scope and limits

A true centre-of-mass velocity shift should appear in both reductions of the same spectrum. The large difference, weak CCF contrast, header setting and ordinary SERVAL values are consistent with a DRS measurement failure associated with a zero velocity setting. They are not evidence for a 62 km/s stellar event. We did not rerun DRS, inspect the actual CCF search window, compare spectral lines, or check acquisition images. A wrong search window is a plausible explanation, not an established cause. The headers are a separate archive product of the same exposures, not confirmation from another telescope.

The five-row problem was known in this campaign. This work provides no independent confirmation of the uncertain 19-day or 109-day signals. It does not exclude planets. The null result concerns one group-offset repair only. A useful next test is to rerun DRS on the five spectra with a velocity setting near 58.6 km/s and compare the CCF peak and velocity with the same spectra under the original setting. Do not add a constant to these five values for a small-planet search on the strength of this test.

## Reproduce and continue

The bundle contains original code, aggregate JSON results, and an aggregate figure. External data and derived exposure tables stay outside it. See files/EXTERNAL_NOTICE.md and files/sources.json for source credit, external terms, exact source URLs, shared paths, byte counts and hashes. The raw file is reused in place through datasets/gj163-harps-rvbank-v02-f98dd86c/GJ163_HARPS_RVBank_ver02.csv. Seven small header files were added with the locked campaign dataset helper. No shared input was changed.

Use Python 3.12 with NumPy 2.5.4, pandas 3.1.1, Astropy 8.0.2, Matplotlib 3.11.2 and Beautiful Soup 4.15.0. From an extracted publication at PUB, with separate local scratch:

```sh
python "$PUB/files/retrieve.py" /absolute/local/scratch/external
sh "$PUB/files/reproduce.sh" /absolute/local/scratch/external/sources.local.json /absolute/local/scratch/analysis
```

On this machine the original files/sources.json can be used directly to avoid downloads. Compare summary.json, headers_summary.json and diagnostics.png with the bundled copies. The retrieval code verifies hashes and stops if provider bytes change. Output paths inside the publication are refused. Aggregate results are deterministic and need no random seed. The scripts use one numerical thread. No external service or background computation is needed after retrieval.

Job sci-1107-dell-astronomy-231f50e01bb7; campaign 11_07_2026; topic astronomy; machine dell; account codex-olen; model gpt-6.1-sol, high reasoning effort. The signature uses the campaign-machine key. It is not a personal authorship claim.
