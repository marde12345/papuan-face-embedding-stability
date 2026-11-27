# Data dictionary

- **Content:** every file is an aggregate table, with one row per method, subset, statistic or resampling scheme. No row describes an individual face crop, person, pair or video frame.
- **Format:** values are CSV and use a dot as the decimal separator.
- **Definitions:** they follow the paper's Methodology section (Section III).

## Method codes (column `condition`, and the prefixes in `statistic` and `contrast`)
| Code | Method in the paper |
|---|---|
| `B1` | Unenhanced Baseline |
| `A` | Reconstructed Melanin-Aware Preprocessing (routed: each crop goes either to the Melanin-Aware path or to an unchanged common path) |
| `B3` | Unified Luminance Enhancement |
| `X-Y` | Paired difference, method X minus method Y. For example, `A-B1` is Melanin-Aware minus baseline. |

## Common terms
- **Same-tracklet pair (`positive`):**
  - Two face crops from one automatically linked track, a few seconds apart.
  - Two reviewers judged them to show the same person. This is **not** a verified identity.
  - 359 pairs.
- **Different-face pair (`negative`):**
  - Two faces from different tracks in the same video frame. This is an easy control.
  - 494 pairs.
- **Cosine similarity:** the similarity of two face embeddings (Eq. 2 in the paper).
- **Paired change `d`:** for one same-tracklet pair, its similarity under method X minus its similarity under method Y.
- **`dz`:** mean of `d` divided by the standard deviation of `d`.
- **`share_negative`:** the share of pairs with `d < 0`.
- **AUC:** the probability that a same-tracklet pair scores higher than a different-face pair. Ties count as one half.
- **`dprime` (d′):** (mean positive − mean negative) / √((var positive + var negative)/2).
- **CIs:** 95% percentile bootstrap intervals. `n_boot` resamples were used, with seed `20261118`.
- **Route subsets** (Melanin-Aware reconstruction only):
  - `melanin_melanin`: both crops took the Melanin-Aware path.
  - `common_common`: both crops took the common (unchanged) path.
  - `mixed_route`: one crop took each path.
  - `same_route`: the first two combined.
  - `all_positives`: all 359 pairs.
- **Brightness quartile:** quartile of image luma, computed on the aligned, unprocessed crop. Luma is **image brightness, not skin tone**.

## Files

### `data/embedding_stability/`
| File | Columns (as in the file) | Paper item |
|---|---|---|
| `similarity_separation_summary.csv` | `condition, pair_type, n, mean, median, sd, q25, q75, iqr, p5, p95, min, max, auc, dprime` | Table 2 (point values) |
| `similarity_separation_bootstrap_ci.csv` | `statistic, point_estimate, ci95_low, ci95_high, boot_mean, n_boot, seed`. Statistics: medians, AUC and d′ per method, and their paired differences. | Table 2 (CIs), Table 4 |
| `paired_change_by_route.csv` | `subset, n_pairs, contrast, paired_median_diff, ci95_low, ci95_high, paired_mean_diff, dz, dz_ci95_low, dz_ci95_high, share_negative, median_of_X_minus_median_of_Y` | Table 3 |
| `similarity_descriptives_by_route.csv` | `subset, n_pairs, condition, mean, sd, median, q25, q75, iqr` | Route-subset descriptives (Section IV) |
| `similarity_by_brightness_quartile.csv` | `pair_type, brightness_quartile, luma_range, condition, n, mean, median, sd, iqr, median_minus_B1` | Table 5 |
| `sensitivity_resampling_ci.csv` | `scheme, n_clusters, statistic, point_estimate, ci95_low, ci95_high, ci_width, zero`. `zero` says whether the CI excludes 0. | Table 6 |
| `sensitivity_cluster_sizes.csv` | `scheme, n_clusters, largest_cluster_pairs, median_cluster_pairs, singleton_clusters, clusters_ge10_pairs, max_positives_in_cluster, size_distribution_json`. The last column is a JSON count of clusters by size. | Sensitivity analysis (Section IV) |
| `sensitivity_separation_cluster_ci.csv` | `statistic, point_estimate, ci95_low, ci95_high, n_boot, seed, unit` | Sensitivity of AUC and d′ differences to tracklet-cluster resampling |
| `sensitivity_repeat_exclusion.csv` | `statistic, full_point, full_pair_ci_low, full_pair_ci_high, excl_point, change, excl_pair_ci_low, excl_pair_ci_high, excl_window30_ci_low, excl_window30_ci_high` | Table 6, row "Repeat excluded" |
| `sensitivity_repeat_exclusion_absolute.csv` | `sample, n_pos, n_neg, condition, pos_median, neg_median, auc, dprime`. `sample` is `full` or `s3_excluded` (pairs linked to reviewed repeated footage removed). | Section IV sensitivity text |

**Resampling schemes** (`scheme`):
- `pair_level_primary`: resample pairs.
- `tracklet_linkage_only`: resample clusters of pairs linked by shared tracks.
- `linkage+repeat`: as above, plus links from reviewed repeated footage.
- `window_10s/30s/60s+linkage+repeat`: as above, plus 10, 30 or 60 s time windows.

### `data/preprocessing_latency/`
| File | Columns | Paper item |
|---|---|---|
| `preprocessing_latency_summary.csv` | `condition, n_crops, repetitions, mean_ms, mean_ms_sd_reps, median_ms, median_ms_sd_reps, p95_ms, p95_ms_sd_reps, total_s_1600, total_s_sd_reps, median_overhead_vs_B1_ms, median_ratio_vs_B1` | Table 8 |

- **What was timed:** the preprocessing step only, per crop, in milliseconds, on one Apple M1 Pro machine.
- **Paths:** `A_melanin_path` and `A_common_path` split the Melanin-Aware reconstruction by the path each crop took.
